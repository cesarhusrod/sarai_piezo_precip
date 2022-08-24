# Precipitación y Piezometría en SARAI

El notebook generado toma las **localizaciones de muestreo** dadas por un fichero de entrada y 

1. descarga información de precipitación y piezometría de dos fuentes de la red,
2. asocia cada una de las localizaciones con las ubicaciones en las que se han tomado las medidas de las magnitudes anteriores y, finalmente,
3. genera ficheros CSV en los que se dan las medidas temporales de esas magnitudes para cada localización de muestreo.

## Fuentes de datos

1. Fichero CSV con las **localizaciones de muestreo**. Contiene, entre otras, la ubicación geográfica de dichos puntos y un campo con valor único para cada localización (FID), que se empleará para determinar las medidas asociadas a cada una de ellas (como nombre de columnas en los ficheros de salida).
2. **Medidas de precipitación**, comprimido y empaquetado (*.tar.gz) y ubicado en la web. Viene dado por 3 ficheros:
   - README, con información sobre el contenido del paquete,
   - Master, con ifnromación sobre la ubicación de los puntos de la malla y su identificador,
   - fichero de datos, que contiene medidas interpoladas con una resolución espacial de malla 5x5 km, y una resolución temporal diaria desde el 01/01/1951 hasta el 31/12/2020.
3. **Medidas de pieometría**, comprimido (ZIP). Es una base de datos MS Access con dos tablas:
   - Una que contiene informacion sobre los piezómetros y su ubicación (junto con su identificador)
   - Otra, con medidas piezométricas.

## Directorios recomendados

La estructura de directorios pensada para el correcto funcionamiento del notebook es

1. *directorio_base*, que puede ser cualquiera,
2. *directorio_base/notebooks*, donde ubicaremos el notebook,
3. *directorio_base/datos*, donde el notebook buscará los ficheros de entrada y descargará, descomprimirá y desempaquetará los ficheros de precipitación y piezometría,
4. *directorio_base/resultados*, donde almacenará los ficheros CSV con el resultado de la asociación entre loclizaciones de muestreo y puntos de medida de la precipitación y piezometría.

## Criterios de asociación entre localizaciones geográficas

Sólo se considerarán fuentes cercanas a las ubicaciones de muestreo dentro de un radio de 5 km.

### Para la precipitación

Dos criterios:

1. el de medidas asociadas al **punto más cercano**.
2. el de la **media ponderada con el inverso de la distancia para las ubicaciones próximas** (distancia menor de 5 km).


### Para la piezometría

Un único criterio que consiste en

1. Se asocia la medida cuya **serie temporal de medidas sea la más larga dentro** de las localizaciones válidas para cada localización de muestreo.
