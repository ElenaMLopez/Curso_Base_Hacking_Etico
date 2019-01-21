# FCEH_Unidad 20: Técnicas de ocultamiento. 1ª Parte

Todo lo que se trabaja en esta unidad, se realiza con Kali linux.

Dentro de las actividades delictivas, lo básico es ocultar tu identidad, y esto lo hacen todos los hackers. Lo básico para ocultar es la direccion IP y la MAC de la targeta de red, puesto que cada targeta tiene uns IP propia a nivel mundial.

### Adivinar cual es nuestra IP y MAC

Podemos montar un proxy server para ocultar nuestra identidad, de hecho muy comunmente usuarios se conectan a aplicaciones online, o descargar alguna aplicación como multiproxy.

Hacemos un *ifcofig* y vemos las direcciones red de los adaptadores de red que tenemos (MAC), para cambiar la dirección MAC en una maquina virtual, estando apagada en el menú lateral/red podemos cambiar la mac dando al botón de acualizar que tiene al lado.

Si deseamos hacerlo con la máquina encendida, o bien en un host del sistema operativo, utilizaremos el siguiente comando:
```bash
 macchanger -A [interfaz a cambiar] 
# Por ejemplo:
# macchanger -A eth1
```

Después de esto al hacer un ifconfig podemos ver cómo ha cambiado la mac. Al lado del las mac que vamos cambiando aparecen diferentes fabricantes de red, puesto que según la marca aparecen por defecto los primeros dígitos, que son los rangos de direcciones MAC que la marca ha comprado.

Podemos asignar una IP determinada con 
```bash
 macchanger -m [mac nueva en hexadecimal] [interfaz]
# Por ejemplo:
# macchanger -m 22:33:44:ad:bf:fa eth1
```
Hay que tener en cuenta que los números son del 0-9 y las letras de la A a la F

De esta forma se asigna esta MAc pero si esto lo hacemos usando una interfaz de red nos va a dar problemas, por lo que antes de cambiar la MAC debemos apagar esta interfaz en uso:

```bash
ifconfig [interfaz de red] down
# Por ememplo:
#ifconfig eth1 down
```
El cambio, y luego levantamos de nuevo la interfaz :

```bash
ifcongif [interfaz de red] up
# Por ejemplo
# ifcongif eth1 up
```

Con esto estamos cambiando la MAC de nuestro adaptador de red deseado (interfaz de red) con la consola.

### Privacidad con TOR

Buscar el navegador Tor y descargarlo desde su página oficial [Tor Project](https://www.torproject.org/projects/torbrowser.html) y descargar la versión para linux

Una vez descargado seguir los siguientes pasos:

1. Abrir la carpeta raiz de tor-browser_es-ES

2. Entrar en la carpeta Browser

3. Abrir el archivo start-tor-browser y buscar la palabra *root*

4. Editar el archivo de la siguiente forma:

```bash
#if [ "`id -u`" -eq 0 ]; then
    complain "Tor Browser Bundle should not be run as root. Exiting"
    #exit 1
#fi
```
    Es decir, comentamos el if del archivo. Guardamos y salimos. Con esto evitamos que al intentar ejecutar Tor nos de un error si somos el uruario root

5. Una vez echo esto, podemos ir a la raiz y hacer doble clic en el icono. En caso de que haya un problema, podemos ejecutar el comando directamente desde la consola con el comando 

```bash
./start-tor-browser.desktop
```

    Pueden seguise las instrucciones del la página oficial tambien:

>Download the architecture-appropriate file above, save it somewhere, then run one of the following two commands to extract the package archive:

```bash
tar -xvJf tor-browser-linux32-8.0.4_LANG.tar.xz

# or (for the 64-bit version):

tar -xvJf tor-browser-linux64-8.0.4_LANG.tar.xz
```

>(where LANG is the language listed in the filename).

>Once that's done, switch to the Tor browser directory by running:

```bash
cd tor-browser_LANG
```

>(where LANG is the language listed in the filename).

>To run Tor Browser, click either on the Tor Browser or the Tor Browser Setup icon or execute the start-tor-browser.desktop file in a terminal:

```bash
./start-tor-browser.desktop
```

> **This will launch Tor Launcher and once that connects to Tor, it will launch Firefox. Do not unpack or run TBB as root.**

Hay unos sistemas operativos especializados en temas de privacidad. Los más conocidos son:

- Tails
- Whonix
- Ipredia
- Privatix.

De ellos el mas conocido es Tails. Privatix tiene la ventaja de que sólo puede ejecutarser como un live USB.

#### Trabajando con Tor Browser:

Tor browser tiene muchas ventajas, para resumir podemos decir que lo que hace al torificar la cominicación es poner capas de seguridad (por eso lo de la cebolla) y redirige nuestro tráfico a traves de una serie de servidores, encriptado sin que realmente estos servidores puedan saber el origen real de esta conexión, tan sólo saben a donde tienen que mandar la petición. Con cada servidor se añade una capa de seguridad a la transmisión. 

Lo que ocurre es que si utilizamos servicios como por ejemplo twitter o páginas con login, la seguridad queda comprometida, así que si se van a visitar ciertas páginas de internet **NO DEBE** usarse Tor. La lista la podemos ver aquí:
```

Acciones que debemos evitar siempre que nos conectemos a la red Tor
Nunca debemos acceder a nuestra página web desde la red Tor. Si nuestra página web tiene pocas visitas y no se encuentra dentro de la red distribuida, el relay de salida puede identificarnos como el administrador de la web.

No debemos iniciar sesión en Facebook, Twitter y cualquier otra plataforma personal (redes sociales, correo electrónico, etc). Existen muchas técnicas que se pueden llevar a cabo para identificarnos en el momento que iniciamos sesión en una red social o plataforma personal. De igual forma, es posible incluso que los responsables de los relays de salida capturen los paquetes de inicio de sesión y puedan llegar incluso a suplantar nuestra identidad. Tampoco debemos entrar en webs comerciales como Amazon, eBay, PayPal o nuestra cuenta del banco ya que, además de lo anterior, es posible incluso que nos suspendan la cuenta.

Debemos evitar alternar entre la red Tor y Wi-Fi abierto. Siempre debemos utilizar ambos elementos a la vez ya que, de lo contrario, puede que identifiquen nuestra MAC con la actividad en la red anónima y distribuida.

No debemos utilizar Tor sobre Tor, es decir, con una sola entrada y salida a la red anónima y distribuida es suficiente. Aplicar una doble entrada y una doble salida, además de no mejorar la privacidad, puede dar lugar a graves fallos de seguridad.

Debemos asegurarnos de enviar la información privada de forma segura y cifrada, es decir, utilizar correctamente el navegador conectado a la red y un complemento como HTTPS Everywhere que nos asegure que toda la información viaja de forma segura.

Debemos evitar el uso de información personal dentro de la red Tor, por ejemplo, nombres, apodos, lugar de nacimiento, fechas, etc.

Si es posible, es recomendable evitar el uso de Bridges (Relays de la red Tor no listados para evitar que los ISP los bloqueen).

No es recomendable utilizar diferentes identidades, ya que prácticamente siempre es posible que ambas estén relacionadas.

Nunca debemos editar la configuración de seguridad que configuran por defecto las herramientas que nos permiten el acceso a la red Tor, salvo que sepamos exactamente lo que estamos haciendo. De hacerlo, es muy probable que estemos reduciendo drásticamente el nivel de seguridad, por ejemplo, permitiendo el rastreo de actividad.

No debemos utilizar al mismo tiempo Tor y una conexión directa a Internet ya que, de hacerlo, es posible que en alguna ocasión nos equivoquemos con la salida y enviemos ciertos datos por la red que no es. Cada cosa a su tiempo, y de una en una. Lo mismo se aplica a las conexiones con servidores remotos.

Anonimato no es lo mismo que seudónimo. Anonimato es no existir. Seudónimo es un nombre secundario asociado a nosotros.

Si creamos una red dentro de la red Tor no debemos facilitar el enlace en las redes sociales.

Nunca debemos abrir un archivo recibido desde la red Tor, ya que probablemente tenga un virus o malware que infecte nuestro ordenador. Especialmente los archivos PDF.

En la red Tor debemos evitar el uso de sistemas de doble autenticación, ya que por lo general estos están asociados a un teléfono, a una SIM, y es posible que las autoridades nos identifiquen en cuestión de segundos.

Siguiendo estas pautas no deberíamos tener problemas al conectarnos a esta red anónima y distribuida y garantizar así tanto nuestra privacidad como nuestro anonimato.
```
Arrancamos Tor y comprobamos nuestra IP desde la página de [cúal es mi IP](http://www.cualesmiip.com/) o bien con google poniendo *my IP* en las búsquedas.

Tenemos un icono al lado de las direcciones del navegador con una cebolla. Pulsando ahí, podemos configurar una nueva identidad:

![Nueva identidad](img/tor.png)

Nos pedirá reiniciar Tor y dejamos marcada la casilla de no preguntar de nuevo. Reiniciamos y ya estaremos navegando con una nueva identidad dentro de la red tor. Una vez echo esto podemos volver a [comprobar nuestra dirección IP](http://www.cualesmiip.com/) y veremos que ésta ha cambiado.

Este menú *Cebolla* es muy importante, puesto que podemos configurar el nivel de seguridad de las funciones del navegador, por defecto nos trae ya algunas como el JS deshabilitado.

### Deep Web:

El internet que nos ofrencen los navegadores habituales es el 10% de internet. Esto es así porque el 90% de internet en realidad tiene contenido ilegal o que no interesa que se conoczca, como opiniones políticas de personas que no se desean que sean conocidas. 

Pero hay que tener cuidado, puesto de dentro de la Deep Web tenemos una gran cantidad de estafas. La moneda de cambio suele ser bitcoins.

## ATENCION NO NAVEGUES A ESTAS WEBS SI NO ESTAS EN TOR Y HAS CAMBIADO TU IP!!!!

Dentro de la página web de [http://deepweblinks.org/](http://deepweblinks.org/) podemos encontrar un listado de páginas dentro de la Deep Web con los servicios que ofrecen. Este listado suele variar bastante, puesto que al ser actividades delictivas, en el momento en el que se encuentra y cierra el servidor cambian el dominio:

Ejemplos:


To browse .onion Deep Web links, install Tor Browser from http://torproject.org/

 
Hidden Service lists and search engines
http://3g2upl4pq6kufc4m.onion/ – DuckDuckGo Search Engine

http://xmh57jrzrnw6insl.onion/ – TORCH – Tor Search Engine

http://zqktlwi4fecvo6ri.onion/wiki/index.php/Main_Page – Uncensored Hidden Wiki

http://32rfckwuorlf4dlv.onion/ – Onion URL Repository

http://e266al32vpuorbyg.onion/bookmarks.php – Dark Nexus

http://5plvrsgydwy2sgce.onion/ – Seeks Search

http://2vlqpcqpjlhmd5r2.onion/ – Gateway to Freenet

http://nlmymchrmnlmbnii.onion/ – Is It Up?

http://kpynyvym6xqi7wz2.onion/links.html – ParaZite

http://wiki5kauuihowqi5.onion/ – Onion Wiki

http://kpvz7ki2v5agwt35.onion – The Hidden Wiki

http://idnxcnkne4qt76tg.onion/ – Tor Project: Anonymity Online

http://torlinkbgs6aabns.onion/ – TorLinks

http://jh32yv5zgayyyts3.onion/ – Hidden Wiki .Onion Urls

http://wikitjerrta4qgz4.onion/ – Hidden Wiki – Tor Wiki

http://xdagknwjc7aaytzh.onion/ – Anonet Webproxy

http://3fyb44wdhnd2ghhl.onion/wiki/index.php?title=Main_Page – All You’re Wiki – clone of the clean hidden wiki 
that went down with freedom hosting

http://3fyb44wdhnd2ghhl.onion/ – All You’re Base

http://j6im4v42ur6dpic3.onion/ – TorProject Archive

http://p3igkncehackjtib.onion/ – TorProject Media

http://kbhpodhnfxl3clb4.onion – Tor Search

http://cipollatnumrrahd.onion/ – Cipolla 2.0 (Italian)

http://dppmfxaacucguzpc.onion/ – TorDir – One of the oldest link lists on Tor
Marketplace Financial

http://torbrokerge7zxgq.onion/ – TorBroker – Trade securities anonymously with bitcoin, currently supports 
nearly 1000 stocks and ETFs

http://fogcore5n3ov3tui.onion/ – Bitcoin Fog – Bitcoin Laundry

http://2vx63nyktk4kxbxb.onion/ – AUTOMATED PAYPAL AND CREDIT CARD STORE

http://samsgdtwz6hvjyu4.onion – Safe, Anonymous, Fast, Easy escrow service.

http://easycoinsayj7p5l.onion/ – EasyCoin – Bitcoin Wallet with free Bitcoin Mixer

http://jzn5w5pac26sqef4.onion/ – WeBuyBitcoins – Sell your Bitcoins for Cash (USD), ACH, WU/MG, LR, PayPal and 
more

http://ow24et3tetp6tvmk.onion/ – OnionWallet – Anonymous Bit

... Y muchas más...

Como podemos ver las direcciones de Tor no son como las habituales direcciones de internet, puesto que los dominios tienen extensión *.onion* y el dominio se asigna automáticamente con letras y números.

![Ejemplo de WEB](img/tor3.png)