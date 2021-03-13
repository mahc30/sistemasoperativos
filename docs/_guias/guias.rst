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

Operadores
^^^^^^^^^^^^^^

Loops
^^^^^^^^^^^^^^

Funciones
^^^^^^^^^^^^

Ownership
^^^^^^^^^^^^^^