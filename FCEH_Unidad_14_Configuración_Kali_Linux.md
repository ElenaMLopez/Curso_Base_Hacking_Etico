# FCEH_Unidad 14: Configuración Kali Linux


Voy a contestar las preguntas más habituales de cada unidad, ya que veo que son muy reiterativas. Las del WiFi las respondo en su correspondiente lección, así mantenemos la información ordenada.

Lo primero son una parte fundamental de Linux, los repositorios.

Los repositorios son enlaces de cada distribución de Linux donde obtenemos las actualizaciones y un enlace a las aplicaciones de cada distribución, de forma que usando el apt-get install sepa dónde encontrar esa aplicación, o actualización, ya sea del sistema o de un programa.

Cuando en la instalación le decimos que No al instalar desde la red, lo que hace es dejarnos este archivo vacío, pudiendo nosotros mismos introducir los repositorios que creamos convenientes.

Esto se hace así en el curso para entender la importancia de los repositorios, ya que cuando cambian la versión de una misma distribución, pueden crear nuevos repositorios que deberemos pegar en el sources.list si queremos mantenernos totalmente actualizados.

En este momento los Kali-Rolling son los repositorios oficiales más actuales, aquí los pongo:

deb [http://http.kali.org/kali](http://http.kali.org/kali) kali-rolling main contrib non-free
deb-src [http://http.kali.org/kali](http://http.kali.org/kali) kali-rolling main contrib non-free

Una vez tenemos esto correcto, con el comando apt-get update actualizamos estos repositorios, es bueno hacerlo de vez en cuando.

Luego podemos actualizar el sistema y las aplicaciones, para ello usamos apt-get upgrade. Para ver que tenemos el kernel actualizado, usamos el comando uname -r, que nos dirá la versión, por ejemplo la 4.14.

Si vemos que hay versiones más actualizadas y aún con estos comandos no se actualiza, deberemos usar también el comando apt-get dist-upgrade. Para conocer el kernel más actual, podemos ir a la web oficial del kernel para todos los Linux: https://www.kernel.org debemos ver la versión stable.

Cada vez que hacemos un upgrade, es importante ver si no nos da ningún aviso, hay veces que dispone de paquetes obsoletos que debemos borrar para seguir actualizando, para ello debemos ejecutar el comando que nos indica: apt autoremove. Si durante alguna actualización se queda la pantalla retenida con el cursor y dos puntos (:), está esperando a que metamos parámetros, lo mejor es dar siempre la tecla Q para continuar con la actualización.


### Instalaciones en Kali Linux

Debido a que la distribución que se pasa en el curso es muy antigua, es bastante complicado resolver los problemas que plantea. Dentro de los comentarios de la página, Ivan Campos Lorenzo parece solucionar todos los problemas así que tomo sus pasos. 

No obstante he optado por descargar una versión más reciente de la ISO, comprobar el código sha de la misma y realizar una nueva máquina virtual con Kali.

### Pasos:

**GUEST ADDITIONS FUNCIONANDO**: Hola. He leído en muchos comentarios problemas con la instalación de las Guest Adiitions. Yo también los he sufrido al principio y recopilo todos los pasos que he seguido para resolverlo (es ua mezcla de todos los comentarios, no me he inventado nada. Muchas gracias a Javier Blanco por su aciencia con nosotros)

### Lo primero de todo, se debe tener en cuenta que hemos instalado Kali con la lista de repositiors VACÍA. Esto lo debemos resolver con el siguiente comando
sudo nano /etc/apt/sources.list
### Pegamos las dos líneas que indico a continuación

```bash
deb http://http.kali.org/kali kali-rolling main contrib non-free
deb-src http://http.kali.org/kali kali-rolling main contrib non-free
```

### Guardamos (Ctrl+O ) y salimos de nano (Ctrl+X). Ya tenemos los repositorios correctamente configurados. Continuamos
```bash
sudo apt-get update	# Esto actualiza los repositorios
sudo apt-get upgrade	# Esto actualiza sistema y aplicaciones
uname -r	# Nos indica la version de Kernel. A mi me devuelve el valor 4.15.0-kali2-amd64
sudo apt-get dist-upgrade	# Actualiza la versión (también el Kernel)
uname -r	# Nos indica la version de Kernel. Compruebo que ahora el valor es 4.16.0-kali2-amd64 (ha actualizado el Kernel)
sudo apt-get install linux-headers-$(uname -r) dkms	# Actualiza las cabeceras: Con esto ya no debería quejarse al instalar las Guest Additions
sudo apt autoremove	# Elimina paquetes obsoletos
subo reboot	# Reinicia el equipo
```
### Montamos la imagen del CD de las “Guest Additions”

```bash
sudo sh ./VBoxLinuxAdditions.run	
Por fin consigue instalar las Guest Additions sin quejarse de los headers.
sudo reboot	# Reiniciamos de nuevo
```

### Después podemos comprobar que están bien instaladas si conseguimos copiar carpetas desde el Host hasta la VM arrastrando y si nos funcionan lasa “Carpetas compartidas”

# Solucion para la versión 18.04.0

Bajar la iso de: www....

Se instala la versión 18.04.0-kali2-amd64

Editar el archivo sources.liet:
```
gedit /etc/apet/sources.list
```
Y añadir el repositorio que encontramos en la web oficial de docs apartado 5 primero:
```
# Kali sources.list Repositories
deb http://http.kali.org/kali kali-rolling main non-free cotrib
```
Updatear el sistema:
```bash
apt update
```

Podemos ver la versión del kernel poniendo 
```bash
uname -r
```
Comprobar si nuestro kernel es compatible con alguna de las versiones del kernel, para ver las versiones del kernel disponibles poner 

```bash
apt install linux-headers*
```

Actualizar la version del kernel
```bash

```


Actualizar las cabeceras para la nueva versión del kernel:
```bash
apt install linux-headers-$(uname -r)
```

Instalar la imagen de kali linux-image-4.18.0-kali3-amd64

reiniciar
```bash
reboot
```
Hay que descargar la imagen del Guest Additions para realizar la instalación en kali. En este caso instalamos la versión 6.0.0. 
La forma en que he conseguido hacer esto es la siguiente, aunque puede haber otras.

Una vez reiniciado ir a la pagina del tracker de debian y acceder a *A new upstream version is avaliable: 6.0.0* o seguir este [link](http://download.virtualbox.org/virtualbox/6.0.0/VBoxGuestAdditions_6.0.0.iso)

Esto nos descarga la imagen de la iso, dentro de la makina virtual de kali. Navegar hasta la carpeta de descargas y haciendo doble clic, montamos la imagen y normalmente lanzarse una consola y realizarse la instalación, puesto que es un autoejecutable.

En caso de error o que no se pueda abrir, podemos navegar con una terminal hasta la carpeta donde tenemos la imagen montada, y se ejecuta el siguiente comando:

```bash
sh ./VBoxLinuxAdditions.run
```
Con esto ejecutamos el instalador.

Reiniciar, y debería funcionar aunque salte algún mensaje de error, puesto que estos suelen saltar como aviso de que el kernel no se acutaliza realmente hasta el reinicio.


![Felicidades](img/kali_full.png)

Enhorabuena si has llegado hasta aquí sin decidirte a cambiar de sector y dedicarte al enriqucedos cultivo de patatas en tu vida ;)

### Comrpbar q se reconoce la tarjeta de red:

Habrir una terminal y poner un 
``` 
ifconfig
```
Si tenemos una tarjeta de red wireless por usb por ejemplo nos saldrá, así como con el comando 
```
wconfig
```
Tener en cuenta que si no se ha configurado ningun adaptador de red más, tan solo aparece la cableada que hay por defecto.

### Una vez funcione se puede realizar una exportación de servicio virtualizado

Apagar la máquina virtual

En VM :
Archivo/Exportar servicio virtualizado ò Ctr+e

Seleccionar kali o la que deseemos y siguiente

Nos pregunta dónde guardarla y esto nos genera una copia de seguridad con extensión .ova, de la que podemos disponer en caso de que nuestra maquina se vea dañada po algún r motivo.