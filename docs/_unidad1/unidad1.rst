Unidad 1: Rust
=======================

Introducción
--------------

Para poder abordar el curso de sistemas operativos con un enfoque
práctico necesitamos aprender un nuevo lenguaje de programación
llamado Rust. Este lenguaje resulta muy apropiado para nuestros
propósitos por su gran cercanía con los conceptos que estudiaremos.

Rust es un lenguaje fácil de aprender y muy poderoso. En pocas semanas
estarás programando en este lenguaje.

Propósito de aprendizaje
^^^^^^^^^^^^^^^^^^^^^^^^^^

Aplicar el lenguaje de programación Rust en la solución de problemas
simples haciendo uso de variables, estructuras de control, punteros,
estructuras de datos, funciones y archivo.


Trayecto de actividades
------------------------

Ejercicio 1: Entorno de Trabajo
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Para poder trabajar en los ejercicios vas
a necesitar un ambiente de trabajo. Te propongo que instales en una USB o en una
partición de tu computador el sistema operativo Linux. Te 
preguntarás si puedes instalarlo en una máquina virtual.
Lo puedes hacer pero usualmente no lo recomiendo porque la
experiencia de uso no resulta agradable si tu sistema es muy lento.

Vas a necesitar dos memorias USB. Una grande (> 16GB), donde instalarás tu sistema operativo
y otra más pequeña (8GB) donde grabaras el instalador. Trata de utilizar la USB más rápida y
más grande para instalar tu sistema operativo.

Te voy a dejar unos videos de ayuda:

* Este `video <https://www.youtube.com/watch?v=zSGZe8NSEAc>`__ 
  te muestra como grabar en la USB pequeña el instalador. En este caso la distribución es PopOS,
  es la misma que yo uso; sin embargo, puedes grabar la que más te guste, por ejemplo Ubuntu.
  Ten presente que la versión del video no será la última. También, debes investigar
  cómo entrar al menú de configuración de tu BIOS para que ajustes el orden de boot. 
  Nota que debes darle prioridad a la USB para que al tenerle conectada arranques el 
  instalador del sistema operativo.

* Ahora, este video `video <https://www.youtube.com/watch?v=RR9Vgytjj24>`__ te mostrará
  cómo instalar, usando la USB pequeña con el instalador, tu sistema operativo en la USB grande.
  Te recomiendo iniciar a ver el video en el minuto 6:29, donde comienza en si el proceso
  de instalación. Una vez termines de instalar Linux en la USB grande, NO OLVIDES desconectar la USB
  pequeña para que tu computador inicie con la versión instalada de Linux en la USB grande.


Ejercicio 2: Herramientas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Antes que nada, en la terminal ejecuta los comandos:

.. code-block:: bash

    $ sudo apt update
    $ sudo apt upgrade

Para programar en Rust recomiendo instalar:

#. Eclipse
#. Visual Studio Code
#. Extensión de Rust en Visual Studio Code
#. Rustup

Eclipse te permitirá tener un depurador visual de código, pero la verdad
es un poco lento. Visual Studio Code, no tiene un depurador visual tan rico, pero es
muy liviano. Yo uso ambos. Normalmente trabajo con Visual Studio Code y cuando
algo no me funciona lo pruebo con Eclipse.

En Visual Studio Code podemos instalar la extensión de Rust, nos ayudará a programar en Rust
con snippets, autocompletado y muchas otras funciones.

.. image:: \../_static/unidad_1/rust_vscode_extension.png

Rustup es un instalador de Rust y administrador de paquetes, para instalarlo en Linux
puedes correr el siguiente comando en la terminal:

.. code-block:: bash

    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

*Elegimos la instalación por defecto,* 1

.. image:: \../_static/unidad_1/rust_default_install.png
   :width: 400pt

También necesitaremos instalar cargo.

.. code-block:: bash

    apt install cargo

Cargo es un administrador de paquetes que nos permitirá
instalar librerías, en Rust las librerías son llamadas *crates.*

Para comprobar que Rust y Cargo fueron instalados correctamente podemos usar el siguiente comando:

.. code-block:: bash

    rustc --version

.. code-block:: bash

    cargo --version

Ejercicio 3: línea de comandos
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Explorando un poco más la línea de comandos, disponible en casi todos los sistemas operativos. 
Para ello te propongo realizar la siguiente `guía <https://drive.google.com/open?id=11tTtbCuVjYcBBYPrULbCeb0PABJLyhGEtzRGKMRG5u0>`__.


Ejercicio 4: lenguaje de programación Rust
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

En esta unidad vamos a aprender un nuevo lenguaje de programación, es simple 
pero muy poderoso. En este :doc:`enlace <../_guias/guias>` 
encontrarás una guía básica de Rust.

Ejercicio 5: Strings en Rust
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

En Rust los strings son una colección de bytes, cuando hablamos de Strings
nos referimos tanto al objeto String cómo al slice ``&str``, que son referencias
a strings UTF-8 guardadas en alguna parte de la memoria.

Muchas de las operaciones que el tipo ``Vec`` implementa también están presentes en la clase ``String``.

.. code-block:: rust

    //Inicializar String
    let mut myString = String::new();

    //Inicializar String desde un literal
    let mut s1 = "esto es un literal".to_string();
    let mut s2 = String::from(" y esta es otra forma de hacer lo mismo");

    //Modificar String
    s1.push(s2);
    //"Esto es un literal y esta es otra forma de hacer lo mismo"

    //Concatenar varios strings
    let mut s3 = String::from("Hola");
    let mut s4 = String::from("Mundo");
    let mut s5 = format!("{} {}", s3, s4);

    
Ejercicio 6: Indexando Strings
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

En C los Strings eran usados como arreglos de caracteres y referencias, por ejemplo:

.. code-block:: c

    char nombres[3][20] = {"fulano","mengano","perano"};

``nombres`` es un arreglo de arreglos, es decir, un arreglo de 3 arreglos de 20 caracteres cada uno.
Por lo que es posible acceder a cada uno de los caracteres con un índice.

.. code-block:: c

    printf("%c", nombres[2][1]);
    //e

Pero en Rust no es posible por la forma en que está implementada la clase. String es un *Wrapper* para un ``Vec<u8>``. 
Veamos ejemplos de strings codificadas en formato `UTF-8 <https://es.wikipedia.org/wiki/UTF-8>`__
Ejemplos tomados del `libro oficial de Rust <https://doc.rust-lang.org/nightly/book/ch08-02-strings.html>`__

.. code-block:: rust

    let hello = String::from("Hola");

En este caso ``hello.len()`` es 4, lo que significa que el vector almacenando "Hola" tiene 4 bytes de largo.
Porque cada una de estas letras toma 1 byte cuando están codificadas en UTF-8.

.. code-block:: rust

    let hello = String::from("Здравствуйте");
    

Ahora, si bien parece que son 12 caracteres, ``len()`` es 24, porque 24 son los bytes que se necesitan para
codificar "Здравствуйте" en UTF-8, porque cada valor escalar en este String toma 2 bytes de almacenamiento.

Es por esto que indexar los strings puede hacer referencia a un valor escalar Unicode inválido.

.. code-block:: rust

    let hello = String::from("Здравствуйте");
    let hello = "Здравствуйте";
    let answer = &hello[0];


¿Cuál debería ser el valor de ``answer``? ¿Debería  ser ``З``, la primera letra?
Cuando los Strings están codificados en UTF-8, el primer byte de ``З`` es ``208`` y el segundo es ``151``,
por lo tanto la respuesta sería ``208``, pero ``208`` no es un caracter válido por si mismo. Retornar el ``208``
no es lo que espera el usuario, pero es toda la información que tenemos disponible en ``&hello[0]``

Ejercicio 7
^^^^^^^^^^^^^^

Rust ofrece muchos métodos para manipular strings sin tener que recurrir a apuntadores y bytes.

Por ejemplo para iterar sobre caracteres individuales unicode podemos usar el método ``chars()`` que retorna
valores de tipo char que pueden ser iterados.

.. code-block:: rust

    for c in "नमस्ते".chars() {
        println!("{}", c);
    }

Retorna

न
म
स
्
त
े

Ejercicio 8
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

En la guía introductoria del lenguaje Rust vimos un ejemplo de
una representación de cómo se guardan los strings en memoria.

En el ejemplo declaramos los strings como arreglos de caracteres

.. code-block:: rust

    let nombres : [[char; 10]; 3] = [['F','u','l','a','n','o', '\0', '\0', '\0', '\0'], ['M','e','n','g','a','n','o', '\0', '\0', '\0'], ['P','e','r','a','n','o', '\0', '\0', '\0', '\0']];

Más adelante vimos que Rust tenía métodos más fáciles y seguros para instanciar y manejar Strings,
en los siguientes ejercicios vamos a ver otros métodos que son muy útiles para trabajar con Strings.

Al introducir texto en la terminal, además de los caracteres visibles, se introduce un ENTER.
Así, por ejemplo, al introducir el número 325 y luego presionar
ENTER, se están ingresando 4 bytes: 0x33 0x32 0x35 0x0A. los
tres primeros bytes corresponden a los códigos ASCII de cada dígito
del número 325 y el 0x0A corresponde al código ASCII del ENTER
o nueva línea (NEW LINE).

Considere el siguiente código:

.. code-block:: rust

    use std::io;

    fn main() {

        let mut input : String = String::new();
        let num: i64;
        let key: char;
        let mut num_bytes: usize;

        println!("Ingrese el numero 325 y presione ENTER:\n");

        num_bytes = io::stdin().read_line(&mut input).expect("Failed to read");
        num = input.trim().parse().expect("El texto ingresado no es un número");

        println!("Se leyeron: {} bytes\nnum: {}", num_bytes, num);
    
        print!("Ingrese cualquier tecla para terminar y presione ENTER:\n");
        input = String::new();

        num_bytes = io::stdin().read_line(&mut input).expect("Failed to read");
        key = input.chars().next().expect("No se pudo leer el caracter");

        println!("num_bytes: {}\nkey: {}", num_bytes, key);
    }

Ejecuta el código anterior. ¿Cuál es el resultado? ¿Por qué?

El primer read_line (``io::stdin().read_line(&mut input).expect("Failed to read");``) buscará en el flujo de entrada una
secuencia de bytes (cadena de texto) y parará de leer una vez detecte un carácter NEWLINE (0xA) o EOF.
En este caso ``io::stdin().read_line(&mut input).expect("Failed to read");`` copiará en nuestro buffer ``input`` 
los bytes 0x33 0x32 0x35, correspondientes a ``'3'`` ``'2'`` ``'5'``, e incluirá el byte 0x0A (correspondiente al ENTER). 

Luego usando las funciones de la clase String, ``input.trim().parse().expect("El texto ingresado no es un número");``
convertirá la cadena de 3 bytes en ASCII al número que representan, es decir,
al 325 que en base 16 sería 0x0145 (comprueba esto con la calculadora del sistema operativo).

Gracias a la inferencia de tipos, Rust sabe que estamos intentando convertir el String almacenado en ``input`` a 
un número entero, porque estamos asignando el valor que retorna ``parse()`` a la variable ``num`` que al comienzo
del programa fue declarada como ``i64``.

Antes de volver a leer el flujo, es necesario limpiar la variable en la que estamos almacenando el input del usuario, si no tenemos otra,
para esto usamos ``String::new()`` para asignar el nuevo valor a nuestra variable ``input``.

El segundo scanf ``io::stdin().read_line(&mut input).expect("Failed to read");`` leerá de nuevo el flujo de entrada, pero
en este caso solo queremos obtener el primer caracter de este flujo, para esto podemos invocar al método ``chars()`` para
obtener un iterador del string, y luego al método ``next()`` del iterador para obtener el primer elemento del iterador, o en este caso, del String.

- ¿Qué es el **newline character**?
- ¿Qué hace la función ``trim()``?

Ejercicio 9: I/O
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Crea una función que reciba un apuntador a una variable tipo String y guarde el input del usuario en la dirección de esa variable

.. raw:: html

    <details>
    <summary> <strong>Spoiler</strong> una solución al problema puede ser: </summary>
 
.. code-block:: rust

    fn read_user_input(buffer: &mut String) {
        buffer.clear();
        io::stdin().read_line(buffer).expect("Failed to read_user_input");
    }

.. raw:: html

   </details>

|

Ejercicio 10: Parsing
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Vamos a continuar con el código del ejemplo anterior, agrega a tu código las siguientes modificaciones:

.. code-block:: rust

    fn main() {

        let mut input : String = String::new();
        let num: i64;
        let key: char;
        let mut num_bytes: usize;

        println!("Ingrese el numero 325 y presione ENTER:\n");

        num_bytes = io::stdin().read_line(&mut input).expect("Failed to read");
        num = input.trim().parse().expect("El texto ingresado no es un número");

        println!("Se leyeron: {} bytes\nnum: {}\nnum to Hex {:#X}", num_bytes, num, num);

        let buffer: Vec<u8> = input.as_bytes().to_vec();

        for i in 0..buffer.capacity(){
            println!("{:#X}", buffer[i]);
        }

        print!("Ingrese cualquier tecla para terminar y presione ENTER:\n");
        input = String::new();

        num_bytes = io::stdin().read_line(&mut input).expect("Failed to read");
        key = input.chars().next().expect("No se pudo leer el caracter");
        println!("num_bytes: {}\nkey: {}", num_bytes, key);


        let key_to_hex = key as u32; //Casteo Explícito

    
        println!("{} Key to Hex {:#X}", key, key_to_hex); 
    }

Presta atención al primer ``println!()``, en las guías hablamos de los ``{}`` eran reemplazados por los demás
argumentos que pasabamos a la función, pero también podemos agregarles `Formatting Traits <https://doc.rust-lang.org/std/fmt/#formatting-traits>`__,
para indicar que un argumento tiene cierto formato. Para el caso de ``{:#X}``, ``#`` significa que queremos imprimir el
**0x** al comienzo del hexadecimal y ``X`` es Hexadecimales en mayúscula (A,B,C,...,F).

Ejecuta el código anterior y responde:

- ¿El valor hexadecimal del 325 si concuerda con el de la explicación del punto anterior?
- ¿Cuál es el valor hexadecimal de la letra 'a'? ¿y de 'A'?
- Cuando aparezca el mensaje de "Ingrese cualquier tecla para terminar" intenta ingresar los siguientes valores
- ENTER 
- A
- Á
- 🐧
- ¿Qué valores en hexadecimal tienen? ¿Cuántos bytes fueron leídos en cada caso?

Ejercicio 11
^^^^^^^^^^^^^

- ¿Qué ocurre si cuando nos pida ingresar un número ingresamos una palabra?
- ¿Qué ocurre si solo presionamos ENTER?
- Modifica el programa anterior para que el programa no se detenga en caso de que el input del usuario no sea válido.

.. raw:: html

    <details>
    <summary> <strong>Spoiler</strong> una solución al problema puede ser: </summary>
 
.. image:: \../_static/unidad_1/user_input_loop.png

.. raw:: html

   </details>

|

Ejercicio 12: Pattern Matching
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Otra expresión nueva que usamos en la guía fue ``match`` para codificar manejo de errores cuando leemos
input del usuario, pero esta expresión tiene muchos más usos, analiza el siguiente programa:

.. image:: \../_static/unidad_1/pattern_matching_char.png

- ¿Qué hace el programa?
- Modifica el programa para que la variable op sea un valor asignado por el usuario y prueba ingresando los caracteres `+` `-` `*` `/` `a`.
- ¿Cuáles son los resultados?

Ejercicio 13
^^^^^^^^^^^^^^

Las expresiones ``match`` consisten de un **value**, y varios **arms** con patrones y expresiones para 
ser ejecutadas en caso de que el **value** sea el mismo que el del patrón. 

.. code-block:: rust

    match VALUE {
        PATTERN => EXPRESSION,
        PATTERN => EXPRESSION,
        PATTERN => EXPRESSION,
    }

*Tomado del* `*libro oficial de Rust* <https://doc.rust-lang.org/book/ch18-01-all-the-places-for-patterns.html>`__.

- Haz un programa que lea un número del usuario y que imprima "Es positivo" si es mayor o igual a cero y "Es negativo" menor que 0

.. raw:: html

    <details>
    <summary> <strong>Spoiler</strong> una solución al problema puede ser: </summary>
 
.. image:: \../_static/unidad_1/pattern_matching_fn.png

.. raw:: html

   </details>

|

Ejercicio 14: Wildcard Pattern
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Usar ``_`` como patrón es usado para ignorar valores que no nos interesan o que no coinciden con alguno de los patrones
de los arms. En la imagen del ejercicio 9 puedes ver que lo usamos para indicar qué comportamiento tendrá el programa en caso
de que el caracter ĺeido no sea alguna de las operaciones indicadas.

- Haz un programa que con solo un ``match`` imprima "Es positivo", "Es negativo" o "Es cero" según sea el caso.

Ejercicio 15
^^^^^^^^^^^^^^

Programa una calculadora que permita sumar, restar, dividir o multiplicar dos números. El usuario debe poder
terminar el programa escribiendo 'N' o 'n'. 

Ejercicio 16: Arreglos y Punteros
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

(Este ejercicio es adaptado de `aquí <https://www.geeksforgeeks.org/pointer-array-array-pointer/>`__)

Relación arreglos y punteros

.. code-block:: rust
    :linenos:

    unsafe {
        let mut arr: [i32; 5] = [0;5];
        let mut p: *mut i32;
        let mut ptr : *mut [i32;5];

        p = arr.as_mut_ptr();
        ptr = &mut arr;

        println!("p = {:p}, ptr = {:p}", p, ptr);

        p = p.add(1);
        ptr = ptr.add(1);
        println!("p = {:p}, ptr = {:p}", p, ptr);
    }

Ejecuta el programa anterior. El resultados es:

.. code-block:: c
    :linenos:
    
    p = 0x7fff4f32fd50, ptr = 0x7fff4f32fd50
    p = 0x7fff4f32fd54, ptr = 0x7fff4f32fd64


En la expresión ``let mut p: *mut i32;`` p es una variable de tipo
``i32 *``. En este tipo de variables se almacenan las
``direcciones`` de variables de tipo ``i32``. Por tanto, ``*p``
(sin colocar i32 antes del ``*``) es de tipo ``i32`` porque 
p es de tipo ``i32 *``.

En la expresión ``let mut ptr : *mut [i32;5];`` ptr es una variable de tipo
``* [i32;5]``. En este tipo de variables se almacenan direcciones
de variables de tipo ``[i32;5]``, es decir, variables de tipo
arreglo de cinco posiciones. Por tanto, ``*ptr`` es de tipo 
``[i32;5]`` porque ptr es de tipo ``i32 (*)[5]``.

En la expresión ``p = arr.as_mut_ptr();`` arr es el nombre del arreglo y un puntero
al primer elemento del arreglo.
En este caso `arr` es de tipo ``i32 *`` porque el primer elemento
del arreglo es de tipo ``i32``. Por tanto, ``*arr`` 
será tipo ``i32``.

En la expresión ``ptr = &arr;`` ``&arr`` es la dirección del arreglo.
``&arr`` es tipo ``i32 (*)[5]``.

La expresión ``println!("p = {:p}, ptr = {:p}", p, ptr);`` imprime el
contenido de p y ptr. Según el resultado
``(p = 0x7fff4f32fd50, ptr = 0x7fff4f32fd50`)``, la dirección del
arreglo y del primer elemento del arreglo es la misma; sin embargo,
como p es tipo ``i32 *``, la expresión ``p.add(1);`` hará que p apunte
(almacene la dirección) al siguiente entero. En cambio, en la
expresión ``ptr.add(1);`` ptr apuntará al siguiente arreglo de 5
enteros (5 enteros ocupan 20 bytes en memoria considerando
que cada entero ocupa 4 bytes), ya que ptr es de tipo
``i32 (*)[5]``.

Ejercicio 17: Análisis de una expresión más compleja
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

El siguiente ejercicio es más complejo que el anterior, sin embargo,
se analiza de igual manera. Considera el siguiente código:

.. code-block:: rust
    :linenos:

    unsafe{
        let arr: [[i32;4];3] = [ [1,2,3,4], [5,6,7,8], [9,10,11,12]];
    
        let p: *const [[i32;4];3] = &arr;
    
        println!("{}", ((*p)[2])[3]);
        println!("{}",  *(*(*p).as_ptr().offset(2)).as_ptr().offset(3));
    }


``arr`` es un arreglo de arreglos, es decir, es un arreglo de 3 arreglos
de 4 enteros cada uno.

``arr`` es el nombre del arreglo de arreglos y un puntero al primer elemento
del arreglo. Por tanto, ``arr`` es de tipo ``i32 (*)[4]`` ya que el primer elemento
de arr es un arreglo de tipo ``i32 [4]``.

``p`` es un puntero que almacena la dirección de un arreglo de arreglos.
Por tanto, p es de tipo ``i32 (*)[3][4]``.

Si ``p`` es de tipo ``i32 (*)[3][4]`` entonces ``*p`` será de tipo ``i32 [3][4]`` o
``i32 (*)[4]`` (un puntero al primer elemento del arreglo de arreglos).

El operador ``[]`` en la expresión ``(*p)[2]`` es equivalente a ``*( *p.offset(2))``.
Como el tipo de ``(*p.offset(2))`` es ``i32 (*)[4]`` el tipo de ``*( *p.offset(2))``
será ``i32 [4]``. la expresión ``(*p)[2]`` accede al tercer elemento de arr, es
decir, a ``{9,10,11,12}`` que es de tipo ``i32 [4]``.

Por último, como ``(*p)[2]`` es tipo ``i32[4]``, entonces ``( (*p)[2] )[3] )`` es
tipo i32 y corresponderá al cuarto elemento del tercer arreglo de arr.

Nota que ``( (*p)[2] )[3] )`` es equivalente a ``*( (*p)[2] + 3)`` que a su
vez es equivalente a  ``*( * ( *p.offset(2)).as_ptr().offset(3))``

El programa imprimirá el número ``12``.

La expresión ``println!("{}",  *(*(*p).as_ptr().offset(2)).as_ptr().offset(3));`` al ser equivalente a
``println!("{}", ((*p)[2])[3]);`` también mostrará un ``12``.


Ejercicio 18
^^^^^^^^^^^^^

Te propongo que realices un programa que:

* Solicite el tamaño de un arreglo.
* Solicite uno por uno sus elementos.
* Realiza una función para imprimir el contenido del arreglo. A esta
  función deberás pasar la dirección del arreglo y el tamaño.
* Solicite insertar un nuevo elemento en el
  arreglo mediante la selección de la posición deseada. La posición
  será un número de 1 hasta en el tamaño del arreglo.

Trata de PENSARLE UNOS MINUTOS. Más abajo está la solución.

.. note::
    ¡Alerta de Spoiler!

El siguiente código muestra una posible solución:

.. code-block:: rust
   :linenos:

    use std::io;

	fn read_user_input(buffer: &mut String) {
 	   buffer.clear();
 	   io::stdin().read_line(buffer).expect("Failed to read_user_input");
	}

	fn print_array(arr: &mut Vec<i32>){
   	 for i in 0..arr.len(){
  	      println!("data[{}] = {}", i, arr[i]);
  	  }
	}

	fn main() {
    
   	 let mut buffer = String::new();
    
    	println!("Escriba el tamaño del arreglo");
    	read_user_input(&mut buffer);
    
   	 let n : usize = buffer.trim().parse().unwrap();
   	 let mut data : Vec<i32> = Vec::with_capacity(n);
    
   	 for i in 0..n {
    
      	  println!("Escriba el elemento {}", i);
      	  read_user_input(&mut buffer);
        
    	    let elem : i32 = buffer.trim().parse().unwrap();
    	    data.push(elem);
   	 }
        print_array(&mut data);
    
  	 println!("Ingrese la posición donde quiere insertar");
  	 read_user_input(&mut buffer);
 	 let mut position : usize = buffer.trim().parse().unwrap();
 	 position = position - 1;
    
      data.push(0); //El vector necesita un nuevo espacio para mover los dato antes de la inserción
  
 	 for i in (position..data.len() - 1).rev() {
  	    data[i+1] = data[i];
  	}
  
 	 println!("Ingrese el valor a insertar");
 	 read_user_input(&mut buffer);

 	 data[position] = buffer.trim().parse().unwrap();

	 print_array(&mut data);
	}

Ejercicio 19
^^^^^^^^^^^^^^

Analiza con detenimiento el siguiente ejemplo:

* Utiliza el *debugger* de eclipse.
* Agrega un breakpoint para que el programa pare antes de terminar.
* En la pestaña de variables como se muestra en la imagen de más abajo haz click derecho sobre una de las posiciones de la variable nombres y selecciona "View Memory".
* Mira cómo se guardan las cadenas en memoria.

.. code-block:: rust

    let nombres : [[char; 10]; 3] = [['F','u','l','a','n','o', '\0', '\0', '\0', '\0'], ['M','e','n','g','a','n','o', '\0', '\0', '\0'], ['P','e','r','a','n','o', '\0', '\0', '\0', '\0']];


.. image:: \../_static/unidad_1/vista_memoria.png

Ejercicio 20
^^^^^^^^^^^^^^^^

Repasa el manejo de archivos y la gestión de errores. 
Lee esta información:

* `¿Cómo vamos a gestionar los errores en Rust? <https://doc.rust-lang.org/nightly/book/ch09-02-recoverable-errors-with-result.html>`__

Ejercicio 21
^^^^^^^^^^^^^

Escribe una función que te permita encontrar los elementos comunes de
dos arreglos de enteros. El encabezado de la función es:

.. code-block:: c
   :linenos:

    fn arrayCommon(arr1: &mut [i32], arr2: &mut [i32], arrRes: &mut [i32])

* La función debe recibir las direcciones de memoria de los dos arreglos
  a comparar y del arreglo resultado. También debe recibir el tamaño de
  cada arreglo.
* Debe devolver la cantidad de elementos comunes encontrados o 0 si no
  encuentra.
* Incluye el archivo de cabeceras ``#include <stdint.h>`` para que el
  compilador encuentra la definición de ``uint8_t``.
* Crea un programa que solicite el tamaño de los arreglos y sus
  elementos.
* El programa debe mostrar el resultado de la función.
* Antes de insertar un elemento en el arreglo resultado debe verificar
  que este no exista en el arreglo, es decir, el arreglo resultado
  no debe tener elementos repetidos.

El flujo del programa será:

* Solicite el tamaño del primer arreglo.
* Ingrese los elementos del primer arreglo.
* Solicite el tamaño del segundo arreglo.
* Ingrese los elementos del segundo arreglo.
* Indicar cuántos elementos comunes se encontraron y el arreglo
  con dichos elementos.

Ejercicio 22
^^^^^^^^^^^^^^^^

En este ejercicio te propongo encriptar y desencriptar un archivo

Se busca realizar dos programas que permitan encriptar
y desencriptar un archivo.

El programa que encripta:

* Debe solicitar al usuario la función para encriptar
  la información y el nombre del archivo de entrada y
  el de salida. El archivo de entrada tendrá la
  información y el de salida la información encriptada.
* La función debe modificar cada uno de los bytes que
  componen el archivo. Tenga presente que también se
  encriptará el byte de nueva línea.

El programa que desencripta:

* Debe solicitar al usuario la función para encriptar
  la información y el nombre del archivo de entrada y
  el de salida. En este caso el archivo de entrada
  tendrá la información encriptada y el archivo de salida
  la información desencriptada.
* Tenga presente que el usuario ingresa la función
  con la cual se encripta y usted debe encontrar la
  función inversa para desencriptar.

.. note::
    ¡Alerta de Spoiler!

Te dejo una posible solución al ejercicio. Ten en cuenta, que voy
a obviar todas las verificaciones de error para mantener
el código compacto y te puedas concentrar justo en la
funcionalidad solicitada.

.. warning:: Este código asumen que la información ingresada está
             bien formateada y libre de errores. Por tanto, se omiten
             algunas verificaciones.

.. note:: Para probar los siguientes programas (es el mismo para encriptar
          y desencriptar) es necesario que crees el archivo de texto que
          será encriptado.

.. code-block:: rust

    use std::fs;
    use std::io::{stdin, stdout, Write};
    use std::fs::OpenOptions;

    fn main() {

        let mut command = String::new();

        println!("Enter in_file out_file function\n");
        read(&mut command);

        let instructions : Vec<String> = command.split(" ").map(|s| s.to_string()).collect();

        let in_file  = String::from(instructions[0].clone().trim());
        let out_file = String::from(instructions[1].clone().trim());
        let function = String::from(instructions[2].clone().trim());

        let in_file_buffer = fs::read(in_file).expect("Error leyendo el archivo");

        // Abrir archivo de salida
        let mut out = OpenOptions::new()
        .write(true)
        .append(true)
        .create(true)
        .open(out_file)
        .unwrap();

        for mut character in in_file_buffer {
            match function.as_str() {
                "xor" => character = enc_xor_function(character),
                _ => character = character,
            }

            if let Err(e) = write!(out, "{}", character as char) {
                eprintln!("Couldn't write to file: {}", e);
            }
        }    
    }

    fn enc_xor_function(data : u8) ->  u8{
        data ^ 0xFF
    }

    fn read(input: &mut String) {
        stdout().flush().expect("Couldn't flush in_file_buffer");
        stdin().read_line(input).expect("Failed to read");
    }


Ejercicio 23
^^^^^^^^^^^^^^^

Al comienzo de la unidad hablamos de cómo los Strings eran arreglos de bytes y que debíamos tener cuidado
cuando los manipularamos. Habrás notado que el ejemplo anterior tiene un error a la hora de desencriptar un archivo.
El error se debe a cómo estamos leyendo el archivo.

En el ejemplo anterior usamos la función ``fs::read(&buffer)`` para leer un archivo, esta función retorna ``Vec<u8>``,
que usamos para iterar sobre cada byte y aplicar la función de encriptado. Sin embargo el xor sobre los bytes no tiene en cuenta
que estamos iterando caracteres en UTF-8, que podrían ser de entre 1 y 4 bytes. 

Por lo que cuando escribimos el mensaje encriptado al archivo de salida estaremos escribiendo no solo los caracteres encriptados
si no otros cuantos bytes de "basura". Por lo que al ser leido nuevamente y desencriptado el mensaje también estaremos pasando los bytes
de basura a la función de desencriptado, lo que resulta en un mensaje distinto del original.

Para solucionarlo debemos usar métodos y tipos de dato apropiados para manejar Strings y caracteres, para que cuando el programa lea
los bytes los maneje como si fueran Strings y caracteres apropiados y no simples bytes por separado.

Presta atención a los cambios, como ``fs::read_to_string()`` y ``"xor" => character = enc_xor_function(character as u8) as char``.

.. code-block:: rust
    :linenos:

    use std::fs;
    use std::io::{stdin, stdout, Write};
    use std::fs::OpenOptions;
    
    fn main() {
       
        let mut command = String::new();
    
        println!("Enter in_file out_file function\n");
        read(&mut command);
    
        let instructions : Vec<String> = command.split(" ").map(|s| s.to_string()).collect();
        
        let in_file  = String::from(instructions[0].clone().trim());
        let out_file = String::from(instructions[1].clone().trim());
        let function = String::from(instructions[2].clone().trim());
    
        let in_file_buffer = fs::read_to_string(in_file).expect("Error leyendo el archivo");
    
        // Abrir archivo de salida
        let mut out = OpenOptions::new()
        .write(true)
        .append(true)
        .create(true)
        .open(out_file)
        .unwrap();
    
        for mut character in in_file_buffer.chars() {
            match function.as_str() {
                "xor" => character = enc_xor_function(character as u8) as char,
                _ => character = character,
            }
            
            if let Err(e) = write!(out, "{}", character as char) {
                eprintln!("Couldn't write to file: {}", e);
            }
        }    
    }
    
    fn enc_xor_function(data : u8) ->  u8{
        data ^ 0xFF
    }
    
    fn read(input: &mut String) {
        stdout().flush().expect("Couldn't flush in_file_buffer");
        stdin().read_line(input).expect("Failed to read");
    }


Ejercicio 24
^^^^^^^^^^^^^^

Modifica el código anterior para que reciba
la información como argumentos de la función main,
al ejecutar el programa. NO DEBES SOLICITAR información
al usuario, todas la información será pasada cuando
se invoque el ejecutable en línea de comandos.

Ejercicio 25: Cargo
^^^^^^^^^^^^^^^^^^^^^^

En Rust es muy fácil utilizar librerías externas, basta con buscar el `Crate <https://crates.io/>`__.
Veamos el ejemplo del crate `ferris-says <https://crates.io/crates/ferris-says>`__.

- Editar el archivo **Cargo.toml** agregando el nombre del crate que vamos a usar.

.. code-block:: rust

[dependencies]
ferris-says = "0.2"

- Importar el crate en nuestro código:

.. code-block:: rust
    :linenos:

    extern crate ferris_says;

Por Ejemplo:

.. code-block:: rust

    extern crate ferris_says;

    use ferris_says::say;
    use std::io::{ stdout, BufWriter };

    fn main() {
        let out = b"Hello fellow Rustaceans!";
        let width = 24;

        let mut writer = BufWriter::new(stdout());
        say(out, width, &mut writer).unwrap();
    }

Imprime: 

.. code-block:: bash

    __________________________
    < Hello fellow Rustaceans! >
     --------------------------
            \
             \
                _~^~^~_
            \) /  o o  \ (/
              '_   -   _'
              / '-----' \

Ejercicio 26: Macros
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Hasta el momento habíamos hablado que los macros en Rust son diferentes de las funciones y que se pueden identificar por
el ``!`` como en ``println!()``. Los macros son fundamentalmente una forma de escribir código que escribe más código, también 
conocido como *metaprogramming*. Uno de sus mayores ventajas y diferencias con las funciones es que podemos escribir
macros que toman ua cantidad variable de parámetros, así como lo hemos visto con el ``println("{1} {2} ... {n}, a, b, ..., n)``.

Además tienen un impacto sobre el proceso de compilación pues deben ser expandidos antes de que el código sea compilado, las desventajas
de los macros es que suelen ser más complicados de escribir, leer y mantener debido a su naturaleza de ser código en rust que genera más 
código.

Ejercicio 27: Proceso de Compilación 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Veamos cómo se transforma el código que escribimos en Rust en un ejecutable. Hasta el momento solo hemos visto como se compila un programa 
con el comando ``rustc`` o compilamos indirectamente e intermediatamente ejecutamos el progama usando ``cargo run``, pero no hemos visto qué hace
la máquina para llegar a los resultados.

Ya habíamos visto que para compilar con rustc solo usabamos ``rustc <ruta_del_programa>``, generando directamente el ejecutable, pero no nos dice
cómo lo hizo. Para ver el proceso de compilación vamos a pasar `argumentos a rustc <https://doc.rust-lang.org/rustc/command-line-arguments.html>`__.
Ejecutar los siguientes comandos puede causar un error "the option -Z is only accepted on the nightly compiler", para solucionarlo corre en la terminal:

.. code-block:: bash

    rustup default nightly

En los siguientes ejercicios vamos a ver detalladamente lo que significan los pasos de la siguiente imagen, que representa los
`pasos de compilación de un programa en Rust <Tomada de: https://blog.rust-lang.org/2016/04/19/MIR.html>`__.

.. image:: \../_static/unidad_1/compilation_steps.png

Ejercicio 28: Lexing and Parsing
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

El primer paso es `Lexing and Parsing <https://rustc-dev-guide.rust-lang.org/the-parser.html>`__, esto es que el compilador
va a leer los caracteres unicode de nuestro progama y convertirlos en algo con lo que el compilador puede trabajar más cómodamente
que si fueran solo Strings. Esto se hace en dos pasos:

El `LEXER o ANÁLISIS LÉXICO <https://en.wikipedia.org/wiki/Lexical_analysis>`__, su propósito es obtener una representación
intermedia del programa conocida como stream of tokens. Por ejemplo, supongamos la siguiente
expresión en un lenguaje de programación arbitrario: ``print hola``. Un token es una unidad
indivisible que consiste de un tipo y un valor. En la expresión anterior el primer token es de
tipo Identificador y el valor es print. El segundo token es de tipo CADENA y el valor es hola.. 

Otro ejemplo: ``a.b + c`` es convertido en el stream de tokens `a`,`.`,`b`,`+` y `c`.

.. note:: `¿Alguien quiere porfavor pensar en la notación polaca inversa? <https://es.wikipedia.org/wiki/Notaci%C3%B3n_polaca_inversa>`__

El `PARSER <https://es.wikipedia.org/wiki/Analizador_sint%C3%A1ctico>`__, su propósito es validar si la sintaxis de el programa es válida o no.
Por tanto, a esta fase se le conoce como análisis sintáctico. El PARSER toma la gramática formal
del lenguaje y trata de hacer un match con el texto del programa. En términos simples, la gramática
formal del lenguaje es el conjunto de reglas que se deben seguir para usar correctamente las
'palabras' definidas por el lenguaje. El PARSER valida si el programa que escribiste cumple las
reglas definidas en la gramática y si todo está bien produce una representación intermedia 
del programa conocida como AST o Abstract Syntax Tree.

Ahora que ya sabemos cómo se transforma un programa del código fuente al lenguaje de máquina,
podemos indagar un poco más en las fases. ¿Cómo funciona un compilador?

Un compilador también funciona por fases. Así:

  No olvides que un programa en lenguaje C se puede compilar a múltiples lenguajes ensambladores
  o set de instrucciones. Cada set de instrucciones es específico para cada CPU;
  sin embargo, sin importar el set de instrucciones final, la representación AST será la misma. 
  A esta parte del compilador se le conoce como frontend y luego, a la parte del compilador que
  toma el AST y lo convierte a un set de instrucciones específico, se le conoce como backend.

* La tercera fase es el generador de código ensamblador. Es precisamente el backend del que te hablé
  hace un momento. El generador toma el AST, lo optimiza y genera instrucciones en lenguaje ensamblador
  para la CPU específica que estemos compilando.

Veamos el siguiente programa:

.. code-block:: rust

    fn main() {
        let a = 1;
        let b = -5;

        let suma = sum(a, b);

        println!("{} + {} = {}", a,b, suma);
    }

    fn sum(a: i32, b: i32) -> i32 {
        a + b
    }

Podemos pedirle a ``rustc`` que nos muestre el resultado después de solo realizar el parsing

.. code-block:: bash

    rustc -Z unstable-options --pretty normal main.rs 

Este es el resultado

.. image:: \../_static/unidad_1/compile_pretty_normal.png


Ejercicio 29: Macro Expansion
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Cabe destacar que durante el proceso de **parsing** el parser puede encontrarse con macros e invocaciones, que deben ser expandidos
y revelar más macros e invocaciones, y así... Por esto hay un paso más dedicado solo a expandir estos macros. Recuerda que los macros
son como fragmentos de código que generan más código, por lo que es posible que al momento de expandir un macro se revele que este macro
implementa otro macro.

Esto puede convertirse en un problema bastante complicado porque puede ocurrir que el parser al momento de expandir un macro no sepa que es,
porque aún no conoce la implementación de ese macro en específico, por esto implementa un sistema de **queue** que de una forma **muy** resumida
y general es:

- Sacar el macro de la cola
- Intentar resolverlo
- Si lo logra lo integra al Abstract Syntax Tree o **AST**.
- Si no lo logra lo devuelve a la cola y sigue iterando sobre la cola.
- Si no hace ningún progreso tenemos un error de compilación. (Por ejemplo un macro indefinido)

Usando el mismo código del ejemplo vamos a pedirle a rustc que nos muestre el resultado después de expandir los macros:

.. code-block:: bash

    rustc -Z unstable-options --pretty normal main.rs 

Este es el resultado

.. image:: \../_static/unidad_1/compile_pretty_expanded.png
    
Presta especial atención a la expansión de ``println!()``, la implementación del macro
nos ahorra escribir código como este, que es el código que en verdad es ejecutado cuando invocamos el macro, y lo simplifica en una simple expresión
como ``println!()``. 

Hagamos pequeño cambio al programa para ver cómo afecta el resultado, reemplaza el 
``println!("{} + {} = {}", a,b, suma);`` por ``println!("El resultado es {}", suma);``
y vuelve a invocar rustc para que muestre el resultado después de expandir los macros.

- ¿Que cambios notaste en el resultado?

Ejercicio 30: HIR
^^^^^^^^^^^^^^^^^^^^^^^^^^

El **High-Level Intermediate Representation** o **HIR** es la `representación intermedia (IR) <https://en.wikipedia.org/wiki/Intermediate_representation>`__ más utilizada por rustc.
Es una representación del **AST** y algunas partes de este son similares en sintaxis a Rust de cierta manera, debido a un paso
conocido como **lowering**, muchas de las estructuras son eliminadas si no son relevantes para los análisis. Algunos ejemplos de esto son:

- Eliminar parentesis.
- Los ciclos ``for`` son convertidos en ``loop`` y ``match``.
- ``if let`` son convertidos en ``match``

Podemos ver el HIR de nuestro programa con

.. code-block:: bash

    rustc -Z unpretty=hir-tree main.rs


En la creación de **HIR** se agregan varios identificadores a los nodos, como
``DefId`` para referirse a la definición de un *crate*, ``LocalDefId`` para referirse a una
*definición* dentro del crate actualmente compilado, o ``HirId`` para referirse a otro nodo del
**HIR**. Estas definiciones permiten asociar diferentes elementos entre ellos, y organizar mejor los contenidos
del *crate* que estamos compilando para que sean más fáciles de acceder, **solo se construye un HIR para el crate que se está compilando en ese momento**.

Ejercicio 31: HIR MAP & HIR BODIES
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Una ventaja del **HIR** es que gracias a esta representación se puede iterar fácilmente sobre todos los *items* del crate con 
pares de llaves y valores, sin la necesidad de iterar sobre todo el HIR.

Por ejemplo, si se quiere convertir un ``defDefId``en ``NodeId`` se puede usar una función ``tcx.hir().as_local_node_id(def_id)`` para buscar
un nodo con el id de la definición.

Luego se podría buscar un Nodo para un ``NodeId`` con ``tcx.hir().find(n)`` y obtener informaciń de ese nodo e incluso un apuntador a la información
o expresión que representa ese nodo.

Un **Body** representa algún tipo de código ejecutable, como lo puede ser el cuerpo de una función o la definición de una constante.

Mira el siguiente ejemplo:

.. code-block:: rust

    fn sum((x, y): (u32, u32)) -> u32 {
        x + y
    }

Aquí el ``Body``asociado a ``sum()`` tendría:

- un arreglo ``params`` que contiene el patrón de ``(x, y)``
- un valor que contiene la **expresión** ``x + y``
- un ``generator_kind`` que sería ``None``.

Todos los bodies tienen un owner

Ejercicio 32: MIR
^^^^^^^^^^^^^^^^^^^^^^^

A partir del **HIR** se puede construir el **MIR** (Mid-Level Intermediate Representation). Las características
principales del MIR son:

- Basado en un `Grafo de Control de Flujo <https://www.geeksforgeeks.org/software-engineering-control-flow-graph-cfg/>`__.
- No tiene expresiones anidadas.
- Todos los tipos en MIR son explícitos.

Viendo el MIR de un programa podremos comprender mejor la estructura de este, podemos generar un .mir del programa que hemos
usado en los últimos ejemplos con el comando:

.. code-block:: bash

    rustc --emit mir main.rs

El resultado es:

.. code-block:: bash

    // WARNING: This output format is intended for human consumers only
    // and is subject to change without notice. Knock yourself out.
    fn sum(_1: i32, _2: i32) -> i32 {
        debug a => _1;                       // in scope 0 at main.rs:10:8: 10:9
        debug b => _2;                       // in scope 0 at main.rs:10:16: 10:17
        let mut _0: i32;                     // return place in scope 0 at main.rs:10:27: 10:30
        let mut _3: i32;                     // in scope 0 at main.rs:11:5: 11:6
        let mut _4: i32;                     // in scope 0 at main.rs:11:9: 11:10
        let mut _5: (i32, bool);             // in scope 0 at main.rs:11:5: 11:10

        bb0: {
            _3 = _1;                         // scope 0 at main.rs:11:5: 11:6
            _4 = _2;                         // scope 0 at main.rs:11:9: 11:10
            _5 = CheckedAdd(_3, _4);         // scope 0 at main.rs:11:5: 11:10
            assert(!move (_5.1: bool), "attempt to compute `{} + {}`, which would overflow", move _3, move _4) -> bb1; // scope 0 at main.rs:11:5: 11:10
        }

        bb1: {
            _0 = move (_5.0: i32);           // scope 0 at main.rs:11:5: 11:10
            return;                          // scope 0 at main.rs:12:2: 12:2
        }
    }

    fn main() -> () {
        let mut _0: ();                      // return place in scope 0 at main.rs:1:11: 1:11
        let _1: i32;                         // in scope 0 at main.rs:2:9: 2:10
        let mut _4: i32;                     // in scope 0 at main.rs:5:20: 5:21
        let mut _5: i32;                     // in scope 0 at main.rs:5:23: 5:24
        let _6: ();                          // in scope 0 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:9: 97:62
        let mut _7: std::fmt::Arguments;     // in scope 0 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
        let mut _8: &[&str];                 // in scope 0 at main.rs:7:14: 7:34
        let mut _9: &[&str; 2];              // in scope 0 at main.rs:7:14: 7:34
        let _10: &[&str; 2];                 // in scope 0 at main.rs:7:14: 7:34
        let mut _11: &[std::fmt::ArgumentV1]; // in scope 0 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
        let mut _12: &[std::fmt::ArgumentV1; 1]; // in scope 0 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
        let _13: &[std::fmt::ArgumentV1; 1]; // in scope 0 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
        let _14: [std::fmt::ArgumentV1; 1];  // in scope 0 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
        let mut _15: (&i32,);                // in scope 0 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
        let mut _16: &i32;                   // in scope 0 at main.rs:7:36: 7:40
        let mut _18: std::fmt::ArgumentV1;   // in scope 0 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
        let mut _19: &i32;                   // in scope 0 at main.rs:7:36: 7:40
        let mut _20: for<'r, 's, 't0> fn(&'r i32, &'s mut std::fmt::Formatter<'t0>) -> std::result::Result<(), std::fmt::Error>; // in scope 0 at main.rs:7:36: 7:40
        scope 1 {
            debug a => _1;                   // in scope 1 at main.rs:2:9: 2:10
            let _2: i32;                     // in scope 1 at main.rs:3:9: 3:10
            scope 2 {
                debug b => _2;               // in scope 2 at main.rs:3:9: 3:10
                let _3: i32;                 // in scope 2 at main.rs:5:9: 5:13
                scope 3 {
                    debug suma => _3;        // in scope 3 at main.rs:5:9: 5:13
                    let _17: &i32;           // in scope 3 at main.rs:7:36: 7:40
                    let mut _21: &[&str; 2]; // in scope 3 at main.rs:7:14: 7:34
                    scope 4 {
                        debug arg0 => _17;   // in scope 4 at main.rs:7:36: 7:40
                    }
                }
            }
        }

        bb0: {
            _1 = const 1_i32;                // scope 0 at main.rs:2:13: 2:14
            _2 = const -5_i32;               // scope 1 at main.rs:3:13: 3:15
            _4 = const 1_i32;                // scope 2 at main.rs:5:20: 5:21
            _5 = const -5_i32;               // scope 2 at main.rs:5:23: 5:24
            _3 = sum(move _4, move _5) -> bb1; // scope 2 at main.rs:5:16: 5:25
                                             // mir::Constant
                                             // + span: main.rs:5:16: 5:19
                                             // + literal: Const { ty: fn(i32, i32) -> i32 {sum}, val: Value(Scalar(<ZST>)) }
        }

        bb1: {
            _21 = const main::promoted[0];   // scope 3 at main.rs:7:14: 7:34
                                             // ty::Const
                                             // + ty: &[&str; 2]
                                             // + val: Unevaluated(main, [], Some(promoted[0]))
                                             // mir::Constant
                                             // + span: main.rs:7:14: 7:34
                                             // + literal: Const { ty: &[&str; 2], val: Unevaluated(Unevaluated { def: WithOptConstParam { did: DefId(0:3 ~ main[317d]::main), const_param_did: None }, substs: [], promoted: Some(promoted[0]) }) }
            _10 = _21;                       // scope 3 at main.rs:7:14: 7:34
            _9 = _10;                        // scope 3 at main.rs:7:14: 7:34
            _8 = move _9 as &[&str] (Pointer(Unsize)); // scope 3 at main.rs:7:14: 7:34
            _16 = &_3;                       // scope 3 at main.rs:7:36: 7:40
            (_15.0: &i32) = move _16;        // scope 3 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
            _17 = (_15.0: &i32);             // scope 3 at main.rs:7:36: 7:40
            _19 = _17;                       // scope 4 at main.rs:7:36: 7:40
            _20 = <i32 as std::fmt::Display>::fmt as for<'r, 's, 't0> fn(&'r i32, &'s mut std::fmt::Formatter<'t0>) -> std::result::Result<(), std::fmt::Error> (Pointer(ReifyFnPointer)); // scope 4 at main.rs:7:36: 7:40
                                             // mir::Constant
                                             // + span: main.rs:7:36: 7:40
                                             // + literal: Const { ty: for<'r, 's, 't0> fn(&'r i32, &'s mut std::fmt::Formatter<'t0>) -> std::result::Result<(), std::fmt::Error> {<i32 as std::fmt::Display>::fmt}, val: Value(Scalar(<ZST>)) }
            _18 = ArgumentV1::new::<i32>(move _19, move _20) -> bb2; // scope 4 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
                                             // mir::Constant
                                             // + span: /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
                                             // + user_ty: UserType(1)
                                             // + literal: Const { ty: for<'b> fn(&'b i32, for<'r, 's, 't0> fn(&'r i32, &'s mut std::fmt::Formatter<'t0>) -> std::result::Result<(), std::fmt::Error>) -> std::fmt::ArgumentV1<'b> {std::fmt::ArgumentV1::new::<i32>}, val: Value(Scalar(<ZST>)) }
        }

        bb2: {
            _14 = [move _18];                // scope 4 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
            _13 = &_14;                      // scope 3 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
            _12 = _13;                       // scope 3 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
            _11 = move _12 as &[std::fmt::ArgumentV1] (Pointer(Unsize)); // scope 3 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
            _7 = Arguments::new_v1(move _8, move _11) -> bb3; // scope 3 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
                                             // mir::Constant
                                             // + span: /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:28: 97:61
                                             // + user_ty: UserType(0)
                                             // + literal: Const { ty: fn(&[&'static str], &[std::fmt::ArgumentV1]) -> std::fmt::Arguments {std::fmt::Arguments::new_v1}, val: Value(Scalar(<ZST>)) }
        }

        bb3: {
            _6 = _print(move _7) -> bb4;     // scope 3 at /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:9: 97:62
                                             // mir::Constant
                                             // + span: /rustc/42816d61ead7e46d462df997958ccfd514f8c21c/library/std/src/macros.rs:97:9: 97:27
                                             // + literal: Const { ty: for<'r> fn(std::fmt::Arguments<'r>) {std::io::_print}, val: Value(Scalar(<ZST>)) }
        }

        bb4: {
            _0 = const ();                   // scope 0 at main.rs:1:11: 8:2
            return;                          // scope 0 at main.rs:8:2: 8:2
        }
    }

    promoted[0] in main: &[&str; 2] = {
        let mut _0: &[&str; 2];              // return place in scope 0 at main.rs:7:14: 7:34
        let mut _1: [&str; 2];               // in scope 0 at main.rs:7:14: 7:34

        bb0: {
            _1 = [const "El resultado es ", const "\n"]; // scope 0 at main.rs:7:14: 7:34
                                             // ty::Const
                                             // + ty: &str
                                             // + val: Value(Slice { data: Allocation { bytes: [69, 108, 32, 114, 101, 115, 117, 108, 116, 97, 100, 111, 32, 101, 115, 32], relocations: Relocations(SortedMap { data: [] }), init_mask: InitMask { blocks: [65535], len: Size { raw: 16 } }, size: Size { raw: 16 }, align: Align { pow2: 0 }, mutability: Not, extra: () }, start: 0, end: 16 })
                                             // mir::Constant
                                             // + span: main.rs:7:14: 7:34
                                             // + literal: Const { ty: &str, val: Value(Slice { data: Allocation { bytes: [69, 108, 32, 114, 101, 115, 117, 108, 116, 97, 100, 111, 32, 101, 115, 32], relocations: Relocations(SortedMap { data: [] }), init_mask: InitMask { blocks: [65535], len: Size { raw: 16 } }, size: Size { raw: 16 }, align: Align { pow2: 0 }, mutability: Not, extra: () }, start: 0, end: 16 }) }
                                             // ty::Const
                                             // + ty: &str
                                             // + val: Value(Slice { data: Allocation { bytes: [10], relocations: Relocations(SortedMap { data: [] }), init_mask: InitMask { blocks: [1], len: Size { raw: 1 } }, size: Size { raw: 1 }, align: Align { pow2: 0 }, mutability: Not, extra: () }, start: 0, end: 1 })
                                             // mir::Constant
                                             // + span: main.rs:7:14: 7:34
                                             // + literal: Const { ty: &str, val: Value(Slice { data: Allocation { bytes: [10], relocations: Relocations(SortedMap { data: [] }), init_mask: InitMask { blocks: [1], len: Size { raw: 1 } }, size: Size { raw: 1 }, align: Align { pow2: 0 }, mutability: Not, extra: () }, start: 0, end: 1 }) }
            _0 = &_1;                        // scope 0 at main.rs:7:14: 7:34
            return;                          // scope 0 at main.rs:7:14: 7:34
        }
    }

Si lo analizamos un poco en detalle podremos identificar que al comienzo de la función ``sum`` la declaración de varias variables:

.. code-block:: bash

        debug a => _1;                       // in scope 0 at main.rs:10:8: 10:9
        debug b => _2;                       // in scope 0 at main.rs:10:16: 10:17
        let mut _0: i32;                     // return place in scope 0 at main.rs:10:27: 10:30
        let mut _3: i32;                     // in scope 0 at main.rs:11:5: 11:6
        let mut _4: i32;                     // in scope 0 at main.rs:11:9: 11:10
        let mut _5: (i32, bool);             // in scope 0 at main.rs:11:5: 11:10

Nota que en el MIR las variables no tienen nombres, pero si tienen índices, como ``_0`` o ``_3``, y podemos diferenciar
variables definidas por nosotros porque tienen asociadas variables **debuginfo**.

Si seguimos analizando la función podremos encontrar los **basic blocks**, son unidades del grafo control de flujo,
consisten de:

- **statements**: acciones con un sucesor.
- **terminators**: acciones con múltiples posibles sucesores, siempre al final del bloque

.. code-block:: bash

    bb0: {
            _3 = _1;                         // scope 0 at main.rs:11:5: 11:6
            _4 = _2;                         // scope 0 at main.rs:11:9: 11:10
            _5 = CheckedAdd(_3, _4);         // scope 0 at main.rs:11:5: 11:10
            assert(!move (_5.1: bool), "attempt to compute `{} + {}`, which would overflow", move _3, move _4) -> bb1; // scope 0 at main.rs:11:5: 11:10
        }
    
    bb1: {
            _0 = move (_5.0: i32);           // scope 0 at main.rs:11:5: 11:10
            return;                          // scope 0 at main.rs:12:2: 12:2
    }

En los bloques podemos ver varias asignaciones y statements.

.. code-block:: bash

    _3 = _1;
    _4 = _2;
    _5 = CheckedAdd(_3, _4);         // scope 0 at main.rs:11:5: 11:10

    ____________________________________
    
    _0 = move (_5.0: i32);           // scope 0 at main.rs:11:5: 11:10
    return;                          // scope 0 at main.rs:12:2: 12:2


Las asignaciones generalmente tienen la forma:

.. code-block:: bash

    <Place> = <Rvalue>

Un *Place* es una expresión como ``_3``, ``_3.f`` o ``*_3``- Denotando una ubicación en memoria. Un **Rvalue** es una expresión
que crea un valor, el rvalue es una expresión de referencia mutable parecida a ``&mut <Place>``. De esta manera podemos definir
una gramática para rvalues como:

.. code-block:: bash

    <Rvalue>  = & (mut)? <Place>
              | <Operand> + <Operand>
              | <Operand> - <Operand>
              | ...

    <Operand> = Constant
              | copy Place
              | move Place

- Intenta identificar algunas de estas estructuras y bloques para la función ``main``.


Ejercicio 33: Análisis
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

En este punto el compilador hace un análisis del código, esta parte es conocida como "El sistema de tipos de Rust", durante todo
el proceso de compilación se hacen varios análisis en diferentes etapas, no todos los análisis no ocurren en un solo momento o una etapa, 
sino que están repartidos entre varias etapas del proceso. Por ejemplo el *type checking* ocurre en el HIR mientras que el *borrow checking* ocurre en el MIR.

Los análisis son:

- Type Representation.
- Type Inference. 
- Typechecking.
- Pattern and Exhaustiveness Checking.
- MIR dataflow.
- Borrow Checking
- Parameter Environments
  
De cierta forma están orientados a analizar el programa pensando en *lo que podría ser* en lugar de lo que ya es, de esta forma puede identificar
casos en los que *podría* ocurrir un error. Puedes profundizar en este tema leyendo sobre `Static program Analysis <https://en.wikipedia.org/wiki/Static_program_analysis>`_.


Ejercicio 34: LLVM
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Después de que el compilador termina con todos los pasos vistos en elos ejercicios anteriores, finalmente tendremos nada que que la máquina entienda.
¡¡Hasta el momento no hemos generado ni una sola línea de código ejecutable!!. Pero estamos cerca, en este punto al compilador solo le falta hacer
optimizaciones finales, como sustituir tipos, simplificar referencias, analizar constantes y estará listo para pasar a la etapa de generar código.

Para generar el código ejecutable Rust utiliza `LLVM <https://llvm.org/>`__. "Es una infraestructura para desarrollar compiladores, 
escrita a su vez en el lenguaje de programación C++, que está diseñada para optimizar el tiempo de compilación, el tiempo de enlazado, 
el tiempo de ejecución y el 'tiempo ocioso' en cualquier lenguaje de programación que el usuario quiera definir."

Al final de las optimizaciones mencionadas anteriormente, cada bloque básico del MIR es *mapeado* a un bloque básico de LLVM, generando un LLVM IR,
que es básicamente código de ensamblador con unos tipos y anotaciones adicionales que facilitan hacer optimizaciones.

Luego ya hacia las etapas finales del proceso de compilación, LLVM toma como input el LLVM IR, lo agrupa en módulos para la generación de código y hace 
el *linking*, en esta etapa puede que haga *más* optimizaciones para generar finalmente un ejecutable.

¿En donde quedó la parte en que el compilador de rust genera código?

Rust no implementa la parte de generación de código por si mismo, sino que se vale de LLVM, esto tiene varias ventajas como:

- No hay que escribir un compilador entero.
- Se puede aprovechar una gran cantidad de herramientas que ofrece el proyecto de LLVM.
- Se puede compilar Rust a cualquiera de las plataformas para las que LLVM tiene soporte.
- Los avances de los proyectos que usan LLVM benefician a todos. Por ejemplo cuando se descubrieron las vulnerabilidades de `Spectre y Meltdown <https://meltdownattack.com/>`__ solo fue necesario hacer un parche para LLVM para solucionarlo.

Podemos ver el código LLVM generado con los flags ``--emit llvm-ir``, entonces:

.. code-block:: bash

    rustc --emit llvm-ir main.rs

Produce:

.. code-block:: bash

    ; ModuleID = 'main.7rcbfp3g-cgu.0'
    source_filename = "main.7rcbfp3g-cgu.0"
    target datalayout = "e-m:e-p270:32:32-p271:32:32-p272:64:64-i64:64-f80:128-n8:16:32:64-S128"
    target triple = "x86_64-unknown-linux-gnu"

    %"std::fmt::Formatter" = type { [0 x i64], { i64, i64 }, [0 x i64], { i64, i64 }, [0 x i64], { {}*, [3 x i64]* }, [0 x i32], i32, [0 x i32], i32, [0 x i8], i8, [7 x i8] }
    %"core::fmt::Opaque" = type {}
    %"std::fmt::Arguments" = type { [0 x i64], { [0 x { [0 x i8]*, i64 }]*, i64 }, [0 x i64], { i64*, i64 }, [0 x i64], { [0 x { i8*, i64* }]*, i64 }, [0 x i64] }
    %"std::panic::Location" = type { [0 x i64], { [0 x i8]*, i64 }, [0 x i32], i32, [0 x i32], i32, [0 x i32] }
    %"unwind::libunwind::_Unwind_Exception" = type { [0 x i64], i64, [0 x i64], void (i32, %"unwind::libunwind::_Unwind_Exception"*)*, [0 x i64], [6 x i64], [0 x i64] }
    %"unwind::libunwind::_Unwind_Context" = type { [0 x i8] }

    @vtable.0 = private unnamed_addr constant { void (i64**)*, i64, i64, i32 (i64**)*, i32 (i64**)*, i32 (i64**)* } { void (i64**)* @"_ZN4core3ptr85drop_in_place$LT$std..rt..lang_start$LT$$LP$$RP$$GT$..$u7b$$u7b$closure$u7d$$u7d$$GT$17he9c53e06c5d4b711E", i64 8, i64 8, i32 (i64**)* @"_ZN3std2rt10lang_start28_$u7b$$u7b$closure$u7d$$u7d$17hce1a25dfefc4f916E", i32 (i64**)* @"_ZN3std2rt10lang_start28_$u7b$$u7b$closure$u7d$$u7d$17hce1a25dfefc4f916E", i32 (i64**)* @"_ZN4core3ops8function6FnOnce40call_once$u7b$$u7b$vtable.shim$u7d$$u7d$17h427fda46e047ab3fE" }, align 8
    @alloc1 = private unnamed_addr constant <{ [16 x i8] }> <{ [16 x i8] c"El resultado es " }>, align 1
    @alloc3 = private unnamed_addr constant <{ [1 x i8] }> <{ [1 x i8] c"\0A" }>, align 1
    @alloc2 = private unnamed_addr constant <{ i8*, [8 x i8], i8*, [8 x i8] }> <{ i8* getelementptr inbounds (<{ [16 x i8] }>, <{ [16 x i8] }>* @alloc1, i32 0, i32 0, i32 0), [8 x i8] c"\10\00\00\00\00\00\00\00", i8* getelementptr inbounds (<{ [1 x i8] }>, <{ [1 x i8] }>* @alloc3, i32 0, i32 0, i32 0), [8 x i8] c"\01\00\00\00\00\00\00\00" }>, align 8
    @alloc29 = private unnamed_addr constant <{ [7 x i8] }> <{ [7 x i8] c"main.rs" }>, align 1
    @alloc30 = private unnamed_addr constant <{ i8*, [16 x i8] }> <{ i8* getelementptr inbounds (<{ [7 x i8] }>, <{ [7 x i8] }>* @alloc29, i32 0, i32 0, i32 0), [16 x i8] c"\07\00\00\00\00\00\00\00\0B\00\00\00\05\00\00\00" }>, align 8
    @str.1 = internal constant [28 x i8] c"attempt to add with overflow"

    ; std::sys_common::backtrace::__rust_begin_short_backtrace
    ; Function Attrs: noinline nonlazybind uwtable
    define internal void @_ZN3std10sys_common9backtrace28__rust_begin_short_backtrace17hf66d8c7a932d6f71E(void ()* nonnull %f) unnamed_addr #0 personality i32 (i32, i32, i64, %"unwind::libunwind::_Unwind_Exception"*, %"unwind::libunwind::_Unwind_Context"*)* @rust_eh_personality {
    start:
      %0 = alloca { i8*, i32 }, align 8
    ; call core::ops::function::FnOnce::call_once
      call void @_ZN4core3ops8function6FnOnce9call_once17hfa3234c194bf7715E(void ()* nonnull %f)
      br label %bb1

    bb1:                                              ; preds = %start
    ; invoke core::hint::black_box
      invoke void @_ZN4core4hint9black_box17hd3ed79ea75a8b07eE()
              to label %bb2 unwind label %cleanup

    bb2:                                              ; preds = %bb1
      ret void

    bb3:                                              ; preds = %cleanup
      br label %bb4

    bb4:                                              ; preds = %bb3
      %1 = bitcast { i8*, i32 }* %0 to i8**
      %2 = load i8*, i8** %1, align 8
      %3 = getelementptr inbounds { i8*, i32 }, { i8*, i32 }* %0, i32 0, i32 1
      %4 = load i32, i32* %3, align 8
      %5 = insertvalue { i8*, i32 } undef, i8* %2, 0
      %6 = insertvalue { i8*, i32 } %5, i32 %4, 1
      resume { i8*, i32 } %6

    cleanup:                                          ; preds = %bb1
      %7 = landingpad { i8*, i32 }
              cleanup
      %8 = extractvalue { i8*, i32 } %7, 0
      %9 = extractvalue { i8*, i32 } %7, 1
      %10 = getelementptr inbounds { i8*, i32 }, { i8*, i32 }* %0, i32 0, i32 0
      store i8* %8, i8** %10, align 8
      %11 = getelementptr inbounds { i8*, i32 }, { i8*, i32 }* %0, i32 0, i32 1
      store i32 %9, i32* %11, align 8
      br label %bb3
    }

    ; std::rt::lang_start
    ; Function Attrs: nonlazybind uwtable
    define hidden i64 @_ZN3std2rt10lang_start17h358cf2a9c1254586E(void ()* nonnull %main, i64 %argc, i8** %argv) unnamed_addr #1 {
    start:
      %_7 = alloca i64*, align 8
      %0 = bitcast i64** %_7 to void ()**
      store void ()* %main, void ()** %0, align 8
      %_4.0 = bitcast i64** %_7 to {}*
    ; call std::rt::lang_start_internal
      %1 = call i64 @_ZN3std2rt19lang_start_internal17hab5a8a909af4f90eE({}* nonnull align 1 %_4.0, [3 x i64]* align 8 dereferenceable(24) bitcast ({ void (i64**)*, i64, i64, i32 (i64**)*, i32 (i64**)*, i32 (i64**)* }* @vtable.0 to [3 x i64]*), i64 %argc, i8** %argv)
      br label %bb1

    bb1:                                              ; preds = %start
      ret i64 %1
    }

    ; std::rt::lang_start::{{closure}}
    ; Function Attrs: inlinehint nonlazybind uwtable
    define internal i32 @"_ZN3std2rt10lang_start28_$u7b$$u7b$closure$u7d$$u7d$17hce1a25dfefc4f916E"(i64** align 8 dereferenceable(8) %_1) unnamed_addr #2 {
    start:
      %0 = bitcast i64** %_1 to void ()**
      %_3 = load void ()*, void ()** %0, align 8, !nonnull !3
    ; call std::sys_common::backtrace::__rust_begin_short_backtrace
      call void @_ZN3std10sys_common9backtrace28__rust_begin_short_backtrace17hf66d8c7a932d6f71E(void ()* nonnull %_3)
      br label %bb1

    bb1:                                              ; preds = %start
    ; call <() as std::process::Termination>::report
      %1 = call i32 @"_ZN54_$LT$$LP$$RP$$u20$as$u20$std..process..Termination$GT$6report17h748f98991ea520fbE"()
      br label %bb2

    bb2:                                              ; preds = %bb1
      ret i32 %1
    }

    ...


Ejercicio 35
^^^^^^^^^^^^^^

¿Qué necesitas para correr el archivo ejecutable en un sistema operativo? pues necesitas que el sistema
operativo cree una abstracción denominada PROCESO. Por medio de esta abstracción el sistema operativo
administrará cuándo se ejecutarán, por parte de alguno de los CORE disponibles, el flujo de instrucciones
definido en el archivo ejecutable. Como te has podido dar cuenta, la ejecución de un programa en Rust comienza
llamando la función ``main``; sin embargo, el punto de entrada de un archivo ejecutable no es la función
``main``, sino otro punto que tendrá definidas las instrucciones necesarias para preparar el llamado a main.

Cuando enlazas un programa puedes usar bibliotecas estáticas o dinámicas. El código de la biblioteca
estática hará parte del archivo ejecutable. En contraste, el código de la biblioteca dinámica no será
parte del ejecutable; sin embargo, el archivo ejecutable si tendrá que indicar qué dependencias a
bibliotecas dinámicas tiene. De esta manera cuando quieras ejecutar el archivo, el sistema operativo tendrá
que cargar EN TIEMPO DE EJECUCIÓN el código de la biblioteca necesaria.

¿Qué es un biblioteca estática? es un archivo contenedor de múltiples relocatable object files. Este
archivo no es producido por el enlazador. En sistemas como Linux será el programa ``ar`` quien
lo generará. Como las bibliotecas estáticas son colecciones de relocatable object files, estas
pueden ser enlazadas con otros object files para producir ejecutables. De esta manera, la biblioteca
estática HARÁ PARTE DEL EJECUTABLE.

¿Y qué es una biblioteca dinámica? es un archivo creado directamente por el enlazador. Es 
similar en estructura a los archivos ejecutables, pero NO LO PUEDES EJECUTAR directamente. Una
biblioteca dinámica no tiene punto de entrada como un ejecutable. Más bien tiene pedazos de código
que pueden ser llamados por el programa. Lo más interesante de todo, es que puedes tener muchos
programas que dependan de la misma biblioteca. Aquí es donde brilla el sistema operativo. Este
te permitirá que varios procesos puedan compartir la misma biblioteca. Por tanto, a diferencia
de una biblioteca estática, las bibliotecas dinámicas no hacen parte del archivo ejecutable
de un programa, sino que son cargadas en la memoria del computador en tiempo de ejecución y
son compartidas por múltiples procesos. ¡QUE BELLEZA!

¿Y cómo funciona un enlazador? ya sabes que un enlazador toma varios relocatable object files
y los combina para generar un ejecutable. ¿Cómo los combina? Para responder esta pregunta
debemos indagar al interior de un relocatable object file. Ya sabes que estos archivos tienen
instrucciones de máquina, pero organizadas en secciones denominadas SÍMBOLOS. Para entender mejor
hagamos un ejemplo. Escribe los siguientes códigos:

.. code-block:: rust
   :linenos:

    fn suma(a: i32, b: i32) -> i32 {
       a + b
    }

    fn sumatoria(numeros: &mut [i32], cantidad: i32) -> i32 {
       let mut acumulado : i32 = 0;
    
       for i in 0..numeros.len(){
           acumulado = acumulado + numeros[i];
       }

       return acumulado
    }

Compila el archivo anterior para producir una librería estática, generará un archivo llamado **libsum.a** en la misma carpeta:

``rustc --crate-type=cdylib sum.rs``

Ahora observa los símbolos definidos en libsum.rlib utilizando el siguiente comando:

``nm libsum.a``

El resultado será algo como:

.. code-block:: bash

    sum.sum.3a1fbbbh-cgu.0.rcgu.o:

    sum.1yafyrf2uaakrs3o.rcgu.o:
                     U __rdl_alloc
                     U __rdl_alloc_zeroed
                     U __rdl_dealloc
                     U __rdl_realloc
                     U __rg_oom
    0000000000000000 T __rust_alloc
    0000000000000000 T __rust_alloc_error_handler
    0000000000000000 T __rust_alloc_zeroed
    0000000000000000 T __rust_dealloc
    0000000000000000 T __rust_realloc

    ...

    0000000000000000 t _ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E
    0000000000000000 T _ZN100_$LT$std..fs..Metadata$u20$as$u20$std..sys_common..FromInner$LT$std..sys..unix..fs..FileAttr$GT$$GT$10from_inner17h387c9900483a2027E
    0000000000000000 T _ZN100_$LT$std..sys..unix..args..Args$u20$as$u20$core..iter..traits..double_ended..DoubleEndedIterator$GT$9next_back17hb6813e0770a15fdaE
    0000000000000000 T _ZN101_$LT$std..sys..unix..ext..net..datagram..UnixDatagram$u20$as$u20$std..sys..unix..ext..io..AsRawFd$GT$9as_raw_fd17ha028ccd0c2ce1d7fE
    0000000000000000 T _ZN101_$LT$std..sys..unix..ext..net..listener..UnixListener$u20$as$u20$std..sys..unix..ext..io..AsRawFd$GT$9as_raw_fd17hcebfc332dc457fb0E
    0000000000000000 T _ZN101_$LT$std..sys..unix..process..process_inner..ExitStatus$u20$as$u20$core..convert..From$LT$i32$GT$$GT$4from17hd9b7c8ec2c7b620fE
    0000000000000000 T _ZN102_$LT$std..net..addr..SocketAddr$u20$as$u20$core..convert..From$LT$std..net..addr..SocketAddrV4$GT$$GT$4from17h95583c5051ab4864E
    0000000000000000 T _ZN102_$LT$std..net..addr..SocketAddr$u20$as$u20$core..convert..From$LT$std..net..addr..SocketAddrV6$GT$$GT$4from17h0cfe5afae9165c5eE
    0000000000000000 T _ZN102_$LT$std..sys..unix..ext..net..stream..UnixStream$u20$as$u20$std..sys..unix..kernel_copy..CopyRead$GT$10properties17hf27b60c9b7e49a04E
    0000000000000000 T _ZN103_$LT$std..io..cursor..Cursor$LT$$RF$mut$u20$alloc..vec..Vec$LT$u8$GT$$GT$$u20$as$u20$std..io..Write$GT$14write_vectored17h38ebbd3505ee8bbaE
    0000000000000000 T _ZN103_$LT$std..io..cursor..Cursor$LT$$RF$mut$u20$alloc..vec..Vec$LT$u8$GT$$GT$$u20$as$u20$std..io..Write$GT$5write17h937b1b19baba9b33E
    0000000000000000 T _ZN103_$LT$std..sync..mpsc..TryRecvError$u20$as$u20$core..convert..From$LT$std..sync..mpsc..RecvError$GT$$GT$4from17ha4b4a7d34465a49bE
    0000000000000000 T _ZN103_$LT$std..sys..unix..ext..net..datagram..UnixDatagram$u20$as$u20$std..sys..unix..ext..io..FromRawFd$GT$11from_raw_fd17ha26aab0b65b908f1E
    0000000000000000 T _ZN103_$LT$std..sys..unix..ext..net..datagram..UnixDatagram$u20$as$u20$std..sys..unix..ext..io..IntoRawFd$GT$11into_raw_fd17h74991f6b35230010E
    0000000000000000 T _ZN103_$LT$std..sys..unix..ext..net..listener..Incoming$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17h58d3a980223e9f36E
    0000000000000000 T _ZN103_$LT$std..sys..unix..ext..net..listener..Incoming$u20$as$u20$core..iter..traits..iterator..Iterator$GT$9size_hint17h4d2a05ea7e60b5cbE
    0000000000000000 T _ZN103_$LT$std..sys..unix..ext..net..listener..UnixListener$u20$as$u20$std..sys..unix..ext..io..FromRawFd$GT$11from_raw_fd17h6eff91f4f989a159E
    0000000000000000 T _ZN103_$LT$std..sys..unix..ext..net..listener..UnixListener$u20$as$u20$std..sys..unix..ext..io..IntoRawFd$GT$11into_raw_fd17hd0aa02cb3e67b38fE
    0000000000000000 T _ZN103_$LT$std..sys..unix..ext..net..stream..UnixStream$u20$as$u20$std..sys..unix..kernel_copy..CopyWrite$GT$10properties17heb82c6fd6e496069E
    0000000000000000 T _ZN104_$LT$std..fs..OpenOptions$u20$as$u20$std..sys_common..AsInner$LT$std..sys..unix..fs..OpenOptions$GT$$GT$8as_inner17h2dc06cb7da351606E
    0000000000000000 T _ZN104_$LT$std..sys_common..net..LookupHost$u20$as$u20$core..convert..TryFrom$LT$$LP$$RF$str$C$u16$RP$$GT$$GT$8try_from17h855a667c71f7ff0aE
    0000000000000000 T _ZN104_$LT$std..sys..unix..ext..net..ancillary..Messages$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17h46a682f0d43ac8dbE
    0000000000000000 T _ZN105_$LT$std..fs..DirBuilder$u20$as$u20$std..sys_common..AsInnerMut$LT$std..sys..unix..fs..DirBuilder$GT$$GT$12as_inner_mut17he4d941d7f97adfd8E
    0000000000000000 T _ZN105_$LT$std..sys..unix..ext..net..ancillary..ScmRights$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17he0b1360303b18799E
    0000000000000000 T _ZN106_$LT$$LT$std..path..Iter$u20$as$u20$core..fmt..Debug$GT$..fmt..DebugHelper$u20$as$u20$core..fmt..Debug$GT$3fmt17h59dfd7db8a8a6db2E
    0000000000000000 T _ZN106_$LT$$RF$std..sys..unix..ext..net..stream..UnixStream$u20$as$u20$std..sys..unix..kernel_copy..CopyRead$GT$10properties17hb4b2bc3a4a2ff006E
    0000000000000000 T _ZN107_$LT$$RF$std..sys..unix..ext..net..stream..UnixStream$u20$as$u20$std..sys..unix..kernel_copy..CopyWrite$GT$10properties17h76e83c8f4b9fd2f1E
    0000000000000000 T _ZN107_$LT$std..fs..OpenOptions$u20$as$u20$std..sys_common..AsInnerMut$LT$std..sys..unix..fs..OpenOptions$GT$$GT$12as_inner_mut17h627309799f3b2f65E
    0000000000000000 T _ZN107_$LT$std..process..ChildStdin$u20$as$u20$std..sys_common..AsInner$LT$std..sys..unix..pipe..AnonPipe$GT$$GT$8as_inner17hd552ff1371ec801aE
    0000000000000000 T _ZN107_$LT$std..sync..mpsc..RecvTimeoutError$u20$as$u20$core..convert..From$LT$std..sync..mpsc..RecvError$GT$$GT$4from17h1afb9e5affb9acc5E
    0000000000000000 T _ZN107_$LT$std..sys_common..process..CommandEnvs$u20$as$u20$core..iter..traits..exact_size..ExactSizeIterator$GT$3len17hd88922040fa650a0E
    0000000000000000 T _ZN107_$LT$std..sys_common..process..CommandEnvs$u20$as$u20$core..iter..traits..exact_size..ExactSizeIterator$GT$8is_empty17h33dd8a30e65bd2cfE
    0000000000000000 T _ZN107_$LT$std..sys..unix..time..inner..SystemTime$u20$as$u20$core..convert..From$LT$libc..unix..timespec$GT$$GT$4from17he9ab015ad8c0cab8E
    0000000000000000 T _ZN108_$LT$std..fs..Permissions$u20$as$u20$std..sys_common..AsInner$LT$std..sys..unix..fs..FilePermissions$GT$$GT$8as_inner17h362fd002e1922ff3E
    0000000000000000 T _ZN108_$LT$std..net..tcp..TcpStream$u20$as$u20$std..sys_common..AsInner$LT$std..sys_common..net..TcpStream$GT$$GT$8as_inner17h4a6a1454a7ca46f7E
    0000000000000000 T _ZN108_$LT$std..net..udp..UdpSocket$u20$as$u20$std..sys_common..AsInner$LT$std..sys_common..net..UdpSocket$GT$$GT$8as_inner17h157edfef7174b955E
    0000000000000000 T _ZN108_$LT$std..process..ChildStderr$u20$as$u20$std..sys_common..AsInner$LT$std..sys..unix..pipe..AnonPipe$GT$$GT$8as_inner17h3baee59fb179f398E
    0000000000000000 T _ZN108_$LT$std..process..ChildStdout$u20$as$u20$std..sys_common..AsInner$LT$std..sys..unix..pipe..AnonPipe$GT$$GT$8as_inner17heaf4ca451eaa2292E
    0000000000000000 T _ZN109_$LT$std..process..ChildStdin$u20$as$u20$std..sys_common..FromInner$LT$std..sys..unix..pipe..AnonPipe$GT$$GT$10from_inner17h10d9708291e372b5E
    0000000000000000 T _ZN109_$LT$std..process..ChildStdin$u20$as$u20$std..sys_common..IntoInner$LT$std..sys..unix..pipe..AnonPipe$GT$$GT$10into_inner17h239cc29da4158a23E
    0000000000000000 T _ZN110_$LT$std..fs..Permissions$u20$as$u20$std..sys_common..FromInner$LT$std..sys..unix..fs..FilePermissions$GT$$GT$10from_inner17ha3db65e7b3148327E
    0000000000000000 T _ZN110_$LT$std..net..tcp..TcpStream$u20$as$u20$std..sys_common..FromInner$LT$std..sys_common..net..TcpStream$GT$$GT$10from_inner17hbb79400cf437f20dE
    0000000000000000 T _ZN110_$LT$std..net..tcp..TcpStream$u20$as$u20$std..sys_common..IntoInner$LT$std..sys_common..net..TcpStream$GT$$GT$10into_inner17h163b962f2a6eb4d9E
    0000000000000000 T _ZN110_$LT$std..net..udp..UdpSocket$u20$as$u20$std..sys_common..FromInner$LT$std..sys_common..net..UdpSocket$GT$$GT$10from_inner17h5cfd430702c9cc88E
    0000000000000000 T _ZN110_$LT$std..net..udp..UdpSocket$u20$as$u20$std..sys_common..IntoInner$LT$std..sys_common..net..UdpSocket$GT$$GT$10into_inner17h0d26198641829835E
    0000000000000000 T _ZN110_$LT$std..process..ChildStderr$u20$as$u20$std..sys_common..FromInner$LT$std..sys..unix..pipe..AnonPipe$GT$$GT$10from_inner17he8c6aa5ad800aa43E
    0000000000000000 T _ZN110_$LT$std..process..ChildStderr$u20$as$u20$std..sys_common..IntoInner$LT$std..sys..unix..pipe..AnonPipe$GT$$GT$10into_inner17h47dcc749374c6657E
    0000000000000000 T _ZN110_$LT$std..process..ChildStdout$u20$as$u20$std..sys_common..FromInner$LT$std..sys..unix..pipe..AnonPipe$GT$$GT$10from_inner17hffb6fe5a0a3dfdaaE
    0000000000000000 T _ZN110_$LT$std..process..ChildStdout$u20$as$u20$std..sys_common..IntoInner$LT$std..sys..unix..pipe..AnonPipe$GT$$GT$10into_inner17h258e7762f553acbdE
    0000000000000000 T _ZN110_$LT$std..sys..unix..ext..net..ancillary..ScmCredentials$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hafd3ccd0c816760eE
    0000000000000000 T _ZN111_$LT$std..io..buffered..bufwriter..BufWriter$LT$W$GT$..flush_buf..BufGuard$u20$as$u20$core..ops..drop..Drop$GT$4drop17h41b18358dc6ccfb4E
    0000000000000000 T _ZN111_$LT$std..sys..unix..process..process_common..CommandArgs$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17h5ded5b4a6081551aE
    0000000000000000 T _ZN111_$LT$std..sys..unix..process..process_common..CommandArgs$u20$as$u20$core..iter..traits..iterator..Iterator$GT$9size_hint17h9dab81d35a73bb5fE
    0000000000000000 T _ZN112_$LT$$LT$std..path..Components$u20$as$u20$core..fmt..Debug$GT$..fmt..DebugHelper$u20$as$u20$core..fmt..Debug$GT$3fmt17h993bfb1fa47adbbcE
    0000000000000000 T _ZN112_$LT$std..net..tcp..TcpListener$u20$as$u20$std..sys_common..AsInner$LT$std..sys_common..net..TcpListener$GT$$GT$8as_inner17h91852d3528f07718E
    0000000000000000 T _ZN113_$LT$std..ffi..c_str..CStr$u20$as$u20$core..ops..index..Index$LT$core..ops..range..RangeFrom$LT$usize$GT$$GT$$GT$5index17h284edcc3b107bdafE
    0000000000000000 T _ZN113_$LT$std..sys_common..net..TcpStream$u20$as$u20$std..sys_common..FromInner$LT$std..sys..unix..net..Socket$GT$$GT$10from_inner17hbdfd80d382eee1adE
    0000000000000000 T _ZN113_$LT$std..sys_common..net..UdpSocket$u20$as$u20$std..sys_common..FromInner$LT$std..sys..unix..net..Socket$GT$$GT$10from_inner17hbe965199a4b5064bE
    0000000000000000 T _ZN114_$LT$$RF$std..sys..unix..ext..net..listener..UnixListener$u20$as$u20$core..iter..traits..collect..IntoIterator$GT$9into_iter17h3a8a7350c1c7fe3dE
    0000000000000000 T _ZN114_$LT$std..net..tcp..TcpListener$u20$as$u20$std..sys_common..FromInner$LT$std..sys_common..net..TcpListener$GT$$GT$10from_inner17h7898e683873df298E
    0000000000000000 T _ZN114_$LT$std..net..tcp..TcpListener$u20$as$u20$std..sys_common..IntoInner$LT$std..sys_common..net..TcpListener$GT$$GT$10into_inner17hcd0a9575c070e2aaE
    0000000000000000 T _ZN114_$LT$std..sys_common..os_str_bytes..Buf$u20$as$u20$std..sys_common..IntoInner$LT$alloc..vec..Vec$LT$u8$GT$$GT$$GT$10into_inner17h4d1beeb66de645c9E
    0000000000000000 T _ZN115_$LT$std..sys_common..net..TcpListener$u20$as$u20$std..sys_common..FromInner$LT$std..sys..unix..net..Socket$GT$$GT$10from_inner17h67e0e93d3d5c9186E
    0000000000000000 T _ZN115_$LT$std..time..SystemTime$u20$as$u20$std..sys_common..FromInner$LT$std..sys..unix..time..inner..SystemTime$GT$$GT$10from_inner17h3852ef15c886226fE
    0000000000000000 T _ZN118_$LT$std..net..addr..SocketAddrV4$u20$as$u20$std..sys_common..FromInner$LT$libc..unix..linux_like..sockaddr_in$GT$$GT$10from_inner17h8b287417f69a45dcE
    0000000000000000 T _ZN118_$LT$std..sys..unix..process..process_common..Stdio$u20$as$u20$core..convert..From$LT$std..sys..unix..fs..File$GT$$GT$4from17hc6bec8a134a86f69E
    0000000000000000 T _ZN119_$LT$std..net..addr..SocketAddrV6$u20$as$u20$std..sys_common..FromInner$LT$libc..unix..linux_like..sockaddr_in6$GT$$GT$10from_inner17hca8907c447e614b9E
    0000000000000000 T _ZN119_$LT$std..process..Child$u20$as$u20$std..sys_common..AsInner$LT$std..sys..unix..process..process_inner..Process$GT$$GT$8as_inner17h88e15e3603a7e76eE
                     U _ZN11miniz_oxide7inflate4core10decompress17h14b50345d601c863E
                     U _ZN11miniz_oxide7inflate4core17DecompressorOxide3new17h0862ef666c0be558E
    0000000000000000 T _ZN120_$LT$std..process..Stdio$u20$as$u20$std..sys_common..FromInner$LT$std..sys..unix..process..process_common..Stdio$GT$$GT$10from_inner17h311420a80cfd0b5dE
    0000000000000000 T _ZN121_$LT$std..process..Child$u20$as$u20$std..sys_common..IntoInner$LT$std..sys..unix..process..process_inner..Process$GT$$GT$10into_inner17hd9ea52da024e5f7eE
    0000000000000000 T _ZN122_$LT$std..process..Command$u20$as$u20$std..sys_common..AsInner$LT$std..sys..unix..process..process_common..Command$GT$$GT$8as_inner17h9a90aa29ebc95f03E
    0000000000000000 T _ZN122_$LT$std..sys..unix..process..process_common..CommandArgs$u20$as$u20$core..iter..traits..exact_size..ExactSizeIterator$GT$3len17hd9397ffdc156a7c7E
    0000000000000000 T _ZN122_$LT$std..sys..unix..process..process_common..CommandArgs$u20$as$u20$core..iter..traits..exact_size..ExactSizeIterator$GT$8is_empty17hb04ea8634c45cb8fE
    0000000000000000 T _ZN124_$LT$std..sys..unix..process..process_common..Stdio$u20$as$u20$core..convert..From$LT$std..sys..unix..pipe..AnonPipe$GT$$GT$4from17ha89e5b662a4a3428E
    0000000000000000 T _ZN125_$LT$std..process..Command$u20$as$u20$std..sys_common..AsInnerMut$LT$std..sys..unix..process..process_common..Command$GT$$GT$12as_inner_mut17h29209e601de6266eE
    0000000000000000 T _ZN127_$LT$std..process..ExitStatus$u20$as$u20$std..sys_common..AsInner$LT$std..sys..unix..process..process_inner..ExitStatus$GT$$GT$8as_inner17h780bd35757f3d50fE
    0000000000000000 T _ZN129_$LT$$LT$std..sync..mutex..Mutex$LT$T$GT$$u20$as$u20$core..fmt..Debug$GT$..fmt..LockedPlaceholder$u20$as$u20$core..fmt..Debug$GT$3fmt17h7b7685f951726faaE
    0000000000000000 T _ZN129_$LT$std..process..ExitStatus$u20$as$u20$std..sys_common..FromInner$LT$std..sys..unix..process..process_inner..ExitStatus$GT$$GT$10from_inner17haa0ac8a7652d5983E
    0000000000000000 T _ZN131_$LT$$LT$std..sync..rwlock..RwLock$LT$T$GT$$u20$as$u20$core..fmt..Debug$GT$..fmt..LockedPlaceholder$u20$as$u20$core..fmt..Debug$GT$3fmt17h3882bc0c0bcf9f13E
    0000000000000000 T _ZN136_$LT$std..sys..unix..fs..FileAttr$u20$as$u20$std..sys_common..AsInner$LT$libc..unix..linux_like..linux..gnu..b64..x86_64..stat64$GT$$GT$8as_inner17h05f40fa88a52bd18E
    0000000000000000 T _ZN145_$LT$$RF$std..net..addr..SocketAddr$u20$as$u20$std..sys_common..IntoInner$LT$$LP$$BP$const$u20$libc..unix..linux_like..sockaddr$C$u32$RP$$GT$$GT$10into_inner17hc92eaafc674ad36cE
                     U _ZN14rustc_demangle12try_demangle17h71e2a263d21b65d0E
                     U _ZN14rustc_demangle8Demangle6as_str17h910192c79a17d80aE
    0000000000000000 T _ZN163_$LT$std..sys..unix..process..process_inner..$LT$impl$u20$std..sys..unix..process..process_common..Command$GT$..do_exec..Reset$u20$as$u20$core..ops..drop..Drop$GT$4drop17hf77cf480c8df1826E
    0000000000000000 T _ZN176_$LT$std..sys..unix..process..process_inner..$LT$impl$u20$std..sys..unix..process..process_common..Command$GT$..posix_spawn..PosixSpawnattr$u20$as$u20$core..ops..drop..Drop$GT$4drop17hac0adddb605dc6ccE
    0000000000000000 T _ZN183_$LT$std..process..Child$u20$as$u20$std..sys_common..FromInner$LT$$LP$std..sys..unix..process..process_inner..Process$C$std..sys..unix..process..process_common..StdioPipes$RP$$GT$$GT$10from_inner17he190b1b81c28c615E
    0000000000000000 T _ZN183_$LT$std..sys..unix..process..process_inner..$LT$impl$u20$std..sys..unix..process..process_common..Command$GT$..posix_spawn..PosixSpawnFileActions$u20$as$u20$core..ops..drop..Drop$GT$4drop17hbfca1a1ba5a18ad5E
    0000000000000000 T _ZN242_$LT$std..error..$LT$impl$u20$core..convert..From$LT$alloc..string..String$GT$$u20$for$u20$alloc..boxed..Box$LT$dyn$u20$std..error..Error$u2b$core..marker..Sync$u2b$core..marker..Send$GT$$GT$..from..StringError$u20$as$u20$core..fmt..Debug$GT$3fmt17habdb8af57a7e2b61E
    0000000000000000 T _ZN243_$LT$std..error..$LT$impl$u20$core..convert..From$LT$alloc..string..String$GT$$u20$for$u20$alloc..boxed..Box$LT$dyn$u20$std..error..Error$u2b$core..marker..Sync$u2b$core..marker..Send$GT$$GT$..from..StringError$u20$as$u20$std..error..Error$GT$11description17h89cb4ac9ca2ff6ecE
    0000000000000000 T _ZN244_$LT$std..error..$LT$impl$u20$core..convert..From$LT$alloc..string..String$GT$$u20$for$u20$alloc..boxed..Box$LT$dyn$u20$std..error..Error$u2b$core..marker..Sync$u2b$core..marker..Send$GT$$GT$..from..StringError$u20$as$u20$core..fmt..Display$GT$3fmt17h6019571529181cadE
    0000000000000000 t _ZN36_$LT$T$u20$as$u20$core..any..Any$GT$7type_id17h060d580da122534bE
    0000000000000000 t _ZN36_$LT$T$u20$as$u20$core..any..Any$GT$7type_id17h16b373c61bda163aE
    0000000000000000 t _ZN36_$LT$T$u20$as$u20$core..any..Any$GT$7type_id17h38b4c4ecd234c448E
    0000000000000000 t _ZN36_$LT$T$u20$as$u20$core..any..Any$GT$7type_id17hd77dd1c9aad9489fE
    0000000000000000 b _ZN3std10sys_common11at_exit_imp4LOCK17h6c064a898299c4e7E
    0000000000000000 b _ZN3std10sys_common11at_exit_imp5QUEUE17hf4585e219ab0571cE
    0000000000000000 t _ZN3std10sys_common11thread_info10ThreadInfo4with28_$u7b$$u7b$closure$u7d$$u7d$17h833b60b5aed8b05fE
    0000000000000000 b _ZN3std10sys_common11thread_info11THREAD_INFO7__getit5__KEY17hc87dac05a8e8ee5eE
    0000000000000000 T _ZN3std10sys_common11thread_info3set17h1ed4f2ca8849b5daE
    0000000000000000 T _ZN3std10sys_common12os_str_bytes3Buf10push_slice17hd177149ec3dab8d9E
    0000000000000000 T _ZN3std10sys_common12os_str_bytes3Buf11from_string17h4e53b47808ef12f2E
    0000000000000000 T _ZN3std10sys_common12os_str_bytes3Buf11into_string17h83a160cd9b3a41ecE
    0000000000000000 T _ZN3std10sys_common12os_str_bytes5Slice10clone_into17h036cc2149a489d1dE
    0000000000000000 T _ZN3std10sys_common12os_str_bytes5Slice15to_string_lossy17h4bb6d802d47c3919E
    0000000000000000 T _ZN3std10sys_common12os_str_bytes5Slice6to_str17hbf999f856a25a221E
    0000000000000000 T _ZN3std10sys_common12os_str_bytes5Slice8to_owned17h9c69f14bdc733d26E
    0000000000000000 T _ZN3std10sys_common12os_str_bytes5Slice9empty_box17h1952de7aa4a81d35E
    0000000000000000 T _ZN3std10sys_common16thread_local_key9StaticKey3new17h32ac13c9f25d6864E
    0000000000000000 T _ZN3std10sys_common16thread_local_key9StaticKey9lazy_init17h283697afc18c04c5E
    0000000000000000 d _ZN3std10sys_common17thread_local_dtor22register_dtor_fallback5DTORS17h3be3e4012eabdddaE
    0000000000000000 t _ZN3std10sys_common17thread_local_dtor22register_dtor_fallback9run_dtors17he785945a5fda7a00E
    0000000000000000 T _ZN3std10sys_common2fs14remove_dir_all17hcd15c5b79df12056E
    0000000000000000 t _ZN3std10sys_common2fs24remove_dir_all_recursive17ha780780f89559c35E
    0000000000000000 T _ZN3std10sys_common3net11TcpListener4bind17h6f6a17a602360777E
    0000000000000000 t _ZN3std10sys_common3net9TcpStream11socket_addr17ha50a64aefe2ee8c8E
    0000000000000000 T _ZN3std10sys_common3net9TcpStream7connect17hebeddbbe1d36617bE
    0000000000000000 t _ZN3std10sys_common3net9TcpStream9peer_addr17hb50eed9af37b54b6E
    0000000000000000 T _ZN3std10sys_common3net9UdpSocket4bind17h1d0934ad27016247E
    0000000000000000 T _ZN3std10sys_common3net9UdpSocket7connect17hd1ecc188b6c0a477E

    ...

En el archivo generado encontramos una gran cantidad de símbolos, no podemos identificarlos, esto es porque
el compilador de rust no solo ha compilado nuestro código sino que ha agregado algunas cosas resultado
de los análisis y optimizaciones que vimos en los ejercicios anteriores. Las funciones que definimos en si se encuentran 
entre estos símbolos, pero su nombre o identificador ha cambiado debido a un proceso llamado **Name Mangling** necesario
para la etapa de linking. Por ejemplo, dos funciones que tengan el mismo nombre pero se encuentren en librerías diferentes
podrían causar que el enlazador enlace los datos de una función en lugar de la otra por error, o simplemente no pueda 
resolverlo y arroje un error.

Podemos ver más detalles sobre los símbolos del programa con:

``readelf -s libsum.so``

Obtendrás esto:

.. code-block:: bash

    File: libsum.a(sum.sum.3a1fbbbh-cgu.0.rcgu.o)

    Symbol table '.symtab' contains 2 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.3a1fbbbh-cgu.0

    File: libsum.a(sum.1yafyrf2uaakrs3o.rcgu.o)

    Symbol table '.symtab' contains 17 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS 1yafyrf2uaakrs3o
         2: 0000000000000000     0 SECTION LOCAL  DEFAULT    3 
         3: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
         4: 0000000000000000     0 SECTION LOCAL  DEFAULT    7 
         5: 0000000000000000     0 SECTION LOCAL  DEFAULT    9 
         6: 0000000000000000     0 SECTION LOCAL  DEFAULT   11 
         7: 0000000000000000     0 NOTYPE  GLOBAL HIDDEN   UND __rdl_alloc
         8: 0000000000000000     0 NOTYPE  GLOBAL HIDDEN   UND __rdl_alloc_zeroed
         9: 0000000000000000     0 NOTYPE  GLOBAL HIDDEN   UND __rdl_dealloc
        10: 0000000000000000     0 NOTYPE  GLOBAL HIDDEN   UND __rdl_realloc
        11: 0000000000000000     0 NOTYPE  GLOBAL HIDDEN   UND __rg_oom
        12: 0000000000000000     5 FUNC    GLOBAL DEFAULT    3 __rust_alloc
        13: 0000000000000000     5 FUNC    GLOBAL DEFAULT   11 __rust_alloc_error_handle
        14: 0000000000000000     5 FUNC    GLOBAL DEFAULT    9 __rust_alloc_zeroed
        15: 0000000000000000     5 FUNC    GLOBAL DEFAULT    5 __rust_dealloc
        16: 0000000000000000     5 FUNC    GLOBAL DEFAULT    7 __rust_realloc

    File: libsum.a(std-c6dddd3d354e6bea.std.9m6hw7w6-cgu.0.rcgu.o)

    Symbol table '.symtab' contains 4798 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS std.9m6hw7w6-cgu.0
         2: 0000000000000230     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1027_0
         3: 0000000000000240     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1027_1
         4: 0000000000000250     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1163_0
         5: 0000000000000260     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1211_0
         6: 0000000000000270     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1212_0
         7: 0000000000000280     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1212_1
         8: 0000000000000290     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1217_0
         9: 00000000000002a0     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1220_0
        10: 00000000000002b0     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1221_0
        11: 00000000000002c0     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1238_0
        12: 00000000000002d0     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1239_0
        13: 00000000000002e0     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1239_1
        14: 00000000000002f0     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1248_0
        15: 0000000000000300     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1262_0
        16: 0000000000000310     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1262_1
        17: 0000000000000320     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1273_0
        18: 0000000000000340     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1343_0
        19: 0000000000000350     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI1344_0
        20: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI228_0
        21: 0000000000000010     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI294_0
        22: 0000000000000020     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI305_0
        23: 0000000000000040     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI313_0
        24: 0000000000000050     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI315_0
        25: 0000000000000060     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI330_0
        26: 0000000000000070     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI349_0
        27: 0000000000000080     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI349_1
        28: 0000000000000090     0 NOTYPE  LOCAL  DEFAULT  470 .LCPI350_0

        ...

        File: libsum.a(compiler_builtins-8b33f9cbbc9652fe.compiler_builtins.84hxjowu-cgu.0.rcgu.o)

    Symbol table '.symtab' contains 9 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS compiler_builtins.84hxjow
         2: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
         3: 0000000000000000     0 SECTION LOCAL  DEFAULT    6 
         4: 0000000000000000     0 SECTION LOCAL  DEFAULT    7 
         5: 0000000000000000     0 SECTION LOCAL  DEFAULT   11 
         6: 0000000000000000     0 SECTION LOCAL  DEFAULT   17 
         7: 0000000000000000     0 SECTION LOCAL  DEFAULT   19 
         8: 0000000000000000    42 FUNC    GLOBAL HIDDEN     5 __unordsf2

    File: libsum.a(compiler_builtins-8b33f9cbbc9652fe.compiler_builtins.84hxjowu-cgu.1.rcgu.o)

    Symbol table '.symtab' contains 10 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS compiler_builtins.84hxjow
         2: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
         3: 0000000000000000     0 SECTION LOCAL  DEFAULT    6 
         4: 0000000000000000     0 SECTION LOCAL  DEFAULT    7 
         5: 0000000000000000     0 SECTION LOCAL  DEFAULT   11 
         6: 0000000000000000     0 SECTION LOCAL  DEFAULT   12 
         7: 0000000000000000     0 SECTION LOCAL  DEFAULT   18 
         8: 0000000000000000     0 SECTION LOCAL  DEFAULT   20 
         9: 0000000000000000   173 FUNC    GLOBAL HIDDEN     5 __floatsisf

    File: libsum.a(compiler_builtins-8b33f9cbbc9652fe.compiler_builtins.84hxjowu-cgu.10.rcgu.o)

    Symbol table '.symtab' contains 9 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS compiler_builtins.84hxjow
         2: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
         3: 0000000000000000     0 SECTION LOCAL  DEFAULT    6 
         4: 0000000000000000     0 SECTION LOCAL  DEFAULT    7 
         5: 0000000000000000     0 SECTION LOCAL  DEFAULT   11 
         6: 0000000000000000     0 SECTION LOCAL  DEFAULT   17 
         7: 0000000000000000     0 SECTION LOCAL  DEFAULT   19 
         8: 0000000000000000    83 FUNC    GLOBAL HIDDEN     5 __rust_u128_shlo

    File: libsum.a(compiler_builtins-8b33f9cbbc9652fe.compiler_builtins.84hxjowu-cgu.100.rcgu.o)

    Symbol table '.symtab' contains 11 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS compiler_builtins.84hxjow
         2: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT    5 .LCPI0_0
         3: 0000000000000000     0 SECTION LOCAL  DEFAULT    6 
         4: 0000000000000000     0 SECTION LOCAL  DEFAULT    8 
         5: 0000000000000000     0 SECTION LOCAL  DEFAULT    9 
         6: 0000000000000000     0 SECTION LOCAL  DEFAULT   13 
         7: 0000000000000000     0 SECTION LOCAL  DEFAULT   14 
         8: 0000000000000000     0 SECTION LOCAL  DEFAULT   20 
         9: 0000000000000000     0 SECTION LOCAL  DEFAULT   22 
        10: 0000000000000000   112 FUNC    GLOBAL HIDDEN     6 __powidf2

    File: libsum.a(compiler_builtins-8b33f9cbbc9652fe.compiler_builtins.84hxjowu-cgu.101.rcgu.o)

    Symbol table '.symtab' contains 10 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS compiler_builtins.84hxjow
         2: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
         3: 0000000000000000     0 SECTION LOCAL  DEFAULT    6 
         4: 0000000000000000     0 SECTION LOCAL  DEFAULT    7 
         5: 0000000000000000     0 SECTION LOCAL  DEFAULT   11 
         6: 0000000000000000     0 SECTION LOCAL  DEFAULT   12 
         7: 0000000000000000     0 SECTION LOCAL  DEFAULT   18 
         8: 0000000000000000     0 SECTION LOCAL  DEFAULT   20 
         9: 0000000000000000    77 FUNC    GLOBAL HIDDEN     5 __ltsf2

    ...
    
Nota varias cosas interesantes:

* La dirección asociada a los símbolos suma y sumatoria es relativa a 0. Esto ocurrirá
  con cada relocatable object file. Por tanto será responsabilidad del enlazador ubicar
  los símbolos en una dirección apropiada una vez se mezclen los archivos para formar
  el ejecutable.
* Hay algunos símbolos marcados como LOCAL y otros GLOBAL. Que sea GLOBAL indica que son visibles al momento de combinarlos con otros relocatable
  object files.

Ya hemos dicho en varias oportunidades que los relocatable object files incluyen
el código de máquina del programa. Lo puedes observar con el siguientes comando:

``objdump -d libsum.a``

.. code-block:: bash

    In archive libsum.a:

    sum.sum.3a1fbbbh-cgu.0.rcgu.o:     file format elf64-x86-64


    sum.1yafyrf2uaakrs3o.rcgu.o:     file format elf64-x86-64


    Disassembly of section .text.__rust_alloc:

    0000000000000000 <__rust_alloc>:
       0:	e9 00 00 00 00       	jmpq   5 <__rust_alloc+0x5>

    Disassembly of section .text.__rust_dealloc:

    0000000000000000 <__rust_dealloc>:
       0:	e9 00 00 00 00       	jmpq   5 <__rust_dealloc+0x5>

    Disassembly of section .text.__rust_realloc:

    0000000000000000 <__rust_realloc>:
       0:	e9 00 00 00 00       	jmpq   5 <__rust_realloc+0x5>

    Disassembly of section .text.__rust_alloc_zeroed:

    0000000000000000 <__rust_alloc_zeroed>:
       0:	e9 00 00 00 00       	jmpq   5 <__rust_alloc_zeroed+0x5>

    Disassembly of section .text.__rust_alloc_error_handler:

    0000000000000000 <__rust_alloc_error_handler>:
       0:	e9 00 00 00 00       	jmpq   5 <__rust_alloc_error_handler+0x5>

    std-c6dddd3d354e6bea.std.9m6hw7w6-cgu.0.rcgu.o:     file format elf64-x86-64


    Disassembly of section .text._ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E:

    0000000000000000 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E>:
       0:	55                   	push   %rbp
       1:	41 57                	push   %r15
       3:	41 56                	push   %r14
       5:	41 55                	push   %r13
       7:	41 54                	push   %r12
       9:	53                   	push   %rbx
       a:	48 83 ec 18          	sub    $0x18,%rsp
       e:	b0 02                	mov    $0x2,%al
      10:	80 7f 41 00          	cmpb   $0x0,0x41(%rdi)
      14:	74 05                	je     1b <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1b>
      16:	e9 18 02 00 00       	jmpq   233 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x233>
      1b:	48 89 fb             	mov    %rdi,%rbx
      1e:	4c 8b 7f 10          	mov    0x10(%rdi),%r15
      22:	48 8b 6f 20          	mov    0x20(%rdi),%rbp
      26:	4c 8b 77 28          	mov    0x28(%rdi),%r14
      2a:	4c 89 f2             	mov    %r14,%rdx
      2d:	48 29 ea             	sub    %rbp,%rdx
      30:	0f 82 c5 01 00 00    	jb     1fb <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1fb>
      36:	48 8b 43 18          	mov    0x18(%rbx),%rax
      3a:	48 89 44 24 08       	mov    %rax,0x8(%rsp)
      3f:	4c 39 f0             	cmp    %r14,%rax
      42:	0f 82 b3 01 00 00    	jb     1fb <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1fb>
      48:	4c 8b 63 30          	mov    0x30(%rbx),%r12
      4c:	49 83 fc 04          	cmp    $0x4,%r12
      50:	0f 86 d0 00 00 00    	jbe    126 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x126>
      56:	4c 8b 2d 00 00 00 00 	mov    0x0(%rip),%r13        # 5d <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x5d>
      5d:	eb 0d                	jmp    6c <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x6c>
      5f:	90                   	nop
      60:	4c 89 f2             	mov    %r14,%rdx
      63:	48 29 ea             	sub    %rbp,%rdx
      66:	0f 82 8f 01 00 00    	jb     1fb <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1fb>
      6c:	49 8d 34 2f          	lea    (%r15,%rbp,1),%rsi
      70:	42 8a 44 23 3b       	mov    0x3b(%rbx,%r12,1),%al
      75:	48 83 fa 10          	cmp    $0x10,%rdx
      79:	73 35                	jae    b0 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0xb0>
      7b:	48 85 d2             	test   %rdx,%rdx
      7e:	74 41                	je     c1 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0xc1>
      80:	31 c9                	xor    %ecx,%ecx
      82:	66 2e 0f 1f 84 00 00 	nopw   %cs:0x0(%rax,%rax,1)
      89:	00 00 00 
      8c:	0f 1f 40 00          	nopl   0x0(%rax)
      90:	38 04 0e             	cmp    %al,(%rsi,%rcx,1)
      93:	74 3b                	je     d0 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0xd0>
      95:	48 83 c1 01          	add    $0x1,%rcx
      99:	48 39 ca             	cmp    %rcx,%rdx
      9c:	75 f2                	jne    90 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x90>
      9e:	31 c0                	xor    %eax,%eax
      a0:	48 83 f8 01          	cmp    $0x1,%rax
      a4:	74 4a                	je     f0 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0xf0>
      a6:	e9 4c 01 00 00       	jmpq   1f7 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1f7>
      ab:	0f 1f 44 00 00       	nopl   0x0(%rax,%rax,1)
      b0:	0f b6 f8             	movzbl %al,%edi
      b3:	41 ff d5             	callq  *%r13
      b6:	48 83 f8 01          	cmp    $0x1,%rax
      ba:	74 34                	je     f0 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0xf0>
      bc:	e9 36 01 00 00       	jmpq   1f7 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1f7>
      c1:	31 d2                	xor    %edx,%edx
      c3:	31 c0                	xor    %eax,%eax
      c5:	48 83 f8 01          	cmp    $0x1,%rax
      c9:	74 25                	je     f0 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0xf0>
      cb:	e9 27 01 00 00       	jmpq   1f7 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1f7>
      d0:	b8 01 00 00 00       	mov    $0x1,%eax
      d5:	48 89 ca             	mov    %rcx,%rdx
      d8:	48 83 f8 01          	cmp    $0x1,%rax
      dc:	0f 85 15 01 00 00    	jne    1f7 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1f7>
      e2:	66 2e 0f 1f 84 00 00 	nopw   %cs:0x0(%rax,%rax,1)
      e9:	00 00 00 
      ec:	0f 1f 40 00          	nopl   0x0(%rax)
      f0:	48 01 d5             	add    %rdx,%rbp
      f3:	48 83 c5 01          	add    $0x1,%rbp
      f7:	48 89 6b 20          	mov    %rbp,0x20(%rbx)
      fb:	4c 39 e5             	cmp    %r12,%rbp
      fe:	0f 82 5c ff ff ff    	jb     60 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x60>
     104:	48 39 6c 24 08       	cmp    %rbp,0x8(%rsp)
     109:	0f 82 51 ff ff ff    	jb     60 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x60>
     10f:	48 8d 15 00 00 00 00 	lea    0x0(%rip),%rdx        # 116 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x116>
     116:	be 04 00 00 00       	mov    $0x4,%esi
     11b:	4c 89 e7             	mov    %r12,%rdi
     11e:	ff 15 00 00 00 00    	callq  *0x0(%rip)        # 124 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x124>
     124:	0f 0b                	ud2    
     126:	48 8d 43 3c          	lea    0x3c(%rbx),%rax
     12a:	48 89 44 24 10       	mov    %rax,0x10(%rsp)
     12f:	eb 1b                	jmp    14c <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x14c>
     131:	66 2e 0f 1f 84 00 00 	nopw   %cs:0x0(%rax,%rax,1)
     138:	00 00 00 
     13b:	0f 1f 44 00 00       	nopl   0x0(%rax,%rax,1)
     140:	4c 89 f2             	mov    %r14,%rdx
     143:	48 29 ea             	sub    %rbp,%rdx
     146:	0f 82 af 00 00 00    	jb     1fb <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1fb>
     14c:	49 8d 34 2f          	lea    (%r15,%rbp,1),%rsi
     150:	42 8a 44 23 3b       	mov    0x3b(%rbx,%r12,1),%al
     155:	48 83 fa 0f          	cmp    $0xf,%rdx
     159:	77 35                	ja     190 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x190>
     15b:	31 c9                	xor    %ecx,%ecx
     15d:	48 85 d2             	test   %rdx,%rdx
     160:	74 1f                	je     181 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x181>
     162:	66 2e 0f 1f 84 00 00 	nopw   %cs:0x0(%rax,%rax,1)
     169:	00 00 00 
     16c:	0f 1f 40 00          	nopl   0x0(%rax)
     170:	38 04 0e             	cmp    %al,(%rsi,%rcx,1)
     173:	74 2f                	je     1a4 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1a4>
     175:	48 83 c1 01          	add    $0x1,%rcx
     179:	48 39 ca             	cmp    %rcx,%rdx
     17c:	75 f2                	jne    170 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x170>
     17e:	48 89 d1             	mov    %rdx,%rcx
     181:	31 c0                	xor    %eax,%eax
     183:	48 83 f8 01          	cmp    $0x1,%rax
     187:	74 27                	je     1b0 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1b0>
     189:	eb 6c                	jmp    1f7 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1f7>
     18b:	0f 1f 44 00 00       	nopl   0x0(%rax,%rax,1)
     190:	0f b6 f8             	movzbl %al,%edi
     193:	ff 15 00 00 00 00    	callq  *0x0(%rip)        # 199 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x199>
     199:	48 89 d1             	mov    %rdx,%rcx
     19c:	48 83 f8 01          	cmp    $0x1,%rax
     1a0:	74 0e                	je     1b0 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1b0>
     1a2:	eb 53                	jmp    1f7 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1f7>
     1a4:	b8 01 00 00 00       	mov    $0x1,%eax
     1a9:	48 83 f8 01          	cmp    $0x1,%rax
     1ad:	75 48                	jne    1f7 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1f7>
     1af:	90                   	nop
     1b0:	48 01 cd             	add    %rcx,%rbp
     1b3:	48 83 c5 01          	add    $0x1,%rbp
     1b7:	48 89 6b 20          	mov    %rbp,0x20(%rbx)
     1bb:	49 89 ed             	mov    %rbp,%r13
     1be:	4d 29 e5             	sub    %r12,%r13
     1c1:	0f 82 79 ff ff ff    	jb     140 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x140>
     1c7:	48 39 6c 24 08       	cmp    %rbp,0x8(%rsp)
     1cc:	0f 82 6e ff ff ff    	jb     140 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x140>
     1d2:	4b 8d 3c 2f          	lea    (%r15,%r13,1),%rdi
     1d6:	48 8b 74 24 10       	mov    0x10(%rsp),%rsi
     1db:	4c 89 e2             	mov    %r12,%rdx
     1de:	ff 15 00 00 00 00    	callq  *0x0(%rip)        # 1e4 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x1e4>
     1e4:	85 c0                	test   %eax,%eax
     1e6:	0f 85 54 ff ff ff    	jne    140 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x140>
     1ec:	48 8b 03             	mov    (%rbx),%rax
     1ef:	49 29 c5             	sub    %rax,%r13
     1f2:	48 89 2b             	mov    %rbp,(%rbx)
     1f5:	eb 21                	jmp    218 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x218>
     1f7:	4c 89 73 20          	mov    %r14,0x20(%rbx)
     1fb:	80 7b 40 00          	cmpb   $0x0,0x40(%rbx)
     1ff:	48 8b 03             	mov    (%rbx),%rax
     202:	4c 8b 6b 08          	mov    0x8(%rbx),%r13
     206:	75 09                	jne    211 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x211>
     208:	49 39 c5             	cmp    %rax,%r13
     20b:	75 04                	jne    211 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x211>
     20d:	b0 02                	mov    $0x2,%al
     20f:	eb 22                	jmp    233 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x233>
     211:	c6 43 41 01          	movb   $0x1,0x41(%rbx)
     215:	49 29 c5             	sub    %rax,%r13
     218:	49 01 c7             	add    %rax,%r15
     21b:	4c 89 ff             	mov    %r15,%rdi
     21e:	4c 89 ee             	mov    %r13,%rsi
     221:	ff 15 00 00 00 00    	callq  *0x0(%rip)        # 227 <_ZN100_$LT$core..iter..adapters..fuse..Fuse$LT$I$GT$$u20$as$u20$core..iter..traits..iterator..Iterator$GT$4next17hb3cd5fb68302d125E+0x227>
     227:	48 89 d1             	mov    %rdx,%rcx
     22a:	48 c1 e9 08          	shr    $0x8,%rcx
     22e:	48 0f a4 c2 38       	shld   $0x38,%rax,%rdx
     233:	48 0f a4 d1 08       	shld   $0x8,%rdx,%rcx
     238:	48 c1 e2 08          	shl    $0x8,%rdx
     23c:	0f b6 c0             	movzbl %al,%eax
     23f:	48 09 d0             	or     %rdx,%rax
     242:	48 89 ca             	mov    %rcx,%rdx
     245:	48 83 c4 18          	add    $0x18,%rsp
     249:	5b                   	pop    %rbx
     24a:	41 5c                	pop    %r12
     24c:	41 5d                	pop    %r13
     24e:	41 5e                	pop    %r14
     250:	41 5f                	pop    %r15
     252:	5d                   	pop    %rbp
     253:	c3                   	retq   

    Disassembly of section .text._ZN36_$LT$T$u20$as$u20$core..any..Any$GT$7type_id17h060d580da122534bE:

    0000000000000000 <_ZN36_$LT$T$u20$as$u20$core..any..Any$GT$7type_id17h060d580da122534bE>:
       0:	48 b8 04 cb 36 d0 05 	movabs $0x68c68305d036cb04,%rax
       7:	83 c6 68 
       a:	c3                   	retq   

    Disassembly of section .text._ZN36_$LT$T$u20$as$u20$core..any..Any$GT$7type_id17h16b373c61bda163aE:

    0000000000000000 <_ZN36_$LT$T$u20$as$u20$core..any..Any$GT$7type_id17h16b373c61bda163aE>:
       0:	48 b8 f2 09 f7 9f 24 	movabs $0xb9ca6a249ff709f2,%rax
       7:	6a ca b9 
       a:	c3                   	retq   

    Disassembly of section .text._ZN36_$LT$T$u20$as$u20$core..any..Any$GT$7type_id17h38b4c4ecd234c448E:

    0000000000000000 <_ZN36_$LT$T$u20$as$u20$core..any..Any$GT$7type_id17h38b4c4ecd234c448E>:
       0:	48 b8 1f 5f e7 3e 03 	movabs $0x2c628e033ee75f1f,%rax
       7:	8e 62 2c 
       a:	c3                   	retq   

    ...

Recuerdas cuando programaste en ensamblador? Mira de nuevo el código anterior.
Ahí tienes código ensamblador y su equivalente código de máquina para
el procesador de tu computador.

No tiene mucho sentido analizar los símbolos y aprender de linking con
los resultados de un programa de Rust pues no son fáciles de entender, los 
próximos ejemplos serán en C, que no hace name mangling, para que podamos ver más fácilmente los cambios
del programa reflejados en los símbolos.

Ahora vamos a realizar otro ejemplo donde verás cómo se combinan varios
relocatable object files para producir un ejecutable:

file1.h:

.. code-block:: c
   :linenos:

    #ifndef _FILE1_H
    #define _FILE1_H

    int suma(int, int);
    int multiplicacion(int, int);

    #endif

file2.c:

.. code-block:: c
   :linenos:

    int suma(int a, int b){
        return (a+b);
    }

file3.c:

.. code-block:: c
   :linenos:

    int multiplicacion(int a, int b){
        return a*b;
    }

main.c:

.. code-block:: c
   :linenos:

    #include "file1.h"

    int main(int argc, char* argv[]) {
        int a = suma(4, 5);
        int b = multiplicacion(9, a);
        return b;
    }

Nota que ``main.c`` debe incluir ``file.h`` donde están las declaraciones de
las funciones suma y multiplicacion. Esto es necesario en C para poder
utilizar las funciones. 

Vamos a compilar los programas:

``gcc -Wall -c file2.c -o file2.o``

``gcc -Wall -c file3.c -o file3.o``

``gcc -Wall -c main.c -o main.o``

Ahora observamos de nuevo las tablas de símbolos de cada relocatable object file:

.. code-block:: bash

    $ readelf -s file2.o

    Symbol table '.symtab' contains 10 entries:
          Num:    Value          Size Type    Bind   Vis      Ndx Name
            0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
            1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS file2.c
            2: 0000000000000000     0 SECTION LOCAL  DEFAULT    1 
            3: 0000000000000000     0 SECTION LOCAL  DEFAULT    2 
            4: 0000000000000000     0 SECTION LOCAL  DEFAULT    3 
            5: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
            6: 0000000000000000     0 SECTION LOCAL  DEFAULT    6 
            7: 0000000000000000     0 SECTION LOCAL  DEFAULT    7 
            8: 0000000000000000     0 SECTION LOCAL  DEFAULT    4 
            9: 0000000000000000    24 FUNC    GLOBAL DEFAULT    1 suma

    $ readelf -s file3.o

    Symbol table '.symtab' contains 10 entries:
          Num:    Value          Size Type    Bind   Vis      Ndx Name
            0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
            1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS file3.c
            2: 0000000000000000     0 SECTION LOCAL  DEFAULT    1 
            3: 0000000000000000     0 SECTION LOCAL  DEFAULT    2 
            4: 0000000000000000     0 SECTION LOCAL  DEFAULT    3 
            5: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
            6: 0000000000000000     0 SECTION LOCAL  DEFAULT    6 
            7: 0000000000000000     0 SECTION LOCAL  DEFAULT    7 
            8: 0000000000000000     0 SECTION LOCAL  DEFAULT    4 
            9: 0000000000000000    23 FUNC    GLOBAL DEFAULT    1 multiplicacion

    $ readelf -s main.o

    Symbol table '.symtab' contains 13 entries:
          Num:    Value          Size Type    Bind   Vis      Ndx Name
            0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
            1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS main.c
            2: 0000000000000000     0 SECTION LOCAL  DEFAULT    1 
            3: 0000000000000000     0 SECTION LOCAL  DEFAULT    3 
            4: 0000000000000000     0 SECTION LOCAL  DEFAULT    4 
            5: 0000000000000000     0 SECTION LOCAL  DEFAULT    6 
            6: 0000000000000000     0 SECTION LOCAL  DEFAULT    7 
            7: 0000000000000000     0 SECTION LOCAL  DEFAULT    8 
            8: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
            9: 0000000000000000    60 FUNC    GLOBAL DEFAULT    1 main
            10: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND _GLOBAL_OFFSET_TABLE_
            11: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND suma
            12: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND multiplicacion

Puedes ver que en la tabla de símbolos de main.o, suma y multiplicacion
se marcan como GLOBAL y muestra que no están definidos (UND), es decir, no
sabemos dónde está el código de ambas funciones.

Ahora necesitamos pasar estos tres archivo ``.o`` al enlazador para
unirlos y generar el ejecutable:

``gcc -Wall file2.o file3.o main.o -o exe``

El ejecutable se generó correctamente. Incluso puedes ejecutarlo. Puedes
ver el valor retornado por la función main con el comando echo $?

Recuerdas que en un ejercicio anterior te comenté que el punto de entrada
de un archivo ejecutable no es la función ``main``, sino otro punto que 
tendrá definidas las instrucciones necesarias para preparar el llamado a main.
¿Dónde está el código que hace lo anterior? si ejecutas el comando 
``readelf -d exe | grep '(NEEDED)'``

.. code-block:: c

     0x0000000000000001 (NEEDED)             Shared library: [libc.so.6]

Observarás que nuestro ejecutable exe dependerá de una biblioteca dinámica
llamada ``libc``. El enlazado con esta biblioteca lo hace por nosotros gcc
y como ya te habrás dado cuenta esta biblioteca incluye el código de entrada
que prepará el entorno del programa para poder llamar a la función main.

Modifica el archivo main.c:

.. code-block:: c
   :linenos:

    #include "file1.h"
    #include <stdio.h>
    
    int main(int argc, char* argv[]) {
        int a = suma(4, 5);
        int b = multiplicacion(9, a);
        printf("b value is: %d",b);
        return 0;
    }

Compila de nuevo el archivo main.c. ``gcc -Wall -c main.c -o main.o``. Observa
la tabla de símbolos:

.. code-block:: bash

    readelf -s main.o

    Symbol table '.symtab' contains 15 entries:
          Num:    Value          Size Type    Bind   Vis      Ndx Name
            0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
            1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS main.c
            2: 0000000000000000     0 SECTION LOCAL  DEFAULT    1 
            3: 0000000000000000     0 SECTION LOCAL  DEFAULT    3 
            4: 0000000000000000     0 SECTION LOCAL  DEFAULT    4 
            5: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
            6: 0000000000000000     0 SECTION LOCAL  DEFAULT    7 
            7: 0000000000000000     0 SECTION LOCAL  DEFAULT    8 
            8: 0000000000000000     0 SECTION LOCAL  DEFAULT    9 
            9: 0000000000000000     0 SECTION LOCAL  DEFAULT    6 
            10: 0000000000000000    84 FUNC    GLOBAL DEFAULT    1 main
            11: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND _GLOBAL_OFFSET_TABLE_
            12: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND suma
            13: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND multiplicacion
            14: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND printf

Nota que ahora aparece como un símbolo global la función printf. Además
dice que no está definido el símbolo

Genera el ejecutable: ``gcc -Wall file2.o file3.o main.o -o exe``. Observa que no
salió error. Quiere decir que el enlazador encontró la definición del símbolo
printf. ¿Pero dónde? ejecuta de nuevo: ``readelf -d exe | grep '(NEEDED)'``

.. code-block:: c
    
    0x0000000000000001 (NEEDED)             Shared library: [libc.so.6]

Ah!!! la definición de printf también está en la biblioteca libc. Solo
por curiosidad, ¿En dónde está la biblioteca? ejecuta ``whereis libc.so.6``

.. code-block:: c

    libc.so: /usr/lib/x86_64-linux-gnu/libc.so.6 /usr/lib/x86_64-linux-gnu/libc.so

Ejercicio 36
^^^^^^^^^^^^^^

El ejercicio anterior va muy largo, pero podemos seguir experimentando:

Prueba ahora haciendo esto ``gcc -Wall file2.o main.o``

Obtendrás esto:

.. code-block:: c

    /usr/bin/ld: main.o: in function main:
    main.c:(.text+0x30): undefined reference to multiplicacion
    collect2: error: ld returned 1 exit status

¿Qué pasó? en este caso el enlazador no encontró el símbolo multiplicacion
definido en ninguna parte y por tanto no es posible generar el ejecutable.

Los símbolos suma y multiplicacion los tenemos definidos. Entonces que tal
si hacemos esto: ``gcc -Wall file2.o file3.o`` ¿Obtenemos un ejecutable?

.. code-block:: c

    /usr/bin/ld: /usr/lib/gcc/x86_64-linux-gnu/9/../../../x86_64-linux-gnu/Scrt1.o: in function _start:
    (.text+0x24): undefined reference to main
    collect2: error: ld returned 1 exit status

¿Qué pasó? Muy interesante, nota que para generar el ejecutable el enlazador
está mezclando nuestro código con otro relocatable object file: ``Scrt1.o``. En
este archivo hay una función llamada ``_start``. Lo que acabamos de descubrir
es que esa función está llamando a la función main. ¿Pero dónde está la función main? pues
nota que al generar el ejecutable no le entregamos al enlazador ningún archivo con
la definición de main. Por tanto, el enlazador no puede generar el ejecutable.

Ejercicio 37
^^^^^^^^^^^^^^

En el ejercicio anterior vimos que nuestro programa está llamando a la función _start quien
luego llama a la función main. Vimos que la función _start el enlazador la toma del
archivo Scrt1.o. ¿Podemos ver el código ensamblador final del programa?

Ejecuta estos comandos:

``objdump -f ex`` 

Este comando te permitirá ver la dirección en la cuál iniciará la ejecución de nuestro programa:

.. code-block:: c

    exe:     file format elf64-x86-64
    architecture: i386:x86-64, flags 0x00000150:
    HAS_SYMS, DYNAMIC, D_PAGED
    start address 0x0000000000001060

El programa arranca en la dirección ``0x0000000000001060``. Ejecuta: ``objdump --disassemble exe``
y podrás ver que en esa dirección efectivamente está la función ``_start``

.. code-block:: bash

    Disassembly of section .init:

    0000000000001000 <_init>:
        1000:	f3 0f 1e fa          	endbr64 
        1004:	48 83 ec 08          	sub    $0x8,%rsp
        1008:	48 8b 05 d9 2f 00 00 	mov    0x2fd9(%rip),%rax        # 3fe8 <__gmon_start__>
        100f:	48 85 c0             	test   %rax,%rax
        1012:	74 02                	je     1016 <_init+0x16>
        1014:	ff d0                	callq  *%rax
        1016:	48 83 c4 08          	add    $0x8,%rsp
        101a:	c3                   	retq   

    Disassembly of section .plt:

    0000000000001020 <.plt>:
        1020:	ff 35 9a 2f 00 00    	pushq  0x2f9a(%rip)        # 3fc0 <_GLOBAL_OFFSET_TABLE_+0x8>
        1026:	f2 ff 25 9b 2f 00 00 	bnd jmpq *0x2f9b(%rip)        # 3fc8 <_GLOBAL_OFFSET_TABLE_+0x10>
        102d:	0f 1f 00             	nopl   (%rax)
        1030:	f3 0f 1e fa          	endbr64 
        1034:	68 00 00 00 00       	pushq  $0x0
        1039:	f2 e9 e1 ff ff ff    	bnd jmpq 1020 <.plt>
        103f:	90                   	nop

    Disassembly of section .plt.got:

    0000000000001040 <__cxa_finalize@plt>:
        1040:	f3 0f 1e fa          	endbr64 
        1044:	f2 ff 25 ad 2f 00 00 	bnd jmpq *0x2fad(%rip)        # 3ff8 <__cxa_finalize@GLIBC_2.2.5>
        104b:	0f 1f 44 00 00       	nopl   0x0(%rax,%rax,1)

    Disassembly of section .plt.sec:

    0000000000001050 <printf@plt>:
        1050:	f3 0f 1e fa          	endbr64 
        1054:	f2 ff 25 75 2f 00 00 	bnd jmpq *0x2f75(%rip)        # 3fd0 <printf@GLIBC_2.2.5>
        105b:	0f 1f 44 00 00       	nopl   0x0(%rax,%rax,1)

    Disassembly of section .text:

    0000000000001060 <_start>:
        1060:	f3 0f 1e fa          	endbr64 
        1064:	31 ed                	xor    %ebp,%ebp
        1066:	49 89 d1             	mov    %rdx,%r9
        1069:	5e                   	pop    %rsi
        106a:	48 89 e2             	mov    %rsp,%rdx
        106d:	48 83 e4 f0          	and    $0xfffffffffffffff0,%rsp
        1071:	50                   	push   %rax
        1072:	54                   	push   %rsp
        1073:	4c 8d 05 c6 01 00 00 	lea    0x1c6(%rip),%r8        # 1240 <__libc_csu_fini>
        107a:	48 8d 0d 4f 01 00 00 	lea    0x14f(%rip),%rcx        # 11d0 <__libc_csu_init>
        1081:	48 8d 3d f0 00 00 00 	lea    0xf0(%rip),%rdi        # 1178 <main>
        1088:	ff 15 52 2f 00 00    	callq  *0x2f52(%rip)        # 3fe0 <__libc_start_main@GLIBC_2.2.5>
        108e:	f4                   	hlt    
        108f:	90                   	nop

    0000000000001090 <deregister_tm_clones>:
        1090:	48 8d 3d 79 2f 00 00 	lea    0x2f79(%rip),%rdi        # 4010 <__TMC_END__>
        1097:	48 8d 05 72 2f 00 00 	lea    0x2f72(%rip),%rax        # 4010 <__TMC_END__>
        109e:	48 39 f8             	cmp    %rdi,%rax
        10a1:	74 15                	je     10b8 <deregister_tm_clones+0x28>
        10a3:	48 8b 05 2e 2f 00 00 	mov    0x2f2e(%rip),%rax        # 3fd8 <_ITM_deregisterTMCloneTable>
        10aa:	48 85 c0             	test   %rax,%rax
        10ad:	74 09                	je     10b8 <deregister_tm_clones+0x28>
        10af:	ff e0                	jmpq   *%rax
        10b1:	0f 1f 80 00 00 00 00 	nopl   0x0(%rax)
        10b8:	c3                   	retq   
        10b9:	0f 1f 80 00 00 00 00 	nopl   0x0(%rax)

    00000000000010c0 <register_tm_clones>:
        10c0:	48 8d 3d 49 2f 00 00 	lea    0x2f49(%rip),%rdi        # 4010 <__TMC_END__>
        10c7:	48 8d 35 42 2f 00 00 	lea    0x2f42(%rip),%rsi        # 4010 <__TMC_END__>
        10ce:	48 29 fe             	sub    %rdi,%rsi
        10d1:	48 89 f0             	mov    %rsi,%rax
        10d4:	48 c1 ee 3f          	shr    $0x3f,%rsi
        10d8:	48 c1 f8 03          	sar    $0x3,%rax
        10dc:	48 01 c6             	add    %rax,%rsi
        10df:	48 d1 fe             	sar    %rsi
        10e2:	74 14                	je     10f8 <register_tm_clones+0x38>
        10e4:	48 8b 05 05 2f 00 00 	mov    0x2f05(%rip),%rax        # 3ff0 <_ITM_registerTMCloneTable>
        10eb:	48 85 c0             	test   %rax,%rax
        10ee:	74 08                	je     10f8 <register_tm_clones+0x38>
        10f0:	ff e0                	jmpq   *%rax
        10f2:	66 0f 1f 44 00 00    	nopw   0x0(%rax,%rax,1)
        10f8:	c3                   	retq   
        10f9:	0f 1f 80 00 00 00 00 	nopl   0x0(%rax)

    0000000000001100 <__do_global_dtors_aux>:
        1100:	f3 0f 1e fa          	endbr64 
        1104:	80 3d 05 2f 00 00 00 	cmpb   $0x0,0x2f05(%rip)        # 4010 <__TMC_END__>
        110b:	75 2b                	jne    1138 <__do_global_dtors_aux+0x38>
        110d:	55                   	push   %rbp
        110e:	48 83 3d e2 2e 00 00 	cmpq   $0x0,0x2ee2(%rip)        # 3ff8 <__cxa_finalize@GLIBC_2.2.5>
        1115:	00 
        1116:	48 89 e5             	mov    %rsp,%rbp
        1119:	74 0c                	je     1127 <__do_global_dtors_aux+0x27>
        111b:	48 8b 3d e6 2e 00 00 	mov    0x2ee6(%rip),%rdi        # 4008 <__dso_handle>
        1122:	e8 19 ff ff ff       	callq  1040 <__cxa_finalize@plt>
        1127:	e8 64 ff ff ff       	callq  1090 <deregister_tm_clones>
        112c:	c6 05 dd 2e 00 00 01 	movb   $0x1,0x2edd(%rip)        # 4010 <__TMC_END__>
        1133:	5d                   	pop    %rbp
        1134:	c3                   	retq   
        1135:	0f 1f 00             	nopl   (%rax)
        1138:	c3                   	retq   
        1139:	0f 1f 80 00 00 00 00 	nopl   0x0(%rax)

    0000000000001140 <frame_dummy>:
        1140:	f3 0f 1e fa          	endbr64 
        1144:	e9 77 ff ff ff       	jmpq   10c0 <register_tm_clones>

    0000000000001149 <suma>:
        1149:	f3 0f 1e fa          	endbr64 
        114d:	55                   	push   %rbp
        114e:	48 89 e5             	mov    %rsp,%rbp
        1151:	89 7d fc             	mov    %edi,-0x4(%rbp)
        1154:	89 75 f8             	mov    %esi,-0x8(%rbp)
        1157:	8b 55 fc             	mov    -0x4(%rbp),%edx
        115a:	8b 45 f8             	mov    -0x8(%rbp),%eax
        115d:	01 d0                	add    %edx,%eax
        115f:	5d                   	pop    %rbp
        1160:	c3                   	retq   

    0000000000001161 <multiplicacion>:
        1161:	f3 0f 1e fa          	endbr64 
        1165:	55                   	push   %rbp
        1166:	48 89 e5             	mov    %rsp,%rbp
        1169:	89 7d fc             	mov    %edi,-0x4(%rbp)
        116c:	89 75 f8             	mov    %esi,-0x8(%rbp)
        116f:	8b 45 fc             	mov    -0x4(%rbp),%eax
        1172:	0f af 45 f8          	imul   -0x8(%rbp),%eax
        1176:	5d                   	pop    %rbp
        1177:	c3                   	retq   

    0000000000001178 <main>:
        1178:	f3 0f 1e fa          	endbr64 
        117c:	55                   	push   %rbp
        117d:	48 89 e5             	mov    %rsp,%rbp
        1180:	48 83 ec 20          	sub    $0x20,%rsp
        1184:	89 7d ec             	mov    %edi,-0x14(%rbp)
        1187:	48 89 75 e0          	mov    %rsi,-0x20(%rbp)
        118b:	be 05 00 00 00       	mov    $0x5,%esi
        1190:	bf 04 00 00 00       	mov    $0x4,%edi
        1195:	e8 af ff ff ff       	callq  1149 <suma>
        119a:	89 45 f8             	mov    %eax,-0x8(%rbp)
        119d:	8b 45 f8             	mov    -0x8(%rbp),%eax
        11a0:	89 c6                	mov    %eax,%esi
        11a2:	bf 09 00 00 00       	mov    $0x9,%edi
        11a7:	e8 b5 ff ff ff       	callq  1161 <multiplicacion>
        11ac:	89 45 fc             	mov    %eax,-0x4(%rbp)
        11af:	8b 45 fc             	mov    -0x4(%rbp),%eax
        11b2:	89 c6                	mov    %eax,%esi
        11b4:	48 8d 3d 49 0e 00 00 	lea    0xe49(%rip),%rdi        # 2004 <_IO_stdin_used+0x4>
        11bb:	b8 00 00 00 00       	mov    $0x0,%eax
        11c0:	e8 8b fe ff ff       	callq  1050 <printf@plt>
        11c5:	b8 00 00 00 00       	mov    $0x0,%eax
        11ca:	c9                   	leaveq 
        11cb:	c3                   	retq   
        11cc:	0f 1f 40 00          	nopl   0x0(%rax)

    00000000000011d0 <__libc_csu_init>:
        11d0:	f3 0f 1e fa          	endbr64 
        11d4:	41 57                	push   %r15
        11d6:	4c 8d 3d db 2b 00 00 	lea    0x2bdb(%rip),%r15        # 3db8 <__frame_dummy_init_array_entry>
        11dd:	41 56                	push   %r14
        11df:	49 89 d6             	mov    %rdx,%r14
        11e2:	41 55                	push   %r13
        11e4:	49 89 f5             	mov    %rsi,%r13
        11e7:	41 54                	push   %r12
        11e9:	41 89 fc             	mov    %edi,%r12d
        11ec:	55                   	push   %rbp
        11ed:	48 8d 2d cc 2b 00 00 	lea    0x2bcc(%rip),%rbp        # 3dc0 <__do_global_dtors_aux_fini_array_entry>
        11f4:	53                   	push   %rbx
        11f5:	4c 29 fd             	sub    %r15,%rbp
        11f8:	48 83 ec 08          	sub    $0x8,%rsp
        11fc:	e8 ff fd ff ff       	callq  1000 <_init>
        1201:	48 c1 fd 03          	sar    $0x3,%rbp
        1205:	74 1f                	je     1226 <__libc_csu_init+0x56>
        1207:	31 db                	xor    %ebx,%ebx
        1209:	0f 1f 80 00 00 00 00 	nopl   0x0(%rax)
        1210:	4c 89 f2             	mov    %r14,%rdx
        1213:	4c 89 ee             	mov    %r13,%rsi
        1216:	44 89 e7             	mov    %r12d,%edi
        1219:	41 ff 14 df          	callq  *(%r15,%rbx,8)
        121d:	48 83 c3 01          	add    $0x1,%rbx
        1221:	48 39 dd             	cmp    %rbx,%rbp
        1224:	75 ea                	jne    1210 <__libc_csu_init+0x40>
        1226:	48 83 c4 08          	add    $0x8,%rsp
        122a:	5b                   	pop    %rbx
        122b:	5d                   	pop    %rbp
        122c:	41 5c                	pop    %r12
        122e:	41 5d                	pop    %r13
        1230:	41 5e                	pop    %r14
        1232:	41 5f                	pop    %r15
        1234:	c3                   	retq   
        1235:	66 66 2e 0f 1f 84 00 	data16 nopw %cs:0x0(%rax,%rax,1)
        123c:	00 00 00 00 

    0000000000001240 <__libc_csu_fini>:
        1240:	f3 0f 1e fa          	endbr64 
        1244:	c3                   	retq   

    Disassembly of section .fini:

    0000000000001248 <_fini>:
        1248:	f3 0f 1e fa          	endbr64 
        124c:	48 83 ec 08          	sub    $0x8,%rsp
        1250:	48 83 c4 08          	add    $0x8,%rsp
        1254:	c3                   	retq 


Ejercicio 38
^^^^^^^^^^^^^^

Ya viste que tanto en C como Rust es posible incluir en el proceso de enlazado bibliotecas estáticas
y dinámicas. Ahora la idea es ver cómo las puedes incluir. Antes de ver esto, debemos
revisar algunos conceptos. Sabes qué es el Application binary interface (ABI)?

Antes de responder la pregunta, te haré otra que tal vez sea más familiar para ti.
¿Has oido hablar del API de una bilioteca? API quiere decir Application Programming
Interface. El API de una biblioteca es la interfaz pública que provee esta para
poder usar su funcionalidad. En términos prácticos, puedes pensar el API como las
CONVENCIONES que debes seguir para llamar una de las funciones de la biblioteca.

El ABI es similar al API, pero son aquellas convenciones que necesitas seguir para
que un programa pueda llamar a otro programa a nivel de LENGUAJE DE MÁQUINA. Entonces
cuando tu programa quiere utilizar una biblioteca dinámica, solo podrá usarla si
utiliza la misma ABI. Entre las conveciones que define la ABI de un sistema están:

* El set de instrucciones de la CPU, la estructura de memoria a utilizar, el ENDIAN,
  entre otros.
* Los tipos de datos, el tamaño y como se ubicarán en la memoria.
* Cómo se deben llamar las funciones (calling convection), en dónde se pasan los
  parámetros y en dónde se devuelven resultados.
* MUY IMPORTANTE: cómo se deben hacer los llamados al sistema operativo (luego hablamos
  sobre eso).
* Cómo será el formato de los relocatable object files, de las bibliotecas dinámicas, 
  de los ejecutables.
* Entre otras cosas...

En el caso de Linux, el ABI utilizada se llama 
`System V ABI <https://drive.google.com/file/d/1hF_FvOsMJsG5NxymjykvFP-L111j75TN/view?usp=sharing>`__ 
y el formato de los ejecutable `ELF <https://www.packtpub.com/product/learning-linux-binary-analysis/9781782167105>`__.
En Windows el formato de los ejecutables es `PE <https://docs.microsoft.com/en-us/windows/win32/debug/pe-format>`__


Ejercicio 40
^^^^^^^^^^^^^^

En este ejercicio vamos a analizar un poco más los relocatable object files. Recuerda que
este es el tipo de archivo que obtendrás como salida del proceso de ensamblado.
¿Qué hay en un relocatable object file? Vas a encontrar al menos estas cosas: el código del máquina,
el valor inicial de las variables globales y la tabla de símbolos.

Te has preguntado ¿Por qué tienen la palabra relocatable estos object files? Recuerda que parte
del contenido del archivo es código de máquina. Recuerda también que la idea es que estos archivos
los toma el enlazador y los combina para generar un ejecutable. Por tanto, las instrucciones contenidas
en el relocatable object file no pueden manipular direcciones de memoria absolutas. Esto permite
que el enlazador asigne esas direcciones solo después de enlazar y generar el ejecutable.

Considera este código:

funcs.c:

.. code-block:: c
   :linenos:

    int suma(int a, int b) {
        return (a + b);
    }

    int sumatoria(int* numeros, int cantidad) {
        int acumulado = 0;
        for (int i = 0; i < cantidad; i++) {
            acumulado += numeros[i];
        }
        return acumulado;
    }

Compila el programa: ``gcc -Wall -c functions.c -o functions.o``. Ahora observa el archivo
de salida: ``readelf -hSl functions.o``

.. code-block:: none

    ELF Header:
    Magic:   7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00 
    Class:                             ELF64
    Data:                              2's complement, little endian
    Version:                           1 (current)
    OS/ABI:                            UNIX - System V
    ABI Version:                       0
    Type:                              REL (Relocatable file)
    Machine:                           Advanced Micro Devices X86-64
    Version:                           0x1
    Entry point address:               0x0
    Start of program headers:          0 (bytes into file)
    Start of section headers:          768 (bytes into file)
    Flags:                             0x0
    Size of this header:               64 (bytes)
    Size of program headers:           0 (bytes)
    Number of program headers:         0
    Size of section headers:           64 (bytes)
    Number of section headers:         12
    Section header string table index: 11

    Section Headers:
    [Nr] Name              Type             Address           Offset
        Size              EntSize          Flags  Link  Info  Align
    [ 0]                   NULL             0000000000000000  00000000
        0000000000000000  0000000000000000           0     0     0
    [ 1] .text             PROGBITS         0000000000000000  00000040
        0000000000000061  0000000000000000  AX       0     0     1
    [ 2] .data             PROGBITS         0000000000000000  000000a1
        0000000000000000  0000000000000000  WA       0     0     1
    [ 3] .bss              NOBITS           0000000000000000  000000a1
        0000000000000000  0000000000000000  WA       0     0     1
    [ 4] .comment          PROGBITS         0000000000000000  000000a1
        0000000000000025  0000000000000001  MS       0     0     1
    [ 5] .note.GNU-stack   PROGBITS         0000000000000000  000000c6
        0000000000000000  0000000000000000           0     0     1
    [ 6] .note.gnu.propert NOTE             0000000000000000  000000c8
        0000000000000020  0000000000000000   A       0     0     8
    [ 7] .eh_frame         PROGBITS         0000000000000000  000000e8
        0000000000000058  0000000000000000   A       0     0     8
    [ 8] .rela.eh_frame    RELA             0000000000000000  00000268
        0000000000000030  0000000000000018   I       9     7     8
    [ 9] .symtab           SYMTAB           0000000000000000  00000140
        0000000000000108  0000000000000018          10     9     8
    [10] .strtab           STRTAB           0000000000000000  00000248
        000000000000001c  0000000000000000           0     0     1
    [11] .shstrtab         STRTAB           0000000000000000  00000298
        0000000000000067  0000000000000000           0     0     1

Observa las secciones. La .text continen el código de máquina, la .data
tendrán los valores iniciales de las variables globales y .symtab será la tabla
de símbolos.

Ahora mira la tabla de símbolos:

``readelf -s functions.o``

.. code-block:: bash

    Symbol table '.symtab' contains 11 entries:
          Num:    Value          Size Type    Bind   Vis      Ndx Name
            0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
            1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS functions.c
            2: 0000000000000000     0 SECTION LOCAL  DEFAULT    1 
            3: 0000000000000000     0 SECTION LOCAL  DEFAULT    2 
            4: 0000000000000000     0 SECTION LOCAL  DEFAULT    3 
            5: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
            6: 0000000000000000     0 SECTION LOCAL  DEFAULT    6 
            7: 0000000000000000     0 SECTION LOCAL  DEFAULT    7 
            8: 0000000000000000     0 SECTION LOCAL  DEFAULT    4 
            9: 0000000000000000    24 FUNC    GLOBAL DEFAULT    1 suma
           10: 0000000000000018    73 FUNC    GLOBAL DEFAULT    1 sumatoria

Nota las direcciones de las funciones: 0 y 0x18. Estas direcciones no son
absolutas, son relativas. En todos los relocatable object files verás este mismo
comportamiento.

Ahora crea un nuevo archivo donde utilices las funciones de functions.c y
compila: ``gcc -Wall -c main.c -o main.o``

main.c:

.. code-block:: c
   :linenos:

    #include <stdio.h>

    int suma(int, int);
    int sumatoria(int*, int );

    int main(int argc, char* argv[]) {
        int a = suma(4, 5);
        int array[] = {1,2,3,4,5};
        int b = sumatoria(array,(sizeof(array))/(sizeof(int)));
        printf("suma(4,5): %d\n",a);
        printf("sumatoria(1..5): %d\n",b);
        return 0;
    }


Genera el ejecutable con ``gcc -Wall main.o functions.o -o exe`` y la tabla de símbolos
con ``readelf -s exe``

.. code-block:: bash

    Symbol table '.dynsym' contains 8 entries:
    Num:    Value          Size Type    Bind   Vis      Ndx Name
        0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
        1: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND _ITM_deregisterTMCloneTab
        2: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND __stack_chk_fail@GLIBC_2.4 (2)
        3: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND printf@GLIBC_2.2.5 (3)
        4: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND __libc_start_main@GLIBC_2.2.5 (3)
        5: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND __gmon_start__
        6: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND _ITM_registerTMCloneTable
        7: 0000000000000000     0 FUNC    WEAK   DEFAULT  UND __cxa_finalize@GLIBC_2.2.5 (3)

    Symbol table '.symtab' contains 69 entries:
    Num:    Value          Size Type    Bind   Vis      Ndx Name
        0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
        1: 0000000000000318     0 SECTION LOCAL  DEFAULT    1 
        2: 0000000000000338     0 SECTION LOCAL  DEFAULT    2 
        3: 0000000000000358     0 SECTION LOCAL  DEFAULT    3 
        4: 000000000000037c     0 SECTION LOCAL  DEFAULT    4 
        5: 00000000000003a0     0 SECTION LOCAL  DEFAULT    5 
        6: 00000000000003c8     0 SECTION LOCAL  DEFAULT    6 
        7: 0000000000000488     0 SECTION LOCAL  DEFAULT    7 
        8: 0000000000000528     0 SECTION LOCAL  DEFAULT    8 
        9: 0000000000000538     0 SECTION LOCAL  DEFAULT    9 
        10: 0000000000000568     0 SECTION LOCAL  DEFAULT   10 
        11: 0000000000000628     0 SECTION LOCAL  DEFAULT   11 
        12: 0000000000001000     0 SECTION LOCAL  DEFAULT   12 
        13: 0000000000001020     0 SECTION LOCAL  DEFAULT   13 
        14: 0000000000001050     0 SECTION LOCAL  DEFAULT   14 
        15: 0000000000001060     0 SECTION LOCAL  DEFAULT   15 
        16: 0000000000001080     0 SECTION LOCAL  DEFAULT   16 
        17: 00000000000012f8     0 SECTION LOCAL  DEFAULT   17 
        18: 0000000000002000     0 SECTION LOCAL  DEFAULT   18 
        19: 0000000000002028     0 SECTION LOCAL  DEFAULT   19 
        20: 0000000000002080     0 SECTION LOCAL  DEFAULT   20 
        21: 0000000000003db0     0 SECTION LOCAL  DEFAULT   21 
        22: 0000000000003db8     0 SECTION LOCAL  DEFAULT   22 
        23: 0000000000003dc0     0 SECTION LOCAL  DEFAULT   23 
        24: 0000000000003fb0     0 SECTION LOCAL  DEFAULT   24 
        25: 0000000000004000     0 SECTION LOCAL  DEFAULT   25 
        26: 0000000000004010     0 SECTION LOCAL  DEFAULT   26 
        27: 0000000000000000     0 SECTION LOCAL  DEFAULT   27 
        28: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS crtstuff.c
        29: 00000000000010b0     0 FUNC    LOCAL  DEFAULT   16 deregister_tm_clones
        30: 00000000000010e0     0 FUNC    LOCAL  DEFAULT   16 register_tm_clones
        31: 0000000000001120     0 FUNC    LOCAL  DEFAULT   16 __do_global_dtors_aux
        32: 0000000000004010     1 OBJECT  LOCAL  DEFAULT   26 completed.8059
        33: 0000000000003db8     0 OBJECT  LOCAL  DEFAULT   22 __do_global_dtors_aux_fin
        34: 0000000000001160     0 FUNC    LOCAL  DEFAULT   16 frame_dummy
        35: 0000000000003db0     0 OBJECT  LOCAL  DEFAULT   21 __frame_dummy_init_array_
        36: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS main.c
        37: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS functions.c
        38: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS crtstuff.c
        39: 00000000000021c4     0 OBJECT  LOCAL  DEFAULT   20 __FRAME_END__
        40: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS 
        41: 0000000000003db8     0 NOTYPE  LOCAL  DEFAULT   21 __init_array_end
        42: 0000000000003dc0     0 OBJECT  LOCAL  DEFAULT   23 _DYNAMIC
        43: 0000000000003db0     0 NOTYPE  LOCAL  DEFAULT   21 __init_array_start
        44: 0000000000002028     0 NOTYPE  LOCAL  DEFAULT   19 __GNU_EH_FRAME_HDR
        45: 0000000000003fb0     0 OBJECT  LOCAL  DEFAULT   24 _GLOBAL_OFFSET_TABLE_
        46: 0000000000001000     0 FUNC    LOCAL  DEFAULT   12 _init
        47: 00000000000012f0     5 FUNC    GLOBAL DEFAULT   16 __libc_csu_fini
        48: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND _ITM_deregisterTMCloneTab
        49: 0000000000004000     0 NOTYPE  WEAK   DEFAULT   25 data_start
        50: 0000000000004010     0 NOTYPE  GLOBAL DEFAULT   25 _edata
        51: 00000000000012f8     0 FUNC    GLOBAL HIDDEN    17 _fini
        52: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND __stack_chk_fail@@GLIBC_2
        53: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND printf@@GLIBC_2.2.5
        54: 000000000000121b    24 FUNC    GLOBAL DEFAULT   16 suma
        55: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND __libc_start_main@@GLIBC_
        56: 0000000000004000     0 NOTYPE  GLOBAL DEFAULT   25 __data_start
        57: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND __gmon_start__
        58: 0000000000004008     0 OBJECT  GLOBAL HIDDEN    25 __dso_handle
        59: 0000000000002000     4 OBJECT  GLOBAL DEFAULT   18 _IO_stdin_used
        60: 0000000000001280   101 FUNC    GLOBAL DEFAULT   16 __libc_csu_init
        61: 0000000000004018     0 NOTYPE  GLOBAL DEFAULT   26 _end
        62: 0000000000001080    47 FUNC    GLOBAL DEFAULT   16 _start
        63: 0000000000004010     0 NOTYPE  GLOBAL DEFAULT   26 __bss_start
        64: 0000000000001169   178 FUNC    GLOBAL DEFAULT   16 main
        65: 0000000000001233    73 FUNC    GLOBAL DEFAULT   16 sumatoria
        66: 0000000000004010     0 OBJECT  GLOBAL HIDDEN    25 __TMC_END__
        67: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND _ITM_registerTMCloneTable
        68: 0000000000000000     0 FUNC    WEAK   DEFAULT  UND __cxa_finalize@@GLIBC_2.2


Nota que te aparecen dos tablas de símbolos. .dynsym contiene los símbolos que
se deben definir en tiempo de ejecución. .symtab contiene los símbolos, es decir,
los que ya están resueltos y los que vienen de las bibliotecas dinámicas. 
¿Cuáles bibliotecas? ``readelf -d exe | grep '(NEEDED)'``


.. code-block:: c

    0x0000000000000001 (NEEDED)             Shared library: [libc.so.6]

Ejercicio 41
^^^^^^^^^^^^^^

Ahora si vamos a probar como enlazar un programa con una bilioteca estática

Crea los siguientes archivos:

uno.c:

.. code-block:: c
   :linenos:

    int uno(){
        return 1;
    }

dos.c:

.. code-block:: c
   :linenos:

    int dos(){
        return 2;
    }

tres.c:

.. code-block:: c
   :linenos:

    int tres(){
        return 3;
    }

Compila:

``gcc -Wall -c uno.c -o uno.o``

``gcc -Wall -c dos.c -o dos.o``

``gcc -Wall -c tres.c -o tres.o``

Para generar la bilioteca estática debes seguir la convención de iniciar el nombre
con lib y colocar la extensión ``.a``:

``ar crc libstatic.a uno.o dos.o tres.o``

Puedes listar el contenido de la biblioteca con ``ar t libstatic.a``

Ahora necesitamos crear el API de la biblioteca

api.h:

.. code-block:: c
   :linenos:

    int uno();
    int dos();
    int tres();

Ahora usamos la biblioteca así

main.c:

.. code-block:: c
   :linenos:

    #include <stdio.h>
    #include "api.h"

    int main(int argc, char* argv[]){

        printf("uno: %d\n",uno());
        printf("dos: %d\n",dos());
        printf("tres: %d\n",tres());

        return 0;
    }

Finalmente genera el ejecutable con ``gcc main.o -L./ -lstatic -o exe`` y
ejecuta el programa. En este caso:

* Con la opción ``-L./`` estás indicando una posible donde donde tendrás
  almacenadas bibliotecas estáticas y/o dinámicas.
* Con la opción ``-lstatic`` estás indicando que se debe utilizar la bilioteca
  libstatic.a o libstatic.so. Nota que en este caso se tiene en cuenta la
  convención, es decir, si tu pasas ``-lstatic`` el enlazador buscará
  el archivo libstatic.a o libstatic.so.
* Luego de ser enlazado el programa, ya no tendrás dependencias con la biblioteca
  estática porque está hará parte del ejecutable. Recuerda que en el caso de las
  bibliotecas dinámicas es diferente.

Ejercicio 42
^^^^^^^^^^^^^^^^^

Finalmente, vamos a probar como enlazar un programa con una bilioteca dinámica.
Recuerda que la biblioteca dinámica no hace parte del ejecutable, por tanto
para poder ejecutar el programa es necesario que le des a conocer al sistema
operativo el ejecutable mismo y las dependencias a bibliotecas dinámicas.

Cuando enlazas un programa con una biblioteca dinámica, en el ejecutable te
quedarán símbolos sin definir. Estos símbolos tendrán que definirse al momento
de ejecutar el programa. En este caso, cuando se ejecute el programa, será necesario
que el sistema operativo cargue de manera dinámica (dynamic linker) los símbolos
pendientes que estarán en la biblioteca dinámica. El dynamic linker se encargará
entonces de cargar a memoria la biblioteca y mapear esta a una región de memoria
del proceso (recuerda, un proceso es la abstracción que usa el sistema operativo
para poder correr y controlar la ejecución de un programa).

Es importante señalar que las biblotecas dinámicas tienen un formato ELF similar
al de los ejecutables; sin embargo, la direcciones de los símbolos no son absolutas,
sino relativas a un punto (position independent code). Eso permite entonces que
dos instrucciones separadas por 100 bytes, por ejemplo, puedan ser ubicadas en un
proceso en las direcciones 100 y 200 y en otro en la 512 y 612. Adicionalmente, las
bibliotecas dinámicas no puede ejecutarse.

Ahora considera los mismo programas del ejercicio anterior. Construye la biblioteca
dinámica así:

``gcc -c uno.c -fPIC -o uno.o``

``gcc -c dos.c -fPIC -o dos.o``

``gcc -c tres.c -fPIC -o tres.o``

La opción ``-fPIC`` quiere decir position independent code. FInalmente mezclamos
los código:

``gcc -shared uno.o dos.o tres.o -o libstatic.so``

Antes de generar el ejecutable borra la bilioteca estática con ``rm -fv ./libstatic.a``.
Ejecuta el comando ``gcc main.o -L./ -lstatic -o exe`` y luego ejecuta el programa. El
resultado debería ser algo similar a esto:

.. code-block:: c

    ./exe: error while loading shared libraries: libstatic.so: 
    cannot open shared object file: No such file or directory

¿Por qué ocurre esto? como te dije antes, debes decirle al sistema operativo en dónde está
la bilioteca dinámica. Esto se hace actualizando la variable de ambiente (environment variable)
``LD_LIBRARY_PATH`` con ``export LD_LIBRARY_PATH=./``. Ejecuta de nuevo el programa.
¿Funcionó?

¿Será posible que el propio programa ejecutable le indique al sistema operativo cuándo cargar
la biblioteca y dónde está ubicada? SI!!! Y esto es genial porque te permite cargar en ejecución
diferentes versiones de biblioteca, es decir, tienes más flexibilidad.

Considera el siguiente programa:

.. code-block:: c
    :linenos:

    #include <stdio.h>
    #include <stdlib.h>
    #include <dlfcn.h>
    #include "api.h"
    
    int main(int argc, char* argv[]) {

        int (*func_ptr)() = NULL;

        // Cargo la biblioteca dinámica
        void* handle = dlopen ("./libstatic.so", RTLD_LAZY);

        if (!handle) {
            fprintf(stderr, "%s\n", dlerror());
            exit(1);
        }
        
        // Busco el símbolo que necesito
        func_ptr = dlsym(handle, "uno");
        if (!func_ptr) {
            fprintf(stderr, "%s\n", dlerror());
            exit(1);
        }
        printf("uno(): %d\n", func_ptr());

        func_ptr = dlsym(handle, "dos");
        if (!func_ptr) {
            fprintf(stderr, "%s\n", dlerror());
            exit(1);
        }
        printf("dos(): %d\n", func_ptr());


        func_ptr = dlsym(handle, "tres");
        if (!func_ptr) {
            fprintf(stderr, "%s\n", dlerror());
            exit(1);
        }
        printf("tres(): %d\n", func_ptr());


        return 0;
    }


Compila con ``gcc -Wall -c main.c -o main.o``

En el ejemplo anterior al generar el ejecutable hicimos esto ``gcc main.o -L./ -lstatic -o exe``.
Si nuestro programa dependiera de más biliotecas haríamos ``gcc main.o -L./ -lstatic -lXXX -lXXX -o exe``
Recuerda que la bilioteca se generó con el comando ``gcc -shared uno.o dos.o tres.o -o libstatic.so``;
sin embargo, para este ejemplo como vamos a cargar de manera `manual` la biblioteca, es necesario
generar nuestra biblioteca dinámica indicando todas las dependencias que esta tendrá a otras
bibliotecas, así: ``gcc -shared uno.o dos.o tres.o -lXXX -lXXX -o libstatic.so``. En este
caso no tenemos más dependencias, por tanto podemos conservar la biblioteca del ejemplo anterior.

Para generar el ejecutable escribe ``gcc -Wall main.o -ldl -o exe``. Ejecuta el programa. ¿Funciona?

Ten presente los siguientes puntos:

* ``int (*func_ptr)() = NULL;`` en esta expresión ``func_ptr`` es una variable que almacena
  direcciones de funciones que no reciben nada y devuelven un entero.
* ``void* handle = dlopen ("./libstatic.so", RTLD_LAZY);`` carga la biblioteca dinámica.
* ``func_ptr = dlsym(handle, "uno");`` carga nu símbolo en particular.
* En ``gcc -Wall main.o -ldl -o exe`` pasamos la opción ``-ldl``. Esta opción indica que
  vamos a realizar una carga perezosa (lazy loading) de la biblioteca dinámica.

Ejercicio 43
^^^^^^^^^^^^^^^^^

Ya sabemos cuáles son los pasos necesarios para ir desde
un lenguaje como C y C++ a código de máquina; sin embargo, nos falta
una última estación en este recorrido. ¿Qué pasa con lenguajes como C#?

Para resolver esta pregunta vamos a tener que analizar un poco más
qué es un compilador y qué es un intérprete.


En este ejercicio vamos a investigar un poco más sobre algunos conceptos
de los lenguajes de programación. En particular analizaremos qué son
las implementaciones interpretadas y qué son las implementaciones compiladas.
Nota por favor que no te dije lenguajes interpretados o compilados. Al final
de los ejercicios que te propongo tu mismo podrás explicar la diferencia.

En ejercicios pasados discutimos las fases para transformar un
programa del código fuente a lenguaje de máquina.¿ Lo recuerdas?

* Iniciamos con el programa.
* Luego hacemos un análisis léxico, con el Tokenizer, para generar los tokens.
* Los tokens son unidades indivisibles compuestas por un tipo y un valor.
  Los tokens nos permiten identificar las palabras que componen nuestro programa.
* Ahora hacemos un análisis semántico, utilizando un Parser. Esto nos permiten
  reconocer si estamos combinando correctamente las palabras en el programa
  realizado.
* El Parser genera, si el programa es válido, una representación del programa
  conocida como AST.

Es precisamente este AST el que pasamos a un intérprete o a un compilador. El
intérprete ejecutará el código. El compilador convertirá el AST a otro lenguaje,
que posiblemente será transformado de nuevo o interpretado.

Por ejemplo, en el caso de C, luego de generar el AST, utilizamos un generador
de código y producimos lenguaje ensamblador. Luego este lenguaje ensamblador
lo convertimos en lenguaje de máquina. Finalmente, el lenguaje de máquina es
INTERPRETADO por la CPU.

Hay dos tipos de intérpretes que se diferencian en el formato del programa
que interpretan. En ese sentido el programa puede estar representado como un AST
o como Bytecodes. Los intérpretes que utilizan el primer formato se conocen
como intérpretes recursivos y los segundos como Máquinas Virtuales (VM). En el
caso de los segundos, la representación será muy parecida a un programa en lenguaje
ensamblador, como el de una CPU real, y por tanto el nombre de máquinas virtuales.

En el caso de los compiladores tenemos tres tipos: 

* Ahead-of-time (AOT): todo el código se traduce a un nuevo lenguaje antes de ser
  ejecutado. Como en el caso de C y C++. Sin embargo, es interesante anotar, 
  por ejemplo, que C++ se comparta como un interprete a la hora de optimizar el código.
* Just-in-time (JIT): el código se genera durante la ejecución del programa.
* AST-transformer o también conocidos como transpilers. Aquí la idea es realizar
  una transformación de un tipo de AST a otro, para generar, por ejemplo, de un
  lenguaje de programación a otro.

Ejercicio 44
^^^^^^^^^^^^^^

Profundicemos un poco más en los intérpretes.

Los AST interpreters: ejecutan el programa directamente desde la representación AST,
es decir, producen el resultado modelado con el lenguaje de programación directamente,
en tiempo de ejecución.

Realiza el siguiente ejercicio utilizando la herramienta `AST-explorer <https://astexplorer.net/>`__:

* Selecciona javacript.
* Escribe el siguiente código
  
  .. code-block:: javascript
     :linenos:

     a = 5;
     b = a*2 + 10;

* Analiza el AST generado. Verás que la herramienta te identifica expresiones y cada expresión la
  organiza como un árbol identificando el lado izquierdo y el lado derecho.

¿Puedes pintar árboles para los dos expresiones anteriores?


Ejercicio 45
^^^^^^^^^^^^^^

Profundicemos un poco más en los intérpretes.

Los bytecodes interpreters no parten de una representación AST en forma de árbol, sino
que parten de un arreglo de bytecodes. Por tanto, necesitarán un paso más en tiempo
de compilación:

* Iniciamos con el programa.
* Análisis léxico --> genera tokens
* Análisis semántico --> genera el AST.
* Bytecode emitter --> Generar bytecodes

Ahora si, en tiempo de ejecución se ejecutará el programa representado como un
arreglo de bytecodes.

¿Para qué hacemos este paso extra? Se hace para optimizar el almacenamiento del
programa en comparación con la representación AST. También será más fácil
de recorrer el programa y se tendrá un control más granular de la ejecución.

Recuerda que a este tipo de intérprete lo llamamos también virtual machine. Usualmente,
estas virtual machines son de dos tipos: stack-based y register-based.

Si consideramos a una CPU como un intérprete
de las instrucciones de máquina, podríamos decir que la CPU es una virtual machine register-based.

¿Cómo serán las VM stack-based? Imagina el stack, como un pila de platos.
Estas VM apilan (stack) los operandos y luego aplican las operaciones. Por tanto, 
los resultados siempre quedan en el tope de la pila. Entonces, para realizar la operación
``5+6`` la VM colocará en la pila el 5, luego el 6, y finalmente realizará la operación suma.
Como resultado, los operandos 5 y 6 serán retirados de la pila y quedará el resultado 11
en la parte superior de esta.

Realiza el siguiente ejercicio:

* Crea un programa Test.java:

  .. code-block:: java
     :linenos:

        class Test{

            public static void main(String[] args){
                int x = 5;
                System.out.println(x+2-1);
            }
        }

* Compila el programa así: ``javac Test.java``. Verás que se genera en el directorio un
  archivo Test.class

* Ahora ejecuta ``hexdump -C Test.class``. El resultado será el bytecode
  
.. code-block:: bash  

        00000000  ca fe ba be 00 00 00 34  00 1b 0a 00 05 00 0e 09  |.......4........|
        00000010  00 0f 00 10 0a 00 11 00  12 07 00 13 07 00 14 01  |................|
        00000020  00 06 3c 69 6e 69 74 3e  01 00 03 28 29 56 01 00  |..<init>...()V..|
        00000030  04 43 6f 64 65 01 00 0f  4c 69 6e 65 4e 75 6d 62  |.Code...LineNumb|
        00000040  65 72 54 61 62 6c 65 01  00 04 6d 61 69 6e 01 00  |erTable...main..|
        00000050  16 28 5b 4c 6a 61 76 61  2f 6c 61 6e 67 2f 53 74  |.([Ljava/lang/St|
        00000060  72 69 6e 67 3b 29 56 01  00 0a 53 6f 75 72 63 65  |ring;)V...Source|
        00000070  46 69 6c 65 01 00 09 54  65 73 74 2e 6a 61 76 61  |File...Test.java|
        00000080  0c 00 06 00 07 07 00 15  0c 00 16 00 17 07 00 18  |................|
        00000090  0c 00 19 00 1a 01 00 04  54 65 73 74 01 00 10 6a  |........Test...j|
        000000a0  61 76 61 2f 6c 61 6e 67  2f 4f 62 6a 65 63 74 01  |ava/lang/Object.|
        000000b0  00 10 6a 61 76 61 2f 6c  61 6e 67 2f 53 79 73 74  |..java/lang/Syst|
        000000c0  65 6d 01 00 03 6f 75 74  01 00 15 4c 6a 61 76 61  |em...out...Ljava|
        000000d0  2f 69 6f 2f 50 72 69 6e  74 53 74 72 65 61 6d 3b  |/io/PrintStream;|
        000000e0  01 00 13 6a 61 76 61 2f  69 6f 2f 50 72 69 6e 74  |...java/io/Print|
        000000f0  53 74 72 65 61 6d 01 00  07 70 72 69 6e 74 6c 6e  |Stream...println|
        00000100  01 00 04 28 49 29 56 00  20 00 04 00 05 00 00 00  |...(I)V. .......|
        00000110  00 00 02 00 00 00 06 00  07 00 01 00 08 00 00 00  |................|
        00000120  1d 00 01 00 01 00 00 00  05 2a b7 00 01 b1 00 00  |.........*......|
        00000130  00 01 00 09 00 00 00 06  00 01 00 00 00 01 00 09  |................|
        00000140  00 0a 00 0b 00 01 00 08  00 00 00 2e 00 03 00 02  |................|
        00000150  00 00 00 0e 08 3c b2 00  02 1b 05 60 04 64 b6 00  |.....<.....`.d..|
        00000160  03 b1 00 00 00 01 00 09  00 00 00 0e 00 03 00 00  |................|
        00000170  00 04 00 02 00 05 00 0d  00 06 00 01 00 0c 00 00  |................|
        00000180  00 02 00 0d                                       |....|
        00000184

* Para ver una representación simbólica de este bytecode escribe ``javap -c Test.class``:

.. code-block:: bash 

        Compiled from "Test.java"
        class Test {
        Test();
            Code:
            0: aload_0
            1: invokespecial #1                  // Method java/lang/Object."<init>":()V
            4: return

        public static void main(java.lang.String[]);
            Code:
            0: iconst_5
            1: istore_1
            2: getstatic     #2                  // Field java/lang/System.out:Ljava/io/PrintStream;
            5: iload_1
            6: iconst_2
            7: iadd
            8: iconst_1
            9: isub
            10: invokevirtual #3                  // Method java/io/PrintStream.println:(I)V
            13: return
        }

* Observa el código en el método main: ``iconst_5`` coloca un 5 en el stack, ``istore_1`` almacena el valor
  en x. Esto corresponde a la operación ``x = 5``. Ahora mira cómo se resulte ``x+2-1``. Primero
  se coloca en el stack el valor de x con ``iload_1``, luego se coloca el 2 ``iconst_2``, se hace
  la suma ``iadd`` dejando el resultado en el stack. Luego se coloca en el stack el 1 con ``iconst_1``
  y finalmente se realiza la resta ``isub``.

Ejercicio 46
^^^^^^^^^^^^^^

Continuado con el tema del ejercicio anterior.

* Abre la aplicación `compiler explorer <https://godbolt.org/>`__.
* Selecciona python
* Ingresa el programa:

  .. code-block:: python
     :linenos:

     def main():
        x = 5;
        print(x+2-1)

* Observa la salida al lado derecho:

    .. code-block:: python
       :linenos:

            1           0 LOAD_CONST               0 (<code object main at 0x5653b7cb2980, file "example.py", line 1>)
                        2 LOAD_CONST               1 ('main')
                        4 MAKE_FUNCTION            0
                        6 STORE_NAME               0 (main)
                        8 LOAD_CONST               2 (None)
                        10 RETURN_VALUE

            Disassembly of <code object main at 0x5653b7cb2980, file "example.py", line 1>:
            2           0 LOAD_CONST               1 (5)
                        2 STORE_FAST               0 (x)

            3           4 LOAD_GLOBAL              0 (print)
                        6 LOAD_FAST                0 (x)
                        8 LOAD_CONST               2 (2)
                        10 BINARY_ADD
                        12 LOAD_CONST               3 (1)
                        14 BINARY_SUBTRACT
                        16 CALL_FUNCTION            1
                        18 POP_TOP
                        20 LOAD_CONST               0 (None)
                        22 RETURN_VALUE

* ¿Qué tipo de VM será el intérprete de python?


Ejercicio 47
^^^^^^^^^^^^^^

Ahora profundicemos un poco más en los compiladores.

Los AOT (Ahead-of-time) compilers. Ahead-of-time quiere decir, antes de la
ejecución, es decir, estos compiladores traducen completamente el código
fuente antes de ser ejecutados. Recuerda, por ejemplo, C o C++. Una vez el código
de máquina es generado, este es interpretado por la CPU. 

Los siguientes pasos permiten generar, en tiempo de compilación,
código de máquina:

* Iniciamos con el programa.
* Análisis léxico --> genera tokens
* Análisis semántico --> genera el AST.
* Code generator --> produce representaciones intermedias que luego
  se traducen a código de máquina especifico para cada CPU.

Los pasos desde el programa hasta la generación del AST se conocen como FRONTEND. 
Los pasos desde el generador de código, pasando por las representaciones
intermedias y el código de máquina se conocen como BACKEND.

Un última cosita:

¿Qué es el proyecto LLVM? Es una infraestructura de compilación compuesta
por un conjunto de compiladores y herramientas que permiten desarrollar
un fronted para cualquier lenguaje de programación y un backend para cualquier
set de instrucciones.

Los pasos que se siguen al usar LLVM, todos en tiempo de compilación, son:

* Iniciamos con el programa.
* Análisis léxico --> genera tokens
* Análisis semántico --> genera el AST.
* LLVM IR generator --> genera LLVM bytecode o LLVM IR
* El LLVM IR lo recibe el generador de código LLVM encargado
  de generar código de máquina para múltiples plataformas.

 Considera el siguiente ejemplo llamado main.cpp:

 .. code-block:: c 
    :linenos:

    int main(void){
        int x = 10;
        return x+5-2;
    }

Compila usando ``clang++ main.cpp`` el resultado será el archivo 
``a.out``. Ejecuta el archivo con ``./a.out`` y lee el resultado generado
por el programa con ``echo $?``

Ahora ejecuta ``clang++ main.cpp -S`` para producir el archivo ``main.s``
que tendrá el código ensamblador:

.. code-block:: c
    :linenos:

    int main(void){
        int x = 10;
        return x+5-2;
    }

.. code-block:: bash 
    
		.text
		.file	"main.cpp"
		.globl	main                    # -- Begin function main
		.p2align	4, 0x90
		.type	main,@function
	main:                                   # @main
		.cfi_startproc
	# %bb.0:
		pushq	%rbp
		.cfi_def_cfa_offset 16
		.cfi_offset %rbp, -16
		movq	%rsp, %rbp
		.cfi_def_cfa_register %rbp
		movl	$0, -4(%rbp)
		movl	$10, -8(%rbp)
		movl	-8(%rbp), %eax
		addl	$5, %eax
		subl	$2, %eax
		popq	%rbp
		.cfi_def_cfa %rsp, 8
		retq
	.Lfunc_end0:
		.size	main, .Lfunc_end0-main
		.cfi_endproc
											# -- End function
		.ident	"clang version 10.0.0-4ubuntu1 "
		.section	".note.GNU-stack","",@progbits
		.addrsig

Observa las línas 17 y 18 donde hace el cálculo correspondiente
a la expresión ``return x+5-2``. 

Compila de nuevo el código, pero esta vez con 

Ahora ejecuta ``clang++ main.cpp -S -O3`` y lee de nuevo main.s:


.. code-block:: bash
    :linenos:

		.text
		.file	"main.cpp"
		.globl	main                    # -- Begin function main
		.p2align	4, 0x90
		.type	main,@function
	main:                                   # @main
		.cfi_startproc
	# %bb.0:
		movl	$13, %eax
		retq
	.Lfunc_end0:
		.size	main, .Lfunc_end0-main
		.cfi_endproc
											# -- End function
		.ident	"clang version 10.0.0-4ubuntu1 "
		.section	".note.GNU-stack","",@progbits
		.addrsig


Observa la línea 9. ¿Qué notas? ¿Recuerdas el resultado obtenido al ejecutar
el programa? Mira de nuevo la línea 9. 

Estrictamente hablando, se supone que estamos compilando el código, pero
podrás notar que clang++ con la opción -O3 está interpretando, en tiempo,
de compilación, el código, para optimizarlo. Interesante, ¿Cierto? :)

Ahora ejecuta el comando ``clang++ main.cpp -S -emit-llvm`` observa
el archivo main.ll:

.. code-block:: bash

    ; ModuleID = 'main.cpp'
    source_filename = "main.cpp"
    target datalayout = "e-m:e-p270:32:32-p271:32:32-p272:64:64-i64:64-f80:128-n8:16:32:64-S128"
    target triple = "x86_64-pc-linux-gnu"

    ; Function Attrs: noinline norecurse nounwind optnone uwtable
    define dso_local i32 @main() #0 {
      %1 = alloca i32, align 4
      %2 = alloca i32, align 4
      store i32 0, i32* %1, align 4
      store i32 10, i32* %2, align 4
      %3 = load i32, i32* %2, align 4
      %4 = add nsw i32 %3, 5
      %5 = sub nsw i32 %4, 2
      ret i32 %5
    }

    attributes #0 = { noinline norecurse nounwind optnone uwtable "correctly-rounded-divide-sqrt-fp-math"="false" "disable-tail-calls"="false" "frame-pointer"="all" "less-precise-fpmad"="false" "min-legal-vector-width"="0" "no-infs-fp-math"="false" "no-jump-tables"="false" "no-nans-fp-math"="false" "no-signed-zeros-fp-math"="false" "no-trapping-math"="false" "stack-protector-buffer-size"="8" "target-cpu"="x86-64" "target-features"="+cx8,+fxsr,+mmx,+sse,+sse2,+x87" "unsafe-fp-math"="false" "use-soft-float"="false" }

    !llvm.module.flags = !{!0}
    !llvm.ident = !{!1}

    !0 = !{i32 1, !"wchar_size", i32 4}
    !1 = !{!"clang version 10.0.0-4ubuntu1 "}

¿Sabes qué es eso? Es código LLVM IR. Observa las líneas 13 y 14. De nuevo corresponde al
cálculo de la expresión ``return x+5-2``. Desde esta representación se puede generar
código para múltiples set de instrucciones como te comenté antes.


Ejercicio 48
^^^^^^^^^^^^^^

Ahora hablemos un poco más de los Just-In-Time (JIT) compilers. Los AOT traducen
el programa a código de máquina en tiempo de compilación. Los JIT lo hacen en
tiempo de ejecución.

Los pasos que sigue un JIT compiler en tiempo de compilación son:

* Iniciamos con el programa.
* Análisis léxico --> genera tokens.
* Análisis semántico --> genera el AST.
* Bytecode emitter --> Generar bytecode.

En tiempo de ejecución un intérprete (lo que llamamos virtual machine) interpreta
el bytecode, pero algunos bytecode son compilados a código de máquina. La primera
vez que se compilan dichos bytecodes y se ejecuta el código de máquina producido
toma un tiempo; sin embargo, la interpretación posterior de estos bytecodes compilados
será muy rápido puesto que la ejecución no será efectuada por el intérprete sino
directamente por la CPU.

Ejercicio 49
^^^^^^^^^^^^^^

Finalmente, analicemos un poco más los transpilers o AST transformers.

Los pasos que sigue el transpiler, en tiempo de compilación, son:

* Iniciamos con el programa.
* Análisis léxico --> genera tokens
* Análisis semántico --> genera el AST.
* El transpiler o AST transformer --> genera otro AST para el mismo lenguaje
  o para otro lenguaje de programación. Por ejemplo, traducir una versión vieja
  de javascript a una versión nueva o de python a javascript.
* El nuevo AST se pasa a un generador de código --> genera el programa en otro lenguaje
  de programación (claramente conservando la semántica del programa inicial).

La salida de todo este proceso puede pasarse ahora a un AOT o un JIT compiler.

Ejercicio 50
^^^^^^^^^^^^^^^

¿Los lenguajes javascript, python, C, C#, c++ son lenguajes interpretados o compilados?

:)

La verdad es que esta pregunta es incorrecta. Lo que es interpretado o compilado
es la implementación específica. ¿Cómo así? Creo que con lo que aprendiste tu mismo
puedes explicar que significa esto. ¿Te animas?

Ejercicio 51
^^^^^^^^^^^^^^^

¿Cómo es la implementación de C#?

Te voy a dejar `aquí <https://codeasy.net/lesson/c_sharp_compilation_process>`__
un enlace para que leas.

Ahora si, escribe ¿Cómo es la implementación de C#?

Te dejo algunas preguntas adicionales:

* ¿Es posible generar código de máquina partiendo de C# en tiempo de compilación?
* ¿Qué ventaja tiene entonces generar código Just-In-Time en tiempo de ejecución?
* ¿Pudiste identificar en la lectura cómo se llama la máquina virtual utilizada
  para interpretar código IL?
* ¿Qué es el .NET framework?

PROYECTO 1
^^^^^^^^^^^

Realiza un programa que permita crear un base de datos de estudiantes.
Cada registro de la base de datos estará dado por:
número de cédula, nombre y semestre. Cada registro corresponde a un 
estudiante.

Implemente los siguientes comandos:

**mkdb nombre tamaño** : crea una base de datos especificando el nombre
y la cantidad de registros.

**loaddb nombre** : carga la base de datos en memoria desde el archivo
especificado. El comando debe indicar si la base de datos se cargó
correctamente o no existe. La base de datos debe cargarse en memoria
dinámica antes de poder aplicar los siguientes comandos.

**savedb nombre** : este comando salva la base de datos en el archivo
especificado.

**readall** : lee todos los registros de la base de datos.

**readsize** : lee la cantidad de registros de la base datos.

**mkreg cedula nombre semestre** : crea un nuevo registro en la base
de datos.

**readreg cédula** : busca en la base de datos por número de cédula.
En caso de encontrar la cédula imprime el registro completo.

**exit** : salir del programa. Antes de terminar debe preguntar si se desea
salvar la base de datos en el archivo especificado con el comando loaddb.

Cada comando deberá implementarse como una función.

Cada registro es así:

.. code-block:: c
   :linenos:

    struct estudiante
    {
        int cedula;
        char nombre[30];
        int semestre;
    };


Ejercicio 52
^^^^^^^^^^^^^

Ya hemos hablado de los procesos, ¿Recuerdas? Pues
un proceso no es más que una abstracción que emplea el sistema operativo para
ejecutar y administrar un programa en ejecución. Los programas están almacenados
en archivos conocidos como object files. Para ejecutar un programa el sistema
operativo crea un proceso que ejecuta el object file, es decir, la CPU (o un
core) consumirá (fetch) y ejecutará las instrucciones del object file que estarán
almacenadas en alguna región de la memoria principal. Tu sabes también que los
programas en ejecución necesitarán memoria para almacenar las variables. Entonces
surge la siguiente pregunta ¿Cómo es la memoria de un proceso
y cuál es su estructura?

Cuando el sistema operativo crea un proceso para ejecutar un programa, también
es necesario asignarle memoria y aplicarle una estructura particular. En casi todos
los sistemas operativos las estructura de memoria del proceso es más o menos la misma.
La memoria de un proceso está dividida en múltiples partes conocidas como segmentos:

* Block Started by Symbol (BSS) es el segmentos de datos no inicializados.
* Data.
* Text segment o segmento de código.
* Stack.
* Heaps.

Algunos de estos segmentos se crean con la información almacenada en el
object file mientras que otros segmentos aparecen al momento de ejecutar el programa.

Ejercicio 53
^^^^^^^^^^^^^

¿Cómo hacemos para ver el contenido de los segmentos de memoria provenientes del
object file?

Escribe el siguiente programa llamado main.c:

.. code-block:: c
   :linenos:

    int main(int argc, char* argv[]) {

        return 0;
    }

Compila el programa con ``gcc -Wall main.c -o main``. Podrás observar el tamaño de 
algunos segmentos:

``size main`` 

.. code-block:: c

   text	   data	    bss	    dec	    hex	filename
   1418	    544	      8	   1970	    7b2	main

Puedes observar tres segmentos: text, data y bss.

Ejercicio 54
^^^^^^^^^^^^^
Te estarás preguntado ¿Para qué sirve cada uno de los segmentos
que acabas de ver?

El segmento BSS denota la cantidad de memoria reservada para variables globales
que no se inicializaron o que se inicializan a 0.

Modifica el programa anterior así:

.. code-block:: c
   :linenos:

    int var1;
    int var2;
    int var3 = 0;

    int main(int argc, char* argv[]) {

        return 0;
    }

De nuevo, compila y ejecuta ``size main``:

.. code-block:: c

   text	   data	    bss	    dec	    hex	filename
   1418	    544	     16	   1978	    7ba	main

Compara esta salida con la anterior. ¿Notas un cambio en BSS?

Ejercicio 55
^^^^^^^^^^^^^^

Tal vez alguna vez has escuchado decir que declarar variables globales
no es buena práctica. ¿Por qué?

* Si defines muchas variables globales incrementas el tamaño
  del binario (como puedes ver con size)
* Puede introducir problemas de seguridad
* Pueden introducir problemas de concurrencia como las condiciones
  de carrera.
* Polucionan el espacio de nombres del programa.

Estas respuestas seguro te generan más preguntas. Algunas de estas
preguntas seguro las responderemos en las próximas semanas, otras
de ellas quedan para tu curiosidad o en una nueva temporada de esta seria :)

Ejercicio 56
^^^^^^^^^^^^^

Para analizar el segmento data te propongo modificar de nuevo nuestro programa:

.. code-block:: c
   :linenos:

    int var1;
    int var2;
    int var3 = 0;
    int var4 = 69;
    int var5 = 666;

    int main(int argc, char* argv[]) {

        return 0;
    }

Compila y ejecuta ``size main``:

.. code-block:: c
   
   text	   data	    bss	    dec	    hex	filename
   1418	    552	     16	   1986	    7c2	main

Compara, ¿El segmento data cambió? El segmento ``data`` entonces te sirve para almacenar
las variables inicializadas con valores diferentes de 0.

Ejercicio 57
^^^^^^^^^^^^^^

Modifica de nuevo el archivo:

.. code-block:: c
   :linenos:

    int var1;
    int var2;
    int var3 = 0;
    int var4 = 69;
    int var5 = 666;

    void func(){
      static int i = 10;
      i++;
    }

    int main(int argc, char* argv[]) {
        func();
        return 0;
    }

Compila y ejecuta ``size main``:

.. code-block:: c

   text	   data	    bss	    dec	    hex	filename
   1506	    556	     20	   2082	    822	main

Observa entonces que los segmentos data y bss se incrementan.

Ejercicio 58
^^^^^^^^^^^^^^

¿Cómo hago para ver el contenido del segmento data?

Toma como referencia el programa anterior y escribe el comando ``objdump -s -j .data main``

.. code-block:: bash

    main:     file format elf64-x86-64

    Contents of section .data:
    4000 00000000 00000000 08400000 00000000  .........@......
    4010 45000000 9a020000                    E....... 

¿Puedes ver efectivamente el contenido? observa los valores iniciales de ``var4`` y ``var5`` en
el programa. Ten presente que ``4000`` y ``4010`` son direcciones. El resto de información
es datos, cada file muestra 16 bytes (máximo) y luego se ve la representación de cada byte en ASCII.

Ejercicio 59
^^^^^^^^^^^^^

En el segmento de texto está contenido todo el código de máquina del programa producido por
el compilador.

¿Cómo puedes ver el contenido?

Ejecuta ``objdump -S main``

Podrás observar el código de máquina y la representación simbólica en lenguaje ensamblador.

Ejercicio 60
^^^^^^^^^^^^^^

¿Cómo hacemos para ver el contenido de los segmentos stack y heap?

Solo podemos ver esta parte de la memoria cuando el programa esté en ejecución. Cuando
quieres ejecutar un object file, el sistema operativo crea un nuevo proceso e inicializa
su memoria. Los segmentos BSS, data y text son inicializados con la información que está en
el object file y, el stack y el heap se añaden y son modificados a medida que el código
del segmento text es leído por parte de la CPU.

Veamos un ejemplo:

.. code-block:: c
   :linenos:

    #include <unistd.h> 
    int main(int argc, char* argv[]) {
        while (1) {
            sleep(1); 
        };

        return 0;
    }

Compila el código con ``gcc -Wall main.c -o main``

Y ahora ejecuta el programa así ``./main &`` para que quede en background y retomes
el control de la terminal para que puedas seguir escribiendo comandos. Ten en cuenta
que el número que te aparece en la terminal al ejecutar el programa es el ``pid`` o
identificador del proceso en el sistema operativo:

.. code-block:: bash

    juanfranco@pop-os:/tmp/linker$ ./main &
    [1] 295236

NO LO HAGAS AHORA, pero si después quieres matar el proceso escribe en la terminal 
``kill -9 295236``.

En Linux puedes consultar información del proceso en el directorio ``/proc`` allí tendrás
una entrada para el proceso identificada con el pid del mismo.

Ejecuta el comando ``ls -al /proc/295236``:

.. code-block:: c 
   :linenos:

    total 0
    dr-xr-xr-x   9 juanfranco juanfranco 0 Sep 21 14:17 .
    dr-xr-xr-x 714 root       root       0 Sep 18 07:13 ..
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 arch_status
    dr-xr-xr-x   2 juanfranco juanfranco 0 Sep 21 15:12 attr
    -rw-r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 autogroup
    -r--------   1 juanfranco juanfranco 0 Sep 21 15:12 auxv
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 cgroup
    --w-------   1 juanfranco juanfranco 0 Sep 21 15:12 clear_refs
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 14:17 cmdline
    -rw-r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 comm
    -rw-r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 coredump_filter
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 cpuset
    lrwxrwxrwx   1 juanfranco juanfranco 0 Sep 21 15:12 cwd -> /tmp/linker
    -r--------   1 juanfranco juanfranco 0 Sep 21 15:12 environ
    lrwxrwxrwx   1 juanfranco juanfranco 0 Sep 21 14:17 exe -> /tmp/linker/main
    dr-x------   2 juanfranco juanfranco 0 Sep 21 15:12 fd
    dr-x------   2 juanfranco juanfranco 0 Sep 21 15:12 fdinfo
    -rw-r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 gid_map
    -r--------   1 juanfranco juanfranco 0 Sep 21 15:12 io
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 limits
    -rw-r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 loginuid
    dr-x------   2 juanfranco juanfranco 0 Sep 21 15:12 map_files
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 maps
    -rw-------   1 juanfranco juanfranco 0 Sep 21 15:12 mem
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 mountinfo
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 mounts
    -r--------   1 juanfranco juanfranco 0 Sep 21 15:12 mountstats
    dr-xr-xr-x   5 juanfranco juanfranco 0 Sep 21 15:12 net
    dr-x--x--x   2 juanfranco juanfranco 0 Sep 21 15:12 ns
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 numa_maps
    -rw-r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 oom_adj
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 oom_score
    -rw-r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 oom_score_adj
    -r--------   1 juanfranco juanfranco 0 Sep 21 15:12 pagemap
    -r--------   1 juanfranco juanfranco 0 Sep 21 15:12 patch_state
    -r--------   1 juanfranco juanfranco 0 Sep 21 15:12 personality
    -rw-r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 projid_map
    lrwxrwxrwx   1 juanfranco juanfranco 0 Sep 21 15:12 root -> /
    -rw-r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 sched
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 schedstat
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 sessionid
    -rw-r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 setgroups
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 smaps
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 smaps_rollup
    -r--------   1 juanfranco juanfranco 0 Sep 21 15:12 stack
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 14:17 stat
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 statm
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:11 status
    -r--------   1 juanfranco juanfranco 0 Sep 21 15:12 syscall
    dr-xr-xr-x   3 juanfranco juanfranco 0 Sep 21 15:12 task
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 timers
    -rw-rw-rw-   1 juanfranco juanfranco 0 Sep 21 15:12 timerslack_ns
    -rw-r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 uid_map
    -r--r--r--   1 juanfranco juanfranco 0 Sep 21 15:12 wchan

Cada una de estas entradas corresponde a una característica del proceso.

Para preguntar por el mapa de memoria del proceso ejecuta: ``cat /proc/295236/maps``:

.. code-block:: c
   :linenos:

    563fa1aeb000-563fa1aec000 r--p 00000000 08:03 8393449                    /tmp/linker/main
    563fa1aec000-563fa1aed000 r-xp 00001000 08:03 8393449                    /tmp/linker/main
    563fa1aed000-563fa1aee000 r--p 00002000 08:03 8393449                    /tmp/linker/main
    563fa1aee000-563fa1aef000 r--p 00002000 08:03 8393449                    /tmp/linker/main
    563fa1aef000-563fa1af0000 rw-p 00003000 08:03 8393449                    /tmp/linker/main
    7f28fb8f9000-7f28fb91e000 r--p 00000000 08:03 1049202                    /usr/lib/x86_64-linux-gnu/libc-2.31.so
    7f28fb91e000-7f28fba96000 r-xp 00025000 08:03 1049202                    /usr/lib/x86_64-linux-gnu/libc-2.31.so
    7f28fba96000-7f28fbae0000 r--p 0019d000 08:03 1049202                    /usr/lib/x86_64-linux-gnu/libc-2.31.so
    7f28fbae0000-7f28fbae1000 ---p 001e7000 08:03 1049202                    /usr/lib/x86_64-linux-gnu/libc-2.31.so
    7f28fbae1000-7f28fbae4000 r--p 001e7000 08:03 1049202                    /usr/lib/x86_64-linux-gnu/libc-2.31.so
    7f28fbae4000-7f28fbae7000 rw-p 001ea000 08:03 1049202                    /usr/lib/x86_64-linux-gnu/libc-2.31.so
    7f28fbae7000-7f28fbaed000 rw-p 00000000 00:00 0 
    7f28fbb0b000-7f28fbb0c000 r--p 00000000 08:03 1049197                    /usr/lib/x86_64-linux-gnu/ld-2.31.so
    7f28fbb0c000-7f28fbb2f000 r-xp 00001000 08:03 1049197                    /usr/lib/x86_64-linux-gnu/ld-2.31.so
    7f28fbb2f000-7f28fbb37000 r--p 00024000 08:03 1049197                    /usr/lib/x86_64-linux-gnu/ld-2.31.so
    7f28fbb38000-7f28fbb39000 r--p 0002c000 08:03 1049197                    /usr/lib/x86_64-linux-gnu/ld-2.31.so
    7f28fbb39000-7f28fbb3a000 rw-p 0002d000 08:03 1049197                    /usr/lib/x86_64-linux-gnu/ld-2.31.so
    7f28fbb3a000-7f28fbb3b000 rw-p 00000000 00:00 0 
    7ffdd8feb000-7ffdd900c000 rw-p 00000000 00:00 0                          [stack]
    7ffdd9183000-7ffdd9186000 r--p 00000000 00:00 0                          [vvar]
    7ffdd9186000-7ffdd9187000 r-xp 00000000 00:00 0                          [vdso]
    ffffffffff600000-ffffffffff601000 --xp 00000000 00:00 0                  [vsyscall]

Observa cada línea. Tomemos por ejemplo la primera:

``563fa1aeb000-563fa1aec000 r--p 00000000 08:03 8393449                    /tmp/linker/main``

Primero tienes un rango de direcciones: ``563fa1aeb000-563fa1aec000`` en ese 
rango tienes mapeada información del object file ``/tmp/linker/main``. Después del 
rango de direcciones encuentras los permisos: r se puede leer, w modificar, x ejecutar, p para
indicar si la región de memoria es privada o compartida con otro procesos (s). Si la región
está mapeada a un archivo, lo que sigue es el offset en el archivo. Si la región está mapeada
a un archivo verás el identificador del dispositivo (08:03) donde está el archivo. Luego aparece
el inode (lo vemos luego). Y finalmente el path del archivo que está mapeado a esta región. También
puedes ver un espacio en blanco o el propósito de la región, por ejemplo [stack] para indicar
que es una región utilizada para implementar el segmento de stack.

¿Puedes identificar el tamaño del stack? Mira que no es muy grande, es por ello que no DEBES
usar el stack para guardar variables grandes. Si necesitas arreglos o estructuras de datos grandes
debes usar el HEAP.

Ejercicio 61
^^^^^^^^^^^^^^

Profundicemos un poco más en el stack.

¿Recuerdas qué se almacena en el stack?

* Variables locales que no sean estáticas.
* El ``stack frame`` cuando llamas una función. Allí se encuentra 
  la dirección a la que debe retornar el programa luego de llamar la función.
* Parámetros de entrada y salida de una función.

MUY MUY IMPORTANTE: 

* Al llamar un función, las variables que declares en el stack se van
  apilando, como si fueran una columna de platos. El puntero de pila se va ajustando siempre
  el TOP del stack; sin embargo, cuando retornes de la función el puntero de pila se ajustará
  nuevamente a la base de la columna de platos (las variables). Los datos de las variables 
  locales siguen allí pero en cualquier momento pueden ser destruidos al llamar otra función 
  o al producirse una interrupción. Las interrupciones interrumpen el flujo de instrucciones,
  para ejecutar un nuevo flujo conocido como servicio de atención a la interrupción, y hacen
  uso del stack para almacenar temporalmente parte del contexto de la CPU. EN CONCLUSIÓN: una
  vez retornes de una función NO PUEDES contar con las variables locales (¡Murieron!).

* Como el stack no es tan grande comparado con el HEAP debes evitar llamados recursivos
  infinitos para evitar desbordar su capacidad.

¿Cómo puedes ver el contenido del stack? Necesitas un depurador (un debugger).

Ejercicio 62
^^^^^^^^^^^^^^

Profundicemos un poco más en el heap.

Considera el siguiente código:

.. code-block:: c
   :linenos:

    #include <unistd.h>
    #include <stdlib.h> 
    #include <stdio.h> 
    
    int main(int argc, char* argv[]) {
        void* ptr = malloc(1024); 
        printf("Address: %p\n", ptr);
     
        while (1) {
            sleep(1); 
        };
        
        return 0;
    }

Compila y ejecuta:

.. code-block:: c

    ./main &
    [2] 321982
    Address: 0x55f05576b2a0

Ahora ejecuta de nuevo ``cat /proc/321982/maps`` (nota que estamos usando el pid del nuevo
proceso):

.. code-block:: c

    55f054ece000-55f054ecf000 r--p 00000000 08:03 8394826                    /tmp/linker/main
    55f054ecf000-55f054ed0000 r-xp 00001000 08:03 8394826                    /tmp/linker/main
    55f054ed0000-55f054ed1000 r--p 00002000 08:03 8394826                    /tmp/linker/main
    55f054ed1000-55f054ed2000 r--p 00002000 08:03 8394826                    /tmp/linker/main
    55f054ed2000-55f054ed3000 rw-p 00003000 08:03 8394826                    /tmp/linker/main
    55f05576b000-55f05578c000 rw-p 00000000 00:00 0                          [heap]
    7f4b21bb2000-7f4b21bd7000 r--p 00000000 08:03 1049202                    /usr/lib/x86_64-linux-gnu/libc-2.31.so
    7f4b21bd7000-7f4b21d4f000 r-xp 00025000 08:03 1049202                    /usr/lib/x86_64-linux-gnu/libc-2.31.so
    7f4b21d4f000-7f4b21d99000 r--p 0019d000 08:03 1049202                    /usr/lib/x86_64-linux-gnu/libc-2.31.so
    7f4b21d99000-7f4b21d9a000 ---p 001e7000 08:03 1049202                    /usr/lib/x86_64-linux-gnu/libc-2.31.so
    7f4b21d9a000-7f4b21d9d000 r--p 001e7000 08:03 1049202                    /usr/lib/x86_64-linux-gnu/libc-2.31.so
    7f4b21d9d000-7f4b21da0000 rw-p 001ea000 08:03 1049202                    /usr/lib/x86_64-linux-gnu/libc-2.31.so
    7f4b21da0000-7f4b21da6000 rw-p 00000000 00:00 0 
    7f4b21dc4000-7f4b21dc5000 r--p 00000000 08:03 1049197                    /usr/lib/x86_64-linux-gnu/ld-2.31.so
    7f4b21dc5000-7f4b21de8000 r-xp 00001000 08:03 1049197                    /usr/lib/x86_64-linux-gnu/ld-2.31.so
    7f4b21de8000-7f4b21df0000 r--p 00024000 08:03 1049197                    /usr/lib/x86_64-linux-gnu/ld-2.31.so
    7f4b21df1000-7f4b21df2000 r--p 0002c000 08:03 1049197                    /usr/lib/x86_64-linux-gnu/ld-2.31.so
    7f4b21df2000-7f4b21df3000 rw-p 0002d000 08:03 1049197                    /usr/lib/x86_64-linux-gnu/ld-2.31.so
    7f4b21df3000-7f4b21df4000 rw-p 00000000 00:00 0 
    7fffc1d25000-7fffc1d46000 rw-p 00000000 00:00 0                          [stack]
    7fffc1dec000-7fffc1def000 r--p 00000000 00:00 0                          [vvar]
    7fffc1def000-7fffc1df0000 r-xp 00000000 00:00 0                          [vdso]
    ffffffffff600000-ffffffffff601000 --xp 00000000 00:00 0                  [vsyscall]

¿Ves el segmento heap? ¿Qué tamaño tiene? Nota que en el programa reservamos 1 KiB pero realmente se
reservar 4 KiB.

Mira el rango de direcciones del heap: ``55f05576b000-55f05578c000``, ahora observa la dirección
de ``ptr``: ``0x55f05576b2a0`` Ah! está en el rango, está en el heap.

IMPORTANTE: el tamaño del heap puede crecer hasta varias gigas, solo que en este caso se reservaron
de entrada 4 KiB.

Volvamos al programa. Considera esta línea: ``void* ptr = malloc(1024)`` ¿La variable ptr
en qué segmento está?

¿Qué pasa con la dirección de la región que reservamos una vez salgamos del ámbito en el cual
se declaró prt?

Y si perdemos la dirección ¿Qué pasa con esa memoria que reservamos? ¿Y qué pasa si esto
nos comienza a ocurrir mucho en nuestro programa?

¿Recuerdas cómo evitamos este desperdicio de memoria? (¿Cuál es la función que libera la reserva?)

No olvides que reservar y devolver la reserva de la memoria es tu responsabilidad cuando
trabajas en con lenguajes como C y C++. Otros implementaciones de lenguajes cuentan con un componente que se ejecuta
concurrente a tu código y se denomina el garbage collector (por ejemplo C#). El garbage collector se encarga
de liberar o devolver la reserva de memoria por nosotros.

Y ¿Cómo puedes hacer para detectar errores en la gestión de memoria? Puedes utilizar una herramienta
llamada valgrind.

Considera este programa:

.. code-block:: c
   :linenos:

    #include <stdio.h>
    #include <stdlib.h>

    int main(int argc, char* argv[]) {
        char *ptr = malloc(20*sizeof(char));
        return 0;
    }

Compila el programa así: ``gcc -g -Wall main.c -o main``. Instala valgrind
con ``sudo apt install valgrind``. Corre el programa así: ``valgrind ./main``:

.. code-block:: none

    ==331725== Memcheck, a memory error detector
    ==331725== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
    ==331725== Using Valgrind-3.15.0 and LibVEX; rerun with -h for copyright info
    ==331725== Command: ./main
    ==331725== 
    ==331725== 
    ==331725== HEAP SUMMARY:
    ==331725==     in use at exit: 20 bytes in 1 blocks
    ==331725==   total heap usage: 1 allocs, 0 frees, 20 bytes allocated
    ==331725== 
    ==331725== LEAK SUMMARY:
    ==331725==    definitely lost: 20 bytes in 1 blocks
    ==331725==    indirectly lost: 0 bytes in 0 blocks
    ==331725==      possibly lost: 0 bytes in 0 blocks
    ==331725==    still reachable: 0 bytes in 0 blocks
    ==331725==         suppressed: 0 bytes in 0 blocks
    ==331725== Rerun with --leak-check=full to see details of leaked memory
    ==331725== 
    ==331725== For lists of detected and suppressed errors, rerun with: -s
    ==331725== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)

Podrás observar en la sección LEAK SUMMARY que valgrind detectó un leak de 20 bytes.

¿Pero en dónde está el error?

Ejecuta ``valgrind --leak-check=full  ./main``

.. code-block:: none

    ==331978== Memcheck, a memory error detector
    ==331978== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
    ==331978== Using Valgrind-3.15.0 and LibVEX; rerun with -h for copyright info
    ==331978== Command: ./main
    ==331978== 
    ==331978== 
    ==331978== HEAP SUMMARY:
    ==331978==     in use at exit: 20 bytes in 1 blocks
    ==331978==   total heap usage: 1 allocs, 0 frees, 20 bytes allocated
    ==331978== 
    ==331978== 20 bytes in 1 blocks are definitely lost in loss record 1 of 1
    ==331978==    at 0x483B7F3: malloc (in /usr/lib/x86_64-linux-gnu/valgrind/vgpreload_memcheck-amd64-linux.so)
    ==331978==    by 0x109165: main (main.c:5)
    ==331978== 
    ==331978== LEAK SUMMARY:
    ==331978==    definitely lost: 20 bytes in 1 blocks
    ==331978==    indirectly lost: 0 bytes in 0 blocks
    ==331978==      possibly lost: 0 bytes in 0 blocks
    ==331978==    still reachable: 0 bytes in 0 blocks
    ==331978==         suppressed: 0 bytes in 0 blocks
    ==331978== 
    ==331978== For lists of detected and suppressed errors, rerun with: -s
    ==331978== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 0 from 0)

Puedes ver que el error ocurrió en la línea 5 del programa ``main.c``. ¡Genial!

Ejercicio 63
^^^^^^^^^^^^^^^

¿Te animas a corregir el error del ejercicio anterior y verificar con valgrind que
todo esté bien?

Ejercicio 64
^^^^^^^^^^^^^^^^

¿Recuerdas que para poder ver el contenido del stack necesitas un debugger? Pues
vamos a probar uno. En este caso usaremos GDB. Escribe gdb en la terminal. Si el comando
no es reconocido, lo puedes instalar con ``sudo apt-get install build-essentials``.

Considera este programa:

.. code-block:: c
   :linenos:

    #include <stdio.h>

    int main(int argc, char* argv[]) {
        char arr[14];
        
        arr[0] = 'C';
        arr[1] = 'o';
        arr[2] = 'n';
        arr[3] = 't';
        arr[4] = 'r';
        arr[5] = 'o';
        arr[6] = 'l';
        arr[7] = 'a';
        arr[8] = 'd';
        arr[9] = 'o';
        arr[10] = 'r';
        arr[11] = 'e';
        arr[12] = 's';
        arr[13] = 0;

        printf("arr: %s", arr);

        return 0;
    }

Compila el programa con ``gcc -g -Wall main.c -o main``. La opción ``-g`` le
dice al compilador que genere el ejecutable incluyendo información de depuración
en la tabla de símbolos. Esta información será usada posteriormente por GDB

Ejecuta el programa con GDB: ``gdb main``:

.. code-block:: c

    GNU gdb (Ubuntu 9.1-0ubuntu1) 9.1
    Copyright (C) 2020 Free Software Foundation, Inc.
    License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
    This is free software: you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law.
    Type "show copying" and "show warranty" for details.
    This GDB was configured as "x86_64-linux-gnu".
    Type "show configuration" for configuration details.
    For bug reporting instructions, please see:
    <http://www.gnu.org/software/gdb/bugs/>.
    Find the GDB manual and other documentation resources online at:
        <http://www.gnu.org/software/gdb/documentation/>.

    For help, type "help".
    Type "apropos word" to search for commands related to "word"...
    Registered pretty printers for UE4 classes
    Reading symbols from main...
    (gdb) 

Observa que te aparecerá un nuevo prompt: ``(gdb)`` donde escribirás comandos
para GBD.

* Para comenzar la ejecución del programa escribe ``run``
* Coloca un breakpoint al iniciar la función main: ``break main``. El breakpoint le indica
  al depurador que debe tener la ejecución del proceso en ese punto.
* Escribe ``run``. Verás que la ejecución del programa se detiene en en la función
  main.
* Utiliza el comando ``n`` para ejecutar la siguiente línea de código.
* Imprime el contenido de la variable arr con ``print arr``.

La variable arr está en el stack. Puedes ver el contenido del stack con ``x/16x arr``. 
El comando es ``x`` pero además puedas indicar la cantidad de bytes (16) y el formato
(x para hexadecimal):

.. code-block:: c

    (gdb) x/16x arr
    0x7fffffffdb8a:	0x43	0x6f	0x6e	0x74	0x72	0x6f	0x6c	0x61
    0x7fffffffdb92:	0x64	0x6f	0x72	0x65	0x73	0x00	0x00	0xcd
    (gdb)

Puedes ver el interpretados en ASCII de los valores:

.. code-block:: c

(gdb) x/16c arr
0x7fffffffdb8a:	67 'C'	111 'o'	110 'n'	116 't'	114 'r'	111 'o'	108 'l'	97 'a'
0x7fffffffdb92:	100 'd'	111 'o'	114 'r'	101 'e'	115 's'	0 '\000'	0 '\000'	-51 '\315'
(gdb) 

Cambia el contenido del stack:

.. code-block:: bash

    (gdb) set arr[11] = 'a'
    (gdb) print arr
    $2 = "Controladoras"
    (gdb) x/16x arr
    0x7fffffffdb8a:	0x43	0x6f	0x6e	0x74	0x72	0x6f	0x6c	0x61
    0x7fffffffdb92:	0x64	0x6f	0x72	0x61	0x73	0x00	0x00	0xcd
    (gdb) x/16c arr
    0x7fffffffdb8a:	67 'C'	111 'o'	110 'n'	116 't'	114 'r'	111 'o'	108 'l'	97 'a'
    0x7fffffffdb92:	100 'd'	111 'o'	114 'r'	97 'a'	115 's'	0 '\000'	0 '\000'	-51 '\315'
    (gdb)

Ejercicio 65
^^^^^^^^^^^^^^^^^


El siguiente ejemplo te mostrará una técnica para el manejo de la memoria dinámica
que le entrega la responsabilidad de reservar y liberar la memoria dinámica al
código definido en el archivo queue.c. Si analizas detenidamente podrás ver
que el código en queue.h y queue.c trata de implementar el concepto de clase que
ya conoces de otros lenguajes de programación.

queue.h:

.. code-block:: c 
   :linenos:

    #ifndef _QUEUE_H
    #define _QUEUE_H

    typedef struct {
        int front;
        int rear;
        double* arr;
    } queue_t;

    queue_t* create(int size);
    void destroy(queue_t* this);
    int size(queue_t* this);
    void enqueue(queue_t* this, double item);
    double dequeue(queue_t* q);

    #endif

queue.c:

.. code-block:: c 
   :linenos:

    #include "queue.h"
    #include <stdlib.h> 

    static void init(queue_t* this, int size) {
        this->front = 0;
        this->rear = 0;
        this->arr = (double*)malloc(size * sizeof(double));
    }

    queue_t* create(int size){
        queue_t* q = malloc(sizeof(queue_t));
        init(q,size);
        return(q);
    }

    void destroy(queue_t* this){
        free(this->arr);
        free(this);
    }

    int size(queue_t* this){
        return this->rear - this->front;
    }

    void enqueue(queue_t* this, double item) {
        this->arr[this->rear] = item;
        this->rear++;
    }
    
    double dequeue(queue_t* this) {
        double item = this->arr[this->front];
        this->front++;
        return item;
    }

main.c:

.. code-block:: c 
   :linenos:

    #include <stdio.h> 
    #include "queue.h"

    int main(int argc, char** argv) {

        queue_t* q = create(10);
        enqueue(q, 6.5);
        enqueue(q, 1.3);
        enqueue(q, 2.4);
        printf("%f\n", dequeue(q));
        printf("%f\n", dequeue(q));
        printf("%f\n", dequeue(q));
        destroy(q);
        return 0;
    }

Para compilar este ejemplo sigue los siguientes pasos:

gcc -c -g -Wall queue.c -o queue.o

gcc -c -g -Wall main.c -o main.o

gcc -g -Wall queue.o main.o -o exe

Ejecuta el código y verifica con valgrind el manejo de la memoria

./exe

valgrind ./exe

¿Qué resultado obtienes?
¿En qué parte de la memoria está almacenada la variable q?
¿Explica cuánta memoria y dónde se está creando con la función create(10)?

Ejercicio 66
^^^^^^^^^^^^^

Ahora que conocemos más detalles de la memoria de un proceso y luego
del ejercicio anterior, ya tenemos buenas herramientas para hablar del
modelo de programación orientado a objetos.

Como te has dado cuenta hasta ahora, C no es un lenguaje de programación
orientado a objetos; sin embargo, te preguntarás ¿Es posible escribir 
programas orientados a objetos con C? La respuesta es si. El punto es que
en su sintaxis C no soporta los conceptos de clases, herencia, y funciones
virtuales. Aún así, es posible implementar estos conceptos de manera indirecta.

¿Y en últimas qué son los objetos?

Mira, no le demos vueltas conceptuales al asunto. Un objeto no es más que
un conjunto de datos en la memoria de un proceso. OJO: SON DATOS y están en la
MEMORIA DE UN PROCESO. Esto último es clave. Los objetos solo viven en tiempo
de ejecución.

Entonces cuando estoy escribiendo el programa hay objetos? NO, ese es el punto
precisamente que intento aclararte de entrada. Cuando escribes un programa orientado
a objetos, NO TIENES OBJETOS aún. Lo que defines es cómo serán esos objetos,
cómo se crearán, cuándo se crearán, cómo y cuándo se usarán y cómo y cuándo
se destruirán (en algunos lenguajes de programación). Es decir, tu programa
describe lo que pasará con los OBJETOS cuando lo ejecutes.

Te lo repito de nuevo: cuando programas orientado a objetos NO estás creando objetos.
Estás más bien indicando qué se debe hacer para crearlos cuando el programa se EJECUTE.

¿Claro lo anterior? Pregunta si no es claro.

Por lo anterior, es que existe el término DISEÑO ORIENTADO A OBJECTOS. Porque
cuando DISEÑAS un programa orientado a objetos te tienes qué imaginar cómo serán esos
OBJETOS, cuándo se crearán y cuáles serán las relaciones entre ellos cuando 
ejecutes el programa.

Ejercicio 67
^^^^^^^^^^^^^^^

Profe, si yo pudiera ir a ver un objeto en memoria ¿Cómo se vería?

No lo olvides, en últimas, un objeto es una colección de bytes en la memoria. A esas 
posiciones de memoria que componen el objeto las denominamos ATRIBUTOS y al contenido
de esos atributos los llamamos EL ESTADO DEL OBJETO. 

Cuando puedes modificar los valor de los atributos de un objeto mientras el programa
corre se dice que el objeto es MUTABLE. Pero también el objeto puede ser INMUTABLE,
es decir, que una vez creado el objeto e inicializados sus atributos, no podrás cambiar
sus valores o su estado.

Ejercicio 68
^^^^^^^^^^^^^^

Ya te comenté que los objetos (colecciones de bytes) pueden estar relacionados entre
ellos. ¿Qué significa eso?

En términos muy generales, si dos objetos están relacionados, es posible que al modificar
el estado de uno de ellos se afecte el estado del otro. Ya en términos más concretos podemos
decir que un objeto está relacionado con otro cuando uno de sus atributos contiene la dirección
de memoria del otro objeto.

Ejercicio 69
^^^^^^^^^^^^^

No lo olvides, un objeto son bytes en memoria. Pero entonces, ¿Qué pasa con el código?

Parte de tus tareas al diseñar o PLANEAR un programa orientado a objetos es decir qué
OPERACIONES vas a realizar para crear los objetos (asignarles memoria), iniciar su estado
(¿Qué es eso?) (construirlos), destruirlos, leer y modificar su ESTADO. PERO, POR FAVOR,
no lo olvides, cuando estás escribiendo el programa estás MODELANDO tu solución,
tu programa es un PLAN que DESCRIBE lo que ocurrirá cuando sea ejecutado.

Ejercicio 70
^^^^^^^^^^^^^

¿Cómo puedes definir la construcción de un objeto?

Lo puedes hacer de dos formas:

* Construyes un objeto vacío o con un conjuntos mínimo de atributos. A medida que el programa
  se ejecuta, se van añadiendo más atributos. A esta
  técnica se le conoce como prototype-based OOP, por ejemplo en python y javascript.
* El objeto ya tiene unos atributos predeterminados. A esta
  técnica se le conoce como class-based OOP, por ejemplo en C++, C#, java y python.

Para utilizar la segunda forma, debes crear una plantilla predeterminada o CLASE que indique
los atributos que tendrá un objeto al ejecutar el programa.

Te preguntarás, pero en un clase también hay código, entonces ¿Los objetos tienen código? 
Nop. Por lo que hemos venido discutiendo ya sabes que los objetos son solo datos. 
También ya sabes que cuando escribes una clase estás PLANEANDO qué atributos tendrá cada
objeto en memoria. Entonces cuando escribes código en una clase está indicando que ese código
y los atributos están relacionados, es decir, estás indicando de manera explícita 
las posibles OPERACIONES que puedes realizar sobre los DATOS. De esta manera ENCAPSULAS
en el conceptos de CLASE los DATOS y el CÓDIGO. Ten en cuenta que al código también
se le conoce cómo el COMPORTAMIENTO de los objetos, es decir, las acciones que se realizarán
sobre los datos.  

Ejercicio 71
^^^^^^^^^^^^^

¿Cómo hacemos para implementar las ideas anteriores en C? Ya sabes que C no soporta 
de manera explícita el concepto de clase, pero podemos implementar dicho concepto de manera
implícita:

* Usa un estructura para encapsular los atributos del objeto.
* Utiliza funciones para definir el comportamiento de los objetos. Las funciones
  que definen el comportamiento del objeto recibirán como argumento la dirección
  en memoria de la estructura que encapsula los atributos del objeto.

Analiza de nuevo este código:

queue.h:

.. code-block:: c 
   :linenos:

    #ifndef _QUEUE_H
    #define _QUEUE_H

    typedef struct {
        int front;
        int rear;
        double* arr;
    } queue_t;

    queue_t* create(int size);
    void destroy(queue_t* this);
    int size(queue_t* this);
    void enqueue(queue_t* this, double item);
    double dequeue(queue_t* q);

    #endif

queue.c:

.. code-block:: c 
   :linenos:

    #include "queue.h"
    #include <stdlib.h> 

    static void init(queue_t* this, int size) {
        this->front = 0;
        this->rear = 0;
        this->arr = (double*)malloc(size * sizeof(double));
    }

    queue_t* create(int size){
        queue_t* q = malloc(sizeof(queue_t));
        init(q,size);
        return(q);
    }

    void destroy(queue_t* this){
        free(this->arr);
        free(this);
    }

    int size(queue_t* this){
        return this->rear - this->front;
    }

    void enqueue(queue_t* this, double item) {
        this->arr[this->rear] = item;
        this->rear++;
    }
    
    double dequeue(queue_t* this) {
        double item = this->arr[this->front];
        this->front++;
        return item;
    }

Nota que en queue.h declaras qué atributos tendrá el objeto:

.. code-block:: c 
   :linenos:

    #ifndef _QUEUE_H
    #define _QUEUE_H

    typedef struct {
        int front;
        int rear;
        double* arr;
    } queue_t;

Y qué funciones podrás invocar para leer o escribir dichos atributos, es decir, el comportamiento
del objeto:

.. code-block:: c 
   :linenos:

    queue_t* create(int size);
    void destroy(queue_t* this);
    int size(queue_t* this);
    void enqueue(queue_t* this, double item);
    double dequeue(queue_t* q);

Estas cuatro funciones te permiten crear una cola, destruirla, conocer su tamaño,
almacenar en la cola y leer información de ella. Nota que casi todas las funciones
definen un parámetro llamado this. Este parámetro contendrá la dirección del objeto
sobre el cual actuará el código definido en la función.

Por último, observa de nuevo la función main.c:

.. code-block:: c 
   :linenos:

    #include <stdio.h> 
    #include "queue.h"

    int main(int argc, char** argv) {

        queue_t* q = create(10);
        enqueue(q, 6.5);
        enqueue(q, 1.3);
        enqueue(q, 2.4);
        printf("%f\n", dequeue(q));
        printf("%f\n", dequeue(q));
        printf("%f\n", dequeue(q));
        destroy(q);
        return 0;
    }

Nota que debemos incluir queue.h para poder utilizar las funciones y el nuevo
tipo de dato ``queue_t``. Observa que la función ``create(10)`` nos permite
crear un cola (un objeto) de 10 enteros en el heap. La dirección de la cola la almacenamos
en la variable ``q`` que estará en el stack.

Si analizas un poco más el archivo ``queue.c`` varás que create reserva el espacio
en heap para el objeto y adicionalmente inicializa sus atributos:

.. code-block:: c 
   :linenos:

    static void init(queue_t* this, int size) {
        this->front = 0;
        this->rear = 0;
        this->arr = (double*)malloc(size * sizeof(double));
    }

    queue_t* create(int size){
        queue_t* q = malloc(sizeof(queue_t));
        init(q,size);
        return(q);
    }

Ejercicio 72
^^^^^^^^^^^^^

Ahora compara el programa anterior con una implementación en C#:

.. code-block:: csharp
   :linenos:

    using System;

    public class Queue{
        
        private int front;
        private int rear;
        private double[] arr;
        
        public Queue(int size){
            
            front = 0;
            rear = 0;
            arr = new double[size];
        }    
        
        public int size(){
            return (rear - front);
        }
        
        public void enqueue(double item) {
            arr[rear] = item;
            rear++;
        }
        
        public double dequeue() {
            double item = arr[front];
            front++;
            return item;
        }
    }

    class Program {
        static void Main() {
            Queue q = new Queue(10);
            q.enqueue(6.5);
            q.enqueue(1.3);
            q.enqueue(2.4);
            Console.WriteLine(q.dequeue());
            Console.WriteLine(q.dequeue());
            Console.WriteLine(q.dequeue());
        }
    }

Mira los atributos:

En C:

.. code-block:: c 
   :linenos:

    #ifndef _QUEUE_H
    #define _QUEUE_H

    typedef struct {
        int front;
        int rear;
        double* arr;
    } queue_t;

En C#:

.. code-block:: csharp
   :linenos:

    using System;

    public class Queue{
        
        private int front;
        private int rear;
        private double[] arr;

Mira cómo se crea el objeto y se llaman los métodos:

En C:

.. code-block:: c
   :linenos:

    queue_t* q = create(10);
    enqueue(q, 6.5);

.. code-block:: csharp
   :linenos:

   Queue q = new Queue(10);
   q.enqueue(6.5);

En la comparación anterior, notas que la implementación en C# no tiene
código para ``destroy``. ¿Recuerdas por qué es esto?

El programa en C# también podríamos escribirlo así:


.. code-block:: csharp
   :linenos:

    using System;

    public class Queue{
        
        private int front;
        private int rear;
        private double[] arr;
        
        public Queue(int size){
            
            this.front = 0;
            this.rear = 0;
            this.arr = new double[size];
        }    
        
        public int size(){
            return (this.rear - this.front);
        }
        
        public void enqueue(double item) {
            this.arr[rear] = item;
            this.rear++;
        }
        
        public double dequeue() {
            double item = this.arr[front];
            this.front++;
            return item;
        }
    }
    
    
    class Program {
        
      static void Main() {
        Queue q = new Queue(10);
        q.enqueue(6.5);
        q.enqueue(1.3);
        q.enqueue(2.4);
        Console.WriteLine(q.dequeue());
        Console.WriteLine(q.dequeue());
        Console.WriteLine(q.dequeue());
      }
    }

Nota qué cambió con respecto a la primera implementación que te mostré.
¿Lo notaste? En esta segunda implementación estoy utilizando la palabra
reservada ``this``. Esta variable contiene la dirección en memoria del
objecto a través del cual llamamos el método. Observa de nuevo el código
en C. Notas ¿Cómo están relacionados los conceptos?

Ejercicio 73
^^^^^^^^^^^^^^

Cuando DISEÑAS un programa orientado a objetos
también debes considerar las relaciones entre esos objetos. Pues bien, en general
hay dos tipos:

* Relaciones TO-HAVE o HAS-TO (TIENE UN)

* Relaciones TO-BE o IS-A (ES UN) (¿recuerdas la herencia?)

Vamos a concentrarnos primero en las TO-HAVE: la composición y la agregación.

¿Qué es una relación de composición? 

Dos objetos tienen una relación de composición cuando uno de ellos contiene a
otro objeto. Debes tener en cuenta que en una relación de composición la VIDA del objeto
contenido depende de la vida del objeto contenedor, es decir, 
si el objeto contenedor muere, el objeto contenido también. Cuando el objeto
contenedor se va destruir, primero tendrá que hacerse con el objeto contenido.

Mira de nuevo este código:

.. code-block:: c 
   :linenos:

    #include "queue.h"
    #include <stdlib.h> 

    static void init(queue_t* this, int size) {
        this->front = 0;
        this->rear = 0;
        this->arr = (double*)malloc(size * sizeof(double));
    }

    queue_t* create(int size){
        queue_t* q = malloc(sizeof(queue_t));
        init(q,size);
        return(q);
    }



Observa la función ``create``. Dicha función crear una ``queue``.
¿Qué datos componen la cola?

.. code-block:: c 
   :linenos:

    typedef struct {
        int front;
        int rear;
        double* arr;
    } queue_t;

    #endif

A su vez se en ``init`` estamos creando un nuevo objeto que no es más
que un arreglo de ``size`` ``doubles``. La relación entre estos dos objetos
es de composición.  

Ahora nota que al momento de destruir el objeto contenedor, primero se
destruye el objeto contenido:

.. code-block:: c 
   :linenos:

    void destroy(queue_t* this){
        free(this->arr);
        free(this);
    }

Ejercicio 74
^^^^^^^^^^^^^^^^

¿Qué es la agregación?

En esta relación tenemos también un objeto contenedor y un objeto contenido, la
gran diferencia con la composición es que la vida del objeto contenido no depende
de la vida del objeto contenedor. El objeto contenido puede ser construido incluso
antes de que el objeto contenedor sea construido.

Ejercicio 75: MINI-RETO
^^^^^^^^^^^^^^^^^^^^^^^^^

Con todo lo anterior en mente y esta nueva definición, te tengo un mini RETO:

Implementa un programa en C modelado con objetos que implemente una relación de
agregación para esta situación: " ...el jugador recoge un arma, la usa varias veces 
y luego la tira..."

.. note::
    ¡Alerta de Spoiler!

    Una posible implementación a este mini-reto la puedes ver en el siguiente código
    tomado de `este <https://www.packtpub.com/free-ebook/extreme-c/9781789343625>`__ 
    . Le hice unas pequeñas modificaciones al código para que puedas ver el resultado
    en la terminal.

gun.h:

.. code-block:: c 
   :linenos:

	#ifndef GUN_H_
	#define GUN_H_
	
	typedef int bool_t;
	
	// Type forward declarations
	struct gun_t;
	
	// Memory allocator
	struct gun_t* gun_new();
	
	// Constructor
	void gun_ctor(struct gun_t*, int);
	
	// Destructor
	void gun_dtor(struct gun_t*);
	
	// Behavior functions
	bool_t gun_has_bullets(struct gun_t*);
	void gun_trigger(struct gun_t*);
	void gun_refill(struct gun_t*);
	
	
	#endif /* GUN_H_ */

gun.c:

.. code-block:: c 
   :linenos:

	#include <stdlib.h>
	#include <stdio.h>
	
	typedef int bool_t;
	
	// Attribute structure
	typedef struct {
	  int bullets;
	} gun_t;
	
	// Memory allocator
	gun_t* gun_new() {
	  return (gun_t*)malloc(sizeof(gun_t));
	}
	
	// Constructor
	void gun_ctor(gun_t* gun, int initial_bullets) {
	  gun->bullets = 0;
	  if (initial_bullets > 0) {
		gun->bullets = initial_bullets;
	  }
	}
	
	// Destructor
	void gun_dtor(gun_t* gun) {
	  // Nothing to do
	}
	
	// Behavior functions
	bool_t gun_has_bullets(gun_t* gun) {
	  return (gun->bullets > 0);
	}
	
	void gun_trigger(gun_t* gun) {
	  gun->bullets--;
	  printf("gun triggered\n");
	}
	
	void gun_refill(gun_t* gun) {
	  gun->bullets = 7;
	}
	
player.h:

.. code-block:: c 
   :linenos:

	#ifndef PLAYER_H_
	#define PLAYER_H_
	
	// Type forward declarations
	struct player_t;
	struct gun_t;
	
	// Memory allocator
	struct player_t* player_new();
	
	// Constructor
	void player_ctor(struct player_t*, const char*);
	
	// Destructor
	void player_dtor(struct player_t*);
	
	// Behavior functions
	void player_pickup_gun(struct player_t*, struct gun_t*);
	void player_shoot(struct player_t*);
	void player_drop_gun(struct player_t*);
	
	#endif /* PLAYER_H_ */

player.c:

.. code-block:: c 
   :linenos:

	#include <stdlib.h>
	#include <string.h>
	#include <stdio.h>
	
	#include "gun.h"
	
	// Attribute structure
	typedef struct {
	  char* name;
	  struct gun_t* gun;
	} player_t;
	
	// Memory allocator
	player_t* player_new() {
	  return (player_t*)malloc(sizeof(player_t));
	}
	
	// Constructor
	void player_ctor(player_t* player, const char* name) {
	  player->name = (char*)malloc((strlen(name) + 1) * sizeof(char));
	  strcpy(player->name, name);
	  // This is important. We need to nullify aggregation pointers
	  // if they are not meant to be set in constructor.
	  player->gun = NULL;
	}
	
	// Destructor
	void player_dtor(player_t* player) {
	  free(player->name);
	}
	
	// Behavior functions
	void player_pickup_gun(player_t* player, struct gun_t* gun) {
	  // After the following line the aggregation relation begins.
	  player->gun = gun;
	}
	
	void player_shoot(player_t* player) {
	  // We need to check if the player has picked up th gun
	  // otherwise, shooting is meaningless
	  if (player->gun) {
		gun_trigger(player->gun);
	  } else {
		printf("Player wants to shoot but he doesn't have a gun!\n");
		exit(1);
	  }
	}
	
	void player_drop_gun(player_t* player) {
	  // After the following line the aggregation relation
	  // ends between two objects. Note that the object gun
	  // should not be freed since this object is not its
	  // owner like composition.
	  player->gun = NULL;
	}

main.c:

.. code-block:: c 
   :linenos:

	#include <stdio.h>
	#include <stdlib.h>
	#include "gun.h"
	#include "player.h"
	
	int main(int argc, char* argv[]) {
	
		  // Create and constructor the gun object
		  struct gun_t* gun = gun_new();
		  gun_ctor(gun, 3);
	
		  // Create and construct the player object
		  struct player_t* player = player_new();
		  player_ctor(player, "Billy");
	
		  // Begin the aggregation relation.
		  player_pickup_gun(player, gun);
	
		  // Shoot until no bullet is left.
		  while (gun_has_bullets(gun)) {
			player_shoot(player);
		  }
	
		  // Refill the gun
		  gun_refill(gun);
	
		  // Shoot until no bullet is left.
		  while (gun_has_bullets(gun)) {
			player_shoot(player);
		  }
	
		  // End the aggregation relation.
		  player_drop_gun(player);
	
		  // Destruct and free the player object
		  player_dtor(player);
		  free(player);
	
		  // Destruct and free the gun object
		  gun_dtor(gun);
		  free(gun);
	
		  return 0;
	
	}

Ejercicio 76
^^^^^^^^^^^^^

¿Recuerdas que en tu curso de programación y diseño orientado a objetos
vistes las relaciones anteriores?

En ese curso a los dos relaciones anteriores: agregación y composición
se les denomina en general asociaciones, es decir, dos objetos pueden estar
asociados mediante una relación de agregación o composición.

Estas relaciones pueden mostrarse de manera gráfica utilizando un
lenguaje de modelado conocido como `UML <http://uml.org/>`__. Te dejo aquí
una imagen:

.. image:: ../_static/UMLasoc.png

Ejercicio 77
^^^^^^^^^^^^^

¿Te animas a realizar un modelo UML para nuestros dos ejemplos de composición
y agregación?

Ejercicio 78
^^^^^^^^^^^^^

El otro tipo de relación que podemos tener entre dos objetos es la relación TO-BE, 
mejor conocida como herencia. 

¿Cómo funciona la herencia?

En términos simples, la herencia permite añadirle a un objeto atributos de otro
objeto. 

.. code-block:: c
   :linenos:

	typedef struct {
		char first_name[32];
		char last_name[32];
		unsigned int birth_year;
	} person_t;

	typedef struct {
		char first_name[32];
		char last_name[32];
		unsigned int birth_year;
		char student_number[16]; // Extra attribute
		unsigned int passed_credits; // Extra attribute
	} student_t;

En el ejemplo anterior (tomado del de `aquí <https://www.packtpub.com/free-ebook/extreme-c/9781789343625>`__
nota los atributos de la estructura person_t y student_t. ¿Ves alguna relación entre ellos?

student_t ``extiende`` los atributos de person_t. Por tanto, podemos decir que student_t también
ES UN (IS-A) person_t.

Observa entonces que podemos escribir de nuevo el código anterior así:

.. code-block:: c
   :linenos:

	typedef struct {
		char first_name[32];
		char last_name[32];
		unsigned int birth_year;
	} person_t;
	
	typedef struct {
		person_t person;
		char student_number[16]; // Extra attribute
		unsigned int passed_credits; // Extra attribute
	}student_t;

¿Ves lo que pasó? estamos anidando una estructura en otra estructura. Por tanto student_t hereda
de person_t. Observa que un puntero a student_t estará apuntando al primer atributo que es
un person_t. ¿Lo ves? Por eso decimos que un student_t también ES UN person_t. Míralo en acción
aquí:

.. code-block:: c
   :linenos:

    #include <stdio.h>

    typedef struct {
        char first_name[32];
        char last_name[32];
        unsigned int birth_year;
    }person_t;

    typedef struct {
        person_t person;
        char student_number[16]; // Extra attribute
        unsigned int passed_credits; // Extra attribute
    } student_t;

    int main(int argc, char* argv[]) {
        student_t s;
        student_t* s_ptr = &s;
        person_t* p_ptr = (person_t*)&s;
        printf("Student pointer points to %p\n", (void*)s_ptr);
        printf("Person pointer points to %p\n", (void*)p_ptr);
        return 0;
    }

Ejercicio 79
^^^^^^^^^^^^^^^^^^


En este punto te pido que te pongas cómodo. Lo que viene será alucinante...

Del ejercicio anterior concluimos que student_t está heredando de person_t.
Por tanto, a las funciones que definas para manipular un objeto de tipo
person_t también le puedes pasar un puntero a un student_t (para manipular
sus atributos correspondiente a person_t). SEÑORES y SEÑORAS, estamos
reutilizando código.

Ejercicio 80
^^^^^^^^^^^^^^^^^^

Ahora te voy a mostrar una técnica para implementar herencia simple en C.
Analiza con detenimiento este código por favor 
(`tomado de aquí <https://www.packtpub.com/free-ebook/extreme-c/9781789343625>`__):

person.h:

.. code-block:: c
   :linenos:

	#ifndef PERSON_H_
	#define PERSON_H_
	
	// Forward declaration
	struct person_t;
	
	// Memory allocator
	struct person_t* person_new();
	
	// Constructor
	void person_ctor(struct person_t*,
	const char* /* first name */,
	const char* /* last name */,
	unsigned int /* birth year */);
	
	// Destructor
	void person_dtor(struct person_t*);
	
	// Behavior functions
	void person_get_first_name(struct person_t*, char*);
	void person_get_last_name(struct person_t*, char*);
	unsigned int person_get_birth_year(struct person_t*);
	
	#endif /* PERSON_H_ */

person.c:

.. code-block:: c
   :linenos:

	#include <stdlib.h>
	#include <string.h>
	#include <stdlib.h>
	#include "personPrivate.h"
	
	// Memory allocator
	person_t* person_new() {
		return malloc(sizeof(person_t));
	}
	
	// Constructor
	void person_ctor(person_t* person,
			const char* first_name,
			const char* last_name,
			unsigned int birth_year) {
	
				strcpy(person->first_name, first_name);
				strcpy(person->last_name, last_name);
				person->birth_year = birth_year;
	}
	
	// Destructor
	void person_dtor(person_t* person) {
		// Nothing to do
	}
	
	// Behavior functions
	void person_get_first_name(person_t* person, char* buffer) {
		strcpy(buffer, person->first_name);
	}
	
	void person_get_last_name(person_t* person, char* buffer) {
		strcpy(buffer, person->last_name);
	}
	
	unsigned int person_get_birth_year(person_t* person) {
		return person->birth_year;
	}

personPrivate.h:

.. code-block:: c
   :linenos:

	#ifndef PERSONPRIVATE_H_
	#define PERSONPRIVATE_H_
	
	// Private definition
	typedef struct {
		char first_name[32];
		char last_name[32];
		unsigned int birth_year;
	} person_t;
	
	
	#endif /* PERSONPRIVATE_H_ */

student.h:

.. code-block:: c
   :linenos:

	#ifndef STUDENT_H_
	#define STUDENT_H_
	
	//Forward declaration
	struct student_t;
	
	// Memory allocator
	struct student_t* student_new();
	
	// Constructor
	void student_ctor(struct student_t*,
					const char* /* first name */,
					const char* /* last name */,
					unsigned int /* birth year */,
					const char* /* student number */,
					unsigned int /* passed credits */);
	
	// Destructor
	void student_dtor(struct student_t*);
	
	// Behavior functions
	void student_get_student_number(struct student_t*, char*);
	unsigned int student_get_passed_credits(struct student_t*);
	
	#endif /* STUDENT_H_ */

student.c:

.. code-block:: c
   :linenos:

	#include <stdlib.h>
	#include <stdio.h>
	#include <string.h>
	
	
	#include "person.h"
	#include "personPrivate.h"
	
	
	//Forward declaration
	typedef struct {
	// Here, we inherit all attributes from the person class and
	// also we can use all of its behavior functions because of
	// this nesting.
		person_t person;
		char* student_number;
		unsigned int passed_credits;
	} student_t;
	
	// Memory allocator
	student_t* student_new() {
		return (student_t*)malloc(sizeof(student_t));
	}
	
	// Constructor
	void student_ctor(student_t* student,
					const char* first_name,
					const char* last_name,
					unsigned int birth_year,
					const char* student_number,
					unsigned int passed_credits) {
	
		// Call the constructor of the parent class
		person_ctor((struct person_t*)student,
		first_name, last_name, birth_year);
		student->student_number = (char*)malloc(16 * sizeof(char));
		strcpy(student->student_number, student_number);
		student->passed_credits = passed_credits;
	}
	
	// Destructor
	void student_dtor(student_t* student) {
		// We need to destruct the child object first.
		free(student->student_number);
		// Then, we need to call the destructor function
		// of the parent class
		person_dtor((struct person_t*)student);
	}
	
	// Behavior functions
	void student_get_student_number(student_t* student,
			char* buffer) {
			strcpy(buffer, student->student_number);
	}
	
	unsigned int student_get_passed_credits(student_t* student) {
		return student->passed_credits;
	}

main.c:

.. code-block:: c
   :linenos:

	#include <stdio.h>
	#include <stdlib.h>
	#include "person.h"
	#include "student.h"
	
	int main(int argc, char* argv[]) {
		// Create and construct the student object
		struct student_t* student = student_new();
		student_ctor(student, "John", "Doe", 1987, "TA5667", 134);
	
		// Now, we use person's behavior functions to
		// read person's attributes from the student object
		char buffer[32];
	
		// Upcasting to a pointer of parent type
		struct person_t* person_ptr = (struct person_t*)student;
		person_get_first_name(person_ptr, buffer);
		printf("First name: %s\n", buffer);
		person_get_last_name(person_ptr, buffer);
		printf("Last name: %s\n", buffer);
		printf("Birth year: %d\n", person_get_birth_year(person_ptr));
	
		// Now, we read the attributes specific to the student object.
		student_get_student_number(student, buffer);
		printf("Student number: %s\n", buffer);
		printf("Passed credits: %d\n",
		student_get_passed_credits(student));
	
		// Destruct and free the student object
		student_dtor(student);
		free(student);
		return 0;
	}

Ejercicio 81
^^^^^^^^^^^^^^^^^^

Ahora te voy a mostrar una técnica para implementar polimorfismo en tiempo de 
ejecución en C (`tomado de aquí <https://www.packtpub.com/free-ebook/extreme-c/9781789343625>`__).

Pero antes ¿Qué es el polimorfismo en tiempo de ejecución? Antes mira qué te permite hacer
el polimorfismo. Considera que tienes estos tres objetos:

.. code-block:: c
   :linenos:

	struct animal_t* animal = animal_new();
	animal_ctor(animal);

	struct cat_t* cat = cat_new();
	cat_ctor(cat);

	struct duck_t* duck = duck_new();
	duck_ctor(duck);

cat y duck heredan de animal. Por tanto, como cat y duck son animal también,
entonces al hacer esto:

.. code-block:: c
   :linenos:

	// This is a polymorphism
	animal_sound(animal);
	animal_sound((struct animal_t*)cat);
	animal_sound((struct animal_t*)duck);

Consigues esta salida:

.. code-block:: c
   :linenos:

	Animal: Beeeep
	Cat: Meow
	Duck: Quack

Entonces puedes ver que la función animal_sound exhibe un comportamiento polimórfico
dependiendo del tipo de referencia que le pasemos.

¿Para qué sirve esto? Supón que tienes un código base al cual quieres adicionarle
funcionalidades nuevas. El polimorfismo te permite mantener el código base lo más intacto
posible a medida que añades más comportamientos por medio de la herencia.

Ahora, si. Mira cómo se puede implementar:

animal.h:

.. code-block:: c
   :linenos:

	#ifndef ANIMAL_H_
	#define ANIMAL_H_
	
	// Forward declaration
	struct animal_t;
	
	// Memory allocator
	struct animal_t* animal_new();
	
	// Constructor
	void animal_ctor(struct animal_t*);
	
	// Destructor
	void animal_dtor(struct animal_t*);
	
	// Behavior functions
	void animal_get_name(struct animal_t*, char*);
	void animal_sound(struct animal_t*);
	
	
	#endif /* ANIMAL_H_ */

animal.c:

.. code-block:: c
   :linenos:

	#include <stdlib.h>
	#include <string.h>
	#include <stdio.h>
	
	#include "animalPrivate.h"
	
	// Default definition of the animal_sound at the parent level
	void __animal_sound(void* this_ptr) {
		animal_t* animal = (animal_t*)this_ptr;
		printf("%s: Beeeep\n", animal->name);
	}
	
	// Memory allocator
	animal_t* animal_new() {
		return (animal_t*)malloc(sizeof(animal_t));
	}
	
	// Constructor
	void animal_ctor(animal_t* animal) {
		animal->name = (char*)malloc(10 * sizeof(char));
		strcpy(animal->name, "Animal");
		// Set the function pointer to point to the default definition
		animal->sound_func = __animal_sound;
	}
	
	// Destructor
	void animal_dtor(animal_t* animal) {
		free(animal->name);
	}
	// Behavior functions
	void animal_get_name(animal_t* animal, char* buffer) {
		strcpy(buffer, animal->name);
	}
	
	void animal_sound(animal_t* animal) {
		// Call the function which is pointed by the function pointer.
		animal->sound_func(animal);
	}


animalPrivate.h:

.. code-block:: c
   :linenos:

	#ifndef ANIMALPRIVATE_H_
	#define ANIMALPRIVATE_H_
	
	// The function pointer type needed to point to
	// different morphs of animal_sound
	typedef void (*sound_func_t)(void*);
	
	// Forward declaration
	typedef struct {
		char* name;
		// This member is a pointer to the function which
		// performs the actual sound behavior
		sound_func_t sound_func;
	} animal_t;
	
	#endif /* ANIMALPRIVATE_H_ */


cat.h:

.. code-block:: c
   :linenos:

	#ifndef CAT_H_
	#define CAT_H_
	
	// Forward declaration
	struct cat_t;
	
	// Memory allocator
	struct cat_t* cat_new();
	
	// Constructor
	void cat_ctor(struct cat_t*);
	
	// Destructor
	void cat_dtor(struct cat_t*);
	// All behavior functions are inherited from the animal class.
	
	#endif /* CAT_H_ */

cat.c:

.. code-block:: c
   :linenos:

	#include <stdio.h>
	#include <stdlib.h>
	#include <string.h>
	
	#include "animal.h"
	#include "animalPrivate.h"
	
	typedef struct {
		animal_t animal;
	} cat_t;
	
	// Define a new behavior for the cat's sound
	void __cat_sound(void* ptr) {
		animal_t* animal = (animal_t*)ptr;
		printf("%s: Meow\n", animal->name);
	}
	
	// Memory allocator
	cat_t* cat_new() {
		return (cat_t*)malloc(sizeof(cat_t));
	}
	// Constructor
	void cat_ctor(cat_t* cat) {
		animal_ctor((struct animal_t*)cat);
		strcpy(cat->animal.name, "Cat");
		// Point to the new behavior function. Overriding
		// is actually happening here.
		cat->animal.sound_func = __cat_sound;
	}
	
	// Destructor
	void cat_dtor(cat_t* cat) {
		animal_dtor((struct animal_t*)cat);
	}

duck.h:

.. code-block:: c
   :linenos:

	
	#ifndef DUCK_H_
	#define DUCK_H_
	
	// Forward declaration
	struct duck_t;
	
	// Memory allocator
	struct duck_t* duck_new();
	
	// Constructor
	void duck_ctor(struct duck_t*);
	
	// Destructor
	void duck_dtor(struct duck_t*);
	
	// All behavior functions are inherited from the animal class.
	
	
	#endif /* DUCK_H_ */

duck.c:

.. code-block:: c
   :linenos:

	#include <stdio.h>
	#include <stdlib.h>
	#include <string.h>
	
	#include "animal.h"
	#include "animalPrivate.h"
	
	typedef struct {
		animal_t animal;
	} duck_t;
	
	// Define a new behavior for the duck's sound
	void __duck_sound(void* ptr) {
		animal_t* animal = (animal_t*)ptr;
		printf("%s: Quacks\n", animal->name);
	}
	
	// Memory allocator
	duck_t* duck_new() {
		return (duck_t*)malloc(sizeof(duck_t));
	}
	
	// Constructor
	void duck_ctor(duck_t* duck) {
		animal_ctor((struct animal_t*)duck);
		strcpy(duck->animal.name, "Duck");
		// Point to the new behavior function. Overriding
		// is actually happening here.
		duck->animal.sound_func = __duck_sound;
	}
	
	// Destructor
	void duck_dtor(duck_t* duck) {
		animal_dtor((struct animal_t*)duck);
	}


main.c:

.. code-block:: c
   :linenos:

	#include <stdio.h>
	#include <stdlib.h>
	#include <string.h>
	
	// Only public interfaces
	#include "animal.h"
	#include "cat.h"
	#include "duck.h"
	
	
	int main(int argc, char** argv) {
		struct animal_t* animal = animal_new();
		struct cat_t* cat = cat_new();
		struct duck_t* duck = duck_new();
	
		animal_ctor(animal);
		cat_ctor(cat);
		duck_ctor(duck);
	
		animal_sound(animal);
		animal_sound((struct animal_t*)cat);
		animal_sound((struct animal_t*)duck);
	
		animal_dtor(animal);
		cat_dtor(cat);
		duck_dtor(duck);
	
		free(duck);
		free(cat);
		free(animal);
		return 0;
	}

Ejercicio 82
^^^^^^^^^^^^^^^^

¿Qué son las clases abstractas? Son un tipo de clases de las cuales no puedes
crear OBJETOS. Entonces ¿Para qué sirven? Sirven para crear programas
orientados a objetos que puedan extenderse al máximo y con la menor cantidad
de dependencias entre sus componentes. ¿Te suena que vale la pena?

Mira este problema: tienes que construir una biblioteca que te permita comunicar,
por un puerto serial, a Unity con un sensor. Las responsabilidades del código
son: gestionar el puerto serial, gestionar la comunicación con el hilo
principal o hilo del motor y enviar-recibir datos siguiendo un protocolo específico.
En este escenario podrías escribir una biblioteca que resuelva este problema solo
para el sensor particular o escribirla de tal manera que puedas reutilizar
casi todo el código y solo cambiar el protocolo de comunicación si a futuro
cambias de sensor.

¿Cuál de las dos opciones de suena más?

Si te suena más la segunda, entonces todas las partes comunes del código irán
en la clase abstracta y las partes que varían, en este caso el protocolo de comunicación,
irán en otra clase que herede de la clase abstracta. Aquí entra en juego el otro concepto
que estudiamos, el POLIMORFISMO, ¿Cómo? En el código de la clase
abstracta se llamará el código que varía o métodos VIRTUALES, pero este código no estará 
implementado. Por tanto, los métodos virtuales tendrás que implementarlo en la clase que
hereda, de la cual, si PUEDES crear OBJETOS. Hermoso, ¿No?.

En lenguajes de programación como C# se hace
`así <https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/abstract>`__.
En C++ sería `así <https://www.geeksforgeeks.org/virtual-function-cpp/>`__.

Ten presente que en la medida que llevas al extremo este concepto de abstracción podrás
llegar a clases que no tengan atributos sino SOLO métodos virtuales. En este punto habrás
llegado a las INTERFACES, de las cuales tampoco podrás crear objetos.

PROYECTO 2
^^^^^^^^^^^

Realiza un programa y su modelo de clases UML. Para una aplicación
que permita crear bases de datos de estudiantes.

Cada registro de la base de datos estará dado por:
número de cédula, nombre y semestre. Cada registro corresponde a un 
estudiante.

Implementa los siguientes comandos:

**exit** : salir del programa. Antes de terminar debe mostrar el nombre
de la base de datos activa y solicitar si desea guardarla.

**mdb nombre tamaño** : crea EN MEMORIA una base de datos especificando el nombre
y la cantidad de registros.

**ldb nombre** : carga TODA la base de datos en MEMORIA desde el archivo
especificado. El comando debe indicar si la base de datos se cargó
correctamente o no existe.

Una vez la base de datos esté cargada en memoria desde el archivo o con ``mdb``
puedes aplicar los siguientes comandos:

**lsdbs** : este comando mostrará todas las bases de datos que tengas cargadas
en la memoria indicando su nombre, tamaño y cantidad de registros almacenados.

**gdb**: muestra el nombre de la base de datos activa, qué tamaño tiene
y cuántos registros le quedan disponibles.

**sdb nombre**: este comando selecciona la base de datos activa para aplicar
los siguientes comandos:

**svdb** : este comando salva la base de datos activa en un archivo
con el mismo nombre de la base de datos.

**radb** : lee todos los registros de la base de datos.

**rsdb** : lee la cantidad de registros de la base datos.

**mreg cedula nombre semestre** : crea un nuevo registro en la base
de datos.

**rr cédula** : busca en la base de datos por número de cédula.
En caso de encontrar la cédula imprime el registro completo.

No olvides:

* Cada comando deberá implementarse como una función.
* En un momento dado puedes tener ``varias`` bases de datos en memoria.

