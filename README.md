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
  
  Un objeto de una clae adecuada es creado cuando abres el archivo y lo aniquilas al momento de cerrarlo.
  
  Nunca se utiliza el constructor para dar vida a estos objetos. La unica forma de obtenerlos es invocar la función llamada open().
  
  Si deseas deshacerte del objeto, invoca el método denominado close().
  
  Solo nos ocuparemos de los streams representados por los objetos BufferIOBase y TextIOBase.
  
  Los streams se diiden en tipo texto y binario.
  
  ABRIENDO LOS STREAMS: el abrir un stream se realiza mediante una función que se puede invocar de la siguiente manera:
  
  stream= open(file,mode= 'r',enconding=None)
  
  El nombre de la función (open) habla por sí mismo; si la apertura es exitosa, la función devuelve un objeto stream ; de lo contrario se genera una excepción (por ejemplo FileNotFoundError si el archivo que vas a leer no existe).
  
  El segundo parámetro (mode) especifica el modo de apertura utilizado para el stream; es una cadena llena de una secuencia de caracteresm y cada uno de ellos tiene su propio significado especial.
  
  El tercer parámetro (encoding) especifica el tipo de codificación (por ejemplo UTF-8 cuando se trabaja con archivos de texto).
  
  La apertura debe ser la primera operación realizada en el stream.
  
  
  
  ABRIENDO LOS STREAMS: MODOS
  
  Modo de apertura r:lectura
  
  El stream será abierto en modo lectura
  El archivo asociado con el stream debe existir y tiene que ser legible, de lo contrario la función open() lanzará una excepción.
  
  Modo de apetura w: escritura
  
   El stream será abierto en modo escritura
   El archivo asociado con el stream no necesita existir. Si no existe, se truncará a la longitud de 0 (se borra); si la creación no es posible la función open() lanzará una excepción.
   
   Modo de apertura a:adjuntar
   
   El stream será abierto en modo adjuntar
   El archivo asociado con el stream no necesita existir: si no existe, se creará; si existe el cabezal de grabación virtual se establecerá al final del archivo ( el contenido anterior del archivo permanece intacto).
   
   Modo de apertura r+:leer y actualizar
   
   El stream será abierto en modo leer y actualizar
   El archivo asociado con el stream debe existir y tiene que ser escribible, de lo contrario la función open() lanzará una excepción.
   Se permiten operaciones de lectura y escritura en el stream.
   
   Modo de apertura w+: escribir y actualizar
   
   El stream será abierto en modo escribir y actualizar
   El archivo asociado con el stream no necesita existir; si no existe, se creará.El contenido anterior del archivo permanece intacto.
   
   Se permiten operaciones de lectura y escritura en el stream.
   
   
   SELECCIONANDO MODO DE TEXTO Y MODO BINARIO:
   
   Si hay una tecla b al final de la cadena del modo significa que el stream se debe abrir en el modo binario.
   Si la cadena del modo termina con una letra t el stream es abierto en modo texto.
   
   Modo texto    Modo binario    Descripción
   
   rt               rb            lectura
   wt               wb            escritura
   at               ab            adjuntar
   r+t              r+b           leer y actualizar
   w+t              w+b           escribir y actualizar
   
   
   
   
   Imagina que queremos desarrollar un programa que lea el contenido del archivo de texto llamada: C:\Users\User\Desktop\file.txt
   
   try:
   
      stream=open ("C:\Users\User\Desktop\file.txt","rt")
      
      #aqui se procesa el archivo
      
      stream.close()
      
   except Exception as exc:
   
    print("No se puede abrir el archivo:", exc)
    
  Hemos abierto el bloque try-except ya que queremos manejar los errores de triempo de ejecución suavemente.
  Se emplea la función open() para intentar abrir el archivo especificado .
  El modo de apertura se define como texto para leer (como texto es la configuración predeterminada, podemos omitir la t en la cadena de modo).
  En caso de éxito obtenemos un objeto de la función open() y lo asignamos a la variable del stream.
  Si open() falla, manejando la excepción imprimiendo la información completa del error (esbueno saber qué sucedió exactamente).
  
  
STREAMS PRE-ABIERTOS:

Dijimos anteriormente que cualquier operación del stream debe estar precedida por la invocación de la función open(). Hay tres excepciones bien definidas a esta regla.

Cuando comienza nuestro programa, los tres streams ya están abiertos y no requieren ninguna preparación adicional. Además, tu programa puede usar estos streams explícitamente si tienes cuidado de importar el módulo sys:

import sys

Porque ahí es donde se coloca la declaración de estos streams.

Los nombres de los streams son: sys.stdin, sys.stdout y sys.stderr.

Vamos a analizarlos:

sys.stdin
stdin (significa entrada estándar).
El stream stdin normalmente se asocia con el teclado, se abre previamente para la lectura y se considera como la fuente de datos principal para los programas en ejecución.
La función bien conocida input() lee datos de stdin por default.

sys.stdout
stdout (significa salida estándar).
El stream stdout normalmente está asociado con la pantalla, preabierta para escritura, considerada como el objetivo principal para la salida de datos por el programa en ejecución.
La función bien conocida print() envía los datos al stream stdout.

sys.stderr
stderr (significa salida de error estándar).
El stream stderr normalmente está asociado con la pantalla, preabierta para escribir, considerada como el lugar principal donde el programa en ejecución debe enviar información sobre los errores encontrados durante su trabajo.
No hemos presentado ningún método para enviar datos a este stream (lo haremos pronto, lo prometemos).
La separación de stdout (resultados útiles producidos por el programa) de stderr (mensajes de error, indudablemente útiles pero no proporcionan resultados) ofrece la posibilidad de redirigir estos dos tipos de información a los diferentes objetivos. Una discusión más extensa sobre este tema está más allá del alcance de nuestro curso. El manual del sistema operativo proporcionará más información sobre estos temas.


Cerrando streams
La última operación realizada en un stream (esto no incluye a los streams stdin, stdout, y stderr pues no lo requieren) debe ser cerrarlo.

Esa acción se realiza mediante un método invocado desde dentro del objeto del stream: stream.close().

El nombre de la función es fácil de entender close(), es decir cerrar.
La función no espera argumentos; el stream no necesita estar abierto.
La función no devuelve nada pero lanza una excepción IOError en caso de un error.
La mayoría de los desarrolladores creen que la función close() siempre tiene éxito y, por lo tanto, no hay necesidad de verificar si ha realizado su tarea correctamente.

Esta creencia está solo parcialmente justificada. Si el stream se abrió para escribir y luego se realizó una serie de operaciones de escritura, puede ocurrir que los datos enviados al stream aún no se hayan transferido al dispositivo físico (debido a los mecanismos de cache o buffer). Dado que el cierre del stream obliga a los búferes a descargarse, es posible que dichas descargas fallen y, por lo tanto, close() falle también.
Ya hemos mencionado fallas causadas por funciones que operan con los streams, pero no mencionamos nada sobre cómo podemos identificar exactamente la causa de la falla.

La posibilidad de hacer un diagnóstico existe y es proporcionada por uno de los componentes de excepción de los streams.

Diagnosticando problemas con los streams
El objeto IOError está equipado con una propiedad llamada errno (el nombre viene de la frase error number, número de error) y puedes accederla de la siguiente manera:


try:

    # operaciones con streams
    
except IOError as exc:

    print(exc.errno)


El valor del atributo errno se puede comparar con una de las constantes simbólicas predefinidas en módulo errno.
  
  
 Echemos un vistazo a algunas constantes seleccionadas útiles para detectar errores de flujo:

errno.EACCES → Permiso denegado

El error se produce cuando intentas, por ejemplo, abrir un archivo con atributos de solo lectura para abrirlo.


errno.EBADF → Número de archivo incorrecto

El error se produce cuando intentas, por ejemplo, operar un stream sin abrirlo.

errno.EEXIST → Archivo existente

El error se produce cuando intentas, por ejemplo, cambiar el nombre de un archivo con su nombre anterior.


errno.EFBIG → Archivo demasiado grande

El error ocurre cuando intentas crear un archivo que es más grande que el máximo permitido por el sistema operativo.


errno.EISDIR → Es un directorio

El error se produce cuando intentas tratar un nombre de directorio como el nombre de un archivo ordinario.


errno.EMFILE → Demasiados archivos abiertos

El error se produce cuando intentas abrir simultáneamente más streams de los aceptables para el sistema operativo.


errno.ENOENT → El archivo o directorio no existe

El error se produce cuando intentas acceder a un archivo o directorio inexistente.


errno.ENOSPC → no queda espacio en el dispositivo

El error ocurre cuando no hay espacio libre en el dispositivo.


La lista completa es mucho más larga (incluye también algunos códigos de error no relacionados con el procesamiento del stream).


Diagnosticando problemas con los streams: continuación
Si eres un programador muy cuidadoso, puedes sentir la necesidad de usar una secuencia de sentencias similar a la que se presenta a continuación:

import errno

try:

    s = open("c:/users/user/Desktop/file.txt", "rt")
    
    # el procesamiento va aquí
    
    s.close()
    
except Exception as exc:

    if exc.errno == errno.ENOENT:
    
        print("El archivo no existe.")
        
    elif exc.errno == errno.EMFILE:
    
        print("Has abierto demasiados archivos.")
        
    else:
    
        printf("El número de error es:", exc.errno)
        

Afortunadamente, existe una función que puede simplificar el código de manejo de errores. Su nombre es strerror(), y proviene del módulo os y espera solo un argumento: un número de error.

Su función es simple: proporciona un número de error y una cadena que describe el significado del error.

Nota: Si pasas un código de error inexistente (un número que no está vinculado a ningún error real), la función lanzará una excepción ValueError.

Ahora podemos simplificar nuestro código de la siguiente manera:

from os import strerror

try:

    s = open("c:/users/user/Desktop/file.txt", "rt")
    
    # el procesamiento va aquí
    
    s.close()
    
except Exception as exc:

    print("El archivo no se pudo abrir:", strerror(exc.errno));
    

Bueno. Ahora es el momento de tratar con archivos de texto y familiarizarse con algunas técnicas básicas que puedes utilizar para procesarlos.

ejemplos:

stream = open("tzop.txt", "rt", encoding = "utf-8") # se abre el archivo tzop.txt en modo lectura, devolviéndolo como un objeto de archivo

print(stream.read()) # se imprime el contenido del archivo

Procesamiento de archivos de texto: continuación
La lectura del contenido de un archivo de texto se puede realizar utilizando diferentes métodos; ninguno de ellos es mejor o peor que otro. Depende de ti cuál de ellos prefieres y te gusta.

Algunos de ellos serán a veces más prácticos y otros más problemáticos. Se flexible. No tengas miedo de cambiar tus preferencias.

El más básico de estos métodos es el que ofrece la función read(), la cual pudiste ver en acción en la lección anterior.

Si se aplica a un archivo de texto, la función es capaz de:

Leer un número determinado de caracteres (incluso solo uno) del archivo y devolverlos como una cadena.
Leer todo el contenido del archivo y devolverlo como una cadena.
Si no hay nada más que leer (el cabezal de lectura virtual llega al final del archivo), la función devuelve una cadena vacía.

Comenzaremos con la variante más simple y usaremos un archivo llamado text.txt. El archivo contiene lo siguiente:

Lo hermoso es mejor que lo feo.
Explícito es mejor que implícito.
Simple es mejor que complejo.
Complejo es mejor que complicado.

Ahora observa el código en el editor y analicémoslo.

La rutina es bastante simple:

Se usa el mecanismo try-except y se abre el archivo con el nombre (text.txt en este caso).
Intenta leer el primer caracter del archivo (ch = s.read(1)).
Si tienes éxito (esto se demuestra por el resultado positivo de la condición while), se muestra el caracter (nota el argumento end=,¡es importante! ¡No querrás saltar a una nueva línea después de cada caracter!).
Se actualiza el contador (cnt).
Intenta leer el siguiente carácter y el proceso se repite.


Otro ejemplo:

from os import strerror

try:

    cnt = 0
    
    s = open('text.txt', "rt")
    
    ch = s.read(1)
    
    while ch != '':
    
        print(ch, end='')
        
        cnt += 1
        
        ch = s.read(1)
        
    s.close()
    
    print("\n\nCaracteres en el archivo: ", cnt)
    
except IOError as e:

    print("Se produjo un error de E/S: ", strerr(e.errno))
    
    
    
 Procesamiento de archivos de texto: continuación
Si estás absolutamente seguro de que la longitud del archivo es segura y puedes leer todo el archivo en la memoria de una vez, puedes hacerlo: la función read(), invocada sin ningún argumento o con un argumento que se evalúa a None, hará el trabajo por ti.

Recuerda - el leer un archivo muy grande (en terabytes) usando este método puede dañar tu sistema operativo.

No esperes milagros: la memoria de la computadora no se puede extender.

Observa el código en el editor. ¿Que piensas de el?

Vamos a analizarlo:

Abre el archivo, como anteriormente se hizo.
Lee el contenido mediante una invocación de la función read().
Despues, se procesa el texto, iterando con un bucle for su contenido, y se actualiza el valor del contador en cada vuelta del bucle.
El resultado será exactamente el mismo que en el ejemplo anterior.


 
 Otro ejemplo:
 
 from os import strerror

try:

    cnt = 0
    
    s = open('text.txt', "rt")
    
    content = s.read()
    
    for ch in content:
    
        print(ch, end='')
        
        cnt += 1
        
        ch = s.read(1)
        
    s.close()
    
    print("\n\nCaracteres en el archivo: ", cnt)
    
except IOError as e:

    print("Se produjo un error de E/S: ", strerr(e.errno))


Procesando archivos de texto: readline()
Si deseas manejar el contenido del archivo como un conjunto de líneas, no como un montón de caracteres, el método readline() te ayudará con eso.

El método intenta leer una línea completa de texto del archivo, y la devuelve como una cadena en caso de éxito. De lo contrario, devuelve una cadena vacía.

Esto abre nuevas oportunidades: ahora también puedes contar líneas fácilmente, no solo caracteres.

Hagámos uso de ello. Observa el código en el editor.

Como puedes ver, la idea general es exactamente la misma que en los dos ejemplos anteriores.


from os import strerror

try:

    ccnt = lcnt = 0
    
    s = open('text.txt', 'rt')
    
    line = s.readline()
    
    while line != '':
    
        lcnt += 1
        
        for ch in line:
        
            print(ch, end='')
            
            ccnt += 1
            
        line = s.readline()
        
    s.close()
    
    print("\n\nCaracteres en el archivo: ", ccnt)
    
    print("Lineas en el archivo:     ", lcnt)
    
except IOError as e:

    print("Se produjo un error de E/S: ", strerr(e.errno))
   
   
   Procesando archivos de texto: readlines()
Otro método, que maneja el archivo de texto como un conjunto de líneas, no como caracteres, es readlines().

Cuando el método readlines(), se invoca sin argumentos, intenta leer todo el contenido del archivo y devuelve una lista de cadenas, un elemento por línea del archivo.

Si no estás seguro de si el tamaño del archivo es lo suficientemente pequeño y no deseas probar el sistema operativo, puedes convencer al método readlines() de leer no más de un número especificado de bytes a la vez (el valor de retorno sigue siendo el mismo, es una lista de una cadena).

Siéntete libre de experimentar con este código de ejemplo para entender cómo funciona el método readlines().

El tamaño máximo del búfer de entrada aceptado se pasa al método como argumento.

Puedes esperar que readlines() procese el contenido del archivo de manera más efectiva que readline(), ya que puede ser invocado menos veces.

Nota: cuando no hay nada que leer del archivo, el método devuelve una lista vacía. Úsalo para detectar el final del archivo.

Puedes esperar que al aumentar el tamaño del búfer mejore el rendimiento de entrada, pero no hay una regla de oro para ello: intenta encontrar los valores óptimos por ti mismo.


Observa el código en el editor. Lo hemos modificado para mostrarte cómo usar readlines().

Hemos decidido usar un búfer de 15 bytes de longitud. No pienses que es una recomendación.

Hemos utilizado ese valor para evitar la situación en la que la primera invocación de readlines() consuma todo el archivo.

Queremos que el método se vea obligado a trabajar más duro y que demuestre sus capacidades.

Existen dos bucles anidados en el código: el exterior emplea el resultado de readlines() para iterar a través de él, mientras que el interno imprime las líneas carácter por carácter.



 
 Sandbox
Code
from os import strerror

try:
ccnt = lcnt = 0
s = open('text.txt', 'rt')
lines = s.readlines(20)
while len(lines) != 0:
for line in lines:
lcnt += 1
for ch in line:
print(ch, end='')
ccnt += 1
lines = s.readlines(10)
s.close()
print("\n\nCaracteres en el archivo: ", ccnt)
print("Lineas en el archivo: ", lcnt)
except IOError as e:
print("Se produjo un error de E/S: ", strerr(e.errno))
from os import strerror


Console 

from os import strerror

try:

    ccnt = lcnt = 0
    
    s = open('text.txt', 'rt')
    
    lines = s.readlines(20)
    
    while len(lines) != 0:
    
        for line in lines:
        
            lcnt += 1
            
            for ch in line:
            
                print(ch, end='')
                
                ccnt += 1
                
        lines = s.readlines(10)
        
    s.close()
    
    print("\n\nCaracteres en el archivo: ", ccnt)
    
    print("Lineas en el archivo:     ", lcnt)
    
except IOError as e:

    print("Se produjo un error de E/S: ", strerr(e.errno))
    
  
  Procesando archivos de texto: continuación
El último ejemplo que queremos presentar muestra un rasgo muy interesante del objeto devuelto por la función open() en modo de texto.

Creemos que puede sorprenderte - el objeto es una instancia de la clase iterable.

¿Extraño? De ningúna manera. ¿Usable? Si, por supuesto.

El protocolo de iteración definido para el objeto del archivo es muy simple: su método __next__ solo devuelve la siguiente línea leída del archivo.

Además, puedes esperar que el objeto invoque automáticamente a close() cuando cualquiera de las lecturas del archivo lleguen al final del archivo.

Mira el editor y ve cuán simple y claro se ha vuelto el código.


from os import strerror

try:

	ccnt = lcnt = 0
  
	for line in open('text.txt', 'rt'):
  
		lcnt += 1
    
		for ch in line:
    
			print(ch, end='')
      
			ccnt += 1
      
	print("\n\nCaracteres en el archivo: ", ccnt)
  
	print("Lineas en el archivo:     ", lcnt)
  
except IOError as e:

	print("Se produjo un error de E/S: ", strerr(e.errno))
  
  

LIST OF CONTENTS
Module 5 
BACK
MODULE 5
5.1.1 Fundamentos de Python: Parte 2 
BACK
5.1.1 FUNDAMENTOS DE PYTHON: PARTE 2
5.1.1.1 Fundamentos de Python: Parte 2
5.1.1.2 Fundamentos de Python: M&oacute;dulo 5
5.1.1.3 M&oacute;dulos
5.1.1.4 Empleando M&oacute;dulos
5.1.1.5 Empleando M&oacute;dulos
5.1.1.6 Empleando M&oacute;dulos
5.1.1.7 Importando un M&oacute;dulo | math
5.1.1.8 Importando un M&oacute;dulo | math
5.1.1.9 Importando un M&oacute;dulo | math
5.1.1.10 Importando un M&oacute;dulo | math
5.1.1.11 Importando un M&oacute;dulo | * y as
5.1.1.12 Importando un M&oacute;dulo | aliasing
5.1.2.1 M&oacute;dulos &Uacute;tiles
5.1.2.2 M&oacute;dulos &Uacute;tiles | math
5.1.2.3 M&oacute;dulos &Uacute;tiles | math
5.1.2.4 M&oacute;dulos &Uacute;tiles | math
5.1.2.5 M&oacute;dulos &uacute;tiles | aleatorio
5.1.2.6 M&oacute;dulos &Uacute;tiles | random
5.1.2.7 M&oacute;dulos &Uacute;tiles | random
5.1.2.8 M&oacute;dulos &Uacute;tiles | random
5.1.2.9 M&oacute;dulos &Uacute;tiles | random
5.1.2.10 M&oacute;dulos &Uacute;tiles | platform
5.1.2.11 M&oacute;dulos &Uacute;tiles | platform
5.1.2.12 M&oacute;dulos &Uacute;tiles | platform
5.1.2.13 M&oacute;dulos &Uacute;tiles | platform
5.1.2.14 M&oacute;dulos &Uacute;tiles | platform
5.1.2.15 M&oacute;dulos &Uacute;tiles | platform
5.1.2.16 M&oacute;dulos &Uacute;tiles
5.1.3.1 M&oacute;dulos y Paquetes
5.1.3.2 M&oacute;dulos y Paquetes
5.1.3.3 M&oacute;dulos y Paquetes
5.1.3.4 M&oacute;dulos y Paquetes
5.1.3.5 M&oacute;dulos y Paquetes
5.1.3.6 M&oacute;dulos y Paquetes
5.1.3.7 M&oacute;dulos y Paquetes
5.1.3.8 M&oacute;dulos y Paquetes
5.1.3.9 M&oacute;dulos y Paquetes
5.1.3.10 M&oacute;dulos y Paquetes
5.1.4.1 Errores: el pan diario del programador
5.1.4.2 Errores: el pan diario del programador
5.1.4.3 Errores: el pan diario del programador
5.1.4.4 Errores: el pan diario del programador
5.1.4.5 Errores: el pan diario del programador
5.1.4.6 Errores: el pan diario del programador | try-except
5.1.4.7 Errores: el pan diario del programador | try-except
5.1.4.8 Errores: el pan diario del programador | try-except
5.1.4.9 Errores: el pan diario del programador | try-except
5.1.4.10 Errores: el pan diario del programador | try-except
5.1.4.11 Errores: el pan diario del programador | try-except
5.1.5.1 La anatom&iacute;a de las excepciones
5.1.5.2 La anatom&iacute;a de las excepciones
5.1.5.3 La anatom&iacute;a de las excepciones
5.1.5.4 La anatom&iacute;a de las excepciones
5.1.5.5 La anatom&iacute;a de las excepciones | raise
5.1.5.6 La anatom&iacute;a de las excepciones | raise
5.1.5.7 La anatom&iacute;a de las excepciones | assert
5.1.6.1 Excepciones &uacute;tiles
5.1.6.2 Excepciones &uacute;tiles
5.1.6.3 Excepciones &uacute;tiles
5.1.6.4 Leer ints de forma segura Lab
5.1.7.1 Caracteres y Cadenas
5.1.7.2 Caracteres y Cadenas
5.1.7.3 Caracteres y Cadenas
5.1.8.1 La naturaleza de las cadenas en Python
5.1.8.2 La naturaleza de las cadenas en Python
5.1.8.3 La naturaleza de las cadenas en Python
5.1.8.4 La naturaleza de las cadenas en Python
5.1.8.5 La naturaleza de las cadenas en Python
5.1.8.6 La naturaleza de las cadenas en Python
5.1.8.7 La naturaleza de las cadenas en Python
5.1.8.8 La naturaleza de las cadenas en Python
5.1.8.9 La naturaleza de las cadenas en Python
5.1.8.10 La naturaleza de las cadenas en Python
5.1.8.11 La naturaleza de las cadenas en Python
5.1.8.12 La naturaleza de las cadenas en Python
5.1.8.13 La naturaleza de las cadenas en Python
5.1.8.14 La naturaleza de las cadenas en Python
5.1.9.1 M&eacute;todos de cadenas
5.1.9.2 M&eacute;todos de cadenas
5.1.9.3 M&eacute;todos de cadenas
5.1.9.4 M&eacute;todos de cadenas
5.1.9.5 M&eacute;todos de cadenas
5.1.9.6 M&eacute;todos de cadenas
5.1.9.7 M&eacute;todos de cadenas
5.1.9.8 M&eacute;todos de cadenas
5.1.9.9 M&eacute;todos de cadenas
5.1.9.10 M&eacute;todos de cadenas
5.1.9.11 M&eacute;todos de cadenas
5.1.9.12 M&eacute;todos de cadenas
5.1.9.13 M&eacute;todos de cadenas
5.1.9.14 M&eacute;todos de cadenas
5.1.9.15 M&eacute;todos de cadenas
5.1.9.16 M&eacute;todos de cadenas
5.1.9.18 Tu propio split Lab
5.1.10.1 Cadenas en acci&oacute;n
5.1.10.2 Cadenas en acci&oacute;n
5.1.10.3 Cadenas en acci&oacute;n
5.1.10.4 Cadenas en acci&oacute;n
5.1.10.6 LABORATORIO: Un Display LED Lab
5.1.11.1 Cuatro simples programas
5.1.11.2 Cuatro simples programas
5.1.11.3 Cuatro simples programas
5.1.11.4 Cuatro simples programas
5.1.11.6 LABORATORIO: Mejorando el cifrado C&eacute;sar Lab
5.1.11.7 LABORATORIO: Pal&iacute;ndromos Lab
5.1.11.8 LABORATORIO: Anagramas Lab
5.1.11.9 LABORATORIO: El D&iacute;gito de la Vida Lab
5.1.11.10 LABORATIORIO: &iexcl;Encuentra una palabra! Lab
5.1.11.11 LABORATORIO: Sudoku Lab
5.2.1 Module 5 Quiz Quiz 
BACK
5.2.1 MODULE 5 QUIZ
5.2.1.1 Module 5 Quiz Quiz
5.3.1 Module 5 Test Quiz 
BACK
5.3.1 MODULE 5 TEST
5.3.1.1 Module 5 Test Quiz
Module 6 Now 
BACK
MODULE 6
6.1.1 Fundamentos de Python: M&oacute;dulo 6 
BACK
6.1.1 FUNDAMENTOS DE PYTHON: M&OACUTE;DULO 6
6.1.1.1 Fundamentos de Python: M&oacute;dulo 6
6.1.1.2 Los fundamentos de la POO
6.1.1.3 Los fundamentos de la POO
6.1.1.4 Los fundamentos de la POO
6.1.1.5 Los fundamentos de la POO
6.1.1.6 Los fundamentos de la POO
6.1.1.7 Los fundamentos de la POO
6.1.1.8 Los fundamentos de la POO
6.1.2.1 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.2 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.3 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.4 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.5 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.6 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.7 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.8 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.9 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.10 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.11 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.12 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.3.1 Propiedades de la POO
6.1.3.2 Propiedades de la POO
6.1.3.3 Propiedades de la POO
6.1.3.4 Propiedades de la POO
6.1.3.5 Propiedades de la POO
6.1.3.6 Propiedades de la POO
6.1.3.7 Propiedades de la POO
6.1.3.8 Propiedades de la POO
6.1.4.1 POO: M&eacute;todos
6.1.4.2 POO: M&eacute;todos
6.1.4.3 POO: M&eacute;todos
6.1.4.4 POO: M&eacute;todos
6.1.4.5 POO: M&eacute;todos
6.1.4.6 POO: M&eacute;todos
6.1.4.7 POO: M&eacute;todos
6.1.4.8 POO: M&eacute;todos
6.1.4.9 POO: M&eacute;todos
6.1.4.10 POO: M&eacute;todos
6.1.5.1 Fundamentos de POO: Herencia
6.1.5.2 Fundamentos de POO: Herencia
6.1.5.3 Fundamentos de POO: Herencia
6.1.5.4 Fundamentos de POO: Herencia
6.1.5.5 Fundamentos de POO: Herencia
6.1.5.6 Fundamentos de POO: Herencia
6.1.5.7 Fundamentos de POO: Herencia
6.1.5.8 Fundamentos de POO: Herencia
6.1.5.9 Fundamentos de POO: Herencia
6.1.5.10 Fundamentos de POO: Herencia
6.1.5.11 Fundamentos de POO: Herencia
6.1.5.12 Fundamentos de POO: Herencia
6.1.5.13 Fundamentos de POO: Herencia
6.1.5.14 Fundamentos de POO: Herencia
6.1.5.15 Fundamentos de POO: Herencia
6.1.5.16 Fundamentos de POO: Herencia
6.1.5.17 Fundamentos de POO: Herencia
6.1.5.18 Fundamentos de POO: Herencia
6.1.5.19 Fundamentos de POO: Herencia
6.1.6.1 Excepciones una vez m&aacute;s
6.1.6.2 Excepciones una vez m&aacute;s
6.1.6.3 Excepciones una vez m&aacute;s
6.1.6.4 Excepciones una vez m&aacute;s
6.1.6.5 Excepciones una vez m&aacute;s
6.1.6.6 Excepciones una vez m&aacute;s
6.1.6.7 Excepciones una vez m&aacute;s
6.1.6.8 Excepciones una vez m&aacute;s
6.1.7.1 Generadores y cierres
6.1.7.2 Generadores y cierres
6.1.7.3 Generadores y cierres
6.1.7.4 Generadores y cierres
6.1.7.5 Generadores y cierres
6.1.7.6 Generadores y cierres
6.1.7.7 Generadores y cierres
6.1.7.8 Generadores y cierres
6.1.7.9 Generadores y cierres
6.1.7.10 Generadores y cierres
6.1.7.11 Generadores y cierres
6.1.7.12 Generadores y cierres
6.1.7.13 Generadores y cierres
6.1.7.14 Generadores y cierres
6.1.8.1 Procesando archivos
6.1.8.2 Procesando archivos
6.1.8.3 Procesando archivos
6.1.8.4 Procesando archivos
6.1.8.5 Procesando archivos
6.1.8.6 Procesando archivos
6.1.8.7 Procesando archivos
6.1.8.8 Procesando archivos
6.1.8.9 Procesando archivos
6.1.8.10 Procesando archivos
6.1.8.11 Procesando archivos
6.1.9.1 Trabajando con archivos reales
6.1.9.2 Trabajando con archivos reales
6.1.9.3 Trabajando con archivos reales
6.1.9.4 Trabajando con archivos reales
6.1.9.5 Trabajando con archivos reales
6.1.9.6 Trabajando con archivos reales
6.1.9.7 Trabajando con archivos reales Now
6.1.9.8 Trabajando con archivos reales
6.1.9.9 Trabajando con archivos reales
6.1.9.10 Trabajando con archivos reales
6.1.9.11 Trabajando con archivos reales
6.1.9.12 Trabajando con archivos reales
6.1.9.13 Trabajando con archivos reales
6.1.9.14 Trabajando con archivos reales
6.1.9.15 LABORATORIO: Histograma de frecuencia de caracteres Lab
6.1.9.16 LABORATORIO: Histograma de frecuencia de caracteres ordenado Lab
6.1.9.17 LABORATORIO: Evaluando los resultados de los estudiantes Lab
6.2.1 Module 6 Quiz Quiz 
BACK
6.2.1 MODULE 6 QUIZ
6.2.1.1 Module 6 Quiz Quiz
6.3.1 Module 6 Test Quiz 
BACK
6.3.1 MODULE 6 TEST
6.3.1.1 Module 6 Test Quiz
6.6.1 Fundamentos de Programaci&oacute;n en Python - PCAP 
BACK
6.6.1 FUNDAMENTOS DE PROGRAMACI&OACUTE;N EN PYTHON - PCAP
Fundamentos de Programaci&oacute;n en Python - PCAP
Manejando archivos de texto: write()
Escribir archivos de texto parece ser más simple, ya que hay un método que puede usarse para realizar dicha tarea.

El método se llama write() y espera solo un argumento: una cadena que se transferirá a un archivo abierto (no lo olvides), el modo de apertura debe reflejar la forma en que se transfieren los datos - escribir en un archivo abierto en modo de lectura no tendrá éxito).

No se agrega carácter de nueva línea al argumento de write(), por lo que debes agregarlo tu mismo si deseas que el archivo se complete con varias líneas.

El ejemplo en el editor muestra un código muy simple que crea un archivo llamado newtext.txt (nota: el modo de apertura w asegura que el archivo se creará desde cero, incluso si existe y contiene datos) y luego pone diez líneas en él.

La cadena que se grabará consta de la palabra línea, seguida del número de línea. Hemos decidido escribir el contenido de la cadena carácter por carácter (esto lo hace el bucle interno for) pero no estás obligado a hacerlo de esta manera.

Solo queríamos mostrarte que write() puede operar con caracteres individuales.

El código crea un archivo con el siguiente texto:

línea #1
línea #2
línea #3
línea #4
línea #5
línea #6
línea #7
línea #8
línea #9
línea #10

¿Puedes imprimir el contenido del archivo en la consola?

Te alentamos a que pruebes el comportamiento del método write() localmente en tu máquina.

from os import strerror

try:

	fo = open('newtext.txt', 'wt') #un nuevo archivo (newtext.txt) es creado
  
	for i in range(10):
  
		s = "línea #" + str(i+1) + "\n"
    
		for ch in s:
    
			fo.write(ch)
      
	fo.close()
  
except IOError as e:

	print("Se produjo un error de E/S: ", strerr(e.errno))
  
  
  Manejando archivos de texto: continuación
Mira el ejemplo en el editor. Hemos modificado el código anterior para escribir líneas enteras en el archivo de texto.

El contenido del archivo recién creado es el mismo.

Nota: puedes usar el mismo método para escribir en el stream stderr, pero no intentes abrirlo, ya que siempre está abierto implícitamente.

Por ejemplo, si deseas enviar un mensaje de tipo cadena a stderr para distinguirlo de la salida normal del programa, puede verse así:

import sys
sys.stderr.write("Mensaje de Error")


from os import strerror

try:

	fo = open('newtext.txt', 'wt')
  
	for i in range(10):
  
		fo.write("line #" + str(i+1) + "\n")
    
	fo.close()
  
except IOError as e:

	print("Se produjo un error de E/S: ", strerr(e.errno))
  
  
  ¿Qué es un bytearray?
Antes de comenzar a hablar sobre archivos binarios, tenemos que informarte sobre una de las clases especializadas que Python usa para almacenar datos amorfos.

Los datos amorfos son datos que no tienen forma específica - son solo una serie de bytes.

Esto no significa que estos bytes no puedan tener su propio significado o que no puedan representar ningún objeto útil, por ejemplo, gráficos de mapa de bits.

Los datos amorfos no pueden almacenarse utilizando ninguno de los medios presentados anteriormente: no son cadenas ni listas.

Debe haber un contenedor especial capaz de manejar dichos datos.




Python tiene más de un contenedor, uno de ellos es una clase especializada llamada bytearray - como su nombre indica, es un arreglo que contiene bytes (amorfos).

Si deseas tener dicho contenedor, por ejemplo, para leer una imagen de mapa de bits y procesarla de alguna manera, debes crearlo explícitamente, utilizando uno de los constructores disponibles.

Observa:

data = bytearray(100)

Tal invocación crea un objeto bytearray capaz de almacenar diez bytes.

Nota: dicho constructor llena todo el arreglo con ceros.


Bytearrays: continuación
Bytearrays se asemejan a listas en muchos aspectos. Por ejemplo, son mutables, son suceptibles a la función len(), y puedes acceder a cualquiera de sus elementos usando indexación convencional.

Existe una limitación importante - no debes establecer ningún elemento del arreglo de bytes con un valor que no sea un entero (violar esta regla causará una excepción TypeError) y tampoco está permitido asignar un valor fuera del rango de 0 a 255 (a menos que quieras provocar una excepción ValueError).

Puedes tratar cualquier elemento del arreglo de bytes como un valor entero - al igual que en el ejemplo en el editor.

Nota: hemos utilizado dos métodos para iterar el arreglo de bytes, y hemos utilizado la función hex() para ver los elementos impresos como valores hexadecimales.

Ahora te vamos a mostrar cómo escribir un arreglo de bytes en un archivo binario, como no queremos guardar su representación legible, queremos escribir una copia uno a uno del contenido de la memoria física, byte a byte.

data = bytearray(10)

for i in range(len(data)):

    data[i] = 10 - i

for b in data:

    print(hex(b))
    
    
    
    
Bytearrays: continuación
Entonces, ¿cómo escribimos un arreglo de bytes en un archivo binario?

Observa el código en el editor. Analicémoslo:

Primero, inicializamos bytearray con valores a partir de 10; si deseas que el contenido del archivo sea claramente legible, reemplaza el 10con algo como ord('a'), esto producirá bytes que contienen valores correspondientes a la parte alfabética del código ASCII (no pienses que harás que el archivo sea un archivo de texto; sigue siendo binario, ya que se creó con un indicador - bandera wb).
Después, creamos el archivo usando la función open(), la única diferencia en comparación con las variantes anteriores es que el modo de apertura contiene el indicador b.
El método write() toma su argumento (bytearray) y lo envía (como un todo) al archivo.
El stream se cierra de forma rutinaria.
El método write() devuelve la cantidad de bytes escritos correctamente.

Si los valores difieren de la longitud de los argumentos del método, puede significar que hay algunos errores de escritura.

En este caso, no hemos utilizado el resultado; esto puede no ser apropiado en todos los casos.

Intenta ejecutar el código y analiza el contenido del archivo recién creado.

Lo vas a usar en el siguiente paso.


Cómo leer bytes de un stream
La lectura de un archivo binario requiere el uso de un método especializado llamado readinto(), ya que el método no crea un nuevo objeto del arreglo de bytes, sino que llena uno creado previamente con los valores tomados del archivo binario.

Nota:

El método devuelve el número de bytes leídos con éxito.
El método intenta llenar todo el espacio disponible dentro de su argumento; si existen más datos en el archivo que espacio en el argumento, la operación de lectura se detendrá antes del final del archivo; el resultado del método puede indicar que el arreglo de bytes solo se ha llenado de manera fragmentaria (el resultado también lo mostrará y la parte del arreglo que no está siendo utilizada por los contenidos recién leídos permanece intacta).
Mira el código completo a continuación:

from os import strerror

data = bytearray(10)

try:
    bf = open('file.bin', 'rb')
    bf.readinto(data)
    bf.close()

    for b in data:
        print(hex(b), end=' ')
except IOError as e:
    print("Se produjo un error de E/S: ", strerr(e.errno))

Analicémoslo:

Primero, abrimos el archivo (el que se creó usando el código anterior) con el modo descrito como rb.
Luego, leemos su contenido en el arreglo de bytes llamado data, con un tamaño de diez bytes.
Finalmente, imprimimos el contenido del arreglo de bytes: ¿Son los mismos que esperabas?
Ejecuta el código y verifica si funciona.


from os import strerror

data = bytearray(10)

for i in range(len(data)):

    data[i] = 10 + i

try:

    bf = open('file.bin', 'wb')
    
    bf.write(data)
    
    bf.close()
    
except IOError as e:

    print("Se produjo un error de E/S: ", strerr(e.errno))




LIST OF CONTENTS
Module 5 
BACK
MODULE 5
5.1.1 Fundamentos de Python: Parte 2 
BACK
5.1.1 FUNDAMENTOS DE PYTHON: PARTE 2
5.1.1.1 Fundamentos de Python: Parte 2
5.1.1.2 Fundamentos de Python: M&oacute;dulo 5
5.1.1.3 M&oacute;dulos
5.1.1.4 Empleando M&oacute;dulos
5.1.1.5 Empleando M&oacute;dulos
5.1.1.6 Empleando M&oacute;dulos
5.1.1.7 Importando un M&oacute;dulo | math
5.1.1.8 Importando un M&oacute;dulo | math
5.1.1.9 Importando un M&oacute;dulo | math
5.1.1.10 Importando un M&oacute;dulo | math
5.1.1.11 Importando un M&oacute;dulo | * y as
5.1.1.12 Importando un M&oacute;dulo | aliasing
5.1.2.1 M&oacute;dulos &Uacute;tiles
5.1.2.2 M&oacute;dulos &Uacute;tiles | math
5.1.2.3 M&oacute;dulos &Uacute;tiles | math
5.1.2.4 M&oacute;dulos &Uacute;tiles | math
5.1.2.5 M&oacute;dulos &uacute;tiles | aleatorio
5.1.2.6 M&oacute;dulos &Uacute;tiles | random
5.1.2.7 M&oacute;dulos &Uacute;tiles | random
5.1.2.8 M&oacute;dulos &Uacute;tiles | random
5.1.2.9 M&oacute;dulos &Uacute;tiles | random
5.1.2.10 M&oacute;dulos &Uacute;tiles | platform
5.1.2.11 M&oacute;dulos &Uacute;tiles | platform
5.1.2.12 M&oacute;dulos &Uacute;tiles | platform
5.1.2.13 M&oacute;dulos &Uacute;tiles | platform
5.1.2.14 M&oacute;dulos &Uacute;tiles | platform
5.1.2.15 M&oacute;dulos &Uacute;tiles | platform
5.1.2.16 M&oacute;dulos &Uacute;tiles
5.1.3.1 M&oacute;dulos y Paquetes
5.1.3.2 M&oacute;dulos y Paquetes
5.1.3.3 M&oacute;dulos y Paquetes
5.1.3.4 M&oacute;dulos y Paquetes
5.1.3.5 M&oacute;dulos y Paquetes
5.1.3.6 M&oacute;dulos y Paquetes
5.1.3.7 M&oacute;dulos y Paquetes
5.1.3.8 M&oacute;dulos y Paquetes
5.1.3.9 M&oacute;dulos y Paquetes
5.1.3.10 M&oacute;dulos y Paquetes
5.1.4.1 Errores: el pan diario del programador
5.1.4.2 Errores: el pan diario del programador
5.1.4.3 Errores: el pan diario del programador
5.1.4.4 Errores: el pan diario del programador
5.1.4.5 Errores: el pan diario del programador
5.1.4.6 Errores: el pan diario del programador | try-except
5.1.4.7 Errores: el pan diario del programador | try-except
5.1.4.8 Errores: el pan diario del programador | try-except
5.1.4.9 Errores: el pan diario del programador | try-except
5.1.4.10 Errores: el pan diario del programador | try-except
5.1.4.11 Errores: el pan diario del programador | try-except
5.1.5.1 La anatom&iacute;a de las excepciones
5.1.5.2 La anatom&iacute;a de las excepciones
5.1.5.3 La anatom&iacute;a de las excepciones
5.1.5.4 La anatom&iacute;a de las excepciones
5.1.5.5 La anatom&iacute;a de las excepciones | raise
5.1.5.6 La anatom&iacute;a de las excepciones | raise
5.1.5.7 La anatom&iacute;a de las excepciones | assert
5.1.6.1 Excepciones &uacute;tiles
5.1.6.2 Excepciones &uacute;tiles
5.1.6.3 Excepciones &uacute;tiles
5.1.6.4 Leer ints de forma segura Lab
5.1.7.1 Caracteres y Cadenas
5.1.7.2 Caracteres y Cadenas
5.1.7.3 Caracteres y Cadenas
5.1.8.1 La naturaleza de las cadenas en Python
5.1.8.2 La naturaleza de las cadenas en Python
5.1.8.3 La naturaleza de las cadenas en Python
5.1.8.4 La naturaleza de las cadenas en Python
5.1.8.5 La naturaleza de las cadenas en Python
5.1.8.6 La naturaleza de las cadenas en Python
5.1.8.7 La naturaleza de las cadenas en Python
5.1.8.8 La naturaleza de las cadenas en Python
5.1.8.9 La naturaleza de las cadenas en Python
5.1.8.10 La naturaleza de las cadenas en Python
5.1.8.11 La naturaleza de las cadenas en Python
5.1.8.12 La naturaleza de las cadenas en Python
5.1.8.13 La naturaleza de las cadenas en Python
5.1.8.14 La naturaleza de las cadenas en Python
5.1.9.1 M&eacute;todos de cadenas
5.1.9.2 M&eacute;todos de cadenas
5.1.9.3 M&eacute;todos de cadenas
5.1.9.4 M&eacute;todos de cadenas
5.1.9.5 M&eacute;todos de cadenas
5.1.9.6 M&eacute;todos de cadenas
5.1.9.7 M&eacute;todos de cadenas
5.1.9.8 M&eacute;todos de cadenas
5.1.9.9 M&eacute;todos de cadenas
5.1.9.10 M&eacute;todos de cadenas
5.1.9.11 M&eacute;todos de cadenas
5.1.9.12 M&eacute;todos de cadenas
5.1.9.13 M&eacute;todos de cadenas
5.1.9.14 M&eacute;todos de cadenas
5.1.9.15 M&eacute;todos de cadenas
5.1.9.16 M&eacute;todos de cadenas
5.1.9.18 Tu propio split Lab
5.1.10.1 Cadenas en acci&oacute;n
5.1.10.2 Cadenas en acci&oacute;n
5.1.10.3 Cadenas en acci&oacute;n
5.1.10.4 Cadenas en acci&oacute;n
5.1.10.6 LABORATORIO: Un Display LED Lab
5.1.11.1 Cuatro simples programas
5.1.11.2 Cuatro simples programas
5.1.11.3 Cuatro simples programas
5.1.11.4 Cuatro simples programas
5.1.11.6 LABORATORIO: Mejorando el cifrado C&eacute;sar Lab
5.1.11.7 LABORATORIO: Pal&iacute;ndromos Lab
5.1.11.8 LABORATORIO: Anagramas Lab
5.1.11.9 LABORATORIO: El D&iacute;gito de la Vida Lab
5.1.11.10 LABORATIORIO: &iexcl;Encuentra una palabra! Lab
5.1.11.11 LABORATORIO: Sudoku Lab
5.2.1 Module 5 Quiz Quiz 
BACK
5.2.1 MODULE 5 QUIZ
5.2.1.1 Module 5 Quiz Quiz
5.3.1 Module 5 Test Quiz 
BACK
5.3.1 MODULE 5 TEST
5.3.1.1 Module 5 Test Quiz
Module 6 Now 
BACK
MODULE 6
6.1.1 Fundamentos de Python: M&oacute;dulo 6 
BACK
6.1.1 FUNDAMENTOS DE PYTHON: M&OACUTE;DULO 6
6.1.1.1 Fundamentos de Python: M&oacute;dulo 6
6.1.1.2 Los fundamentos de la POO
6.1.1.3 Los fundamentos de la POO
6.1.1.4 Los fundamentos de la POO
6.1.1.5 Los fundamentos de la POO
6.1.1.6 Los fundamentos de la POO
6.1.1.7 Los fundamentos de la POO
6.1.1.8 Los fundamentos de la POO
6.1.2.1 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.2 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.3 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.4 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.5 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.6 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.7 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.8 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.9 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.10 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.11 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.2.12 Un corto viaje desde el enfoque procedimental hasta el orientado a objetos
6.1.3.1 Propiedades de la POO
6.1.3.2 Propiedades de la POO
6.1.3.3 Propiedades de la POO
6.1.3.4 Propiedades de la POO
6.1.3.5 Propiedades de la POO
6.1.3.6 Propiedades de la POO
6.1.3.7 Propiedades de la POO
6.1.3.8 Propiedades de la POO
6.1.4.1 POO: M&eacute;todos
6.1.4.2 POO: M&eacute;todos
6.1.4.3 POO: M&eacute;todos
6.1.4.4 POO: M&eacute;todos
6.1.4.5 POO: M&eacute;todos
6.1.4.6 POO: M&eacute;todos
6.1.4.7 POO: M&eacute;todos
6.1.4.8 POO: M&eacute;todos
6.1.4.9 POO: M&eacute;todos
6.1.4.10 POO: M&eacute;todos
6.1.5.1 Fundamentos de POO: Herencia
6.1.5.2 Fundamentos de POO: Herencia
6.1.5.3 Fundamentos de POO: Herencia
6.1.5.4 Fundamentos de POO: Herencia
6.1.5.5 Fundamentos de POO: Herencia
6.1.5.6 Fundamentos de POO: Herencia
6.1.5.7 Fundamentos de POO: Herencia
6.1.5.8 Fundamentos de POO: Herencia
6.1.5.9 Fundamentos de POO: Herencia
6.1.5.10 Fundamentos de POO: Herencia
6.1.5.11 Fundamentos de POO: Herencia
6.1.5.12 Fundamentos de POO: Herencia
6.1.5.13 Fundamentos de POO: Herencia
6.1.5.14 Fundamentos de POO: Herencia
6.1.5.15 Fundamentos de POO: Herencia
6.1.5.16 Fundamentos de POO: Herencia
6.1.5.17 Fundamentos de POO: Herencia
6.1.5.18 Fundamentos de POO: Herencia
6.1.5.19 Fundamentos de POO: Herencia
6.1.6.1 Excepciones una vez m&aacute;s
6.1.6.2 Excepciones una vez m&aacute;s
6.1.6.3 Excepciones una vez m&aacute;s
6.1.6.4 Excepciones una vez m&aacute;s
6.1.6.5 Excepciones una vez m&aacute;s
6.1.6.6 Excepciones una vez m&aacute;s
6.1.6.7 Excepciones una vez m&aacute;s
6.1.6.8 Excepciones una vez m&aacute;s
6.1.7.1 Generadores y cierres
6.1.7.2 Generadores y cierres
6.1.7.3 Generadores y cierres
6.1.7.4 Generadores y cierres
6.1.7.5 Generadores y cierres
6.1.7.6 Generadores y cierres
6.1.7.7 Generadores y cierres
6.1.7.8 Generadores y cierres
6.1.7.9 Generadores y cierres
6.1.7.10 Generadores y cierres
6.1.7.11 Generadores y cierres
6.1.7.12 Generadores y cierres
6.1.7.13 Generadores y cierres
6.1.7.14 Generadores y cierres
6.1.8.1 Procesando archivos
6.1.8.2 Procesando archivos
6.1.8.3 Procesando archivos
6.1.8.4 Procesando archivos
6.1.8.5 Procesando archivos
6.1.8.6 Procesando archivos
6.1.8.7 Procesando archivos
6.1.8.8 Procesando archivos
6.1.8.9 Procesando archivos
6.1.8.10 Procesando archivos
6.1.8.11 Procesando archivos
6.1.9.1 Trabajando con archivos reales
6.1.9.2 Trabajando con archivos reales
6.1.9.3 Trabajando con archivos reales
6.1.9.4 Trabajando con archivos reales
6.1.9.5 Trabajando con archivos reales
6.1.9.6 Trabajando con archivos reales
6.1.9.7 Trabajando con archivos reales
6.1.9.8 Trabajando con archivos reales
6.1.9.9 Trabajando con archivos reales
6.1.9.10 Trabajando con archivos reales
6.1.9.11 Trabajando con archivos reales
6.1.9.12 Trabajando con archivos reales Now
6.1.9.13 Trabajando con archivos reales
6.1.9.14 Trabajando con archivos reales
6.1.9.15 LABORATORIO: Histograma de frecuencia de caracteres Lab
6.1.9.16 LABORATORIO: Histograma de frecuencia de caracteres ordenado Lab
6.1.9.17 LABORATORIO: Evaluando los resultados de los estudiantes Lab
6.2.1 Module 6 Quiz Quiz 
BACK
6.2.1 MODULE 6 QUIZ
6.2.1.1 Module 6 Quiz Quiz
6.3.1 Module 6 Test Quiz 
BACK
6.3.1 MODULE 6 TEST
6.3.1.1 Module 6 Test Quiz
6.6.1 Fundamentos de Programaci&oacute;n en Python - PCAP 
BACK
6.6.1 FUNDAMENTOS DE PROGRAMACI&OACUTE;N EN PYTHON - PCAP
Fundamentos de Programaci&oacute;n en Python - PCAP
Cómo leer bytes de un stream
Se ofrece una forma alternativa de leer el contenido de un archivo binario mediante el método denominado read().

Invocado sin argumentos, intenta leer todo el contenido del archivo en la memoria, haciéndolo parte de un objeto recién creado de la clase bytes.

Esta clase tiene algunas similitudes con bytearray, con la excepción de una diferencia significativa: es immutable.

Afortunadamente, no hay obstáculos para crear un arreglo de bytes tomando su valor inicial directamente del objeto de bytes, como aquí:

from os import strerror

try:

    bf = open('file.bin', 'rb')
    
    data = bytearray(bf.read())
    
    bf.close()

    for b in data:
    
        print(hex(b), end=' ')

except IOError as e:

    print("Se produjo un error de E/S: ", strerr(e.errno))
    
    
    
    Cómo leer bytes de un stream: continuación
Si el método read() se invoca con un argumento, se especifica el número máximo de bytes a leer.

El método intenta leer la cantidad deseada de bytes del archivo, y la longitud del objeto devuelto puede usarse para determinar la cantidad de bytes realmente leídos.

Puedes usar el método como aquí:

try:

    bf = open('file.bin', 'rb')
    
    data = bytearray(bf.read(5))
    
    bf.close()

    for b in data:
    
        print(hex(b), end=' ')

except IOError as e:

    print("Se produjo un error de E/S:", strerr(e.errno))

Nota: los primeros cinco bytes del archivo han sido leídos por el código; los siguientes cinco todavía están esperando ser procesados.


Copiando archivos: una herramienta simple y funcional
Ahora vas a juntar todo este nuevo conocimiento, agregarle algunos elementos nuevos y usarlo para escribir un código real que pueda copiar el contenido de un archivo.

Por supuesto, el propósito no es crear un reemplazo para los comandos como copy de (MS Windows) o cp de (Unix/Linux) pero para ver una forma posible de crear una herramienta de trabajo, incluso si nadie quiere usarla.

Observa el código en el editor. Analicémoslo:

Las líneas 3 a la 8: solicitan al usuario el nombre del archivo a copiar e intentan abrirlo para leerlo; se termina la ejecución del programa si falla la apertura; nota: emplea la función exit() para detener la ejecución del programa y pasar el código de finalización al sistema operativo; cualquier código de finalización que no sea 0 significa que el programa ha encontrado algunos problemas; se debe utilizar el valor errno para especificar la naturaleza del problema.
Las líneas 9 a la 15: repiten casi la misma acción, pero esta vez para el archivo de salida.
La línea 17: prepara una parte de memoria para transferir datos del archivo fuente al destino; Tal área de transferencia a menudo se llama un búfer, de ahí el nombre de la variable; el tamaño del búfer es arbitrario; en este caso, decidimos usar 64 kilobytes; técnicamente, un búfer más grande es más rápido al copiar elementos, ya que un búfer más grande significa menos operaciones de E/S; en realidad, siempre hay un límite, cuyo cruce no genera más ventajas; pruébalo tú mismo si quieres.
Línea 18: cuenta los bytes copiados: este es el contador y su valor inicial.
Línea 20: intenta llenar el búfer por primera vez.
Línea 21: mientras se obtenga un número de bytes distinto de cero, repite las mismas acciones.
Línea 22: escribe el contenido del búfer en el archivo de salida (nota: hemos usado un segmento para limitar la cantidad de bytes que se escriben, ya que write() siempre prefiero escribir todo el búfer).
Línea 23: actualiza el contador.
Línea 24: lee el siguiente fragmento de archivo.
Las líneas 29 a la 31: limpieza final: el trabajo está hecho.


 
 Sandbox
Code

from os import strerror

srcname = input("¿Nombre del archivo fuente?: ")

try:
src = open(srcname, 'rb')

except IOError as e:

print("No se puede abrir archivo fuente: ", strerror(e.errno))

exit(e.errno)

dstname = input("¿Nombre del archivo de destino?: ")



try:

dst = open(dstname, 'wb')

except Exception as e:

print("No se puede crear el archivo de destino: ", strerr(e.errno))

src.close()

exit(e.errno)


buffer = bytearray(65536)

total = 0




try:

readin = src.readinto(buffer)

while readin > 0:

written = dst.write(buffer[:readin])

total += written

readin = src.readinto(buffer)

except IOError as e:

print("No se puede crear el archivo de destino: ", strerr(e.errno))

exit(e.errno)

print(total,'byte(s) escritos con éxito')

src.close()

dst.close()

from os import strerror



    
    
