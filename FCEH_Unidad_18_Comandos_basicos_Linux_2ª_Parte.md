# FCEH_Unidad 18: Comandos básicos Linux. 2ª Parte



## Gestión de usuarios en linux

### Gestión de usuarios

Vamos a **crear** usuarios, destruirlos y realizar varias gestiones con ellos.

- Crear un usuario: Vamos a la raiz con cd y escribimos

```bash
adduser user1
```

Al pulsar intro nos pide la contraseña y luego que la confirmemos y nos muestra un menú con opciones para introducir datos del usuario. Puede dejarse en blanco dando al intro. Al final nos pide confirmación, pulsamos *s* para decir q sí y listo. Ya tenemos otro usuario con contraseña.

Si usamos el comando *useradd* en ved de *adduser* se agraga un usuario sin contraseña. 

```bash
useradd usuario2
```

Pero podemos ponerle una contraseña posteriormente con 

```bash
passwd user2
```

Y nos pide una contraseña con confirmación.

- Borrar un usuario: Para **borrar** un usuario tan solo es necesario poner

```bash
userdel usuario2
```

y borraríamos el usuario2.

- Cambiar la contraseña de un usuario: Si deseamos cambiar la contraseña de un usuario tan solo hay que hacer el paso de poner una contraseña:

```bash
passwd user2 #contraseña nueva cuando la pida
```

- Cambiar de usuario:

```bash
su usuario_a_cambiar # su usuario1 cambiaría al usuario1
```

### Gestión de grupos

- Crear un grupo:

```bash
groupadd nombre_grupo
```

Por ejemplo el grupo puede ser test1

```bash
groupadd test1
groupadd test2
```

- Agregar un usuario a un grupo:

```bash
usermod -a -G test user1
```

- Ver que grupos tiene el usuario: Estando en un usuario concreto podemos ver en que grupos está incluido

```bash
groups
```

Podemos cambiar de usuario y ver en que grupos se encuentra:

```bash
su usuario1
groups # Test1
```

Por defecto nos deja en la carpeta en la que estábamos con el usuario anterior, en este caso *root* por lo que para ir a la carpeta propia de este usuario debemos poner *cd* para ir a la carpeta raíz de este usuario.

```bash
su suruario1
cd
ls
```

- Borrar un grupo: para borrar un grupo debe existir antes.

```bash
groupdel test2
```

### Ver que grupos y usuarios existen y gestionarlos

- Ver los usuarios que existen: Podemos ver los usuarios que existen editando el archivo */etc/passw*

```bash
cat /etc/passwd
```

Nos miestra todos los usuarios que hay, y son muchos, porque son creados para aplicaciones y servicios de sistema, y los últimos son los que hayamos creado nosotros.

- Ver los grupos que existen: Para ver los grupos es tan sencillo como ver el archivo donde están listados.

```bash
cat /etc/group
```

Igualmente nos muestra arios grupos, y al final los creados, con los usuarios que tienen dentro, hay que fijarse en que por cada usuario que hayamos creado, tendremos un grupo independiente.

### Cambiar permisos de archivos para usuarios y grupos

Continuando con la sección anterior y ampliando el tema de los permisos (*chmod*)tenemos lo siguiente.

Si quisiera cambiar el usuario propietario, a otro usuario existente, por ejemplo javier, usaría el comando:

```bash
chown javier directorio1
```

Dando un ls -l aparecería lo siguiente:

```bash
-rw-r–rwx    javier    root    4566    mar 24    06:21    directorio1
```

Si ahora además quiero cambiar el grupo propietario por ejemplo a alumnos (debe existir o ser creado antes), uso el siguiente comando:

```bash
chgrp alumnos directorio1
```

Vuelvo a ejecutar ls -l y el resultado debe ser el siguiente:

```bash
-rw-r–rwx    javier    alumnos    4566    mar 24    06:21    directorio1
```

Ahora para entender como dar y quitar permisos, simplemente hay que entender que la x tenga valor 1,  la w valor 2, y la r valor 4 (nada del 3, aquí no existe, está basado en algo llamado pesos específicos que no voy a explicar).

Olvidándonos del primer paquete, que será un archivo o carpeta, los otros 3 paquetes funcionan de la misma forma. Por ejemplo el segundo paquete (rw-) sería = 6, ya que es la suma del 4 del valor de la r, más 2 del valor de la w.

El tercer paquete (r–) sería = 4, que es el valor de la r.

El último paquete (rwx), sería = 7, es la suma de 4 (valor de r), más 2 (valor de w), más 1 (valor de la x).

Como se puede ver, el valor de un paquete puede ser de cero (—) hasta 7 (rwx) y son un total de 3 paquetes sobre los que queremos aplicar cambios de permisos. Ejemplo, para poner permiso total al usuario propietario (root, javier o el que sea), permiso total al grupo de usuarios propietarios (grupo root, alumnos o el que sea), y no dar ningún permiso a quien no sea propietario o perteneciente al grupo propietario, usamos el comando chmod de la siguiente forma:

```bash
chmod 770 directorio1
```

Ejecutando ls -l saldría: ```-rwxrwx—    javier    alumnos    4566    mar 24    06:21    directorio1```

Si ahora quiero además dar permiso de lectura (r) a todos los usuarios, y que de escritura solo tenga el usuario propietario (no el grupo propietario), usaría el chmod de la siguiente forma:

```bash
chmod 754 directorio1
```

Ejecutando ls -l saldría: ```-rwxr-xr–    javier    alumnos    4566    mar 24    06:21    directorio1```

- Cambiar el grupo: Podemos cambiar el grupo que tiene privilegios de la misma forma que el usuario, pero con el comando *chgroup*, que nos cambiaría el grupo que tiene privilegios (el segundo bloque):

```bash
chgroup test2 test.txt
```
Con esto el grupo *test2* tiene privilegios sobre test2

**Hacer siempre un *ls -l* para confirmar que hemor realizado las operaciones correctamente!**

### Otros comandos

- Ver el estado de la memoria del disco duro

```bash
free
```
Nos muestra el estado del disco duro y particiones

- Mostrar procesos: Es un comando importante

```bash
top
```
Es recomendable ver el manual con ```man top``` para ver las opciones, puesto que es un comando importante a nivel de administración y nos está listando los procesos que se están ejecutando, y puesto que nos da el PID podemos utilizar esto para matar procesos:

```bash
kill nº_proceso
```

Con *kill -9* lo aniquilamos totalmente en caso de que kill no funcione correctamente (quizás los permisos de root no sean suficientes para ello).

- Reiniciar: para reiniciar el la máquina

```bash
reboot
```

- Apagar la máquina: Tiene varias opciones, así que podemos mirar la ayuda para ver todas ellas

```bash
shutdown #apaga la máquina
shutdown -h #nos muestra la ayuda y opciones de shutdown
```