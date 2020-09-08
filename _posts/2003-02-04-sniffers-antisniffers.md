---
title: "Detección de Sniffers (y AntiSniffers)"
date: "2003-04-02"
image: assets/images/antisniffers.jpg
author: jpalanco
layout: post
tags: [ redes, seguridad ]
categories: [ old-school ]
---

```

Un sniffer es un programa que intercepta los datos transmitidos por
la red

En principio los sniffers son dificil de detectar, su naturaleza hace que env�en
el m�nimo n�mero de datos.

..:: 1.- M�todos de detecci�n

No siempre es posible detectar un sniffer, es algo dificil por su naturaleza,
sin embargo detectar una m�quina que est� sniffando es m�s f�cil.


De alguna manera podemos diferenciar a los distintos m�todos que existen en dos
grupos en funci�n de que sean:

- localmente
- remotamente

...:: 1.1.- Detecci�n local

Es un m�todo determinante, pero de un proceso largo. Debemos estudiar cada
m�quina, cada sistema operativo...

Buscaremos evidencias como interfaces en modo promiscuo, procesos sospechosos.

En un sistema como linux podr�amos usar route o netstat para ver el uso de una
interfaz. 

bockvan@tango:~$ netstat -re
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
172.16.0.0      *               255.255.255.0   U     0      0        0 eth0
default         172.16.0.1      0.0.0.0         UG    0      0        0 eth0

En caso de que el uso de una interfaz sea algo m�s que sospechosa, usaremos
ifconfig para ver si se encuentra en modo promiscuo.

bockvan@tango:~$ /sbin/ifconfig eth0
eth0      Link encap:Ethernet  HWaddr 00:05:1C:13:CE:F0
          inet addr:172.16.0.3  Bcast:172.16.0.255  Mask:255.255.255.0
          UP BROADCAST RUNNING PROMISC MULTICAST  MTU:1500  Metric:1
          RX packets:11583 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11306 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:100
          RX bytes:3799031 (3.6 MiB)  TX bytes:10693650 (10.1 MiB)
          Interrupt:11 Base address:0xc000
		  
Como podeis ver hay una interfaz en modo promiscuo, para desactivar este modo
usaremos:  ifconfig &lt;interfaz&gt; -promisc

Tambi�n podemos ver los logs por si alguna interfaz se puso en modo promiscuo:

root@tango:/home/bockvan# tail /var/log/messages
Feb 12 18:40:08 tango kernel: device eth0 entered promiscuous mode
Feb 12 18:41:47 tango kernel: device eth0 left promiscuous mode
Feb 12 18:42:01 tango kernel: eth0: Promiscuous mode enabled.
Feb 12 18:42:01 tango kernel: device eth0 entered promiscuous mode
Feb 12 18:42:02 tango kernel: eth0: Promiscuous mode enabled.
Feb 12 18:42:02 tango kernel: device eth0 left promiscuous mode
Feb 12 18:44:37 tango kernel: eth0: Promiscuous mode enabled.
Feb 12 18:44:37 tango kernel: device eth0 entered promiscuous mode
Feb 12 18:47:28 tango kernel: eth0: Promiscuous mode enabled.
Feb 12 18:47:28 tango kernel: device eth0 left promiscuous mode


En cualquier caso, si el atacante que instal� el sniffer tiene un gran control
sobre la m�quina, podr� ocultar todas esta evidencias, eliminar logs, ...

Un buen ejemplo de esto es RhideS, que es un LKM programado por Ripe que oculta
el modo promiscuo en interfaces de red. Podeis encontrar este m�dulo y muchas
m�s cosas en la p�gina de 7a69 [1].



...:: 1.2.- Detecci�n remota



Existen principalmente dos pruebas para detectar un sniffer en nuestra red.

...:: 1.2.1- M�todo pasivo 

Escucha todos los paquetes que circulan por la red en busca de actividad
sospechosa. Por ejemplo el env�o de arp request's (1).

...:: 1.2.2- M�todo activo 

Env�a paquetes modificados esperando la respuesta que nos dar�a una m�quina con
una interfaz en modo promiscuo. En este tipo de test, entran en juego las
caracter�sticas propias de los sniffers, asi como de las de los propios sistemas
en los que se encuentran. Esto �ltimo implica estudiar la pila TCP/IP del
sistema operativo y encontrar caracter�sticas que nos permitan determinar la
existencia de un sniffer.

Algunas de las pruebas mas conocidas son:

- de ICMP
- de ARP
- de DNS
- de LATENCIA


..:: 2.- Detecci�n 

Por ejemplo, el sistema operativo GNU/Linux, estando en modo promiscuo,
responder� a los paquetes de TCP/IP enviados a su IP ADDRESS incluso si 
la MAC ADDRESS en ese paquete est� mal cuando lo habitual es que
los paquetes que contienen una MAC ADDRESS incorrecta no sean contestados 
porque el interfaz de la red los ignora (son dropeados). Por esta raz�n,
si enviamos paquetes TCP/IP con las MAC ADDRES con informaci�n incorrecta
a una subred entera, nos respondar�n las maquinas en modo promiscuo (nos
responder�n con RESET -RST-).

...:: 2.2- T�cnicas 

Dependiendo del sistema operativo que se utilice deberemos de enviar paquetes
modificados de una u otra forma ya que la pila tcp/ip de cada sistema a pesar
de seguir un est�ndar no est�n definidas para peticiones no est�ndarizadas.

...:: 2.2.1- PING 

Un fallo en la implementaci�n de la pila TCP/IP en algunos n�cleos de GNU/Linux
puede ser explotada para descubrir sniffers en el sistema. El n�cleo comprueba
todos y cada uno de los paquetes para comprobar si la IP es de la m�quina en
cuesti�n; en caso de que sea as�, este paquete pasa al apilado TCP/IP para que
que sea procesado. Lo que no se comprueba es que la direcci�n (ethernet) de la 
tarjeta de red contenida el paquete, coincida con la MAC ADDRESS de la interfaz
de la tarjeta. La raz�n por lo que esto no es comprobado es por que la tarjeta
de red permite el paso de paquetes entrantes que no emparejan su direcci�n de
red. Si enviaremos un ICMP "echo request" con una IP ADDRESS correcta y una MAC
ADDRESS falsa, si el objetivo de nuestro test responde, significa que
probablemente est� sniffando la red y tenga la interfaz en modo promiscuo.

En algunos n�cleos de FreeBSD sucede algo similar, solo que en vez de utilizar
una IP ADDRESS correcta deberemos de utilizar una direccion de broadcast
correcta.

En los sistemas Windows de Microsoft podemos realizar esta prueba usando una
IP ADDRESS correcta y como direcci�n ethernet ff:00:00:00:00:00, que no es una
direcci�n de broadcast pero debido a la pobre implementaci�n de la pila TCP/IP
de estos sistemas, al realizar este tipo de peticiones obtendremos respuesta.
Reazlizando esta prueba es sabido que ciertos dispositivos de red curiosamente
tambien responden sin que ello signifique forzosamente que su interfaz (o 
interfaces) est� en modo promiscuo.

Los sniffers actuales vienen provistos con un filtro de MAC ADDRESS, de tal
manera que no contesten con ECHO REPLY.

...:: 2.2.2- ARP 

Existen varias formas de comprobar remotamente la existencia de una interfaz en
modo promiscuo. El m�todo m�s sencillo consistir�a en enviar una peticion ARP
a una direcci�n que no sea broadcast. En caso de que la m�quina reponda, debe
de estar en modo promiscuo.

Un m�todo m�s elaborado podr�a aprovechar la cach� de ARP. Cada ARP dispone de
informaci�n completa tanto del origen como del destino. Si se envia un �nico ARP
a una direcci�n broadcast, incluyo mi propia direcci�n de tal manera que en los
siguiente minutos los dem�s equipos recordar�n esta informaci�n. 
Luego si enviamos un ARP pero no al broadcast y despu�s hacemos un ping al 
broadcast, cualquiera que responda sin ARPing s�lo ha podido obtener la
direcci�n MAC esnifando.

Una variaci�n de este m�todo (usaba por nepped, desarrollada por savage de
apostols) utiliza un fallo de arp.c en los sistemas de kernel linux, se trata
de la funci�n arp_rcv(). Esta funci�n se ocupa de determinar cuando hay que
enviar respuestas de ARP. Al llegar insuficientes peticiones y da�adas, los
sistemas linux responder�n con peticiones ARP independientemente de la MAC
de destino. En general s�lo marcos con la MAC de la m�quina se procesan, as�
que no es un problema. En modo promiscuo, como sabemos, todos los marcos son
procesados sin comprobaci�n del la direcci�n MAC de destino y no hay manera
de diferenciar si el paquete fue realmente limitado para la m�quina que 
est� escuchando.

...:: 2.1.3 - DNS

Muchos sniffers ofrecen la posibilidad de mostrar la resoluci�n de nombres 
de las m�quinas que est�n sniffando, de tal manera que se le presente al
usuario m�s informaci�n. 

Los sniffers de peticiones dns capturan el trafico en bruto de la red, y
es necesario traducir las direcciones IP a los nombres de las m�quinas. Es
habitual que los sniffers realicen peticiones de DNS para traducir las IP's
de los paquetes capturados. Un ejemplo de esto es AntiSniff, que env�a paquetes
falsos con IP's falsas (tanto de origen como de destino) y escucha (esnifa)
las peticiones DNS buscando una resoluci�n para las IP's falsas que cre�.
Las m�quinas que realicen peticiones de resoluci�n para las IP's que
pongamos en los paquetes de prueba, tendr�n un sniffery estar� escuchando el
tr�fico de nuestra red. 

Una soluci�n que est�n implementando los nuevos sniffers de �ltima generaci�n 
es resolver los nombres con algo de delay (retraso) que depende de los datos
que recivamos y decodifiquemos, de tal manera que si no conseguimos esnifar
datos, no hay necesidad de resolver la IP. Gracias a esto los sniffers no
saturan la red con peticiones de resoluci�n de DNS.


...:: 2.1.4 - De estado latente 

Consiste en comparar el tiempo de reacci�n de de una m�quina antes y depu�s de
saturar el tr�fico de la red con informaci�n irrelevante. De esta manera los
equipos en los que haya un sniffer instalado analizar�n todo el tr�fico in�til
para depu�s procesarlo y tardar�n m�s en respondernos que cuando no hay 
saturaci�n en la red.

Existen casos en los que esta t�cnica puede fallar:

Debido a la carga en la red, pueden haber falsas alarmas, esto es debido a que
el medio no puede soportar tanta cantidad y algunos paquetes llegan con algo de
retraso, para arreglar estos solo debemos de cargar algo menos la red. 

Los sniffers suelen ejecutarse como modo usuario, mientr�s que el env�o de 
paquetes ICMP tiene que ser ejecutado como modo kernel siendo independientes de
la carga del la m�quina los procesos de cada cosa, por lo que posibles sniffers
no ser�n detectados ya que el sistema intentar� responder de la misma manera
que si no hubiese sniffer. 


..:: 3.- Enga�ando a AntiSiff

Este antisniffer es capaz de trabajar con la mayor�a de sniffers, pero sigue
unos patrones muy especificos, con lo que basta modificar alguna cosa para
detectarle. Existen t�cnicas que permiten esnifar sin que antisniff pueda
evitarlo. Pero sin duda resulta molesto tener que escribir un sniffer para
cada antiesniffer cuando los sniffers que hay en 'el mercado' son realmente
buenos. Si Mahoma no quiere reescribir el programa, se hace m�dulo para el
kernel... �que es lo que va a hacer este m�dulo? Pues sencillo, mofificar
un poco la pila TCP/IP de nuestro sistema, de tal manera que todas las
herramientas comunes que el antisniff es capaz de detectar ser�n filtradas.
La t�cnica del sniffing ya est� muy trabajada, las utilidades de la red son
muy buenas, lo unico que tendriamos que hacer ser�a realizar m�dulos para
los antisniffers.

Unos �ltimos consejos para desarollar un sniffer :
- No realices peticiones DNS (no siquiera con delay).
- Para de esnifar cuando haya demasiada actividad en la red. 

 
..:: APENDICE

Referencias:

[1] http://www.7a69ezine.org/


               
```