# FCEH_Unidad 19: Comandos básicos de Red en Windows & Linux


### Itroducción:

El más habitual es al ejecutar el comando nmblookup -M — -, donde no sale el mismo resultado que muestro en el vídeo. Esto es debido a que este comando consulta al NetBios, por lo que es preciso disponer de un sistema operativo arrancado con este protocolo, por ejemplo el Windows Server.

Otro posible problema que me he encontrado, es que la máquina con NetBios y desde la que se ejecuta el comando, están en un rango de IPs diferente.

Si por ejemplo tenemos una máquina con Adaptador Puente y la IP 192.168.1.25, y en otra NAT con la IP 10.0.2.15, es literalmente imposible que ambas máquinas se puedan ver. Es por eso que siempre recomiendo que todas las máquinas del laboratorio de pruebas tengan una única interface de red habilitada con la opción Adaptador Puente para obtener IPs del rango del router y el equipo anfitrión.

A los que uséis portátiles, recordar que en esta opción os pedirá que seleccionéis del desplegable la tarjeta de red a usar. Si vuestro equipo anfitrión conecta por la tarjeta WiFi y en el desplegable seleccionáis la tarjeta ethernet, no os funcionará correctamente. Recordar que estamos con virtualización, por lo que todo, incluidas las tarjetas de red, estarán virtualizadas.

### Comandos en Windows

Abrir menú de inicio den windows y con clicl secundario del ratón sobre CMD ejecutar como administrador, puesto que si no hay una serie de comandos que no se podrán ejecutar por los permisos.

- ping: manda paquetes por protocolos icmp a una máquina para comprobar que está levantada o no. Al hacer un ping nos da la ip, en caso de haber puesto una url (cisco.com, google.com....). Nos da los datos de los enviados, los recibidos y los perdidos. Lo habitual es que lleguen los 4. Se puede hacer un ping a la ip también. Si no tenemos la dirección de la wb podemos hacer *ping -a* y nos dice la url.
    - ping -n 8 cisco.com: con esto le decimos el númemro de pines que vamos a hacer a la url.

- ipconfig: Con este comando listamos los adaptadores de red disponibles así como sus direcciones IP.
    - ipconfig /all: Nos da las Ipv6 los servidores DNS primario y secundario, básicamente una información más detallada.
    En ambos casos nos da la DHCP, es importante, puesto que nos da la dirección del router o punto de acceso a la red de internet.

- nbtstat -n: Nos muestra la interfaz de red, con los nombres de los equipos que se encuentran en ella así como
sus IPs.

- netstat -a: estado de la conexion por los puertos

- netstat -s: muestra las estadisticas por cada uno de los protocolos IPv4, IPv6...

- netstat -r: muestra las tablas de ruta

- netstat -b: muestra los procesos asociados por puertos

- netstat -o: nos muestra el pid identificador del proceso o servicio

- route print: muestra todas las rutas

- route [change, delete, add]: para cambiar, borrar o añadir respectivamente (sin corchetes)

- nslookup: nos muestra la direccion dns primaria y nos permite introducirle una ip o una url, en caso de introducir una url nos va a devolver la ip que pertenece a esa url y viceversa. (Para salir de la aplicacion deberemos de escribir exit)

- nslookup -d [dominio]: nos enumera los distintos registros (archivos a nivel de servidor   )

- nslookup -a [dominio]: nos permite ver rango de direcciones ip ejemp: nslookup -a microsoft.com

- nslookup -type=MX [dominio]: nos muestra distintos servidores de correo electronico

- net user: nos muestra el nombre de usuarios que hay dentro de una red

- net share: nos muestra los recursos compartidos de una red y el directorio en el que se encuentra

- net user [user] [pass] /add: añade(crea) un usuario a la red

- net user [user] /delete: elimina el usuario introducido



### Comandos en linux

Los comandos de ping para linus es lo mismo con la diferencia de que linux no manda 4 paquetes, sino que hace ping hasta que se pare con *Ctrl + c*

En ved de ipconfig en linux tenemos *ifconfig*

- nmblookup -M -- -: muestra las ips de los equipos, donde la primera es la ip del anfitrión

- nmblookup -A [ip]: muestra el nombre del ordenador de la ip, dominio, nombre del grupo de trabajo etc...

- netstat: son los mismos comandos que los explicados anteriormente en windows

- netstat: -i: nos muestra la transmisión dentro de cada uno de los interfaces de red que tenemos

- route: vemos todas las tablas de rutas al igual que en windows

- nslookup: igual que en windows

- fping -g [ip red]/[mascara de sub-red] 2> /dev/null | grep alive: muestra equipos en la red y muestra los que respondan ejemp: fping -g 192.168.0.0/24 2> /dev/null | grep alive

- fping -g -s [ip red]: realiza pings a todos los ordenadores que estan en la red para comprobar cuales están respondiendo. Este proceso seguirá activo hasta que hagamos ctrl + c que finalizara el proceso y nos mostrará las estadisticas.
