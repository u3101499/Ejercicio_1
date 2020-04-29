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

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/7.jpg)

Generación de los polígonos

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/8.jpg)


Se realiza el corte para ajustarlo a la ciudad de Bogotá


![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/9.jpg)


Como se observa, cada punto crítico de acumulación de residuos cuenta con una zona.

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/10.jpg)

Se realiza la superposición de las capas de contenedores y canecas, con los poligonos de Thiessen, y utilizando la herramienta spatial Join podemos determinar cuantos contenedores y canecas están presentes dentro de las zonas de puntos críticos, con estos datos se puede establecer que puntos críticos pudiero haber mejorado después de la instalación de los recipientes. 

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/11.jpg)

El resultado es una capa donde se muestra la sumatoria de puntos en cada polígono de Thiessen. 

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/12.jpg)

Esto nos permite clasificar y establecer rangos para determinar que polígonos tienen una mayor o menor concentración de recipientes, esto se puede representar con una buena simbología, donde se establecieron 6 clases que permiten identificar de manera sencilla las concentraciones mas altas y mas bajas de los recipientes en cada área. 

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/13.jpg)


![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/14.jpg)


![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/15.jpg)

Ya determinadas las zonas donde se produce mayor concentración de contenedores, tenemos como alternativa también poder conocer cuál es la distancia del recipiente más cercano a cada punto crítico, para obtener otra perspectiva del problema. Por medio de la herramienta near. Esta herramienta busca los contenedores más cercanos y determina la distancia más cercana.

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/16.jpg)

La herramienta adiciona una columna donde determina cual es el recipiente mas cercano a cada punto crítico. 

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/17.jpg)

Según la literatura establecen que es necesario ubicar un contenedor de residuos a menos de 50 metros de los usuarios para que estos los utilicen de manera adecuada, por lo tanto, aquellos puntos críticos que presenten una distancia mayor a la establecida, sería necesario replantear la ubicación de los recipientes para poder dar solución a la acumulación de residuos o evaluar otras alternativas. 


![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/18.jpg)

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/19.jpg)

Ya que según la literatura se deberia instalar un contenedor de residuos solidos a 50m del usuario, se selecciono como resultado aquellos puntos que cumplen con esta condicion, y adicional se amplia el rango a 100m ya que se considera que esta distancia tambien es apta para que un usuario realice esta tarea sin restricción alguna, por medio de la herramienta select by atributte se buscan los puntos criticos que cumplan con la condicion de tener un contenedor o caneca a menos de 100 m, los demas son motivo de estudio, ya que se considera que un usuario no utulizaria un recipiente que le quede a mas de 100 m del sitio donde se encuentra.

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/20.jpg)

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/21.jpg)


**CARGA DE DOCUMENTOS A POSTGIS**

Utilizando el sotfware Qgis, se realizara el proceso de cargar los shapes a la base de datos establecida para la clase, este procedimiento se utilizo para todos los archivos.


•	Se abre el menu base de datos, y  buscampos administrar bases de datos


![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/22.jpg)


Se busca la base de datos donde se va a cargar y se da click en importar

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/23.jpg)


Se selecciona el archivo a cargar, se re nombra utilizando el prefijo asignago (ma_), se marcan las casillas correspondientes y se carga el archivo.

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/24.jpg)


**CARGAR LOS DATOS A GEOSERVER**

En la pagina del servidor , se busca la opcion capas, y alli se selecciona agregar nueva capa

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/25.jpg)

Se selecciona el espacio de trabajo presente en postgis.

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/27.jpg)

Se edita la capa, se asigna un nombre y una descripción

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/28.jpg)

Se buscan las capas  cargadas con el prefijo ma_ y damos click en publicación

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/28a.jpg)

Damos click en guardar para cargar la capa a geoserver

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/29.jpg)

**NOMBRE DE LAS CAPAS CARGADAS**

**1.ma_canecas_clip**

**2.ma_contenedores_clip**

**3.ma_localidades_bogota**

**4.ma_puntos_canecas**

**5.ma_puntos_canecas_100**

**6.ma_puntos_contenedores**

**7.ma_puntos_contenedores_100**


**4. CAPA SIMBOLOGIA SLD**

**•	Publicar una de las capas utilizando simbología basada en SLD**

Con esta simbología se van a publicar las siguientes capas:

o	Capa de puntos críticos con distancia mínima a una caneca

o	Capa de puntos críticos con distancia mínima a un contenedor

o	Capa de polígonos de los puntos críticos con las concentraciones de canecas

o	Capa de polígonos de los puntos críticos con las concentraciones de contenedores.


**•	Si utiliza QGIS para generar el SLD, favor mencionar brevemente el proceso realizado.**

**Proceso capas de puntos**

Para las dos capas de puntos que se implementa la simbología SLD, se utilizó el siguiente procedimiento:

 a.	Se utilizo un estilo graduado con cuantiles iguales para clasificar la distancia de un recipiente al punto crítico de acumulación de residuos, el campo a clasificar será la distancia al recipiente más cercano.

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/30.jpg)

 b.	Para clasificar los datos se tuvo en cuenta los valores máximos y mínimos, y además también se adecuo la categoría que cumple con las condiciones planteadas de que un recipiente que este a menos de 50m el cual es adecuado para que un usuario lo utilice sin restricción, también considerando que aquellos que estén a menos de 100 m pueden ser otra buena opción para los usuarios. 

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/31.jpg)

 c.	Se utilizo una paleta de colores que alterna tonalidades verdes y rojas, las cuales permiten identificar que a mayor distancia estará asociado un color rojo, y que irá disminuyendo hasta llegar a una menor distancia con tonalidad verde.

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/32.jpg)


**PROCESO CAPAS DE POLÍGONOS**

a. Se utilizo un estilo graduado con cuantiles iguales para clasificar los polígonos de los puntos críticos de acumulación de residuos sólidos, que tienen mayor concentración de recipientes. El campo para utilizar es la sumatoria de los recipientes en el polígono (Join_count). 


![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/30a.jpg)

b. 2.	Para clasificar los datos se tuvo en cuenta los valores máximos y mínimos, estableciendo un criterio para establecer las áreas donde menos se concentran recipientes.

c. 3.	Se utilizo una paleta de colores que alterna tonalidades entre el rango anaranjado y azul, y tonalidades naranjas las cuales permiten identificar que a mayor concentración estará asociado un color naranja, y que irá disminuyendo hasta llegar a una menor concentración con tonalidad azul.

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/30c.jpg)


**GUARDAR LA SIMBOLOGÍA Y ASIGNARLOS A UNA CAPA EN GEOSERVER**

Se guarda la simbología como un archivo sld, y luego se asigna esta simbología a la capa designada en geoserver. Este proceso se realizo para todas las capas.


En simbologia, se busca la pestaña estilos, le damos guardar estilo y seleccionamos el formato SLD, asignamos el archivo en una carpeta y guardamos. 


![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/33.jpg)

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/34.jpg)

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/35.jpg)


En la página de geoserver vamos a estilos y buscamos la opción nuevo estilo

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/36.jpg)

Asignamos un nombre, seleccionamos estilo sld y cargamos el archivo.

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/37.jpg)


Se valida el codigo para que no exista ningun error, cuando la validacion sea correcta se da click en aplicar.

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/38.jpg)


Asignamos la simbología a la capa correspondiente

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/39.jpg)

Validamos, aplicamos y enviamos para cargar la simbología

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/40.jpg)

**EJEMPLOS TEXTO SLD**

**ma_poligonos_canecas_simb**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<StyledLayerDescriptor xmlns="http://www.opengis.net/sld" version="1.1.0" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ogc="http://www.opengis.net/ogc" xsi:schemaLocation="http://www.opengis.net/sld http://schemas.opengis.net/sld/1.1.0/StyledLayerDescriptor.xsd" xmlns:se="http://www.opengis.net/se">
  <NamedLayer>
    <se:Name>Canecas_clip</se:Name>
    <UserStyle>
      <se:Name>Canecas_clip</se:Name>
      <se:FeatureTypeStyle>
        <se:Rule>
          <se:Name>0 - 10 </se:Name>
          <se:Description>
            <se:Title>0 - 10 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThanOrEqualTo>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>0</ogc:Literal>
              </ogc:PropertyIsGreaterThanOrEqualTo>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>10</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PolygonSymbolizer>
            <se:Fill>
              <se:SvgParameter name="fill">#e66101</se:SvgParameter>
            </se:Fill>
            <se:Stroke>
              <se:SvgParameter name="stroke">#232323</se:SvgParameter>
              <se:SvgParameter name="stroke-width">1</se:SvgParameter>
              <se:SvgParameter name="stroke-linejoin">bevel</se:SvgParameter>
            </se:Stroke>
          </se:PolygonSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>10 - 20 </se:Name>
          <se:Description>
            <se:Title>10 - 20 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>10</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>20</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PolygonSymbolizer>
            <se:Fill>
              <se:SvgParameter name="fill">#f9a74f</se:SvgParameter>
            </se:Fill>
            <se:Stroke>
              <se:SvgParameter name="stroke">#232323</se:SvgParameter>
              <se:SvgParameter name="stroke-width">1</se:SvgParameter>
              <se:SvgParameter name="stroke-linejoin">bevel</se:SvgParameter>
            </se:Stroke>
          </se:PolygonSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>20 - 50 </se:Name>
          <se:Description>
            <se:Title>20 - 50 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>20</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>50</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PolygonSymbolizer>
            <se:Fill>
              <se:SvgParameter name="fill">#fadebc</se:SvgParameter>
            </se:Fill>
            <se:Stroke>
              <se:SvgParameter name="stroke">#232323</se:SvgParameter>
              <se:SvgParameter name="stroke-width">1</se:SvgParameter>
              <se:SvgParameter name="stroke-linejoin">bevel</se:SvgParameter>
            </se:Stroke>
          </se:PolygonSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>50 - 100 </se:Name>
          <se:Description>
            <se:Title>50 - 100 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>50</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>100</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PolygonSymbolizer>
            <se:Fill>
              <se:SvgParameter name="fill">#dcd9e9</se:SvgParameter>
            </se:Fill>
            <se:Stroke>
              <se:SvgParameter name="stroke">#232323</se:SvgParameter>
              <se:SvgParameter name="stroke-width">1</se:SvgParameter>
              <se:SvgParameter name="stroke-linejoin">bevel</se:SvgParameter>
            </se:Stroke>
          </se:PolygonSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>100 - 150 </se:Name>
          <se:Description>
            <se:Title>100 - 150 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>100</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>150</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PolygonSymbolizer>
            <se:Fill>
              <se:SvgParameter name="fill">#a195c7</se:SvgParameter>
            </se:Fill>
            <se:Stroke>
              <se:SvgParameter name="stroke">#232323</se:SvgParameter>
              <se:SvgParameter name="stroke-width">1</se:SvgParameter>
              <se:SvgParameter name="stroke-linejoin">bevel</se:SvgParameter>
            </se:Stroke>
          </se:PolygonSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>150 - 273 </se:Name>
          <se:Description>
            <se:Title>150 - 273 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>150</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>273</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PolygonSymbolizer>
            <se:Fill>
              <se:SvgParameter name="fill">#5e3c99</se:SvgParameter>
            </se:Fill>
            <se:Stroke>
              <se:SvgParameter name="stroke">#232323</se:SvgParameter>
              <se:SvgParameter name="stroke-width">1</se:SvgParameter>
              <se:SvgParameter name="stroke-linejoin">bevel</se:SvgParameter>
            </se:Stroke>
          </se:PolygonSymbolizer>
        </se:Rule>
      </se:FeatureTypeStyle>
    </UserStyle>
  </NamedLayer>
</StyledLayerDescriptor>
```

**ma_poligonos_contenedores_sim**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<StyledLayerDescriptor xmlns="http://www.opengis.net/sld" version="1.1.0" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ogc="http://www.opengis.net/ogc" xsi:schemaLocation="http://www.opengis.net/sld http://schemas.opengis.net/sld/1.1.0/StyledLayerDescriptor.xsd" xmlns:se="http://www.opengis.net/se">
  <NamedLayer>
    <se:Name>Contenedores_clip</se:Name>
    <UserStyle>
      <se:Name>Contenedores_clip</se:Name>
      <se:FeatureTypeStyle>
        <se:Rule>
          <se:Name>0 - 10 </se:Name>
          <se:Description>
            <se:Title>0 - 10 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThanOrEqualTo>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>0</ogc:Literal>
              </ogc:PropertyIsGreaterThanOrEqualTo>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>10</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PolygonSymbolizer>
            <se:Fill>
              <se:SvgParameter name="fill">#ffffb2</se:SvgParameter>
            </se:Fill>
            <se:Stroke>
              <se:SvgParameter name="stroke">#232323</se:SvgParameter>
              <se:SvgParameter name="stroke-width">1</se:SvgParameter>
              <se:SvgParameter name="stroke-linejoin">bevel</se:SvgParameter>
            </se:Stroke>
          </se:PolygonSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>10 - 20 </se:Name>
          <se:Description>
            <se:Title>10 - 20 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>10</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>20</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PolygonSymbolizer>
            <se:Fill>
              <se:SvgParameter name="fill">#ffd76d</se:SvgParameter>
            </se:Fill>
            <se:Stroke>
              <se:SvgParameter name="stroke">#232323</se:SvgParameter>
              <se:SvgParameter name="stroke-width">1</se:SvgParameter>
              <se:SvgParameter name="stroke-linejoin">bevel</se:SvgParameter>
            </se:Stroke>
          </se:PolygonSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>20 - 50 </se:Name>
          <se:Description>
            <se:Title>20 - 50 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>20</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>50</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PolygonSymbolizer>
            <se:Fill>
              <se:SvgParameter name="fill">#fea649</se:SvgParameter>
            </se:Fill>
            <se:Stroke>
              <se:SvgParameter name="stroke">#232323</se:SvgParameter>
              <se:SvgParameter name="stroke-width">1</se:SvgParameter>
              <se:SvgParameter name="stroke-linejoin">bevel</se:SvgParameter>
            </se:Stroke>
          </se:PolygonSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>50 - 100 </se:Name>
          <se:Description>
            <se:Title>50 - 100 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>50</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>100</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PolygonSymbolizer>
            <se:Fill>
              <se:SvgParameter name="fill">#f86c30</se:SvgParameter>
            </se:Fill>
            <se:Stroke>
              <se:SvgParameter name="stroke">#232323</se:SvgParameter>
              <se:SvgParameter name="stroke-width">1</se:SvgParameter>
              <se:SvgParameter name="stroke-linejoin">bevel</se:SvgParameter>
            </se:Stroke>
          </se:PolygonSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>100 - 150 </se:Name>
          <se:Description>
            <se:Title>100 - 150 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>100</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>150</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PolygonSymbolizer>
            <se:Fill>
              <se:SvgParameter name="fill">#e62f21</se:SvgParameter>
            </se:Fill>
            <se:Stroke>
              <se:SvgParameter name="stroke">#232323</se:SvgParameter>
              <se:SvgParameter name="stroke-width">1</se:SvgParameter>
              <se:SvgParameter name="stroke-linejoin">bevel</se:SvgParameter>
            </se:Stroke>
          </se:PolygonSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>150 - 302 </se:Name>
          <se:Description>
            <se:Title>150 - 302 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>150</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>sumatoria</ogc:PropertyName>
                <ogc:Literal>302</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PolygonSymbolizer>
            <se:Fill>
              <se:SvgParameter name="fill">#bd0026</se:SvgParameter>
            </se:Fill>
            <se:Stroke>
              <se:SvgParameter name="stroke">#232323</se:SvgParameter>
              <se:SvgParameter name="stroke-width">1</se:SvgParameter>
              <se:SvgParameter name="stroke-linejoin">bevel</se:SvgParameter>
            </se:Stroke>
          </se:PolygonSymbolizer>
        </se:Rule>
      </se:FeatureTypeStyle>
    </UserStyle>
  </NamedLayer>
</StyledLayerDescriptor>
```

**ma_puntos_caneca_simb**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<StyledLayerDescriptor xmlns="http://www.opengis.net/sld" version="1.1.0" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ogc="http://www.opengis.net/ogc" xsi:schemaLocation="http://www.opengis.net/sld http://schemas.opengis.net/sld/1.1.0/StyledLayerDescriptor.xsd" xmlns:se="http://www.opengis.net/se">
  <NamedLayer>
    <se:Name>puntos_canecas</se:Name>
    <UserStyle>
      <se:Name>puntos_canecas</se:Name>
      <se:FeatureTypeStyle>
        <se:Rule>
          <se:Name>0 - 50 </se:Name>
          <se:Description>
            <se:Title>0 - 50 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThanOrEqualTo>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>0</ogc:Literal>
              </ogc:PropertyIsGreaterThanOrEqualTo>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>50</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PointSymbolizer>
            <se:Graphic>
              <se:Mark>
                <se:WellKnownName>circle</se:WellKnownName>
                <se:Fill>
                  <se:SvgParameter name="fill">#168036</se:SvgParameter>
                </se:Fill>
                <se:Stroke>
                  <se:SvgParameter name="stroke">#232323</se:SvgParameter>
                  <se:SvgParameter name="stroke-width">0.5</se:SvgParameter>
                </se:Stroke>
              </se:Mark>
              <se:Size>11</se:Size>
            </se:Graphic>
          </se:PointSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>50 - 100 </se:Name>
          <se:Description>
            <se:Title>50 - 100 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>50</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>100</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PointSymbolizer>
            <se:Graphic>
              <se:Mark>
                <se:WellKnownName>circle</se:WellKnownName>
                <se:Fill>
                  <se:SvgParameter name="fill">#81ff21</se:SvgParameter>
                </se:Fill>
                <se:Stroke>
                  <se:SvgParameter name="stroke">#232323</se:SvgParameter>
                  <se:SvgParameter name="stroke-width">0.5</se:SvgParameter>
                </se:Stroke>
              </se:Mark>
              <se:Size>11</se:Size>
            </se:Graphic>
          </se:PointSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>100 - 500 </se:Name>
          <se:Description>
            <se:Title>100 - 500 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>100</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>500</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PointSymbolizer>
            <se:Graphic>
              <se:Mark>
                <se:WellKnownName>circle</se:WellKnownName>
                <se:Fill>
                  <se:SvgParameter name="fill">#dcf09e</se:SvgParameter>
                </se:Fill>
                <se:Stroke>
                  <se:SvgParameter name="stroke">#232323</se:SvgParameter>
                  <se:SvgParameter name="stroke-width">0.5</se:SvgParameter>
                </se:Stroke>
              </se:Mark>
              <se:Size>11</se:Size>
            </se:Graphic>
          </se:PointSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>500 - 900 </se:Name>
          <se:Description>
            <se:Title>500 - 900 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>500</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>900</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PointSymbolizer>
            <se:Graphic>
              <se:Mark>
                <se:WellKnownName>circle</se:WellKnownName>
                <se:Fill>
                  <se:SvgParameter name="fill">#ffdf9a</se:SvgParameter>
                </se:Fill>
                <se:Stroke>
                  <se:SvgParameter name="stroke">#232323</se:SvgParameter>
                  <se:SvgParameter name="stroke-width">0.5</se:SvgParameter>
                </se:Stroke>
              </se:Mark>
              <se:Size>11</se:Size>
            </se:Graphic>
          </se:PointSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>900 - 2500 </se:Name>
          <se:Description>
            <se:Title>900 - 2500 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>900</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>2500</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PointSymbolizer>
            <se:Graphic>
              <se:Mark>
                <se:WellKnownName>circle</se:WellKnownName>
                <se:Fill>
                  <se:SvgParameter name="fill">#f69053</se:SvgParameter>
                </se:Fill>
                <se:Stroke>
                  <se:SvgParameter name="stroke">#232323</se:SvgParameter>
                  <se:SvgParameter name="stroke-width">0.5</se:SvgParameter>
                </se:Stroke>
              </se:Mark>
              <se:Size>11</se:Size>
            </se:Graphic>
          </se:PointSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>2500 - 6169 </se:Name>
          <se:Description>
            <se:Title>2500 - 6169 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>2500</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>6169</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PointSymbolizer>
            <se:Graphic>
              <se:Mark>
                <se:WellKnownName>circle</se:WellKnownName>
                <se:Fill>
                  <se:SvgParameter name="fill">#d7191c</se:SvgParameter>
                </se:Fill>
                <se:Stroke>
                  <se:SvgParameter name="stroke">#232323</se:SvgParameter>
                  <se:SvgParameter name="stroke-width">0.5</se:SvgParameter>
                </se:Stroke>
              </se:Mark>
              <se:Size>11</se:Size>
            </se:Graphic>
          </se:PointSymbolizer>
        </se:Rule>
      </se:FeatureTypeStyle>
    </UserStyle>
  </NamedLayer>
</StyledLayerDescriptor>
```

**ma_puntos_contenedores_simb**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<StyledLayerDescriptor xmlns="http://www.opengis.net/sld" version="1.1.0" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ogc="http://www.opengis.net/ogc" xsi:schemaLocation="http://www.opengis.net/sld http://schemas.opengis.net/sld/1.1.0/StyledLayerDescriptor.xsd" xmlns:se="http://www.opengis.net/se">
  <NamedLayer>
    <se:Name>puntos_contenedores</se:Name>
    <UserStyle>
      <se:Name>puntos_contenedores</se:Name>
      <se:FeatureTypeStyle>
        <se:Rule>
          <se:Name>0 - 50 </se:Name>
          <se:Description>
            <se:Title>0 - 50 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThanOrEqualTo>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>0</ogc:Literal>
              </ogc:PropertyIsGreaterThanOrEqualTo>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>50</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PointSymbolizer>
            <se:Graphic>
              <se:Mark>
                <se:WellKnownName>circle</se:WellKnownName>
                <se:Fill>
                  <se:SvgParameter name="fill">#1a9641</se:SvgParameter>
                </se:Fill>
                <se:Stroke>
                  <se:SvgParameter name="stroke">#232323</se:SvgParameter>
                  <se:SvgParameter name="stroke-width">0.5</se:SvgParameter>
                </se:Stroke>
              </se:Mark>
              <se:Size>11</se:Size>
            </se:Graphic>
          </se:PointSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>50 - 100 </se:Name>
          <se:Description>
            <se:Title>50 - 100 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>50</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>100</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PointSymbolizer>
            <se:Graphic>
              <se:Mark>
                <se:WellKnownName>circle</se:WellKnownName>
                <se:Fill>
                  <se:SvgParameter name="fill">#8acc62</se:SvgParameter>
                </se:Fill>
                <se:Stroke>
                  <se:SvgParameter name="stroke">#232323</se:SvgParameter>
                  <se:SvgParameter name="stroke-width">0.5</se:SvgParameter>
                </se:Stroke>
              </se:Mark>
              <se:Size>11</se:Size>
            </se:Graphic>
          </se:PointSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>100 - 500 </se:Name>
          <se:Description>
            <se:Title>100 - 500 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>100</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>500</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PointSymbolizer>
            <se:Graphic>
              <se:Mark>
                <se:WellKnownName>circle</se:WellKnownName>
                <se:Fill>
                  <se:SvgParameter name="fill">#dcf09e</se:SvgParameter>
                </se:Fill>
                <se:Stroke>
                  <se:SvgParameter name="stroke">#232323</se:SvgParameter>
                  <se:SvgParameter name="stroke-width">0.5</se:SvgParameter>
                </se:Stroke>
              </se:Mark>
              <se:Size>11</se:Size>
            </se:Graphic>
          </se:PointSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>500 - 900 </se:Name>
          <se:Description>
            <se:Title>500 - 900 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>500</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>900</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PointSymbolizer>
            <se:Graphic>
              <se:Mark>
                <se:WellKnownName>circle</se:WellKnownName>
                <se:Fill>
                  <se:SvgParameter name="fill">#ffdf9a</se:SvgParameter>
                </se:Fill>
                <se:Stroke>
                  <se:SvgParameter name="stroke">#232323</se:SvgParameter>
                  <se:SvgParameter name="stroke-width">0.5</se:SvgParameter>
                </se:Stroke>
              </se:Mark>
              <se:Size>11</se:Size>
            </se:Graphic>
          </se:PointSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>900 - 2500 </se:Name>
          <se:Description>
            <se:Title>900 - 2500 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>900</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>2500</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PointSymbolizer>
            <se:Graphic>
              <se:Mark>
                <se:WellKnownName>circle</se:WellKnownName>
                <se:Fill>
                  <se:SvgParameter name="fill">#f69053</se:SvgParameter>
                </se:Fill>
                <se:Stroke>
                  <se:SvgParameter name="stroke">#232323</se:SvgParameter>
                  <se:SvgParameter name="stroke-width">0.5</se:SvgParameter>
                </se:Stroke>
              </se:Mark>
              <se:Size>11</se:Size>
            </se:Graphic>
          </se:PointSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:Name>2500 - 4880 </se:Name>
          <se:Description>
            <se:Title>2500 - 4880 </se:Title>
          </se:Description>
          <ogc:Filter xmlns:ogc="http://www.opengis.net/ogc">
            <ogc:And>
              <ogc:PropertyIsGreaterThan>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>2500</ogc:Literal>
              </ogc:PropertyIsGreaterThan>
              <ogc:PropertyIsLessThanOrEqualTo>
                <ogc:PropertyName>dist_canec</ogc:PropertyName>
                <ogc:Literal>4880</ogc:Literal>
              </ogc:PropertyIsLessThanOrEqualTo>
            </ogc:And>
          </ogc:Filter>
          <se:PointSymbolizer>
            <se:Graphic>
              <se:Mark>
                <se:WellKnownName>circle</se:WellKnownName>
                <se:Fill>
                  <se:SvgParameter name="fill">#d7191c</se:SvgParameter>
                </se:Fill>
                <se:Stroke>
                  <se:SvgParameter name="stroke">#232323</se:SvgParameter>
                  <se:SvgParameter name="stroke-width">0.5</se:SvgParameter>
                </se:Stroke>
              </se:Mark>
              <se:Size>11</se:Size>
            </se:Graphic>
          </se:PointSymbolizer>
        </se:Rule>
      </se:FeatureTypeStyle>
    </UserStyle>
  </NamedLayer>
</StyledLayerDescriptor>
```
4. Leyendas

Capa | Leyenda y visualización
--- | ---
ma_puntos_canecas | ![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/leyenda_puntos_canecas.jpg)
ma_puntos_contenedores | ![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/leyenda_puntos_contenedores.jpg)
ma_canecas_clip | ![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/leyenda_poligono_canecas.jpg)
ma_contenedores_clip | ![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/leyenda_poligono_contenedores.jpg)


**5. CAPA SIMBOLOGÍA CSS**

•	Publicar una de las capas utilizando simbología basada en CSS

La capa que utilizara esta simbologia es la que se selecciono previamente de los puntos criticos que tienen una caneca a menos de 100m, como estos puntos cumplen con nuestra condición, se le da una coloración verde para saber que son los puntos criticos que posiblemente ya no existen o que han reducido su tamaño.

Creamos un nuevo estilo

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/41.jpg)


Escribimos el codigo 

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/42.jpg)


Leyenda y pre visualización

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/43.jpg)


![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/leyenda_css.jpg)

**Codigo CSS**
```xml
* {
   mark: symbol(circle);
   label: [dist_canec];
   font-fill: black;
   font-family: Arial;
   font-size: 12;
   font-weight: bold;
   label-anchor: 0.5 0;
   label-offset: 0 5;
 }

 :mark {
   stroke: black;
   stroke-width: 2px;
   fill: green;
 }

 [@sd < 0.2M] {
   mark-size: 12;
 }

 [@sd > 1.6M] [@sd < 32M] {
   mark-size: 8;
 }

 [@sd > 3.2M] {
   mark-size: 4;
 }
```


**6. CAPA SIMBOLOGÍA YSLD**

•	Publicar una de las capas utilizando simbología basada en YSLD

La capa que utilizara esta simbologia es la que se selecciono previamente de los puntos criticos que tienen un contenedor a menos de 100m, como estos puntos cumplen con nuestra condición, se le da una coloración verde para saber que son los puntos criticos que posiblemente ya no existen o que han reducido su tamaño. Ademas de esto, asignamos un color azul y rojo a medida que nos alejamos de la capa de puntos.


Se crea un estilo nuevo tipo YSLD

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/44.jpg)


Escribimos el codigo

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/45.jpg)

Leyenda y previsualización

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/47.jpg)


![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/leyenda_ysld.jpg)

**Codigo YSDLD**
```xml
title: 'distancia'
feature-styles:
- name: name
  rules:
  - name: Large
    scale: [min,1.6e6]
    symbolizers:
    - point:
        size: 12
        symbols:
        - mark:
            shape: circle
            fill-color: '#08CC2C'
            stroke-color: '#000000'
    - text:
        label: ${dist_conte}
        fill-color: '#000000'
        font-family: Arial
        font-size: 12
        font-style: normal
        font-weight: bold
        placement: point
        anchor: [0.5,0.0]
        displacement: [0,5]
  - name: Medium
    scale: [1.6e6,3.2e8]
    symbolizers:
    - point:
        size: 8
        symbols:
        - mark:
            shape: circle
            fill-color: '#CC3300'
            stroke-color: '#000000'
    - text:
        label: ${dist_conte}
        fill-color: '#000000'
        font-family: Arial
        font-size: 12
        font-style: normal
        font-weight: bold
        placement: point
        anchor: [0.5,0.0]
        displacement: [0,5]      
  - name: Small
    scale: [3.2e8,max]
    symbolizers:
    - point:
        size: 4
        symbols:
        - mark:
            shape: circle
            fill-color: '#084CCC'
            stroke-color: '#000000'
```                 


**7. GRUPO CAPAS**

**•	Crear un layer group que contenga las capas creadas en los puntos 4, 5 y 6 y las adicionales que considere necesarias para darle contexto a la visualización (ejm. límites departamentales, límites municipales, límites internacionales, etc)**


Buscar la opción grupo de capas, y se selecciona nuevo grupo de capas

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/48.jpg)


Adicionamos todas las capas que queremos adjuntar en nuetro grupo de capas


![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/49.jpg)



![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/50.jpg)


**Enlace del grupo de capas**

[http://34.83.176.208:18080/geoserver/wms?service=WMS&version=1.1.0&request=GetMap&layers=ma_estudio_puntos_criticos_residuos&bbox=958587.2630515667%2C904328.769813754%2C1010108.8815953921%2C1026614.9533830815&width=330&height=768&srs=EPSG%3A3116&format=application/openlayers]


**8.CONCLUSIONES**

**•	Publicar un video en Loom [https://www.loom.com/] de mínimo 5 minutos y máximo 8 y adjuntar el url del mismo.**


**Link del video**
[https://www.loom.com/share/a0b28150ea384483b44562382994baba]



**ACTIVIDADES OPCIONALES**


**3. MAPA BASE CON MAPBOX**

Obtendrá un punto extra si crea o personaliza un mapa base que pudiera utilizarse como base map para los resultados generados durante la tarea 2.

Iniciamos mapbox

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/1m.jpg)


Seleccionamos una base

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/3n.jpg)


Cargamos la capa de localidades

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/4n.jpg)


![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/5n.jpg)


Cambiamos los colores a las localidades para diferenciar las áreas

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/6n.jpg)

Modificamos los colores del mapa base para resaltar las zonas verdes, y los cuerpos de agua

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/7n.jpg)

Compartimos nuestro mapa base como WMTS

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/8n.jpg)


**Visualización de las capas con el mapa base**

Ya que son capas completas , si ponemos todas las capas juntas en un solo archivo no se puede evidenciar la superposición sobre el mapa base, por lo tanto se muestran por grupos.


![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/9n.jpg)


![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/10n.jpg)


![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/11n.jpg)


**5. RASTER**

**Obtendrá un punto extra si publica una o más capas de tipo ráster adicionales a las vectoriales de los puntos 4, 5 y 6.**

Los contenedores de residuos pueden ser la solución para reducir los puntos criticos de acumulación, por lo tanto se elaboro un mapa de densidades basado en las distancias de los contenedores a los puntos criticos.


**•	Cargar imágenes ráster**

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/1r.jpg)

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/2r.jpg)

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/3r.jpg)

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/4r.jpg)

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/5r.jpg)



**•	Publicar la o las capas utilizando simbología basada en SLD**

La clasificación se realizo teniendo en cuenta las distancias del punto critico al contenedor, y se represento siendo la tonalidad verde con la menor distancia, y aumentando con la tonalidad roja hasta la mayor distancia.

Generarmos la simbologia en qgis

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/9r.jpg)


Guardamos la simbologia como un archivo SLD

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/10r.jpg)


Le asignamos la simbologia al raster en geoserver

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/6r.jpg)

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/7r.jpg)


**LEYENDA**

![alt text](https://u3101499.github.io/Ejercicio_1/Tarea_2/Imagenes/8r.jpg)



**•	Incluir texto del SLD**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<StyledLayerDescriptor xmlns="http://www.opengis.net/sld" xmlns:gml="http://www.opengis.net/gml" xmlns:ogc="http://www.opengis.net/ogc" version="1.0.0" xmlns:sld="http://www.opengis.net/sld">
  <UserLayer>
    <sld:LayerFeatureConstraints>
      <sld:FeatureTypeConstraint/>
    </sld:LayerFeatureConstraints>
    <sld:UserStyle>
      <sld:Name>Densidades_contenedores</sld:Name>
      <sld:FeatureTypeStyle>
        <sld:Rule>
          <sld:RasterSymbolizer>
            <sld:ChannelSelection>
              <sld:GrayChannel>
                <sld:SourceChannelName>1</sld:SourceChannelName>
              </sld:GrayChannel>
            </sld:ChannelSelection>
            <sld:ColorMap type="ramp">
              <sld:ColorMapEntry label="0" quantity="0" color="#1a9641"/>
              <sld:ColorMapEntry label="521.274108886719" quantity="521.274108886719" color="#a6d96a"/>
              <sld:ColorMapEntry label="1042.54821777344" quantity="1042.54821777344" color="#ffffc0"/>
              <sld:ColorMapEntry label="1563.82232666016" quantity="1563.82232666016" color="#fdae61"/>
              <sld:ColorMapEntry label="2085.09643554688" quantity="2085.09643554688" color="#d7191c"/>
            </sld:ColorMap>
          </sld:RasterSymbolizer>
        </sld:Rule>
      </sld:FeatureTypeStyle>
    </sld:UserStyle>
  </UserLayer>
</StyledLayerDescriptor>
```


**URL DEL VISOR**

[http://34.83.176.208:18080/geoserver/clase_2020_01/wms?service=WMS&version=1.1.0&request=GetMap&layers=clase_2020_01%3Ama_densidades_contenedores&bbox=958646.6955728859%2C904337.5290631293%2C1010094.3256417034%2C1026577.0981066397&width=330&height=768&srs=EPSG%3A3116&format=application/openlayers]












