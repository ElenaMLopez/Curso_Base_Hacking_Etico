# FCEH_Unidad 8: Instalación en Virtualbox

Al instalar una ISO de cualquier sistema operativo, hay que tener varias cosas en cuenta. Lo primero es mirar en Sistema si nuestro sistema anfitrión es de 32 ó 64 bits. Todas las máquinas que instalemos deben de ser de los mismos bits, especialmente los Linux.

Después si veis que vuestro sistema es de 64 bits (que es lo normal), cuando creáis una máquina debe dejaros ambas opciones, si sólo aparece la arquitectura de 32 bits, es porque vuestra BIOS o SETUP no tiene habilitada la virtualización o VT-x. Para solucionarlo acceder a la BIOS en el arranque de vuestro equipo y entrad en opciones avanzadas para habilitar esa opción.

También tened en cuenta que los **sistemas Linux, deben tener marcada la opción PAE/NX en el VBox en Sistema**, Procesador para que sea compatible.

Siempre que descarguéis una máquina, será mejor descargarla de la web oficial, así estará preparada y no necesitará tantas actualizaciones, ocupa mucho más por ejemplo una Kali de hace 2 años actualizada, que una recién descargada ya con las actualizaciones.

Microsoft dispone de los sistemas en versión de prueba, y más en estos casos que es para un tema formativo, es buscar la descarga en la web oficial, salvo el XP con Service Pack 2, que se precisa con esas vulnerabilidades para el segundo curso, donde se enseña a atacar con esa máquina, así no hay que estar instalando aplicaciones vulnerables.

### Las opciones de red del VirtualBox son:

**NAT**: es un protocolo que usan por ejemplo los routers, lo que hacen es generar una red virtualizada interna. Este protocolo se encarga de traducir las peticiones de red desde el exterior al interior y viceversa. El problema es que el rango NAT al ser virtualizado no es el del router o el equipo anfitrión.

**Adaptador Puente**: Simula una conexión de red, como si fuese un ordenador físico. Usa la tarjeta de red del equipo anfitrión, por lo que recibe la IP del DHCP del router. También se le puede asignar una IP privada interna de forma manual.

**Red Interna**: Viene a ser como crear una nueva red interna de equipos, no ven equipos que no estén dentro de esa misma red. Está bien para laboratorios de prueba, pero si queremos conectividad con el equipo anfitrión o el router no nos sirve.

**Adaptador sólo-anfitrión**: Es una conexión directa con el equipo anfitrión, pero no permite conectar con el exterior directamente. Es útil para crear máquinas que simulen router o enrutadores de red.

Personalmente **recomiendo dejar NAT durante las instalaciones**. Una vez ya están todas las máquinas preparadas, pondría en todas como primer y único adaptador: Adaptador Puente, así todas estarán en un mismo rango de IP de cara a trabajar con el laboratorio de pruebas.