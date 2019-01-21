# FCEH_Unidad 9: Instalación Windows 2008 Server

Respondiendo a las preguntas más frecuentes de este tema. Windows 2008 puede descargarse desde la web oficial en este enlace:
https://www.microsoft.com/es-es/download/details.aspx?id=5023

Una vez instalado, nos pedirá pulsar Control+Alt+Supr. Si hacemos esto se bloquea la pantalla del equipo anfitrión, para insertar esas teclas en la máquina virtual, hay que ir al menú Insertar, Teclado, Ctrl+Alt+Supr y ya nos pedirá usuario y contraseña.

Luego recordar, cuando se configuran las opciones de red en las máquinas, NAT está muy bien para empezar e instalar todo, pero cuando tengamos varias máquinas, necesitamos que todas estén en un mismo rango de direcciones IP para que se vean entre ellas. Para esto la mejor opción es Adaptador Puente, que hará que el router nos asigne una IP de su rango mediante el DHCP. Así podremos hacer pruebas entre las máquinas, con NAT nos asigna la IP 10.0.2.15 en todas las máquinas, no viéndose entre ellas. Es importante también al poner Adaptador Puente, seleccionar en el desplegable la tarjeta de red que esté usando el equipo anfitrión, si conecta por cable, debemos poner la ethernet, ya que si seleccionamos la tarjeta wifi no tendremos conexión en la máquina virtual.

Recordar que con ipconfig en Windows y con ifconfig en Linux, podemos ver las IPs que nos asigna, para verificar la conectividad, podemos lanzar un ping y ver que responda.

### Proceso:

Es muy similar a la instalación de Win10 que hemos hecho previamente. 

1 - Abrir virtualbox, y dar al boton de nueva.

2 - Ponemos el nombre de la maquina virtual que queremos isntalar y el sistema operativo. Seleccionamos el win server 2008, tipo ms windows y elegimos el de 32 o 64.

3 - Dejar la memoria ram por defecto y siguiente.

4 - Creamos el disco duro, por defecto nos pone 25GB lo dejamos tal cual, puesto que luego se asignará memoria de forma dinámica.

5 - Seleccionamos **VDI** que es la extensión por defecto para la creación de discos duros por defecto para virtual box.

6 - En la siguiente pantalla ya se puede asignar un tamaño inferior (20GB por ejemplo) y asignarlo dinámicamente. Finalizar.

7 - El siguiente paso es **configurar la máquina virtual**, sobre la máquina boton derecho o pulsar en configuración: 

    7.1- En general/Avanzado seleccionar Bidireccional en los menús 'Compartir portapapeles' y 
    'Arrastrar y soltar', esto es para compartir archivos entre la máquina virtual y el host. 
    En la pestaña General/Cifrado, puede cifrarse el sistema.

    7.3- Nos da opciones de pantalla, y tenemos caputra de video.

    7.4- En **Almacenamiento** vemos los controladores para almacenamiento. Dentro de este 
    apartado, en *Atributos* podemos configurar como Unidad óptica dando en el CD que aparece 
    al lado dle campo, el origen de la ISO que vamos a instalar. Si no lo hacemos en el 
    momento de iniciar la maquina virtual nos lo solicitará.

    7.5- Red: Aquí encontrmos los adaptadores de Red que se pueden habilitar:

      7.5.a - Adaptador 1: El habilitado pro defecto, conectado pro NAT y si damos a avanzadas 
      vemos las tarjetas de red disponibles, así como la dirección MAC que se puede cambiar 
      dando al botón de actualizar que tiene al lado.

      7.5.b - Adaptador 2: Vamos a habilitar un segundo adaptador conectado a una red interna, 
      le damos un nombre y en avanzadas es importante poner en *modo promiscuo* porner 
      *permitir todo*.

      7.6.c - El resto de adaptadores no hace falta habilitarlos.

    7.6- Puertos serie: Aquí es donde pondríamos los puertos serie, como el de impresora 
    en caso de ir a utilizarlos.

    7.7- En USB podemos cerciorarnos de tener los puertos USB habilitados.

    7.8.- En carpetas compartidas, podemos poner las carpetas que deseamos compartir con el 
    equipo anfitrion o Host. Damos en el símbolo de más de la derecha, y seleccionamos 
    *Otro...* y ahí o bien navegamos a la carpeta del host que deseamos o creamos una nueva. 
    Una vez seleccionada podemos asignar permisos, y hay que seleccionar automontar.

    7.9- Interfaz de usuario: Es importante **dejar marcado el checkbox de abajo**.

8 - Dar al botón de *Iniciar* o bien botón derecho en la máquina, elegir *Iniciar*.

### Instalción del Windows Server 2008:
1- No es necesario introducir ninguna clave de activación de producto, dejar marcado que se active automáticamente cuando se conecte a Internet.

2- Seleccionar la versión de Win a instalar, en este caso Standar Completa y checkear *He seleccionado la edición de Windows adquirida*.

3- Seleccionar la opción de avanzada para poder determinar el espacio de disco ea 20Gb .

4- Insertar una contraseña.  Por ejemplo Seguridad 2016.

### Cambiar a pantalla completa la máquina virtual

Para poner nuestra máquina virtual a pantalla completa, basta con pulsar la tecla de control derecha y F.







