# Precipitation and Piezometry in SARAI

The notebook takes data given by CSV input file (**sampling locations**) and

1. downloads precipitation and piezometric historical measurements from two internet sources,
2. associates previous measurements with sampling locations given by the input file and, finally,
3. generates output CSV files with measurements or interpolated measurements associated with the closest input sampling locations.

## Installation
It's pretty simple: you need [anaconda](https://www.anaconda.com/) installed on your computer and import environment file *environment_sarai.yml*. It generates a new environment that allows the notebook to run without problems.

## Configuration file

It's named as **config.ini** and used by notebook as input parameters file. It's self-explaining (there are comments that describeeach parameter).

| Section      | Parameter name  | Description     |  Default value |
| :---        |    :----:   |          ---: |          ---: |
| directories | data_dir | Directory for downloading, unpacking and uncompressing input files given by URLs. | ./data |
| directories | output_dir | Output directory for CSV precipitation and piezometry associations. Plots are stored here too. | ./results |
|||||
|urls | piezometry_url | URL of piezometry data package. | https://www.miteco.gob.es/es/cartografia-y-sig/ide/descargas/basedatospiezometria_tcm30-533415.zip  |
|urls | precipitations_url | URL of precipitation data package. | https://www.aemet.es/documentos/es/serviciosclimaticos/cambio_climat/datos_diarios/dato_observacional/rejilla_5km/v2/Serie_AEMET_v2_pcp_1951a2020_txt.tar.gz |
|||||
| paths | locations_file | Input CSV file with locations of interest. | Point_Sampling_Murcia_desc.txt |
| paths | out_closest_prepic | Precipitation to the closest sample-node precipitation CSV output file. | historico_precipitaciones_punto_mas_cercano.csv |
| paths | out_interp_precip | Precipitation associated toeach sample location computed with the inverse distance to precipitation nodes. It's a CSV text output file.| historico_precipitaciones_ponderado_distancia.csv |
| paths | out_longer_piezo | Piezometry associated to sampling location. Again, a CSV text file. | historico_piezometrias.csv |
|||||
| buffer | radius | Distance (in m) to each sampling location where piezometry and precipitation locations are considered. | 5000 |
|||||
| fields | location_id_field | Identification field name (unique) for each sampling location. | FID |
| fields | location_lat | Field name with geographic longitude in sampling locations input file (locations_file). | Y |
| fields | location_lon | Field name with geographic latitude in sampling locations input file (locations_file). | X |
| fields | precip_date | Field name inside precipitation file (precipitations_url) that contains dates when precipitation was computed. | fecha |
| fields | precip_lon | Field name that contains geograhic longitude for each node in preipitations grid. | longitude  |
| fields | precip_lat | Field name that contains geograhic latitude for each node in preipitations grid. | latitude |
| fields | piezo_id_field | Identification field name (unique) for each piezometer (piezometry_url). | IDPIEZ |
| fields | piezo_date | Field name inside piezometrical levels file (inside piezometry_url package) that contains dates when piezometry level was taken. | FechaP |
| fields | piezo_lat | Field name with geographic longitude in piezometers input file (inside piezmetry_url package). | CY89_HUSO30 |
| fields | piezo_lon | Field name with geographic latitude in piezometers input file (inside piezmetry_url package). | CX89_HUSO30 |
| fields | piezo_field | Field name that contains piezometrical measurement. | Cota_NP_msnm |
|||||
| crs | geographic | Geographic system of coordinates. | EPSG:4326 |
| crs | projected | Projected system of coordinates. | EPSG:25830 |

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

Located in **output_dir** (*./results*) directory given by *config.ini* configuration file.

- **out_interp_precip** (*historico_precipitaciones_ponderado_distancia.csv*), with historical interpolated precipitation measurements, weighted by inverse of distance.

- **out_closest_prepic** (*historico_precipitaciones_punto_mas_cercano.csv*), with historical interpolated precipitation equals to the closest point with measurements.

- **out_longer_piezo** (*historico_piezometrias.csv*), with measurements of longest temporal serie of piezometry taken inside a buffer of, by default, **radius** (*5.000 m*).

- JPG files: all figures generated and showed in the notebook.

## Contact

My name is César Husillos Rodríguez. You can contact me just via GitHub or through our e-mails: c.husillos@igme.es.

## License

This project is licensed under the terms of the GNU General Public License v3.0

## Example

We will show you some screen captures for illustrating the notebook algorithm.

### 1. Loading locations of interest

First of all, the input data file. It's a CSV text format file. Field separator is given by character ','. Thousand marker is a point '.'.

```python
locations_file = config.get('paths', 'locations_file') # reading input CSV file path from 'config.ini' file
df_loc = pd.read_csv(locations_file, sep=';', decimal=',') 
id_loc = config.get('fields', 'location_id_field') # reading field ID from 'config.ini' file
df_loc = df_loc.set_index(id_loc, drop=False)
print(df_loc.info()) # showing input dataframe info
```

After that, plot sampling locations.

![Sampling locations](/sample_images/localizaciones_de_muestreo.jpg)

### 2. Downloading and processing precipitation data

Next step is to load precipitation data, filtering to interesting area and plotting both on a map.

![Sampling locations and precipitations grid](/sample_images/nodos_precipitacion_En_area_de_muestreo.jpg)

As it was mentioned before, there are two association algorithms. Next figure shows the closest sources implementation for a precipitation node of the grid (given by ID = 1868).

And the next one, shows precipitation nodes associated to sampling locations.

![Sampling locations and selected node of the precipitations grid](/sample_images/nodos_de_precipitacion_seleccionados.jpg)

and the histogram of distances between associated locations

![distance between sampling and precipitation node locations histogram ](/sample_images/histograma_distancias_nodos_precipitacion-puntos_muestreo.jpg)


### 3. Downloading and processing piezomtryc data

Similar procedure is followed in case of piezometrical measurements.

![Sampling locations and piezometers grid](/sample_images/piezometros_en_zona_de_muestreo.jpg)

In this case, association is given between piezometry and samplig locations whose 
- temporal length series is the longest one and
- distance is lower than a number of meters given by *radius* parameter in input config.ini file.

Following image shows piezometers associated to sampling locations.

![Sampling locations and selected node of the piezometer locations](/sample_images/piezometros_seleccionados.jpg)

and the histogram of distances between these associations.

![distance between sampling and piezometer locations histogram ](/sample_images/histograma_distancias_a_piezometros.jpg)

Here is the the histogram that shows number of sampling locations associated to each piezometer.

![association between sampling and piezometer locations histogram ](/sample_images/localizaciones_asociadas_a_piezometros.jpg)

And finally, following figure shows sampling locations associated to the most popular piezometer (IDPIEZ=2015).

![Samplnig locations associated to a given piezometer](/sample_images/localizaciones_asociadas_piezometro_2015.jpg)
