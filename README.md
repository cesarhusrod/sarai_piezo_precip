![Funding Ministery](/sample_images/ministerio_ciencia_logo.jpg)


# Precipitation and Piezometry in SARAI

The notebook takes data given by CSV input file (**sampling locations**) and

1. downloads precipitation and piezometric historical measurements from two internet sources,
2. associates previous measurements with sampling locations given by the input file and, finally,
3. generates output CSV files with measurements or interpolated measurements associated with the closest input sampling locations.

## Installation
It's pretty simple:

1. Install [anaconda](https://www.anaconda.com/) on your computer and 
2. import environment file *environment_sarai.yml*. It generates a new environment that allows the notebook to run without problems.
   
After executing the **Anaconda.Navigator** program, the following screenshots show you how to do it and launch the repository notebook step by step.

1. Select *Environments* tab and click on *Import* button.

![Anaconda environments backend management](/sample_images/environment/administracion_entornos_anaconda.jpg)

2. Select *Local drive* option and search for repository environment file (*environment_sarai.yml). Set a name for your imported environment and press *Import* button.
   
![Anaconda: how to import environment](/sample_images/environment/importar_entorno_sarai.jpg)

3. Click on your enviroment name for activate it.
   
![Anaconda has successfully installed new environment called sarai](/sample_images/environment/entorno_sarai_instalado.jpg)

Now, sarai environmet is activated and ready for use.

![Anaconda activated sarai environment](/sample_images/environment/entorno_sarai_activado.jpg)

4. Change to *Home* tab. You can see all options available for selected environment. Please, check *sarai* environment is selected (green rectangle in figure). If *Jupyter notebbok* grid entry must be installed, please, clik button to do it. It it's previously installed, click *Launch* button.

![Anaconda: how to lauch notebook interface](/sample_images/environment/lanzar_notebook_en_entorno_sarai.jpg)

5. Anaconda notebook interface is loaded as a new tab in your favourite web browser.
   
![Anaconda running notebook interface](/sample_images/environment/notebook_en_entorno_sarai_operativo.jpg)

6. Follow link options to access your repository folder. Then click on sarai notebook (*precipitacion_y_piezometria.ipynb*).
   
![Anaconda: notebook selection](/sample_images/environment/seleccion_notebook_en_entorno_sarai.jpg)

7. Previous operation loads the selected notebook. 
   
![sarai Anaconda notebook ready for use](/sample_images/environment/cargado_notebook_en_entorno_sarai.jpg)

Congratulations! Now you can execute or edit what you want in this notebook.


## Configuration file

It's named **config.ini** and is used by the notebook as an input parameters file. It's self-explaining (some comments describe each parameter).

*config.ini* is a file text. It is structured in two types of lines:
   1. Section line.
   
      It represent a group of parameters. The syntax is

      *[Section name]*

      (inside [])

   2. Parameter line.
      
      It is used to define
      - a paramater name, 
      - its value, and 
      - optionally, a brief description (after an ' ' and a '#' characters). 
  
      The syntax for each line is a follows:

      *parameter_name=parameter_value # optional comment*

      As said previously, if you don't want use comments at his line, the other valid syntax for each line would be

      *parameter_name=parameter_value*   


Default parameters values allows you to run and test all cells of repository notebook. If you want to set new values in some parameters, take into account following advices:

1. Only one value is valid for each parameter.
2. All values are considered as text by notebook.
3. The notebook cells that process URL parameters were developped exclusively for given default values. If you change them, you'll have to adapt then according to compression and/or package methods used by new sources pointed by parameters group by *urls* section.

This table shows you information about parameters you can find in *config.ini* file:


| Section     |   Parameter name   |                                                                                                                                                 Description |                                                                                                                                                Default value |
| :---------- | :----------------: | ----------------------------------------------------------------------------------------------------------------------------------------------------------: | -----------------------------------------------------------------------------------------------------------------------------------------------------------: |
| directories |      data_dir      |                                                     It's the directory where input files given by section *URLs* are downloaded, unpacked and uncompressed. |                                                                                                                                                       ./data |
| directories |     output_dir     |               It's the output directory where CSV precipitation and piezometric associations are stored. Plots generated by the notebook are kept here too. |                                                                                                                                                    ./results |
|             |                    |                                                                                                                                                             |                                                                                                                                                              |
| urls        |   piezometry_url   |                                                                                                                            The piezometry data package URL. |                                                           https://www.miteco.gob.es/es/cartografia-y-sig/ide/descargas/basedatospiezometria_tcm30-533415.zip |
| urls        | precipitations_url |                                                                                                                         The precipitation data package URL. | https://www.aemet.es/documentos/es/serviciosclimaticos/cambio_climat/datos_diarios/dato_observacional/rejilla_5km/v2/Serie_AEMET_v2_pcp_1951a2020_txt.tar.gz |
|             |                    |                                                                                                                                                             |                                                                                                                                                              |
| paths       |   locations_file   |                                                                                   It's the CSV input file with information about the locations of interest. |                                                                                                                               Point_Sampling_Murcia_desc.txt |
| paths       | out_closest_prepic |                                                        It's the CSV precipitation output file obtained using the closest sample-node association algorithm. |                                                                                                              historico_precipitaciones_punto_mas_cercano.csv |
| paths       | out_interp_precip  | It refers to the precipitation associated with each sample location computed with the inverse distance to precipitation nodes. It's a CSV text output file. |                                                                                                            historico_precipitaciones_ponderado_distancia.csv |
| paths       |  out_longer_piezo  |                                                                              Piezometry associated with the sampling location. Again, it's a CSV text file. |                                                                                                                                   historico_piezometrias.csv |
|             |                    |                                                                                                                                                             |                                                                                                                                                              |
| buffer      |       radius       |                                                         Distance (in m) to each sampling location where piezometry and precipitation points are considered. |                                                                                                                                                         5000 |
|             |                    |                                                                                                                                                             |                                                                                                                                                              |
| fields      |    location_id     |                                                                           It's the numerical identification field name (unique) for each sampling location. |                                                                                                                                                          FID |
| fields      |   location_label   |                                                                             Field used to identify sampling locations in output header precipitation files. |                                                                                                                                                        PS_ID |
| fields      |    location_lat    |                                                                     Field name with geographic longitude in sampling locations input file (locations_file). |                                                                                                                                                            Y |
| fields      |    location_lon    |                                                                      Field name with geographic latitude in sampling locations input file (locations_file). |                                                                                                                                                            X |
| fields      |    precip_date     |                                                     Field name inside precipitation file (precipitations_url). It contains dates of computed precipitation. |                                                                                                                                                        fecha |
| fields      |     precip_lon     |                                                                   The field name contains the geographic longitude for each node in the precipitation grid. |                                                                                                                                                    longitude |
| fields      |     precip_lat     |                                                                    The field name contains the geographic latitude for each node in the precipitation grid. |                                                                                                                                                     latitude |
| fields      |      piezo_id      |                                                                                    Identification field name (unique) for each piezometer (piezometry_url). |                                                                                                                                                       IDPIEZ |
| fields      |     piezo_date     |                                    Field name inside piezometric levels file (inside piezometry_url package). It keeps dates of piezometric level measured. |                                                                                                                                                       FechaP |
| fields      |     piezo_lat      |                                                         Field name with geographic longitude in the piezometers input file (inside piezometry_url package). |                                                                                                                                                  CY89_HUSO30 |
| fields      |     piezo_lon      |                                                          Field name with geographic latitude in the piezometers input file (inside piezometry_url package). |                                                                                                                                                  CX89_HUSO30 |
| fields      |   piezo_measure    |                                                                                                  It's the field name that contains piezometric measurement. |                                                                                                                                                 Cota_NP_msnm |
|             |                    |                                                                                                                                                             |                                                                                                                                                              |
| crs         |     geographic     |                                                                                                                           Geographic system of coordinates. |                                                                                                                                                    EPSG:4326 |
| crs         |     projected      |                                                                                                                            Projected system of coordinates. |                                                                                                                                                   EPSG:25830 |

## Data sources

1. Input CSV file with **sampling locations**. It's given by *locations_file* parameter in *config.ini* file. It contains, among others, a geographic location defined by coordinates and a unique field (*location_id_field* parameter in *config.ini* file). The notebook used it as location identification in output measurements CSV files (as column name).

This file must have the character ';' as the field delimiter. Sampling location coordinates are given by geographic coordinates longitude (field *location_lon*) and latitude (field *location_lat*) in *geographic* (*EPSG:4326*) reference system of coordinates.

2. **Precipitation measurements**. Coded as an input parameter *precipitations_url* in the *config.ini* configuration file. It points by default to a packed, compressed file (*\*.tar.gz*) located in [https://www.aemet.es/documentos/es/serviciosclimaticos/cambio_climat/datos_diarios/dato_observacional/rejilla_5km/v2/Serie_AEMET_v2_pcp_1951a2020_txt.tar.gz](https://www.aemet.es/documentos/es/serviciosclimaticos/cambio_climat/datos_diarios/dato_observacional/rejilla_5km/v2/Serie_AEMET_v2_pcp_1951a2020_txt.tar.gz). It contains three files:
   - *README*, which informs about the content of files,
   - *Master*, with precipitation grid coordinates and their IDs,
   - *historical precipitation file*, which contains interpolated precipitation measurements in a grid with a spatial resolution of 5x5 km, and temporal resolution of one day from 1951-01-01 to 2020-21-31. 
  
3. **Piezometric measurements**. Coded again as input parameter *piezometry_url* in the *config.ini* configuration file. It points by default to a compressed file (*\*.zip*) available thought URL [https://www.miteco.gob.es/es/cartografia-y-sig/ide/descargas/basedatospiezometria_tcm30-533415.zip](https://www.miteco.gob.es/es/cartografia-y-sig/ide/descargas/basedatospiezometria_tcm30-533415.zip). This package is composed by two files:
   - The first one contains information about piezometers and geographical locations (with *geometry* as coordinate reference system)
   - The second one includes historical piezometrical measurements.

## Association criteria between input sampling locations and precipitations/piezometric files

Only sources inside a 5 km buffer are taken into account.

### Precipitation
Two criteria applied:
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

CSV output files have following structure: 

*date,ID1, ID2, ID3,...,IDN*

where IDs are the unqie values that identify precipitation grid nodes or piezometers.

## Acknowledgements

This work is part of the SARAI project of the Spanish Science and Innovation Ministry with reference PID2020-116540RB-C22 funded by MCIN/ AEI /10.13039/501100011033. This work has been performed within the SARAI subproject leaded by the Geological and Mining Institute of Spain (CN IGME), which is a research body integrated into the Higher Council for Scientific Research (CSIC). 

Project link: [https://webwp.igme.es/sarai/index.php/en/home/](https://webwp.igme.es/sarai/index.php/en/home/)

## Contact

My name is César Husillos Rodríguez. You can contact me just via GitHub or through our e-mails: c.husillos@igme.es.

## License

This project is licensed under the terms of the GNU General Public License v3.0

## Example

We will show you some screen captures for illustrating the notebook algorithm.

### 1. Loading locations of interest

First, the input data file is a CSV text format file with the character  ';' as the field separator and '.' as the thousand marker.

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

The next step is to load precipitation data, filtering to the exciting area and plotting both on a map.

![Sampling locations and precipitations grid](/sample_images/nodos_precipitacion_En_area_de_muestreo.jpg)

As mentioned before, there are two association algorithms. Taking into account the 'buffer' mode, the assotiations between sampling places and precipitation node grids are showed in the following picture.

![Number of precipitation nodes linked to sampling locations](/sample_images/histograma_asociacion_nodos_precipitacion-puntos_muestreo.jpg)

In case of the closest association method is applied, the next one shows the closest sources implementation for a precipitation node of the grid (given by ID = 1868).

![Sampling locations associated to precipitation node grid labelled as 1868](/sample_images/localizaciones_mas_proximas_al_nodo_de_precipitacion_1868.jpg)

Next figure shows all precipitation nodes associated with sampling locations.

![Sampling locations and selected node of the precipitations grid](/sample_images/nodos_de_precipitacion_seleccionados.jpg)

and the histogram of distances between associated locations

![distance between sampling and precipitation node locations histogram ](/sample_images/histograma_distancias_nodos_precipitacion-puntos_muestreo.jpg)


Of course, the notebook generates two CSV files with 

- precipitation related to the closest node-sampling location, and
- precipitation computed used the inverse of distance node-sampling location for grid nodes inside a buffer of predefined distance.

Column names are :
- date of measure and
- 'location_lable' field from the *config.ini* file, that identifies each sampling location.
  
### 3. Downloading and processing piezometric data

The process applied to piezometric measures is the same.

![Sampling locations and piezometers grid](/sample_images/piezometros_en_zona_de_muestreo.jpg)

In this case, the association is given between piezometric and sampling locations whose 
- temporal length series is the longest one and
- distance is lower than the number of meters given by the *radius* parameter in the input *config.ini* file.

The following image shows piezometers associated with sampling locations.

![Sampling locations and selected node of the piezometer locations](/sample_images/piezometros_seleccionados.jpg)

And this one the histogram of distances between these associations.

![distance between sampling and piezometer locations histogram ](/sample_images/histograma_distancias_a_piezometros.jpg)

Here is the the histogram that shows number of sampling locations associated to each piezometer.

![association between sampling and piezometer locations histogram ](/sample_images/localizaciones_asociadas_a_piezometros.jpg)

And finally, the following figure shows sampling locations associated with the most popular piezometer (IDPIEZ=2015).

![Sampling locations associated to a given piezometer](/sample_images/localizaciones_asociadas_piezometro_2015.jpg)

Again, the notebook generates a CSV file with associated piezometric measurements to sampling locations as output.


