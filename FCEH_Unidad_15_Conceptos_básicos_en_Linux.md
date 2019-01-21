# FCEH_Unidad 15: Conceptos básicos en Linux



Tema muy importante dentro del mundo hacking, Linux. Voy a destacar algunas de las preguntas más frecuentes y que creo son importantes retener.

Lo primero y fundamental en Linux, es saber que son los repositorios, una de las muchas ventajas sobre otros sistemas operativos. Los repositorios son servidores de los que dispone cada distribución de Linux, son por lo tanto diferentes repositorios para Ubuntu, que para Debian, lo mismo sucede con Kali.

La lista de repositorios de Linux la podemos editar con cualquier editor de texto, por ejemplo con nao de la siguiente forma:

```
nano /etc/apt/sources.list
```

El archivo sources.list es el que contiene los repositorios. Estos pueden cambiar cada cierto tiempo, por lo que si vemos que nuestro sistema y aplicaciones no se actualizan, lo más correcto es acudir a la web oficial de la distribución que usemos y ver los repositorios más recientes. Si vamos por ejemplo a la de Kali, en este momento están los Kali-rolling, que es el siguiente:

```
deb http://http.kali.org/kali kali-rolling main contrib non-free
```

Hay muchos, pero siempre es recomendable usar el oficial. En el archivo sources.list, veremos otras líneas con la almohadilla (#) delante, esto quiere decir que esa línea está comentada, por lo que si ponemos la almohadilla delante del repositorio no nos actualizará.

El repositorio tiene una función básica, la actualización del sistema operativo y de las aplicaciones instaladas. Otra gran característica, es que mediante el comando apt-get install, podremos instalar infinidad de aplicaciones contenidas en estos repositorios sin necesidad de buscar en internet para descargarlas, como sucede en Windows por ejemplo.

Luego otro concepto importante es el kernel, la base de todo el sistema. Es importante mediante las actualizaciones tenerlo actualizado para una mejor integración del sistema con los dispositivos, aplicaciones, eliminar fallos de todo tipo, etc.

Para ver la versión de kernel que tenemos usamos el comando siguiente:

```bash
uname -r
```

Para saber cual es la más reciente en el mercado, hay una web que es la que se encarga de este tema a nivel mundial, es [https://www.kernel.org](https://www.kernel.org)

En esta web veremos la versión de prueba más actual, y también la versión llamada estable última. Normalmente las distribuciones Linux suelen ir actualizandose a estas versiones de kernel, aunque hay veces que tardan un poco.

Otro archivo muy útil es el de red, podemos editarlo con el comando nano:

```bash
nano /etc/network/interfaces
```

Si por ejemplo queremos poner una IP fija en Linux, podemos editar este archivo y poner por ejemplo abajo del todo lo siguiente (ejemplo con el eth0, si es para otro interface cambiarlo):

```bash
auto eth0

iface inet eth0 static

address 192.168.1.25

netmask 255.255.255.0

gateway 192.168.1.1
```

Salvamos y salimos. Para parar un interface y levantarlo, se usan los comandos ifdown eth0, y ifup eth0, aunque en virtualización no suele funcionar muy bien, por lo que es recomendable reiniciar la Kali.

Recordar que tenemos un comando imprescindible para ver que IP nos asigna: ifconfig. Si quisiera ver la puerta de enlace por ejemplo, podemos usar el comando:

```bash
route -n
```

Luego está el problema de conexión a internet desde la Kali. Lo primero siempre es ver que tengamos IP. Después hay que diferenciar en el problema si está en el tráfico IP o sólo en el DNS. Me explico. Si hago un ping (lanzar paquete de datos y esperar respuesta) a una IP pública de internet, por ejemplo de la siguiente forma:

```bash
ping 8.8.8.8
```

Puede pasar que responda o no. Esa IP es un DNS de Google. Si no responde el problema está en el interface de red o en la configuración de red. Si responde, pero no navega con Firefox, puede ser un problema de DNS. Para verificar hacemos un ping de nuevo, pero esta vez a un nombre DNS:

```bash
ping google.com
```

Si responde, el problema está en el navegador. Puede ser que tengamos un proxy activado, etc. Si no responde, el problema es ciertamente del DNS. Para ello podemos forzar servidores DNS. Aquí entra en juego otro archivo fundamental en Linux, el resolv.conf. Lo editamos:

```bash
nano /etc/resolv.conf
```

Si vemos que no hay DNS, debemos ponerlo. En ocasiones veremos que sale la IP del router, eso es porque es el router el que hace función de DNS en vuestra red. Si está vacío se ponen los que queramos, yo recomiendo los de Google. Se ponen por ejemplo en diferentes líeas de la siguiente forma, siendo los 2 primeros DNSs de Google y el tercero de Movistar:

```bash
nameserver 8.8.8.8

nameserver 8.8.4.4

nameserver 80.58.61.250

```

RC.LOCAL

En la Kali, el rc.local ha sido modificado. Aquí os indico como crear de nuevo un rc.local para no tener problemas con este tema:

1- Editar el siguiente archivo:

```bash
nano /etc/systemd/system/rc-local.service
```

2- Introducir el siguiente contenido en el archivo anterior:

```bash
[Unit]
Description=/etc/rc.local
ConditionPathExists=/etc/rc.local

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
StandardOutput=tty
RemainAfterExit=yes
SysVStartPriority=99

[Install]
WantedBy=multi-user.target
```

3- Crear el rc,local

```bash
nano /etc/rc.local
```
4- Introducir los siguiente:

```bash
#!/bin/sh -e
exit 0
```

5- Activar el rc.local y ponerlo de inicio con los siguientes comandos:

```bash
chmod +x /etc/rc.local
systemctl enable rc-local
systemctl start rc-local.service
systemctl status rc-local.service
cp /etc/rc.local /etc/init.d/rc.local

/etc/init.d/rc,local start
```

### Conceptos básicos:

Kali es una distribución de Debian, y tiene un entorno Gnome, con un montón de aplicaciones gratuitas como fillezilla para el FPT. Todas son de código abierto. 

Hay que diferenciar entre el nucleo (que es linux), y el GNU (que es el sistema operativo como tal), así que dependiendo del nucleo y GNU tendremos diferentes sistemas operativos. 

Respecto a entorno gráfico, tiene por defecto GNU, pero puede tener otro entorno gráfico como KDE. 

#### Escritorio

(**NOTA: En el curso se ha instalado una versión más antigua que la que hay actualmente, por lo que el entorno varía un poco, aunque en esencia es lo mismo** se recomienda investigar un poco la distribución de las opciones)

A la izquierda arriba,hay un menú donde podemos encontrar diferentes aplicaciones, y lo interesante es ir viendo un pococ como se distribuyen las aplicaciones

Al lado tenemos el menú *Lugares* donde tenemos equipo que es el equivalente a miPC, donde tenemos entre otras cosas el examinador de red.

A la izquierda un menú con iconos de las aplicaciones más comunes.

En la parte superior derecha, tenemos seleccions de idioma, grabación de pantalla, modo avion volumen, y *Red*. Entrando en Red, tenemos la configuración de red, qeu puede ser inalámbrica, cableada y una interesante parte que es la configuración de proxy, que nos da 3 opciones como método de configuración:

- Ninguno: No hay proxy.

- Manual: Seleccionamos los puertos manualmente.

- Automático: Podemos insertar la URL de un proxy web.

En la opción de red cableada podemos ver las diferentes opciones de configuración de la red cableada, que pude configurarse pulsando sobre la red en cuestión viendo un menú que nos da las siguientes opciones:

- Detalles: Datos de la red cableada

- Seguridad: Opciones de configuración de seguridad como encriptación.

- PIv4: que da opciones de configuración automática por DCHP, dando la dirección DNS del servidor, dirección, máscara de subred, puerta de enlace....O bien manual. Es similar a la configuración de un dispositivo de red en Windows.

- Otras opciones.

Dentro del menú que sale a la derecha superior, hay un icono con unas herramientas que equivale al antiguo menú de panel de control de windows, o lo que viene a ser opciones de configuración generales. Se llama *Todas las configuraciones*, donde tenemos usuarios, fondos de pantalla y demás.


### Aplicaciones:

Tenemos más de 300 aplicaciones por defecto para pentesting, y podemos ver muchas de ellas pulsando en el icono de cuadraditos que hay al final del menú de la izquierda.

![Kali desk](img/kali_desk.png)

Algunas poseen entorno gráfico como hermitage y otras tan solo de consola. 

### Istalar aplicaciones.

Una vez configurado el source.list, en el momento de querer instalar algún repositorio, pondremos en la consola tan solo el comando habitual:

```bash

apt-get install nombre-aplicacion
```

Podemos ver por ejemplo el nombre de nuestra máquina, en consola, ponemos

```bash
nano /etc/hostname
```

Y nos dice el nombre de la máquina y podemos cambiarlo también, para guardar se pone *Ctrl+o*, enter y *Ctrl+x* para salir de nano.

En el archivo host tenemos las direcciones del locakhost de nuestra máquina, así como la IP de nuestra maquina configurada, pra realizar purebas sobre esta máquina. Es la forma de enlazar nombres a direcciones.

![Kali desk](img/kali_desk2.png)

El archivo rc.local, nos permite poner comandos y aplicaciones que deseamos arrancar en el inicio de la máquina, como se ha explicado antes.

Editando el archivo que tenemos en */etc/fstab* podemos **montar** desde el inicio discos y particiones que tenemos disponibles.

### Equipo

Es la raíz del equipo, aquí podemos ver una serie de carpetas donde tenemos:

- bin: Comandos propios del sistema, 

- boot: Archivos de arranque como GRUB o el kernel que esté compilado. Como por ejemplo el grub.cfg que es el archivo que nos da las opciones de arranque ANTES de cargar el sistema en cuestión. 

- dev: Dispositivos del sistema, donde se monta todo. Pendrives, particiones de discos... etc.

- etc: Archivos de configuración del sistema, como todosl los archivos que hemos visto antes.

- home: Dependiendo de los usuarios que haya, crea una carpeta por usuario. que es lo que nos crea el menú que aparece en *lugares*

- lib: Bibliotecas del software que usa el sistema.

- var: tiene los logs del sistema.

- root: Tenemos las carpetas a las que tiene acceso root.

En caso de no saber donde está la papelera la tenemos dentro del explorador de archivos en la barra de la izquierda.