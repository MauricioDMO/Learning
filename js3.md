- [JS Level Master](#js-level-master)
  - [Prototipos](#prototipos)
  - [Modo estricto ("use strict")](#modo-estricto-use-strict)
    - [Trabajando propiedades de objetos](#trabajando-propiedades-de-objetos)
    - [Otras propiedades.](#otras-propiedades)
  - [Funciones flechas 2.](#funciones-flechas-2)
    - [This](#this)
  - [Recursividad](#recursividad)
  - [Clausuras o closures](#clausuras-o-closures)
  - [Parametro Rest](#parametro-rest)
  - [Desestructuracion](#desestructuracion)
  - [Ternarias](#ternarias)
  - [Spread](#spread)
  - [Objeto Date](#objeto-date)
  - [Guardar datos en el navegador](#guardar-datos-en-el-navegador)
    - [LocalStorage](#localstorage)
    - [SessionStorage](#sessionstorage)
  - [Drag \& Drop](#drag--drop)
    - [DataTransfer](#datatransfer)
  - [Geolocalizacion](#geolocalizacion)
  - [Historial](#historial)
  - [FileReader](#filereader)

# JS Level Master

En este capitulo se aprendera el consumo de APIs en js.

<br>

## Prototipos

---

Todos los objetos de JS tienen un prototipo padre, podemos a acceder a el con el atributo `.__proto__` todos estos tienen un prototipo el cual es el prototipo de objeto, luego heredan otro prototipo diferente dependiendo del dato tienen un prototipo diferente como: string, number, objec.

todos heredan 2 prototipos, a esto se le llama prototype Chain "Cadena de prototipos", que es que nuestra variable tiene como padre la clase a la que pertenescan, ya sea string number o demas, luego estas antes heredaron el prototipo de object.

Para acceder a los prototipos ya creados usamos el atributo `__proto__` y para los que nosotros creamos (digamos una funcion) usamos el atributo `prototype`.

_Caracteristicas_

Cuando nosotros creamos un prototipo este es mutable.
Tienen existencia en la memoria.
Puede ser llamado y modificarlo.
El modelo ejemplar de una familia es el prototipo object.
Un objeto ehereda propiedades (valores y metodos) de su prototipo.

<br>

**Como trabajar con prototipos?**

Seleccionamos el elemento al cual le queremos modificar el prototipo y hacemos lo siguiente.

```javascript
class Objeto {
  hablar() {
    console.log("hola");
  }
}

let arr = [];
arr.__proto__ = new Objeto();

arr.hablar();
```

Asi sobreescribiria el proto del array.

<br>

## Modo estricto ("use strict")

---

**Que es lo que hace?**

-   Convierte los errores en excepcione, nos falta escribir el tipo de alcance de la variable pues esto se convierte en un error.

-   Consigue mejores tiempos de ejecucion ya que no se da el trabajo de entender nuestro codigo.

-   Evitas la sintaxis anterior a ES6

-   No permmite que el programador realize una "sintaxis mala"

**Como usamos el modo estricto?**

Tiene que ponerse la string: `"use strict"` al comienzo del bloque en ejecucion.

Si por error no declaramos el tipo de la variable esta nos dara un error y nos dira que usemos var, let o const.

### Trabajando propiedades de objetos

> Estaremos trabajando con el objeto `Object`

**Definir una propiedad de un objeto** <br>

Metodo `defineProperty()`

Si le ponemos en los valores `writeable: false` esto hara que no podamos sobreescribir el valor inicial.

```javascript
"use strict";

const obj = {};
Object.defineProperty(obj, "nombre", { value: "Mario", writeable: false });
console.log(obj.nombre);
```

**Prevenir extensiones de propiedades** <br>

Metodo `preventExtensions()`

Evita añadir nuevas propiedades al objeto al que lo apliquemos.

```javascript
"use strict";

const obj = { nombre: "Mario" };
Object.preventExtensions(obj);

console.log(obj);
```

### Otras propiedades.

**Nuevas propiedades a un string** <br>

Por defecto no se puede añador propiedades a las strings, pero si lo tratamos de hacer no nos da ni un error, en cambio con `"use strict"` esto no sucede.

```javascript
"use strict";

let str = "Hola";
str.continuacion = "Como estas?";
```

**Parametros duplicados** <br>

Evita que a la hora de crear una funcion esta le coloquemos parametros duplicados, de normal agarra el ultimo parametro definido y el anterior lo deja como `undefined`.

```javascript
"use strict";

function saludar(text, text) {
    console.log(text);
}
```

**Eliminar variables** <br>

No se nos permite eliminar variables lo unico que podemos eliminar propiedades de un objeto.

```javascript
"use strict";

const obj = { nombre: "Mario" };

delete obj.nombre;

console.log(obj.nombre);
```

**Cambia el comportamiento de palabras reservadas** <br>

Elimina la palabras reservadas `new`, `this` y `with`.

`Arguments` y `Eval` no pueden ser variables.

**Podemos usar "use strict" en funciones** <br>

De este modo solamente usamos el modo estricto en un solo bloque de codigo.

```javascript
nombre = "Mario";

function decir() {
    "use strict";
    console.log(nombre);
}

decir();
```

<br>

## Funciones flechas 2.

---

**Nuevas propedades** <br>

- Si solamente hay una instruccion la retornan automaticamente.
- Si solo hay un parametro no son necesarios los parentesis.
- No son adecuadas para definir metodos.

El `this` dentro de las funciones flechas hace referencia la objeto que la llama.

- No son recomendadas como constructores. 
- 

```javascript
const nombre = nombre => nombre

console.log(nombre("Mario"))
```

### This

`this` si se utiliza fuera de cualquier funcion este hace referencia al objeto `window`.

Si a this no lo contiene un objeto este hace referencia a `window` pero si este lo contiene un objeto hace referencia a un propio atributo del objeto que lo contiene.

```javascript
"use strict"

var nombre = "Mario"

function saludar() {
    console.log(`Hola ${this.nombre}`);
}

const persona = {
    nombre: "Mauricio",
    saludar: saludar
}

persona.saludar()
saludar()

```

Se puede resumir la asignacion de propiedades en los objetos si estas tienen el mismo nombre que una variable simplemente poniendo el nombre la variable.

```javascript
let nombre = "Mauricio"
let apellido = "Martinez"

const persona = {
    nombre,
    apellido
}

console.log(persona.nombre)
```

<br>

## Recursividad
---

En pocas palabras es cuando una funcion se llama a si misma.

Con estas hay que tener cuidado ya que pueden entrar en un bucle infinito.

Un uso interezante y util de las funciones recursivas es el de validar datos que introduce un usuario.

ejemplo:

```javascript
const validarEdad = msg => {
  let edad
  try {
    if (msg) edad = prompt(msg)
    else edad = prompt("Introduce tu edad")

    edad = parseInt(edad)
    if (isNaN(edad)) throw "Introduce un numero para tu edad"
    
    if (edad >= 18) console.log("Eres mayor de edad")
    else console.log("Eres menor de edad")

  } catch (e) {
    validarEdad(e)
  }
}

validarEdad()
```

<br>

## Clausuras o closures
---



Una clausura es definir una funcion que nos devuelve una funcion, esto con el objetivo de reutilizarla y resumir el codigo (Ser un poco mas legible)

```javascript
const changeSize = size => {
  return () => {
    document.querySelector('.text').style.fontSize = `${size}px`
}
}

const px12 = changeSize(12)
const px14 = changeSize(14)
const px16 = changeSize(16)

document.querySelector(".t12").addEventListener("click", px12)
document.querySelector(".t14").addEventListener("click", px14)
document.querySelector(".t16").addEventListener("click", px16)
```
[Ejemplo](./Closures/)

<br>

## Parametro Rest
---

Podemos asignar valores por defecto si estos no nos los otorgan y asi poder evitar posibles errores.

```javascript
const suma = (a = 0, b = 0) => a + b
```

Para poder usar el parametro Rest simplemente en los parametros de una funcion colocamos 3 puntos seguidos de como queremos nombrar tal parametro.
Este actuara como un array que almacenara todos los datos que nos pasen.

```javascript
"use strict";

const suma = (...nums) => {
  return nums.reduce((prev, current) => prev + current)
}

console.log(suma(10,3,23))
```

<br>

## Desestructuracion
---

La sintaxis de desestructuración es una expresión de JavaScript que permite desempacar valores de arreglos o propiedades de objetos en distintas variables.

[Más info](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

Podemos hacer diversas cosas para desempacar los datos de un array o objeto.

**Array** <br>

```javascript
const [a, b] =[120, 2]
console.log(a) // 120
console.log(b) // 2

const c, d, rest
[c, d, ...rest] = [10, 20, 30, 40, 50]
console.log(a) // 10
console.log(b) // 20
console.log(rest) // [30, 40, 50]
```

cambiar de nombre u orden variables:

```javascript
let a = 10;
let b = 30;

[a, b] = [b, a]
console.log(a) // 30
console.log(b) // 10
```

Tambien para desempacar la salida de una funcion y poner valores predeterminados en caso de que no nos lo otorguen.

```javascript
const f = () => [2,4]
const [a, b, c = 5] = f()
```

**Objetos** <br>

funciona practicamente igual pero en ves de `[]` se utiliza`{}` y no se puede escoger cualquier nombre, si no el que utiliza el objeto.

```javascript
let {a, b} = {a: 1, b: 2};
```

Si queremos cambiar el nombre lo tenemos que hacer de la siguiente manera:


```javascript
let {a: c, b: d} = {a: 1, b: 2};
```

de igual manera podemos cambiar el nombre y poner un valor predeterminado.

```javascript
const {a: aa = 10, b: bb = 5} = {a: 3};
```

Tambien podemos desempaquetar datos en los parametros de una funcion.

```javascript
const user = {
  id: 42,
  displayName: 'jdoe',
  fullName: {
    firstName: 'John',
    lastName: 'Doe'
  }
};

function userId({id}) {
  return id;
}

function whois({displayName, fullName: {firstName: name}}) {
  return `${displayName} es ${name}`;
}
```

Si queremos acceder a diferentes datos con una misma llave, digamos vamos iterando, tenemos que hacerlo de esta manera:

```javascript
let key = 'z';
let {[key]: foo} = {z: 'bar'};

console.log(foo); // "bar"
```

Rest:

```javascript
let {a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40}
a; // 10
b; // 20
rest; // { c: 30, d: 40 }
```

<br>

## Ternarias
---

Podemos usarlo de diversas formas...
Las ternarias son como un `if` y un `else` solo que en forma de operador.

Primero colocamos el elemento o variable a evaluar, prodiguiendo con un `?` que actuara como `if` y se ejecutara si es `true` lo anterior evaluado, luego ponemos `:` que este sera un `else`.

```javascript
let edad = 16

(edad >= 18) ? console.log('Es mayor') : console.log('Es menor')

// Otro ejemplo
edad = ''
edad = edad ? 12 : 13
console.log(edad);
```

Las Ternarias consumen menos  recursos que los `if`.

Se pueden generar bloques de codigo con los parentesis y comas pero no es recomendable.

```javascript
let edad = 16

(edad >= 18) ? console.log('Es mayor')
             : (
                console.log('Es menor'),
                console.log('No puede pasar')
              )
```

<br>

## Spread
---

Descomprime los valores contenmidos en un array u objeto.

```javascript
const arr1 = [2, 3, 4]
const arr2 = [1, ...arr1, 5]

console.log(arr2)

// Podemos concatenar arrays de una forma mas eficiente.

const arr3 = [...arr1, ...arr2]

// Podemos pasarlo como argumento

const showCoords = (x, y) => console.log(x, y)
const coords = [12, 34]
showCoords(...coords)
```

Lo mismo sucede con los objetos.

<br>

## Objeto Date
---

Para trabajar con el objeto Date tenemos que instanciar tal objeto. este tiene diversos metodos.

`const fecha = new Date()`

|    Metodo     | Descripcion                            |
| :-----------: | -------------------------------------- |
|   getDate()   | Devuelve la fecha del mes              |
|   getDay()    | Devuelve el dia en que estamos -1      |
|   getMonth    | Devuelve el mes en que estamos -1      |
|   getYear()   | Devuelve el año en que estamos -1900   |
| getFullYear() | Devuelve el año en que estamos         |
|  getHours()   | Devuelve la hora actual en formato 24h |
| getMinutes()  | Devuelve los minutos actuales          |
| getSeconds()  | Devuelve los segundos actuales         |

Podemos añadir parametros en la instanciacion del objeto Date, para asi poder setear la hora a una que nosotros querramos.

<br>

## Guardar datos en el navegador
---

Hay dos formas de guardar datos una en la que al cerrar la pestaña o actualizarla se pierda la informacion y otra en la cual es permanente (cache).

<br>

### LocalStorage
---

Cachea la informacion y no se pierde a no ser que el usuario lo quiera.

`localStorage` Tiene diversos metodos para poder guardar o borrar informacion.

- `setItem(<key>, <value>)` Para poder guardar un elemento.
- `getItem(<key>)` Recuperar un elemento que ya hemos guardado.
- `removeItem(<key>)` Eliminar los datos que que hemos guardado.
- `clear()` Borra todo el local storage.

<br>

### SessionStorage
---

`sessionStorage` Tiene los mismos metodos de localStorage, pero esta informacion es mas volatil, cada vez que cerramos el navegador o cerramos la ventana se borra.

<br>

## Drag & Drop
---

API para agarrar y arrastrar.

Esto se trabaja con eventos, los cuales son:

|   Evento    | Descripcion                                            |
| :---------: | ------------------------------------------------------ |
| "Dragstart" | Cuando agarramos el elemento                           |
|   "Drag"    | Mientras estamos agarrandolo (Se ejecuta muchas veces) |
|  "Dragend"  | Cuando lo soltamos                                     |

Estos eventos son para el elemento que queremos mover, pero hay otros eventos que son para la zona en la cual soltamos el elemento.

|   Evento    | Descripcion                                           |
| :---------: | ----------------------------------------------------- |
| "dragenter" | Cuando enra un elemento a la zona                     |
| "dragover"  | Mientras hay un elemento en la zona (Multiples veces) |
|   "drop"    | Cuando se suelta el elemeno                           |
| "dragleave" | Cuando sale el elemento                               |

Para poder soltar algun elemento en una zona nosotros lo tenemos que permitir con el evento dragover y prevenimos el evento por defecto. esto nos permitira captar cuando se suelte algun objeto en nuestra zona.

```javascript
const circulo = document.querySelector(".circulo")
const cuadrado = document.querySelector(".cuadrado")

cuadrado.addEventListener("dragover", (e)=> e.preventDefault())
cuadrado.addEventListener("drop", ()=> console.log(1))
```

<br>

### DataTransfer
---

El evento tienen un metodo que se llama dataTransfer con el cual podemos crear o consegir informacion, pero este solo puede pasar strings.

```javascript
circulo.addEventListener("dragstart", (e) => {
  e.dataTransfer.setData("clase", e.target.className)
})
cuadrado.addEventListener("dragover", (e)=> e.preventDefault())
cuadrado.addEventListener("drop", (e)=> console.log(e.dataTransfer.getData('clase')))
```

<br>

## Geolocalizacion
---

Para poder acceder a la geolocalizacion tenemos que usar el objeto `navigator` que tiene un atributo que es `geolocation` el cual tiene un metodo para poder obtener la ubicacion, el cual es: `getCurrentPosition()`.

A este metodo se le pasan 2 callbacks y un objeto con la configuracion de la obtencion de la info.

`navigator.geolocation.getCurrentPosition(<position>, <error>, <options>)`

Options puede ajusgtarse lo siguiente: 

```javascript
const options = {
  maximumAge: 0, // Para que no se optenla la posision cacheada
  timeout: 3000, // 3s De espera
  enableHightAccuracy: true // La maxima presicion posible.
}
```

Un ejemplo de uso.

```javascript
navigator.geolocation.getCurrentPosition(
  (pos) => console.log(pos.coords),
  (err) => console.log(err),
  {
    enableHighAccuracy: true,
    timeout: 3000,
    maximumAge: 0
  }
)
```

**watchPosition()** <br>

Para ver la posision en tiempo real.

<br>

## Historial
---

Manejar el historial de la ventana.
Este es un objeto de window asi que podemos usarlo sin mas.

`history`

Este tiene diversos metodos, los cuales son:

|                  Metodos                  | descripcion                                       |
| :---------------------------------------: | ------------------------------------------------- |
|                 `back()`                  | Vuelve atras (como la flecha)                     |
|                `forward()`                | Va hacia adelante                                 |
|                 `length`                  | Tamaño del historial                              |
|                  `go(n)`                  | n>0 va n veces adelante, n=0 reload, n<0 atras    |
|  `pushState(<obj>, <title>, <addUrl> )`   | Añade una entrada al historial usar "?..." en url |
| `replaceState(<obj>, <title>, <addUrl> )` | Lo mismo que pushState pero edita el historial    |

Hay un evento para detectar los cambios en el historial.

```javascript
addEventListener("popstate", e => console.log(e.state))
```

Este nos devolvera el objeto que mandamos con `pushState()` o `replaceState()`

<br>

## FileReader
---

Para poder leer archivos lo hacemos iterando el objeto `FileReader()`, el cual tiene varios metodos, segun lo que querramos leer.

Para leer txt o json podemos usar el metodo `.readAsText(<element>)` el elemento lo obtenemos de un input type='file' a el cual le podemos poder el atributo multiple para recibir varios archivos, este tipo de input siempre devolvera un array sin importal al atriburo multiple.

Se leccionamos el input y le colocamos el evento `change` que llamara a nuestra funcion para leer cada vez que cambie.

