# FECH_Unidad11_Installacion_Ubuntu_Mate:


Ante los problemas más comunes con Ubuntu, aquí os dejo unas posibles soluciones:

1- Ver si su sistema anfitrión es de 32 ó 64 bits. Una vez visto esto, usar sistemas virtualizados de la misma arquitectura. En la plataforma se han subido los de 32 bits por ser los más complicados de encontrar. Si su equipo es de 64 bits, descargue mejor el Ubuntu de la web oficial, así además estará actualizada.

2- Mire que en Sistema, Procesador, dentro de la configuración de la máquina en VBox tenga marcada la casilla PAE/NX. Esto debería marcarse en todos los Linux por temas de compatibilidad con el microprocesador.

3- Si su sistema es de 64 bits, cuando instala una máquina virtual, le deja instalarlas de 32 y 64 bits, o sólo de 32? A los que sólo os deja de 32 bits, es porque tenéis deshabilitada la virtualización en la BIOS. Es simplemente acceder a la BIOS o SETUP del equipo anfitrión, y habilitar en opciones avanzadas la Intel virtualization, VT-x, o similar, dependiendo de vuestra BIOS.

AVISO: En las últimas versiones de Debian están poniendo un repositorio que comienza por “deb cdrom”. Es importante comentar este repositorio para poder actualizar correctamente la distribución sin necesidad de descargarse todos los CDs.


### Crear la máquina virtual

Hacemos una máquina virtual modificanto tan solo como de costumbre en sistema/procesador el PAE/NX y seleccionando el origen de la ISO para que no la pida luego.

### Instalando Ubuntu Mate:

Es una muy simple instalación, dejamos todo lo que nos da por defecto y es tan solo dar a siguiente. En el caso de Usuario podemos poner Hacker y la contraseña que usamos habitualmente Seguridad2016, o bien el que se elija.

