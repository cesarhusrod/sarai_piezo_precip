# Precipitación y Piezometría en SARAI

El notebook toma las **localizaciones de muestreo** dadas por un fichero de entrada y 

1. descarga información de precipitación y piezometría en España de dos fuentes de la red,
2. asocia cada una de las localizaciones con las ubicaciones en las que se han tomado las medidas de las magnitudes anteriores y, finalmente,
3. genera ficheros CSV en los que se dan las medidas temporales de esas magnitudes para cada localización de muestreo.


## Install
It's pretty simple: you need [anaconda](https://www.anaconda.com/) installed on your computer and import environment file *environment_sarai.yml*. It generates a new environment that allows the notebook to run without problems.


## Fuentes de datos

1. Fichero CSV con las **localizaciones de muestreo**. Contiene, entre otras, la ubicación geográfica de dichos puntos y un campo con valor único para cada localización (FID), que se empleará para determinar las medidas asociadas a cada una de ellas (como nombre de columnas en los ficheros de salida).

Este fichero puede ser cualquier CSV que tenga el carácter ';' como separador de campos. Las coordenadas de las ubicaciones de muestreo vendrán dadas por los campos *X* e *Y* con valores geográficos de longitud y latitud en el sistema WGS64 (ETRS:4326), respectivamente.

2. **Medidas de precipitación**, comprimido y empaquetado (*.tar.gz) y ubicado en la siguiente dirección web:[https://www.aemet.es/documentos/es/serviciosclimaticos/cambio_climat/datos_diarios/dato_observacional/rejilla_5km/v2/Serie_AEMET_v2_pcp_1951a2020_txt.tar.gz](https://www.aemet.es/documentos/es/serviciosclimaticos/cambio_climat/datos_diarios/dato_observacional/rejilla_5km/v2/Serie_AEMET_v2_pcp_1951a2020_txt.tar.gz). Viene dado por 3 ficheros:
   - README, con información sobre el contenido del paquete,
   - Master, con ifnromación sobre la ubicación de los puntos de la malla y su identificador,
   - fichero de datos, que contiene medidas interpoladas con una resolución espacial de malla 5x5 km, y una resolución temporal diaria desde el 01/01/1951 hasta el 31/12/2020.
3. **Medidas de pieometría**, comprimido (ZIP). Es una base de datos MS Access accesible desde [https://www.miteco.gob.es/es/cartografia-y-sig/ide/descargas/basedatospiezometria_tcm30-533415.zip](https://www.miteco.gob.es/es/cartografia-y-sig/ide/descargas/basedatospiezometria_tcm30-533415.zip), y que consta de dos tablas:
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

## Ficheros de salida

Ubicados en el directorio *output_dir* definido en el notebook.

- *historico_precipitaciones_ponderado_distancia.csv*, con medidas de precipitación interpolada según inverso de las distancias a los nodos de precipitación dentro de un buffer de, por defecto, 5.000 m de distancia a cada localización de muestreo.

- *historico_precipitaciones_punto_mas_cercano.csv*, con medidas de precipitación para cada localización de muestreo iguales al punto más cercano de medida de precipitación (dentro del buffer de 5.000 m por defecto).

- *historico_piezometrias.csv*, con las medidas de piezometría correspondientes a la serie más larga de todos los piezometros que están a una distancia igual o inferior al radio del buffer de cada punto de muestreo (por defecto 5.000 m).

- Ficheros de tipo JPG de todas las representaciones generadas en el notebook, tanto de distribución espacial como de estadísticas.

## Contact

My name is César Husillos Rodríguez. You can contact me just via GitHub or through our e-mails: c.husillos@igme.es.

## License

This project is licensed under the terms of the GNU General Public License v3.0

## Example


