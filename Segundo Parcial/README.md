<h3 align="center">MULTIPLICACIÓN DE MATRICES DE GRAN TAMAÑO UTILIZANDO MPI Y CUDA</h3>
<br>
<br>
<br>
<br>
<br>
<h3 align="center">HIGH PERFORMANCE COMPUTING</h3>
<br>
<br>
<br>
<br>
<br>
<h3 align="center">DOUGLAS HERNANDEZ</h3>
<h3 align="center">SEBASTIAN ARDILA AGUDELO</h3>
<br>
<br>
<br>
<br>
<br>
<h3 align="center">UNIVERSIDAD TECNOLÓGICA DE PEREIRA</h3>
<h3 align="center">INGENIERÍA DE SISTEMAS Y COMPUTACIÓN</h3>
<h3 align="center">2016</h3>
<br>
<HR width=100% align="center">
<br>
<h2 >ENUNCIADO</h2>
**1.** Construir una aplicación que realice la multiplicación de matrices de gran tamaño utilizando MPI y CUDA.
<br>

**2.** La aplicación deberá distribuir el trabajo a realizarse en 4 nodos máximo.
<br>

**3.** Para cada uno de los nodos envueltos en el procesamiento se deberá realizar el cálculo necesario sobre la GPU.
<br>

**4.** El tamaño de las matrices a multiplicar será definido por cada uno de los estudiantes y será tenido en cuenta como un 10% de ésta nota.
<br>

**5.** Se tendrá que hacer un análisis de tiempo que muestre cómo el algoritmo desarrollado se comporta al correr usando 1 solo nodo, usando 2, usando 3 y finalmente 4. (10%)
<br>

**6.** Se deberá comparar la solución obtenida con una donde se usen solamente CPU’s. Esta comparativa deberá también incluir tiempos de ejecución y gráficas de aceleración. (10%). De nuevo hacer el análisis para cada uno de los nodos.
<br>

**7.** Será necesario para el desarrollo del trabajo que los estudiantes investiguen sobre el proceso de compilación de aplicaciones que usan OPENMPI+CUDA.
<br>

**8.** El correcto funcionamiento de la aplicación será evaluado, esto significa incluir una rutina de comparación de resultados que deberá ser ejecutada sólo cuando el profesorlo indique y con ánimo de verificar que la multiplicación es correcta. (10%)
<br>

**9.** La calidad y claridad del reporte que se presentará utilizando el markdown del repositorio tendrá un peso de 10%.
<br>

**10.** La entrega se hará de forma individual y tendrá un peso en la evaluación del 50%. Esto indica la claridad en la explicación, el conocimiento de los comandos básicos para ejecutar programas através de slurm y la comprensión en los procesos de compilación.
<br>
<br>
**NOTA:** Recuerden que el recurso (Clúster) es compartido por todos y será vital el buen manejo que le demos al mismo. Verificar siempre si ustedes como primeros usuarios han dejado alguna tarea que no finaliza nunca y matar el trabajo. No dejen el desarrollo para la última semana porque probablemente van a estar todos haciendo pruebas a última hora. Si tienen problemas de ejecución por caída del cluster no olviden avisarme. Pueden crear grupos de trabajo de máximo 2 estudiantes.
<br>
<h2 >GENERACIÓN DEL CÓDIGO</h2>
Para la generación del código en el momento de usar mpi+cuda al mismo tiempo usamos dos archivos donde se encuentra el código de mpi y el de cuda respectivamente, las funciones que se encuentran en el archivo de cuda llamado **multi_mpi_cuda.cu** servirán para multiplicar las matrices bajo cuda, a su vez estas funciones se pueden llamar como funciones externas, esto gracias a que un archivo aparte llamado **extern.h** hace posible esta labor. Desde el archivo mpi llamado **multi_mpi.c** se puede importar el archivo extern.h como una librería, permitiendo usar sus funciones, es de este modo al ejecutarse cada nodo usando mpi se hace el respectivo calculo con gpu usando las librerias externas previamente definidas.
Los siguientes comandos permiten usar cuda+mpi y compilar los archivos:

``` /usr/local/bin/mpicxx -o multi.o -c multi_mpi.c ```

``` "/usr/local/cuda-8.0"/bin/nvcc -ccbin g++ -m64 -gencode arch=compute_30,code=sm_30 -gencode arch=compute_35,code=sm_35 -gencode arch=compute_37,code=sm_37 -gencode arch=compute_50,$ ```

``` /usr/local/bin/mpicxx -o multi multi.o multi_cuda.o  -L"/usr/local/cuda-8.0"/lib64 -lcudart ```

Aquí podemos ver como el archivo extern.h deja usar las librerias de otro programa:
<br>
![imagen 1.1](images_data/extern.png)
<br>
Luego al exportar este archivo podemos usar las funciones:
<br>
![imagen 1.2](images_data/include-extern.png)
<br>
De esta forma definimos cuales funciones dentro de extern.h usaremos:
![imagen 1.2](images_data/extern-functions-definition.png)
<br>
<h2 >PROBLEMAS QUE SE ENCUENTRAN</h2>
Tuvimos problemas a la hora de entender como compilar el programa para poder compilar y ejecutar cuda+mpi, por lo que tuvimos que investigar de varias fuentes mencionadas en la sección de referencias, también tuvimos problemas al correr los tiempos de ejecución con la implementación y usando solo CPU.
<br>
<HR width=100% align="center">
<br>
<h2>RECOLECCIÓN DE DATOS</h2>
<br>
1. En la **tabla 1.1**, Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
![tabla 1.1](Tamaños_matriz.PNG)
<br>
<h6>tabla 1.1</h6>
<br>
2. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum como podemos observar en la **gráfica 1.1** para la CPU y la **gráfica 1.2** para la GPU
![gráfica 1.1](grafica1-CPU.PNG)
<br>
<h6>gráfica 1.1</h6>
<br>
<HR width=100% align="center">
<br>
<h2>REFERENCIAS</h2>
1. https://www.pdc.kth.se/resources/software/old-installed-software/mpi-libraries/cuda-and-mpi
2. https://github.com/kala855/hpccourse/tree/master/mpiexamples/mpi_cuda_hello_world
3. http://lsi.ugr.es/jmantas/pdp/ayuda/ayuda.php
<br>
<h2>CONCLUSIONES</h2>
1. Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
2. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum
3. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. 
<br>