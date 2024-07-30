# Todos Compilados

## C++: Standard Template Library y Conceptos

> ¿Qué son las librerías STL? ¿Qué ventajas ofrece? Dé un ejemplo de su uso.

STL es el acrónimo de *Standard Template Library*, una librería para el desarrrollo de programas en C++. Esta librería la componen **algoritmos**, **iteradores**, **contenedores** y **funciones**. Todas están relacionadas entre sí y dedicadas a facilitar la implementación de diversas estructuras de datos frecuentemente utilizadas en la programación.

```cpp
std::list<int> numeros = {0, -1, 5, 2, 9};
std::sort(numeros.begin(), numeros.end());
numeros.push_back(13);
std::list::iterator it;
for (it = numeros.begin(); it != numeros.end(); ++it) {
    std::cout << *it << std::endl;
}
```

> ¿Qué es un iterador en STL? Ejemplificar

STL es la Standard Template Library de C++. Un iterador es un objeto usado para recoorer secuencialmente los elementos de tipos contenedores, tales como un `std::vector`, una `std::list` o un `std::map`. Sirven para recorrer estas estructuras y permiten la modificación del elemento contenido, modificando al espacio de memoria apuntado.

En STL, los iteradores son usados por varios algoritmos, como por ejemplo, `std::sort`, `std::find` o los métodos `begin()` y `end()` de los contenedores, que devuelven un iterador.

```cpp
std::vector<int> numeros = {1, 2, 3};

// it es del tipo std::vector<int>::iterator.
for (auto it = numeros.begin(); it != numeros.end(); it++) {
    std::cout << *it << std::endl;
}
```

> Explicar constructor move. Ejemplificar.

> ¿Qué es un **functor**? ¿Qué ventaja ofrece frente a una función convencional? **Ejemplifique**.

> ¿En qué consiste el patrón de diseño **RAII**? Ejemplifique.

> ¿Qué significa que una función sea **blocante**? ¿Cómo subsanaría esa limitación en términos de **mantener el programa 'vivo'**?

> ¿Qué significa la palabra **virtual** antepuesta a un método de una clase? ¿Qué cambios genbera a nivel **compilación** y al momento de **ejecución**?

> ¿Qué significado tiene la palabra reservada `static` cuando es antepuesta a una variable local a una función? Ejemplifique.

La palabra `static` en dicho contexto connota que la variable no será una variable temporal de la función sino que perdurará en la ejecución de la misma. Esta variable será alojada en el segmento de datos (data segment) y se inicializará una sola vez.

> Explicar el efecto de anteponer la palabra `static` a un método de una clase. Ejemplifique con un código simple.

Declarar un método estático significa que el método pertenece a la clase en sí y no a una instancia, por lo que se puede acceder al método sin necesidad de crear un objeto de la clase.

```cpp
clas Printer {
 public:
    static void printMessage(const std::string& msg) {
        std::cout << msg << std::endl;
    }
};

int main() {
    Printer::printMessage("Imprimí esto");
    return 0;
}
```

> ¿Qué es un parámetro **constante**? **Ejemplifique**.

Es un parámetro al cual no se le puede modificar su estado, solo se puede llamar a sus métodos constantes.

```cpp
int suma(const int a, const int b) {
    return a + b;
}
```

### Constructores

> Explique qué es y para qué sirve un **constructor de copia** en C++.
>
> - Indique cómo se comporta el sistema si éste **no es definido por el desarrollador**
> - Explique al menos una estrategia para **evitar que una clase particular sea copiable**
> - Indique qué **diferencia** existe entre un constructor de **copia** y uno **move**.

> ¿Qué diferencia existe entre un **constructor por copia** y uno por **movimiento**? **Ejemplifique**.

> Explique qué es y para qué sirve una **variable de clase** (o atributo estático) en C++. Mediante un ejemplo de uso, indique cómo se define dicha variable, su inicialización y el acceso a su valor para realizar una impresión simple dentro de un **main**.

> Explique qué es y para qué sirve un **constructor MOVE** en C++. Indique cómo se comporta el sistema si éste **no es definido por el desarrollador**.

> ¿Qué significa la palabra `const` cuando sucede a una declaración de un método de una clase? Ejemplifique.

Significa que el valor de sus atributos **no** puede **ni debe** cambiar, por lo que quedarán fijos sin sufrir alteraciones. En caso de querer modificar algún valor de estos, habría un error de compilación.

> ¿Qué significa `this`en C++? ¿Dónde se usa explícita o implícitamente?

Es un puntero que mantiene la dirección de memoria del objeto actual, es decir, aquel usado para llamar al método. Se usa explícitamente para diferenciar ambigüedades cuando aparecen variables o parámetros con el mismo nombre que algún atributo de la clase o para retornar una referencia al mismo; implícitamente, al usar atributos del objeto.

## Compilación y Enlace

> ¿Qué es una **macro** de **C**? Detalle las **buenas prácticas** para su definición. Ejemplifique.

Una macro es una instrucción al procesador que permite reemplazar una secuencia de texto por otra durante la compilación.
Una buena práctica es que las constantes sean definidas por esta vía así se evita tener que cambiar su valor en varios lugares del código en lugar de hacerlo en un solo lugar.

```c
#define PI 3.141592652589
#define CUADRADO(x) x*x

int main(int argc, char* argv[]) {
    float radio = argv[1];
    float areaCirculo = PI * CUADRADO(radio);
}
```

> Describa el **proceso de transformación de código** fuente a un ejecutable. Precise las **etapas**, las **tareas desarrolladas** y los **tipos de error** generados en cada una de ellas.

> Explique qué se entiende por "**compilación condicional**". ¿En qué etapa del proceso de transformación de código se resuelve? **Ejemnplifique** mediante código C dando un caso de uso útil.

C++ ofrece la posibilidad de compilación condicional mediante la inclusión de ciertas directivas que controlan el comportamiento del preprocesador, de forma tal que este puede ignorar o compilar determinadas líneas de código en función de ciertas condiciones que son evaluadas durante el preprocesamiento. Las directivas #ifndef, #define, #endif, etc funcionan análogamente a los condicionales. En este ejemplo, si ifndef es positivo, no se redefine:

```c
#ifndef ALGO_H_
#define ALGO_H_
...
#endif // ALGO_H_
```

> **¿Qué características debe tener un compilador C para que sea considerado "portable"?**

> Explique **qué es** cada uno de los siguientes, haciendo referencia a su **inicialización**, su **comportamiento** y el **área de memoria** donde residen:
>
> - Una variable **global static**.
> - Una variable **local static**.
> - Un **atributo de clase static**.

> Explique el funcionamiento de la sentencia de precompilación `#undef`.

La secuencia de precompilación `#undef` elimina la definición previa de algún símbolo de precompilación. Si no encuentra ningún símbolo con dicho nombre, no realiza ninguna acción.

> ¿Cómo se evita que un .h sea compilado **más de una vez** dentro de la misma unidad? ¿Qué **instrucciones de precompilación** suelen utilizarse? Ejemplifique.

Se suelen usar las instrucciones `#ifndef`, `#define` y `#endif`. Estas directivas comprueban la presencia o ausencia de los identificadores definidos.

```c
#ifndef MI_CLASE_H_
#define MI_CLASE_H_
...
#endif // MI_CLASE_H_
```

> ¿Qué es el pre-compilador? Explique dos instrucciones cualquiera que éste procese.

Es un procesador de texto que identifica MACROS y hace reemplazo de texto o algunas ediciones condicionales. Sirve para definir secuencias de código que se repetirán pero no tienen sentido como función o definir constantes.
Una sentencia usada es el `#define`, que define un símbolo para el precompilador que perdurará durante la compilación, por lo que se podrá consultar si ya se encuentra definido.
Otra sentencia usada es el `#include`, que busca el archivo indicado y lo copia en la fuente actual. Se puede usar para llamar a bibliotecas, secuencias, funciones y objetos dentro o fuera del programa.

> ¿En qué consiste el proceso de linkedición?

Consiste en asociar los símbolos procesaddos por el compilador con la dirección de memoria correspondiente. Por ejemplo, los métodos con sus definiciones, las funciones con sus bloques de memoria correspondiente, las variables globales con sus posiciones de memoria.

> **Describa y ejemplifique** el uso de la siguiente instrucción de precompilación: **#if**.

La instrucción de precompilación `#if` abre una compilación condicional, donde el código solo se compila si la expresión correspondiente al símbolo es verdadera.
En el código de ejemplo, DEBUG es verdadero puesto que está definido en 1, mientras que TESTING es falso ya que se define como 0. Por lo tanto, sí se imprimirá "DEBUGGING" pero no "TESTING".

```cpp
#define DEBUG 1
#define TESTING 0

#if DEBUG
    std::cout << "DEBUGGING" << std::endl;
#endif
#if TESTING
    std::cout << "TESTING" << std::endl;
#endif
```

## Declaraciones y Definiciones

> Describir y decir si es una declaración/definición:
>
> - `static int *(*A)();`
> - `extern unsigned char *(*B)[1];`
> - `bool *C() {return 0;}`

> **Describa con exactitud** las siguientes **declaraciones/definiciones globales**:
>
> 1. *`void (*F)(int i);`*
> 2. *`static void B(float a, float b) {}`*
> 3. *`int *(*C)[5];`*

> **Describa con exactitud** las siguientes **declaraciones/definiciones globales**:
>
> - `extern float (*l)[3];`
> - `static int *C[3];`
> - `static short F(const float *a);`

> Describa con exactitud cada uno de los siguientes:
>
> - **`statuc int A=7;`**
> - **`extern char *(*B)[7];`**
> - **`float **C;`**

> Escriba las siguientes definiciones/declaraciones:
>
> - Definición de una la función SUMA, que tome dos enteros largos con signo y devuelva su suma. Esta función solo debe ser visible en el módulo donde se la define.
> - Declaración de un puntero a puntero a entero sin signo.
> - Definición de un caracter solamente visible en el módulo donde se define.

> Escriba las siguientes definiciones/declaraciones:
>
> - Declaración de un puntero a puntero a entero largo con signo.
> - Definición de una la función RESTA, que tome dos enteros largos con signo y devuelva su resta. Esta función debe ser visible en todos los módulos del programa.
> - Definición de un caracter solamente visible en el módulo donde se define.

## Explicación de funciones

> Explique breve y concretamente qué es **f**:
>
> ```cpp
> int (*f) (short *, char[4]);
> ```

> Explique breve y concretamente qué es **f**:
>
> ```cpp
> int (*f) (short int*, char[3]);
> ```

> Explique breve y concretamente qué es **f**:
>
> `char (*f)(int *, char[3]);`

## Programación Orientada a Objetos

> Explicar "code bloat" en la construcción de un Template. Ejemplificar y mostrar cómo evitarlo.

El *code bloat* se produce cuando un Template termina siendo muy grande y teniendo demasiadas responsabilidades, normalmente también teniendo código duplicado.[^1]

[^1]: https://refactoring.guru/refactoring/smells/bloaters

En este fragmento, se tiene una clase que realiza demasiadas acciones, pudiéndose modularizar.

```cpp
#include <iostream>
#include <vector>

template <typename T>
class DataProcessor {
public:
    void addData(const T& data) {
        data_.push_back(data);
    }

    void processData() {
        for (const auto& item : data_) {
            std::cout << item << std::endl;
        }
    }

    void clearData() {
        data_.clear();
    }

    void sortData() {
        std::sort(data_.begin(), data_.end());
    }

    T getMax() {
        return *std::max_element(data_.begin(), data_.end());
    }

    T getMin() {
        return *std::min_element(data_.begin(), data_.end());
    }

private:
    std::vector<T> data_;
};
```

> Explique qué son **los métodos virtuales** y para qué sirven. Dé un breve ejemplo donde su uso sea imprescindible.

> Explique qué son **los métodos virtuales puros** y para qué sirven. Dé un breve ejemplo donde su uso sea **imprescindible**.

> ¿Por qué las librerías que usan **Templates** se publican con todo el código fuente y no como un .h y .o/.obj?

> ¿Cuál es el motivo por el cual las clases que utilizan templates se declaran y definen en los .h?

Los template deben poseer la definición en el mismo .h porque el compilador los usa para generar la clase actual, y este necesita el código para instanciar la plantilla. Si se colocara una implementación de plantilla en un archivo .cpp, solo podrá crear una instancia de la plantilla en ese mismo archivo .cpp.

> ¿Qué es el **polimorfismo**? Ejemplifique mediante código.

> ¿Qué consideración particular debe tenerse en cuenta al momento de definir una clase que usa memoria dinámica y será usada con polimorfismo? ¿Por qué?

El destructor debe ser virtual. El objeto, si bien será una instancia de la clase derivada, será tratado como una instancia de clase base y, si su destructor no es virtual, al llamarlo no se liberará la memoria alocada por la clase derivada porque no se llamará al destructor de derivada.

## Análisis de Código

> Analice el siguiente código y determine lo que se imprime (valor de Pi)
>
> ```cpp
> main() {
>     int *Pi = 1000;
>     Pi++;
>     printf("Pi apunta a la dirección: %l", (long)Pi);
> }
> ```

> Considere la estructura `struct ejemplo {int a; char b;}`. ¿Es verdad que **sizeof(ejemplo) = sizeof(a) + sizeof(b)**? **Justifique**.

> Indique la **salida** del siguiente programa:
>
> ```cpp
> class A {
>     A() {
>         cout << "A()" << endl;
>     }
>     ~A() {
>         cout << "~A()" << endl;
>     }
> }
>
> class B : public A {
>     B() {
>         cout << "B()" << endl;
>     }
>     ~B() {
>         cout << "~B()" << endl;
>     }
> }
>
> int main() {
>     B b;
>     return 0;
> }
> ```

> ¿Qué valor arroja **sizeof(int)**? **Justifique**.

> Explique **qué es (a), (b), (c) y (d)**, haciendo referencia a su valor y momento de **inicialización**, su **comportamiento** y el **área de memoria** donde residen:
>
> ```cpp
> static int a;
> int b() {
>     static int c;
>     char d = 65;
>     return c + (int) d;
> }
> ```

## Programación Orientada a Eventos

> **Describa** el concepto de **loop de eventos (events loop)** utilizando en programación orientada a eventos y, en particular, en entornos de interfaz gráfica (GUIs).

## Redes y Concurrencia - Threads

> ¿Qué es la critical section? Ejemplificar cómo protegerla.

> ¿Qué función se usa para lanzar un hilo? Ejemplificar.

> ¿Cómo se logra que 2 **threads** accedan (lectura/escritura) a un mismo recurso compartido sin que se generen problemas de consistencia? **Ejemplifique**.

> ¿Qué ventaja ofrece un **lock raii** frente al tradicional **lock/unlock**?

> ¿Qué función utiliza para esperar la terminación de un **thread**? Ejemplifique mediante código.

Cuando un thread se quiere cerrar o termina su vida útil, se usa la función `join()`.

```cpp
void doSomething(int num) {
    std::cout << "Hilo " << num << " comienza ejecución." << std::endl;
    // Hace algo
    std::cout << "Hilo " << num << " finaliza ejecución." << std::endl;
}

int main() {
    std::thread thread1(doSomething, 1);
    std::thread thread2(doSomething, 2);

    thread1.join();
    thread2.join();

    return 0;
}
```

> ¿Qué es un **Deadlock**? **Ejemplifique**.

> Explique el propísito y uso de la función `BIND`.

Fue pensada para asignarle un socket abierto a una dirección. El uso de la función es previo al de la función `accept` ya que la misma prepara al socket para poder escuchar conexiones. `bind` establece a qué interfaz, IP y puerto se quiere asociar al socket. La dirección usada en la función `bind` son el resultado de la función `getaddrinfo`.

> ¿Para qué sirve la función `htons`? ¿A qué se debe su existencia?

Transforma el orden de los bytes de un short recibido por parámetro del endianness usado por el host al endianness de la red (big endian). Su existencia se debe a que la comunicación debe funcionar entre máquinas de distinto tipo, con distinta arquitectura y diferentes endianness, permitiendo trabajar con una representación común. La función `htons` asegura que los números se almacenen en memoria en el orden de bytes de la red, con el más significativo primero.

> Explique el propósito del llamado a **bind** y **accept** en una aplicación servidor **TCP/IP**.

Bind fue pensada para asignarle a un socket abierto una dirección. El uso de la función es previo al uso de la función accept, prepara al socket para poder escuchar conexiones.
Luego de hacer bind e iniciar el socket con listen para escuchar conexiones, la llamada accept bloquea al hilo de ejecución actual hasta obtener una conexión entrante al socket, devolviendo un nuevo file descriptor socket con el que se puede invocar un send o receive.

> ¿Cuál es el uso de la función `listen`? ¿Qué parámetros tiene y para qué sirven?

El listen define cuántas conexiones en espera pueden esperar hasta ser aceptadas. No limita cuántas conexiones totales puede haber.
Indica que el servidor está listo para recibir peticiones marcando el socket como pasivo.

> ¿Puede la función `pthread_join` lockear algún hilo? Justifique.

La función `pthread_join` espera a que el hilo se detenga antes de realizar alguna acción. Si el objeto nunca fue detenido o se encuentra en alguna llamada bloqueante, puede generarle un lock al hilo que haya intentado sincronizar.

> Explique en qué situaciones es recomendable utilizar programación **multi-hilo** (**multithreading**) para realizar cierto procesamiento. ¿Existe algún caso donde utilizar multithreading sea perjudicial?

Las clases de sincronización se usan cuando se debe controlar el acceso a un recurso para garantizar la integridad del mismo. Las clases de acceso dee sincronización se usan para acceder a estos recursos controlados. El multithreadding permite a la CPU procesar varias tareas simultáneamente.
**Es perjudicial si sólo se tiene un núcleo de CPU sin bloqueo/espera en ningún subproceso**. Necesariamente hay una pérdida de tiempo de CPU para coordinar subprocesos múltiples. Dado que solo se puede ejecutar un subproceso, aunque todos podrían hacerlo (y por eso la condición de no bloqueo/no espera), el tiempo total es mayor.

## Ejercicios de Código

### Sockets

> Escribir un programa que reciba el puerto, escuche una conexión, reciba paquetes terminados en '\0' y envíe el largo del paquete recibido. Si recibe un paquete de menos de 10 caracteres debe finalizar el programa liberando recursos.

> Escriba un **programa** (desde la inicialización hasta la liberación de recursos) que **reciba pauetes de la forma nnn+nn+...+nnnn=** (números separados por +, seguidos de =) e **imprima el resultado de la suma de cada paquete** por pantalla. Al recibir un **paquete vacío ("=") debe cerrarse orenadamente**. No considere errores.

> Escriba un programa que reciba por **línea de comandos** un **Puerto** y una **IP**. El programa debe establecer una única conexión, quedar en escucha e **imprimir en stdout todo** lo recibido. Al recibir el texto 'FINAL' **debe finalizar** el programa **sin imprimir dicho texto**.

> Escriba un programa que reciba por **línea de comandos un Puerto y una IP**. El programa debe aceptar una **única conexión e imprimir en stdout la sumatoria de los enteros recibidos en cada paquete**. Un paquete está definido como una **sucesión de números recibidos como texto, en decimal, separados por comas y terminado con un signo igual** (ej, "27,12,32="). Al recibir el texto **'FIN' debe finalizar el programa ordenadamente** liberando los recursos.

> Escriba un programa que reciba por **línea de comandos** un **Puerto** y una **IP**. El programa debe aceptar una **única conexión** y recibir paquetes (**cada paquete inicia con '[' y finalza con ']'**). Para cada paquete recibido debe **imprimir el checksum** (sumatoria de bytes del paquete) del mismo, excepto que el **paquete esté vacío** ('[]'), en cuyo caso **debe finalizar**.

### Estructuras de Datos - Operadores

> Declarar una clase que contenga: atributos, accesibilidad, operadores +, ++, --, float, <<, >> y constructor move.

> Escriba el **.H de una biblioteca** de funciones **ISO C** para cadenas de caracteres. Incluya, al menos, 4 funciones.

> Escriba el **.H de una biblioteca** de funciones **ISO C** para números complejos. Incluya, al menos, 4 funciones.

> **Declare** una clase de elección libre. Incluya todos los **campos de datos** requeridos con su **correcta exposición/publicación**, y los operadores ++, -, ==, >> (carga), << (impresión), constructor move y operador float().

> **Declare la clase Número**, para encapsular una cadena numérica larga. Incluya al menos: Constructor(unsigned long), Constructor default y Constructor move; operador <<, (), =, long y ++(int). Implemente el operador >>.

> **Declare** una clase a elección considerando:
>
> - **Atributos** que son necesarios
> - **Accesibilidad** a la Clase
> - **Incluir** los operadores +, ++ (post-incremento), --(pre-incremento), >> (impresión), << (carga desde consola), long

> **Declare la clase TELEFONO** para encapsular una cadena numérica correspondiente a un teléfono. Incluya al menos: **Constructor(area, numero)**, **Constructor move** y constructor de **Copia**; **Operador <<, ==, =, long y >>**. Implemente el **operador >>**.

> **Declare** la clase IPv4 para almacenar una dirección IP. Incluya **constructor default, constructor move, constructor de copia**, y los siguientes operadores: **operator<<, operator==, operator= y operator+**.

### Manejo de Archivos

> Escribir un programa ISO C que procese "nros11.bin" sobre sí mismo. El procesamiento consiste en leer números big endian en base 11 de 3 símbolos y duplicar los múltiplos de 13.

> Escribir **un programa ISO C** que procese el archivo de **enteros de 3 bytes big endian cuyo nombre es recibido como parámetro**. El procesamiento consiste en **eliminar los números múltiplos de 3**, trabajando sobre el mismo archivo (sin archivos intermedios ni en memoria).

> Escribir **un programa ISO C** que procese el archivo "nros2bytes.dat" **sobre sí mismo, duplicando los enteros de 2 butes múltiplos de 3**.

> Escribir **un programa ISO C** que reciba por argumento el nombre de un archivo de texto y lo procese sobre sí mismo (sin crear archivos intermedios ni subiendo todo su contenido a memoria). El procesamiento consiste en **eliminar las líneas de 1 sola palabra**.

> Escribir **un programa C** que procese el archivo "numeros.txt" sobre sí mismo (sin crear archivos intermedios y sin subir el archivo a memoria). El procesamiento consiste en leer grupos de 4 caracteres hexadecimales y reemplazarlos por los correspondientes dígitos decimales (que representen el mismo número leído pero en decimal).

> Escriba una **función ISO C** que permita **procesar un archivo texto que contenga frases (1 por línea) sobre sí mismo, sin generar archivos intermedios ni cargar el archivo completo a memoria**. El procesamiento consiste en eliminar las palabras de más de 3 letras de cada línea.

> Escribir **un programa ISO C** que procese el archivo "nros_2bytes_bigendian.dat" **sobre sí mismo, eliminando los números múltiplos de 7**.

> Escribir **un programa C** que procese el archivo "numeros.txt" sobre sí mismo (sin crear archivos intermedios y sin subir el archivo a memoria). El procesamiento consiste en leer nros hexadecimales de 4 símbolos y reemplazarlos por su valor decimal (en texto).

> Escribir **un programa ISO C** que procese el archivo "valuesword.dat" **sobre sí mismo, eliminando los words (2 bytes) múltiplos de 16**.

> Escriba una **función ISO C** que permita **procesar un archivo texto sobre sí mismo**, que contenga **una palabra por línea**. El procesamiento consiste en **ordenar las palabras (líneas) alfabéticamente** considerando que el archivo **no entra en memoria**.

> Escribir **programa ISO C** que procese el archivo de **texto cuyo nombre es recibido como parámetro**. El procesamiento consiste en **leer oraciones y suprimir aquellas que tengan más de 3 palabras**. Asuma que el archivo no puede cargarse en memoria, pero una oración sí puede.

### Funciones C++

> Implemente una función **C++** denominada **DobleSiNo** que reciba dos listas de elementos y devuelva una nueva lista **duplicando los elementos de la primera que no están en la segunda**:
>
> ```cpp
> std::list<T> DobleSiNo(std::list<T> a, std::list<T> b);
> ```

> Implemente una función **C++** denominada **Sacar** que reciba dos listas de elementos y devuelva una nueva lista con los elementos de la primera que no están en la segunda:
>
> ```cpp
> std::list<T> Sacar(std::list<T> a, std::list<T> b);
> ```

> Escriba **una función ISO C** llamada ***Replicar*** que reciba 1 cadena (**S**), dos índices (**I1 e I2**) y una cantidad (**Q**). La función debe retornar una copia de S salvo los caracteres que se encuentran entre los índices I1 e I2, que serán duplicados Q veces.
> Ej, replicar("Hola", 1, 2, 3) retorna "Hololola".

> Escriba **un programa C** que tome 2 cadenas por línea de comandos: A y B; e imprima la cadena A después de haber duplicado **todas las ocurrencias de B**.
>
> Ej: reemp.exe "Este es el final" final ---> Este es el final final.

> Implemente una función **C++** denominada **DobleSegunda** que reciba dos listas de elementos y devuelva una nueva lista duplicando los elementos de la primera si están en la segunda:
>
> ```cpp
> std::list<T> DobleSegunda(std::list<T> a, std::list<T> b);
> ```

> **Implemente** la función **`void ValorHex(char *hex, int *ent)`** que interprete la cadena **hex** (de símbolos hexadecimales) y guarde el valor correspondiente en el entero indicado por **ent**.

> Implemente una función C++ denominada **Interseccion** que reciba dos listas de elementos y devuelva una nueva lista con los elementos que se encuentran en ambas listas:
>
> `std::list<T> Interseccion(std::list<T> a, std::list<T> b);`

> Escriba un programa (desde la inicialización hasta la liberación de recursos) que reciba **paquetes de texto delimitados por corchetes angulares ("<...>") y los imprima completos por pantalla**. Al recibir un paquete vacío ("<>") debe cerrarse ordenadamente. No considere errores.

> Implemente una función C++ denominada **Suprimir** que reciba dos listas de elementos y devuelva una nueva lista con elementos de la primera que no están en la segunda:

```cpp
std::list<T> Suprimir(std::list<T> a, std::list<T> b);
```

### Threads

> Escriba un programa que imprima por salida estándar los números entre 1 y 100, **en orden ascendente**. Se pide que los números sean **contabilizados por una variable global única** y que los **pares sean escritos por un hilo** mientras que los **impares sean escritos por otro**. **Contemple la correcta sincronización** entre hilos y la liberación de los recursos utilizados.

### Librerías gráficas

> Escriba una rutina que dibuje las dos diagonales de la pantalla en color rojo.

> **Escriba una rutina** (para ambiente gráfico Windows o Linux) que dibuje un **triángulo amarillo** del tamaño de la ventana.
