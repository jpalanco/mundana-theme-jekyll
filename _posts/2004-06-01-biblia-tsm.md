---
title: "Biblia del TSM"
date: "2004-06-01"
image: assets/images/tsm100.jpg
author: jpalanco
layout: post
tags: [ tsm, moviles, hacking ]
categories: [ old-school ]
---

El año 2003 salió al mercado el móvil TSM30 de Vitelcom un móvil con muchas prestaciones desarrollado por una empresa española a un precio muy razonable. Antes del TSM30 habían salido el TSM100, un teléfono similar pero con pantalla táctil resistiva.
Estos móviles crearon una comunidad de usuarios en España y sucedieron cosas muy interesantes. Pero lo que sin duda hace especial a este móvil, es que fue la primera vez que se filtraba el stack GSM así como el código de un DSP (TI Calypso). Este leak
se atribuye al grupo ?Hispaphreak, que colgó en el (por aquel entonces famoso) portal de proyectos libres Sourceforge, todo el código fuente. Al no percatarse nadie durante tantos años, inmediatamente el código pasó a considerarse de DOMINIO PÚBLICO.
Gracias a esta aportación de este grupo de hackers españoles, surgieron proyectos como OpenBSC, OpenBTS, OsmocomBB...

![tsm30]({{ site.baseurl }}/assets/images/tsm30.jpg)


# Características del terminal TSM30 205

## Sistema
- Sistema Operativo: Propietario
- Almacenamiento: 2 MB
- Tarjeta: MMC/SD Imagen tarjeta MMC/SD
- J2ME: SI

## Pantalla

- 160x128 pixels, 65k colores


# Cámara

- 0,3MP (640x480 Pixels)

## Otros datos

- Calendario: SI
- Vibración: SI
- Radio: NO
- Observaciones: I-Mode,SD/mmc
- SAR: 0,95 W/kg (cabeza)


## Redes

- Banda: 2G: GSM 1800, GSM 900, GSM 1900
- GPRS: SI

## Batería

- Autonomía (Llamada): 2,3 h (GSM)
- Autonomía (Espera): 180 h (GSM)
- Bateria: Li-Ion
- Extraíble: SI

## Aspecto

- Dimensiones: 113x48x21 mm
- Peso: 110 gr
- SIM: SIM

## Comunicaciones

- Bluetooth: NO
- NFC: NO
- IrDa: SI
- USB: SI
- WIFI: NO
- GPS: NO
- Mensajes: SMS/EMS/MMS


# Entorno de desarrollo

El código del firmware está completamente escrito en C, para compilarlo desde las [fuentes, que están disponibles en Internet](http://cryptome.org/tsm30/tsm30.7z) necesitaremos instalar algunas utilidades de Texas Instruments, o bien descargarnos el entorno de desarrollo que sólo funciona en sistemas compatibles con NT (Windows NT, 2000, XP,2003).

 Dentro del zip no solo encontraremos el fuente del firmware, sino también los compiladores necesarios (TEXAS INSTRUMENTS) para construir el firmware.

El código está muy bien organizado y documentado. Podemos encontrar diferentes directorios clasificados. Quiero destacar que en el proyecto se compilan objetos tanto para la MCU (MicroController Unit) como para el DSP (Digital Signal Processor). Como podéis imaginar el sistema operativo se ejecuta sobre la MCU y la Baseband en el DSP.

Para montar las unidades con los compiladores, ejecutaremos el fichero mount.bat. Esto nos montará 3 unidades:
- R:
- S: 
- W: 

Nos encontraremos un fichero llamado Official.zip, es el que contiene el código fuente propiamente dicho. Deberemos de descomprimirlo (asegurándonos de que las propiedades no son de solo lectura) y montarlo como V: de esta manera:

```
subst V: Official
```

Para compilar el firmware, solo debemos ir a V:\Common\INTEGRATION\bin y ejecutar dmakeall.bat

## definicion de prototipos de internos

```cpp
#if (MODULE_NUMBER == MODULE_PKRN) 
```

## Comunicaciones

Las rutinas de comunicación GSM están en el directorio **MCU\Layer1** y **MCU\Protocol** con algunas definiciones en **MCU\inc\cdg**

Las estructuras de las estramas se pueden encontrart en **spy_decoding.ini**

Por ejemplo, podemos ver que soporta para "Progress indicator information element" estos valores:

```cpp
LOC_USER 0x0 /* user */
LOC_PRIV_NET_LOCAL_USER 0x1 /* private network serving the local user */
LOC_PUB_NET_LOCAL_USER 0x2 /* public network serving the local user */
LOC_TRANSIT_NET 0x3 /* transit network */
LOC_PUB_NET_REMOTE_USER 0x4 /* public network serving the remote user */
LOC_PRIV_NET_REMOTE_USER 0x5 /* private network serving the remote user */
LOC_INTERNATIONAL_NET 0x7 /* international network */
LOC_BEYOND_POINT 0xA /* network beyond interworking point */
LOC_GNOLZ_1 0x1 /* reserved */ 
```

Lo cual quiere decir que sí admite el valor 0x3, y lo tratará con el significado de "transit network", aunque luego el programa en
**MCU\Protocol\CC\Src\CC_FFK.C** la maneja como si fuera lo mismo que LOC_PUB_NET_LOCAL_USER.  Transforma LOC_TRANSIT_NET en LOC_USER. 


# Hola Mundo

Bueno, ya que nos hemos familiarizado con el entorno de desarrollo del móvil, vamos a hacer alguna practica... y... ¿Que mejor que "Hola mundo"?

Nos moveremos al directorio V:\MCU\Presentation\Idle\Src y abriremos pidl04debug.hv que contiene definiciones de utilidades de depuración. Aquí podremos capturar un código introducido por teclado y lanzar la aplicación que queramos (nuestro "Hola Mundo")... y bueno, como vosotros sois muy l33t y hax0rs... pondremos "##31337" como código que de acceso a nuestra aplicación.

```cpp
typedef struct {
char * p_KeySeq;
t_pidl_KeyFunction * p_Func;
} st_pidl_KeyTable;


GLOBAL_EXT const st_pidl_KeyTable tabla[]
= {
"##31337", pidl04_nuestra_funcion,
/*
...
...
...
*/
NIL, pidl04_06UnknownSeq
};
```



Ahora vamos a crear nuestra_funcion() añadiendo las siguientes líneas a pidl04debug.c :


```cpp
u8 pidl04_nuestra_funcion(char *pp_String)
{

pcom02_11SimpleTimedBox((u8 *)"Hola Mundo", (u8 *)"l33t Msg", PPMT_EOL_DUMMY_PROMPT_SPT2, PPMT_EOL_DUMMY_PROMPT_SPT2, 0 );

return (TRUE);
}
```


Las interfaces de usuario para confirmación están definidas en V:\MCU\Presentation\Common\Src\pcom02cfirm.c :

```cpp
void pcom02_01EasySettingMessageBox( st_MsgBoxPZ *pl_MsgBox );
u16 pcom02_09SimpleMsgBox( u8* p_Text, u8* p_Title, t_PromptId v_Text, t_PromptId v_Title, u32 v_Flags );
u16 pcom02_10SimpleBox( u8* p_Text, u8* p_Title, t_PromptId v_Text, t_PromptId v_Title, u32 v_Clear );
u16 pcom02_11SimpleTimedBox( u8* p_Text, u8* p_Title, t_PromptId v_Text, t_PromptId v_Title, u32 v_Clear );
u16 pcom02_12SimpleYesNoBox( u8* p_Text, u8* p_Title, t_PromptId v_Text, t_PromptId v_Title, u32 v_Clear );
u16 pcom02_13SimpleInfoBox( u8* p_Text, u8* p_Title, t_PromptId v_Text, t_PromptId v_Title, u32 v_Clear );
u16 pcom02_14SimpleWarningBox( u8* p_Text, u8* p_Title, t_PromptId v_Text, t_PromptId v_Title, u32 v_Clear );
u16 pcom02_15SimpleYesNoCancelBox( u8* p_Text, u8* p_Title, t_PromptId v_Text, t_PromptId v_Title, u32 v_Clear );
u16 pcom02_16SpecialTimedBox( u8* p_Text, u8* p_Title, t_PromptId v_Text, t_PromptId v_Title, u32 v_Clear, u8 vp_DisplayAttributes );
u16 pcom02_17SimpleGoPostponeDeleteBox( u8* p_Text, u8* p_Title, t_PromptId v_Text, t_PromptId v_Title, u32 v_Clear );
u16 pcom02_18SimpleSilentBox( u8* p_Text, u8* p_Title, t_PromptId v_Text, t_PromptId v_Title, u32 v_Clear );
u16 pcom02_19SimpleSilentTimedBox( u8* p_Text, u8* p_Title, t_PromptId v_Text, t_PromptId v_Title, u32 v_Flags ) ;
u16 pcom02_20SimpleBoxGo( u8* p_Text, u8* p_Title, t_PromptId v_Text, t_PromptId v_Title, u32 v_Flags, st_MsgBoxPZ *pl_MsgBox );
u16 pcom02_23SimpleIconTimedBox ( u8* p_Text, u8* p_Title, t_PromptId v_Text, t_PromptId v_Title, t_IconId v_Icon, u32 v_Flags );
u16 pcom02_24SimpleBoxWarm( u8* p_Text, u8* p_Title, t_PromptId v_Text, t_PromptId v_Title, u32 v_Flags );
u16 pcom02_26ExitAndDiscardNotif( void );
u16 pcom02_27DeleteConfirmation( void );
u16 pcom02_99MsgBoxTest( u8* p_Text, u8* p_Title, u8* p_But );
u16 pcom02_25OneButton( u8* p_Text, u8* p_Title, t_PromptId v_Text, t_PromptId v_Title, u32 v_Flags );
u16 pcom02_26ExitAndDiscardNotif(void);
u16 pcom02_27DeleteConfirmation(void);
u16 pcom02_28DeleteAllConfirmation(void);
u16 pcom02_29PleasePowerCycle(void);
u16 pcom02_30FileSystemFull(void);
u16 pcom02_31MemoryCheckAndNotify(u8 * pp_Level, u8 * pp_Percentage);
```

Si queremos trabajar con buffers que el usuario copia y desea pegar usaremos las siguientes funciones:

- _globext_ u8 pcom03_01Copy ( t_BufferType vp_BufferType, void *vp_Data, u16 vp_Size );
- _globext_ t_BufferType pcom03_02Paste ( void **pp_DataPtr, u16 *pp_SizePtr );
- _globext_ void pcom03_03InitialiseClipboard ( void );
- _globext_ t_BufferType pcom03_04IsBufferData ( void );
- _globext_ u8 pcom03_05IsBufferLocked ( void );
- _globext_ void pcom03_06LockBuffer ( void );
- _globext_ void pcom03_07UnlockBuffer ( void );
- _globext_ u8 pcom03_08CanCopy ( u8 a, u16 b, st_HandlerControlBlock *c );
- _globext_ void pcom03_09LaunchTimeoutTimer ( t_TimeoutContext ) ;
- _globext_ void pcom03_10StopTimeoutTimer ( t_TimeoutContext ) ;



# Introducción GSM/GPRS/I-MODE


Cada vez que encendemos un móvil se nos presenta en pantalla una invitación (CHV1) a meter el PIN1 que nos permitirá entrar a la red GSM. Este Personal Identification Number no necesita de la red telefónica móvil, sino que su validación la hace la propia tarjeta SIM.

Para hacer otras cosas como cambio de opciones una vez estamos conectados a la red (CHV2) deberemos de usar el PIN2, pero no es necesario conocerlo para un uso normal en la red.

El proceso de acceso a la red lo inicia el móvil una vez el usuario ha introducido el PIN correctamente; en ese momento el movil recibe de la red el RAND, que es un numero aleatorio (RANDOM) que utiliza junto con el Ki para generar claves SRES y Kc.

El Ki (Internal Key) es un numero almacenado en la SIM al que no se tiene acceso directo desde el terminal móvil, sin embargo las operadoras tienen una base de datos con los Ki’s en el AC (Authentication Center).

El SRES (Result) es devuelto a la red para completar el sistema de autenticación y es generado con el Ki y el RAND.

El Kc (ciphering key) se genera con el algoritmo A3, y nos servirá como clave para cifrar las comunicaciones cuando la red disponga el cifrado activo. Al igual que el SRES, el Kc se genera con el Ki y el RAND. El 11M muchos teléfonos móviles de la compañía MoviStar avisaban de que no se estaba utilizando ningún tipo de cifrado por razones que somos todos capaces de imaginar.

El IMSI (Mobile SUbscriber Identification Number) es un numero nos identifica mundialmente como abonados a una red de una operadora de telefonía móvil. Se compone de MCC, MNC y MSIN.

MCC (mobile country code) es el identificador de la red de un país y consta de 3 dígitos. MNC (mobile network code) es el identificador de una red de una operadora, se forma a partir de 2 dígitos. MSIN (mobile subscriber identification number) numero de identificación del abonado (no tiene porque coincidir con el MSISDN, o sea, el numero de teléfono del abonado que nos lo asigna la red cuando ha comprobado los datos), y se reservan 10 dígitos para el.

La mayoría de los móviles se fijan en los primeros 3 dígitos del IMSI (que indican el país) para mostrar los menús en uno u otro idioma.

El TMSI es el tiempo que debe ejecutar una actualización de localización para informar a la red de la disponibilidad de nuestro terminal móvil.
