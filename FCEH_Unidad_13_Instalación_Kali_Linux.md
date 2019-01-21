# FCEH_Unidad 13: Instalación Kali Linux


Os dejo cómo solucionar los problemas más habituales de Kali:

Al instalar una ISO de cualquier sistema operativo, hay que tener varias cosas en cuenta. Lo primero es mirar en Sistema si nuestro sistema anfitrión es de 32 ó 64 bits. Todas las máquinas que instalemos deben de ser de los mismos bits, especialmente los Linux.

Después si veis que vuestro sistema es de 64 bits (que es lo normal), cuando creáis una máquina debe dejaros ambas opciones, si sólo aparece la arquitectura de 32 bits, es porque vuestra BIOS o SETUP no tiene habilitada la virtualización o VT-x. Para solucionarlo acceder a la BIOS en el arranque de vuestro equipo y entrad en opciones avanzadas para habilitar esa opción.

También tened en cuenta que los sistemas Linux, deben tener marcada la opción PAE/NX en el VBox en Sistema, Procesador para que sea compatible.

Kali linux en algunos equipos necesita 2 Gb de RAM para la instalación, pudiendo ajarse después sin problema, el error que suele dar cuando esto pasa, es que se queda la pantalla en negro y no continua la carga.

Siempre que descarguéis una máquina, será mejor descargarla de la web oficial, así estará preparada y no necesitará tantas actualizaciones, ocupa mucho más por ejemplo una Kali de hace 2 años actualizada, que una recién descargada ya con las actualizaciones.

En la web oficial de Kali, disponéis de una versión para Virtual Box actualizada. Recordar que cuando no ponéis vosotros la contraseña, la que Kali trae por defecto es usuario root y contraseña toor.

### Montar maquina virtual y realizar la instalación:

En realidad es muy similar a la instalación de Debian Server, como podemos ver en las siguientes imágenes

![Kali](img/kali.png)

![Kali](img/kali2.png)

![Kali](img/kali3.png)

![Kali](img/kali4.png)

![Kali](img/kali5.png)

Se deja todo por defecto y se da a siguiente. 

En el momento de iniciar sesión, el usuario es root y la contraseña es la que hemos selsccionado: Seguridad2016.

## Realizar la evaluación!