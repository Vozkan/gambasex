 [DOCS](exdocu.md) - [DIFF](exdiferenciasoriginal.md) - [GIT](https://gitlab.com/venenux/gambasex) - [LICENSE](https://gitlab.com/venenux/gambasex/blob/master/LICENSE.md)

# exModulos documentacion

Este documento solo documenta los modules estaticos, consulte [exdocu.md](exdocu.md).
Se pueden invocar directamente (estaticos) sus funciones en los "exModulos".

* [emi] (#emi) : ExModSysInfo, funciones de informacion del sistema
* [emf] (#emf) : ExModSysfile, funciones de manejo de archivos
* [emn] (#emn) : ExModSysNet, funciones e informacion de red
* [emu] (#emu) : ExModSysUtils, manejo y manipulacion de variables

## emi
 
Funciones utilitarias de informacion del sistema instalado ejecutandose.

* `itsRunIDE() As Boolean` : retorna `True` si esta ejecutando elprograma como cgi o aplication, -1 si en el ide. 
* `cmd_checks(aCommands As String[], Optional bDisplayDialog As Boolean = False) As Boolean` : retorna verdadero si todo lo requerido en array esta instalado o presente
* `cmd_exits(sCommand As String) As Boolean` : devuelve el nombre del comando si existe, sino null

## emf
 
Funciones utilitarias de manipulacion de archivos

* `CharacterSets() As String[]` : deveulve un arreglo con los tipos de codificaciones soportadas por el sistemaoperativo y su softwareinstalado
* `getMimeEncoding(sFilePath As String) As String` : devuelve el tipo de archivo si es texto plano o binario
* `getMimeType(sFilePath As String, Optional ruta As String = "") As String` : devuelve el tipo de archivo en forma mime ambito/tipo la ruta debe ser absoluta, sino entonces asume raiz dcel proyecto
* `getFileDev(Optional ruta As String = "") As String` : devuelve el dispositivo o disco, segun ruta, sino el del sistema de ficheros raiz, si es mapeado no devuelve el dispositivo real, solo el mapa
* `caltoods(file) As String` : convierte `file` a ods, mismo nombre, ruta siempre /tmp

## emn

Se detecta toda informacion de red usando `/sbin/ifconfig` esto es estandar en linux y mac 
por ende es seguro usar ruta absoluta.

Ofrece ip activa (cual se usa para obetenr los bytes d einternet/red activa)
y las ip configuradas del sistema activas, tambien los dispositivos equivalentes a las ip activas.
Las llamadas de las funciones necesitan `netstat`, `ifconfig`, `awk`, `grep` y `head`, 
los paquetes son al menos en linux: **coreutils** (`cut`,`head`), **net-tools** (`netstat`,`ifconfig`), 
asi como **nawk/gawk** (`awk`), **grep** (`grep`) y **sed** (`sed`), en mac todos siempre estan.
* los paquetes **coreutils** y **net-tools** siempre estaran tanto en linux como en mac.
* los paquetes **nawk/gawk**, **sed**, **grep**, se exige esten instalados en ***modSysInfo*** rutina.

* `getImdef(Optional defIf As String = Me.getIfdef()) As String` : obtener la mac que se usa para enviar y recibir datos en la red/internet de todas las activas<br> si @param defif se provee se usara este dispositivo de red como el activo para optener la ip
* `getIfdef() As String` : obtener la interfaz que se usa para enviar y recibir datos en la red/internet de todas las activas
* `getIpdef(Optional defIf As String = Me.getIfdef()) As String` : obtener la ip que se usa para enviar y recibir datos en la red/internet de todas las activas<br> si @param defif se provee se usara este dispositivo de red como el activo para optener la ip
* `getIfall() As String[]` : obtener todas las interfaces de red activas de las disponibles
* `getIpall() As String[]` : obtener todas las ip/direcciones de red activas de las configuradas

## emu

Se trabaja con manipulacion de variables, comunmente cadenas de texto y enteros.

* `substr_count(strInput As String, pattern As String, Optional compare As Integer = gb.Binary) As Integer` : Count the number of substring occurrences, default is case sensitive
* `ucfirst(strInput As String) As String` : Devuelve un texto con la primera letra en mayusculas y todas las siguientes en minúsculas.
* `ucwords(strInput As String) As String` : Devuelve un texto con la primera letra en mayusculas de cada una de las palabras, removiendo espacios extra
* `urisegment(strInput As String, Optional segment As Integer = 999) As String` : Devuelve el segmento ultimo o parte segun de un uri o ruta dada de archivos
* `urifilepath(strInput As String) As String` : Devuelve la ruta absoluta de un uri que termina en un archivo
* `gethttpbuf(Optional urltogetinfo As String = "") As String`: obtiene todo el contenido de una url en una cadena/buffer para analizar **en crudo**, util para json, xml o para descargar binarios, @parameter url: la uri, @return string html de la respuesta, o string "" si invalido o no hay nada, string "-1" si invalido o agotado en server


