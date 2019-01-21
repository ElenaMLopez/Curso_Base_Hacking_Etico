# Unidad_5_Conceptos_basicos_de_Redes.md

### Conceptos básicos:

- MAC: Dirección que se presenta en dígitos exadecimales (de 0 a 9 y con las letras de la A a la Z), separados por parejas con dos puntos:
```50:56:bf:23:8b:a7 ```

Dependiendo de los números de la MAC se puede saber el fabricante, puesto que todas las targetas de red fabricadas tienen su MAC propia, de forma que los primeros dígitos nos dan por ejemplo el fabricante. A traves de esta dirección se puede localizar una targeta concreta, por lo que habitualmente los hackers suelen cambiar su MAC para protegerse y no dejar rastro. 

- IP: La dirección IP, puede ser de dos tipos, y siempre tenemos estas dos direcciones en nuestro ordenador:
  - Publica: La IP pública es la dirección de nuestra máquina dentro de internet. Dan información por ejemplo del país desde el que se accede, el proovedor etc, pueden comenzar por cualquier dígito. Por ejemplo ```80.90.128.23``` donde el rango de los dos primeros nos da por ejemplo el país y el proovedor, que ha comprado un rango o pool de direcciones para ofrecer servicio. 
  - Privada: Suele comenzar con un rango ```192.168.0.nº``` donde el número final puede ser de 0 a 255. Esta es la dirección de nuestra máquina en la red que está por detras del router que da acceso a internet.

- Máscara: A parte de la IP de la red, tenemos una máscara de subred que suele ser ```255.255.255.0``` lo que hace que nos da el número máximo de equipos que se vana a conectar en nuestra red. Por ejemplo con una mascara de subred que fuera ```255.255.0.0``` tendríamos un rango de red mucho mayor, puesto que nos daría direcciones IP desde la

 ```192.168.(0-255).(0-255)```
 Ejemplo de clases de direcciones ip:

 ![clases de ip](img/clases_direcciones_ip.gif)

- Broadcast: Dirección por defecto que es la última dentro del rango que la máscara de surbred provee, las peticiones se envían a través del router que al ser devuelta solicita al broadcast la IP del equipo ha solicitado la petición, es el que se encarga de gestionar las respuestas del router. Este boradcast envía la petición a todos los equipos de la red para saber cual de ellos ha solicitado la información. 

- Gateway: Puerta de enlace, es la IP del router y por defecto suele ser ```192.168.1.1``` y es la IP a la que deben apuntar todos los ordenadores de la red. Puede cambiarse si se desea. Es el que hace la transición de la red local a internet, sea a traves de protocolos como el NAT, Bridge. 

- DNS: Servidores DNS son de dos tipos:

    - Privado: ```192.168.1.20``` Son servidores q ponemos dentro de nuestra red, en donde ponemos las consultas de DNS internas para los equipos de nuestra red privada. Suele configurarse en un servidor. 

    - Público: ```80.58.61.250/8.8.8.8``` Es el que usamos habitualmente, son unas direcciones IP de unos servidores encargados de proveer las IP de las URL's que insertamos en el navegador, son ese directorio de IP que se encuentran en unas tablas que tienen, de forma que no necesitamos conocer las IP de la página de google por ejemplo.

- Puerto: 

- Directorio Activo: (el cerebro de la red). Son un servidor, con windows server por ejemplo, permite el control del dominio con las siguientes características:
    - *Autentificación de usuarios de red*: permite que un usuario acceda a una red, con LDAP por ejemplo, que es un tipo de autentificación (usuario pasword), esto se puede insertar en un dominio y lo controla el directorio activo
    - *Políticas de grupo*: Por ejemplo que las contraseñas tengan mínimo n caracteres.
    - *Control de logs de registro*: Controlan quien se conecta y accede a sevicios compartidos, así como los fallos de conexión
    - *Organiza la informacíon de red*: Permite tener un arbol de carpetas y dar permisos de acceso a diferentes roles de usuarios.

- DHCP: Es un protocolo de configuración dinámica de host. Es un protocolo de red tipo cliente/servidor, mediante el cual un servidor DCHP asigna IP's. Tenemos tres tipos: 
    - DCHP Estático: Asigna siempre la misma IP a cada máquina. 
    - DCHP Dinámico: El equipo tiene una dirección IP cada vez que se conecta
    - DCHP Mixto: Usa el DCHP dinámico pero se reserva un rando de IP para diferentes máquinas.

- Tabla ARP: 
- Enrutamiento:
- ACL: Access Control List (listas de control de acceso), son tablas donde se dice que tipo de tráfico hace el qué, esto es muy típoco de un firewall por ejemplo, donde se determina que tipo de tráfico va a donde, por ejemplo el tráfico de un puerto en concreto sólo va a un ordenador concreto de la red. Lo encontramos 
    - Routers / Switchs
    - Firewall/Bastiones
    - Proxy Server
    - Equipos mediante creación de rutas.

- Host:
- Roles: Personajes virtuales, que tienen unos papeles determinados dentro del funcionamiento de la red
    - NTP: Servidor de hora, que busca en internet la franja horaria que hemos determinado. Este servicio es muy importante y podemos configurar un servidor windows server por ejemplo, puesto que para poder autentificarse mediante KERBEROS y por defecto, si hay una diferencia horaria de más de 5 minutos, aunque tengamos usuario administrador con user y password, no vamos a poder autentificar. Lo que se puede hacer es configurar este tiempo por defecto a 2 o 3 minutos y decirle a la red que en realidad su hora es 5 minutos más que la que viene por defecto, de forma que un usuario externo a la red y que no sepa de esta configuración, no podrá acceder aunque tenga las credenciales de Admin.
    - Controlador de Dominio: Es el cerebro de la red y que genera el directorio activo.
    - DNS Server, DHCP: Al crear un controlador de dominio nos va a pedir que tengamos estos servidores activos.
    - DFS, Backups: DFS es una forma de estructurar la información de la red, repartiéndola en direntes discos duros y distribuyendo todos los archivos, y los backups que son para guardar copias de seguridad.
    - Proxy server: aplicación q esta entre los ordenadores y la red, para poder dar acceso a internet.
    - Web Server, intranet: Alberga servicos web (CRM, Paginas WEB, ...), mientras que la intranet es un portal web para la red interna, al que se puede acceder desde la propia red o desde el exterior con una VPN por ejemplo.

### Protocolos Base:

#### TCP:

- Inicia y finaliza la comunicacón entre los equipos antes de transmitir el mensaje. Las comunicaciones suele realizarse a través del protocolo TCP/IP, y aunque es más lento que otros protocolos es más seguro, puesto que va haciendo autentificaciones.
- Los mensajes llegan de forma ordenada y sin duplicados.
- Es fiable a la hora de saber que el mensaje llega a su destino.

#### UDP:

Es mucho más rápido pero menos seguro:

- Comunicación sencilla entre aplicaciones. 
- Sin establecimiento de conexión previa entre dos equipos, envía el mensaje directamente pudiendo este duplicarse, llegar desordenado, perderse, o ser dañados.
- Incorpora puertos de origen y destino en sus mensajes. 

#### ICMP:

- Protocolo de mensajes de control y error.
- Informa al origen si se producen errores en la entrega del mensaje
- Protocolo informativo.

Por ejemplo cuando se realiza un *ping* a una IP, se realiza a través de este protocolo.

### Puertos de red:

Mirando la siguiente imagen podemos ver los más comunes. Los más importantes son HTTP, DNS, SSL...

![puertos](img/puertos.png)

- HTTP(80): Puerto por defecto para páginas web
- DNS(53): Puerto que permite cambiar la IP por url de web y viceversa.
- SSL(443): Puerto de protocolo SSL, a traves del cual podemos ver las páginas con url *https*, para acceder con un certificado digital que da una encriptación a las comunicaciones a traves de este puerto.
- POP3(110): Es el puerto a través del que se escuha la recepción de correo electrónico, es el encargado de la recepción.
- SMTP(25): Es el puerto encargado de enviar el correo electrónico
- IMAP(143): Recepción de las cabeceras de los correos electrónicos.
- IRC(194): Puerto de entrada de chat.
- FTP(21): Trasnmisión y recepción de paquetes a traves de servidores FTP (lo que antiguamente se usaba para subir archivos de páginas web al hosting)
- TELNET(23): Puerto de conexión con equipos remotos
- SNMP(161): Protocolo y puerto de conexión a administradores de red, que permite la monitorización y gestión de la red, que equipos están conectados, ver si hay fallos, etc.
- NTP(123): Servidor de hora.
- SSH(22): Puerto que permite tener comunicaciones internas dentro de la red de forma segura.
- NetBios-ns(137): Servicio que da acceso a la red, a diferentes aplicaciones y que asigna un nombre a cada ordenador de una red.
- RPC(530): Permite ejecutar aplicaciones en un ordenador remoto. Se usan tambien en aplicaciones cliente/servidor.
