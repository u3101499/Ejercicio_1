# Tarea 3 - Publicación de mapas utilizando servicios en la nube

# Objetivos

Aplicar técnicas para el procesamiento, análisis y visualización de información georrefenciada para plantear la solución de un problema de interés.

Entender y aplicar los procedimientos requeridos para realizar la publicación y visualización de datos geográficos en internet utilizando SaaS (Software as a Service).

Aprovechar los elementos de interactividad proporcionados por las diferentes herramientas para la generación de aplicaciones que incorporan mapas.

Narrar la solución dada al problema propuesto a través de una historia interactiva que involucre mapas y elementos multimedia.

# Tema Principal

Efectos, impacto y consecuencias en el mundo a causa de la cuarentena ocasionada por la pandemia causada por el virus SRAS-CoV-2 y la enfermedad COVID-19 en diversos aspectos en transporte, economía, empleo, salud, movilidad, uso de internet, etc.

## Tema Seleccionado 

**3101499: "Posible afectación a empresas comerciales por encontrarse ubicadas en zonas vulnerables a contagios por el COVID-19"**

# Actividades

**1.Definición del problema y fuentes de datos**

**Titulo: Posible afectación a empresas comerciales por encontrarse ubicadas en zonas vulnerables a contagios por el COVID-19**

La llegada del COVID-19 ha generado un cambio a nivel mundial, en cuanto a las actividades que el ser humano ha desarrollado a lo largo de la historia, para prevenir el contagio los países a nivel mundial optaron por decretar un aislamiento social, que cambio la forma en que los seres humanos desarrollaban sus actividades, y Colombia no fue la excepción. Al estar todos en casa estamos disminuyendo el riesgo de exponernos a la enfermedad, pero este aislamiento afecta muchos sectores económicos que se vieron obligados a parar sus actividades. Uno de los más golpeados ha sido el sector comercial, El Departamento de Planeación Nacional, el Instituto de Evaluación Tecnológica en Salud y el Dane lanzaron una herramienta de georreferenciación en la que se puede detectar la vulnerabilidad que hay en los barrios, e inclusive en las manzanas, con llegar a tener más complicaciones en caso de contagiarse con el coronavirus. Esto nos permite evaluar de acuerdo a los datos de CATASTRO de lotes y usos de suelos, cual será el % de vulnerabilidad que puede presentar este sector en la ciudad de Bogotá.

**Crear un boceto (mockup) donde se plantee la narrativa que se presentará al usuario e incluir cada una de las imágenes del mismo.**

[https://balsamiq.cloud/sy5iunj/psrxt5j]

**Listado detallado de las fuentes de datos seleccionadas.**

Capa | Descripción | Link
--- | --- | ---
Niveles de Vulnerabilidad | En el mapa podrá ubicar su ciudad y su zona para encontrar los resultados, los cuales se realizaron cruzando las características demográficas: edad de la población, nivel de pobreza, entre otros. |[http://visor01.dane.gov.co:9000/visor-vulnerabilidad/]
Lotes | Division Lotes prediales Bogotá | [https://datosabiertos.bogota.gov.co/dataset/mapa-de-referencia]
Uso del Suelo | Tabla que relaciona los usos del suelo establecidos para los lotes en la ciudad de Bogotá | [https://datosabiertos.bogota.gov.co/dataset/mapa-de-referencia]
Barrios | Distribución de los barrios en Bogotá | [https://datosabiertos.bogota.gov.co/dataset/mapa-de-referencia]


**2.Procesamiento de datos**

Mediante el uso del software Arcgis y Qgis, se realiza el geoprocesamiento de los datos.

Cargamos las capas de nivel de vulnerabilidad, lotes, barrios, y tabla de uso del suelo

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/1.jpg)


![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/2.jpg)


![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/3.jpg)

Se realiza un join de la tabla de uso del suelo con la capa de lotes, para obtener el uso del suelo por lote

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/4.jpg)

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/5.jpg)


Se procede a utilizar la herramienta de selección por atributos, para identificar todos los lotes que tengan un uso relacionado con actividades comerciales, las categorias son las siguientes:

003 Comercio puntual NPH (No Propiedad Horizontal)
004 Corredor comercial en NPH
006 Centro comercial mediano NPH
007 Centro comercial grande NPH
039 Comercio puntual en PH
040 Corredor comercial PH
041 Centro comercial mediado PH
042  Centro comercial grande PH
094 Centro comercial pequeño NPH
095 Centro comercial pequeño PH

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/6.jpg)

Obtenemos una nueva capa, con los lotes comerciales

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/7.jpg)


Cargamos la capa barrios

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/8.jpg)

Se va a determinar la cantidad de poligonos comerciales presentes en los barrios utilizando la herramienta Spatial Join

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/9.jpg)


![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/10.jpg)


Para la capa de lotes comerciales, asignaremos a cada lote comercial su nivel de vulnerabilidad, con la herramienta Intersect

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/11.jpg)

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/12.jpg)


**3. CARTO **

**Describir de forma detallada el procedimiento utilizado para publicar la aplicación.**

Mediante la aplicación CARTO, se va a elaborar un mapa donde se visualizara la capa de barrios y su vulnerabilidad, relacionando la cantidad de lotes comerciales.

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/13.jpg)


Cargamos nuestro shape

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/14.jpg)


Creamos nuestro mapa

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/15.jpg)

Asignamos un color a nuestro mapa base

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/16.jpg)

Establecemos el parametro de vulnerabilidad como atributo principal

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/17.jpg)

Se asigna una etiqueta para mostrar los atributos de los poligonos, donde se va a visualizar los nombres del barrio, el nivel de vulnerabilidad y la cantidad de lotes comerciales

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/18.jpg)

Creamos una legenda, con 5 categorias que clasifican los porcentajes de 0 a 100 %, se asigna tonalidades naranjas, siendo las más claras aquellas con menor %.

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/19.jpg)

Creamos los widgets, que nos permiten interactuar con nuestro mapa

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/20.jpg)

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/21.jpg)

Resultado

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/23.jpg)

**LINK**

[https://u3101499.carto.com/builder/1201947e-9860-4c25-8d0a-a42c95a9a1ed/embed?state=%7B%22map%22%3A%7B%22ne%22%3A%5B4.546308224744384%2C-74.26860809326173%5D%2C%22sw%22%3A%5B4.765651753679886%2C-73.9479446411133%5D%2C%22center%22%3A%5B4.655988537587979%2C-74.10827636718751%5D%2C%22zoom%22%3A12%7D%2C%22widgets%22%3A%7B%22b804e80d-c317-418d-a1a9-7bdc361f8df6%22%3A%7B%22normalized%22%3Atrue%7D%2C%222ffda833-a51a-4144-aa00-390c12486ded%22%3A%7B%22normalized%22%3Atrue%7D%7D%7D]


**4.GEONODE.**

**Describir de forma detallada el procedimiento utilizado para publicar la aplicación.**

Cargamos la capa en formato ZIP, y procedemos a crear nuestro mapa, primero se crea el metadato

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/24.jpg)

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/25.jpg)


Asignamos una nueva simbologia, mediante el programa QGIS, donde se clasificaran los lotes, por su vulnerabilidad, con una selección de tonalidades verdes, pastel y rojos. El archivos SLD de la simbologia se guarda.


![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/26.jpg)

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/27.jpg)


Seleccionamos el formato SLD en Geonode

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/28.jpg)

Creamos un nombre para la simbologia

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/29.jpg)

Copiamos el codigo SLD

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/30.jpg)

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/31.jpg)

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/32.jpg)


Creamos los widgets para interactuar con nuestro mapa

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/33.jpg)

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/34.jpg)

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/35.jpg)

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/36.jpg)

Resultado

![alt text](https://github.com/u3101499/Ejercicio_1/blob/master/Tarea_3/Imagenes/37.jpg)

**LINK**

[http://34.83.176.208/maps/32/edit]

**5.PUBLICAR HISTORIA.**

Publique una historia utilizando Slides.com ( https://slides.com/ ) donde se integren las aplicaciones creadas en los puntos 3 y 4 con elementos textuales y multimedia de tal forma que se explique de forma amable al usuario la temática y solución propuesta al trabajo desarrollado. ("Contar una historia")

**LINK**

[https://slides.com/u3101499/deck#/]


**6. CONCLUSIONES**

Publicar un video en Loom ( https://www.loom.com/ ) de mínimo 5 minutos y máximo 8 y adjuntar el url del mismo.
En el video describa brevemente lo siguiente:

Problema planteado
Procesamiento y análisis realizado a los datos
Proceso de creación de las aplicaciones y la historia con las herramientas seleccionadas.
Conclusiones del ejercicio desde el punto de vista temático.

[https://www.loom.com/share/88ecd13cfdec4d1cbbff819d8ccb3755]


