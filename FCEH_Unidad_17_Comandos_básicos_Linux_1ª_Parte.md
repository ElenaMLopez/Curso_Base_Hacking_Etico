# FCEH_Unidad 17: Comandos básicos Linux. 1ª Parte

Para obtener una lista de los comandos disponibles en la consola de linux, podemos poner ```help``` o bien si tenemos alguna duda de un comando específico ```help comando```. El listado de comandos que obtenemos con help es el siguiente:
```bash
GNU bash, versión 4.4.23(1)-release (x86_64-pc-linux-gnu)
Estas órdenes del shell están definidas internamente.  Teclee `help' para
ver esta lista.
Teclee `help nombre' para saber más sobre la función `nombre'.
Use `info bash' para saber más sobre el shell en general.
Use `man -k' o `info' para saber más sobre las órdenes que no están en
esta lista.

Un asterisco (*) junto a un nombre significa que el comando está desactivado.

 id_trabajo [&]                          history [-c] [-d despl] [n] ó histor>
 (( expresión ))                         if ÓRDENES; then ÓRDENES; [ elif ÓRD>
 . fichero [argumentos]                  jobs [-lnprs] [idtrabajo ...] ó jobs>
 :                                       kill [-s id_señal | -n num_señal | ->
 [ arg... ]                              let arg [arg ...]
 [[ expresión ]]                         local [opción] nombre[=valor] ...
 alias [-p] [nombre[=valor] ... ]        logout [n]
 bg [id_trabajo ...]                     mapfile [-d delim] [-n count] [-O or>
 bind [-lpsvPSVX] [-m keymap] [-f file>  popd [-n] [+N | -N]
 break [n]                               printf [-v var] formato [argumentos]
 builtin [orden-interna-shell [arg ...>  pushd [-n] [+N | -N | dir
 caller [expresión]                      pwd [-LP]
 case PALABRA in [PATRÓN [| PATRÓN]...>  read [-ers] [-a matriz] [-d delim] [>
 cd [-L|[-P [-e]] [-@]] [dir]            readarray [-n cuenta] [-O origen] [->
 command [-pVv] orden [arg ...]          readonly [-aAf] [nombre[=valor] ...]>
 compgen [-abcdefgjksuv] [-o option] [>  return [n]
 complete [-abcdefgjksuv] [-pr] [-DE] >  select NOMBRE [in PALABRAS ... ;] do>
 compopt [-o|+o opción] [-DE] [nombre >  set [-abefhkmnptuvxBCHP] [-o nombre->
 continue [n]                            shift [n]
 coproc [NOMBRE] orden [redirecciones>   shopt [-pqsu] [-o] [nombre_opción..>
 declare [-aAfFgilnrtux] [-p] [name[=v>  source fichero [argumentos]
 dirs [-clpv] [+N] [-N]                  suspend [-f]
 disown [-h] [-ar] [jobspec ... | pid >  test [expresión]
 echo [-neE] [arg ...]                   time [-p] tubería
 enable [-a] [-dnps] [-f fichero] [nom>  times
 eval [arg ...]                          trap [-lp] [[arg] id_señal ...]
 exec [-cl] [-a nombre] [orden [argume>  true
 exit [n]                                type [-afptP] nombre [nombre ...]
 export [-fn] [nombre[=valor] ...] ó e>  typeset [-aAfFgilnrtux] [-p] name[=v>
 false                                   ulimit [-SHabcdefiklmnpqrstuvxPT] [l>
 fc [-e nombre_e] [-lnr] [primero] [úl>  umask [-p] [-S] [modo]
 fg [id_trabajo]                         unalias [-a] nombre [nombre ...]
 for NOMBRE [in PALABRAS ... ] ; do ÓR>  unset [-f] [-v] [-n] [name ...]
 for (( exp1; exp2; exp3 )); do ÓRDENE>  until ÓRDENES; do ÓRDENES; done
 function nombre { ÓRDENES ; } ó nombr>  variables - Nombres y significados d>
 getopts cadena_opciones nombre [arg]    wait [-n] [id ...]
 hash [-lr] [-p ruta] [-dt] [nombre ..>  while ÓRDENES; do ÓRDENES; done
 help [-dms] [patrón ...]                { ÓRDENES ; }
```
No vamos a verlos todos, sino tan solo los más relevantes y usados.

### Comandos habituales en linux:

- ls: muestra lo que hay en el directorio en el que estamos

- ls -l: nos da mas informacion que el anterior (si es carpeta o archivo, permisos, fechas etc)

![ls -l](img/linux.jpg)
    
- chmod: cambias los permisos (de lectura, escritura y ejecución) de un archivo o directorio ejemp: chmod 777 test.txt. La explicación detallada abajo.

![ls -l](img/linux2.jpg)

![ls -l](img/linux3.png)

- man: nos da informacion de un comando ejemp: man ls

- cd: navega entre los directorios al igual que haciamos con el comando cd de windows ejemp: cd Desktop/

- cd ..: para subir un nivel en el arbol de directorios (recordar que en windows era cd.. sin el espacio)

- clear: limpia la pantalla de la terminal

- pwd: para saber en que directorio nos encontramos

- mkdir: crea una carpeta dentro del directorio en el que nos encontramos ejemp: mkdir prueba2

- rm -R: elimina una carpeta, ejemp: rm -R prueba2 (el -R lo que hace es que elimine los sub-archivos también), es necesario             poner la *-R* porque si no da un error diciendo que es un directorio y necesita ser elimiando con su contenido

- nano: abre un archivo de texto (si no existe al guardar lo crea.) ejemplo: nano test.txt

- rm: es el mismo que el anterior, tambien podemos borrar archivos ejemplo: rm test.txt

- history: muestra los comandos ejecutados anteriormente. (podemos ejecutar un comando de la lista con ! + el id que aparece              ejemplo: !339)

- head: muestra las primeras lineas de un archivo, ejemplo: head test.txt

- tail: muestra las ultimas lineas de un archivo, ejemplo: tail test.txt

- cat: muestra el contenido de un archivo sin editarlo, ejemplo: cat test.txt

- df: (disk free) nos permite conocer la cantidad de espacio libre y espacio utilizado respectivamente

    Por default, su salida son seis columnas, sistema de archivos (Filesystem), tamaño (1K-blocss o size, depende la opción), lo usado (Used), lo disponible (Available), lo usado en porcentaje (Use%), y donde está mintado (Mounted on). Tal cual nos da lecturas de uso y disponibilidad un poco difíciles de entender, veamos con la opción -H, formato humano, y nos mostrará unidades en Kilobyes, Megas, Gigas, Teras, Petas, etc.:

- fdisk -l: muestra los discos y las particiones que tenemos


## *chmod*: Cambiando los permisos de archivos y directorios:

En un directorio podemos hacer el comando 

```bash
ls -l
```

que lista el contenido del directorio con la información detallada de éste:

```bash
drwxr-xr-x 4 elena elena 4096 ene  7 21:31 Directorio1
drwxr-xr-x 5 elena elena 4096 ene  8 09:41 Directorio2
```
Analicemos una de estas líneas.

Se divide en los siguientes bloques:

```bash
d | rwx | r-x | r-x | 4 | elena | elena | 4096 | ene 7 21:31 | Directorio1
```

Que corresponden a lo siguiente:

|  1  |  2  |  3  |  4  |  5  |   6   |   7   |  8   |      9      |      10     |
| :-: | :-: | :-: | :-: | :-: | :---: | :---: | :--: | :---------: | :---------: |
|  d  | rwx | r-x | r-x |  4  | elena | elena | 4096 | ene 7 21:31 | Directorio1 |

Donde:

1. Tipo de archivo: 'd' -> directorio, '-' ->texto...
2. Permisos para el usuario propietario del archivo (permiso root sobre él)
3. Permisos para el gurpo de usuarios del grupo propietario (gurpo de root)
4. Permisos para el resto de usuarios.
5. Enlaces
6. Nombre del usuario propietario (nombre de root)
7. Nombre del grupo propietario (nombre del grupo de root)
8. Tamaño
9. Fecha
10. Nombre del archivo o direcotrio.


Así fijándonos en los cuatro primeros bloques podemos ver lo siguiente

| Tipo de archivo | Propietario | Gurpo del propietario| Resto usuarios |
| :-------------: | :---------: | :------------------: | :------------: |
| d               | rwx         | r-x                  | r-x            |


Los permisos pueden ser de tres tipos:

|   Tipo    | Letra | Término | Valor |
|  :------: | :---: | :-----: | :---: |
|  Lectura  |   r   |   read  |   4   |
| Escritura |   w   |  write  |   2   |
| Ejecución |   x   | eXecute |   1   |

Si deseamos que el *Propietario* tenga **todos** los permisos (como aparece originalmente), tenemos que realizar la suma de los valores correspondientes, en este caso 
```bash
4 + 2 + 1 = 7
```
Vemos que el *Grupo del propietario* tan solo tiene permisos de lectura y ejecución (con los valores 4 + 1 ), y que el resto de usuarios tiene permisos de lectura y ejecución también ( 4 + 1 ).

Vamos a cambiar los permisos del *Grupo del propietario*:

En la consola ponemos:

```bash
chmod 775 directorio1
```

Cada número representa a uno de los grupos. El primero al propietario, el segundo al grupo del propietario y el tercero al resto de los usuarios. Al realizar este comando estamos diciendo al sistema lo siguiente:

> Para el directorio1 el usuario *root* tiene permiso de lectura, escritura y ejecución: Sumamos los valores de cada permiso 
>(4 + 2 + 1)

> Para el directorio1 los usuarios del *gupo root* tienen permiso de lectura, escritura y ejecución: Sumamos los valores correspondientes a cada permiso
>(4 + 2+ 1)

> Para el resto de usuarios tienen permiso de lectura y ejecución: Sumamos los valores correspondientes de cada permiso
>(4 + 1)

De esta forma, sumando los valores de los permisos y siguiendo el orden damos permisos a diferentes usuarios y con chmod los podemos cambiar. 






