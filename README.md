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
  
3. **Piezometrical measurements**. Coded again as internal notebook variable, it points as default as a compressed file (*\*.zip*) available thought URL [https://www.miteco.gob.es/es/cartografia-y-sig/ide/descargas/basedatospiezometria_tcm30-533415.zip](https://www.miteco.gob.es/es/cartografia-y-sig/ide/descargas/basedatospiezometria_tcm30-533415.zip). This package is composed by two files:
   - The first one contains information about piezometers and geographical locations (*WGS84*)
   - The second one includes historical piezometrical measurements.

## Recommended structure of directories
The notebook code works with the following local structure for directories.
- *base_directory*, it could be anything in the local machine,
- *base_directory/notebooks*, it contains the notebook file,
- *base_directory/data*, where input CSV sampling locations file and precipitation and piezometric measurements files will be downloaded and decompressed,
- *base_directory/results*, where look for CSV output files.

## Association criteria between input sampling locations and precipitations/piezometric files
Only sources inside a 5 km buffer are taken into account.
### Precipitation
Two criteria:
1. Precipitation of the closest point to the sampling location.
2. Interpolated precipitation by inverse distance weighting average method for sources closer or equal to 5 km.

### Piezometry
Only one criterium
1. The most extended temporal piezometric series (for sources with measurements closest or equal to 5 km) is associated with each sampling location.

## Output files

Located in *output_dir* directory, defined as variable in the notebook code.

- *historico_precipitaciones_ponderado_distancia.csv*, with historical interpolated precipitation measurements, weighted by inverse of distance.

- *historico_precipitaciones_punto_mas_cercano.csv*, with historical interpolated precipitation equals to the closest point with measurements.

- *historico_piezometrias.csv*, with measurements of longest temporal serie of piezometry taken inside a buffer of, by default, 5.000 m.

- Several JPG files, of every figures generated and showed in the notebook.

## Contact

My name is César Husillos Rodríguez. You can contact me just via GitHub or through our e-mails: c.husillos@igme.es.

## License

This project is licensed under the terms of the GNU General Public License v3.0

## Example


