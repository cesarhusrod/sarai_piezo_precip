![Funding Ministery](/sample_images/ministerio_ciencia_logo.jpg)


# Precipitación y piezometría en SARAI

El objetivo de este Notebook es completar la información de lugares de muestreo con datos de precipitación y piezometría. Para ello:

1. Descarga de la información de medidas históricas de precipitación y piezometría de dos URLs en la web,
2. Asocia las ubicaciones de muestreo con aquellas en las que se han tomado datos de precipitación y piezometría y, finalmente,
3. Genera ficheros de texto en formato CSV para ambas magnitudes.

## Descarga del repositorio

Debe tener el [cliente GIT](https://git-scm.com/downloads) instalado en su ordenador.

Lo siguiente es abrir la consola de GIT (en el caso de trabajar en Windows) o la terminal (si lo hace en LINUX o MAC) y escribir la siguiente línea de código:

```git clone https://git.igme.es/chusillos/sarai_piezo_precip.git```

eso creará una carpeta de nombre *sarai_piezo_precip* en su disco duro con todo el código necesario y los ficheros de ejemplo. Así de simple.

## Instalación

El proceso es muy sencillo:

1. Instale [anaconda](https://www.anaconda.com/) en su ordenador.
2. Instale el entorno de ejecución definido en el fichero *environment_sarai.yml* usando la interfaz de administración de *Anaconda.Navigator*.

Tras realizar estar operaciones, podrá 
- cargar el nuevo entorno, 
- lanzar la aplicación de Jupyter Notebook en su navegador, 
- cargar el fichero de código (*precipitacion_y_piezometria.ipynb*) y 
- ejecutarlo sin problemas.

### Proceso de importación del entorno

Siga los siguientes pasos para importar el entorno:

1. Ejecute en su ordenador el programa **Anaconda.Navigator**.

2. Seleccione la pestaña de *Environments* y haga clic sobre el botón *Import*.

![Interfaz de administración de entornos de Anaconda.Navigator](/sample_images/environment/administracion_entornos_anaconda.jpg)

3. Seleccione la opción *Local drive* y busque en su disco el directorio donde ha descargado el repositorio. Ahí encontrará el fichero *environment_sarai.yml*. Lo siguiente es poner un nombre al nuevo entorno que creará y presionar el botón *Import*.
   
![Anaconda: cómo importar un entorno](/sample_images/environment/importar_entorno_sarai.jpg)

4. Haga clic sobre el nuevo entorno para activarlo.
   
![Nuevo entorno llamado sarai entre los disponibles en Anaconda](/sample_images/environment/entorno_sarai_instalado.jpg)

Ahora, el entorno llamado en este ejemplo *sarai* está activo y listo para su uso.

![Entorno sarai activo en Anaconda](/sample_images/environment/entorno_sarai_activado.jpg)

5. Cambie a la pestaña *Home*. Ahora podrá ver todas las aplicaciones disponibles para el entorno seleccionado. Por favor, asegúrese de que su nuevo entorno está seleccionado (rectángulo verde que se muestra en la siguiente captura de pantalla). Si la opción *Jupyter notebook* está instalada, pulse bobre el botón *Launch*. Si no es el caso, primero debe pulsar sobre el botón *Install* y, tras finalizar la instalación, sobre el botón *Launch*.

![Cómo se lanza la aplicación de Jupyter Notebook en Anaconda](/sample_images/environment/lanzar_notebook_en_entorno_sarai.jpg)

6. Tras lanzar la aplicación de *Jupyter Notebook*, se abrirá una pestaña en su navegador predeterminado. 
   
![Interfaz web de Jupyter notebook funcionando](/sample_images/environment/notebook_en_entorno_sarai_operativo.jpg)

7. Elija la ruta donde haya descargado el repositorio de SARAI haciendo clic sobre la secuencia de subdirectorios adecuada. Después, haga clic sobre el fichero del Notebook de SARAI (*precipitacion_y_piezometria.ipynb*).
   
![Selección de Notebook en la interfaz web de Jupyter Notebook](/sample_images/environment/seleccion_notebook_en_entorno_sarai.jpg)

8. Finalmente, su Notebook está cargado en el navegador. 
   
![Notebook de SARAI preparado para su edición y ejecución en su navegador](/sample_images/environment/cargado_notebook_en_entorno_sarai.jpg)

¡Enhorabuena! Ya puede ejecutar el código de las celdas de notebook (o cambiar lo que necesite).

## Fichero de configuración

Es el fichero de texto *config.ini*.  Está en el directorio base del repositorio. Se usa para personalizar todos los parámetros del notebook. Es autoexplicativo en el sentido en que en el propio fichero puede obtener una breve descripción de lo que es cada parámetro.

Las filas del fichero *config.ini* son de dos tipos:
- Línea de sección.
  
   Una sección presenta una forma de agrupar los parámetros por funcionalidad. No tiene más función que esa aunque es muy importante ya que organiza la información, haciendo fácil su localización cuando el número de parámetros es elevado. Su sintaxis es
      
    ```[Nombre de sección]```
      
- Línea de parámetro.

   En ella se definen:
   
   - el nombre del parámetro,
   - el valor del parámetro, y
   - de forma opcional, puede incluir una breve descripción del parámetro. Se escribe después de un espacio en blanco (' ') y de una almohadilla ('#').
  
   La sintaxis completa tiene la forma:

    ```nombre_parámetro=valor_de_parámetro # descripción```

   La sintaxis mínima

    ```nombre_parámetro=valor_de_parámetro```

   Si no se desea asignar un valor a un parámetro, simplemente se deja el espacio en blanco.

Los valores por defecto de los parámetros permiten ejecutar sin errores todas las celdas del Notebook. En caso de modificar esos valores, tenga en cuenta que con la actual implementación:

   - Sólo es válido un valor por cada parámetro.
   - Todos los valores que se establezcan son considerados como cadenas de caracteres por el Notebook.
   - Las celdas que procesan la descarga de ficheros desde URLs en la web están codificadas específicamente para los valores asignados por defecto. Si cambia esas URLs, tendrá que adaptar el código que procesa los ficheros o paquetes que desee descargar.
  
La siguiente tabla muestra los parámetros actualmente personalizables en el fichero *config.ini*:


| Sección     | Nombre de parámetro |                                                                                                                                                                                                                                                                                                                                                                                         Descripción |                                                                                                                                                                               Valor por defecto |
| :---------- | :-----------------: | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| directories |      data_dir       |                                                                                                                                                                                                                                                          Es el directorio donde se descargan, descomprimen y desempaquetan los ficheros de entrada establcidos en la sección *URLs* are downloaded. |                                                                                                                                                                                          ./data |
| directories |     output_dir      |                                                                                                                                                                                                                      Directorio de salida. Aquí guardarán los ficheros de texto CSV con información de precipitación y piezometría. También almacenará todas las figuras generadas por el Notebook. |                                                                                                                                                                                       ./results |
|             |                     |                                                                                                                                                                                                                                                                                                                                                                                                     |                                                                                                                                                                                                 |
| urls        |   piezometry_url    |                                                                                                                                                                                                                                                                                                                                        Dirección web del paquete que contiene datos de piezometría. |                                                                  [enlace piezometría](https://www.miteco.gob.es/es/cartografia-y-sig/ide/descargas/basedatospiezometria_tcm30-533415.zip) (ZIP) |
| urls        | precipitations_url  |                                                                                                                                                                                                                                                                                                                                  Dirección web del paquete que contiene los datos de precipitación. | [enlace precipitaciones](https://www.aemet.es/documentos/es/serviciosclimaticos/cambio_climat/datos_diarios/dato_observacional/rejilla_5km/v2/Serie_AEMET_v2_pcp_1951a2020_txt.tar.gz) (TAR.GZ) |
|             |                     |                                                                                                                                                                                                                                                                                                                                                                                                     |                                                                                                                                                                                                 |
| paths       |   locations_file    |                                                                                                                                                                                                                                                                                           Ruta al fichero de texto en formato CSV que contiene información sobre los puntos de muestreo de interés. |                                                                                                                                                                  Point_Sampling_Murcia_desc.txt |
| paths       | out_closest_prepic  |                                                                                                                                                                        Nombre del fichero de texto en formato CSV. Se almacenará en el directorio de salida establecido por el parámetro *output_dir*. Contendrá los datos de precipitación asociados mediante el algoritmo de puntos más próximos. |                                                                                                                                                 historico_precipitaciones_punto_mas_cercano.csv |
| paths       |  out_interp_precip  | Nombre del fichero de texto en formato CSV. Se almacenará en el directorio de salida establecido por el parámetro *output_dir*. Los datos de precipitación para cada punto de muestreo se determinan mediante la media ponderada por el inverso de la distancia a los puntos que contienen medidas de precipitación dentro de una distancia máxima, que está determinada por el parámetro *radius*. |                                                                                                                                               historico_precipitaciones_ponderado_distancia.csv |
| paths       |  out_longer_piezo   |                Nombre del fichero de salida en formato CSV que contendrá los datos de piezometría asociados a los puntos de muestreo. Habrá medidas siempre que la distancia entre punto de muestreo y punto de medida piezométrico sea inferior a la distancia dada por el parámetro *radius*. Si hay varios puntos con medidas piezométricas, se asocia el que tenga la serie temporal más larga. |                                                                                                                                                                      historico_piezometrias.csv |
|             |                     |                                                                                                                                                                                                                                                                                                                                                                                                     |                                                                                                                                                                                                 |
| buffer      |       radius        |                                                                                                                                                                                                                                                                                           Distancia (en metros) máxima entre punto de muestreo y punto con medición de precipitación o piezometría. |                                                                                                                                                                                            5000 |
|             |                     |                                                                                                                                                                                                                                                                                                                                                                                                     |                                                                                                                                                                                                 |
| fields      |     location_id     |                                                                                                                                                                                                                                          Nombre del campo en el fichero de localizaciones de muestreo (*locations_file*) cuyos valores identifican de forma unívoca a cada una de esas ubicaciones. |                                                                                                                                                                                             FID |
| fields      |   location_label    |                                                                                                                                                                                                                         Nombre del campo alfanumérico en el fichero de localizaciones de muestreo (*locations_file*)) que identifica de forma unívoca a cada una de las localizaciones de muestreo. |                                                                                                                                                                                           PS_ID |
| fields      |  location_lon_geo   |                                                                                                                                                                                Nombre del campo del fichero de localizaciones de muestreo (*locations_file*) que contiene la longitud geográfica de cada una de ellas  (el sistema de referencia está dado por el parámetro *location_geographic*). |                                                                                                                                                                                               X |
| fields      |  location_lat_geo   |                                                                                                                                                                                 Nombre del campo del fichero de localizaciones de muestreo (*locations_file*) que contiene la latitud geográfica de cada una de ellas  (el sistema de referencia está dado por el parámetro *location_geographic*). |                                                                                                                                                                                               Y |
| fields      |  location_lon_proj  |                                                                                                                                                                                  Nombre del campo del fichero de localizaciones de muestreo (*locations_file*) que contiene la longitud proyectada de cada una de ellas (el sistema de referencia está dado por el parámetro *location_projected*). |                                                                                                                                                                                      Lon_ETRS89 |
| fields      |  location_lat_proj  |                                                                                                                                                                                   Nombre del campo del fichero de localizaciones de muestreo (*locations_file*) que contiene la latitud proyectada de cada una de ellas (el sistema de referencia está dado por el parámetro *location_projected*). |                                                                                                                                                                                      Lat_ETRS89 |
| fields      |     precip_date     |                                                                                                                                                                                                                                    Nombre del campo que contiene las fechas en las que se registraron las medidas de precipitación (dentro del fichero dado por el parámetro *precipitations_url*). |                                                                                                                                                                                           fecha |
| fields      |   precip_lon_geo    |                                                                                                                                                                                                                 Nombre del campo que contiene la longitud geográfica de cada punto de medida de precipitación (dado por el sistema de referencia establecido por el parámetro *precip_geographic*). |                                                                                                                                                                                       longitude |
| fields      |   precip_lat_geo    |                                                                                                                                                                                                                  Nombre del campo que contiene la latitud geográfica de cada punto de medida de precipitación (dado por el sistema de referencia establecido por el parámetro *precip_geographic*). |                                                                                                                                                                                        latitude |
| fields      |   precip_lon_proj   |                                                                                                                                                                                                                  Nombre del campo que contiene la longitud geográfica de cada punto de medida de precipitación (dado por el sistema de referencia establecido por el parámetro *precip_projected*). |                                                                                                                                                                                                 |
| fields      |   precip_lat_proj   |                                                                                                                                                                                                                   Nombre del campo que contiene la latitud geográfica de cada punto de medida de precipitación (dado por el sistema de referencia establecido por el parámetro *precip_projected*). |                                                                                                                                                                                                 |
| fields      |      piezo_id       |                                                                                                                                                                                                                                             Nombre del campo que identifica de forma unívoca a cada piezómetro. Dicha información se extrae del paquete apuntado por el parámetro *piezometry_url*. |                                                                                                                                                                                          IDPIEZ |
| fields      |     piezo_date      |                                                                                                                                                                                                                                                              Nombre del campo que establece la fecha de toma de medida piezométrica. Es parte del paquete apuntado por el fichero *piezometry_url*. |                                                                                                                                                                                          FechaP |
| fields      |    piezo_lon_geo    |                                                                                                                                                       Nombre del campo que almacena la longitud de la ubicación de los piezómetros. El sistema de referencia usado viene dado por el parámetro *piezo_geographic*. La información se extrae del paquete apuntado por el parámetro *piezometry_url*. |                                                                                                                                                                                                 |
| fields      |    piezo_lat_geo    |                                                                                                                                                        Nombre del campo que almacena la latitud de la ubicación de los piezómetros. El sistema de referencia usado viene dado por el parámetro *piezo_geographic*. La información se extrae del paquete apuntado por el parámetro *piezometry_url*. |                                                                                                                                                                                                 |
| fields      |   piezo_lon_proj    |                                                                                                                                                       Nombre del campo que almacena la longitud de la ubicación de los piezómetros. El sistema de referencia usado viene dado por el parámetro *piezo_geographic*. La información se extrae del paquete apuntado por el parámetro *piezometry_url*. |                                                                                                                                                                                     CX89_HUSO30 |
| fields      |   piezo_lat_proj    |                                                                                                                                                        Nombre del campo que almacena la latitud de la ubicación de los piezómetros. El sistema de referencia usado viene dado por el parámetro *piezo_geographic*. La información se extrae del paquete apuntado por el parámetro *piezometry_url*. |                                                                                                                                                                                     CY89_HUSO30 |
| fields      |    piezo_measure    |                                                                                                                                                                                                                                                                                                                                          It's the field name that contains piezometric measurement. |                                                                                                                                                                                    Cota_NP_msnm |
|             |                     |                                                                                                                                                                                                                                                                                                                                                                                                     |                                                                                                                                                                                                 |
| crs         | location_geographic |                                                                                                                                                                                                                                                                               Sistema de coordenadas para las coordenadas geográficas del fichero de localizaciones de muestreo (*locations_file*). |                                                                                                                                                                                       EPSG:4326 |
| crs         | location_projected  |                                                                                                                                                                                                                                                                               Sistema de coordenadas para las coordenadas proyectadas del fichero de localizaciones de muestreo (*locations_file*). |                                                                                                                                                                                      EPSG:25830 |
| crs         |  precip_geographic  |                                                                                                                                                                                                                                     Sistema de coordenadas para las coordenadas geográficas del fichero de precipitaciones (dentro del paquete referenciado por el parámetro *precipitations_url*). |                                                                                                                                                                                       EPSG:4326 |
| crs         |  precip_projected   |                                                                                                                                                                                                                                     Sistema de coordenadas para las coordenadas proyectadas del fichero de precipitaciones (dentro del paquete referenciado por el parámetro *precipitations_url*). |                                                                                                                                                                                      EPSG:25830 |
| crs         |  piezo_geographic   |                                                                                                                                                                                                                                   Sistema de coordenadas para las coordenadas geográficas del fichero de medidas piezométricas (dentro del paquete referenciado por el parámetro *piezometry_url*). |                                                                                                                                                                                       EPSG:4326 |
| crs         |   piezo_projected   |                                                                                                                                                                                                                                   Sistema de coordenadas para las coordenadas proyectadas del fichero de medidas piezométricas (dentro del paquete referenciado por el parámetro *piezometry_url*). |                                                                                                                                                                                      EPSG:25830 |
| crs         |   final_projected   |                                                                                                                                                                                                                                                 Sistema de coordenadas global para los resultados. Todos los sistemas de referencia de entrada (proyectados o geográficos) se transformarán a éste. |                                                                                                                                                                                      EPSG:25830 |


## Fuentes de datos

1. **Localizaciones de muestreo**
   
    Fichero de texto de entrada, en formato CSV, con información sobre localizaciones de muestreo (*locations_file* en el fichero *config.ini*).

    Como ejemplo sencillo, se toma un caso de estudio del proyecto SARAI (https://webwp.igme.es/sarai). Cada fila define una localización de muestreo a través de las columnas que contienen:
   - longitud, 
   - latitud, 
   - identificador único.

    Este fichero tiene como características sintácticas:
   - carácter ';' como separador de campos.
   - carácter ',' como separador de decimales.

    Un fichero puede contener uno o varios pares de coordenadas (longitud, latitud) codificadas en diferentes sistemas de referencia, bien sean geográficos o proyectados. Para cada una de ellas, se especifica en el fichero *config.ini* así como el sistema de coordenadas empleado:
   - *location_geographic* para los pares de coordenadas (*location_lon_geo*, *location_lat_geo*)
   - *location_projected* para los pares de coordenadas (*location_lon_proj*, *location_lat_proj*)
  
    Se tratan de la misma forma las coordenadas y sistemas de referencia  dadas para las medidas de precipitación y piezometría. 

    En caso de que los ficheros de entrada no tengan campos para algunos de los conceptos parametrizados en el fichero *config.ini*, simplemente se dejan en blanco los valores asociados a dichos parámetros.

2. **Medidas de precipitación**

    Los datos de precipitación registrados para toda la Península y Baleares entre 1951 y 2020 han sido proporcionados por la Agencia Estatal de Meteorología (AEMET). Están referenciados por el parámetro de entrada *precipitations_url* en el fichero *config.ini*. Por defecto, apunta a un fichero comprimido (*\*.tar.gz*) localizado en [https://www.aemet.es/documentos/es/serviciosclimaticos/cambio_climat/datos_diarios/dato_observacional/rejilla_5km/v2/Serie_AEMET_v2_pcp_1951a2020_txt.tar.gz](https://www.aemet.es/documentos/es/serviciosclimaticos/cambio_climat/datos_diarios/dato_observacional/rejilla_5km/v2/Serie_AEMET_v2_pcp_1951a2020_txt.tar.gz). 

    El contenido del paquete comprimido consiste en:

   - un fichero llamado *README.txt*, que contiene información relevante sobre el contenido del paquete de ficheros,

   - *maestro_red_hr_SPAIN.txt*, que es un fichero de texto plano con las coordendas de los puntos de medida de precipitación y su identificador numérico,

   - *pcp_red_SPAIN_1951-2020.txt*, que es otro fichero de texto plano que contiene el histórico de medidas de precipitación interpolada en una malla con resolución espacial de 5x5 km, y resolución temporal de un día desde el 01-01-1951 hasta el 31-12-2020.

3. **Medidas de piezometría**. 
   
    Medidas recopiladas de la base de datos del Ministerio de Transición Ecológica y Reto Demográfico para toda la Península Ibérica y Baleares hasta 2020.

    La ubicación de esa información se define a través del parámetro  *piezometry_url*, en el fichero *config.ini*. Por defecto, apunta a un fichero comprimido (*\*.zip*) con la siguiente dirección web [https://www.miteco.gob.es/es/cartografia-y-sig/ide/descargas/basedatospiezometria_tcm30-533415.zip](https://www.miteco.gob.es/es/cartografia-y-sig/ide/descargas/basedatospiezometria_tcm30-533415.zip). Este fichero comprimido contiene una base de datos de Microsft Access (.mdb). Tiene dos tablas:

   - La primera contiene información de los piezómetros y su ubicación geográfica (en sistema de referencia proyectado).

   - La segunda incluye el histórico de medidas piezométricas tomadas en las ubicaciones referenciadas en la otra tabla.
  
    El Notebook, descarga, descomprime y lee la base de datos. Como salida, genera dos ficheros CSV (uno por cada tabla) para su posterior procesamiento. También, este formato normalizado hace que esta información sea accesible por cualquier otro usuario que no disponga de la suite de Microsoft Office.

## Criterios de asociación entre las localizaciones de muestreo y las medidas de precipitación y piezometría

Sólo las fuentes de datos de piezometría y precipitación cercanas a las localizaciones de muestreo son consideradas para completar la información del fichero original. La distancia máxima en metros se establece en el parámetro *radius*, en el fichero *config.ini*. 

### Precipitación

Para la asociación entre localizaciones de muestreo y puntos de medida de precipitación, se aplican dos criterios:

1. Asignación directa de la precipitación del punto más cercano con medidas a cada localización de muestreo.
2. Asignación de la media de la precipitación ponderada por el inverso de la distancia entre la localización de muestero y los puntos con medidas de precipitación dentro de un área circular centrada en el punto de muestreo y de radio pr el parámetro *radius* en metros.
   
### Piezometría

Sólo se asocia siguiendo el siguiente criterio:

1. Se selecciona la serie piezométrica más larga de entre las ubicaciones de los piezómetros más cercanos a cada localización de muestreo (buffer circular centrado en el punto de muestreo y radio máximo dado por el parámetro *radius*).

## Ficheros de salida

El Notebook los ubica en el directorio dado por el parámetro *output_dir*, en el fichero *config.ini*. Por defecto, se le ha asignado el valor *./results*, que representa un directorio llamado *results* ubicado en el mismo directorio que el fichero del Notebook. No es necesario crearlo de forma manual. El Notebook se encarga de hacerlo si no existe.

Los otros parámetros relacionados con ficheros de salida son:

- *out_interp_precip* (por defecto *historico_precipitaciones_ponderado_distancia.csv*). Almacena el histórico de precipitaciones calculadas según la media de precipitaciones ponderadas por el inverso de la distancia.

- *out_closest_prepic* (por defecto *historico_precipitaciones_punto_mas_cercano.csv*). Las medidas de precipitación histórica corresponden a la del punto con medida de precipitación más cercana a cada localización de interés.

- *out_longer_piezo* (por defecto *historico_piezometrias.csv*), que almacena las medidas con mayor duración temporal para cada punto de localización a distancia inferior a la dada por el parámetro *radius*. Si no hay piezómetros en ese radio, no se asigna medida a la localización de muestreo.

- Adicionalmente, también se guardan todas las imágenes y gráficas generadas por el Notebook.

Todos los ficheros de texto en formato CSV  que se generan relacionados con precipitación y piezometría, tienen la siguiente estructura: 

*Fecha,ID1, ID2, ID3,...,IDN*

donde los IDs se corresponden con los valores del campo *location_label* único que identifica cada una de las localizaciones de muestreo.


## Agradecimientos

Este trabajo es parte del proyecto SARAI del Ministerio de Ciencia e Innovación, con referencia PID2020-116540RB-C22 y financiado por MCIN/ AEI /10.13039/501100011033. Este trabajo ha sido desarrollado dentro del subproyecto liderado por el Instituto Geológico y Minero de España (CN IGME), como centro de investigación integrado en el Consejo Superior de Investigaciones Científicas (CSIC).

Enlace al proyecto: https://webwp.igme.es/sarai/index.php/en/home/ 

Nos gustaría agradecer

- AEMET (https://www.aemet.es/), por facilitar los datos de precipitación usados en este Notebook.
- MINECO (https://www.miteco.gob.es/) , por proporcionar la información sobre estaciones piezométricas y sus mediciones que han sido usadas en este trabajo.


![AEMET Logo](/sample_images/logo_aemet.jpg)

![MITECO Logo](/sample_images/miteco_logo.png)

## Contacto

Estas somos las personas que hemos llevado a cabo este trabajo:

- César Husillos Rodríguez (c.husillos@igme.es), 
- Carolina Guardiola Albert (c.guardiola@igme.es), 
- Héctor Aguilera Alonso (h.aguilera@igme.es),
- Pablo Ezquerro Martín (p.ezquerro@igme.es)
- Ángel Prieto Martín (a.prieto@igme.es). 
  
Pueden contactarnos vía correo electrónico o buscarnos en GitHub.

## Licencia

Este proyecto se ha desarrollado bajo la licencia GNU General Public License v3.0.


## Ejemplo de uso

Se mostrará a través de sucesivas capturas de pantalla que ilustrarán las fases de operación del Notebook.

### 1. Carga de localizaciones de muestreo

El fichero de texto que contiene esta información es un CSV que viene referenciado por el parámetro *locations_file* dentro de la sección *paths*. Tiene
- ';' como carácter separador de campos.
- ',' como carácter separador de decimales.
  
El código que carga esta información en el Notebook se muestra a continuación:


    # lectura el fichero de parámetros'config.ini'
    locations_file = config.get('paths', 'locations_file')

    # lectura ficheros de localizaciones de muestreo 
    df_loc = pd.read_csv(locations_file, sep=';', decimal=',')

    # obteniendo el valor del parámetro 'location_id' 
    id_loc = config.get('fields', 'location_id') 

    # estableciendo este campo como índice del DataFrame
    df_loc = df_loc.set_index(id_loc, drop=False)

    # mostrando información de las localizaciones de muestreo
    print(df_loc.info()) 


Leída la información, se muestra su ubcicación en un mapa.

![Localizaciones de muestreo](/sample_images/localizaciones_de_muestreo.jpg)

### 2. Descarga y procesado de la información sobre precipitación

El paso siguiente consiste en la descarga del paquete de datos sobre el histórico de precipitaciones, su filtrado a la zona de las localizaciones de muestreo y pintarlas en un mapa.

![Localizaciones de muestreo y puntos con información sobre la precipitación](/sample_images/nodos_precipitacion_En_area_de_muestreo.jpg)


Para la determinación de la precipitación en las ubicaciones de muestreo, hay dos algoritmos en consideración:

1. calcular la media ponderada por el inverso de la distancia para los puntos con precipitación dentro de un radio máximo de distancia (en metros). 
2. tomar las medidas del punto más cercano.
  
Si usamos el primer método (media ponderada por el inverso de la distancia), cada localización de muestreo tendrá un número variable de nodos de precipitación cercanos. El siguiente diagrama de barras muestra esa relación.

![Número de nodos de precipitación asociadas a localizaciones de muestreo](/sample_images/histograma_asociacion_nodos_precipitacion-puntos_muestreo.jpg)

Si consideramos el caso de asociación al punto de precipitación más cercano, el siguiente mapa muestra las ubicaciones de muestreo que se asocian a la precipitación medida en un punto de la malla de precipitaciones (la que viene dada por el ID = 1868).

![Puntos de muestreo asociados al nodo de precipitación etiquetado con ID=1868](/sample_images/localizaciones_mas_proximas_al_nodo_de_precipitacion_1868.jpg)

La siguente figura muestra todos los nodos de precipitación asociadas a las localizaciones de muestreo consideradas en este trabajo.

![Puntos de precipitación asociados a los puntos de muestreo Según el criterio de mínima distancia.](/sample_images/nodos_de_precipitacion_seleccionados.jpg)

Y la figura que sigue muestra el histograma de distancias mínimas entre localizaciones de muestreo y puntos donde se ha registrado la precipitación.

![histograma de distancias mínimas entre localizaciones de muestreo y puntos de precipitación](/sample_images/histograma_distancias_nodos_precipitacion-puntos_muestreo.jpg)

Como objetivo final, el Notebook genera dos ficheros en formato CSV. Uno para la asociación según el algoritmo de mínima distancia, y otro para el de media ponderada por el inverso de las distancias. Las columnas incluyen en ambos casos:

- fecha de medida de precipitación
- campos con el campo *location_label* (dado en el fichero *config.ini*) que identifican de forma unívoca la localización de muestreo.
  
### 3. Descarga y procesado de datos piezométricos

Se aplica un proceso similar al caso de la precipitación.

![Puntos de muestreo y ubicaciones de los piezómetros](/sample_images/piezometros_en_zona_de_muestreo.jpg)

A la hora de realizar la asociación entre puntos de medida piezométrica y localizaciones de muestreo, se establecen pares entre puntos
- cuya distancia entre ellos sean menor que la dada por el valor del parámetro *radius* (en el fichero *config.ini*) medida en metros.
- si hay varios puntos que cumplen la anterior condición de distancia, se selecciona aquel cuya serie temporal de medidas piezométricas sea la más larga.

La siguiente imagen muestra los piezómetros relacionados con las ubicaciones de muestreo.


![Localizaciones de muestreo y los piezómetros con los que se relacionan](/sample_images/piezometros_seleccionados.jpg)

El siguiente histograma muestra la distribución de distancias entre localizaciones de muestreo y las ubicaciones de piezómetros a los que se asocian.

![Distancia entre puntos de muesteo y ubicaciones ed piezómetros asociados](/sample_images/histograma_distancias_a_piezometros.jpg)

A continuación, este diagrama de barras muestra el número de localizaciones de muestreo asociadas a cada piezómetro. El número que aparece en el eje de abscisas es el identificador único del piezómetro.

![Número de asociaciones entre piezómetros y lugares de muestreo ](/sample_images/localizaciones_asociadas_a_piezometros.jpg)

Finalmente, la siguiente figura muestra sobre un mapa la distribución espacial de localizaciones de muestreo asociadas al más popular de los piezómetros.

![Sampling locations associated to a given piezometer](/sample_images/localizaciones_asociadas_piezometro_2015.jpg)

Como en el caso de la precipitación, el Notebook genera un fichero CSV con las medidas piezométricas asociadas a cada punto de muestreo. A diferencia de los ficheros de salida de precipitación, no todos los puntos de muestreo se representan en el fichero de salida de piezometría. La condición para su existencia es que haya un piezómetro a una distancia menor que la dada por *radius* en metros.


