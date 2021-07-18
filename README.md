# ejercicios_Archivos
ejercios y apuntes de archivos Python

NOMBRES DE ARCHIVOS:

Los diferentes sistemas operativos pueden tratar a los archivos de diferentes maneras. Por ejemplo, Windowas usa una convención de nomenclatura diferente a la adoptada en Unix/Linux

WINDOWS:

c:\directory\file

LINUX:

/directory/files


Los nombres de archivo de sistemas Unix/Linux distinguen entre mayúsculas y minúsculas. Los sistemas Windows almacenan mayúsculas y minúsculas en el nombre del archivo, pero no distinguen entre ellas.

Esto significa que estas dos cadenas:

EsteEsElNombreDelArchivo

y
esteeselnombredelarchivo

Hay que usar dos separadores diferentes para los nomrbres de directorio: \ en Windows y / en Unix/Linux


Supondamos que estás interesado en un archivo en particular ubicado en el directorio dir y con el nombre de archivo. 
Supongamos también que deseas asignar a una cadena el nombre del archivo.

En sistemas Linux se ve de la siguiente manera:

nombre="/dir/archivo"

En windows seá de la siguiente manera:

nomre="\\dir\\archivo"

Las entidades que conectan con los ficheros son: handles( un tipo de puntero inteligente) o streams(una especie de canal).

La operación de conectar un stream con un archivo es llamada abrir archivo, mientras que desconectar el enlace se denomina cerrar el archivo.

La primera operación realizada en el stream es siempre open (abrir) y la última es close(cerrar). 

La apertura del stream no solo está asociada con el archivo , sino que también se debe declarar la manera en que se procesará el stream. Esta declaración se llama un open mode (modo abierto).

Si la apertura es exitosa, el programa solo podrá realizar las operaciones que sean consistentes con el modo abiert declarado.

Hay dos operaciones básicas a realizar con el stream:

  .Lectura del stream: las porciones de los datos se recuperan del archivo y se colocan en un área de memoria administrada por el programa (por ejemplo, una variable).
  
  .Escritura del stream: las porciones de los datos de la memoria (por ejemplo, una variable) se transfieren al archivo.
  
Hay tres modos básicos utilizados para abrir un stream:
  
  .Modo lectura: un stream abierto en este modo permite solo operaciones de lectura. Intentar escribir en la transmisión provocará una excepción  UnsupportedOperation, la cual hereda el OSError y el ValieError y proviene del módulo io).
  .Modo Escritura: un stream abierto en este modo permite solo operacioes de escritura; intentar leer el stream provocará la excepción mencionad anteriormente.
  .Modo actualizar: un stream abierto en este modo permite tanto lectura como escritura.
  
  
