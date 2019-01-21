# FCEH_Unidad 7: Virtualización en VmWare


Al instalar una ISO de cualquier sistema operativo, hay que tener varias cosas en cuenta. Lo primero es mirar en Sistema si nuestro sistema anfitrión es de 32 ó 64 bits. Todas las máquinas que instalemos deben de ser de los mismos bits, especialmente los Linux.

Después si veis que vuestro sistema es de 64 bits (que es lo normal), cuando creáis una máquina debe dejaros ambas opciones, si sólo aparece la arquitectura de 32 bits, es porque vuestra BIOS o SETUP no tiene habilitada la virtualización o VT-x. Para solucionarlo acceder a la BIOS en el arranque de vuestro equipo y entrad en opciones avanzadas para habilitar esa opción.

Para esta práctica lo importante es conocer vmWare, el sistema operativo a instalar en realidad es indiferente, pero si deseáis usar Windows 10, podréis descargarlo desde el Drive o desde la web oficial:

https://www.microsoft.com/es-es/software-download/windows10

A los que disponéis de un sistema MacOS de 64 bits, el compañero OCEANO25 nos ha compartido un vídeo con los pasos que a él le han funcionado para usar el vmware Fusion: https://www.youtube.com/watch?v=NBQreQ-cl10