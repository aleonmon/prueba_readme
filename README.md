# Importación Fibra Óptica

### Configuración

En principio todas las transformaciones (ficheros .ktr) estan configurados con lo necesario, lo único que tiene que hacer alguien que va a trabajar por primera vez con este repositorio, es tener en cuenta los pasos a seguir.


#### Pasos a seguir

  1. En el directorio de pentaho (data-integration, donde esta spoon.sh), crear un acceso directo a la carpeta 'files_to_import' del repositorio.
  2. Sustituir el fichero "~/.kettle/kettle.properties" por un enlace simbólico al fichero "kettle.properties" de la carpeta 'config_files' del repositorio.

* Tener en cuenta:
   * Si el directorio donde se encuentran los archivos .ktr (transformacion) y .jtr (trabajo) está fuera del directorio de pentaho, entonces habrá que hacer un drag and drop (arrastra y suelta) hasta la ventana de pentaho, esto es debido a que pentaho no muestra los directorios que estan fuera del suyo.

## Notas

### Directorios:

##### En bbdd_fibraoptica/varios se encuentran las tansformaciones.

##### En bbdd_fibraoptica/varios/files_to_import se encuentran los ficheros .mdb (access):

##### En bbdd_fibraoptica/varios/config_files se encuentran los ejemplos de ficheros de configuración:


### Correspondencia entre transformaciones y ficheros mdb

* access_export_ALMACEN FO.ktr ======================> ALMACEN FO.mdb
* access_export_Asignaciones de fibras.ktr ==========> Asignaciones de fibras.mdb
* access_export_AveriasFO.ktr =======================> AveriasFO.mdb
* access_export_Consumos_de_materiales_de_FO.ktr ====> Consumos de materiales de FO.mdb
* access_export_Facturas de FO.ktr ==================> Facturas de FO.mdb
* access_export_Peticiones_Datos.ktr ================> Peticiones_Datos.mdb
* access_export_Peticiones_TC.ktr ===================> Peticiones_TC.mdb
* access_export_Reparaciones.ktr ====================> Reparaciones.mdb

* LA SIGUIENTE OPCIÓN PARA LA CONEXIÓN A LA BBDD SE HA DESCARTADO POR SER INESTABLE: 

Añadir al fichero los datos de conexión:

En el directorio de pentaho (data-integration, donde esta spoon.sh), ir al fichero "../simple-jndi/jdbc.properties" y añadir:

 bbdd_fibra/type=javax.sql.DataSource  <br>
 bbdd_fibra/driver=org.hsqldb.jdbcDriver  <br>
 bbdd_fibra/url=jdbc:oracle:thin:@172.16.10.77:1521/xe  <br>
 bbdd_fibra/user=USUARIO  <br>
 bbdd_fibra/password=CONTRASEÑA  <br>

* En este repositorio se ha añadido en la carpeta 'config_files' un ejemplo de fichero 'jdbc.properties'.


#### Definir variables, en el fichero "~/.kettle/kettle.properties"

     1. cd $Home
     2. cd .kettle
     3. Abrir con un editor de texto el archivo "kettle.properties"
        * Definir las variables que se necesiten. En los apartados correspondientes de este documento se indican que variables hay que definir.
        * Para este proyecto s epodría definir por ejemplo: ESQUEMA_BBDD_FIBRA = nombre_del_esquema. Donde nombre_del_esquema es el nombre del esquema que existe en la base de datos "oracle_pruebas".
  * La definición de variables en este fichero, nos permitirá usarlas en Pentaho así: ${ESQUEMA_BBDD_FIBRA}
  * Se pueden usar estas variables en todos los campos donde aparezca un icono pequeño con forma rombo y con el signo dolar '$' dentro.
  * Se pueden definir variables para almacenar paths de directorios y archivos.
  * Para comprobar que las variables se han creado correctamente y pentaho las usa, ir a la transformación o trabajo correspondiente y teclear F2, a continuación se abrirá una ventana donde se muestran todas las variables definidas que esta usando pentaho.
  * En este repositorio se ha añadido en la carpeta 'config_files' un ejemplo de fichero 'kettle.properties'.
  * Otra de las ventajas es que si queremos cambiar de esquema, hacemos ESQUEMA_BBDD_FIBRA = nuevo_nombre_del_esquema, y para crear las tablas en el nuevo esquema solo hay que darle click al botón con forma de hoja de pergamino y un play verde pequeño, que al poner el ratón encima indica "Generar el SQL necesario para ejecutar esta transformación", a continuación se abre una ventana, dar click a "Execute SQL" y si ha habido éxito cerrar ventana.


#### Definición de variables para los paths de los ficheros mdb
* En pentaho, al poner/seleccionar una ruta para acceder a cualquiera de los archivos mdb, hay que usar rutas relativas, no rutas absolutas,de esta manera si la carpeta del data-integration cambia de lugar, o si se quieren ejecutar las transformaciones desde otro ordenador, no hará falta actualizar las rutas. Por ejemplo:
  * En vez de:  /home/manager/projects/data-integration/bbdd_export/bbdd_access/ALMACEN FO.mdb
  * Usar:       bbdd_access/ALMACEN FO.mdb
* Para facilitar más esta cuestión mejor definir en el fichero de configuración "kettle.properties" las variables para los paths.
