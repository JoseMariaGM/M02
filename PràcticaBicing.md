E3. Ejercicio 3. Transacciones

Introducción
Aunque típicamente las asociamos a entrada por teclado, almacenamiento en archivo, procesado con código y salida por pantalla, este mecanismo actualmente suele darse a partir de datos extraídos de una API (Application Program Interface).

Las API son muy comunes hoy en día. Para que os hagáis una idea mirad cuántas tiene google: https://developers.google.com/apis-explorer/. Estas API permiten que desarrolladores de aplicaciones de cualquier lugar de mundo tengan acceso a datos en tiempo real.
Otros ejemplos típicos son por ejemplo las API meteorológicas. La mayoría requieren de un registro de usuario, a pesar de ser gratuitas, como por ejemplo https://openweathermap.org/api.

Contenidos 

Tenga en esta carpeta diferentes archivos con el paso a paso de un procesado de datos a partir de la api de bicing.
Tomando como partida el archivo general bikesInUse.py que hará toda la transacción, contestar las siguientes preguntas sobre lo que hace y también modifíquelo adecuadamente para lograr el resultado deseado.

Entrega

1.¿Cuál / es paquete / s de los repositorios del sistema operativo necesario instalar y para qué sirven? Debemos instalar el comando "sudo dnf install python3-Tkinter -y".

Con el comando de "sudo dnf install python3 -tkintner -y" te permite dibujar python en un modo gráfico.
 


2. ¿Cuál / es paquete / s de librerías de Python se han de instalar y para qué sirven?
El comando "sudo PIP3 install requests NumPy matplotlib" la libreria matplotlib sirve para que la librería requests nos conecte con direcciones URL.
La librería matplotlib permite hacer gráficas y gestionar sus parámetros a partir de los datos leídos del archivo databicing.csv.


3.Explique qué se hace en cada parte de la transacción de nuestro programa python:

-Entrada: https://www.bicing.cat/current-bikes-in-use.json

-Almacenamiento: databicing.csv

-Procesamiento: dades = numpy.genfromtxt('databicing.csv',delimiter=',', skip_header=1, usecols=(3)

-Salida:  plt.plot(dades)
plt.title('Bicing')
plt.ylabel('Bicis')
plt.xlabel('Temps')

# Generem una finestra on mostrar la gràfica que tenim en memòria.
plt.show()




4.¿Qué deberíamos cambiar el código para que en vez de mostrar las bicicletas totales en uso nos mostrara sólo las bicicletas eléctricas en uso? En "dades = numpy.genfromtxt('databicing.csv',delimiter=',', skip_header=1, usecols=(3))", como el contador de bicis mecánicas es el numero 3, si cambiamos al numero 2, nos mostrará el numero de bicis electricas.



5.Cambie ahora los siguientes parámetros de nuestro programa python y copie aquí el programa completo una vez modificado y comprobado que hace lo que tiene que hacer. También copie aquí los datos que se han almacenado en el archivo:

Haga que haga 30 iteraciones en vez de 10
Cambie el título de la gráfica de 'Bicing' por su nombre y apellidos

Datos almacenados:error,bikesInUsage,electricalBikesInUsage,mechanicalBikesInUsage,dateTime
0,443,2,441,2018-10-22 13:05:38
0,442,2,440,2018-10-22 13:05:40
0,443,2,441,2018-10-22 13:05:41
0,445,2,443,2018-10-22 13:05:42
0,445,2,443,2018-10-22 13:05:44
0,447,2,445,2018-10-22 13:05:46
0,447,2,445,2018-10-22 13:05:47
0,447,2,445,2018-10-22 13:05:49
0,446,2,444,2018-10-22 13:05:50
0,446,2,444,2018-10-22 13:05:52
0,446,2,444,2018-10-22 13:05:53
0,448,2,446,2018-10-22 13:05:55
0,448,2,446,2018-10-22 13:05:56
0,447,2,445,2018-10-22 13:05:57
0,447,2,445,2018-10-22 13:05:59
0,446,2,444,2018-10-22 13:06:00
0,446,2,444,2018-10-22 13:06:02
0,446,2,444,2018-10-22 13:06:03
0,443,2,441,2018-10-22 13:06:05
0,442,2,440,2018-10-22 13:06:06
0,443,2,441,2018-10-22 13:06:08
0,444,2,442,2018-10-22 13:06:09
0,444,2,442,2018-10-22 13:06:11
0,446,2,444,2018-10-22 13:06:13
0,447,2,445,2018-10-22 13:06:14
0,448,2,446,2018-10-22 13:06:16
0,450,2,448,2018-10-22 13:06:17
0,451,2,449,2018-10-22 13:06:19
0,450,2,448,2018-10-22 13:06:20
0,450,2,448,2018-10-22 13:06:22

CÓDIGO FINAL:# coding=utf-8

################################################################################
## Autor: Josep Maria Viñolas Auquer					      ##
## Llicència: AGPLv2                                                          ##
## DESCRIPCIO                                                                 ##
##   Es conectarà 10 vegadas a la api json de bicing en intervals d'un segon  ##
##   i posteriorment mostrarà l'evolució en una gràfica                       ##
## INSTALL LIBRARIES:                                                         ##
##   sudo dnf install python3-tkinter -y                                      ##
##   sudo pip3 install requests numpy matplotlib                              ##
## RUN:									      ##
##   python3 bikesInUse.py                                                    ##
################################################################################


Farem ús de llibreries que contenen funcions que ens seran útils
La llibreria requests ens permetrà conectar amb direccions URL
import requests
La llibreria time té la funció d'esperar uns segons
import time
La llibreria csv ens permet desar dades en format CSV compatible amb
fulls de càlcul
import csv

databicing serà una variable de tipus llista. A la llista hi anirem
desant les dades que ens retorni el web de bicing.
databicing=[]

iteració serà una variable entera que ens servirà per anar comptant
quantes vegades fem el bucle. Inicialment 0.
iteracio=0

El bucle while es repetirà mentre iteracio sigui menor que 10. Per tant
anirà de 0 a 10. Dins el bucle l'incrementarem amb iteracio=iteració+1.
La funció sleep de la llibreria time esperarà 1 segon, sense fer res.
I a la primera linia afegirem el resultat que ens doni el web amb el
requests.get en format json a la llista databicing que hem creat abans.
Al print mostrarem en quin número de petició estem. Fixeu-vos que
convertim el valor enter en un string de caràcters per tal de mostrar-lo.
while iteracio < 30:
	databicing.append(requests.get("https://www.bicing.cat/current-bikes-in-use.json").json())
	time.sleep(1)
	iteracio=iteracio+1
	print("Petició Nº:"+str(iteracio))
	print("  Dades: "+str(databicing[iteracio-1]))

Ara ja tenim les dades a la memòria de l'ordinador, dins la variable
databicing que és una llista. Per accedir a cada petició emmagatzemada
a aquesta llista ho farem amb l'índex, en aquest cas la primera és la 0.
D'aquesta primera petició n'agafarem els títols, que són les claus (keys)
titols = databicing[0].keys()

I aquí el que fem és obrir un fitxer databicing.csv en mode escriptura i
anar-hi desant les dades en format csv
print(databicing)
with open('databicing.csv', 'w') as fitxer:
    punter = csv.DictWriter(fitxer, titols)
    punter.writeheader()
    punter.writerows(databicing)

Hem fet un seguit de peticions al web de bicing mitjançant la tarja de
xarxa i els protocols de xarxa que ens proporciona el sistema operatiu.
Hem anat dient-li al sistema operatiu que desi aquestes dades que rebem
a la memòria volàtil de l'ordinador (RAM) dins la variable databicing.
I finalment li hem dit al sistema operatiu que desi aquestes dades en un
fitxer anomenat databicing.

Ara passarem a llegir les dades i fer-ne una gràfica.

El primer que farem és importar les llibreries que ens facilitaran les
funcions per a fer-ho.
La lliberia numpy ens permetrà llegir les dades del fitxer i desar-les
en un format que ens permeti posteriorment graficar-les
import numpy
La llibreria matplotlib permet fer gràfiques i gestionar-ne els paràmetres
a partir de les dades llegides del fitxer databicing.csv
~ import matplotlib
from matplotlib import pyplot as plt

Llegim les dades del fitxer
dades = numpy.genfromtxt('databicing.csv',delimiter=',', skip_header=1, usecols=(3))
Dibuixem les dades en memòria i posem títols a la gràfica
plt.plot(dades)
plt.title('Jose Mª Gimeno Moreno')
plt.ylabel('Bicis')
plt.xlabel('Temps')

Generem una finestra on mostrar la gràfica que tenim en memòria.
plt.show()
