# Tarea 2 - Publicación de mapas bajo estándares OGC utilizando base de datos espacial y servidor de mapas

## Objetivos

•	Entender el proceso de publicación de mapas en internet utilizando una base de datos espacial y un servidor de mapas bajo el marco de los estándares de interoperabilidad de OGC.

## Restricciones

•	Los datos deben quedar publicados en el servidor postgresql / postgis asignado para la clase.

•	Los mapas generados deben quedar publicados en el servidor geoserver asignado para la clase a través de WMS o WMTS.

•	Dadas las restricciones de ancho de banda que tenemos para la carga de los datos en la base de datos, en caso que los conjuntos de datos a utilizar sean demasiado grandes, se sugiere limitar la zona de estudio a áreas más pequeñas. Por ejemplo, en lugar de todos los predios de Bogotá, utilizar solamente los predios de la localidad X.

•	Tanto para la creación de tablas en postgresql como para la creación de objetos en geoserver (capas, estilos) favor utilizar el prefijo asignado para la clase. Ejemplo: jc_departamentos.

## Calificación 

•	Total, de puntos obligatorios: 8

•	Total, de opcionales para bono extra: 5

•	Cada actividad tiene un valor de 1 punto si está completo y correcto.

•	En caso de estar incompleta o incorrecta se otorgará 0 puntos.

•	En caso de entregar tarde se le restará un punto.

## Entrega de resultados para revisión:

•	Deben publicarse en geoserver como mínimo 3 capas individuales

•	Las capas publicadas deben agruparse bajo un grupo de capas (layer group)

•	En el repositorio github personal creado para la clase crear una carpeta llamada Tarea_2

•	Dentro de la carpeta Tarea_2 Crear un archivo Readme.md con los resultados de las actividades solicitadas.

•	Una vez tenga los resultados publicados en github, crear un issue en [issue link](https://github.com/dersteppenwolf/cartografia_web/issues), con lo siguiente:

o	Título: Tarea 2 - CODIGO_ESTUDIANTE
o	Contenido: Enlace (URL) al archivo Readme.md dentro de la carpeta Tarea_2 publicado en el repositorio personal del curso

## Actividades

**1. Definición del problema**

**•	Describa un problema hipotético que pueda resolverse a través del análisis y visualización de datos espaciales.**

La ciudad de Bogotá es uno de los más grandes generadores de residuos sólidos en Colombia, en el año 2018 se implementó un programa para la instalación de contenedores que pudieran solucionar el problema de acumulación de residuos en muchos barrios de la ciudad, fueron más de 10.000 los instalados. También se instalaron además de las ya existentes, canecas para que los transeúntes puedan disponer adecuadamente de sus residuos. Pero para el 31/05/2019 la unidad administrativa  especial de servicios públicos establecido 747 puntos críticos clandestinos de arrojo de basura a pesar de ya estar implementado el sistema de contenedores y canecas, adicional a  esto en el mes de septiembre de ese año (29/09/2019) la entidad publico las capa con la distribución de los contenedores, y el 31/01/2020 se publicó la capa actualizada de las canecas instaladas,  por lo tanto se desea conocer si la cantidad de canecas y contenedores tienen una adecuada distribución para cubrir todos los puntos críticos de las localidades de Bogotá.

**•	Describa de forma general el enfoque propuesto para desarrollar el problema**

Para el desarrollo del problema se cuentan con 3 capas de puntos, los puntos críticos de acumulación, las canecas y los contenedores. Para poder identificar las áreas o zonas donde tenemos puntos críticos sin la instalación de los recipientes se elaboraron una serie de capas donde se conocerá si la distribución de los contenedores y canecas si está cubriendo la totalidad de los puntos críticos de arrojo clandestino de residuos sólidos. Por medio del programa Qgis y su herramienta Group Stats, se establecieron cuantos puntos críticos se tienen por localidad, y cuantas canecas y recipientes existen.

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/1.jpg)

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/2.jpg)

**2. Fuentes de datos**

Capa | Descripción | Link
---|---|---
**Puntos Críticos de arrojo clandestino de residuos en Bogotá**|En el marco del Decreto 1077 de 2015, los puntos críticos son aquellos lugares donde se acumulan residuos sólidos, generando afectación y deterioro sanitario que conlleva la afectación de la limpieza del área, por la generación de malos olores, focos de propagación de vectores, y enfermedades, entre otros| [https://datosabiertos.bogota.gov.co/dataset/puntos-criticos-de-arrojo-clandestino-de-residuos-bogota-d-c]
**Contenerización Bogotá**|Sistema de disposición temporal de residuos para su recolección mecanizada a través del esquema de aseo del distrito; permite mejorar la presentación de los residuos, evitar la acumulación de estos y promueve el reciclaje. También evita que se formen puntos críticos que afectan y deterioran la armonía del espacio público urbano.| [https://datosabiertos.bogota.gov.co/dataset/contenerizacion-bogota-d-c]
**Caneca Bogotá**| Elemento dispositivo de aseo de alta resistencia al vandalismo para el almacenamiento de residuos producidos por los peatones o transeuntes en el espacio público. Su extensión geográfica es la zona urbana del Distrito Capital.| [https://datosabiertos.bogota.gov.co/dataset/caneca-bogota-d-c]
**Localidad Bogotá**| División política, administrativa y territorial municipal, con competencias claras y criterios de financiación y aplicación de recursos, creada por el Concejo Municipal a iniciativa del alcalde respectivo, con el fin de atender de manera más eficaz las necesidades de esa porción del territorio.|[https://datosabiertos.bogota.gov.co/dataset/localidad-bogota-d-c]

**3. Procesamiento de datos**

**•	Descripción detallada del procesamiento realizado a los datos (algoritmos, herramientas utilizadas, modelos, etc)**

**CAPAS DE PUNTOS**

A las capas se les asigna el sistema de coordenadas, Magna Colombia Bogotá, por medio de la herramienta Project de Arcgis

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/3.jpg)

Capa| Imagen
--- | ---
Puntos Criticos | ![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/4.jpg)
Canecas | ![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/5.jpg)
Contenedores | ![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/6.jpg)

Se plantearon 2 soluciones distintas, la primera va asociada al uso de polígonos de thiessen, esta herramienta permite dividir el área cubierta por las entidades de puntos en zonas o proximales, estas zonas representan áreas completas donde cualquier ubicación dentro de la zona está más cerca de su punto de entrada asociado que de cualquier otro punto de entrada. Por lo tanto, se establecieron las zonas relacionadas a los puntos críticos, para determinar cuántas canecas y contenderos están presenten en estas áreas.

Crear Polígonos con la herramienta create Thiessen polygon

[alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/7.jpg)

Generación de los polígonos

[alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/8.jpg)


Se realiza el corte para ajustarlo a la ciudad de Bogotá


[alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/9.jpg)




