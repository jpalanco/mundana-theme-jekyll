---
title: "Telefonia"
date: "2002-06-01"
image: assets/images/telefonia.jpg
author: jpalanco
layout: post
tags: [ telefonia ]
categories: [ old-school ]
---

```

                ###################################################
                #CAPITULO PRIMERO: ESTRUCTURA DE LA RED TELEFONICA#
                ###################################################

########################
#1.Estructura de la red#
########################

1.1 EXISTENCIA DE LAS CENTRALES
###############################

La  existencias  de las centrales  telefonicas se debe  entre otras  razones a
que se  aprovecha  mas material, al no tener que hacer un cableado entre todos
y cada uno de los abonados.Hoy en dia seria imposible esto ultimo.

Para  calcular  el numero  de  uniones entre N nodos (abonados) se  puede usar
la siguiente formula:


                    [ N ]    N(N-1)
                U = |   | = --------
                    [ 2 ]       2

Con  las  centrales, no hay  que conectar   a  todos  los  abonados  entre si,
sino que hay que conectar a  todos los abonados  con una central  comun que se
encargue de comunicarles.

A  este  tipo de centrales  que se encarga  de  comunicar  a  un  conjunto  de
usuarios de una zona determinada se las denomina CENTRALes de area LOCAL.

El  equipo  de conmutacion  es  el encargado  de hacer esta funcion, que no es
ni mas ni menos que enrutar llamadas  desde el usuario  que realiza la llamada
hasta  el  que  la  recive. Este  enrutamiento se hace en funcion a  un numero 
que  el usuario  llamante  indica  a la central  y  que pertenecen  al usuario 
llamado, y teniendo  en cuenta unos criterios  de  enrutamiento que explicare 
en proximas ediciones.

A los elementos encargados  de unir a una central local con sus abonados se la
llama RED DE ABONADOS o RED LOCAL de la central.

1.2 JERARQUIZACION DE LAS CENTRALES
###################################

Como las centrales locales  solo pueden abarcar  un  area local,  es necesario
conectarlas  entre ellas con el fin  de que  usuarios  de diferentes centrales
locales se puedan comunicar.

Por ello  se recurre a centrales de mayor  rango que se  encarguen de conectar
areas locales. A este tipo de centrales se las  denomina  CENTRALES PRIMARIAS.

Cada   central local  depende  de una unica central  primaria, y  una  central
primaria depende de varias centrales locales.

Las  centrales  primarias han de conectar centrales  locales cursando llamadas
de transito, o sea llamadas a abonados que no les corresponden.

Aunque hay tipos  de centrales  primarias que tienen sus propios abonados,que
no pertenecen a ninguna central local por estar emplazadas mas lejos.

La  union entre una central  local y la central  primaria se  denomina seccion
primaria, cuya  composicion consta  de  un conjunto  de circuitos individuales
que llamaremos enlaces.

Cada  enlace  entre centrales  puede  ser  en  algun  momento  la  base de una
comunicacion.

Asi  como han  de estar comunicados los  abonados de  distintas areas, han  de
estarlo  entre  si tambien  las centrales  primarias; el  numero  de centrales
primarias  ha de  ser muy alto para conectarlas  entre si. Asi, ha  de existir
una central de mayor categoria conectada a las centrales primarias, la central
secundaria.

Cada  central  primaria  depende  solo  de otra secudaria,  y  de  una central
secundaria dependen varias primarias.

La  funcion de  toda central  secundaria es la de conectar centrales primarias
entre si. No hay excepciones como en la central primaria, puesto que NINGUN
tipo de central secundaria tiene abonados propios.

La seccion secundaria es la union entre una central primaria y la secundaria de
la que depende (compuesta por enlaces).

Es necesario  recurrir  a una central de rango superior para que  se comuniquen
entre  si  los abonados de areas  secundarias, ya que  el numero de  centrales
secundarias es alto.

Para ello se  recurre a una central terciaria o NODAL, constituye  un nodo  de
la red telefonica.

Una region NODAL: coincide con una region (region nodal, claro esta..LOL).

La  central  secundaria depende de una unica central terciaria; de la terciara
dependeran varias secundarias.

La funcion de una central terciaria es conectar centrales secundarias entre si.
La union de centrales secundarias y terciarias se conoce como seccion terciaria
y se compone por enlaces.

Las conexiones de los abonados de las areas terciarias no necesitan recurrir a
centrales  de  rango superior  ya que son solo 6 en españa (Madrid, Barcelona,
Valencia, Sevilla, Bilbao y Leon -datos de 1994-) y si se aplica a la  formula
de uniones estos se reducen a 15.

Las  uniones  entre  centrales terciarias se llaman secciones  cuaternarias  o
grandes rutas nacionales.

#######################################
#2 RED JERARQUICA Y RED COMPLEMENTARIA#
#######################################

2.1 RED JERARQUICA.SECCIONES FINALES Y RUTA FINAL
#################################################

La  red  jerarquica  se  define  como el conjunto de estaciones de  abonado  y
centrales   automaticas  unidas  entre  si;  asi  depende  de  una   categoria
inmediatamente superior, estando las de maxima categoria unidas entre si.

La linea de abonado, seccion primaria,  seccion secundaria, seccion terciaria y
seccion  cuaternaria  son  las  uniones  por red  jerarquica  entre  centrales
(secciones finales).

Ruta final, son las secciones finales para unir dos abonados en red jerarquica,
y solo hay una unica ruta final en la conexion entre 2 abonados.

2.2 RED COMPLEMENTARIA.SECCIONES DIRECTAS.CENTRALES TANDEM
##########################################################

A  pesar de que  la ruta final  entre 2 abonados es  unica se podra enrutar la
llamada de forma mas corta siendo mas economico y con mejor servicio.

Esto  se  hace a  traves de la  red complementaria, que se superpone y conecta
a la red jerarquica.

La  red  complementaria esta compuesta de  secciones directas dentro  de ellas
estan las centrales TANDEM.

Las secciones directas son un conjunto de enlaces que unen 2 centrales que por
la logica de la red jerarquica no deberian estar unidas.

El  enrutamiento mediante secciones directas  es mas corto que entre secciones
finales.

Las  secciones directas pueden darse entre  centrales primarias  y secundarias
entre si.

Secciones directas pueden darse entre centrales de distinto rango, siempre que
no difieran en la jerarquia de mas de un grado.

Por lo que se permiten las siguientes secicones directas:

de local a local,                               |
de primaria a primaria,                         | Poseen la misma jerarquia
de secundaria a secundaria,                     |


de local a primaria,                            |
de primaria a seciundaria,                      | Difieren solo en un grado
de secundaria a nodal                           |

El hecho de que esten permitidas depende de un estudio previo.

Es raro que existan secciones directas que no  cumplan las condiciones, pero
pueden darse (de local a nodal o de primaria a nodal).

Las centrales  tandem son centrales  de  transito (sin abonados)  a las que 
se conectan  otras  centrales (sin que las centrales tandem pertenecezcan a
la red jerarquica).

Pueden ser de dos tipos: urbana e interurbana.

La existencia de la red complementaria hace que el camino entre los abonados
ya no sea unico sino que hay varios caminos entre los que las centrales
tendran que decidir el enrutamiento mas adecuado.

La red complementaria se encuentra tan extendida que para ciertos tipos de
trafico cursa la mayoria de las llamadas.

###################################################################
#3 CATEGORIAS DE LAS CENTRALES.AREAS UNICENTRALES Y MULTICENTRALES#
###################################################################

#########################################
#FUNCIONES Y CATEGORIAS DE LAS CENTRALES#
#########################################

3.1 FUNCION Y CATEGORIA DE LAS CENTRALES
########################################

Segun el tamaño, el  emplazamiento (zona  rural  o  urbana), y tipos de trafico 
existen varios tipos de centrales locales, de centrales primarias...denominados
con nombres diferentes.

3.2 RED RURAL
#############

Se organiza en base a una areas primarias denominadas sectores.

Los sectores son areas primarias rurales cuya cabecera es una central primaria
conocida como central de sector.

Numero de sectores: 356 ( unas 7 provincias )

La central primaria esta ubicada en la poblacion mas importante del sector a
ellas se conectan por red jerarquica las centrales locales,que se ocupan de los
abonados situados en poblaciones mas pequeñas (centrales terminales).

Funcion de la central primaria: cursar las llamadas en transito desde las
centrales terminales.

La central de sector tiene una doble funcion:
+de central primaria como cabecera de su sector.
+de central local para los abonados de su poblacion.

Pueden existir  secciones  directas entre  Centrales de Sector o  Centrales  de
Transito  Sectorial de  una provicia con Centrales de  Sector  o  Centrales  de
Transito  Sectorial  de  otra,  inclusive  con  la  C A I  ( Central Automatica
Interurbana, un poco mas adelante la veremos ) de otra provincia.

Los tipos de centrales son:

 central de sector (c.s)
 =======================
 Central primaria de  la que dependen centrales  locales (terminales)  situasen
 distintas  poblaciones. Ejerce  como  central local  para los abonados  de  su
 poblacion.

 central de transito sectorial (c.t.s)
 =====================================
 Central  primaria  de  la que  dependen  centrales locales (terminales) que se
 encuentran en la misma o distintas poblaciones.A ella no se conmectan abonados
 directamente.

 central terminal (c.t)
 ======================
 Central local que conecta abonados de una o varias poblaciones, por lo general
 pequeñas.
 Depende de una central primaria ( C.S  o  C.T.S ) emplazada  en  una poblacion
 distinta.

Exiten otro tipo de centrales rurales que son menos usales:

 central subsector
 ------------------
 En  principio  es una c.t  capaz  de  realizar  transitos entre  otras c.t  del
 sector cuando con ella se ahorra circuiteria.

 central de sector principal
 ---------------------------
 En principio es una c.t capaz de realizar transitos entre otras c.t del sector
 cuando con ellos se ahorra circuiteria.

Su categoria es la de central primaria.


Abonado            Abonado                                             /Abonado
       \              |                                   /CentralTerminal
     CentralTerminal-CentralDeSector-CentralTerminalDeSector           /Abonado
       /                    |                             \CentralTerminal
Abonado                   Abonado                                      \Abonado

3.3 RED URBANA.AREAS UNICENTRALES Y MULTICENTRALES
##################################################

El area unicentral es el area de servicio de una central que debido a la  escasa
demanda existente solo existe ella en la poblacion.

Esas centrales locales se  denominan centrales urbanas, pese a que su categoria
en la red jeraquica sea como la de las centrales terminales.

Se caracterizan por el numero de abonados es mayor, dependen de una central con
funcion  de  primaria  situada en la  misma poblacion; sus  caracteristicas  de
uniones de Red Complementaria son distintas.

Como norma, siempre que el numero de centrales urbanas de una poblacion  no sea
alto, todas  ellas  se interconectaran  con todas las demas de  su area  urbana
mediante secciones directas.

Cuando el numero  de secciones directas necesario para unir todas las centrales
urbanas  entre si  es tan  elevadose denomina Red Urbana Multicentral Compuesta.
Esta consta de 2 zonas: Zona Interior y Zona Exterior.

La  estructura  de  la  zona  interior  es analoga a la Red Urbana Multicentral
Simple,  dado que la zona interior  corresponde  a  las  centrales urbanas  mas
antiguas  cuando  su  numero  era  lo  suficiente  como para  poder conectarlas
mediante secciones directas.

De  las centrales tandem  dependen  las urbanas, la  mayoria  eran "rotary"  un
sistama  muy  antiguo que actualmente  creo que ninguna  central  utilice  (era
mecanico), aunque  he leido  que en Barcelona  hasta hace poco  habia alguna...
este sistema tiene mas de 50 años..

Tipos de centrales:

+central urbana:
Es  una central local con mayor  capacidad que una central terminal. Realiza la
conexion  entre  abonados de una  misma poblacion. Depende de una  centarl  con
funcion  primaria  aunque puede ser  una secundaria,  que este emplazada  en la
misma area urbana

+central tandem urbana:
Central primaria de la que solo dependen centrales urbanas de la zona  exterior
de un area urbana multicentral compuesta.

+central tandem interurbana:
Central de transito,que realiza funciones:
-De central  tandem urbana para diversas centrales  terminales de su mismo  area
metropolitana.
-De  central  de  sector para  centrales  terminales  situadas fuera  del  area
metropolitana y/o central automatica fuera del area metropolitana.

Su categoria es de central primaria.


3.4 TRAFICO INTERPROVICIAL. LA CAI Y LA NODAL
#############################################

La CAI (centerl Automatica Interurbana) conecta por red jerarquica las cabeceras
de los sectores y por via jerarquica a las centrales urbanas de su area urbana,
con esto queda resuelto el trafico telefonico dentro del area secundaria (de la
provincia).

Otra mision de la CAI es la de cursar trafico interprovincial.


Las funciones  de la  CAI  puede  hacerse  con  dos  centrales  distintas,  una
especifica  del transito provicial,  la CAP (Central  Automatica  Provincial) y
otra  dedicada al  trafico  nacional o interprovincial  denominada CAN (Central
Automatica Nacional).

Los tipos pueden ser:

Central Automatica Interurbana (CAI):central  secundaria  encargada del trafico
de transito  destinado o procedente  a las primarias o locales  que dependen  de
ella, tanto si el trafico es provincial como interprovincial (nacional).No tiene
abonados conectados directamente.

Central Automatica Nacional (CAN): central secundaria que  cursa el trafico  de
transito nacional (entre centrales dependientes de ella), situadas en la  misma
provincia  y  centrales  situadas en provincias distintas. No cursa  trafico de
transito entre centrales que de ella dependen.

Central Automatica Provincial (CAP): central  secundaria, que  solo  cursan  el
trafico que de ella dependen (provinciales).

Central Nodal: central terciaria a traves  de la cual conectan varias centrales
secundarias de una region y se dirige el trafico a otras regiones nodales.



2.- Conmutacion telefonica

Es la conexion de unos usuarios con otros, es realizada por las
centrales, mas en concreto por el equipo de conmutacion.

El abonado a traves de su terminal indica el numero de telefono con el
que quiere contactar, la peticion la recive su central local que
habilitara un enlace entre ella misma y la central destino o central que
interconecte con la central destino.

Los enlaces pueden ser de distinto tipo:

+ saliente 
+ entrante
+ en transito
+ local

Si se utiliza un enlace de tipo bidireccional, no se puede realizar el
servicio de llamada entrante o saliente en el mismo instante.

RED DE CONEXION
===============

Es el conjunto de circuitos electromecanicos o electronicos que forman
la unidad de conmutacion, constituyendo el soporte basico de la
conexion.

Esta formado por un numero determinado de puntos de cruce necesarios
para la comunicacion.

- Clasificacion -

Segun la señal que conmute sera analogico o digital.

Segun el tipo de conmutacion podra ser:

- Red espacial
- Red temporal
- Red espacio-temporal

Lo que actualmente se utiliza es la red espacio-temporal.
El sistema europeo consiste en Modulacion por impulsos codificados junto
la multiplexacion en el tiempo.

Utilizando redes espacio-temporales se logra dar servicio a mas abonados
con menor numero de equipos.

Para multiplexarse se crea una trama de 125 microsegundos de duracion
con 32 canales (3.9 ms cada uno). La velocidad es de 2Mb.


            | Muestreo: toma una muestra cada 125 microseg.
            |
TECNICA MIC < Cuantificacion: mediante un logaritmo cuantificador
            |
            | Codificacion: 8 bits

Se toma un canal y durante 3.9 microseg. se lleva a la salida, despues
se toma el siguiente canal...

Los canales 1 y 16 no son de conversacion, sino de alinenacion y 
señalizacion de la trama respectivamente


UNIDAD DE CONTROL
=================

Son los circuitos encargados de la seleccion de puntos de cruce para que
se pueda realizar la llamada.

Se encarga del encaminamiento de de las llamadas a traves de puntos de
cruce libres para llegar al destino (numero de telefono marcado).

- Funcionamiento -

1.- Etapa de concentracion

Se reduce el numero de circuitos entrantes a la unidad de control segun
el trafico (o volumen de llamadas). 

A la relacion entre el numero de entradas y de salidas se le conoce como
indice de concentracion

2.- Etapa de distribucion

Se reciven los circuitos de la unidad de conrtrol para realizar las
conexiones sin eliminar los circuitos.

3.- Etapa de expansion

Se relacionan los circuitos de la unidad central con las salidas
requeridas.

- Control de los sistemas de control -

-------------------------------> Analogicos <-------------------------------

A) Progresivo

Realiza el encaminamiento sin tener en cuanta la etapa de conmutacion
siguiente.

El principal inconveniente es la saturacion.

B) Comun

Selecciona todo el camino de la comunicacion teniendo en cuenta la
siguiete etapa de conmutacion.

-------------------------------> Digitales <-------------------------------


Existen 3 metodos para realizar el camino de la comunicacion,
tarificacion de la llamada, control de intensidad, saturacion (volumen
del trafico), ayuda de mantenimiento...

A) Logica cableada

Se sustituyen los elementos electromecanicos por elementos electronicos,
reduciendo mantenimiento y consumo. Se debia de cambiar toda la
circuiteria, lo que lo hacia costoso y nunca se llevo a cabo.

B) Control por programa almecenado (SPC)

Se desarrollo un programa que almacenase en memoria y controlase los
puntos de cruce. El software era facilmente actualizable con lo que se
ganba en flexiblidad.

** SPC centralizado **

El procesador tiene acceso a todos los recursos del sistema (la central)
y se encarga de realizar todas las funciones de la conmutacion.

Generalmente se dispone de dos micros por si uno falla.

** SPC distribuido **

Solo se tiene acceso a unos determinados recursos, solo se realiza las
funciones de una parte del sistema. Para poder gestionar toda la central
se necesitan varios micros, cada uno se ocupa de unas funciones.

Esto es lo mas normal, pues el funcionamiento de la central no depende
de uno (o dos) micros; si uno de ellos cae no implica que la central
deje de funciona solo algun aspecto de ella.

Otra ventaja es que se dispone de un sistema modular al que es facil
añadirle nuevas funciones, caracteristicas..

< > Clasificacion de los sistemas automaticos de conmutacion < >

Clasificacion en funcion a la unidad de control y red de conexion:

[ Mecanicos ]

- Rotatorios:
Basados en filas y columnas, a este tipo pertenecen las Rotari.


[ Electromecanicos ]

-Sistema crossbar
Consta de:
  multiselector emisor
  mallas
  receptor
  traductor

* Pentaconta 1000 (crossbar)
* ARD

[ Semielectronicos ]

Tienen una red de conexion electromecanica y una unidad de control
electronica.

Pentaconta 2000

[ Electronicos ]

Red de conexion y unidad de control electronicos, todo el sistema es
digital.

AXE                   de Ericsson
5ESS                  de AT&T (si, tiene UNIX dentro :D)
1240                  de alcatel

-- 1240 Alcatel --

Red de conexion digital y espacio-temporal y esta controlada por
programa almacenado distribuido.

                 ** Modulos de 1240 **

= Modulo interfaz (Unidad Remota de Abonados) =
Conecta abonados lejanos y los que no tienen medio fisico con la central
(inalambricos).

= Modulo interfaz de datos =
Conmutan datos en modo paquete y modo circuito.

= Modulos de enlace digital =
Da servicio a los enlaces digitales (120 abonados). Utiliza la tecnica
MIC con 16 bits por intervalo comunicandose a 4Mb.

= Modulo Digital de Abonado =
Da servicio a 128 abonados (no todas las centrales dan servicio a este
tipo de abonados).

= Modulo de Enlaces Analogicos =
Los necesarios para dar servicio a los enlaces de la central

= Modulo analogico de abonados =
Da servicio a 128 abonados, funciones basicas de linea.

= Modulo de Reloj y Tonos =
Marca la velocidad de trabajo (8.192 Mhz), tambien indica los tonos de :

- aviso de llamada
- linea ocupada
- timbre

Suelen tener dos de estos modulos.

= Modulo de Perfifericos y de Mantenimiento =
Aviso de alarma ante fallos. Pantallas, cintas, discos... para
mantenimiento de la funcion. Se suelen tener dos modulos.

= Modulo de Canal Comun =
Sistema de señalizacion por canal comun (SSCC#7) que se utiliza para la
señalizacion entre centrales.

= Modulo de Circuitos de Servicios =
Capacidad de 32 circuitos de servicio (emisores/receptores)

= Modulo Interfaz Operadora =
Hasta 15 posiciones de operadora.

>> Circuiteria auxiliar <<

Es la circuiteria necesaria para que funcionen los modulos.
Funciones de control del micro 8086, unidad interfaz de terminal, una
memoria y un reloj.

>> Circuitos <<

De enlace
De sincronizacion
De reloj

Para programar esta central se utiliza el lengueje CHILEN


FUNCIONES BASICAS DE UN CANAL DE COMUNICACION
=============================================

Interconexion: interconectado con los nodos.

Control: junto con la anterior es la funcion mas basica. Establece el
mantenimiento y liberalizacion del camino.

Supervision: se encarga de la supervision de:
	- lineas de abonado y enlace
	- camino de la conversion

- Señalizacion con abonados -

- Tono de invitacion a marcado
- Tono de llamada (camino libre). 400 Hz
- Tono de ocupado. 400 Hz
- Tono de error o comunicacion no completado. 400 Hz
- Aviso de llamada 25 Hz y hasta 75 v
- Llamada en espera 100 Hz
- Tono de tarificacion 12 KHz

- Señalizacion abonado > red -

Teclado decadico (usa pulsos)
Teclado MF (usa tonos)

- Señalizacion entre centrales -

+ Almacenamiento y analisis de la informacion recivida (depende del
entrada(solicitado, detectado, ocupado).

+ Asignar enlace de salida de la central distante

+ Recivir informacion (al pulsar determinados numeros)

+ Almacenamiento y analisis de la informacion recivida (depende del
sistema de conmutacion).

+ Seleccion y conexion: busqueda de un enlace de salida libre y
activacion.

+ Explotacion : tarificacion y consumo.

+ Sincronizacion: medidas de tiempo para cada paso del sincronismo.

+ Temporizacion: conseguir que todas las centrales actuen al mismo
tiempo (frecuencia de reloj).

+ Conmutacion de paquetes

PROTOCOLOS DE COMUNICACION
==========================

Las vias que utilizan los modulos para comunicarse son de 4 Mb, que
vienen generados por que cada canal consta de 16 bits.

Los dos primeros bits son del protocolo de comunicacion, sirve para
distinguir el tipo de informacion que viaja, y son 4:

- 00 borrado (enlace liberado)
- 01 seleccion (la conmutacion a realizar)
- 10 datos (contiene el mensaje)
- 11 Informacion 

EL CONMUTADOR
=============

Esta constituido por circuitos integrados, se llamaran puertos de
conmutacion y estan unidos por un BUS multiplexado en el tiempo.

Cada uno de los circuitos esta formados por dos puertos independientes
entre si. La funcion es la de recivir una señal (MIC) analizarla,
memorizarla y realizar la conmutacion para de salida por otro puerto.
Todos los puertos se sincronizan en la misma frecuencia de 8.192 Hz.

Un puerto puede llegar a realizar 16 conmutaciones, ya que son 16 las
lineas MIC que llegan.

PLANTA EXTERIOR
===============

La compone toda la planta telefonica situada en el exterior de los
edificios que albergan los edificios de equipos de conmutacion...

Red de enlace.- son la uniones entre centrales que permiten la conexion
de diferentes abonados de diferentes centrales. Pueden ser:

  urbanas : no salen del area primaria
  interurbanas : traspasan el area secundaria.

Red de abonados.- conjunto de elementos que permiten la conexion
electrica entre los equipos de abonados (si, los telefonos..) y la
central local.

Repartidor de abonador.- elemento que limita la planta exterior de los
sistemas de conmutacion. Se distingue:

  armazon: estructura metalica que soporta todos los elementos del
           repartidor.

  lado vertical: dispone de regletas donde se realiza la terminacion de
                 pares.

  lado horizontal: terminacion de lineas de abonado.

  hilos puente: comunican la red externacon la central.

  punto de interconexion: elemento flexibilizador de la red, conecta con
                          cualquier salida.

  punto de distribucion: ultimo punto de la red a partir del cual se
                         distribuyen los pares a los abonados.

  cable terminal: permanece en la central (desde el repartidor a los
                  equipos de conmutacion) 

  cable de alimentacion: une el cable terminal con los puntos de
                         interconexion.

  cable de acometida: entre el punto de dsitribucion y la caja registyro
                      del inmueble.

  red de dispersion: conjunto de cables de acometida



INTELIGENCIA DE RED
===================

Rediris es una red digital superpuesta a la red de telefonia basica. Se
encarga de muchas cosas, entre ellas de la gestion de numeros
especiales.

900 -> cobro revertido automatico
901 -> llamada compartida
902 -> paga el abonado que llama (numero universal para la SAT)

904 -> desvio personal (antes 082)
905 -> llamadas apsivas (encuestas, concursos..)
       9051 -> tarificacion especial
       9055 -> cantidad de pasos independiente del tiempo
906 -> linea de interes

083 -> llamada a cobro revertido (llamada a credito)

CIR (centro de inteligencia de red)
-----------------------------------

Se encarga de centralizar las funciones de inteligencia. Esta formado
por un procesador que gestiona una base de datos (pedazo base de datos!)
en tiempo real, lo que le permite gestionar los servicios de la red.

El funcionamiento en una llamada especial es el siguiente:
Llamanos al numero de telefono especial, que por el prefijo se nos
conmutara la llamada a una central especial, el CIR recoje la peticion
que pregunta al AIR (que en un momento veremos) para indicar el
tratamiento que debe de darse a cada llamada, a la vez se comunica con
el CAS el cual nos da la informacion del plan de abonados.

AIR.- (Agencia de Inteligencia de Red)centrales digitales de conmutacion
que realizan la funcion de transito e interconexion entre la RTB y
REDIRIS.

Realiza funciones basicas a nivel local, pero la mayoria de los
servicios los ha de consultar al CIR, reteniendo la llamada.

Estas centrales estan formadas por tres tipos de modulos:

- Modulo de conmutacion
- Modulo de comunicacion
- Modulo de administracion

FE.- modulo de funciones especiales, se encarga de las funciones basicas
para no cargar a la AIR y liberarla de trabajo. 

Ej: locucion, reconocimiento de voz, recepcion de tonos..

Los modulos estan formados por bases de datos.

CAS.- es unico en toda la red; es el centro de administracion de
servicios. Mediante este servicio se permite acceder a la red mediante
los CIR, para la modificacion de parametros (tarificacion, servicios..).
Se conecta a tarjetas de las AIR.

SERI.- (Sistema de Explotacion de la Red) permite realizar las funciones
de operacion y mantenimiento, hace comprobaciones globales de todo el
sistema (mediciones, alarmas..).

SGR.-(Sistema de Gestion de la Red) es unico, gestiona el trafico,
supervisa las AIR y a los enlaces. Se conecta a tarjetas de las AIR.
```