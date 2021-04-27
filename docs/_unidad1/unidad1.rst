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
el tiempo de ejecución y el "tiempo ocioso" en cualquier lenguaje de programación que el usuario quiera definir. "

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

||||||| WIP

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

    fn main(){

    }

Compila el archivo anterior para producir una librería dinámica, generará un archivo llamado **libsum.so** en la misma carpeta:

``rustc --crate-type=cdylib sum.rs``

Ahora observa los símbolos definidos en libsum.rlib utilizando el siguiente comando:

``nm libsum.so``

El resultado será:

.. code-block:: bash

    0000000000004008 b completed.8060
    w __cxa_finalize@@GLIBC_2.2.5
    0000000000001040 t deregister_tm_clones
    00000000000010b0 t __do_global_dtors_aux
    0000000000003d28 d __do_global_dtors_aux_fini_array_entry
    0000000000004000 d __dso_handle
    0000000000003d90 d _DYNAMIC
    00000000000015f4 t _fini
    00000000000010f0 t frame_dummy
    0000000000003d20 d __frame_dummy_init_array_entry
    000000000000222c r __FRAME_END__
    0000000000003f80 d _GLOBAL_OFFSET_TABLE_
    w __gmon_start__
    0000000000002058 r __GNU_EH_FRAME_HDR
    0000000000001000 t _init
    w _ITM_deregisterTMCloneTable
    w _ITM_registerTMCloneTable
    U pthread_mutex_lock@@GLIBC_2.2.5
    U pthread_mutex_unlock@@GLIBC_2.2.5
    0000000000001070 t register_tm_clones
    0000000000001310 T rust_eh_personality
    0000000000004008 d __TMC_END__
    U _Unwind_GetDataRelBase@@GCC_3.0
    U _Unwind_GetIPInfo@@GCC_4.2.0
    U _Unwind_GetLanguageSpecificData@@GCC_3.0
    U _Unwind_GetRegionStart@@GCC_3.0
    U _Unwind_GetTextRelBase@@GCC_3.0
    U _Unwind_SetGR@@GCC_3.0
    U _Unwind_SetIP@@GCC_3.0
    0000000000001170 t _ZN12panic_unwind5dwarf2eh20read_encoded_pointer17hbec45f6509d5d74aE
    00000000000012f0 t _ZN12panic_unwind8real_imp14find_eh_action28_$u7b$$u7b$closure$u7d$$u7d$17hdd2451d83f6b6178E
    0000000000001300 t _ZN12panic_unwind8real_imp14find_eh_action28_$u7b$$u7b$closure$u7d$$u7d$17heeb8101b14e5ebf6E
    0000000000001100 t _ZN3std3sys4unix4args3imp15ARGV_INIT_ARRAY12init_wrapper17h9bae8a0cafc2b6ccE
    0000000000003d18 d _ZN3std3sys4unix4args3imp15ARGV_INIT_ARRAY17h5b809bb581f98cb0E
    0000000000004010 b _ZN3std3sys4unix4args3imp4ARGC17h393a33c6be9e9b3bE
    0000000000004018 b _ZN3std3sys4unix4args3imp4ARGV17h5274ca72b78295baE
    0000000000004020 b _ZN3std3sys4unix4args3imp4LOCK17h600045dca3348f0eE
    0000000000001140 t _ZN4core3ops8function6FnOnce40call_once$u7b$$u7b$vtable.shim$u7d$$u7d$17h0318dffd3a9d1c14E
    0000000000001150 t _ZN4core3ops8function6FnOnce40call_once$u7b$$u7b$vtable.shim$u7d$$u7d$17h3dfb55efa1414d46E
    0000000000001160 t _ZN4core3ptr88drop_in_place$LT$panic_unwind..real_imp..find_eh_action..$u7b$$u7b$closure$u7d$$u7d$$GT$17haf97ab3c90a49e7cE


En el archivo generado encontramos una gran cantidad de símbolos, no podemos identificarlos, esto es porque
el compilador de rust no solo ha compilado nuestro código sino que ha agregado algunas cosas resultado
de los análisis y optimizaciones que vimos en los ejercicios anteriores. Las funciones que definimos en si se encuentran 
entre estos símbolos, pero su nombre o identificador ha cambiado debido a un proceso llamado **Name Mangling** necesario
para la etapa de linking. Por ejemplo, dos funciones que tengan el mismo nombre pero se encuentren en librerías diferentes
podrían causar que el enlazador tome los datos de una función en lugar de la otra por erorr.

``readelf -s libsum.so``

Obtendrás esto:

.. code-block:: bash

    S
    Symbol table '.dynsym' contains 67 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND getenv@GLIBC_2.2.5 (2)
         2: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND dl_iterate_phdr@GLIBC_2.2.5 (2)
         3: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND free@GLIBC_2.2.5 (2)
         4: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND abort@GLIBC_2.2.5 (2)
         5: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_Backtrace@GCC_3.3 (3)
         6: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND __errno_location@GLIBC_2.2.5 (4)
         7: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_getattr_np@GLIBC_2.2.5 (4)
         8: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND _ITM_deregisterTMCloneTab
         9: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND writev@GLIBC_2.2.5 (2)
        10: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND sigaction@GLIBC_2.2.5 (4)
        11: 0000000000000000     0 FUNC    WEAK   DEFAULT  UND __cxa_thread_atexit_impl@GLIBC_2.18 (5)
        12: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND __xpg_strerror_r@GLIBC_2.3.4 (6)
        13: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND readlink@GLIBC_2.2.5 (2)
        14: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetRegionStart@GCC_3.0 (7)
        15: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND write@GLIBC_2.2.5 (4)
        16: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetTextRelBase@GCC_3.0 (7)
        17: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_RaiseException@GCC_3.0 (7)
        18: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND strlen@GLIBC_2.2.5 (2)
        19: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND mmap@GLIBC_2.2.5 (2)
        20: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_setspecific@GLIBC_2.2.5 (4)
        21: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_mutex_destroy@GLIBC_2.2.5 (4)
        22: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND memset@GLIBC_2.2.5 (2)
        23: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND getcwd@GLIBC_2.2.5 (2)
        24: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetIPInfo@GCC_4.2.0 (8)
        25: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND close@GLIBC_2.2.5 (4)
        26: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_attr_getstack@GLIBC_2.2.5 (4)
        27: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetLanguageSpecif@GCC_3.0 (7)
        28: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND memchr@GLIBC_2.2.5 (2)
        29: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND __libc_start_main@GLIBC_2.2.5 (2)
        30: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND __tls_get_addr@GLIBC_2.3 (9)
        31: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_rwlock_rdlock@GLIBC_2.2.5 (4)
        32: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND calloc@GLIBC_2.2.5 (2)
        33: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND __fxstat64@GLIBC_2.2.5 (2)
        34: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND signal@GLIBC_2.2.5 (2)
        35: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND syscall@GLIBC_2.2.5 (2)
        36: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND __gmon_start__
        37: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND memcpy@GLIBC_2.14 (10)
        38: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetIP@GCC_3.0 (7)
        39: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_getspecific@GLIBC_2.2.5 (4)
        40: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_mutex_unlock@GLIBC_2.2.5 (4)
        41: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND malloc@GLIBC_2.2.5 (2)
        42: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND bcmp@GLIBC_2.2.5 (2)
        43: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_rwlock_unlock@GLIBC_2.2.5 (4)
        44: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND realloc@GLIBC_2.2.5 (2)
        45: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND munmap@GLIBC_2.2.5 (2)
        46: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_key_create@GLIBC_2.2.5 (4)
        47: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetDataRelBase@GCC_3.0 (7)
        48: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND poll@GLIBC_2.2.5 (2)
        49: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_SetGR@GCC_3.0 (7)
        50: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND open64@GLIBC_2.2.5 (4)
        51: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND memmove@GLIBC_2.2.5 (2)
        52: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_self@GLIBC_2.2.5 (2)
        53: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND mprotect@GLIBC_2.2.5 (2)
        54: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND open@GLIBC_2.2.5 (4)
        55: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND sysconf@GLIBC_2.2.5 (2)
        56: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_attr_destroy@GLIBC_2.2.5 (2)
        57: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_key_delete@GLIBC_2.2.5 (4)
        58: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND posix_memalign@GLIBC_2.2.5 (2)
        59: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND _ITM_registerTMCloneTable
        60: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_DeleteException@GCC_3.0 (7)
        61: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND sigaltstack@GLIBC_2.2.5 (2)
        62: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND dlsym@GLIBC_2.2.5 (11)
        63: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_Resume@GCC_3.0 (7)
        64: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_mutex_lock@GLIBC_2.2.5 (4)
        65: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_SetIP@GCC_3.0 (7)
        66: 0000000000000000     0 FUNC    WEAK   DEFAULT  UND __cxa_finalize@GLIBC_2.2.5 (2)
    
    Symbol table '.symtab' contains 674 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 00000000000002e0     0 SECTION LOCAL  DEFAULT    1 
         2: 00000000000002fc     0 SECTION LOCAL  DEFAULT    2 
         3: 0000000000000320     0 SECTION LOCAL  DEFAULT    3 
         4: 0000000000000340     0 SECTION LOCAL  DEFAULT    4 
         5: 0000000000000368     0 SECTION LOCAL  DEFAULT    5 
         6: 00000000000009b0     0 SECTION LOCAL  DEFAULT    6 
         7: 0000000000000de6     0 SECTION LOCAL  DEFAULT    7 
         8: 0000000000000e70     0 SECTION LOCAL  DEFAULT    8 
         9: 0000000000000f60     0 SECTION LOCAL  DEFAULT    9 
        10: 00000000000047d0     0 SECTION LOCAL  DEFAULT   10 
        11: 0000000000005000     0 SECTION LOCAL  DEFAULT   11 
        12: 0000000000005020     0 SECTION LOCAL  DEFAULT   12 
        13: 0000000000005060     0 SECTION LOCAL  DEFAULT   13 
        14: 0000000000005070     0 SECTION LOCAL  DEFAULT   14 
        15: 0000000000032914     0 SECTION LOCAL  DEFAULT   15 
        16: 0000000000033000     0 SECTION LOCAL  DEFAULT   16 
        17: 0000000000037780     0 SECTION LOCAL  DEFAULT   17 
        18: 00000000000384a8     0 SECTION LOCAL  DEFAULT   18 
        19: 000000000003cb98     0 SECTION LOCAL  DEFAULT   19 
        20: 000000000003e8b0     0 SECTION LOCAL  DEFAULT   20 
        21: 000000000003e8b0     0 SECTION LOCAL  DEFAULT   21 
        22: 000000000003e8c0     0 SECTION LOCAL  DEFAULT   22 
        23: 000000000003e8c8     0 SECTION LOCAL  DEFAULT   23 
        24: 00000000000407d8     0 SECTION LOCAL  DEFAULT   24 
        25: 0000000000040a08     0 SECTION LOCAL  DEFAULT   25 
        26: 0000000000041000     0 SECTION LOCAL  DEFAULT   26 
        27: 0000000000041050     0 SECTION LOCAL  DEFAULT   27 
        28: 0000000000000000     0 SECTION LOCAL  DEFAULT   28 
        29: 0000000000000000     0 SECTION LOCAL  DEFAULT   29 
        30: 0000000000000000     0 SECTION LOCAL  DEFAULT   30 
        31: 0000000000000000     0 SECTION LOCAL  DEFAULT   31 
        32: 0000000000000000     0 SECTION LOCAL  DEFAULT   32 
        33: 0000000000000000     0 SECTION LOCAL  DEFAULT   33 
        34: 0000000000000000     0 SECTION LOCAL  DEFAULT   34 
        35: 0000000000000000     0 SECTION LOCAL  DEFAULT   35 
        36: 0000000000000000     0 SECTION LOCAL  DEFAULT   36 
        37: 0000000000000000     0 SECTION LOCAL  DEFAULT   37 
        38: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS std.9m6hw7w6-cgu.0
        39: 000000000003cee0     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1004
        40: 000000000003cf2c     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1005
        41: 000000000003cf5c     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1010
        42: 000000000003cf6c     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1013
        43: 000000000003cf80     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1014
        44: 000000000003cf90     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1015
        45: 000000000003cf9c     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1027
        46: 000000000003cbc0     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table118
        47: 000000000003cbcc     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table120
        48: 000000000003cfc8     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1217
        49: 000000000003cfe4     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1259
        50: 000000000003d00c     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1285
        51: 000000000003d028     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1286
        52: 000000000003d040     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1338
        53: 000000000003d04c     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1341
        54: 000000000003d05c     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1342
        55: 000000000003d138     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1343
        56: 000000000003d158     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1344
        57: 000000000003d280     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1348
        58: 000000000003cbd8     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table135
        59: 000000000003cbf0     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table151
        60: 000000000003cbfc     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table207
        61: 000000000003cc08     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table212
        62: 000000000003cc14     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table220
        63: 000000000003cc28     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table287
        64: 000000000003cc38     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table305
        65: 000000000003ccc0     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table306
        66: 000000000003cce8     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table330
        67: 000000000003cd04     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table352
        68: 000000000003cd14     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table426
        69: 000000000003cd24     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table497
        70: 000000000003cd40     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table547
        71: 000000000003cd58     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table651
        72: 000000000003cd70     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table652
        73: 000000000003cd88     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table653
        74: 000000000003cda0     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table658
        75: 000000000003cdb8     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table901
        76: 000000000003cdd4     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table906
        77: 000000000003cbb4     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table93
        78: 000000000003ce0c     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table938
        79: 000000000003ce24     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table940
        80: 000000000003ce3c     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table941
        81: 000000000003ce50     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table944
        82: 000000000003ce60     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table975
        83: 000000000003ce7c     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table976
        84: 000000000003cea4     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table977
        85: 000000000003cebc     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table981
        86: 000000000003cecc     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table983
        87: 0000000000007780    11 FUNC    LOCAL  DEFAULT   14 _ZN36_$LT$T$u20$as$u20$co
        88: 0000000000007790    11 FUNC    LOCAL  DEFAULT   14 _ZN36_$LT$T$u20$as$u20$co
        89: 00000000000077a0    11 FUNC    LOCAL  DEFAULT   14 _ZN36_$LT$T$u20$as$u20$co
        90: 0000000000041080    40 OBJECT  LOCAL  DEFAULT   27 _ZN3std10sys_common11at_e
        91: 00000000000410a8     8 OBJECT  LOCAL  DEFAULT   27 _ZN3std10sys_common11at_e
        92: 0000000000015ad0   362 FUNC    LOCAL  DEFAULT   14 _ZN3std10sys_common11thre
        93: 0000000000000020    56 TLS     LOCAL  DEFAULT   20 _ZN3std10sys_common11thre
        94: 0000000000041018    16 OBJECT  LOCAL  DEFAULT   26 _ZN3std10sys_common17thre
        95: 0000000000015e40   317 FUNC    LOCAL  DEFAULT   14 _ZN3std10sys_common17thre
        96: 0000000000016070   150 FUNC    LOCAL  DEFAULT   14 _ZN3std10sys_common4util1
        97: 0000000000016170   284 FUNC    LOCAL  DEFAULT   14 _ZN3std10sys_common4util1
        98: 0000000000016110    87 FUNC    LOCAL  DEFAULT   14 _ZN3std10sys_common4util5
        99: 00000000000410e0     8 OBJECT  LOCAL  DEFAULT   27 _ZN3std10sys_common7clean
       100: 00000000000151d0    52 FUNC    LOCAL  DEFAULT   14 _ZN3std10sys_common9backt
       101: 0000000000015440   326 FUNC    LOCAL  DEFAULT   14 _ZN3std10sys_common9backt
       102: 0000000000015210   556 FUNC    LOCAL  DEFAULT   14 _ZN3std10sys_common9backt
       103: 00000000000155d0   363 FUNC    LOCAL  DEFAULT   14 _ZN3std10sys_common9backt
       104: 00000000000410d8     8 OBJECT  LOCAL  DEFAULT   27 _ZN3std10sys_common9backt
       105: 0000000000015590    30 FUNC    LOCAL  DEFAULT   14 _ZN3std10sys_common9backt
       106: 00000000000155b0    30 FUNC    LOCAL  DEFAULT   14 _ZN3std10sys_common9backt
       107: 00000000000410b0    40 OBJECT  LOCAL  DEFAULT   27 _ZN3std10sys_common9backt
       108: 0000000000017980  1603 FUNC    LOCAL  DEFAULT   14 _ZN3std12backtrace_rs5pri
       109: 0000000000019330    68 FUNC    LOCAL  DEFAULT   14 _ZN3std12backtrace_rs9bac
       110: 00000000000223e0   907 FUNC    LOCAL  DEFAULT   14 _ZN3std12backtrace_rs9sym
       111: 00000000000411e0    48 OBJECT  LOCAL  DEFAULT   27 _ZN3std12backtrace_rs9sym
       112: 0000000000019470   216 FUNC    LOCAL  DEFAULT   14 _ZN3std12backtrace_rs9sym
       113: 0000000000019550 19413 FUNC    LOCAL  DEFAULT   14 _ZN3std12backtrace_rs9sym
       114: 000000000001e130   662 FUNC    LOCAL  DEFAULT   14 _ZN3std12backtrace_rs9sym
       115: 000000000001e3d0 16400 FUNC    LOCAL  DEFAULT   14 _ZN3std12backtrace_rs9sym
       116: 0000000000022770   986 FUNC    LOCAL  DEFAULT   14 _ZN3std12backtrace_rs9sym
       117: 0000000000017890   228 FUNC    LOCAL  DEFAULT   14 _ZN3std12backtrace_rs9sym
       118: 00000000000134e0   620 FUNC    LOCAL  DEFAULT   14 _ZN3std2io5Write18write_a
       119: 0000000000013750   579 FUNC    LOCAL  DEFAULT   14 _ZN3std2io5Write18write_a
       120: 00000000000133f0   236 FUNC    LOCAL  DEFAULT   14 _ZN3std2io5Write9write_al
       121: 00000000000139a0   323 FUNC    LOCAL  DEFAULT   14 _ZN3std2io5Write9write_fm
       122: 0000000000013af0   323 FUNC    LOCAL  DEFAULT   14 _ZN3std2io5Write9write_fm
       123: 00000000000131d0   397 FUNC    LOCAL  DEFAULT   14 _ZN3std2io5impls74_$LT$im
       124: 0000000000013360     3 FUNC    LOCAL  DEFAULT   14 _ZN3std2io5impls74_$LT$im
       125: 00000000000133e0     8 FUNC    LOCAL  DEFAULT   14 _ZN3std2io5impls74_$LT$im
       126: 0000000000013160   107 FUNC    LOCAL  DEFAULT   14 _ZN3std2io5impls74_$LT$im
       127: 0000000000013370   103 FUNC    LOCAL  DEFAULT   14 _ZN3std2io5impls74_$LT$im
       128: 0000000000000000    24 TLS     LOCAL  DEFAULT   20 _ZN3std2io5stdio14OUTPUT_
       129: 0000000000041210     1 OBJECT  LOCAL  DEFAULT   27 _ZN3std2io5stdio19OUTPUT_
       130: 0000000000019040    12 FUNC    LOCAL  DEFAULT   14 _ZN3std3sys4unix14abort_i
       131: 0000000000018bf0   470 FUNC    LOCAL  DEFAULT   14 _ZN3std3sys4unix14stack_o
       132: 00000000000411d0     8 OBJECT  LOCAL  DEFAULT   27 _ZN3std3sys4unix14stack_o
       133: 0000000000041211     1 OBJECT  LOCAL  DEFAULT   27 _ZN3std3sys4unix14stack_o
       134: 0000000000018970   636 FUNC    LOCAL  DEFAULT   14 _ZN3std3sys4unix14stack_o
       135: 0000000000018140   363 FUNC    LOCAL  DEFAULT   14 _ZN3std3sys4unix2fs4File6
       136: 0000000000041212     1 OBJECT  LOCAL  DEFAULT   27 _ZN3std3sys4unix2fs9try_s
       137: 0000000000019050   728 FUNC    LOCAL  DEFAULT   14 _ZN3std3sys4unix2fs9try_s
       138: 0000000000041038    24 OBJECT  LOCAL  DEFAULT   26 _ZN3std3sys4unix2fs9try_s
       139: 00000000000185b0   310 FUNC    LOCAL  DEFAULT   14 _ZN3std3sys4unix2os12erro
       140: 00000000000186f0   630 FUNC    LOCAL  DEFAULT   14 _ZN3std3sys4unix2os6geten
       141: 0000000000041188    72 OBJECT  LOCAL  DEFAULT   27 _ZN3std3sys4unix2os8ENV_L
       142: 0000000000018100    55 FUNC    LOCAL  DEFAULT   14 _ZN3std3sys4unix4args3imp
       143: 000000000003e8b0     8 OBJECT  LOCAL  DEFAULT   21 _ZN3std3sys4unix4args3imp
       144: 0000000000041150     8 OBJECT  LOCAL  DEFAULT   27 _ZN3std3sys4unix4args3imp
       145: 0000000000041158     8 OBJECT  LOCAL  DEFAULT   27 _ZN3std3sys4unix4args3imp
       146: 0000000000041160    40 OBJECT  LOCAL  DEFAULT   27 _ZN3std3sys4unix4args3imp
       147: 00000000000068a0   104 FUNC    LOCAL  DEFAULT   14 _ZN3std3sys4unix4weak13We
       148: 00000000000411d8     8 OBJECT  LOCAL  DEFAULT   27 _ZN3std3sys4unix6thread5g
       149: 0000000000014190   646 FUNC    LOCAL  DEFAULT   14 _ZN3std4path10Components2
       150: 0000000000014c90   547 FUNC    LOCAL  DEFAULT   14 _ZN3std4sync4once4Once9ca
       151: 0000000000016290    92 FUNC    LOCAL  DEFAULT   14 _ZN3std5alloc24default_al
       152: 00000000000410e8     8 OBJECT  LOCAL  DEFAULT   27 _ZN3std5alloc4HOOK17h01f9
       153: 0000000000012650    39 FUNC    LOCAL  DEFAULT   14 _ZN3std6thread5local4fast
       154: 0000000000012680   172 FUNC    LOCAL  DEFAULT   14 _ZN3std6thread5local4fast
       155: 0000000000012730   183 FUNC    LOCAL  DEFAULT   14 _ZN3std6thread5local4fast
       156: 00000000000127f0    42 FUNC    LOCAL  DEFAULT   14 _ZN3std6thread5local4fast
       157: 0000000000012820    47 FUNC    LOCAL  DEFAULT   14 _ZN3std6thread5local4fast
       158: 0000000000041058    40 OBJECT  LOCAL  DEFAULT   27 _ZN3std6thread8ThreadId3n
       159: 0000000000041010     8 OBJECT  LOCAL  DEFAULT   26 _ZN3std6thread8ThreadId3n
       160: 0000000000006870    46 FUNC    LOCAL  DEFAULT   14 _ZN3std9panicking11begin_
       161: 0000000000017120    38 FUNC    LOCAL  DEFAULT   14 _ZN3std9panicking11begin_
       162: 0000000000000060    24 TLS     LOCAL  DEFAULT   20 _ZN3std9panicking11panic_
       163: 0000000000016540  1583 FUNC    LOCAL  DEFAULT   14 _ZN3std9panicking12defaul
       164: 0000000000041028     1 OBJECT  LOCAL  DEFAULT   26 _ZN3std9panicking12defaul
       165: 0000000000016b70   673 FUNC    LOCAL  DEFAULT   14 _ZN3std9panicking12defaul
       166: 0000000000016e70   174 FUNC    LOCAL  DEFAULT   14 _ZN3std9panicking19begin_
       167: 0000000000041138    16 OBJECT  LOCAL  DEFAULT   27 _ZN3std9panicking4HOOK17h
       168: 00000000000410f0    72 OBJECT  LOCAL  DEFAULT   27 _ZN3std9panicking9HOOK_LO
       169: 00000000000077b0   130 FUNC    LOCAL  DEFAULT   14 _ZN42_$LT$$RF$T$u20$as$u2
       170: 0000000000007840    86 FUNC    LOCAL  DEFAULT   14 _ZN42_$LT$$RF$T$u20$as$u2
       171: 00000000000078a0    86 FUNC    LOCAL  DEFAULT   14 _ZN42_$LT$$RF$T$u20$as$u2
       172: 0000000000007900    19 FUNC    LOCAL  DEFAULT   14 _ZN42_$LT$$RF$T$u20$as$u2
       173: 0000000000007920    86 FUNC    LOCAL  DEFAULT   14 _ZN42_$LT$$RF$T$u20$as$u2
       174: 0000000000007980     9 FUNC    LOCAL  DEFAULT   14 _ZN44_$LT$$RF$T$u20$as$u2
       175: 0000000000007990    19 FUNC    LOCAL  DEFAULT   14 _ZN44_$LT$$RF$T$u20$as$u2
       176: 00000000000079b0     9 FUNC    LOCAL  DEFAULT   14 _ZN45_$LT$$RF$T$u20$as$u2
       177: 00000000000079c0   264 FUNC    LOCAL  DEFAULT   14 _ZN4core3fmt5Write10write
       178: 0000000000007ad0   216 FUNC    LOCAL  DEFAULT   14 _ZN4core3fmt5Write10write
       179: 0000000000007bb0    63 FUNC    LOCAL  DEFAULT   14 _ZN4core3fmt5Write9write_
       180: 0000000000007bf0    63 FUNC    LOCAL  DEFAULT   14 _ZN4core3fmt5Write9write_
       181: 0000000000007c30   112 FUNC    LOCAL  DEFAULT   14 _ZN4core3ops8function6FnO
       182: 0000000000007ca0     5 FUNC    LOCAL  DEFAULT   14 _ZN4core3ops8function6FnO
       183: 0000000000007cb0     5 FUNC    LOCAL  DEFAULT   14 _ZN4core3ops8function6FnO
       184: 0000000000007cc0    21 FUNC    LOCAL  DEFAULT   14 _ZN4core3ops8function6FnO
       185: 0000000000007ce0     1 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr100drop_in_pl
       186: 0000000000007cf0    19 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr101drop_in_pl
       187: 0000000000007d10    22 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr109drop_in_pl
       188: 0000000000007d30    34 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr111drop_in_pl
       189: 0000000000007d60     5 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr115drop_in_pl
       190: 0000000000007d70   100 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr123drop_in_pl
       191: 0000000000007de0    39 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr125drop_in_pl
       192: 0000000000007e10    93 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr125drop_in_pl
       193: 0000000000007e70    85 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr131drop_in_pl
       194: 0000000000007ed0    40 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr137drop_in_pl
       195: 0000000000007f00   192 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr146drop_in_pl
       196: 0000000000007fc0    30 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr147drop_in_pl
       197: 0000000000007fe0   160 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr153drop_in_pl
       198: 0000000000008080    42 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr154drop_in_pl
       199: 00000000000080b0    38 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr158drop_in_pl
       200: 00000000000080e0    35 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr164drop_in_pl
       201: 0000000000008110    42 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr169drop_in_pl
       202: 0000000000008140   218 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr170drop_in_pl
       203: 0000000000008220   215 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr174drop_in_pl
       204: 0000000000008300    15 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr181drop_in_pl
       205: 0000000000008310    32 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr226drop_in_pl
       206: 0000000000008330    71 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr246drop_in_pl
       207: 0000000000008380    33 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr264drop_in_pl
       208: 00000000000083b0   185 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr269drop_in_pl
       209: 0000000000008470     5 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr275drop_in_pl
       210: 0000000000008480     6 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr34drop_in_pla
       211: 0000000000008490    19 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr40drop_in_pla
       212: 00000000000084b0   117 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr42drop_in_pla
       213: 0000000000008530    33 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr44drop_in_pla
       214: 0000000000008560    36 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr44drop_in_pla
       215: 0000000000008590    24 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr44drop_in_pla
       216: 00000000000085b0    30 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr45drop_in_pla
       217: 00000000000085d0    33 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr46drop_in_pla
       218: 0000000000008600    59 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr46drop_in_pla
       219: 0000000000008640     6 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr49drop_in_pla
       220: 0000000000008650    39 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr50drop_in_pla
       221: 0000000000008680    42 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr52drop_in_pla
       222: 00000000000086b0   447 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr55drop_in_pla
       223: 0000000000008870     9 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr61drop_in_pla
       224: 0000000000008880    35 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr64drop_in_pla
       225: 00000000000088b0     9 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr64drop_in_pla
       226: 00000000000088c0   151 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr65drop_in_pla
       227: 0000000000008960    70 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr65drop_in_pla
       228: 00000000000089b0   286 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr65drop_in_pla
       229: 0000000000008ad0   146 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr67drop_in_pla
       230: 0000000000008b70    24 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr68drop_in_pla
       231: 0000000000008b90     6 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr68drop_in_pla
       232: 0000000000008ba0    43 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr69drop_in_pla
       233: 0000000000008bd0   151 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr70drop_in_pla
       234: 0000000000008c70    33 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr70drop_in_pla
       235: 0000000000008ca0    35 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr73drop_in_pla
       236: 0000000000008cd0    35 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr73drop_in_pla
       237: 0000000000008d00    38 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr78drop_in_pla
       238: 0000000000008d30     9 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr81drop_in_pla
       239: 0000000000008d40    21 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr83drop_in_pla
       240: 0000000000008d60    24 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr84drop_in_pla
       241: 0000000000008d80   240 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr86drop_in_pla
       242: 0000000000008e70   118 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr87drop_in_pla
       243: 0000000000008ef0    32 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr88drop_in_pla
       244: 0000000000008f10    26 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr89drop_in_pla
       245: 0000000000008f30   158 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr91drop_in_pla
       246: 0000000000008fd0  1281 FUNC    LOCAL  DEFAULT   14 _ZN4core3str21_$LT$impl$u
       247: 0000000000005070   534 FUNC    LOCAL  DEFAULT   14 _ZN4core5slice4sort14brea
       248: 0000000000005290   704 FUNC    LOCAL  DEFAULT   14 _ZN4core5slice4sort22part
       249: 00000000000094e0  3364 FUNC    LOCAL  DEFAULT   14 _ZN4core5slice4sort7recur
       250: 0000000000005550   607 FUNC    LOCAL  DEFAULT   14 _ZN4core5slice4sort8heaps
       251: 000000000000a210    40 FUNC    LOCAL  DEFAULT   14 _ZN4core6option15Option$L
       252: 000000000000a240    36 FUNC    LOCAL  DEFAULT   14 _ZN4core6option15Option$L
       253: 00000000000057b0    77 FUNC    LOCAL  DEFAULT   14 _ZN4core9panicking13asser
       254: 0000000000005800    79 FUNC    LOCAL  DEFAULT   14 _ZN4core9panicking13asser
       255: 000000000000a270   107 FUNC    LOCAL  DEFAULT   14 _ZN50_$LT$$BP$mut$u20$T$u
       256: 000000000000a2e0   301 FUNC    LOCAL  DEFAULT   14 _ZN50_$LT$$RF$mut$u20$W$u
       257: 000000000000a410   276 FUNC    LOCAL  DEFAULT   14 _ZN50_$LT$$RF$mut$u20$W$u
       258: 000000000000a530   219 FUNC    LOCAL  DEFAULT   14 _ZN50_$LT$$RF$mut$u20$W$u
       259: 000000000000a610    66 FUNC    LOCAL  DEFAULT   14 _ZN50_$LT$$RF$mut$u20$W$u
       260: 000000000000a660    66 FUNC    LOCAL  DEFAULT   14 _ZN50_$LT$$RF$mut$u20$W$u
       261: 000000000000a6b0    66 FUNC    LOCAL  DEFAULT   14 _ZN50_$LT$$RF$mut$u20$W$u
       262: 000000000000a700     8 FUNC    LOCAL  DEFAULT   14 _ZN50_$LT$$RF$mut$u20$W$u
       263: 000000000000a710   103 FUNC    LOCAL  DEFAULT   14 _ZN50_$LT$$RF$mut$u20$W$u
       264: 000000000000a780   100 FUNC    LOCAL  DEFAULT   14 _ZN50_$LT$$RF$mut$u20$W$u
       265: 000000000000a7f0    76 FUNC    LOCAL  DEFAULT   14 _ZN5alloc4sync12Arc$LT$T$
       266: 000000000000a840    99 FUNC    LOCAL  DEFAULT   14 _ZN5alloc4sync12Arc$LT$T$
       267: 000000000000a8b0    23 FUNC    LOCAL  DEFAULT   14 _ZN5alloc5alloc8box_free1
       268: 000000000000a8d0    16 FUNC    LOCAL  DEFAULT   14 _ZN5alloc5alloc8box_free1
       269: 000000000000a8e0   139 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec11finish
       270: 0000000000005850   185 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       271: 0000000000005910   185 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       272: 00000000000059d0   205 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       273: 0000000000005aa0   205 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       274: 0000000000005b70   185 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       275: 0000000000005c30   201 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       276: 0000000000005d00   205 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       277: 0000000000005dd0   150 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       278: 0000000000005e70   211 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       279: 0000000000005f50   205 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       280: 0000000000006020   204 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       281: 00000000000060f0   185 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       282: 00000000000061b0   182 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       283: 000000000000a970   964 FUNC    LOCAL  DEFAULT   14 _ZN5gimli4read4line15File
       284: 000000000000ad40  2516 FUNC    LOCAL  DEFAULT   14 _ZN5gimli4read4line15pars
       285: 000000000000b720   501 FUNC    LOCAL  DEFAULT   14 _ZN5gimli4read4line27File
       286: 000000000000b920  4718 FUNC    LOCAL  DEFAULT   14 _ZN5gimli4read4unit15pars
       287: 000000000000cb90  2069 FUNC    LOCAL  DEFAULT   14 _ZN5gimli4read4unit18Attr
       288: 000000000000d3b0   567 FUNC    LOCAL  DEFAULT   14 _ZN5gimli4read5dwarf14Dwa
       289: 000000000000d5f0   378 FUNC    LOCAL  DEFAULT   14 _ZN5gimli4read6reader6Rea
       290: 000000000000d770  2709 FUNC    LOCAL  DEFAULT   14 _ZN5gimli4read8rnglists20
       291: 000000000000e210    19 FUNC    LOCAL  DEFAULT   14 _ZN60_$LT$alloc..string..
       292: 0000000000018040   187 FUNC    LOCAL  DEFAULT   14 _ZN61_$LT$std..path..Comp
       293: 0000000000018e90     3 FUNC    LOCAL  DEFAULT   14 _ZN64_$LT$std..sys..unix.
       294: 0000000000013c40   100 FUNC    LOCAL  DEFAULT   14 _ZN80_$LT$std..io..Write.
       295: 0000000000013cb0   403 FUNC    LOCAL  DEFAULT   14 _ZN80_$LT$std..io..Write.
       296: 000000000000e230   774 FUNC    LOCAL  DEFAULT   14 _ZN90_$LT$gimli..read..un
       297: 00000000000171b0    30 FUNC    LOCAL  DEFAULT   14 _ZN91_$LT$std..panicking.
       298: 0000000000017150    95 FUNC    LOCAL  DEFAULT   14 _ZN91_$LT$std..panicking.
       299: 000000000000e540   632 FUNC    LOCAL  DEFAULT   14 _ZN94_$LT$alloc..collecti
       300: 000000000000e7c0  9392 FUNC    LOCAL  DEFAULT   14 _ZN9addr2line16ResUnit$LT
       301: 0000000000010c70   972 FUNC    LOCAL  DEFAULT   14 _ZN9addr2line16ResUnit$LT
       302: 0000000000011040   353 FUNC    LOCAL  DEFAULT   14 _ZN9addr2line16ResUnit$LT
       303: 00000000000111b0  3988 FUNC    LOCAL  DEFAULT   14 _ZN9addr2line17Function$L
       304: 0000000000012150  1216 FUNC    LOCAL  DEFAULT   14 _ZN9addr2line9name_attr17
       305: 0000000000041030     8 OBJECT  LOCAL  DEFAULT   26 _rust_extern_with_linkage
       306: 00000000000341a0    25 OBJECT  LOCAL  DEFAULT   16 str.5
       307: 00000000000341c0    57 OBJECT  LOCAL  DEFAULT   16 str.6
       308: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS addr2line.c1wbpybl-cgu.0
       309: 0000000000026570   139 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec11finish
       310: 0000000000006910   150 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       311: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS gimli.6pztyi9p-cgu.0
       312: 000000000003d2ac     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table56
       313: 000000000003d304     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table57
       314: 000000000003d310     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table59
       315: 0000000000026720    86 FUNC    LOCAL  DEFAULT   14 _ZN42_$LT$$RF$T$u20$as$u2
       316: 0000000000026780     1 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr112drop_in_pl
       317: 0000000000026790    19 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr134drop_in_pl
       318: 00000000000267b0    19 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr138drop_in_pl
       319: 00000000000267d0    42 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr52drop_in_pla
       320: 0000000000026800    43 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr54drop_in_pla
       321: 0000000000026830    43 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr68drop_in_pla
       322: 0000000000026860    35 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr87drop_in_pla
       323: 00000000000069b0    96 FUNC    LOCAL  DEFAULT   14 _ZN4core9panicking13asser
       324: 0000000000026890   139 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec11finish
       325: 0000000000006a10   201 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       326: 0000000000006ae0   185 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       327: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS alloc.bdtv0pny-cgu.0
       328: 000000000003d320     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table31
       329: 000000000002d9c0    32 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr42drop_in_pla
       330: 000000000002da60   139 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec11finish
       331: 0000000000006bb0   150 FUNC    LOCAL  DEFAULT   14 _ZN5alloc7raw_vec19RawVec
       332: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS core.2eb9xv2h-cgu.0
       333: 000000000002dfd0    11 FUNC    LOCAL  DEFAULT   14 _ZN36_$LT$T$u20$as$u20$co
       334: 0000000000032150   152 FUNC    LOCAL  DEFAULT   14 _ZN42_$LT$$RF$T$u20$as$u2
       335: 00000000000321f0    16 FUNC    LOCAL  DEFAULT   14 _ZN42_$LT$$RF$T$u20$as$u2
       336: 0000000000032200     8 FUNC    LOCAL  DEFAULT   14 _ZN42_$LT$$RF$T$u20$as$u2
       337: 0000000000032210   376 FUNC    LOCAL  DEFAULT   14 _ZN42_$LT$$RF$T$u20$as$u2
       338: 0000000000032390   249 FUNC    LOCAL  DEFAULT   14 _ZN42_$LT$$RF$T$u20$as$u2
       339: 0000000000032490    19 FUNC    LOCAL  DEFAULT   14 _ZN44_$LT$$RF$T$u20$as$u2
       340: 0000000000031af0   555 FUNC    LOCAL  DEFAULT   14 _ZN4core3fmt3num52_$LT$im
       341: 000000000002eb50   220 FUNC    LOCAL  DEFAULT   14 _ZN4core3fmt5Write10write
       342: 000000000002ec30    63 FUNC    LOCAL  DEFAULT   14 _ZN4core3fmt5Write9write_
       343: 000000000002e9f0   282 FUNC    LOCAL  DEFAULT   14 _ZN4core3fmt8builders10De
       344: 000000000002f590    79 FUNC    LOCAL  DEFAULT   14 _ZN4core3fmt9Formatter12p
       345: 000000000002dde0   358 FUNC    LOCAL  DEFAULT   14 _ZN4core3num14from_str_ra
       346: 000000000002ddb0    18 FUNC    LOCAL  DEFAULT   14 _ZN4core3ops8function6FnO
       347: 000000000002ddd0     1 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr102drop_in_pl
       348: 0000000000036cac   256 OBJECT  LOCAL  DEFAULT   16 _ZN4core3str11validations
       349: 00000000000367b0    16 OBJECT  LOCAL  DEFAULT   16 _ZN4core7unicode12unicode
       350: 0000000000037450   124 OBJECT  LOCAL  DEFAULT   16 _ZN4core7unicode12unicode
       351: 00000000000374cc   689 OBJECT  LOCAL  DEFAULT   16 _ZN4core7unicode12unicode
       352: 000000000002ec80   223 FUNC    LOCAL  DEFAULT   14 _ZN50_$LT$$RF$mut$u20$W$u
       353: 000000000002ed60    66 FUNC    LOCAL  DEFAULT   14 _ZN50_$LT$$RF$mut$u20$W$u
       354: 000000000002ec70     9 FUNC    LOCAL  DEFAULT   14 _ZN50_$LT$$RF$mut$u20$W$u
       355: 000000000002df50   128 FUNC    LOCAL  DEFAULT   14 _ZN71_$LT$core..ops..rang
       356: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS crtstuff.c
       357: 00000000000074c0     0 FUNC    LOCAL  DEFAULT   14 deregister_tm_clones
       358: 00000000000074f0     0 FUNC    LOCAL  DEFAULT   14 register_tm_clones
       359: 0000000000007530     0 FUNC    LOCAL  DEFAULT   14 __do_global_dtors_aux
       360: 0000000000041050     1 OBJECT  LOCAL  DEFAULT   27 completed.8060
       361: 000000000003e8c0     0 OBJECT  LOCAL  DEFAULT   22 __do_global_dtors_aux_fin
       362: 0000000000007570     0 FUNC    LOCAL  DEFAULT   14 frame_dummy
       363: 000000000003e8b8     0 OBJECT  LOCAL  DEFAULT   21 __frame_dummy_init_array_
       364: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.7rcbfp3g-cgu.0
       365: 0000000000007580     1 FUNC    LOCAL  DEFAULT   14 _ZN3sum4main17h5c177a5c7e
       366: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.7rcbfp3g-cgu.1
       367: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.7rcbfp3g-cgu.2
       368: 0000000000007620    29 FUNC    LOCAL  DEFAULT   14 _ZN68_$LT$std..process..E
       369: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.7rcbfp3g-cgu.3
       370: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.7rcbfp3g-cgu.4
       371: 000000000003cb98     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table1
       372: 0000000000007670    68 FUNC    LOCAL  DEFAULT   14 _ZN4core3ops8function6FnO
       373: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.7rcbfp3g-cgu.5
       374: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.7rcbfp3g-cgu.6
       375: 000000000003cba4     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table0
       376: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS t77eubk5xk9tcs0
       377: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS panic_unwind.b34o5za4-cgu
       378: 000000000003d2a0     0 NOTYPE  LOCAL  DEFAULT   19 GCC_except_table2
       379: 0000000000022c20   381 FUNC    LOCAL  DEFAULT   14 _ZN12panic_unwind5dwarf2e
       380: 0000000000022e90    12 FUNC    LOCAL  DEFAULT   14 _ZN12panic_unwind8real_im
       381: 0000000000022ea0    12 FUNC    LOCAL  DEFAULT   14 _ZN12panic_unwind8real_im
       382: 0000000000022e70    24 FUNC    LOCAL  DEFAULT   14 _ZN12panic_unwind8real_im
       383: 0000000000022b50    12 FUNC    LOCAL  DEFAULT   14 _ZN4core3ops8function6FnO
       384: 0000000000022b60    12 FUNC    LOCAL  DEFAULT   14 _ZN4core3ops8function6FnO
       385: 0000000000022b70   106 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr79drop_in_pla
       386: 0000000000022be0     1 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr88drop_in_pla
       387: 0000000000022bf0    23 FUNC    LOCAL  DEFAULT   14 _ZN5alloc5alloc8box_free1
       388: 0000000000022c10    16 FUNC    LOCAL  DEFAULT   14 _ZN5alloc5alloc8box_free1
       389: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS miniz_oxide.9nze787t-cgu.
       390: 0000000000023b20   503 FUNC    LOCAL  DEFAULT   14 _ZN11miniz_oxide7inflate4
       391: 0000000000023840   721 FUNC    LOCAL  DEFAULT   14 _ZN11miniz_oxide7inflate4
       392: 00000000000231c0  1662 FUNC    LOCAL  DEFAULT   14 _ZN11miniz_oxide7inflate4
       393: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS adler.72iv9051-cgu.0
       394: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS object.1n0j33gf-cgu.0
       395: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS rustc_demangle.axzg541g-c
       396: 000000000002a190   423 FUNC    LOCAL  DEFAULT   14 _ZN14rustc_demangle2v06Pa
       397: 0000000000029410   529 FUNC    LOCAL  DEFAULT   14 _ZN14rustc_demangle2v06Pa
       398: 0000000000029630  1509 FUNC    LOCAL  DEFAULT   14 _ZN14rustc_demangle2v06Pa
       399: 0000000000029c20  1383 FUNC    LOCAL  DEFAULT   14 _ZN14rustc_demangle2v06Pa
       400: 000000000002a410  2177 FUNC    LOCAL  DEFAULT   14 _ZN14rustc_demangle2v07Pr
       401: 000000000002adc0  3125 FUNC    LOCAL  DEFAULT   14 _ZN14rustc_demangle2v07Pr
       402: 000000000002ba00  1161 FUNC    LOCAL  DEFAULT   14 _ZN14rustc_demangle2v07Pr
       403: 000000000002c230  1712 FUNC    LOCAL  DEFAULT   14 _ZN14rustc_demangle2v07Pr
       404: 000000000002c0c0   356 FUNC    LOCAL  DEFAULT   14 _ZN14rustc_demangle2v07Pr
       405: 000000000002c8e0   667 FUNC    LOCAL  DEFAULT   14 _ZN14rustc_demangle2v07Pr
       406: 000000000002aca0   284 FUNC    LOCAL  DEFAULT   14 _ZN14rustc_demangle2v07Pr
       407: 000000000002a340   208 FUNC    LOCAL  DEFAULT   14 _ZN14rustc_demangle2v07Pr
       408: 000000000002be90   545 FUNC    LOCAL  DEFAULT   14 _ZN14rustc_demangle2v07Pr
       409: 0000000000028140     1 FUNC    LOCAL  DEFAULT   14 _ZN4core3ptr33drop_in_pla
       410: 0000000000028150   547 FUNC    LOCAL  DEFAULT   14 _ZN81_$LT$core..str..patt
       411: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS compiler_builtins.84hxjow
       412: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS compiler_builtins.84hxjow
       413: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS crtstuff.c
       414: 000000000003cb94     0 OBJECT  LOCAL  DEFAULT   18 __FRAME_END__
       415: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS 
       416: 0000000000016420   120 FUNC    LOCAL  DEFAULT   14 __rdl_alloc_zeroed
       417: 0000000000016320    75 FUNC    LOCAL  DEFAULT   14 __rdl_alloc
       418: 0000000000007640     4 FUNC    LOCAL  DEFAULT   14 _ZN3std3sys4unix7process1
       419: 00000000000075b0    48 FUNC    LOCAL  DEFAULT   14 _ZN3std2rt10lang_start17h
       420: 00000000000076e0     6 FUNC    LOCAL  DEFAULT   14 _ZN4core4hint9black_box17
       421: 0000000000016370     6 FUNC    LOCAL  DEFAULT   14 __rdl_dealloc
       422: 0000000000016380   150 FUNC    LOCAL  DEFAULT   14 __rdl_realloc
       423: 000000000003e8c0     0 NOTYPE  LOCAL  DEFAULT   21 __init_array_end
       424: 00000000000076c0     8 FUNC    LOCAL  DEFAULT   14 _ZN4core3ops8function6FnO
       425: 00000000000075e0    27 FUNC    LOCAL  DEFAULT   14 _ZN3std2rt10lang_start28_
       426: 000000000002d9e0    12 FUNC    LOCAL  DEFAULT   14 __rg_oom
       427: 00000000000076f0    51 FUNC    LOCAL  DEFAULT   14 _ZN3std10sys_common9backt
       428: 00000000000407d8     0 OBJECT  LOCAL  DEFAULT   24 _DYNAMIC
       429: 000000000003e8b0     0 NOTYPE  LOCAL  DEFAULT   21 __init_array_start
       430: 0000000000007600    21 FUNC    LOCAL  DEFAULT   14 _ZN54_$LT$$LP$$RP$$u20$as
       431: 0000000000037780     0 NOTYPE  LOCAL  DEFAULT   17 __GNU_EH_FRAME_HDR
       432: 0000000000040a08     0 OBJECT  LOCAL  DEFAULT   25 _GLOBAL_OFFSET_TABLE_
       433: 0000000000005000     0 FUNC    LOCAL  DEFAULT   11 _init
       434: 00000000000328f0     5 FUNC    GLOBAL DEFAULT   14 __libc_csu_fini
       435: 0000000000028110    47 FUNC    GLOBAL DEFAULT   14 _ZN5gimli4read4unit20allo
       436: 0000000000031350   654 FUNC    GLOBAL DEFAULT   14 _ZN4core7unicode9printabl
       437: 00000000000317d0   146 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num52_$LT$im
       438: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND getenv@@GLIBC_2.2.5
       439: 00000000000182b0   768 FUNC    GLOBAL DEFAULT   14 _ZN3std3sys4unix2fs8readl
       440: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND dl_iterate_phdr@@GLIBC_2.
       441: 0000000000006280  1189 FUNC    GLOBAL DEFAULT   14 _ZN3std4sync4once4Once10c
       442: 0000000000018eb0   317 FUNC    GLOBAL DEFAULT   14 _ZN3std3sys4unix17thread_
       443: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND free@@GLIBC_2.2.5
       444: 0000000000026a60  5143 FUNC    GLOBAL DEFAULT   14 _ZN5gimli4read6abbrev13Ab
       445: 0000000000031730   146 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num52_$LT$im
       446: 0000000000006730    90 FUNC    GLOBAL DEFAULT   14 _ZN3std9panicking11panic_
       447: 0000000000031870   146 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num53_$LT$im
       448: 0000000000017390   112 FUNC    GLOBAL DEFAULT   14 rust_panic
       449: 0000000000015740   904 FUNC    GLOBAL DEFAULT   14 _ZN73_$LT$std..sys_common
       450: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND abort@@GLIBC_2.2.5
       451: 0000000000031a50   149 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num55_$LT$im
       452: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_Backtrace@@GCC_3.
       453: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND __errno_location@@GLIBC_2
       454: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_getattr_np@@GLIBC
       455: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND _ITM_deregisterTMCloneTab
       456: 0000000000012610    51 FUNC    GLOBAL DEFAULT   14 _ZN68_$LT$std..thread..lo
       457: 0000000000031d20   141 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num3imp51_$L
       458: 000000000002edc0    54 FUNC    GLOBAL DEFAULT   14 _ZN59_$LT$core..fmt..Argu
       459: 00000000000280e0    42 FUNC    GLOBAL DEFAULT   14 _ZN5gimli4read4line7LineR
       460: 000000000002fdd0    18 FUNC    GLOBAL DEFAULT   14 _ZN42_$LT$str$u20$as$u20$
       461: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND writev@@GLIBC_2.2.5
       462: 0000000000014fc0   525 FUNC    GLOBAL DEFAULT   14 _ZN91_$LT$std..sys_common
       463: 0000000000031a50   149 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num53_$LT$im
       464: 0000000000031db0   311 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num3imp52_$L
       465: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND sigaction@@GLIBC_2.2.5
       466: 00000000000319b0   149 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num53_$LT$im
       467: 00000000000164a0    67 FUNC    GLOBAL DEFAULT   14 __rust_drop_panic
       468: 00000000000231a0    22 FUNC    GLOBAL DEFAULT   14 _ZN11miniz_oxide7inflate4
       469: 00000000000316a0   136 FUNC    GLOBAL DEFAULT   14 _ZN4core3num62_$LT$impl$u
       470: 0000000000030130   291 FUNC    GLOBAL DEFAULT   14 _ZN4core5slice6memchr19me
       471: 000000000002fd00     9 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt9Formatter15d
       472: 000000000002e0d0     8 FUNC    GLOBAL DEFAULT   14 _ZN4core5panic9PanicInfo7
       473: 0000000000000000     0 FUNC    WEAK   DEFAULT  UND __cxa_thread_atexit_impl@
       474: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND __xpg_strerror_r@@GLIBC_2
       475: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND readlink@@GLIBC_2.2.5
       476: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetRegionStart@@G
       477: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND write@@GLIBC_2.2.5
       478: 00000000000149e0   685 FUNC    GLOBAL DEFAULT   14 _ZN3std4path4Path13_strip
       479: 000000000002dd90    18 FUNC    GLOBAL DEFAULT   14 _ZN5alloc6string104_$LT$i
       480: 0000000000031a50   149 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num55_$LT$im
       481: 000000000002f5e0  1712 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt9Formatter3pa
       482: 00000000000317d0   146 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num52_$LT$im
       483: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetTextRelBase@@G
       484: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_RaiseException@@G
       485: 0000000000041050     0 NOTYPE  GLOBAL DEFAULT   26 _edata
       486: 000000000002edb0    11 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt10ArgumentV11
       487: 00000000000325b0   293 FUNC    GLOBAL DEFAULT   14 _ZN4core7unicode12unicode
       488: 0000000000041008     8 OBJECT  WEAK   HIDDEN    26 DW.ref.rust_eh_personalit
       489: 0000000000028380  2955 FUNC    GLOBAL DEFAULT   14 _ZN71_$LT$rustc_demangle.
       490: 0000000000041148     8 OBJECT  GLOBAL DEFAULT   27 _ZN3std9panicking11panic_
       491: 0000000000006c50   101 FUNC    GLOBAL DEFAULT   14 _ZN4core6option13expect_f
       492: 000000000002e020   162 FUNC    GLOBAL DEFAULT   14 _ZN84_$LT$core..char..Esc
       493: 0000000000006d90    51 FUNC    GLOBAL DEFAULT   14 _ZN4core9panicking9panic_
       494: 000000000002d910     9 FUNC    GLOBAL DEFAULT   14 _ZN14rustc_demangle8Deman
       495: 0000000000032914     0 FUNC    GLOBAL HIDDEN    15 _fini
       496: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND strlen@@GLIBC_2.2.5
       497: 000000000002eb10    14 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt8builders9Deb
       498: 0000000000012eb0   682 FUNC    GLOBAL DEFAULT   14 _ZN60_$LT$std..io..error.
       499: 0000000000006d10   116 FUNC    GLOBAL DEFAULT   14 _ZN4core9panicking18panic
       500: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND mmap@@GLIBC_2.2.5
       501: 00000000000315e0   174 FUNC    GLOBAL DEFAULT   14 _ZN68_$LT$core..num..erro
       502: 0000000000032900    19 FUNC    GLOBAL HIDDEN    14 fstat64
       503: 0000000000007730     5 FUNC    GLOBAL DEFAULT   14 __rust_alloc
       504: 000000000002db10   633 FUNC    GLOBAL DEFAULT   14 _ZN5alloc6string6String15
       505: 00000000000324b0   220 FUNC    GLOBAL DEFAULT   14 _ZN64_$LT$core..str..erro
       506: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_setspecific@@GLIB
       507: 000000000002d920   153 FUNC    GLOBAL DEFAULT   14 _ZN63_$LT$rustc_demangle.
       508: 0000000000031730   146 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num52_$LT$im
       509: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_mutex_destroy@@GL
       510: 0000000000006830    61 FUNC    GLOBAL DEFAULT   14 _ZN3std9panicking15begin_
       511: 000000000002cb80  3375 FUNC    GLOBAL DEFAULT   14 _ZN14rustc_demangle8deman
       512: 0000000000017400  1168 FUNC    GLOBAL DEFAULT   14 _ZN3std2rt19lang_start_in
       513: 0000000000006f60   116 FUNC    GLOBAL DEFAULT   14 _ZN4core5slice5index22sli
       514: 0000000000016e20    75 FUNC    GLOBAL DEFAULT   14 rust_begin_unwind
       515: 00000000000260c0  1118 FUNC    GLOBAL DEFAULT   14 _ZN5adler7Adler3211write_
       516: 0000000000032020   293 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num3imp54_$L
       517: 0000000000022eb0   737 FUNC    GLOBAL DEFAULT   14 rust_eh_personality
       518: 0000000000006e60   116 FUNC    GLOBAL DEFAULT   14 _ZN4core5slice5index26sli
       519: 0000000000013e50   832 FUNC    GLOBAL DEFAULT   14 _ZN3std4path10Components7
       520: 0000000000027e80   132 FUNC    GLOBAL DEFAULT   14 _ZN5gimli4read6abbrev12Ab
       521: 0000000000022df0   128 FUNC    GLOBAL DEFAULT   14 __rust_start_panic
       522: 0000000000007740     5 FUNC    GLOBAL DEFAULT   14 __rust_dealloc
       523: 000000000002e0f0     5 FUNC    GLOBAL DEFAULT   14 _ZN4core5panic9PanicInfo8
       524: 000000000002e620   422 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt8builders11De
       525: 0000000000007760     5 FUNC    GLOBAL DEFAULT   14 __rust_alloc_zeroed
       526: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND memset@@GLIBC_2.2.5
       527: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND getcwd@@GLIBC_2.2.5
       528: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetIPInfo@@GCC_4.
       529: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND close@@GLIBC_2.2.5
       530: 0000000000031910   146 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num53_$LT$im
       531: 000000000002ee00   613 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt5write17h7aa6
       532: 0000000000015f80   225 FUNC    GLOBAL DEFAULT   14 _ZN3std10sys_common16thre
       533: 00000000000171d0   445 FUNC    GLOBAL DEFAULT   14 _ZN3std9panicking20rust_p
       534: 0000000000012d00   423 FUNC    GLOBAL DEFAULT   14 _ZN3std2fs11OpenOptions5_
       535: 000000000002d9f0   107 FUNC    GLOBAL DEFAULT   14 _ZN5alloc11collections5bt
       536: 0000000000006ee0   116 FUNC    GLOBAL DEFAULT   14 _ZN4core5slice5index24sli
       537: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_attr_getstack@@GL
       538: 0000000000027f30   356 FUNC    GLOBAL DEFAULT   14 _ZN5gimli4read6abbrev10At
       539: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetLanguageSpecif
       540: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND memchr@@GLIBC_2.2.5
       541: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND __libc_start_main@@GLIBC_
       542: 0000000000006270    11 FUNC    GLOBAL DEFAULT   14 _ZN3std7process5abort17h9
       543: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND __tls_get_addr@@GLIBC_2.3
       544: 0000000000016f20   251 FUNC    GLOBAL DEFAULT   14 _ZN90_$LT$std..panicking.
       545: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_rwlock_rdlock@@GL
       546: 00000000000319b0   149 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num53_$LT$im
       547: 0000000000026920   269 FUNC    GLOBAL DEFAULT   14 _ZN5gimli6common9SectionI
       548: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND calloc@@GLIBC_2.2.5
       549: 000000000002dfe0    26 FUNC    GLOBAL DEFAULT   14 _ZN60_$LT$core..cell..Bor
       550: 000000000002fcb0    57 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt9Formatter9wr
       551: 000000000002eb20    38 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt8builders9Deb
       552: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND __fxstat64@@GLIBC_2.2.5
       553: 0000000000031690     5 FUNC    GLOBAL DEFAULT   14 _ZN4core3num21_$LT$impl$u
       554: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND signal@@GLIBC_2.2.5
       555: 000000000002fcb0    57 FUNC    GLOBAL DEFAULT   14 _ZN57_$LT$core..fmt..Form
       556: 000000000002e360   690 FUNC    GLOBAL DEFAULT   14 _ZN68_$LT$core..fmt..buil
       557: 0000000000007060    27 FUNC    GLOBAL DEFAULT   14 _ZN4core3str6traits23str_
       558: 0000000000019380   226 FUNC    GLOBAL DEFAULT   14 _ZN79_$LT$std..backtrace_
       559: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND syscall@@GLIBC_2.2.5
       560: 000000000002fd20    23 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt9Formatter12d
       561: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND __gmon_start__
       562: 00000000000162f0    35 FUNC    GLOBAL DEFAULT   14 rust_oom
       563: 0000000000041000     0 OBJECT  GLOBAL HIDDEN    26 __dso_handle
       564: 0000000000031910   146 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num53_$LT$im
       565: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND memcpy@@GLIBC_2.14
       566: 0000000000014ec0   246 FUNC    GLOBAL DEFAULT   14 _ZN70_$LT$std..sync..once
       567: 000000000002fc90    17 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt9Formatter9wr
       568: 000000000002e020   162 FUNC    GLOBAL DEFAULT   14 _ZN82_$LT$core..char..Esc
       569: 0000000000026530    53 FUNC    GLOBAL DEFAULT   14 _ZN6object4read4util11Str
       570: 0000000000018ff0    71 FUNC    GLOBAL DEFAULT   14 _ZN3std3sys4unix17decode_
       571: 0000000000031240   271 FUNC    GLOBAL DEFAULT   14 _ZN66_$LT$core..str..loss
       572: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetIP@@GCC_3.0
       573: 0000000000007770     5 FUNC    GLOBAL DEFAULT   14 __rust_alloc_error_handle
       574: 0000000000030dc0     7 FUNC    GLOBAL DEFAULT   14 _ZN4core3str5lossy9Utf8Lo
       575: 0000000000006ba0    12 FUNC    GLOBAL DEFAULT   14 _ZN5alloc5alloc18handle_a
       576: 0000000000012a00   468 FUNC    GLOBAL DEFAULT   14 _ZN3std3env11current_dir1
       577: 0000000000017020   148 FUNC    GLOBAL DEFAULT   14 _ZN90_$LT$std..panicking.
       578: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_getspecific@@GLIB
       579: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_mutex_unlock@@GLI
       580: 0000000000032880   101 FUNC    GLOBAL DEFAULT   14 __libc_csu_init
       581: 0000000000030260   605 FUNC    GLOBAL DEFAULT   14 _ZN4core3str8converts9fro
       582: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND malloc@@GLIBC_2.2.5
       583: 0000000000031a50   149 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num53_$LT$im
       584: 0000000000031ef0   293 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num3imp52_$L
       585: 0000000000041218     0 NOTYPE  GLOBAL DEFAULT   27 _end
       586: 0000000000012be0   274 FUNC    GLOBAL DEFAULT   14 _ZN3std3ffi5c_str7CString
       587: 0000000000007490    47 FUNC    GLOBAL DEFAULT   14 _start
       588: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND bcmp@@GLIBC_2.2.5
       589: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_rwlock_unlock@@GL
       590: 000000000002e110   129 FUNC    GLOBAL DEFAULT   14 _ZN60_$LT$core..panic..Lo
       591: 0000000000007080  1038 FUNC    GLOBAL DEFAULT   14 _ZN4core3str16slice_error
       592: 000000000002f070  1308 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt9Formatter12p
       593: 00000000000319b0   149 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num55_$LT$im
       594: 0000000000017fd0   106 FUNC    GLOBAL DEFAULT   14 _ZN62_$LT$std..ffi..c_str
       595: 0000000000030050   220 FUNC    GLOBAL DEFAULT   14 _ZN43_$LT$char$u20$as$u20
       596: 000000000002e0e0     5 FUNC    GLOBAL DEFAULT   14 _ZN4core5panic9PanicInfo7
       597: 00000000000304c0  2290 FUNC    GLOBAL DEFAULT   14 _ZN4core3str7pattern11Str
       598: 000000000002fcf0     9 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt9Formatter9al
       599: 0000000000032590    18 FUNC    GLOBAL DEFAULT   14 _ZN4core7unicode12unicode
       600: 0000000000026520     7 FUNC    GLOBAL DEFAULT   14 _ZN6object4read4util11Str
       601: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND realloc@@GLIBC_2.2.5
       602: 0000000000030dd0     7 FUNC    GLOBAL DEFAULT   14 _ZN4core3str5lossy9Utf8Lo
       603: 000000000002e000    26 FUNC    GLOBAL DEFAULT   14 _ZN63_$LT$core..cell..Bor
       604: 000000000002fd10     9 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt9Formatter15d
       605: 0000000000041050     0 NOTYPE  GLOBAL DEFAULT   27 __bss_start
       606: 0000000000027f10    30 FUNC    GLOBAL DEFAULT   14 _ZN5gimli4read6abbrev10At
       607: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND munmap@@GLIBC_2.2.5
       608: 0000000000007590    21 FUNC    GLOBAL DEFAULT   14 main
       609: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_key_create@@GLIBC
       610: 000000000002fdf0   599 FUNC    GLOBAL DEFAULT   14 _ZN41_$LT$char$u20$as$u20
       611: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetDataRelBase@@G
       612: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND poll@@GLIBC_2.2.5
       613: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_SetGR@@GCC_3.0
       614: 000000000002fdb0    17 FUNC    GLOBAL DEFAULT   14 _ZN57_$LT$core..fmt..Form
       615: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND open64@@GLIBC_2.2.5
       616: 0000000000018ea0     8 FUNC    GLOBAL DEFAULT   14 _ZN64_$LT$std..sys..unix.
       617: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND memmove@@GLIBC_2.2.5
       618: 00000000000164f0    67 FUNC    GLOBAL DEFAULT   14 __rust_foreign_exception
       619: 0000000000032020   293 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num3imp52_$L
       620: 00000000000319b0   149 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num55_$LT$im
       621: 000000000002d8b0    83 FUNC    GLOBAL DEFAULT   14 _ZN14rustc_demangle12try_
       622: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_self@@GLIBC_2.2.5
       623: 000000000002daf0    31 FUNC    GLOBAL DEFAULT   14 _ZN5alloc7raw_vec17capaci
       624: 0000000000026600   275 FUNC    GLOBAL DEFAULT   14 _ZN9addr2line9path_push17
       625: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND mprotect@@GLIBC_2.2.5
       626: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND open@@GLIBC_2.2.5
       627: 00000000000327b0   199 FUNC    GLOBAL HIDDEN    14 __umodti3
       628: 0000000000023d20  9112 FUNC    GLOBAL DEFAULT   14 _ZN11miniz_oxide7inflate4
       629: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND sysconf@@GLIBC_2.2.5
       630: 0000000000006cc0    79 FUNC    GLOBAL DEFAULT   14 _ZN4core9panicking5panic1
       631: 0000000000018e30    92 FUNC    GLOBAL DEFAULT   14 _ZN64_$LT$std..sys..unix.
       632: 000000000002eb10    14 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt8builders8Deb
       633: 0000000000018dd0    95 FUNC    GLOBAL DEFAULT   14 _ZN64_$LT$std..sys..unix.
       634: 00000000000170c0    75 FUNC    GLOBAL DEFAULT   14 _ZN93_$LT$std..panicking.
       635: 0000000000015c40   503 FUNC    GLOBAL DEFAULT   14 _ZN3std10sys_common11thre
       636: 0000000000022da0    74 FUNC    GLOBAL DEFAULT   14 __rust_panic_cleanup
       637: 000000000002e100     4 FUNC    GLOBAL DEFAULT   14 _ZN4core5panic8Location6c
       638: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_attr_destroy@@GLI
       639: 000000000002fc90    17 FUNC    GLOBAL DEFAULT   14 _ZN57_$LT$core..fmt..Form
       640: 000000000002e1a0   448 FUNC    GLOBAL DEFAULT   14 _ZN4core9panicking19asser
       641: 00000000000280a0    64 FUNC    GLOBAL DEFAULT   14 _ZN75_$LT$gimli..read..ab
       642: 000000000002fd40    61 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt9Formatter11d
       643: 0000000000028f10  1273 FUNC    GLOBAL DEFAULT   14 _ZN64_$LT$rustc_demangle.
       644: 0000000000030de0  1105 FUNC    GLOBAL DEFAULT   14 _ZN96_$LT$core..str..loss
       645: 0000000000031870   146 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt3num53_$LT$im
       646: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_key_delete@@GLIBC
       647: 0000000000014420  1460 FUNC    GLOBAL DEFAULT   14 _ZN80_$LT$std..path..Comp
       648: 0000000000006dd0   133 FUNC    GLOBAL DEFAULT   14 _ZN4core6result13unwrap_f
       649: 0000000000041050     0 OBJECT  GLOBAL HIDDEN    26 __TMC_END__
       650: 0000000000026a30    44 FUNC    GLOBAL DEFAULT   14 _ZN5gimli4read6abbrev13Ab
       651: 00000000000076d0     1 FUNC    GLOBAL HIDDEN    14 _ZN4core3ptr85drop_in_pla
       652: 0000000000006fe0   116 FUNC    GLOBAL DEFAULT   14 _ZN4core5slice29_$LT$impl
       653: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND posix_memalign@@GLIBC_2.2
       654: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND _ITM_registerTMCloneTable
       655: 0000000000018ea0     8 FUNC    GLOBAL DEFAULT   14 _ZN64_$LT$std..sys..unix.
       656: 000000000002e820   335 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt8builders10De
       657: 000000000002e7d0    78 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt8builders11De
       658: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_DeleteException@@
       659: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND sigaltstack@@GLIBC_2.2.5
       660: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND dlsym@@GLIBC_2.2.5
       661: 0000000000006790   159 FUNC    GLOBAL DEFAULT   14 _ZN3std9panicking3try7cle
       662: 0000000000007750     5 FUNC    GLOBAL DEFAULT   14 __rust_realloc
       663: 0000000000007650    25 FUNC    GLOBAL HIDDEN    14 _ZN4core3ops8function6FnO
       664: 0000000000017110    11 FUNC    GLOBAL DEFAULT   14 _ZN93_$LT$std..panicking.
       665: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_Resume@@GCC_3.0
       666: 0000000000012850   424 FUNC    GLOBAL DEFAULT   14 _ZN3std6thread6Thread3new
       667: 00000000000316a0   136 FUNC    GLOBAL DEFAULT   14 _ZN4core3num60_$LT$impl$u
       668: 000000000002fd80    35 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt9Formatter10d
       669: 00000000000326e0   202 FUNC    GLOBAL HIDDEN    14 __udivti3
       670: 0000000000000000     0 FUNC    WEAK   DEFAULT  UND __cxa_finalize@@GLIBC_2.2
       671: 000000000002e970   117 FUNC    GLOBAL DEFAULT   14 _ZN4core3fmt8builders10De
       672: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_mutex_lock@@GLIBC
       673: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_SetIP@@GCC_3.0
    
    File: libsum.rlib(sum.sum.3a1fbbbh-cgu.0.rcgu.o)
    
    Symbol table '.symtab' contains 4 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.3a1fbbbh-cgu.0
         2: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
         3: 0000000000000000    24 FUNC    GLOBAL HIDDEN     5 _ZN49_$LT$usize$u20$as$u2
    
    File: libsum.rlib(sum.sum.3a1fbbbh-cgu.1.rcgu.o)
    
    Symbol table '.symtab' contains 4 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.3a1fbbbh-cgu.1
         2: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
         3: 0000000000000000    15 FUNC    GLOBAL HIDDEN     5 _ZN4core3cmp5impls57_$LT$
    
    File: libsum.rlib(sum.sum.3a1fbbbh-cgu.2.rcgu.o)
    
    Symbol table '.symtab' contains 6 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.3a1fbbbh-cgu.2
         2: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
         3: 0000000000000000     0 SECTION LOCAL  DEFAULT    6 
         4: 0000000000000000    46 FUNC    GLOBAL DEFAULT    5 _ZN4core3ptr4read17h970db
         5: 0000000000000000    14 FUNC    GLOBAL DEFAULT    6 _ZN4core3ptr5write17hde06
    
    File: libsum.rlib(sum.sum.3a1fbbbh-cgu.3.rcgu.o)
    
    Symbol table '.symtab' contains 10 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.3a1fbbbh-cgu.3
         2: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
         3: 0000000000000000     0 SECTION LOCAL  DEFAULT    7 
         4: 0000000000000000     0 NOTYPE  GLOBAL HIDDEN   UND _ZN49_$LT$usize$u20$as$u2
         5: 0000000000000000     0 NOTYPE  GLOBAL HIDDEN   UND _ZN4core3cmp5impls57_$LT$
         6: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND _ZN4core3mem7replace17hd8
         7: 0000000000000000   139 FUNC    GLOBAL DEFAULT    5 _ZN4core4iter5range101_$L
         8: 0000000000000000     0 NOTYPE  GLOBAL HIDDEN   UND _ZN4core5clone5impls54_$L
         9: 0000000000000000     7 FUNC    GLOBAL DEFAULT    7 _ZN63_$LT$I$u20$as$u20$co
    
    File: libsum.rlib(sum.sum.3a1fbbbh-cgu.4.rcgu.o)
    
    Symbol table '.symtab' contains 17 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.3a1fbbbh-cgu.4
         2: 0000000000000000    28 OBJECT  LOCAL  DEFAULT   12 str.0
         3: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
         4: 0000000000000000     0 SECTION LOCAL  DEFAULT    7 
         5: 0000000000000000     0 SECTION LOCAL  DEFAULT    9 
         6: 0000000000000000     0 SECTION LOCAL  DEFAULT   10 
         7: 0000000000000000     0 SECTION LOCAL  DEFAULT   12 
         8: 0000000000000000     0 SECTION LOCAL  DEFAULT   13 
         9: 0000000000000000     0 SECTION LOCAL  DEFAULT   15 
        10: 0000000000000000    53 FUNC    GLOBAL DEFAULT    5 _ZN3sum4suma17h06aac0d327
        11: 0000000000000000   278 FUNC    GLOBAL DEFAULT    7 _ZN3sum9sumatoria17h4fb7d
        12: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND _ZN4core4iter5range101_$L
        13: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND _ZN4core5slice29_$LT$impl
        14: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND _ZN4core9panicking18panic
        15: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND _ZN4core9panicking5panic1
        16: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND _ZN63_$LT$I$u20$as$u20$co
    
    File: libsum.rlib(sum.sum.3a1fbbbh-cgu.5.rcgu.o)
    
    Symbol table '.symtab' contains 4 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.3a1fbbbh-cgu.5
         2: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
         3: 0000000000000000     4 FUNC    GLOBAL HIDDEN     5 _ZN4core5clone5impls54_$L
    
    File: libsum.rlib(sum.sum.3a1fbbbh-cgu.6.rcgu.o)
    
    Symbol table '.symtab' contains 4 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.3a1fbbbh-cgu.6
         2: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
         3: 0000000000000000    16 FUNC    GLOBAL DEFAULT    5 _ZN4core5slice29_$LT$impl
    
    File: libsum.rlib(sum.sum.3a1fbbbh-cgu.7.rcgu.o)
    
    Symbol table '.symtab' contains 11 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS sum.3a1fbbbh-cgu.7
         2: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT    7 GCC_except_table0
         3: 0000000000000000     0 SECTION LOCAL  DEFAULT    5 
         4: 0000000000000000     0 SECTION LOCAL  DEFAULT    7 
         5: 0000000000000000     8 OBJECT  WEAK   HIDDEN     9 DW.ref.rust_eh_personalit
         6: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND _Unwind_Resume
         7: 0000000000000000   136 FUNC    GLOBAL DEFAULT    5 _ZN4core3mem7replace17hd8
         8: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND _ZN4core3ptr4read17h970db
         9: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND _ZN4core3ptr5write17hde06
        10: 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND rust_eh_personality
    
    File: libsum.rlib(lib.rmeta)
    
    Symbol table '.dynsym' contains 15 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND _ITM_deregisterTMCloneTab
         2: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetRegionStart@GCC_3.0 (2)
         3: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetTextRelBase@GCC_3.0 (2)
         4: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetIPInfo@GCC_4.2.0 (3)
         5: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetLanguageSpecif@GCC_3.0 (2)
         6: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND __gmon_start__
         7: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_mutex_unlock@GLIBC_2.2.5 (4)
         8: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetDataRelBase@GCC_3.0 (2)
         9: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_SetGR@GCC_3.0 (2)
        10: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND _ITM_registerTMCloneTable
        11: 0000000000000000     0 FUNC    WEAK   DEFAULT  UND __cxa_finalize@GLIBC_2.2.5 (5)
        12: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_mutex_lock@GLIBC_2.2.5 (4)
        13: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_SetIP@GCC_3.0 (2)
        14: 0000000000001310   737 FUNC    GLOBAL DEFAULT   11 rust_eh_personality
    
    Symbol table '.symtab' contains 81 entries:
       Num:    Value          Size Type    Bind   Vis      Ndx Name
         0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
         1: 0000000000000238     0 SECTION LOCAL  DEFAULT    1 
         2: 0000000000000260     0 SECTION LOCAL  DEFAULT    2 
         3: 0000000000000288     0 SECTION LOCAL  DEFAULT    3 
         4: 00000000000003f0     0 SECTION LOCAL  DEFAULT    4 
         5: 000000000000057a     0 SECTION LOCAL  DEFAULT    5 
         6: 0000000000000598     0 SECTION LOCAL  DEFAULT    6 
         7: 0000000000000608     0 SECTION LOCAL  DEFAULT    7 
         8: 0000000000001000     0 SECTION LOCAL  DEFAULT    8 
         9: 0000000000001020     0 SECTION LOCAL  DEFAULT    9 
        10: 0000000000001030     0 SECTION LOCAL  DEFAULT   10 
        11: 0000000000001040     0 SECTION LOCAL  DEFAULT   11 
        12: 00000000000015f4     0 SECTION LOCAL  DEFAULT   12 
        13: 0000000000002000     0 SECTION LOCAL  DEFAULT   13 
        14: 0000000000002058     0 SECTION LOCAL  DEFAULT   14 
        15: 00000000000020b8     0 SECTION LOCAL  DEFAULT   15 
        16: 0000000000003d18     0 SECTION LOCAL  DEFAULT   16 
        17: 0000000000003d28     0 SECTION LOCAL  DEFAULT   17 
        18: 0000000000003d30     0 SECTION LOCAL  DEFAULT   18 
        19: 0000000000003d90     0 SECTION LOCAL  DEFAULT   19 
        20: 0000000000003f80     0 SECTION LOCAL  DEFAULT   20 
        21: 0000000000004000     0 SECTION LOCAL  DEFAULT   21 
        22: 0000000000004008     0 SECTION LOCAL  DEFAULT   22 
        23: 0000000000000000     0 SECTION LOCAL  DEFAULT   23 
        24: 0000000000000000     0 SECTION LOCAL  DEFAULT   24 
        25: 0000000000000000     0 SECTION LOCAL  DEFAULT   25 
        26: 0000000000000000     0 SECTION LOCAL  DEFAULT   26 
        27: 0000000000000000     0 SECTION LOCAL  DEFAULT   27 
        28: 0000000000000000     0 SECTION LOCAL  DEFAULT   28 
        29: 0000000000000000     0 SECTION LOCAL  DEFAULT   29 
        30: 0000000000000000     0 SECTION LOCAL  DEFAULT   30 
        31: 0000000000000000     0 SECTION LOCAL  DEFAULT   31 
        32: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS crtstuff.c
        33: 0000000000001040     0 FUNC    LOCAL  DEFAULT   11 deregister_tm_clones
        34: 0000000000001070     0 FUNC    LOCAL  DEFAULT   11 register_tm_clones
        35: 00000000000010b0     0 FUNC    LOCAL  DEFAULT   11 __do_global_dtors_aux
        36: 0000000000004008     1 OBJECT  LOCAL  DEFAULT   22 completed.8060
        37: 0000000000003d28     0 OBJECT  LOCAL  DEFAULT   17 __do_global_dtors_aux_fin
        38: 00000000000010f0     0 FUNC    LOCAL  DEFAULT   11 frame_dummy
        39: 0000000000003d20     0 OBJECT  LOCAL  DEFAULT   16 __frame_dummy_init_array_
        40: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS std.9m6hw7w6-cgu.0
        41: 0000000000001100    55 FUNC    LOCAL  DEFAULT   11 _ZN3std3sys4unix4args3imp
        42: 0000000000003d18     8 OBJECT  LOCAL  DEFAULT   16 _ZN3std3sys4unix4args3imp
        43: 0000000000004010     8 OBJECT  LOCAL  DEFAULT   22 _ZN3std3sys4unix4args3imp
        44: 0000000000004018     8 OBJECT  LOCAL  DEFAULT   22 _ZN3std3sys4unix4args3imp
        45: 0000000000004020    40 OBJECT  LOCAL  DEFAULT   22 _ZN3std3sys4unix4args3imp
        46: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS panic_unwind.b34o5za4-cgu
        47: 0000000000001170   381 FUNC    LOCAL  DEFAULT   11 _ZN12panic_unwind5dwarf2e
        48: 00000000000012f0    12 FUNC    LOCAL  DEFAULT   11 _ZN12panic_unwind8real_im
        49: 0000000000001300    12 FUNC    LOCAL  DEFAULT   11 _ZN12panic_unwind8real_im
        50: 0000000000001140    12 FUNC    LOCAL  DEFAULT   11 _ZN4core3ops8function6FnO
        51: 0000000000001150    12 FUNC    LOCAL  DEFAULT   11 _ZN4core3ops8function6FnO
        52: 0000000000001160     1 FUNC    LOCAL  DEFAULT   11 _ZN4core3ptr88drop_in_pla
        53: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS 1yafyrf2uaakrs3o
        54: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS crtstuff.c
        55: 000000000000222c     0 OBJECT  LOCAL  DEFAULT   15 __FRAME_END__
        56: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS rustc_demangle.axzg541g-c
        57: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS alloc.bdtv0pny-cgu.0
        58: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS core.2eb9xv2h-cgu.0
        59: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS 
        60: 00000000000015f4     0 FUNC    LOCAL  DEFAULT   12 _fini
        61: 0000000000004000     0 OBJECT  LOCAL  DEFAULT   21 __dso_handle
        62: 0000000000003d90     0 OBJECT  LOCAL  DEFAULT   19 _DYNAMIC
        63: 0000000000002058     0 NOTYPE  LOCAL  DEFAULT   14 __GNU_EH_FRAME_HDR
        64: 0000000000004008     0 OBJECT  LOCAL  DEFAULT   21 __TMC_END__
        65: 0000000000003f80     0 OBJECT  LOCAL  DEFAULT   20 _GLOBAL_OFFSET_TABLE_
        66: 0000000000001000     0 FUNC    LOCAL  DEFAULT    8 _init
        67: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND _ITM_deregisterTMCloneTab
        68: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetRegionStart@@G
        69: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetTextRelBase@@G
        70: 0000000000001310   737 FUNC    GLOBAL DEFAULT   11 rust_eh_personality
        71: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetIPInfo@@GCC_4.
        72: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetLanguageSpecif
        73: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND __gmon_start__
        74: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_mutex_unlock@@GLI
        75: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_GetDataRelBase@@G
        76: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_SetGR@@GCC_3.0
        77: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND _ITM_registerTMCloneTable
        78: 0000000000000000     0 FUNC    WEAK   DEFAULT  UND __cxa_finalize@@GLIBC_2.2
        79: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND pthread_mutex_lock@@GLIBC
        80: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _Unwind_SetIP@@GCC_3.0
    
Nota varias cosas interesantes:

* La dirección asociada a los símbolos suma y sumatoria es relativa a 0. Esto ocurrirá
  con cada relocatable object file. Por tanto será responsabilidad del enlazador ubicar
  los símbolos en una dirección apropiada una vez se mezclen los archivos para formar
  el ejecutable.
* Hay algunos símbolos marcados como LOCAL y otros GLOBAL. GLOBAL indica que son visibles al momento de combinarlos con otros relocatable
  object files.

Ya hemos dicho en varias oportunidades que los relocatable object files incluyen
el código de máquina del programa. Lo puedes observar con el siguientes comando:

``objdump -d functions.o``

.. code-block:: bash

    libsum.so:     file format elf64-x86-64


    Disassembly of section .init:

    0000000000001000 <_init>:
        1000:	f3 0f 1e fa          	endbr64 
        1004:	48 83 ec 08          	sub    $0x8,%rsp
        1008:	48 8b 05 b1 2f 00 00 	mov    0x2fb1(%rip),%rax        # 3fc0 <__gmon_start__>
        100f:	48 85 c0             	test   %rax,%rax
        1012:	74 02                	je     1016 <_init+0x16>
        1014:	ff d0                	callq  *%rax
        1016:	48 83 c4 08          	add    $0x8,%rsp
        101a:	c3                   	retq   

    Disassembly of section .plt:

    0000000000001020 <.plt>:
        1020:	ff 35 62 2f 00 00    	pushq  0x2f62(%rip)        # 3f88 <_GLOBAL_OFFSET_TABLE_+0x8>
        1026:	ff 25 64 2f 00 00    	jmpq   *0x2f64(%rip)        # 3f90 <_GLOBAL_OFFSET_TABLE_+0x10>
        102c:	0f 1f 40 00          	nopl   0x0(%rax)

    Disassembly of section .plt.got:

    0000000000001030 <__cxa_finalize@plt>:
        1030:	ff 25 b2 2f 00 00    	jmpq   *0x2fb2(%rip)        # 3fe8 <__cxa_finalize@GLIBC_2.2.5>
        1036:	66 90                	xchg   %ax,%ax

    Disassembly of section .text:

    0000000000001040 <deregister_tm_clones>:
        1040:	48 8d 3d c1 2f 00 00 	lea    0x2fc1(%rip),%rdi        # 4008 <completed.8060>
        1047:	48 8d 05 ba 2f 00 00 	lea    0x2fba(%rip),%rax        # 4008 <completed.8060>
        104e:	48 39 f8             	cmp    %rdi,%rax
        1051:	74 15                	je     1068 <deregister_tm_clones+0x28>
        1053:	48 8b 05 3e 2f 00 00 	mov    0x2f3e(%rip),%rax        # 3f98 <_ITM_deregisterTMCloneTable>
        105a:	48 85 c0             	test   %rax,%rax
        105d:	74 09                	je     1068 <deregister_tm_clones+0x28>
        105f:	ff e0                	jmpq   *%rax
        1061:	0f 1f 80 00 00 00 00 	nopl   0x0(%rax)
        1068:	c3                   	retq   
        1069:	0f 1f 80 00 00 00 00 	nopl   0x0(%rax)

    0000000000001070 <register_tm_clones>:
        1070:	48 8d 3d 91 2f 00 00 	lea    0x2f91(%rip),%rdi        # 4008 <completed.8060>
        1077:	48 8d 35 8a 2f 00 00 	lea    0x2f8a(%rip),%rsi        # 4008 <completed.8060>
        107e:	48 29 fe             	sub    %rdi,%rsi
        1081:	48 89 f0             	mov    %rsi,%rax
        1084:	48 c1 ee 3f          	shr    $0x3f,%rsi
        1088:	48 c1 f8 03          	sar    $0x3,%rax
        108c:	48 01 c6             	add    %rax,%rsi
        108f:	48 d1 fe             	sar    %rsi
        1092:	74 14                	je     10a8 <register_tm_clones+0x38>
        1094:	48 8b 05 45 2f 00 00 	mov    0x2f45(%rip),%rax        # 3fe0 <_ITM_registerTMCloneTable>
        109b:	48 85 c0             	test   %rax,%rax
        109e:	74 08                	je     10a8 <register_tm_clones+0x38>
        10a0:	ff e0                	jmpq   *%rax
        10a2:	66 0f 1f 44 00 00    	nopw   0x0(%rax,%rax,1)
        10a8:	c3                   	retq   
        10a9:	0f 1f 80 00 00 00 00 	nopl   0x0(%rax)

    00000000000010b0 <__do_global_dtors_aux>:
        10b0:	f3 0f 1e fa          	endbr64 
        10b4:	80 3d 4d 2f 00 00 00 	cmpb   $0x0,0x2f4d(%rip)        # 4008 <completed.8060>
        10bb:	75 2b                	jne    10e8 <__do_global_dtors_aux+0x38>
        10bd:	55                   	push   %rbp
        10be:	48 83 3d 22 2f 00 00 	cmpq   $0x0,0x2f22(%rip)        # 3fe8 <__cxa_finalize@GLIBC_2.2.5>
        10c5:	00 
        10c6:	48 89 e5             	mov    %rsp,%rbp
        10c9:	74 0c                	je     10d7 <__do_global_dtors_aux+0x27>
        10cb:	48 8b 3d 2e 2f 00 00 	mov    0x2f2e(%rip),%rdi        # 4000 <__dso_handle>
        10d2:	e8 59 ff ff ff       	callq  1030 <__cxa_finalize@plt>
        10d7:	e8 64 ff ff ff       	callq  1040 <deregister_tm_clones>
        10dc:	c6 05 25 2f 00 00 01 	movb   $0x1,0x2f25(%rip)        # 4008 <completed.8060>
        10e3:	5d                   	pop    %rbp
        10e4:	c3                   	retq   
        10e5:	0f 1f 00             	nopl   (%rax)
        10e8:	c3                   	retq   
        10e9:	0f 1f 80 00 00 00 00 	nopl   0x0(%rax)

    00000000000010f0 <frame_dummy>:
        10f0:	f3 0f 1e fa          	endbr64 
        10f4:	e9 77 ff ff ff       	jmpq   1070 <register_tm_clones>
        10f9:	0f 1f 80 00 00 00 00 	nopl   0x0(%rax)

    0000000000001100 <_ZN3std3sys4unix4args3imp15ARGV_INIT_ARRAY12init_wrapper17h9bae8a0cafc2b6ccE>:
        1100:	41 57                	push   %r15
        1102:	41 56                	push   %r14
        1104:	53                   	push   %rbx
        1105:	49 89 f7             	mov    %rsi,%r15
        1108:	48 63 df             	movslq %edi,%rbx
        110b:	4c 8d 35 0e 2f 00 00 	lea    0x2f0e(%rip),%r14        # 4020 <_ZN3std3sys4unix4args3imp4LOCK17h600045dca3348f0eE>
        1112:	4c 89 f7             	mov    %r14,%rdi
        1115:	ff 15 d5 2e 00 00    	callq  *0x2ed5(%rip)        # 3ff0 <pthread_mutex_lock@GLIBC_2.2.5>
        111b:	48 89 1d ee 2e 00 00 	mov    %rbx,0x2eee(%rip)        # 4010 <_ZN3std3sys4unix4args3imp4ARGC17h393a33c6be9e9b3bE>
        1122:	4c 89 3d ef 2e 00 00 	mov    %r15,0x2eef(%rip)        # 4018 <_ZN3std3sys4unix4args3imp4ARGV17h5274ca72b78295baE>
        1129:	4c 89 f7             	mov    %r14,%rdi
        112c:	5b                   	pop    %rbx
        112d:	41 5e                	pop    %r14
        112f:	41 5f                	pop    %r15
        1131:	ff 25 91 2e 00 00    	jmpq   *0x2e91(%rip)        # 3fc8 <pthread_mutex_unlock@GLIBC_2.2.5>
        1137:	66 0f 1f 84 00 00 00 	nopw   0x0(%rax,%rax,1)
        113e:	00 00 

    0000000000001140 <_ZN4core3ops8function6FnOnce40call_once$u7b$$u7b$vtable.shim$u7d$$u7d$17h0318dffd3a9d1c14E>:
        1140:	48 8b 07             	mov    (%rdi),%rax
        1143:	48 8b 38             	mov    (%rax),%rdi
        1146:	ff 25 84 2e 00 00    	jmpq   *0x2e84(%rip)        # 3fd0 <_Unwind_GetDataRelBase@GCC_3.0>
        114c:	0f 1f 40 00          	nopl   0x0(%rax)

    0000000000001150 <_ZN4core3ops8function6FnOnce40call_once$u7b$$u7b$vtable.shim$u7d$$u7d$17h3dfb55efa1414d46E>:
        1150:	48 8b 07             	mov    (%rdi),%rax
        1153:	48 8b 38             	mov    (%rax),%rdi
        1156:	ff 25 4c 2e 00 00    	jmpq   *0x2e4c(%rip)        # 3fa8 <_Unwind_GetTextRelBase@GCC_3.0>
        115c:	0f 1f 40 00          	nopl   0x0(%rax)

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

