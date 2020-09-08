---
title: "Hacking WAP"
date: "2003-04-02"
image: assets/images/hacking-wap.jpg
author: jpalanco
layout: post
tags: [ wap, moviles, hacking ]
categories: [ old-school ]
---

```
Resulta que para empezar a trabajar de forma cómoda en entornos móviles
en una red inalámbrica es necesario tener identificados a los clientes. Es más,
cuando hay que facturarles servicios de terceros existe la necesidad de crear
algún tipo de identificador. Lo primero que hacemos es pensar que podemos
identificar a un usuario de una aplicación por su MSISDN (número de teléfono),
pero resulta que la operadora no tiene permisos para ofrecer a un tercero esa
información. Lo que si que puede hacer es crear una pasarela wap desde la que
los móviles accedan a los servidores de aplicaciones. Desde esa pasarela wap
se pueden añadir en la cabera alguna variable definida por la operadora. Lo
más normal es que la operadora asigne como valor de esa variable un hash del
MSISDN: md5, sha1, sha256, ... Se utilizará en el proceso de subscripción como ID.

El funcionamiento de estas third party tools suele ser el mismo cuando utilizan
este método. Para susbcribirte o cobrarte algún servicio se hace a través de una
URL de pago. Cuando el wap proxy detecta que se intenta acceder a alguna de esas
url's se avisa al cliente de que se le va a cobrar un extra. El servidor de
aplicaciones conoce el ID en cuanto el cliente accede a la url y lo almacena
en una base de datos.

Esta es la razón por la cual muchas aplicaciones necesitan utilizar una conexión
especial. Un primer 'hack' sería acceder a la url añadiendo nosotros los 
argumentos necesarios. Para ver los argumentos que inyecta nuetro proxy wap 
es tan sencillo como poner a escuchar el netcat en el puerto 80 y leer las
cabeceras:

# nc -l 80
GET / HTTP/1.1    
... 
cabeceras
...

Las cabeceras tienen el siguiente formato:

Nombre-De-La-Variable: valor 

El siguiente paso sería darnos de alta en el servidor de aplicaciones, pero
sin que nos cobren. Para ello haremos la petición desde internet, con telnet.

Supongamos que la url de subscripción es: 
http://wap.servidor.es/app/subscribe?session_id=346345347832146  

$ telnet wap.servidor.es 80 
Trying 10.10.10.10...
Connected to 10.10.10.10.
Escape character is '^]'.
GET /app/subscribe?session_id=346345347832146 HTTP/1.1
Host:  wap.servidor.es:80
User-Agent: telnet command appeared in 4.2BSD
Variable-ID: fa8853aa22023920e9f06d34a8536b8b_proxy23
                                      
Con esto ya habriamos subscrito al ID fa8853aa22023920e9f06d34a8536b8b_proxy23.
Como podeis apreciar en este ejemplo hay ruido al final del hash, tened en 
cuenta que puede haberlo de distintas formas. En este caso es "_proxy23".

Supongamos que usan sha1, y que el ruido es "local_" antes de la cadena. Lo
que hariamos sería dar de alta un ID así para el numero 346232323232:

$ #generamos el hash 
$ sha1 -s "346232323232"
SHA1 ("346232323232") = 2f5e05a6a96866e11a0d5920e582bfb4f06e7cc6 
$ # con lo que el ID sería: local_2f5e05a6a96866e11a0d5920e582bfb4f06e7cc6


 
Lo suyo sería utilizar el hash que ellos usan, de tal manera que el proxy-wap
nos inyectase el ID, y como está registrado en el servidor de aplicaciones, 
podriamos usarlo como un usuario registrado más. 

Puede haber otro punto de vista. Supongamos que alguien se ha registrado
a un servicio restringido a muy pocas personas, y quisiesemos utilizarlo,
podriamos sacar su hash y modificar la aplicción para que utilizase en la
cabecera ese ID, pero además tendriamos que utilizar una conexión que no
nos pusiera ID, sino nos "machacaría" el que hemos puesto (o sea una 
conexión directa a internet en vez de proxy-wap). 

En caso de que no llegasemos a sacar cual es el algoritmo de hashing,
o nos diese muchos problemas el ruido, podriamos registrar en la base de datos 
un ID inventado por nosotros. Para poder usar ese ID también tendriamos que
modificar la aplicación. 

Tendriamos que descompilar una aplicación-midlet, y añadir un par de funciones
que añadiesen a las cabeceras un ID como el de la aplicación. Para descompilar
la aplicación debemos de bajarnos el jar del midlet y descomprimir las clases.
 
$ unzip AppMvl.jar
   creating: META-INF/
  inflating: META-INF/MANIFEST.MF
   creating: com/
   creating: com/enterprise/
   creating: com/enterprise/AppMvl/
  inflating: com/enterprise/AppMvl/AppMvl.class
  inflating: com/enterprise/AppMvl/CoreComm.class
  inflating: com/enterprise/AppMvl/CoreGraph.class

Podemos utilizar JAD, un descompilador de java. Es probable que los 
desarrolladores hayan ofuscado el código, pero para lo que vamos a hacer
tampoco nos importa mucho. 

$ # desde el directorio donde se encuentran los .class
$ jad *.class

Esto nos generará varios archivos .jad, que son sources de java.
Deberemos de buscar la parte de comunicaciones, en este ejemplo parece claro
que CoreComm.class se encarga de las comunicaciones. 

Para las comunicaciones se utilizan Conectors, y se utilizan así:

miConector.open("http://wap.servidor.es");

Deberemos de modificarlo por:

miConector.open("http://wap.servidor.esi ;variable=miID");   

miID es el ID que hemos dado de alta en la cabecera de la petición o el de
la persona que queremos spoofear.

Renombramos los .jad a .java

$ for i in *.jad; do mv $i \
          $(echo $i|sed -e s/\.jad/\.java/g); done  

Y compilamos. Si quereis un buen IDE con compilador y demás lo podeis
descargar de forma gratuita de: http://netbeans.org/

Cuando ya tengamos nuestro jar, lo instalamos y accedemos a internet a
directamente, no a través de wap-proxy. Con esto ya podriamos utilizar
perfectamente la aplicación. 

Si el servidor de aplicaciones está mal diseñado y en la url de subscrición
no se toman las medidas adecuadas podriamos intentar por SQL Injection
trabajar con la base de datos y añadir por ejemplo al ID null.

Otro punto de vista...

Crackeando MD5

Partimos de que sabemos algo de información, suponemos que lo que hashean es
el MSISDN. El MSISDN se compone de, 9 ó 11 números (no hay nunca caracteres).
En caso de ser 11 caracteres comienzan por 346 en España, y si es de 9 por 6.
Podemos llegar a saber cuales pueden ser algunos de los siguientes dígitos, pues
las operadoras se repartieron los rangos que solo varian en casos particulares
(portabilidad de operadora). Podeis encontrar una lista en:

         http://docs.linenoise.info/crackwap/prefijos.txt 

Supongamos que alguien ha comprometido un servidor de aplicaciones, y
dispone de cantidad de ID's, y lo que quiere es sacar el MSISDN de una persona,
podría intentar quitar el ruido del ID y sacarlo cracreando md5 o lo que sea.

Nos descargamos mdcrack: 
http://membres.lycos.fr/mdcrack/download/mdcrack-1.2.tar.gz    

Deberiamos de retocar el programa un poco dado que ya conocemos algunos
caracteres, yo es que he quedado en media hora, y tal.. nos vemos.

No me suena haber leido nada del funcionamiento del proxy-wap, ni de las
técnicas de "etiquetar" a clientes en wap. Creo que actualmente hay
gran cantidad de servicios vulnerables y la solución es compliada.

Es más, algunos móviles como los Siemens, no pueden salir a través de proxy
wap. Como apaño se puede enviar el IMEI como identificador. Si encontramos
alguna aplicación que utilice este sistema podríamos modificar el imei
de nustro móvil.

(me lo he pasado muy bien escribiendo estas lineas, espero que tu tambien
leyendolas)
               
```