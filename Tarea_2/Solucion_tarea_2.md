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

** 1. Definición del problema **


