# Aprendiendo JavaScript

- [Aprendiendo JavaScript](#aprendiendo-javascript)
  - [Variables](#variables)
  - [Pedir datos](#pedir-datos)
  - [Operadores](#operadores)
  - [Operadores logicos](#operadores-logicos)
  - [Concatenacion](#concatenacion)
  - [Condicionales](#condicionales)
  - [Arrays (arreglos) / Listas](#arrays-arreglos--listas)
  - [Arrays asociativo / Diccionario](#arrays-asociativo--diccionario)
  - [Bucles](#bucles)
    - [**While**](#while)
    - [**For**](#for)
    - [**Break, continue y label**](#break-continue-y-label)
  - [Funciones](#funciones)
    - [**Funciones flecha**](#funciones-flecha)
  - [Programacion Orientada a Objetos (POO)](#programacion-orientada-a-objetos-poo)
    - [**Caracteristicas**](#caracteristicas)
    - [**Declaracion**](#declaracion)
    - [**Herencia y static method**](#herencia-y-static-method)
    - [**Setter y getter**](#setter-y-getter)
  - [Metodos de string](#metodos-de-string)
  - [Metodos de array](#metodos-de-array)
  - [Objeto Math](#objeto-math)
  - [Consola](#consola)
  - [DOM (Document Object Model)](#dom-document-object-model)
    - [**Metodos de seleccion de elementos**](#metodos-de-seleccion-de-elementos)
    - [**Definir, Obtener y Eliminar valores de atributos**](#definir-obtener-y-eliminar-valores-de-atributos)
    - [**Atributos globales**](#atributos-globales)
    - [*Atributos de los inputs*](#atributos-de-los-inputs)
    - [*Atributo style*](#atributo-style)
    - [**Clases, classList y sus metodos**](#clases-classlist-y-sus-metodos)
    - [**Obtencion y Modificacion de elementos**](#obtencion-y-modificacion-de-elementos)
    - [**Creacion de elementos**](#creacion-de-elementos)
    - [**Obtencion y Modificacion de childs**](#obtencion-y-modificacion-de-childs)
    - [**Metodos de childs**](#metodos-de-childs)
    - [**Selectores de padres**](#selectores-de-padres)
    - [**Selectores de Sibling**](#selectores-de-sibling)
    - [Otro selector](#otro-selector)


## Variables
--------------------------------------------------------

existen varios tipos de variables entre los cuales estan:

|   tipo    | Descripcion                    | Ejemplo                  |
| :-------: | ------------------------------ | ------------------------ |
|  string   | Cadena de caracteres           | "Hola mundo"             |
|  number   | Numero                         | 1, 2, 3                  |
|   bool    | Verdadero o falso              | `true`, `false`          |
| undefined | Variable que no se ha definido | `undefined`              |
|   null    | Se iicializa como nula         | `null`                   |
|    nan    | No es un numero                | `var = "x" * 1` => `NaN` |

Existen 3 tipos de declaracion de variable estos son:

* let
    
    Que es de acceso local y no se puede acceder a ella fuera de su bloque
* var

    Que es de acceso global por ende genera mas consumo en la memoria
* const

    de acceso global pero no puede ser editada, es constante

Podemos declarar una variable y despues inicializarla como:

```javascript
let numero
numero = 7
```

Tambiem podemos declarar muchas variables al mismo tiempo asi:

```javascript
let n1, n2, n3
```

<br>

## Pedir datos
--------------------------------------------------------

Solicita datos por medio de una alerta arriba del navegador con:

```javascript
prompt(`¿Cuanto dinero tienes?`)
```

> Para pasar un string a number se utiliza `parseInt()`

<br>

## Operadores
--------------------------------------------------------

| Nombres                                  | Abreviacion |
| ---------------------------------------- | :---------: |
| Asignacion                               |   `x = y`   |
| Adicion                                  |  `x += y`   |
| Sustraccion                              |  `x -= y`   |
| Multiplicacion                           |  `x *= y`   |
| Divivion                                 |  `x /= y`   |
| Resto                                    |  `x %= y`   |
| Exponenciacion                           |  `x **= y`  |
| Desplazaciento a la derecha              |  `x >>= y`  |
| Desplazaciento a la izquierda            |  `x <<= y`  |
| Sin signo de desplazaciento a la derecha | `x >>>= y`  |
| AND                                      |  `x &= y`   |
| XOR                                      |  `x ^= y`   |
| OR                                       |  `x \|= y`  |

## Operadores logicos
--------------------------------------------------------

***Comparadores Logicos***
| Nombre         | Escritura |
| -------------- | :-------: |
| Igualdad       |   `==`    |
| Desigualdad    |   `!=`    |
| Idenicisdad    |   `===`   |
| Desidenticidad |   `!==`   |
| Mayor que      |    `>`    |
| Menor que      |    `<`    |
| Mayor o igual  |   `>=`    |
| Menor o igual  |   `<=`    |


***Operadores Logicos***
| Nombre | Escritura |
| ------ | :-------: |
| AND    |   `&&`    |
| OR     |  `\|\|`   |
| NOT    |    `!`    |

## Concatenacion
--------------------------------------------------------

Hay diversas maneras de concatenar textos y/o umeros, vamos a ver algunas de ellas:

```javascript
let usuario = 'Mauricio' 
document.write('Hola' + usuario + '!')
```

Esta nos devolveria el resultado de `Hola Mauricio!`, pero resulta una manera algo vervosa de hacer y ademas podriamos teer errores de concatenacion dependiendo el tipo de variable que tengamos.

La mas recomendada es la siguiente, en ella utilizamos el signo de \` para rodear la string de codigo y colocamos as variables que querramos concatenar entre las llaves en `${}`.

```javascript
let usuario = 'Mauricio' 
document.write(`Hola ${usuario}!`)
```

Esta es ya una forma mucho mas comoda y entendible de lo que estamos haciendo.

## Condicionales
--------------------------------------------------------

Para evaluar condiciones se utiliza la palabra clave `if`, si hay que evaluar mas de una condicion y hay que ahorrar cpu se utiliza `else if`, ejemplos de esto son:

```javascript
if (condicion) {
    algo
} else if (condicion2) {
    algo
}
```

Un ejemplo usando los operadores logicos:

```JavaScript
if (!(var == var2) && (var3 || var4)) {
    algo
}
```

## Arrays (arreglos) / Listas
--------------------------------------------------------

Las listas guardan conjuntos de elemntos o items a los que podemos crear, leer, actualizar y borrar.

Estas se declaran de la siguiente manera:

```Javascript
let arr = [item, item2, item3]
document.write(arr[0])
```

## Arrays asociativo / Diccionario
--------------------------------------------------------

A este se le pasa una llave para acceder a sus elementos, asi:

```javascript
let arraso = {
    'name':     'Mauricio',
    'lastname': 'Martínez',
    'edad':     18
}

document.write(arraso['name'])
```

## Bucles
--------------------------------------------------------

### **While**

Trozos de codigo que se ejecutan mientras su condicion sea verdadera

Ejemplo:

```Javascript
while (Condicion) {
    algo
}
```

Hay dos tipos de while, el otro seria el `do while`, este ejecuta primero el trozo de codigo y luego evalua la condicion, ejemplo:

```javascript
do {
    algo
} while (condicion)
```

### **For**

El bucle for recorre cualquier iterable, hay 3 tipos de for el for normal, for in y for of, vamos a explicar:

```javascript
for (let i = 0; i < 5; i++) {
    document.write(i)
}

let i = 6
for (i; i > 0; i--) {
    document.write(i)
}
```

Primero declaramos la variable que vamos a usar, luego ponemos la condicion que evaluaremos y por ultimo el aumento o decremento de la variable para que esta cumpla el condicional. 

```javascript
let n = ['uno', 'dos', 'tres']
for (let i in n) {
    document.write(i)
}
```

Este for nos devuelve la posicion de este elemento, entonces este for nos devuelve `012`.

```javascript
let n = ['uno', 'dos', 'tres']
for (let i of n) {
    document.write(i)
}
```
Este for nos devulve el elemento en que se encuentra recorriendo en el momento, lo que nos devolveria seria `unodostres`.

<br>

### **Break, continue y label**

Para ambos podemos cortar o continuar la siguiente teracion del bucle, con `break` y `continue` si ponemos break en un trozo de nuestro codigo el bucle se cortara por completo, en cambio con el continue este pasa a la siguiente vuelta, pero ya no ejecuta lo que este por debajo de el.

Existen los *label* que es una forma de nombrar trozos de codigo, si podemos hacer cosas directamente con ellos, para ello simplemente lo nombramos en la linea anterior de la declaracion del ciclo seguido de dos puntos.

Por ejemplo:

```javascript
let str = `Hello`

father:
for (let i = 0; i < 10; i++) {
    for (let char of str) {
        document.write(char)
        if (char == 'l') {
            break father
        }
    }
}
```

## Funciones
--------------------------------------------------------

Las funciones es una forma de llamar a un trozo de codigo que se ejecuta cada vez que lo llamamos, por la manera en que lo definimos, ellos nos evitan ser repetitivos y a ser mas mantenible nuestro codigo, y hace que ovedescamos el principio.

> Dont repeat your self. 

Una forma de declarar una funcion en javascript seria:

```javascript
function hello() {
    document.write('Hello')
}

hello()
```

Utilizamos la palabra clave `function`, pero esto no es una funcion si esta no devuelve un resultado, para ello utilizamos la palabra clave `return`, lo que haya despues del return no se ejecutara, este funciona como un `break`.

```javascript
function hello() {
    return `Hello`
}

document.write(hello())
```

Ya con esto nos permite tener mas juego con el uso de ellos.

Tambien una funcion no es una funcion si a esta no le podemos pasar parametros, estos se colocan dentro de los parentesis cuando declaramos la funcion. y nombramos a esas variables como nosotros deseamos, ejemplo:

```javascript
function sumar(n1, n2) {
    return n1 + n2
}

document.write(sumar(20, 30))
```

O tambien:

```javascript
const sumar = function(n1, n2) {
    return n1 + n2
}

document.write(sumar(20, 30))
```

<br>

### **Funciones flecha**

Una forma mas rapida de como delcarar funciones.

```javascript
const print = (text) => {
    document.write(text)
}
print('Hi')
```

Nombramos la funcion que va a ser constante, y luego ponemos entre parentesis los parametros y luego el bloque de codigo.

Esta funcion se puede abreviar mas si solo le vamos a padar un parametro y ademas podemos escribir todo en una linea, de esta manera:

```javascript
const print = text => document.write(text)
print('Hi')
```

## Programacion Orientada a Objetos (POO)
------------------------------------------------------------

### **Caracteristicas**

La poo nos permite ahorrarnos el trabajo de estra creando codigo cada vez que querramos crear una cosa, y es mas facil de mantener nuestro codigo.

***Abstraccion:*** Se crea una clase lo mas simple que se pueda, no vamos a poner cada caracteristica del objeto.

***Modularidad:*** Separamos el problemas y vamos reduciendo uno a uno, hasta resolverlos todos.

***Encapsulamiento:*** Maneraen la que cualquier persona no pueda acceder a toda la informacion.

***Polimorfismo:*** Capacidad que tiene  un objeto de comportarse de maneraa distinta  por sus propiedades.

### **Declaracion**

En javascript se hace asi:

```javascript
// Declaracion de clase
class animal { // Nombramos la clase
    constructor(especie, color, edad) {
        this.especie = especie
        this.color = color
        this.edad = edad
        this.info =  `Soy un/a ${especie} de color ${color} y tengo ${edad} años`
    }
}

// Instanciacion de clase 
const perro = new animal('perro', 'negro', 3)
```

*Objeto*: Es la clase instanciada, ya con informacion, el objeto puede tener ***atributos y metodos***, los atributos son las variables unicas del objeto, mientras que los metodos son finciones pero dentro del objeto.

`constructor` es una funcion reservada para ejecutarse al instanciar el objeto, asi este pasa a tener unos valores por defecto.

*Instanciacion*: Cuando se crea un nuevo elemento a partir de la clase, se le llama instanciar.

Para instanciar la clase se necesita declararla como constante, para que esta consuma menos recursos.

Para hacer metodos simpleem

### **Herencia y static method**

Crear una clase que hereda todos sus metodos de su padre y los tributos que asignemos; a este le podemos añadir nuevos metodos y atributos.

Se hace de la siguiente manera (continuando lo anterior):

```javascript
class Perro extends Animal {
    constructor(especie, edad, color, info, raza) {
        super(especie, edad, color, info);
        this.raza = raza;
    }
    static ladrar() {
        alert('guau')
    }
}
```

El metodo static solo depende de los argumentos que se le brinden, no de las variables de la clase y esta se puede ejecutar sin instanciar el objeto.

Un ejemplo mas claro:

```javascript
class Math{
    static ABS(n) {
        if (n > 0) {
            return n
        }  else {
            return -n
        }
    }
}

document.write(Math.ABS(23))
```

### **Setter y getter**

```javascript
class Animal {
    constructor(especie, edad, color) {
        this.especie = especie;
        this.edad = edad;
        this.color = color;
        this.info = `Soy ${this.especie}, tengo ${this.edad} años, y soy de color ${this.color}`;
    }
    get getInfo() {
        return this.info + '<br>'
    }
    set setEdad (newAge){
        this.edad = newAge;
    }
}
```

Esto se utiliza para setear una variable del objeto en lugar de escribir `perro.cambiarRaza('newRaza')` pasamos a escribir:

`perro.setRaza = 'newRaza'`

Y para get es mas facil, ya que esta nos devuelve directamente lo que buscamos y simplemente tenemos que escribir:

`perro.getInfo`

Esto en lugar de `perro.getInfo()` 

> Siempre se utilizaran los prefijos set y get dependiendo de lo que sea, esto para facilitar la interpretacion

<br>

## Metodos de string
---

Siempre con el prefijo de *string.*:

|       Metodo       | Descripcion                                                          |
| :----------------: | -------------------------------------------------------------------- |
|   `concat({x})`    | Para unir cadenas                                                    |
|  `starsWith({x})`  | Devielve bool para validar si inicia con {x}                         |
|   `endWith({x})`   | Devielve bool para validar si termina con {x}                        |
|  `includes({x})`   | Si contiene {x} devuelve true                                        |
|   `indexOf({x})`   | Devuelve la primera posicion de {x} si esta no existe devuelve -1    |
| `lastIndexOf({x})` | Devuelve la ultima posicion de {x} si esta no existe devuelve -1     |
| `padStart(n, {x})` | Rellena el inicio de la string con {x} hasta que tenga un largo de n |
|  `padEnd(n, {x})`  | Rellena el final de la string con {x} hasta que tenga un largo de n  |
|    `repeat(n)`     | Repite n veces la string                                             |

**Transformar cadenas**

|       Metodo       | Descripcion                                                      |
| :----------------: | ---------------------------------------------------------------- |
|    `split({x})`    | Divide la cadena por cada {x} que haya (devulve array)           |
| `substring(n, n2)` | Crea una string desde n hasta n2 sin contar n2                   |
|  `toLowerCase()`   | Combierte la string a minuscula                                  |
|  `toUpperCase()`   | Combierte la string a mayuscula                                  |
|    `toString()`    | Combierte number, array, etc a string                            |
|     `length()`     | Obtener el largo de una string                                   |
|      `trim()`      | Elimina los espacios en blanco antes y despues de los caracteres |
|    `trimEnd()`     | Elimina los espacios del final                                   |
|   `trimStart()`    | Elimina los espacios del inicio                                  |

<br>

## Metodos de array
---

Siempre con el prefijo de *array.*:

|          Metodo           | Descripcion                                                                                                                                                                                                    |
| :-----------------------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|          `pop()`          | Elimina el ultimo elemento del array y retorna el elemento eliminado                                                                                                                                           |
|         `shift()`         | Elimina el primer elemento del array y retorna el eliminado                                                                                                                                                    |
|        `unshift()`        | Agrega elemento al inicio del array                                                                                                                                                                            |
|     `push({x}, ...)`      | Agrega un elemento/s al final del array y devuelve el length                                                                                                                                                   |
|        `reverse()`        | Invierte el orden de los elementos                                                                                                                                                                             |
|         `sort()`          | Ordena el array                                                                                                                                                                                                |
| `splice(n, n2, {x}, ...)` | Funcion principal es reemplazar o añadir elementos  en una posicion especifica \| n = Posicion start (0 inicio, -1 final), n2 = Cantidad de elementos a reemplazar/eliminar, {x} = elementos a añador en pos n |
|        `join({x})`        | Retorna una string separado cada elemento por {x}                                                                                                                                                              |
|      `slice(n, n2)`       | Retora un array de n hasta n2, si es n2 = -1, devuelve todo menos el ultimo, n2 = undefined, selecciona todo                                                                                                   |
|      `includes({x})`      | Si contiene {x} devuelve true                                                                                                                                                                                  |
|      `indexOf({x})`       | Devuelve la primera posicion de {x} si esta no existe devuelve -1                                                                                                                                              |
|    `lastIndexOf({x})`     | Devuelve la ultima posicion de {x} si esta no existe devuelve -1                                                                                                                                               |
|       `toString()`        | Combierte number, array, etc a string                                                                                                                                                                          |

<br><br>

**filter** 

La sintaxis de un forEach es:<br>
`array.forEach(funcion(elemento, index, arr), thisValue)`

Recorre cada item del array y si colocamos un return este luego nos devolvera un array de elementos que se hayan devuelto.

Ejemplos:
```javascript
let arr = [11, 22, 13, 17]

let mayoresDeEdad = arr.filter(edad => return edad >= 18)
console.log(mayoresDeEdad)
```

**forEach**

ForEach es casi igual a filter en su sintaxis, solo que este no devulve nada.

> Todos los filter anteriores puden ser sustituidos por .forEach

La sintaxis de un forEach es:<br>
`array.forEach(funcion(elemento, index, arr), thisValue)`


```javascript
const arr = [1,2,4]
arr.forEach( ( item, i ) => {
  arr[i] += 2
})
```

En conclusion forEach es mas rapido que filter, pero filter es mas completo (falta map, que es mas rapido que forEach)

<br>

## Objeto Math
---

> Siempre con el prefix de *Math.*

|    Metodo     | Descripcion                                               |
| :-----------: | --------------------------------------------------------- |
|   `sqrt(n)`   | Raiz cuadrada de n                                        |
|   `cbrt(n)`   | Raiz cubica de n                                          |
| `max(n, ...)` | Retorna el n maximo, no recibe listas                     |
| `min(n, ...)` | Retorna el n minimo, no recibe listas                     |
|  `random()`   | devuelve un numero pseudo-aleatorio entre 0 y 1           |
|  `round(n)`   | Redondea n                                                |
|  `fround(n)`  | Redondea n a un float aproximado mas corto (15 decimales) |
|  `floor(n)`   | Redondea hacia el numero entero mas bajo (-3.4 = -4)      |
|  `trunc(n)`   | Elimina los decimales  (-3.4 = -3)                        |
|     `PI`      | El valor de Pi (15 decimales)                             |
|   `SQRT1_2`   | Raiz cuadrada de 1/2 (15 decimales)                       |
|    `SQRT2`    | Raiz cuadrada de 2 (15 decimales)                         |
|      `E`      | Constante de euler (15 decimales)                         |
|     `LN2`     | Logaritmo natural de 2                                    |
|    `LN10`     | Logaritmo natural de 10                                   |
|    `LOG2E`    | Logaritmo base 2 de euler                                 |
|   `LOG10E`    | Logaritmo base 10 de euler                                |

<br>

## Consola
---

Una de las apis (objetos) que podemos usar

|        Metodo         | Descripcion                                                               |
| :-------------------: | ------------------------------------------------------------------------- |
|  `assert(condition)`  | Nos dice si la condicion que le pasemos es asertada (no se usa)           |
|       `clear()`       | Se limpia la consola                                                      |
|     `error({x})`      | Muestra x como un error en la consola                                     |
|      `info({x})`      | Es muy parecida a log "roporciona info"                                   |
|      `log({x})`       | Muestra un mensaje de depuracion                                          |
|    `table({arr})`     | Muestra una tabla en consola con el index y value                         |
|      `warn({x})`      | Muestra una advertencia x                                                 |
|      `dir({x})`       | Muestra los metodos del objeto que le pasemos  y nos muestra su contenido |
|       `count()`       | Cuenta las veces que pasa algo                                            |
|    `countReset()`     | resetea lacuena de count                                                  |
|     `group({x})`      | Crea una lista colapsable de nombre x                                     |
|     `groupEnd()`      | Salir del grupo                                                           |
| `groupCollapsed({x})` | Crea un grupo de nombre x colapsado                                       |
|       `time()`        | Inicia un temporizador                                                    |
|      `timeLog()`      | Nos dice cuanto paso desde que se ejecuto time                            |
|      `timeEnd()`      | Termina la cuenta                                                         |

<br>

## DOM (Document Object Model)
---

DOM es la raiz de todo el documento, el cual tiene como hijo la etiqyeta html, de esta salen 2, head y body, y a partir de estas todo nuestro sitio web (Cada hijo se le llama nodo).

*document* es el nodo raiz.
*element* Nodos definidos por etiquetas html.
*text* El text node es el contenido de un element node. (el text dentro de h1)
*Attribute* Los atributo los veremos como informacion asociada a los element node
*comment & others* 

### **Metodos de seleccion de elementos**

> Siempre con el prefix de *document.*
>
> Todo lo que seleccionamos son objetos

* *`getElementById({x})`*:
  
  Seleccionar un elemento por su id x

* *`getElementsByTagName({x})`*:
  
Devulve todos los elementos de tag x

* *`querySelector({x})`*:
  
  Selecciona el primer elemento que coincida con el css selector 

* *`querySelectorAll({x})`*:
  
  Selecciona todos los elementos con el selector css x

### **Definir, Obtener y Eliminar valores de atributos**

> Esto es cuando ya tenemos seleccionado un alemento
> `let elem = document.getElementById('elem')`
> entonces usaremos el prefijo *elem.*

* *`setAttribute({attr}, {x})`*:
  
  Crear/Modificar el valor de attr siempre y cuando sea un attr valido, y x el valor (puede ser lo que sea)

* *`getAttribute({x})`*:
  
  Obtenemos el valor del atributo x

* *`removeAttribute({x})`*:

  Removemos el atributo x del elemento

### **Atributos globales**

> Usaremos el prefijo de *element.setAttribute({attr}, {val})*

| Atributos (attr) | valor  (val) | Descripcion                                                                |
| :--------------: | :----------: | -------------------------------------------------------------------------- |
| contentEditable  | true o false | Podemos editar el contenido como un input text                             |
|       dir        |  ltr o rtl   | Direccion hacia donde va el texto                                          |
|      hidden      |              | Si esta definida oculta el texto                                           |
|      style       | valores css  | Setear valores a css                                                       |
|     tabindex     |      n       | Seleccionar con tab elementos a los que se les asigno (preferible en html) |
|      title       |     text     | Titulo que aparece cuando tenemos el cursor subre el elemento              |

*tabindex*: Este se setea como atributo en diferentes etiquetas html, del 0 al infinito, cada vez que presionemos tab ira al siguiente numero

### *Atributos de los inputs*

> El prefix sera input.

|    Metodo     | Descripcion                                               |
| :-----------: | --------------------------------------------------------- |
|  `className`  | Retorna/modifica el valor de de la clase                  |
|    `value`    | Retorna/modifica el valor del input (text, n, color)      |
|    `type`     | Retorna/modifica el type                                  |
|   `accept`    | Setear el tipo de cosa que acepta, (image/gif, image/png) |
|    `form`     | Dar el id de un formulario para conectarlo                |
|  `minLength`  | Setear el minimo de caracteres o valor para Fenviar       |
| `placeholder` | Setear un placeholder (texto de ejemplo en text)          |
|  `required`   | Poner un compo como requerido                             |

### *Atributo style*

> Prefix *element.style.*
> (Mismos estilos css pero en Camel Case)

|     Metodo      | Descripcion                  |
| :-------------: | ---------------------------- |
|      color      | Setear el color del texto    |
| backgroundColor | Setear el valor del bg       |
|     padding     | setear el tamaño del padding |

### **Clases, classList y sus metodos**

> Esto despues de haber seleccionado un elemento
> Prefix *element.classList.*

|       Metodos       | Descripcion                                                   |
| :-----------------: | ------------------------------------------------------------- |
|     `add({x})`      | Añadir la clase x al elemento                                 |
|    `remove({x})`    | Remueve la clase x                                            |
|     `item({n})`     | Devuelve la clase en posicion n                               |
|   `contains({x})`   | Devuelve true o false si tiene la clase x                     |
|    `toggle({x})`    | Si tiene la clase x la elimina, si no se la añade             |
| `replace({x}, {y})` | reemplaza la clase x por y y devulve true, si no existe false |

> *toggle* devuelve el valor true o false, si se añadio la clase devuelve true y si se borro devuelve false

### **Obtencion y Modificacion de elementos**

> Prefix 
> *element.*

|   Metodos   | Descripcion                                                                                         |
| :---------: | --------------------------------------------------------------------------------------------------- |
| textContent | Devuelve/Modifica TODO texto entre la etiqueta sin devolver html                                    |
|  innerHTML  | Devuelve/Modifica TODO texto entre la etiqueta devolviendo el html y estilos                        |
|  outerHTML  | Devuelve/Modifica TODO texto entre la etiqueta devolviendo el html y estilos incluyendo la etiqueta |

### **Creacion de elementos**

> Prefix *document.*

* `createElement({x})`
  
  Para crear etiquetas html, x es la etiqueta y tenemos que especificar la con mayus (LI, DIV, etc)

```javascript
const contenedor = document.querySelector('.contenedor')

const item = document.createElement('B') // Colocar los elementos en mayus
const text = document.createTextNode('Esto en negrita')

item.appendChild(text) // Metodo para añadir hijos
contenedor.appendChild(item)
```

O tambien esto se podria simplificar con:

```javascript
const contenedor = document.querySelector('.contenedor')

const item = document.createElement('B') // Colocar los elementos en mayus

item.innerHTML = 'Esto en negrita' 

contenedor.appendChild(item)
```

Todos los elemetos que creamos son unicos y estos no se pueden añadir 2 veces al mismo nodo.

Si hacemos un for para que cree multiples elementos es desastrozo ya que al crear un nuevo elemento el navegador al crear algo borra todo y lo vuelve a crear consumiendo muchos recursos en el proceso.

> Gracias a este error aparecio la siguiente funcion:

* `createDocumentFragment()`
  
  Con esto podemos añadir multiples cosas sin afectar la carga y consumo, y lugo de haber hecho todos nuestros desastres, lo añadimos a nuestro elemento seleccionado. (Lo consideraria un elemento "Oculto" que despues integramos)

```javascript
const contenedor = document.querySelector('.contenedor')
const fragmento = document.createDocumentFragment()

for (let i = 0; i < 20; i++) {
    const item = document.createElement('B') 
    item.innerHTML = 'Esto en negrita' 
    fragmento.appendChild(item)
}
contenedor.appendChild(fragmento)
```

### **Obtencion y Modificacion de childs**

> Prefix *contenedor.*
> Esto cuando tenemos seleccionado un elemento

* `firstChild` y `lastChild`
  
  para obtener el primer o ultimo hijo correspondientemente, si el primer elemento esta con identacion el primer hijo seran los espacios que hay entre el padre e primer elemento.

```javascript
const contenedor = document.querySelector('.contenedor')

const child = contenedor.firstChild

console.log(child) // #text
```

* `firstElementChild` y `lastElementChild`

Para evitar estar modificando el HTML y nos devuelva el primer o ultimo hijo elemento correspondiente.

```javascript
const contenedor = document.querySelector('.contenedor')

const child = contenedor.firstElementChild

console.log(child) // <h1>titulo</h1>
```

* `childNodes`

Nos devuelve un objeto que podemmos recorrer como un array pero no es un array, este contiene todos los nodos que contiene el padre.

* `children`

Con este nos devuelve todos los elementos (etiquetas) contenidos. (Este no se puede recorrer con forEach como el pasado) Este se recorre con un forIn o mejor un forOf.

```javascript
const contenedor = document.querySelector('.contenedor')

const hijos = contenedor.children

for (const hijo of hijos) {
    console.log(hijo)
}
```

### **Metodos de childs**

> Prefix *contenedor.*

* `replaceChild({new}, {old})`
  
  Para reemplazar un hijo en especifico por uno nuevo

```javascript
const contenedor = document.querySelector('.contenedor')

const viejoTitulo = contenedor.firstElementChild
const nuevoTitulo = document.createElement('H1')
nuevoTitulo.innerHTML = 'Nuevo Titulo'

contenedor.replaceChild(nuevoTitulo, viejoTitulo)
```

* `removeChild({x})`
  
  Para eliminar un hijo x

```javascript
const contenedor = document.querySelector('.contenedor')

const titulo = contenedor.firstElementChild
contenedor.removeChild(titulo)
```

* `hasChildNodes()`
  
  Devuelve true o false dependiendo si tiene nodos hijos o no (El texto cuenta).

### **Selectores de padres**

> Prefix *`elemento.`* 

* `parentElement`
  
  Para seleccinar el elemento padre del elemento seleccionado.

* `parentNode`
  
  Seleccionar el nodo padre del elemento seleccionado

### **Selectores de Sibling**

> Prefix *element.*

* `nextSibling` y `previousSibling`

  Selecciona al siguiente o previo nodo hermano

*  `nextElementSibling` y `previousElementSibling`

  Selecciona al siguiente o previo elemento hermano

### Otro selector

`element.closest({selector})`

Este selecciona al elemento ascendente que cumpla con el *selector* css mas cercano. 

