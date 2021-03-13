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
y la concurrencia, pero sin sacrificar el rendimiento. Con Rust podemos programar:

- WebAssembly
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

.. image:: \../_static/rust_intro/hello_world_codeblock.png
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

Tipos de Datos
^^^^^^^^^^^^^^^

Operadores
^^^^^^^^^^^^^^

Loops
^^^^^^^^^^^^^^

Funciones
^^^^^^^^^^^^

Ownership
^^^^^^^^^^^^^^