# FCEH_Unidad 1: Presentación

Contenidos del *First Certificatiosn in Ethical Hacking* (FCEH):

- Tipos de ataques
- Conceptos hacking
- Máquinas Virtuales (VM)
- Virtualización de sistemas operativos
- Introducción a Linux
- Comandos de red
- Comandos Linux básicos
- Sistemas de ocultamiento
- Auditar y Hackear redes Wifi
- Hackear Redes Sociales
- Ataques MITM

### Tipos de ataques:

**Pasivos**:

El atacante observa sin alterar las comunicaciones

**Activos**:

El atacante altera las comunicaciones (suplantación de identidad, reactuación, modificación y degradación).


#### ATAQUES:

  - Spoofing: (ARN, DNS, WEB SPOOFING, IP SPOOFIN): Envenena el tráfico, como por ejemplo con el ataque man in the middle

  - Ingenieria social: Engaña a la paersona con fin a obtener acceso a la red, datos, contraseñas, accesos...

  - Scanners: Busqued de vulnerabilidades, puertos web, ip...

  - Sniffings: Se usa una apll o dispo para  interceptar comuni para pasar el trafico de red por un punto

  - Data corruption: altera la información 

  - XSS: Cross Side Scripting, se verá más adelante, el intruso aprovecha vulnerabilidades para secuestrar un site por ejemplo

  - Pharming: Ataca servidores de nombre o dns para redirigir el trafico a una pag web, donde se aloja un malware para infectar a las victimas

  - SQL In yection: Se altera una bbdd aprovechando una vulnerabilidad d la programación de ésta, de forma queinyectando un código de sql se obtine acceso a la BBDD, se puede modificar o incluso obtener la BBDD entera.

  - Fuerza bruta: Consiste en teniendo un usuario dar un número enorme de contraseñas hasta que alguna haga match.

  - Phising: Se envía un mail en nombre de altuna entidad, con un enlace, que redirige a una página que aparentemente es oficial de la entidad, solicitando usuario y contraseña, cuando en realidad estas se almacenan en la BBDD del hacker

  - DoS o DDoS: Ataques de denegación de servicio o denegaciónd e servicio disribuido, se puede realizar desde un dispositivo o varios, se hacen peticiones a un servidor de forma quese colapsa por el overflow.

  - Keylogers: Registran cada pulsación de teclado y envía un mail al atacante, pudiéndose realizar hasta pantallazos de lo que la víctima hace en su pc

  - Exploiting: Tecnica de ataque por exploit que es un codigo que aprovecha una vulnerabiidad concreta de un software. Cmo por ejemplo jtomar control remto de la mákina.

  - Zero Day: Tipo de ataque por exploit que ha sido creado recientemente y no se ha solventado aun, y no hay remedio en el momento del ataque

  - MITM: Man in the middle, se envena la máscara de RP y la DNS o IP, etc.

### Tipos de auditoría:

BLACK-BOX: No hay datos realmente más allá del nombre de la empresa la if de red o dominio ()acceso público)

GREY: Datos de la infraestructura a auditar

WHITE: Se da información cmopleta.

### Tipos de seguridad:

- Seguridad físca: Todo lo físic, un swithc, un candado , cámaras, un guardia.

- Seguridad lógica: Software dedicado a seguridad, honeypot, falsos equipos virtuales.


### Conceptos:

- Spoofing: (ARN, DNS, WEB SPOOFING, IP SPOOFIN): Envenena el tráfico, como por ejemplo con el ataque man in the middle, Se envenena el tráfico, lo que se hace es hacer pensar a la victima que somos el destino, y al destino que somos la víctima. Se puede falsear la tabla RP para queel trafico pase por nosotros

- Bindear: Se trata de adjuntar un virus a un archivo, por ejemplo una foto o PDF, y ocultarlo dentro de él. 

- Scanners: Hay de diferentes tipos, como por ejemplo scaner de puertos con NMAP.

- SQL Inyection: Cosiste en generar un código de SQL, que al conectar con la BBDD estrae la información que deseamos.

- Cifrado: Con el cifrado se altera un texto plano y que para poder acceder a el original se precisa de una contraseña. 

- Gathering: Reunión o recolecta de información, es el proceso que se realiza por un hcacker antes de realizar ningún ataque, para saber que vulnerabilidades existen.

- Hardering: Securizar un sistema, puede ser físico o a través de software.

- Shell: Interfaz de comandos.

- Keyloggers: App que se usa para poder monitorizar lo que la víctima teclea o hace con su PC

- Esnifar: Abrir un flag o bit de la targeta de red, y ponerla en modo promiscuo o modo monitor, de forma queel tráfico de la red llega a nosotros, haciendo pensar al firewall o router que nosotros somos el destino.

- BotNet: Red de ordenadores infectados para lanzar span masivo o realizar un DDoS.

- Malware: Codigo malicioso que tiene como objetivo dañar el ordenador de la víctima, abrir un backdor por ejemplo tb para tomar el control de la máquina.

- Spyware: Software que sirve para recopilar información de la víctima.

- Exploit: Codigos de programación en Python o Ruby que explotan una vulnerabilidad muy concreta de un software

- Metadatos: Datos sobre los datos, es una información oculta que se encuentra dentro de un archivo, y que da información sobre ese archivo.

- Footprinting: Recopilar información para realizar un ataque, puede ser activo o pasivo.


### Sistemas de defensa:

- IDS/IPS: 
    - IDS -> Detectores de intrusos. 
    - IPS -> Detectores de intrusos que tienen proactividad, y toma acciones contra ese ataque.

- Proactividad: Sistema que necesita de personal como un técnico de seguridad informática en la empresa, acciones para prevenir son acciones proactivas. 

- Firewall, Antivirus, Antimalware: Sistemas de defensa que mitigan los accesos y robos de información. Son los más habituales.

- Honeypots: Creación de falsas máquinas por ejemplo, que despistan al hacker o ataqcante, esot botes de miel que atraen las moscas, para despistarlas y hacerlas perder tiempo mientras la defensa lo gana.

- GPOs: Politicas de grupo configuradas en el directorio activo, como por ejemplo tiempo de cambio de contraseñas.

- DMZ: Zona desmilitarizada, o falsa red, que protegen la red real.

- Proxy: Aplicaión o servidor dedicado a controlar el tráfico que hay en una red al exterior. 

- Criptografía: Sistema que estudia sistemas criptográficos o de cifrado.
