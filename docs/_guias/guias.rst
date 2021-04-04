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
|  4 (x)     |     0      |
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

Considere:

.. code-block:: rust
    
    fn main() {
        let vec : [i32; 4] = [1,2,3,4];
        let a = vec[0]; //a = 1
        let a = &vec; // a = 1
    }

+------------+------------+
|  Dirección |            |
+============+============+
| 0 (vec[0]) |     1      |
+------------+------------+
| 4 (vec[1]) |     2      |
+------------+------------+
| 8 (vec[2]) |     3      |
+------------+------------+
| 12 (vec[3])|     4      |
+------------+------------+

.. code-block:: rust
    
    fn main() {
        let vec : [i32; 4] = [1,20,30,40];
        let pvec = vec.as_ptr();

        unsafe{
            let a = *pvec.offset(1);
            let b = *pvec.add(1) + 1;
        }
    }

- En el programa anterior, ¿Cuál es el valor de las variables a y b?

.. code-block:: rust

    fn main()
    {

        let mut arr: [i32; 6] = [2,3,1,0,9,6];

        unsafe{

            let mut ptr1 : *mut i32;
    
            let ptr2 : *mut i32 = arr.as_mut_ptr().add(5);

            ptr1 = arr.as_ptr() as *mut i32; //Casteo explícito para indicar que el apuntador es variable
    
            ptr1 = ptr1.add(2);
    
            *ptr1 = 5;
    
            *ptr2.sub(1) = *ptr2.sub(1) - 1;

            *(ptr2) = *ptr1 + *(ptr2.offset(-1))
        }
    }

- ¿Cómo quedará el arreglo después de que se ejecutan las siguientes instrucciones?

.. note::
    
    En los dos ejemplos anteriores hicimos algo de **aritmética de punteros** con las funciones
    ``offset``, ``add`` y ``sub``. 
    
    Tanto en Rust como en C podemos manipular de forma libre, sin embargo, esto es muy propenso a errores y Rust no lo permite,
    por eso tuvimos que escribir nuestro código dentro del bloque ``unsafe {}``, debemos evitar usarlo
    lo más posible pues Rust nos da herramientas que nos permiten manipular la memoria de forma más segura. 
    En la sección de Memoria Dinámica estudiaremos mejor este tema.
    

**Alimento para el pensamiento 1**

Realice un programa que calcule el promedio de lo valores de un arreglo de 100 posiciones.

Nota: El programa debe generar el arreglo automáticamente y luego llamar una función que calcule el promedio.

Arreglos Multidimencionales
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Un arreglo multidimensional se puede entender como una arreglo de una dimensión cuyos elementos son arreglos.

¿Cómo se almacena el arreglo “numeros” en memoria si los char ocupan 4 bytes?

.. code-block:: rust

    let nombres : [[char; 10]; 3] = [['F','u','l','a','n','o', '\0', '\0', '\0', '\0'], ['M','e','n','g','a','n','o', '\0', '\0', '\0'], ['P','e','r','a','n','o', '\0', '\0', '\0', '\0']];

+------------+------------+-----------+-----------+
|            |            |           |           |
+============+============+===========+===========+
|     0      |     'F'    |     28    |     0     |
+------------+------------+-----------+-----------+
|     4      |     'u'    |     32    |     0     |
+------------+------------+-----------+-----------+
|     8      |     'l'    |     36    |     0     |
+------------+------------+-----------+-----------+
|     12     |     'a'    |     40    |    'M'    |
+------------+------------+-----------+-----------+
|     16     |     'n'    |     44    |    'e'    |
+------------+------------+-----------+-----------+
|     20     |     'o'    |     48    |    'n'    |
+------------+------------+-----------+-----------+
|     24     |      0     |     52    |    'g'    |
+------------+------------+-----------+-----------+

Memoria Dinámica
^^^^^^^^^^^^^^^^^^^^^^^^

Todos los programas tienen una forma de administrar la memoria mientras están corriendo, veamos algunos métodos que usan diferentes lenguajes
para manejar la memoria:

En algunos lenguajes, como C, el programador es el responsable de decirle al sistema cuando reservar y liberar memoria para guardar algún dato. 

- En lenguaje C las variables se puede asignar en memoria de tres formas: estáticamente, automáticamente (en el stack), dinámicamente (en el heap) (algunas se almacenan también en registros del procesador).

- El tamaño de las variables asignadas estáticamente y automáticamente se debe conocer en tiempo de compilación (antes del estándar C99).

- Si el tamaño de la variable únicamente puede ser conocido en tiempo de ejecución, la variable debe asignarse de manera dinámica en el heap.

.. image:: \../_static/guias/memoria_dinamica.png

También hay otros lenguajes en los que la forma en que se maneja la memoria es algo de lo que el programador usualmente no necesita
preocuparse, pues implementan algún mecanismo para manejar la memoria automáticamente como el `Garbage Collector <https://en.wikipedia.org/wiki/Garbage_collection_(computer_science)>`__.
Que busca y libera memoria ocupada por objetos que el programa ya no usa.

Rust tiene otro acercamiento al manejo de la memoria, **Ownership**. El concepto de Ownership es uno de los elementos que más se destacan en Rust,
todo lo que requiere es hacer unas verificaciones en tiempo de compilación para 
permitirle al lenguaje hacer un manejo seguro de la memoria sin sacrificar rendimiento en tiempo de ejecución.

Ownership
^^^^^^^^^^^^
Las reglas de **Ownership** son:

- Cada valor en Rust tiene una variable a la que llamaremos *Owner*.
- Solo puede existir un Owner a la vez.
- Cuando el Owner sale del *Scope*, el valor es eliminado.

El *Scope* es el rango dentro de un programa dentro del que un objeto es válido, digamos que tenemos una variable:

.. code-block:: rust

    let s = "Hello";

La variable s es un string que es válido desde que es declarado hasta el final de su scope actual.

.. code-block:: rust

    { //La variable s no ha sido declarada y no es válida
        let s = "Hello"; //La variable s es declarada y es válida dentro de este scope
        ...
    } //El scope se termina y s ya no es válida

Hasta el momento es muy común a la forma en que funcionan muchos de los otros lenguajes. 
Esta forma de declarar literales es bastante conveniente y fácil de utilizar, pero tienen
un pequeño problema, son inmutables, ¿Qué haríamos si quisieramos almacenar una cadena que escriba el usuario?

Para esto tendremos que usar estructuras más complejas que las que hemos visto hasta el momento, como ``String``, 
que es un tipo que se asigna o guarda en el heap y por eso puede guardar datos que conoceremos solo en tiempo de ejecución.

.. code-block:: rust

    let mut s = String::from("hello");

    s.push_str(", world!"); // push_str() appends a literal to a String

    println!("{}", s); // This will print `hello, world!`

¿Porqué este String si es mutable y los literales no? La diferencia está en la implementación de cómo
estos dos tipos manejan la memoria.

Cómo para los literales ya conocemos el valor en tiempo de compilación, sus valores simplemente son quemados
o *hardcoded* en el ejecutable final, esto solo es posible porque ya sabemos cuál es su tamaño y cuanto espacio
necesitan en memoria antes de la ejecución del programa.

Para que el tipo ``String`` pueda almacenar una cantidad variable de texto, necesitamos pedirle al sistema una cierta
cantidad de memoria, desconocida al momento de compilar, para guardar estos datos. Esto significa que:

- El espacio en memoria debe ser pedido al sistema en tiempo de ejecución.
- Se necesita una manera de devolverle al sistema esa memoria cuando ya no se necesite.

Lo primero se logra cuando llamamos al ``String::from``, que en su implementación pide la memoria que necesita.

Para lo segundo, Rust devuelve automáticamente la memoria al sistema cuando la variable que la contiene
sale del scope.

Veamos el siguiente ejemplo:

.. code-block:: rust

    fn main() {
        let s1 = String::from("hello");
        let s2 = s1;
    }

El código anterior puede parecer bastante simple, ``s1`` es un string y ``s2`` hace una copia 
del valor de s1 y lo asigna a s2. ¿Pero si es esto lo que sucede?

Veamos cómo funciona un ``String``. Este tipo está formado por 3 partes:

- Un apuntador a la memoria que lo contiene
- *lenght*: cuanta memoria está usando este String en un momento dado.
- *capacity*: la cantidad de memoria total que ha recibido del sistema.

.. image:: \../_static/guias/string_1.svg
    :width: 800

Cuando nosotros asignamos ``s1`` a ``s2``, copiamos la información del String, es decir,
copiamos el apuntador, lenght y capacity que está en el **stack**, no la cadena de texto
que se encuentra en el **heap**.

Visualmente podemos verlo así:

``s2`` hace una copia del apuntador, length y capacity de ``s1``

.. image:: \../_static/guias/string_2.svg
    :width: 800

Esto puede ser un problema, pues cuando ambas variables salgan del scope Rust intentará
liberar la memoria de sus apuntadores, pero cómo ambas variables apuntan a la misma dirección
de memoria, tendremos un bug de *double free* que puede corromper el estado del administrador
de memoria del sistema.

Para esto Rust lo que hace es que *"mueve"* la variable ``s1`` a ``s2``, esto quiere decir
que la variable s1 queda invalidada y solo se podra acceder a esta información por medio de 
s2.

Intenta correr el siguiente código:

.. code-block:: rust

    let s1 = String::from("hello");
    let s2 = s1;

    println!("{}, world!", s1);

- ¿Porqué no funcionó?

Para solucionar este problema le debemos indicar explícitamente 
a s2 que **clone** la información del heap a la que apunta s1.

.. code-block:: rust

    let s1 = String::from("hello");
    let s2 = s1.clone();

    println!("s1 = {}, s2 = {}", s1, s2);

.. image:: \../_static/guias/string_3.svg
    :width: 800

En resumen, los valores de los datos guardados en el stack ya los conocemos en
tiempo de compilación y por lo tanto hacer copias de los valores es más fácil y rápido, por otro lado,
cuando tenemos datos guardados en el heap, clonar los valores para una nueva variable puede ser bastante 
costoso y riesgoso, por esta razón es más eficiente **mover** (así se le llama en Rust) los valores (apuntador, length, capacity) 
a la nueva variable, pues son datos que podemos encontrar en el stack.

Todos los ejemplos de esta sección fueron tomados y adaptados de https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html

**Alimento para el pensamiento 3**

Ejecuta el siguiente código y responde a las preguntas:

.. code-block:: rust

    fn main() {
        let s1 = String::from("¿Había mencionado que en Rust los emojis son caracteres válidos 👁️ 👄👁️ ?");

        print_string(s1);

        println!("s1 = {}", s1);
    }

    fn print_string(my_string: String){
        println!("my string: {}", my_string);
    }

- ¿Qué mensaje se imprime en la consola? ¿Porqué ocurre esto?
- ¿Quien tiene el ownership de s1 antes de invocar la función **print_string()**?
- ¿Quien tiene el ownership de s1 después de invocar la función **print_string()**?
- ¿Dónde se libera la memoria asignada a s1?
- Elimine el llamado a println!() que está dentro de main y vuelva a probar el código
- ¿Porqué no podíamos volver a imprimir s1 dentro de **main** después de imprimirlo usando la función **print_string()**?

Estructuras de Datos
^^^^^^^^^^^^^^^^^^^^^^^^

Una estructura es una colección de una o más
variables, estas variables pueden ser de tipos
diferentes, agrupadas bajo un mismo nombre para
facilitar su manejo.

**Ejemplo: ¿Cómo se declara una estructura?**

Quiero crear una colección (estructura) que me permita agrupar dos enteros. 
Los enteros son las coordenadas de un punto en el espacio.

.. image:: \../_static/guias/structs_1.png


.. code-block::rust

    struct Point {
    x: u32,
    y: u32
    }

¿La definición anterior de la estructura Point ocupa espacio en memoria?


Definición de variables del tipo de la estructura e inicialización
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block::rust

    //Diferentes formas de declarar e instanciar estructuras
    let (pt1, pt2) : (Point, Point);
    
    let pt3 : Point = Point{
        x : 4,
        y : 2
    };

    pt1 = Point{
        x : 5,
        y : 6 
   };
    
   pt2 = Point{
       x: 2,
       y: 7
   };

- pt1 y pt2 son dos variables de tipo Point.
- Si los enteros ocupan 2 bytes, el procesador puede direccionar
cada byte, y el endian del procesador es BIG:

+------------+------------+
| Dirección  | Contenido  |
+============+============+
| 0 (pt1.xH) |     0      |
+------------+------------+
| 1 (pt1.xL) |     5      |
+------------+------------+
| 2 (pt1.yH) |     0      |
+------------+------------+
| 3 (pt1.yL) |     6      |
+------------+------------+
| 4 (pt2.xH) |     0      |
+------------+------------+
| 5 (pt2.xL) |     2      |
+------------+------------+
| 6 (pt2.yH) |     0      |
+------------+------------+
| 7 (pt2.yL) |     7      |
+------------+------------+

¿Qué es el endian de un procesador?

**Cree una variable de tipo cdsMusica e inicialice cada uno de sus miembros:**
- Titulo: Brindo con el alma.
- Artista: Diomedes Díaz.
- Genero: Vallenato.
- numCanciones: 11
- Lanzamiento: 1986
- Precio: 19900

Estructuras: ¿Cómo acceder a los miembros de una estructura?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Por medio del operador punto**

.. code-block::rust

    println!("pt1: ({},{})\npt2: ({},{})\npt3: ({},{})", pt1.x, pt1.y, pt2.x, pt2.y, pt3.x, pt3.y);

**Cree un programa que imprima los miembros de la variable cdsMusica del punto anterior.**

Estructuras: anidando estructuras
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

De nuevo considera el ejemplo de los puntos.

.. code-block::rust

    struct Point {
    x: u32,
    y: u32
    }

    struct Rect {
    pt1 : Point,
    pt2 : Point
    }

.. image:: \../_static/guias/structs_2.png

**Analizar este programa**

.. code-block:: rust

    struct Estudiante{
        nombre: String,
        numEstudiante: i32,
        agnoMatricula: u32,
        nota: f32
    }

    fn main() {
    
        let estud1 = Estudiante{
            nombre: String::from("Jose"),
            numEstudiante: 4,
            agnoMatricula: 2009,
            nota: 4.5
        };

        let ptrEstruct : *const Estudiante;

        ptrEstruct  = &estud1;

        unsafe{
            println!("La nota de estud1 es: {} (Con Apuntador)", (*ptrEstruct).nota);
        }

        println!("La nota de estud1 es: {} (Sin Apuntador)", estud1.nota);
    }

ptrEstruct es una variable que puede almacenar la dirección
(apuntador) en memoria de una estructura de tipo estudiante.

Para acceder a los miembros de la estructura a través del
apuntador también usamos el **operador punto**, sin embargo es necesario
usar el **operador de desreferencia**, que nos permite acceder al valor
contenido en la dirección a la que apunta **ptrEstruct**.

- Elimina el bloque **unsafe** e intenta compilarlo. ¿Qué mensaje arroja el compilador?

*Recuerda que cuando programamos en Rust debemos tratar de evitar usar* **Raw Pointers**
*siempre que sea posible pues no son seguros. Rust nos da muchas herramientas para acceder a la memoria de forma segura*

Vuelve a agregar el **unsafe** que eliminaste en el punto anterior para hacer los siguientes puntos:

- Complete este programa para que imprima el contenido de los demás miembros del arreglo.
- Adicione una función al programa que permita actualizar los miembros de la estructura estud1 si se
presiona la tecla r. Imprima de nuevo los valores de los miembros de la estructura.

Archivos
^^^^^^^^^^^

Para poder realizar operaciones de entrada/salida
(leer/escribir) un archivo en Rust es necesario ABRIRLO
primero.

Abra la consola y ejecute los siguientes comandos:

.. code-block:: bash

    echo "hola mundo" > input.txt

    cat input.txt

    hexdump –C input.txt

**¿Cuántos caracteres tiene el archivo?**