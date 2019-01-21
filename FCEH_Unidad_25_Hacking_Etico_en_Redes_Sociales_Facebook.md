# FCEH_Unidad 25: Hacking Ético en Redes Sociales. Facebook

SET es una aplicación que entre muchas otras cosas, permite clonar páginas web. Para que esta sea visible se basa en Apache server, un servidor web que se ve en el 2º curso, al igual que el código fuente de las páginas web.

Siguiendo el vídeo se ve que Facebook, o incluso otras webs se clonan sin problema, pero en el ejercicio se solicita clonar Instagram.

Esta última web no clona por defecto las imágenes. Esto es debido a que Instagram pone medidas de seguridad para este tipo de ataques. Dispone de javascripts (archivos .js) y código en su página, que en vez de redireccionar a las imágenes, lo hace a otra parte de la web. Por ejemplo, si clonamos una web que hace referencia a una imagen que está en un subdiretorio, lo normal es poner /imagenes/imagen.jpg. Instagram para evitar esto, pone www.instagram.com/imagenes/imagen.jpg

Algo tan sencillo como esto hace que al clonar el sitio, y disponer de sistemas de protección, como que ciertas partes sólo puedan ser llamadas desde su web, haga que ciertas imágenes no sean clonadas.

El ejercicio sin imágenes es correcto, lo que quiero mostrar con este ejercicio es algo muy básico en el mundo del hacking, es simplemente que no se puede usar siempre un mismo ataque estandar contra todas las víctimas. En muchas ocasiones, es necesario profundizar más y realizar un ataque personalizado. Al igual que sucede con este tipo de ataque, sucede con todos.

Comentar también, que el directorio donde almacena el harvester puede variar según la versión, por ejemplo hay versiones que guardan la información en el directorio oculto /set/.set/, pero esto puede cambiar con cada actualización. Es por ello muy importante ver los archivos de configuración de cada aplicación para poder ver más a fondo cómoo funciona internamente el programa.

Como es lógico, estamos trabajando con IPs privadas (internas de nuestra red). Si quisiéramos realizar este ataque de forma externa, debemos usar la IP pública, la que asigna nuestro proveedor de línea de internet. Podemos verla por ejemplo en la web cualesmiip.com

Esta IP cambia cada cierto tiempo, normalmente bastante tiempo. Para que siempre sea la misma hay que pagar el servicio al proveedor de internet. Si hacemos la práctica con esta IP pública, veremos que sale el router. Esto es debido a que esa IP se asigna en lo que se llama pata WAN del router. Para que la práctica funcioner de forma correcta externamente, es preciso indicar al router a que  IP interna debe mandar ese tráfico, para ello hay que crear una ruta de forma en que todo el tráfico web vaya a la IP privada de la Kali.

El problema de esto, es que si redireccionamos todas las peticiones web a esa IP, el resto de equipos tendrán problemas de navegación, es por eso que se suele usar una línea independiente, o una vez precisemos usar otros equipos deshabilitar esa regla del firewall que tiene el router.

Para enviar el enlace encubierto, es preciso hacerlo mediante algún medio compatible con HTML, ya sea word o webs que permitan poner este tipo de código. Google por ejemplo va a mostrar el enlace real, para evitar eso debemos poner nuestra falsa web (www.facebook.com/QuienVeMiPerfil) en la etiqueta Title de HTML.

### Pasos

1. Hacer un *ifconfig* para ver la IP que tenemos asignada y dónde:

![ifconfig](img/facebook.png)

En este caso la **10.0.2.15**

2. Abrir en *Aplicaciones/13-Social Engeneering Tools* el programa **SET** (social engeneerinig tool).

3. Dentro del menú que sale, seleccionar la opción de ataque de ingenieria social, es decir, la opción 1:

![set](img/facebook2.png)

4. En el siguiente menú que sale, lo que hay que seleccionar es el tipo de ataque, que en este caso es el 2, ataque a traves de uan web:

![set](img/facebook3.png)

5. Lo que queremos es capturar las credenciales de usuario y contraseña. Así que en el siguiente menú cojemos la opción 3.

![set](img/facebook4.png)

6. En el siguiente menú nos pregunta como vamos a clonar el site para engañar al usuario, si importando o qué preferimos. Lo interesante es que se mantenga actualizado así que elegimos la segunda opción:

![set](img/facebook5.png)

7. A continaución nos pide la IP que tenemos para montar el servidor, así que pegamos la IP nuestra.

