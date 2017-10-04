# EXAMEN 1 SISTEMAS OPERATIVOS

**nombre:** Diego Lamus  
**código:** A00320776  


# SOLUCIÓN

Los puntos del 1 al 5 son los retos de la página  https://cmdchallenge.com. Todos los comandos que se ejecutaron en la máquina virtual también fueron probados en la página, y se verificó que efectivamente pasaran el reto antes de incorporarlos al documento. Lo anterior se observa en la siguiente imagen:  


![](https://github.com/diegolamus/so-exam1/blob/A00320776/solucion/A00320776/IMAGENES/CapturaRETOS.PNG)

**1.** Para sumar todos los números contenidos en un archivo “.txt”, donde se encuentra un número por línea se puede usar el siguiente comando:  


 	awk ‘{ sum += $1} END {print sum}’ nombreArchivo.txt

El comando awk permite recorrer linea por linea el archivo; {sum += $1} indica que por cada línea que se lea se agregue a la variable sum lo que está contenido en la columna 1 (columna 1 = $1); el END indica que cuando se termine de recorrer todas las líneas del archivo se haga {print sum} lo que imprime sum.  

![](https://github.com/diegolamus/so-exam1/blob/A00320776/solucion/A00320776/IMAGENES/CapturaSO1.PNG)  

**2.** Para cambiar los espacios por puntos de todos los nombre de los archivos en un directorio se puede usar el siguiente comando:

	ls -1 | sed ‘s/ /./g’

La primera parte del comando ls -1 despliega los nombres de todos los archivos y directorios en el directorio actual; luego | pasa la salida del comando y con sed ‘s/ /./g’ se cambian todos los espacios por puntos; en ‘s/ /./g’ la s indica que se va a hacer substitución y la g que son todas las ocurrencias del texto, no solo la primera.  

![](https://github.com/diegolamus/so-exam1/blob/A00320776/solucion/A00320776/IMAGENES/CapturaSO2.PNG)   

**3.** Para imprimir todas las líneas de un archivo en orden contrario se puede usar el siguiente comando:

    tac nombreArchivo.txt

En la primera parte la funcionalidad específica de tac es imprimir en orden contrario; en la segunda se pone el nombre del archivo que se quiere imprimir.  

![](https://github.com/diegolamus/so-exam1/blob/A00320776/solucion/A00320776/IMAGENES/CapturaSO3.PNG)  

**4.** Para imprimir las líneas de un archivo, pero solo imprimir las líneas que no se han impreso ya se puede usar el siguiente comando:

	awk ‘!impresos[$0]++’ nombreArchivo.txt

En el comando awk permite recorrer el archivo linea por linea. El comando que recibe ‘!impresos[$0]++’ lo que hace es ingresar cada línea ($0) como el índice de un arreglo (impresos) y ver si aún no se ha asignado (!), en este caso imprime y luego lo opera con (++) asignándole un valor y haciendo imposible que se vuelva a imprimir. La última parte es el nombre del archivo.  

![](https://github.com/diegolamus/so-exam1/blob/A00320776/solucion/A00320776/IMAGENES/CapturaSO4.PNG)   


**5.** Para ordenar las líneas de un archivo, separado por comas cada línea e imprimirlas en una tabla de puede usar el siguiente comando:

    column -t -s, nombreArchivo

El comando column ordena su entrada en varias columnas; -t es una opción del comando que determina el número de columnas en la entrada y las ordena; -s, indica que las columnas están separadas por comas, -s indica que se va a introducir el separador. nombreArchivo es el nombre del archivo que se quiere imprimir en columnas.  

![](https://github.com/diegolamus/so-exam1/blob/A00320776/solucion/A00320776/IMAGENES/CapturaSO5.PNG)   


**6.** A continuación se presenta evidencia de un script que se ejecute cada 5 minutos descargando un libro del proyecto https://www.gutenberg.org/ en el directorio /home/gutenberg/mybooks. En caso de existir el libro se debe sobreescribir.

Para descargar el libro y guardarlo en el directorio adecuado escribí el siguiente código:  

![](https://github.com/diegolamus/so-exam1/blob/A00320776/solucion/A00320776/IMAGENES/CapturaSCRIPT_DESCARGA.PNG)   

* La primera línea indica que es un script de bash.
* Los “echo” se usaron para ver los resultados del script al ejecutarlo.
* Con “wget” se realiza la descarga del libro; -q oculta la información de la descarga; -O guarda la descarga con el nombre que se especifica, en este caso libro.epub.
* Se mueve el libro a su directorio de destino con mv.
* Se verificó que se modificara el libro imprimiendo la fecha del sistema y viendo que concuerde con la hora de modificación del archivo, la cual es verificada con el comando “stat”. Esto coincide cada que se descarga el libro por lo que efectivamente se está sobreescribiendo.  

Ahora, para que la descarga del libro se realice cada cinco minutos se agregó la siguiente línea en el archivo crontab:

    */5 * * * * /root/scripts/downloadbook

Al agregar la linea anterior lo que se se hace es programar la ejecución cada cinco minutos (*/5) cada hora del dia (*/5 *) cada dia del mes (*/5 * *) cada mes del año (*/5 * * *) cada año (*/5 * * * *) de /root/scripts/downloadbook.

Para verificar que la ejecución del script fuera correcta se verificó el estado del libro descargado, y cinco minutos después se verificó de nuevo el estado, cerciorándose que se hubiera actualizado:  

![](https://github.com/diegolamus/so-exam1/blob/A00320776/solucion/A00320776/IMAGENES/CapturaFUNCIONAMIENTO_SCRIPT.PNG)   

En la imagen se puede observar que se actualiza el libro a los cinco minutos después de la última actualización.











