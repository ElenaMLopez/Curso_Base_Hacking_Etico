# FCEH_Unidad 12: Instalación Debian


Ante los problemas más comunes con la instalación de Debian, dejo las principales soluciones:

1- Ver si su sistema anfitrión es de 32 ó 64 bits. Una vez visto esto, usar sistemas virtualizados de la misma arquitectura. En la plataforma se han subido los de 32 bits por ser los más complicados de encontrar. Si su equipo es de 64 bits, descargue mejor la Debian de la web oficial, así además estará actualizada.
2- Mire que en Sistema, Procesador, dentro de la configuración de la máquina en VBox tenga marcada la casilla PAE/NX. Esto debería marcarse en todos los Linux por temas de compatibilidad con el microprocesador.
3- Si su sistema es de 64 bits, cuando instala una máquina virtual, le deja instalarlas de 32 y 64 bits, o sólo de 32? A los que sólo os deja de 32 bits, es porque tenéis deshabilitada la virtualización en la BIOS. Es simplemente acceder a la BIOS o SETUP del equipo anfitrión, y habilitar en opciones avanzadas la Intel virtualization, VT-x, o similar, dependiendo de vuestra BIOS.

Si una vez arrancada la Debian le aparece para que introduzca el login, es porque durante la instalación no ha puesto el entorno gráfico, o bien porque cuando intenta descargar paquetes de internet no dispone de conexión a internet en la máquina virtual. Si es así, es recomendable dejar por defecto la red en NAT cuando se vaya a instalar.

Otro posible error: No se puede recuperar el sistema. Esto puede dar por varios motivos, principalmente por fallo durante la instalación, por lo que habría que reinstalarlo, y otras veces suee ser un fallo de la ISO descargada. Es recomendable ver que la ISO que hemos descargado y la que está en el Drive o web oficial, ocupan el mismo tamaño.


### Creación de máquina virtual

Ponemos como nobre DebianServer y configuramos el PAE/NX y dejamos lo demás por defecto

### Instalando Debian Server:

En este caso la instalación es algo difetente

1- En la primera pantalla seleccionamos 'Instalar'

2- Seleccionar el idioma

3- En la pantalla de configurar red, poner como nombre DebianServer como se muestra, es importante las cammel-case

![red](img/debian.png)

4- El siguiente paso es crear la contraseña de Super usuario o root, en este csao usamos la habitual Seguridad2016 o la que se prefiera, pedirá confirmación.

5- Luego pasamos a la creacion de usuario, para el que nos pedirá contraseña también:
    - Hacker
    - Seguridad2016

6- Seleccionar península en la configuración del reloj.

7- Cuando lleguemos a la hora de especificar las particiones de disco, dejar seleccionada la que viene por defecto que es **Guiado- utilizar todo el disco** como se muestra:

![particion](img/debian2.png)

8- En la siguiente pantalla nos muestra el disco (virtual) que es el único que tenemos.

9- Cuando lleguemos a *Particionado de discos* elegir la primera opción:

![particion2](img/debian3.png)

Tras esto sale otra pantalla con un resumen de lo que va a hacer así que seleccionar con los cursores  en *Finalizar el particionado y escribir los cambios en disco.* y presionar enter.

Confirmar.

10- En *Configurar gestor de paquetes* seleccionar españa, y el servicio ftp que nos da por defecto y dar a continuar porque no vamos a utilizar ningún proxi

11- La siguiente pantalla que nos interesa es la de *Seleccion de programas*, donde podemos seleccionar el tipo de entorno gráfico así como el tipo de servicio que tendrá nuestro server, dejamos lo que viene por defecto, aunque si quisiesemos seleccionar otas cosas, nos movemos con el cursor y pulsando la barra espaciadora seleccionaríamos las opciones:

![seleccion de programas](img/debian4.png)

12- Tras esto estará un rato descargando paquetes e instalando hasta llegar a la pantalla *Instalar el cargador de arranque GRUB en un disco duro*, seleccionamos 'Si', y apararece la siguiente pantalla donde debemos seleccionar el del disco virtual que tenemos creado:

![GRUB](img/debian5.png)

13- Tras eso, aparece la pantalla de *Terminar la instalación*, dar a continuar y reinicia arrancando el sistema por primera vez. Nos da a elegir en el menú de GRUB, donde elegimos Debian GNU/Linux

![Gurb2](img/debian6.png)

14- Cuando arranque poner la contraseña e iniciar sesión. 
