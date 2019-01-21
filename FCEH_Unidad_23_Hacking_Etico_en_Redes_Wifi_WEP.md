# FCEH_Unidad 23: Hacking Ético en Redes Wifi WEP

Hola a todos. Sin duda aquí está el mayor conflicto de todos los temas de todos los cursos, la compatibilidad entre la virtualización y el interface WiFi.

Lo primero es explicar que no todas las tarjetas son compatibles, y muchas que si lo son dan problemas con la virtualización. Voy a indicar cómo solucionar este problema para la mayoría, pero muchos otros tendréis que recurrir a saltarse la virtualización para realizar la práctica. Cuando hablo de realizar la práctica, me refiero a que lo practiquéis, el ejercicio consta de 2 partes y a todos aquellos que tenéis problemas os califico sobre la otra parte, así que por eso no os preocupéis.

La forma de que funcione seguro, suponiendo que vuestra tarjeta es compatible, es crear un DVD o Pendrive en modo Live con la Kali. Hay mucha información en internet, pero básicamente es usar una aplicación para generar un Pendrive auto arrancable, yo suelo usar Rufus. Es simplemente poner la ISO de la Kali y generar el modo de arranque con la aplicación.

Una vez la tenemos, reiniciamos el equipo desde el Pendrive y nos saltará la Kali, debemos marcar la primera opción, el modo LIVE (nunca instalar). Con esto cargaremos la Kali en nuestro equipo sin necesidad de instalarla, eso sí, es un sistema volátil, por lo que todo lo que guardemos se eliminará una vez reiniciemos.

Con esto si hacemos un iwconfig casi seguro que saldrá la wlan0, ya os digo que el problema no es de Linux, es de la virtualización, y así, aunque no me mandéis este ejercicio, al menos podréis realizar la práctica para aprender.

Ahora vamos a intentar que el WiFi funcione virtualizado, pero si véis que os da muchos problemas ya os digo que lo mejor es usar el LivePen.

Para que el VirtualBox reconozca el wlan0, lo primero es verificar que en la configuración de red, esté puesto como primer interface la opción Adaptador Puente y en el desplegable esté selecciona la tarjeta Wifi.

También es necesario que las Guest Additions estén instaladas correctamente o no se generará el interface virtual Wifi. Para ello hay que ver que el sistema esté totalmente actualizado con el comando uname –r y ver que disponemos de una versión actualizada.

Para actualizar el kernel esté actualizado, los repositorios que debe tener en el /etc/sources.list son al menos estos:

deb http://http.kali.org/kali kali-rolling main contrib non-free
deb-src http://http.kali.org/kali kali-rolling main contrib non-free

Si no tiene el kernel actualizado, debe actualizar el sistema, para ello están los siguientes comandos:

apt-get update para actualizar los repositorios

apt-get upgrade para actualizar el sistema y aplicaciones

apt-get dist-upgrade para actualizar la versión

apt-get install linux-headers-$(uname -r) para actualizar las cabeceras

Una vez esté actualizado, puede ver de nuevo con uname -r que tiene la versión actual  y ya si instala las Guest Additions como se muestra en el vídeo no le darán fallo.

Si una vez realizados estos pasos sigue sin aparecerle el wlan0, hay sistemas que requieren de las Extension Pack, para ello hay que descargarlas desde:

https://www.virtualbox.org/wiki/Downloads

Es el enlace en el que pone Oracle VM VirtualBox Extension Pack, en All supported platforms.

Una vez descargadas, se accede al VirtualBox en Archivo, Preferencias, Extensiones y damos al botón de la derecha para añadir una nueva extensión y le indicamos el archivo descargado.

Después hay otros chipset de tarjetas Wifi que precisan de unos drivers concretos para habilitar el modo monitor, una opción sería descargarlos de la web oficial e instalarlos. Adicionalmente en Linux tenemos unos comandos para ver si el sistema detecta un dispositivo, lsusb para los USB y lspci para los dispositivos integrados, si el driver está instalado debería aparecerle su tarjeta wifi.

Si su tarjeta WiFi es USB, abajo a la derecha, dentro de lo que es la pantalla de VBox de la Kali, verá un icono de un Pendrive, debe marcarlo para que la tarjeta USB se asocie a la Kali, no al equipo anfirión.

### Problemas con el reconocimiento de la tarjeta de red

Cuando virtualizamos máquinas, es muy probable que tengamos ciertos problemas tanto para que se nos reconozcan los usb como las tarjetas de red. Para ello ha de instalarse como se comenta las *Extension Pack* pero creando un usuario nuevo, seguir los siguientes pasos que podemos ver en el siguiente foro, o directamente y más sencillo arrancar un live USB con kali.

**Recursos**: Instrucciones [aquí]() leer todo el hilo. 

 ### Protocolo WEP

 Es el más sencillo de todos. Lo primero que hacemos es un *ifconfig*

 De los datos que nos da, la que nos interesa es la wlan0, si tenemos varias tarjetas de red wifi, saldrán más.
 Si queremos saber más datos sobre la wifi ponemos iwconfig. Te muestra si hay extensiones wifi, es decir, nos muestra cúales de nuestras conexiones son wifi.

A continuación realizar los siguientes comandos:

```bash
  ifconfig
  iwconfig
  ifconfig wlan0 up
  airmon-ng start wlan0
  # no me deja poner la tarjeta en modo monitor, puesto que hay una serie de procesos ejecutandose
  # Los matamos y ya podemos poner la tarjeta en modo monitor. Imagnemos que nos da estos tres procesos que matamos a continuación:
  kill 467
  kill 523
  kill 524
  airmon-ng start wlan0
  iwconfig
  #nos pone el modo promiscuo de la tarjeta. Es decir, la pone en modo monitor (escucha)
```

Luego poner:

```bash
airodump-ng wlan0mon
```
Esto empieza a escuchar que paquetes están pasando por las redes que capte la tarjeta.

En la pantalla que sale tenemos algo similar a esto:

![Escuchando redes](img/wifi1.png)

El BSSID es la mac del punto de acceso

Imaginemos que deseamos escuchar a una red en concreto, abrimos otra consola paa poder tomar los datos de la primera, y pondremos lo siguiente:

```bash
airodump-ng wlan0mon -w <ESSID de la red> -c <nº de canal>
```

Tras esto abrimos otra consola más, y en esta ejecutamos un ls (tengamos en cuenta que todo esto se ha hecho en la carpeta raiz de root en el video, pero podemos realizarlo en una carpeta determinada, puesto que airodump nos genera unos archivos que almacenan los datos que ha ido captando. Tomamos el que tiene extensión .cap).

Puesto que puede ir creando más archivos usaremos un *:

```bash
aircrack-ng <nombre_archivo*>.cap
```

Si tenemos los suficientes datos acumulados (unos 5000IVs) encontrará la contraseña y nos la dará en ASCII y en hexadecimal.