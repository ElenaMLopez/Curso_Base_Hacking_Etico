# FCEH_Unidad 22: Generador de Diccionarios

Lo primero es comentar que habitualmente usamos el sistema decimal o base 10, lo que usa los caracteres 0, 1, 2, 3, 4, 5, 6, 7, 8 y 9. Un total de 10 caracteres, por eso decimal o base 10.

Existen muchos otros sistemas, como el binario o base 2 tan conocido, es el sistema que usan en electrónica y en informática, compuesto de 0 y 1.

Hay otros sistemas como el base 8, no tan usado, pero sin duda uno de los más importantes en informática es el hexadecimal o base 16. Esta base hexadecimal tiene los dígitos que corresponden del 0 al 15 (total de 16) y son los siguientes: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E y F, siendo por ejemplo la A igual a 10 y la F igual a 15.

Cuando hacemos un ataque de fuerza bruta mediante diccionario, es imposible crear un diccionario con todos los números, letras minúsculas y mayúsculas, además de caracteres adicionales. Es por esto que se usan diccionarios que hay en internet con palabras clave usadas de forma más frecuente. Lo que sucede es que si esa contraseña no está presente en el diccionario, no lograremos hackearla.

Para el tema del WiFi, lo más interesante es usar diccionarios hexadecimales, ya que este tipo de autenticación permite autentificarse tanto con la contraseña ASCII (la que escribimos habitualmente por teclado), como por su correspondencia en hexadecimal. Podéis hacer la prueba por ejemplo, buscando en Google conversor ASCII a hexadecimal y obtener vuestra contraseña en hexadecimal, veréis que si la ponéis conectará sin problema.

Lo que si es importante saber, es que hexadecimal son 16 dígitos, por lo que no diferencia entre mayúsculas de minúsculas en sus letras, siendo por ejemplo el código hexadecimal 3B igual que 3b, lo que nos facilita la tarea.

### Usando crunch

Abrimos una consola en Kali, y lo primero es ver la versión de *crunch* que tenemos isntalada:

```bash
crunch 2 3 0123456789 -o /root/Desktop/dicnumerico.txt
# crunch <min> <max> [options]
```

Lo que hace esto es crear las conbinaciones de 2 a 3 dígitos, comprendidos entre el 0 y el 9, es decir desde el *00* hasta el *999*.

Crunch tiene varias opciones, por ejemplo podemos crear diccionarios en hexadecimal que tiene dígitos del 0 al 9 y letras de la A a la F, así podemos hacer un diccionario en hexadecimal y guardarlo en el escritorio de nuevo:

```bash
crunch 2 3 0123456789abcdef -o /root/Desktop/dichex.txt
# crunch <min> <max> [options]
```

Nos crea un diccionario desde el *00* hasta el *fff*, esto es, hexadecimal.

Otra opción es por ejemplo indicarle que no se repitan caracteres con 2@:


```bash
crunch 2 3 0123456789abcdef -d 2@ -o /root/Desktop dichex.txt
# crunch <min> <max> [options]
```

No pueden repetirse más de dos dígitos consecutivos, es decir, el *11* por ejemplo si puede estar, pero el *111* ya no podría. Con -d eliminamos caracteres de la generación del diccionario.

Vamos a generar diccionarios que tengan un tamaño máximo, por ejemplo 10Mb, para ello ponemos lo siguiente:

```bash
crunch 4 6 -b 10mib -o START
# crunch <min> <max> [options]
```

Puesto que el mínimo de caracteres son 4 y el máximo 6, nos gernera un diccionario enorme y lo que hacemos con esto es dividirlo en varios archivos de máximo 10Mb. Puede ser mib kib o gib, según queramos megabites, kilobites o gigabite. Como no ponemos si es alfanumérico o hexadecimal, generará todas las combinaciones por lo que podemos encontar palabras como *casa*.

Por otro lado si lo hacemos tal cual, lo genera en la **carpeta donde nos encontremos** y lo interesante es que podemos ver el rango de caracteres que hay en cada archivo.

Se pueden ver las opciones de crunch con el comando man:


```bash
man crunch
```