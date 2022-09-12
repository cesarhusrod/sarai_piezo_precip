# Precipitation and Piezometry in SARAI

The notebook takes data given by CSV input file (**sampling locations**) and

1. downloads precipitation and piezometric historical measurements from two internet sources,
2. associates previous measurements with sampling locations given by the input file and, finally,
3. generates output CSV files with measurements or interpolated measurements associated with the closest input sampling locations.

## Installation
It's pretty simple: you need [anaconda](https://www.anaconda.com/) installed on your computer and import environment file *environment_sarai.yml*. It generates a new environment that allows the notebook to run without problems.


## Data sources

1. Input CSV file with **sampling locations**. It contains, among others, a geographic location defined by coordinates and a unique field (*FID*). The notebook used it as location identification in output measurements CSV files (as column name).

This file must have the character ';' as the field delimiter. Sampling location coordinates are given by geographic coordinates longitude (field *X*) and latitude (field *Y*) in **WGS84** (**ETRS_4326**) system.

2. **Precipitation measurements**. Coded as an internal notebook variable, it points to a packed and compressed file (*\*.tar.gz*) located in [https://www.aemet.es/documentos/es/serviciosclimaticos/cambio_climat/datos_diarios/dato_observacional/rejilla_5km/v2/Serie_AEMET_v2_pcp_1951a2020_txt.tar.gz](https://www.aemet.es/documentos/es/serviciosclimaticos/cambio_climat/datos_diarios/dato_observacional/rejilla_5km/v2/Serie_AEMET_v2_pcp_1951a2020_txt.tar.gz). It contains three files:
   - *README*, which informs about the content of files,
   - *Master*, with precipitation grid coordinates and their IDs,
   - *historical precipitation file*, which contains interpolated precipitation measurements in a grid with a spatial resolution of 5x5 km, and temporal resolution of one day from 1951-01-01 to 2020-21-31. 
  
3. ****
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


