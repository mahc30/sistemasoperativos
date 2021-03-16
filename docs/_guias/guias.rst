Unidad 1: Rust
===============

Introducción a Rust
-------------------

¿Qué es Rust?
^^^^^^^^^^^^^

Rust es un lenguaje de programación compilado, de propósito general y multiparadigma desarrollado por Mozilla,
es decir, está hecho para soportar programación funcional pura, por procedimientos, imperativa y orientada a objetos. 
Además Rust es desarrollado abiertamente gran parte de las contribuciones al lenguaje han sido hechas por la comunidad. 

¿Porqué Rust?
^^^^^^^^^^^^^

Rust está hecho para crear programas tanto del lado del cliente como el servidor, con un énfasis en la seguridad, el manejo adecuado de la memoria
y la concurrencia sin sacrificar el rendimiento. Con Rust podemos programar:

- Web
- Sistemas Embebidos
- Redes y Servidores
- Aplicaciones de Línea de comandos

Características del Lenguaje
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- Es compilado
- No tiene Garbage collector
- Tipos de datos compuestos (Estructuras)
- Ownership
- Inferencia de Tipos

Conociendo el Lenguaje
----------------------

Hello World
^^^^^^^^^^^

Comencemos por hacer un Hello World en Rust, para esto necesitamos solo tenemos que tener instalado Rust en nuestras máquinas.
Vamos a crear una carpeta para guardar nuestro proyecto

.. code-block:: bash

    mkdir hello_world
    cd hello_world
    touch hello_world.rs

.. image:: \../_static/guias/hello_world_codeblock.png
   :width: 400pt

El código aún no puede ser ejecutado, recordemos que Rust es un lenguaje compilado, esto significa que el código aún tiene que ser traducido
a instrucciones que la máquina pueda entender.

.. code-block:: bash

    rustc hello_world.rs

Este comando nos generará un ejecutable en la misma carpeta, ahora sí podemos correr nuestro programa.

.. code-block:: bash

    ./hello_world.rs

Partes de un programa de Rust
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Notarás que la sintaxis de Rust es bastante similar a la de C y C++. 

.. code-block:: rust

    fn main() {
        
    }

En Rust la función ``main()`` es especial, siempre es el primer código que se ejecuta en cualquier programa en Rust. En este caso
no tiene ningún parámetro, si los tuviera iría dentro del ``( )``. Además el cuerpo de la función está dentro del ``{ }``. 
Estos elementos siempre estarán presentes cuando escribamos funciones.

Dentro de la funcion main() encontramos el siguiente código:

.. code-block:: rust

    println!("¡Hello, World!");

Para imprimir el mensaje por consola llamamos ``println!()`` ¡ojo, no es una función! el caracter ``!`` indica que se está llamando es a un
macro, si fuera una función la invocaríamos como ``println()``. Hablaremos de macros más adelante pero por ahora
solo nos interesa saber que ``!`` significa que estamos llamando a un macro en lugar de una función.

Como en todos los lenguajes, Rust también tiene comentarios:

.. code-block:: rust

    //En rust solo existen comentarios de una línea
    //Si queremos hacer comentarios más largos
    //Tendremos que comentar cada línea por separado


Variables
^^^^^^^^^^^^^^^

En Rust tenemos dos palabras para declarar variables, ``let`` y ``const``, 
además las variables son inmutables por defecto, esto significa que no 
podemos reasignar el valor de una variable, vámos a ver cómo funciona,
crea un programa con el siguiente código:

.. image:: \../_static/guias/variables_codeblock.png
   
*Recuerda que para correr el programa puedes usar el comando* ``rustc <programa>``

- ¿Puedes ejecutar el programa? ¿Por qué?
- ¿Qué dice el mensaje en la terminal?
- ¿Qué cambios harías al programa para que funcione?

.. raw:: html

    <details>
    <summary> <strong>Spoiler</strong> una solución al problema puede ser: </summary>
 
.. code-block:: rust
 
    fn main() {
        let mut a = 3;
        let b = 2;

        println!("El valor de a es {} y el de b es {}", a, b);
 
        a = a - b;
 
        println!("El valor de a es {} y el de b es {}", a, b);
    }       
 
.. raw:: html
  
    Lo que hicimos fue agregar la palabra <strong> mut </strong> a la declaración de la variable a
    de esta manera le indicamos al programa que la variable puede ser modificada más adelante.

   </details>

|

La diferencia entre declarar variables con ``let`` y ``const``, es que las constantes **siempre** son inmutables.

También habrás notado que para imprimir variables debemos indicar dónde queremos que aparezca en el mensaje
con ``{}`` y luego pasamos esas variables como argumentos en el orden que queremos que aparezcan. Esto es posible
porque Rust sabe cuál es el tipo de las variables que se quieren imprimir desde el tiempo de compilación.

A esto le llamamos **inferencia de tipos**, también es esta la razón por la que podemos usar palabras como
**let** y **const** para declarar diferentes tipos de variables sin tener que indicarle si es un número, o un booleano, un caracter...
Además se encarga de verificar que no hayan instrucciones que puedan poner en riesgo la 
ejecución del programa. Recordemos que Rust tiene algunas reglas más estrictas que lenguajes como C, y si detecta algo que
*podría* causar un error en tiempo de ejecución simplemente **no compila**.

Tipos de Datos
^^^^^^^^^^^^^^^

En la sección anterior hablamos de que Rust sabe que tipo de dato tiene cada variable con solo conocer su valor, pero también es posible
para nosotros indicar el tipo de dato que queremos en esa variable. Veamos:

.. code-block:: rust
    
    fn main() {
        let a: i8 = -127;
        let mut b: u16 = 65535;
        let c: f32 = 50.23167581519675;
        let d: bool = true;
        let e: char = 'e';
        let array: [i32; 6] = [1,2,3,4,5,6];
        let tupla: (i8, u16, char) = (a, b, e);

        println!("a: {} b: {} c: {} d: {} e: {}",
           a,b,c,d,e);

        for i in 0.. array.len() {
            print!("array[{}] = {}\n", i, array[i]);
        }

        println!("Tupla.1 = {}", tupla.1);
    }

Todo lo que tenemos que hacer es agregar ``:`` después del nombre de la variable e indicar 
el tipo de dato que queremos almacenar en ella.

Notarás que los tipos de dato enteros no son solo un ``int`` si no que es una ``i`` seguida de un número,
esto es para indicar el tamaño en bits del entero. ``i8`` significa que es un número entero con signo de 8 bits.
Del mismo modo podemos declarar números enteros sin signo con la letra ``u`` seguida de su tamaño, como ``u16``.

- ¿Cuál es la diferencia entre un tipo de dato entero con signo y sin signo?
- ¿Cuál es el rango de números decimales para un ``i32``?
- ¿Cuál es el rango de números decimales para un ``u32``?

En la siguiente imagen puedes ver los diferentes tipos de datos entero que hay:

.. image:: \../_static/guias/int_datatype.png

*tomado de: https://doc.rust-lang.org/book/ch03-02-data-types.html*

**Ejercicio**

En un programa de Rust declara dos variables, una que sea i32 y otra u32.
Intenta sumar ambas variables e imprimir el resultado por consola. ¿Qué ocurre?


**Arrays**

En el ejemplo podemos ver cómo declaramos, asignamos e imprimimos un arreglo, en Rust los arreglos tienen tamaño fijo y 
este debe ser conocido en tiempo de compilación, es decir que en ningún momento podemos agregar o eliminar elementos de este,
prestemos atención a esta línea:

.. code-block:: rust

    let array: [i32; 6] = [1,2,3,4,5,6];

Aquí declaramos una variable con la que nos referiremos a un arreglo, podemos leerlo como:


"**array** es un arreglo de tipo **i32** y tamaño **6**".

- ¿Cuantos bytes ocupa este arreglo en la memoria?

En muchos lenguajes de programación el tipo de dato ``char`` ocupa 1 byte en memoria, sin
embargo en Rust los caracteres están pensados para representar cualquier valor Unicode, 
te invito a que consultes cuanto ocupa un char en Rust y respondas la siguiente pregunta:

- ¿Cuántos bytes ocuparía si en lugar de ``i32`` fuera ``char``?

Funciones y Loops
^^^^^^^^^^^^^^^^^^^^^^
Tomate un momento para analizar la siguiente función, es una implementación de
un bubble sort para ordenar un vector.

- ¿Qué palabra se usa para declarar una función?
- ¿Cuántos parametros toma la función?
- ¿Cómo se llaman los parámetros y qué tipos de datos son?
- ¿Cuál parámetro utilizamos para definir el rango de los ciclos for?
- ¿Al finalizar la función, el vector quedaría ordenado de forma ascendente o descendente?

.. code-block:: rust

    fn sort(arr: &mut Vec<i32>, len: usize) {
        for i in 0..len {
            
            for j in 0..len {
                if es_mayor(arr[j], arr[i]) {
                    
                    //Swap
                    let temp: i32 = arr[i];
                    arr[i] = arr[j];
                    arr[j] = temp;
                }
            }
        }
    }

En el ejemplo hay un símbolo que no habíamos visto, el ``&`` indica que 
esta variable es un ``apuntador``. Un apuntador es un tipo de dato que representa
una dirección en la memoria, en este caso, significa que
el parámetro ``arr`` no guarda un ``Vec<i32>`` si no que guarda la **dirección**
en memoria en que se encuentra.

Más adelante estudiaremos mejor los apuntadores, pero por el momento solo tienes que saber que ``&`` indica que esa 
variable guarda una dirección en memoria, en Rust no es común utilizar directamente 
el ``&`` porque el lenguaje tiene muchos métodos que nos ayudan a manipular la memoria de forma segura. 

Entrada y Salida
^^^^^^^^^^^^^^^^^^^

Cuando necesitamos obtener input del usuario, tenemos que importar la librería ``io`` (input/output).
Solo tenemos que importar la librería con ``use`` y ya podremos acceder a todas sus funciones con ``::``. Mira el siguiente ejemplo:

.. code-block:: rust
    
    use std::io;

    fn main() {    
        println!("Escriba algo: ");
        let mut input : String = String::new();
        io::stdin().read_line(&mut input).expect("Failed to read");
        println!("Usted escribió: {}", input);
    }

Tenemos un String mutable "input" que usaremos para guardar lo que escriba el usuario por consola, presta atención a cómo lo inicializamos en la misma
línea, usamos ``::`` para acceder al método ``new()`` de ``String``, la sintaxis del ``::`` se usa para indicar que una función está asociada al tipo 
``String`` más que a una instancia en particular, en algunos lenguajes a esto se le llaman métodos estáticos.

En resumen, en este punto la variable mutable ``input`` está asociado a una instancia vacía de ``String``.

En la siguiente linea, del mismo modo llamamos al método ``stdin()`` de ``io``. Esto nos retorna una instancia de ``stdin()`` de la cuál podemos 
invocar el método ``read_line(&mut input)``. El trabajo de ``read_line`` es tomar cualquier entrada que escriba el usuario y copiarlo en un String,
por lo tanto toma como argumento un String, además el String tiene que ser mutable para que la función pueda cambiar su contenido.

Mira que pasamos como argumento un **apuntador** o **referencia** a ``input``, el ``&`` nos permite acceder a un mismo dato desde diferentes partes
de nuestro programa sin necesidad de copiar todos los datos varias veces. Cuando estudiemos el concepto de *Ownership* en Rust hablaremos más de esto.

Cargo
^^^^^^^^^

Hasta ahora no hemos tenido la necesidad de utilizar ``cargo``, el administrador de paquetes de Rust, que nos permite usar librerías 
externas, usualmente desarrolladas por la comunidad.

Para comprobar que tienes cargo instalado usa el comando 

.. code-block:: bash
    
    cargo --version

Si aún no lo has instalado, en la :doc:`unidad 1 <../_unidad1/unidad1>`  hay instrucciones de como instalarlo.

Cargo nos facilita todo el proceso de crear, organizar, compilar y correr un proyecto de Rust. Es muy sencillo:

Para crear un nuevo proyecto:

.. code-block:: bash
    
    cargo new <nombre_del_proyecto>

Para compilar o 'construir' el proyecto

.. code-block:: bash
    
    cargo build

Para correr el proyecto, este comando también construye el proyecto automáticamente.

.. code-block:: bash
    
    cargo run

Apuntadores
^^^^^^^^^^^^

En algunos de los ejemplos anteriores ya tuvimos un acercamiento a lo que son los apuntadores, un apuntador es una variable que contiene la dirección de
una variable.

+------------+------------+
|  Dirección |            |
+============+============+
|     0      |     10     |
+------------+------------+
|     4      |     11     |
+------------+------------+
|     8      |     12     |
+------------+------------+
|     12     |     13     |
+------------+------------+
|     16     |     4      |
+------------+------------+

- La variable var1 está asociada a la dirección 4 de la memoria.
- Considere que var1 es un entero de 4 bytes, por lo tanto var1 = 11.
- pvar1 es apuntador a variables de tipo entero de 4 bytes.
- pvar1 puede almacenar la dirección var1.
- pvar1 está asociada a la posición de memoria 16 y las direcciones son de 4 bytes.
- Si pvar1 apunta a var1, quiere decir que el contenido de la variable pvar1 (la posición 16 de memoria) es 4, ya que 4 es la dirección de var1.

**¿Cómo se declara un apuntador?**

Se utiliza el operador ``*``.

.. code-block:: rust

    let var1 = 11;
    
    let pvar1 : *mut i32;

Quiere decir que pvar1 es una variable que almacenará direcciones de variables de tipo i32.

+------------+------------+
|  Dirección |            |
+============+============+
|     0      |     10     |
+------------+------------+
|  4 (var1)  |     11     |
+------------+------------+
|     8      |     12     |
+------------+------------+
|     12     |     13     |
+------------+------------+
| 16 (pvar1) |     4      |
+------------+------------+


**¿Cómo se obtiene la dirección de una variable?**

Se utiliza el operador ``&``.

.. code-block:: rust

    let var1: i32 = 11;
    let var2: i32 = 12;

    let pvar1 : *const i32 = &var1;
    let pvar2 : *mut i32;

+------------+------------+
|  Dirección |            |
+============+============+
|     0      |     10     |
+------------+------------+
|  4 (var1)  |     11     |
+------------+------------+
|  8 (var2)  |     12     |
+------------+------------+
| 12 (pvar2) |     13     |
+------------+------------+
| 16 (pvar1) |     4      |
+------------+------------+

- ¿Cómo obtener la dirección de var2 y almacenarla en pvar2?
- ¿Cómo se almacena el contenido de pvar2 en pvar1?

|
| **¿Cómo leer y escribir el contenido de la dirección que está almacenada en el apuntador?**

.. code-block:: rust

    let x = 1;
    let y = 2;
    let px: *const i32;

    px = &x;

+------------+------------+
|  Dirección |            |
+============+============+
|     0      |            |
+------------+------------+
|**4** (var1)|     1      |
+------------+------------+
|  8 (var2)  |     2      |
+------------+------------+
| 12 (pvar2) |   **4**    |
+------------+------------+

**px almacena la dirección de x**

.. code-block:: rust

    let mut x = 1;
    let mut y = 2;
    let px;

    println!("x {} y {}", x, y);

    px = &mut x;
    *px = 0;

    y = *px;

    println!("y {} *px {}",y, *px);

+------------+------------+
|  Dirección |            |
+============+============+
|     0      |            |
+------------+------------+
|**4** (var1)|     1      |
+------------+------------+
|  8 (var2)  |     2      |
+------------+------------+
| 12 (pvar2) |   **4**    |
+------------+------------+

- ¿Cómo se podría almacenar en la posición de memoria 8 el valor almacenado en la posición de memoria 4 utilizando px?

.. code-block:: rust

    let mut x = 1;
    let px;

    px = &mut x;

+------------+------------+
|  Dirección |            |
+============+============+
|     0      |            |
+------------+------------+
|**4** (x)   |     0      |
+------------+------------+
|  8 (y)     |     0      |
+------------+------------+
| 12 (px)    |     4      |
+------------+------------+

.. code-block:: rust
    
    let mut x = 1;
    let px;

    px = &mut x;
    px = px + 1; //Ojo, no podemos sumar a un apuntador así porque si, esto es solo por el contexto del ejemplo.
    *px = 5;

+------------+------------+
|  Dirección |            |
+============+============+
|     0      |            |
+------------+------------+
|**4** (x)   |     1      |
+------------+------------+
|  8 (y)     |     5      |
+------------+------------+
| 12 (px)    |     8      |
+------------+------------+

- ¿Qué ocurre si ahora hacemos esto?

.. code-block:: rust

    px = px - 1;
    *px = 5;

------------------------

**Ejercicio**

Suponga que se tienen las siguientes instrucciones. Cuando se realizo la declaración de las variables se
asignaron las direcciones para cada variable tal y como se muestra en la figura. 
¿Cuáles son los valores finales de las variables después de la ejecución de las instrucciones?

.. image:: \../_static/guias/pointers_2.png

.. image:: \../_static/guias/pointers_1.png

---------------------

***Ejercicio**

.. image:: \../_static/guias/pointers_3.png

Queremos hacer una función que intercambie el contenido de dos variables.
Al ejecutar el programa anterior este es el resultado:

.. image:: \../_static/guias/pointers_3_result.png

¿Qué salió mal? En C los parámetros de una función se pasan por valor. 
Al llamar swap(x,y), se pasan en el stack los números 1 y 2.

- ¿Qué es el **stack**?
- El programa anterior al compilarse genera varios warnings ¿Qué dicen estos mensajes?

--------------------------------

.. image:: \../_static/guias/pointers_4.png

Al ejecutar el programa este es el resultado:

.. image:: \../_static/guias/pointers_4_result.png

El programa funciona correctamente. En este caso estamos pasando a swap la dirección de las variables x, y. 
A esto se le conoce como paso de parámetros por referencia.

-----------------------------------------------

.. image:: \../_static/guias/pointers_3_edit.png

.. image:: \../_static/guias/pointers_4_edit.png

Analice y compare los códigos en los cuales los llamados a
funciones fueron hechos por valor y por referencia y responda las
siguientes preguntas:

- ¿Por qué cuando se hace el llamado por referencia en la función se pasan los parámetros con ``&mut``?
- Suponga que en la línea 12 (del programa de más arriba) se introduce la siguiente instrucción

.. code-block:: rust

    let p = &mut y; 

La invocación (resaltada en el cuadro azul) se puede reemplazar por:

- a.swap(x,*p);
- b.swap(x,&p);
- c.swap(x,p);
- d.Ninguna de las anteriores.

----------------------------------

- Compile el código mostrado a continuación. Si este presenta errores corríjalos. Explique brevemente por que ocurren estos errores.
- Ejecute el programa, observe la salida y diga el por que se observa esta.

.. image:: \../_static/guias/pointers_5.png

Arreglos
^^^^^^^^^^^^

Ownership
^^^^^^^^^^^^

El concepto de Ownership es uno de los elementos que más se destacan en Rust, es lo que le permite a Rust
hacer un manejo seguro de la memoria sin utilizar garbage collector,