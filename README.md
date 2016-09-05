# DecideBien (2011)

La intención de este desarrollo se orienta a que tanto el ciudadano como el funcionario público pueda visualizar la misma información de manera conjunta y de esta manera las decisiones que se adopten entre gobernantes y gobernantes tengan menos puntos de desencuentro y mayores consensos. 

En ese sentido, para hacer un prototipo, que bueno generar en un sistema más complejo de tableros de comando con información en tiempo real, se desarrolló la aplicación que la hemos bautizado como Decide bien por la intención que en ella descansa. 

Así, en los próximos párrafos indicaremos los datos que empleamos, el diagnóstico que hicimos de los mismos, el procedimiento que llevamos adelante, el resultado que obtuvimos y las conclusiones a las cuales arribamos después del trabajo realizado en la 1ra Hackaton organizada por Escuelab y la Municipalidad de Lima Metropolitana entre el 22 y 23 de septiembre del 2012. 

##DATOS EMPLEADOS.
La Municipalidad de Lima Metropolitana dispone de una página web http://www.munlima.gob.pe/datos-abiertos-mml/itemlist/category/991-open-data.html desde la cual se puede descargar algunos conjuntos de datos que pueden ser usados por el pùblico en general. 

En ese sentido, durante la 1ra Hackaton organizada por Escuelab y la Municipalidad de Lima 
seleccione los datos pertenecientes a la Empresa Municipal de Mercados S.A. tal y como se puede apreciar en la siguiente lista: 
a) Producto ingresado por giro
https://opendata.socrata.com/Government/Productos-ingresados-por-giros/3jem-n9jx
b) Precios de los productos ingresados
https://opendata.socrata.com/Government/Precios-de-los-productos-ingresados/zs44-b9nw
c) Productos ingresados por procedencia
https://opendata.socrata.com/Government/Productos-ingresados-por-procedencia/mz3g-jqkw
d) Cantidad de vehículos ingresados
https://opendata.socrata.com/Government/Cantidad-de-veh-culos-ingresados/2pzf-bm2c
e) Volumen de productos ingresados
https://opendata.socrata.com/Government/Volumen-de-productos-ingresados/vmn2-8s9r

DIAGNÓSTICO: 
Después que recogimos los datos hicimos un pequeño análisis de los mismos y se encontró que entre los cinco archivos no contenían necesariamente los campos que existían en los data sets a pesar que la información era complementaria entre si. 
Por ejemplo, el data set <> no podía se cruzada con el data set <> porque este último solo contenía la descripción de los vehículos más no el origen y el destino de los mismos y los productos que trajeron al mercado mayorista, por lo tanto no se podía analizar ambas tablas en conjunto. 

[[Cuadro 1]] Relación de los datos empleados
>>Volumen_de_los_productos_ingresados
AÑO, CÓDIGO, PRODUCTO [[Meses del año]] TOTAL 
2006, 1, ACELGA ------------------------------------------------>>>

>>Precios_de_los_productos_ingresados
AÑO, CÓDIGO, PRODUCTO [[Meses del año]] TOTAL
2006, 0101, ACELGA ---------------------------------------- >

>>Producto_ingresados_por_procedencia
AÑO, CÓDIGO, DEPARTAMENTO, PROVINCIA, CÓDIGO PRODUCTO, PRODUCTO, [[meses del año]] TOTAL
2006, 0101, ACELGA ---->

>>Productos ingresados por giro
AÑO, GIRO [[Meses del año]] TOTAL
2006, HORTALIZA, ---->

>>Cantidad_de_vehículos_ingresados
AÑO, DESCRIPCIÓN, [[Meses del año]] 

Finalmente, después de analizar por algunos horas la situación de los datos que tuvimos en frente optamos por seleccionar el data set <<Producto_ingresados_por_procedencia>> porque nos pareció la tabla más completa. A esta tabla tuvimos que agregar el código general del producto porque en ella solo se consignó el código del producto específico, es decir, por ejemplo: a la papa se designa como 02 (código general) pero la papa amarilla tiene un código específico (0201) y la papa huayro otro similar (0202) por ejemplo. 

Desistimos de agregar el campo de GIRO que provenía del data set <> porque en el archivo de los metadatos no se incluye información de la fuente que designa a un alimento en una giro o en otro. Así por ejemplo no tuvimos claro si un ají era uno fruta u hortaliza. En esesentidoo, seleccionamos trabajar solamente con códigos. 

##PROCEDIMIENTO
Este procedimiento tuvo dos pasos. El primero de ellos fue normalizar el dataset e ingresar a Google Fusion Tables; y el segundo, fue generar otra tabla con los polígonos de las regiones que representan sus límites geográficos. 

En primer lugar, cuando nos referimos a normalización de datos, queremos decir que realizamos actividades de revisión y validación de los mismos, es decir, en la hoja de cálculos verificamos que no existieran datos duplicados, que las sumas estuvieran correctas y así sucesivamente. 

En segundo lugar, para generar el mapa con los polígonos de las regiones del país tuvimos que hacer lo siguiente:
a) Descargar los Límite Departamental (Fuente: INEI-2007) - Tamaño 3Mb en formado shape desde la página web del Ministerio de Medio Ambiente desde el siguiente enlace: http://geoservidor.minam.gob.pe/geoservidor/download.aspx
b) El conjunto de archivos comprimidos shape comprimidos en un archivo zip fueron subidos a la siguiente aplicación en lìnea (http://www.shpescape.com/upload/) que genera de manera automatizada una tabla en Google Fusion Tables con los datos georeferenciados de las regiones.   
Después de normalizar los datos y tener la tabla con los datos geográficos de las regiones, a través de la función de <> del Google Fusion Tables, fue posible extraer los datos de geo-referencia de la regiones y juntarlos con los datos de la tabla de <> de esta manera se dispuso de una tabla con información necesaria para el desarrollo de la aplicación. 
Recién cuando obtuvimos esta nueva tabla fue posible generar dos visualizaciones a modo de prototipo: la primera de ellas de denominado en red y la segunda en un mapa. Posteriormente ambas visualizaciones fueron incrustadas en un sitio web actualmente inactivo. 

##RESULTADOS 
La primera visualización que se obtuvo fue la de red. En este tipo visualización se puede observar la relación existente entre dos nodos y el vector que los une. En ese sentido, seoptóo por seleccionar el campo PRODUCTO y el campo PROVINCIA seleccionando el campo TOTAL para indicar el valor del vector que uniría ambos nodos. [[Ver Imagen 1]]

Imagen 1: Visualización de red en Google Fusion Tables 

Se obtiene pues una red de nodos relacionados entre sí que fácilmente explican las relaciones entre el origen de los productos y las ciudades desde donde llegan determinados productos a la ciudad de Lima. De esta manera es posible observar la complejidad de la relaciones que existen entre productos y las ciudades de origen. 

La segunda visualización es un mapa con la división de las regiones y por cada una de las regiones, al interactuar con ellas, se puede observar como emerge un globo de información que presenta un diagrama de barras e indica a través del mismo cual ha sido la cantidad de productos que ha provenido de aquella región. 

##CONCLUSIONES 
La visualización de datos, desde diferentes perspectivas, ayuda al análisis y el ejercicio de observar la realidad a través de diferentes modelos de tal manera que las decisiones puedan tomarse de manera más racional o al menos con un número mayor de referencias. 

Adicionalmente, la producción de los datos abiertos proporcionados por la Municipalidad de Lima son diversos y fragmentados y la construcción de una forma más sistemática y ordenada en su recolección y procesamiento es necesaria para construir sistemas de información más sólidos que permitan adoptar decisiones de manera más efectiva.  
