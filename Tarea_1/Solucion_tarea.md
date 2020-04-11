# Tarea 1 Publicación de mapas web basicos

## Objetivos

•	Utilizar datos geográficos para resolver un problema específico y publicar los resultados en la web para fácil acceso a los usuarios.

•	Publicar mapas temáticos en la web

## Actividades

•	En el repositorio github personal creado para la clase crear una carpeta llamada Tarea_1
•	Dentro de la carpeta Tarea_1 Crear un archivo Readme.md con la siguiente información:
               oCada item tiene un valor de 1 punto si está completo y correcto.
                oEn caso de estar incompleto o incorrecto se otorgará 0 puntos.
 
## Items

 1. **Cual es el problema a tratar ?** 

El departamento de bomberos de la ciudad de Bogotá desea conocer cuales son las localidades donde se presenta más incidentes para poder asignar más recursos económicos con el fin de adquirir equipos nuevos, por lo tanto, a partir del mes de julio del año 2019, empezaron a registrar las coordenadas del sitio a donde asistían, los datos se registraron hasta el mes de septiembre para completar la investigación. Se realizo la compilación de los datos y se obtuvo como resultado un shape que presenta las coordenadas del incidente y su descripción, todos los registros se clasificaron por categorías, a continuación, se presentan la categorización y el total de registros: 

![tabla1](  https://u3101499.github.io/Ejercicio_1/Tarea_1/Imagenes/1.jpg "ejemplo tabla servicios")


La tabla muestra los datos organizados de acuerdo con el mayor número de atenciones presentadas, ya que las falsas alarmas son las que mayor número de registros presentan también quieren conocer cuales son las localidades que más falsas alarmas están reportando. 

2.	**Por qué los datos geográficos ayudan a resolverlo?**

El departamento de bomberos tiene varias estaciones de atención distribuidas por toda la ciudad a las cuales se les asignan recursos económicos para su funcionamiento, por lo tanto se asigno una cantidad monetaria considerable para aquellas localidades donde se presenten mas incidentes, así pues todos los bomberos registraron la coordenada del sitio de atención, al tener este dato podemos cruzar la información con las áreas establecidas para las localidades y determinar en cual de estas se concentran mas los llamados para esta institución

**3.Descripción de la solución propuesta.**

Se plantea como solución elaborar 2 shapes, que distribuyan los incidentes por localidad, y de acuerdo con el número de datos establecer un color determinado que evidencie donde hay mas casos de llamadas, para este proceso se utilizo una serie de programas que permitieron el desarrollo de la solución, como Qgis, Arcgis, Magna 4.0, Github. La combinación de estas herramientas permitió desarrollar la propuesta para solucionar el problema planteado.

**4.	Listado detallado de las fuentes de datos seleccionadas. Mínimo 3 conjuntos de datos. Incluir información del proveedor de los datos, enlace para descarga, título y descripción del conjunto de datos, descripción de los atributos principales a utilizar.** 

**•Localidades: bogota-laurbano.opendatasoft.com**

**Información proveedor:** El objetivo principal de esta alianza, es establecer las bases y líneas de trabajo conjuntas para dar forma y crear un laboratorio urbano que se caracterice por ser un sitio abierto de interacción y trabajo colaborativo, en el que confluyan iniciativas en torno a la experimentación y el análisis interdisciplinar de los desafíos urbanos que enfrenta Bogotá, con el ánimo de generar soluciones innovadoras, aplicables y replicables.

**Enlace de descarga:** 

[https://bogota-laburbano.opendatasoft.com/explore/dataset/poligonos-localidades/export/?flg=es&location=10,4.47306,-74.05678&basemap=jawg.streets]

**Título y descripción del conjunto de datos:**  Polígonos Localidades, describe los limites de las localidades y su distribución en la ciudad de Bogotá. 

**Atributos para utilizar:**  Nombre de la localidad, área de la localidad 

**•	Incidente atendido por Bomberos: datos abiertos Bogotá**

**Información proveedor:**  la plataforma de Datos Abiertos de Bogotá busca promover la transparencia, el acceso a la información pública, la competitividad, el desarrollo económico, y la generación de impacto social a través de la apertura, la reutilización de los datos públicos, y el uso y apropiación de las TIC de acuerdo a la estrategia de Gobierno en Línea de Colombia. La iniciativa de Datos Abiertos busca que todas las entidades del sector público publiquen la información pertinente y de calidad en formatos estructurados a disposición de los usuarios para que ellos y las entidades la utilicen de diferentes maneras, según su interés: generar informes, reportes, estadísticas, investigaciones, control social, oportunidades de negocio (ej. aplicaciones), entre otros temas. Dicha información es compartida públicamente en formatos digitales estandarizados con una estructura de fácil comprensión para que la misma pueda ser utilizada por los ciudadanos. Dado que son financiados y recopilados con dinero público, la información contenida en estos datos es pública y debe estar a disposición de cualquier ciudadano y para cualquier fin.


**Enlace de descarga:**

[https://datosabiertos.bogota.gov.co/dataset/incidente-atendido-por-bomberos]

**Título y descripción del conjunto de datos:**  Eventos que atiende la Unidad Administrativa Especial Cuerpo Oficial de Bomberos, relacionada con incendios, rescates, incidentes con materiales peligrosos y otras emergencias, que se presenten en el Distrito Capital.

**Atributos para utilizar:**  Fecha, Estación, Servicio, coordenada x, coordenada y

**•	Estaciones de bomberos Cuerpo de bomberos** 

**Información proveedor:** UNIDAD ADMINISTRATIVA ESPECIAL CUERPO OFICIAL BOMBEROS DE BOGOTÁ

**Enlace de descarga:** 

[http://www.bomberosbogota.gov.co/transparencia/informacion-interes/publicacion/datos-abiertos/coordenadas-estaciones-bomberos]

**Título y descripción del conjunto de datos:**   Coordenadas estaciones de bomberos, En este conjunto de datos podrán encontrar los teléfonos, direcciones y coordenadas de las Estaciones de Bomberos de Bogotá. 

**Atributos para utilizar:** nombre estación, coordenada x , coordenada y

**5.	Descripción detallada del procesamiento no trivial realizado a los datos (algoritmos, herramientas utilizadas, modelos, etc).**

La zona de estudio se encuentra en la ciudad de Bogotá, por lo tanto el sistema de referencia que se va a utilizar es el Magna Colombia Bogotá, varios de los datos descargados no cuentan con este sistema por lo tanto fue necesario realizar la respectiva proyección, a continuación se describen todos los procesos que se le realizaron a los datos para poder ser utilizados y solucionar el problema planteado:


**•	Shape de Localidades de Bogotá** 

![pantallazo1](https://u3101499.github.io/Ejercicio_1/Tarea_1/Imagenes/2.jpg "ejemplo pantallazo 1")

El shape de la distribución de localidades para la ciudad de Bogotá se descargó de la página bogota-laurbano.opendatasoft.com, el cual presenta como sistema de referencia el sistema WGS 1984, ya que vamos a trabajar con el sistema de referencia para la ciudad de Bogotá, fue necesario realizar la proyección del shape, utilizando la herramienta Project del software Arcgis, la cual permite establecer el nuevo sistema de referencia. 

![pantallazo1](https://u3101499.github.io/Ejercicio_1/Tarea_1/Imagenes/3.jpg "ejemplo pantallazo 1")

**•	Estaciones de bomberos**

El archivo que se descargo de la pagina oficial de los bomberos se encuentra en formato Excel, por lo tanto, fue necesario realizar varios procesos para obtener su respectivo shape.


![pantallazo1](https://u3101499.github.io/Ejercicio_1/Tarea_1/Imagenes/4.jpg "ejemplo pantallazo 1")

Las coordenadas que se presentan en el archivo son coordenadas planas que con cumplen con la proyección de Magna Colombia Bogotá, asi pies utilizaremos el programa Magna Sirgas pro 4.0 para ajustar las coordenadas del archivo, que como resultado obtuvimos un archivo csv. Con las coordenadas de las estaciones de bomberos y el cual podemos utilizar para ubicarlas espacialmente con uno de los software , para este caso utilizamos qgis. Este procedimiento se realiza mediante la herramienta administrador de fuentes de datos por texto delimitado, allí se selecciona el sistema de referencia y se realizan el respectivo ajuste que solicita la herramienta, y como resultado tenemos las estaciones de Bomberos de la ciudad de Bogotá.

![pantallazo1](https://u3101499.github.io/Ejercicio_1/Tarea_1/Imagenes/5.jpg "ejemplo pantallazo 1")

![pantallazo1](https://u3101499.github.io/Ejercicio_1/Tarea_1/Imagenes/6.jpg "ejemplo pantallazo 1")

![pantallazo1](https://u3101499.github.io/Ejercicio_1/Tarea_1/Imagenes/7.jpg "ejemplo pantallazo 1")



**•Incidentes reportados por el departamento de Bomberos**

Este archivo shape presenta un total de 5083 registros, en WGS84, como primera medida se realizo la transformación a Magna Colombia Bogotá por medio de Arcgis. 


![pantallazo1](https://u3101499.github.io/Ejercicio_1/Tarea_1/Imagenes/8.jpg "ejemplo pantallazo 1")

Al realizar la superposición de la capa incidentes con localidades, se observa que existen datos que no se encuentran dentro de la zona de estudio, estos se eliminan. 

![pantallazo1](https://u3101499.github.io/Ejercicio_1/Tarea_1/Imagenes/9.jpg "ejemplo pantallazo 1")

![pantallazo1](https://u3101499.github.io/Ejercicio_1/Tarea_1/Imagenes/10.jpg "ejemplo pantallazo 1")

Se desea obtener los datos de las falsas alarmas, por lo tanto, se realiza una selección por atributos para la columna servicio, la categoría 21. Representa las falsas alarmas por lo tanto necesitamos generar un shape con estos datos.

![pantallazo1](https://u3101499.github.io/Ejercicio_1/Tarea_1/Imagenes/11.jpg "ejemplo pantallazo 1")

Generamos un shape nuevo y eliminamos de la capa de incidentes los reportes de falsas alarmas, así pues, tenemos dos archivos uno con la información de las falsas alarmas y otro con los incidentes reales atendidos.

![pantallazo1](https://u3101499.github.io/Ejercicio_1/Tarea_1/Imagenes/12.jpg "ejemplo pantallazo 1")

En la tabla de atributos se presentan las estaciones que atendieron cada incidente, pero no tenemos la distribución de los incidentes por localidad. Por lo tanto, es necesario cruzar ambos shapes para obtener este dato, para ambos shapes se utilizo el mismo procedimiento. 

Se realiza un Split para separa el shape de localidades

![pantallazo1](https://u3101499.github.io/Ejercicio_1/Tarea_1/Imagenes/13.jpg "ejemplo pantallazo 1")

![pantallazo1](https://u3101499.github.io/Ejercicio_1/Tarea_1/Imagenes/14.jpg "ejemplo pantallazo 1")

Al realizar el Split obtenemos 20 polígonos que representan el área de cada localidad, así pues podemos proceder a realizar el corte del shape de incidentes y de falsas alarmas por localidades con la herramienta clip de Arcgis, ya que son 20 polígonos se implementó un modelo para ejecutar la herramienta varias veces.




