### Descargue y descomprima los ficheros de los ejercicios (hágalo solo la primera vez):
Utilice 
[este enlace](https://github.com/IB-2022-2023/P02-Intro-Linux/blob/main/ib-p02-Intro-Linux.tar.gz)
para descargar (*Download*) el fichero `ib-p02-Intro-Linux.tar.gz`.


Abra una terminal, colóquese (`cd`) en el directorio donde descargó el fichero y descomprímalo:

``` .bash
$ tar xzvf linux-exercise.tar.gz El indicador
``` 
La opción `v` (*verbose*) en el comando `tar` muestra los ficheros con la ruta conforme son descomprimidos y
extraídos. 
Como resultado de la ejecución del comando obtendrá una cantidad de ficheros en un subdirectorio llamado `linux-exercises`. 
Vaya a ese directorio con el comando `cd`.

### Desplazarse por el árbol de directorios 
Comandos en este ejercicio: `cd`, `mkdir`, `ls`, `mv`, `more`, `less`, `cat`, `tar`.

El objetivo de este ejercicio es aprender a moverse con `cd`, ver el contenido de los ficheros,
crear directorios, mover y copiar ficheros.

#### Descomprimir el fichero dirs.tar.gz
``` .bash
$ cd moving-around
$ tar zxvf dirs.tar.gz
``` 

#### Averigüe qué directorios y ficheros se crearon
``` .bash
$ ls
$ ls -l
$ cd inputs
$ ls -l
$ cd ..
``` 
Y así sucesivamente...

#### ¿Qué fichero de salida trata sobre la cafeína?
Acceda al subdirectorio de resultados (que a su vez contiene subdirectorios). 
Los ficheros `pdb` tienen una línea con con el texto "TITLE AlgúnNombre". 

A continuación se muestran algunos comandos que puede probar para averiguar qué fichero trata sobre la cafeína. 

``` .bash
$ grep caffeine *.pdb
$ grep caffeine */*.pdb
$ grep title */*.pdb
$ grep TITLE */*.pdb
``` 
¿Sobre qué trata la información del resto de ficheros?

Puede mostrar el contenido completo de un fichero usando los comandos `more`, `less` o `cat`.

#### Crear subdirectorios
Solo hay tres directorios `result*`. 
Cree directorios nuevos: `result4` y `result5` para los ficheros de salida 4 y 5 y mueva los ficheros de salida (`out_4.pdb`, `out_5.pdb`) a esos directorios.
* cd al directorio `outputs`
* Cree un nuevo subdirectorio con `mkdir result4`
* Mueva el fichero `out_4.pdb` con el comando `mv result3/out_4.pdb result4`
* Repita para `result5` y `out_5.pdb`

#### Cree un nuevo fichero tar comprimido de la nueva jerarquía de directorios
Colóquese en el directorio `moving-around` donde se encuentra el fichero tar original (`dirs.tar.gz`) usando
el comando `cd`.

``` .bash
$ tar zvcf dirs-new.tar.gz inputs outputs
```

#### Confirme el contenido del fichero tar
``` .bash
$ tar ztf dirs-new.tar.gz
``` 

### Use el comando `man` (*manual*) para encontrar opciones para el comando `ls`
Comandos en este ejercicio: `man`, `ls`.

En este ejercicio aprenderá cómo encontrar información detallada sobre las opciones y sobre cómo ordenar la salida del comando `ls`.


#### Abra la página de manual de `ls`
``` .bash
$ man ls
``` 

Ese comando abre la página del manual para `ls`. 
Como hay muchas opciones para el comando, resulta útil consultarlas en la página de manual.
La búsqueda se activa presionando `/` y luego escribiendo un (comienzo de) una palabra clave. 
Al presionar *enter* se activa la búsqueda y presionando `n` (*next*) se pasa a la siguiente ocurrencia de la
palabra clave.

También puede desplazarse por la pantalla con las teclas de flecha cuando sea necesario. 
Salga de la página del manual presionando la tecla `q` (*quit*).

Practique estas búsquedas localizando una opción para ordenar la salida del comando `ls`.
Para ello en la página de manual escriba `/sort` (*sort* sería la palabra clave) y presione *enter*.


#### Encuentre la opción que ordena la salida por tamaño de fichero
Presione `n` tantas veces como sea necesario hasta que encuentre la opción para ordenar por tamaño de fichero. 
También puede usar alguna otra palabra clave para encontrar eso, por ejemplo, tamaño (*size*).

#### Ordenar el contenido del directorio por tamaño de fichero
Vaya al directorio `moving-around/inputs` y ordene los ficheros por tamaño:

``` .bash
$ ls -S
``` 

#### Opciones adicionales
Busque la opción que invierta el orden de clasificación (es decir, imprima el fichero más grande al final). 
Puede dar las opcións al comando `ls` juntas (por ejemplo, `ls -la` en lugar de `ls -l -a`).

Busque la opción que mostrará el tamaño del fichero en "formato legible por humanos", es decir, kB/MB/GB en lugar de bytes (el valor predeterminado).

Sugerencia: también puede buscar el significado de las opcións directamente por `/-S` (que buscará la aparición de `-S` (o incluso mejor `-S ` (con un espacio final)) si quiere saber qué hace esa opción.


#### Ordenar el contenido del directorio por fecha de creación de los ficheros
El comando:
``` .bash
$ ls -ltr
``` 
Muestra los ficheros en formato largo (`l`) ordenados en orden inverso (`r`, *reverse*) por fecha de creación (`t`, *time*).
De este modo aparecerán los últimos en la lista los últimos ficheros que se hayan creado.

El comando 
``` .bash
$ touch nombre-fichero
``` 
modifica la fecha del fichero que se le pasa como parámetro (*nombre-fichero*).

### Uso de comodines (*wildcards*)
Comandos en este ejercicio: `ls., `cp`.
En este ejercicio aprenderá a actuar sobre múltiples ficheros usando comodines.

Linux habilita comodines o expresiones regulares para hacer coincidir ficheros o cadenas que difieren solo en algunas formas controladas.

#### Limite los ficheros de listado con comodines
Colóquese en el directorio `moving-around/outputs`.
Revise todos los contenidos.

``` .bash
$ ls
```

Enumere solo aquellos ficheros que tienen una "a" en el nombre y terminan en ".pdb"

``` .bash
$ ls *a*.pdb
```

Enumere aquellos ficheros que tienen un nombre con siete caracteres y terminan en ".pdb"

``` .bash
$ ls ???????.pdb
```
Colóquese en el directorio `moving-around/outputs`.
Liste todos los ficheros pdb en los subdirectorios.

``` .bash
$ ls */*.pdb
```

En el comando anterior, el primer asterisco indica que se revisen todos los subdirectorios en el directorio actual, y el segundo todas las cadenas. 
Ahora limite la lista solo a aquellos ficheros de salida que tienen un número 2-5 en su nombre:

``` .bash
$ ls */out_[2-5].pdb
```
¿Cuál es la diferencia con el siguiente comando?

``` .bash
$ ls */*[2-5].pdb
```

