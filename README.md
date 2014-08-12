# Importación Fibra Óptica

En este fichero encontraras las indicaciones necesarias para poder trabajar en este proyecto.

### Directorios:

 * bbdd_fibraoptica/varios/
 * bbdd_fibraoptica/varios/files_to_import
 * bbdd_fibraoptica/varios/sample_config_files


##### En bbdd_fibraoptica/varios se encuentran las tansformaciones:

* all_tables.ktr
* access_export_ALMACEN FO.ktr
* access_export_Asignaciones de fibras.ktr
* access_export_AveriasFO.ktr
* access_export_Consumos_de_materiales_de_FO.ktr
* access_export_Facturas de FO.ktr
* access_export_Peticiones_Datos.ktr
* access_export_Peticiones_TC.ktr
* access_export_Reparaciones.ktr


##### En bbdd_fibraoptica/varios/files_to_import se encuentran los ficheros .mdb (access):

* ALMACEN FO.mdb
* Asignaciones de fibras.mdb
* AveriasFO.mdb
* AveriasFO_Backup.mdb
* Consumos de materiales de FO.mdb
* Facturas de FO.mdb
* Peticiones_Datos.mdb
* Peticiones_TC.mdb
* Reparaciones.mdb

### Correspondencia entre transformaciones y ficheros mdb

* access_export_ALMACEN FO.ktr ======================> ALMACEN FO.mdb
* access_export_Asignaciones de fibras.ktr ==========> Asignaciones de fibras.mdb
* access_export_AveriasFO.ktr =======================> AveriasFO.mdb
* access_export_Consumos_de_materiales_de_FO.ktr ====> Consumos de materiales de FO.mdb
* access_export_Facturas de FO.ktr ==================> Facturas de FO.mdb
* access_export_Peticiones_Datos.ktr ================> Peticiones_Datos.mdb
* access_export_Peticiones_TC.ktr ===================> Peticiones_TC.mdb
* access_export_Reparaciones.ktr ====================> Reparaciones.mdb



##### En bbdd_fibraoptica/varios/sample_config_files se encuentran los ejemplos de ficheros de configuración:
* jdbc.properties
* kettle.properties

En pentaho, al poner/seleccionar una ruta para acceder a cualquiera de los archivos mdb, hay que usar rutas relativas, no rutas absolutas,de esta manera si la carpeta del data-integration cambia de lugar, o si se quieren ejecutar las transformaciones desde otro ordenador, no hará falta actualizar las rutas. Por ejempplo:
  En vez de:  /home/manager/projects/data-integration/bbdd_export/bbdd_access/ALMACEN FO.mdb
  Usar:       bbdd_access/ALMACEN FO.mdb

### Definir variables
En el fichero "~/.kettle/kettle.properties"
    O sea, hacer:
     1. cd $Home
     2. cd .kettle
     3. Abrir con un editor de texto el archivo "kettle.properties"
        * Definir las variables que se necesiten. Para este proyecto definir: ESQUEMA_BBDD_FIBRA = nombre_del_esquema
        * Donde nombre_del_esquema es el nombre del esquema que existe en la base de datos "oracle_pruebas".
        * Un caso concreto sería por ejemplo: ESQUEMA_BBDD_FIBRA = redmine_jesus
  * La definición de variables en este fichero, nos permitirá usarlas en Pentaho así: ${ESQUEMA_BBDD_FIBRA}
  * Se pueden usar estas variables en todos los campos donde aparezca un icono pequeño con forma rombo y con el signo dolar '$' dentro.
  * Se pueden definir variables para almacenar paths de directorios y archivos.
  * Para comprobar que las variables se han creado correctamente y pentaho las usa, ir a la transformación o trabajo correspondiente y teclear F2, a continuación se abrirá una ventana donde se muestran todas las variables que esta usando pentaho.
  * En este repositorio se ha añadido en la carpeta 'config_files' un ejemplo de fichero 'kettle.properties'.

### Añadir al fichero los datos de conexión:

En el directorio del data-integration (donde esta spoon.sh), ir al fichero "../simple-jndi/jdbc.properties" y añadir:

<b> bbdd_fibra/type=javax.sql.DataSource </b> <br>
<b> bbdd_fibra/driver=org.hsqldb.jdbcDriver </b> <br>
<b> bbdd_fibra/url=jdbc:oracle:thin:@172.16.10.77:1521/xe </b> <br>
<b> bbdd_fibra/user=system </b> <br>
<b> bbdd_fibra/password=Mobilife2014 </b> <br>

* En este repositorio se ha añadido en la carpeta 'config_files' un ejemplo de fichero 'jdbc.properties'.
