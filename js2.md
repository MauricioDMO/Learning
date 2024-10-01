# Aprendiendo JS Mid

- [Aprendiendo JS Mid](#aprendiendo-js-mid)
  - [Objeto Window](#objeto-window)
    - [**Screen y Scroll**](#screen-y-scroll)
      - [_Objetos barprop_](#objetos-barprop)
    - [**Location**](#location)
  - [Eventos](#eventos)
    - [Event Listener](#event-listener)
      - [Objeto Event](#objeto-event)
      - [Como se ejecutan los eventos?](#como-se-ejecutan-los-eventos)
      - [Eventos del Mouse](#eventos-del-mouse)
      - [Eventos del Teclado](#eventos-del-teclado)
      - [Eventos de interfaz](#eventos-de-interfaz)
  - [Temporizadores](#temporizadores)
  - [Switch](#switch)
  - [Manejo de errores](#manejo-de-errores)
  - [CallBack](#callback)
  - [Promesas](#promesas)
  - [Async y Await](#async-y-await)
  - [Peticiones HTTP](#peticiones-http)
    - [**Datos estructurados - Javascript Object Notation (JSON)**](#datos-estructurados---javascript-object-notation-json)
    - [AJAX - Asynchronous JavaScript And XML](#ajax---asynchronous-javascript-and-xml)
  - [Fetch](#fetch)
  - [Manejo de errores de fetch](#manejo-de-errores-de-fetch)
  - [Biblioteca Axios](#biblioteca-axios)
  - [Async y Await con Fetch y Axios](#async-y-await-con-fetch-y-axios)

<br>

## Objeto Window

---

(Para mas informacion buscar: window object javascript)

El objeto mas importante en la web, hasta el DOM depende del objeto window.

Este tiene MONTON de metodos.

> Prefix _window._

-   `open(x)`
    Abre en una pestaña nueva el enlace x que le proporcionemos

-   `close()`
    Cierra la ventana que le digamos ejemplo:

```javascript
const ventana = window.open("https://youtu.be");
ventana.close();
```

-   `closed`

    Devuelve bool, verifica si la ventana que le dijimos esta cerrada o no:

```javascript
const ventana = window.open("https://youtu.be");
ventana.closed; // false
ventana.close();
ventana.closed; //true
```

-   `stop()`
    Detiene la carga de la ventana que especifiquemos

-   `alert({x})`
    Metodo proveniente de window pero ya no se utiliza. `window.alert('xd')`

-   `print()`
    Lo podemos colocar simplemente como `print()` y este nos abrira la opcion para mandar a imprimir la pagina web.

-   `prompt({x})`
    Devuelve una string, para pedir datos a usuario por ventana emergente.

-   `confirm({x})`
    Pregunta al usuario, y devuelve bool segun su respuesta.

### **Screen y Scroll**

---

> Prefix _window._

-   `screen`
    Devuelve un objeto con las propiedades del screen.

-   `screen.availHeight` y `screen.availWidth`
    Devuelven el alto y ancho correspondiente de la ventana

-   `screenLeft` y `sreenTop`
    Devuelven la distancia en px de el borde de la vetana hacia el lado correspondiente. (esta no se puede editar)

-   `scrollX` y `scrollY`
    devuelve la cantidad de px que hemos scroleado de el lado correspondiente (x y)

-   `scroll({x}, {y})`
    Para desplazar la vista a las coordenadas x, y.

-   `resizeBy(x, y)` y `resizeTo(x, y)`
    Redimenciona la ventana que le especifiquemos.

-   `moveTo(x, y)` y `moveBy(x, y)`
    Mover la ventana a una pocicion que especifiquemos

> Los dos anteriores casi ni se usan y se tiene que dar permisos desde el servidor.

#### _Objetos barprop_

Para comprobar si el objeto es visible
window.elemento.visible // true o false

-   locationbar
-   menubar
-   personalbar
-   scrollbars
-   statusbar
-   toolbar

### **Location**

---

Para ver donde estan ubicadas ciertas cosas como:

> Prefix _window.location._

-   `href`

    Devuelve la url de la pagina actual.

-   `hostname`

    Devuelve el dominio del server

-   `pathname`

    Devuelve la ruta y el nombre de archivo de la pag.

-   `protocol`

    devuelve el protocolo web utilizado (http o https)

-   `assign({x})`

    Carga el documento x que pedimos

<br>

## Eventos

---

Cualquier cambio/suceso que ocurre en la pagina.

### Event Listener

Añadimos una escucha al elemento.

-   `addEventListener({evento}, {funcion})`

    No se le pueden pasar parametros (solo el evento).

Ejemplo:

```javascript
const button = document.querySelector(".button");
button.addEventListener("click", saludar);

function saludar() {
    alert("Hola Pepe");
}
```

O si queremos usar las funciones flechas hacemos lo siguiente:

```javascript
const button = document.querySelector(".button");
button.addEventListener("click", () => {
    alert("Hola pepe");
});
```

-   `removeEventListener({event}, {function})`
    Esta solo funciona con funciones asociadas, no cuando lo hacemos con funciones flechas.

```javascript
const button = document.querySelector(".button");
button.addEventListener("click", saludar);

function saludar() {
    alert("Hola Pepe");
    button.removeEventListener("click", saludar);
}
```

#### Objeto Event

Es el unico parametro que le podemos pasar a las funciones de los eventos. (Este funciona como this)

Ejemplo:

```javascript
const button = document.querySelector(".button");
button.addEventListener("click", saludar);

function saludar(e) {
    console.log(e.target);
}
```

(Por convecion se utiliza e o evt)

Otra manera de hacer lo mismo seria:

```javascript
const button = document.querySelector(".button");
button.addEventListener("click", (e) => {
    console.log(e.target);
});
```

El metodo target nos devuelve el elemento que llamo al evento.

#### Como se ejecutan los eventos?

Los eventos se ejecutan de dos maneras:

-   Event Bubling

    Este ejecuta el evento mas especifico al menos especifico (hijos => padres)

-   Event Capturing

    Este ejecuta del menos especifico al mas especifico (padres => hijos)

Podemos cambiar esto al poner como tercer parametro en `addEventListener({evt}, {function}, true)`

```javascript
const button = document.querySelector(".button");
const contenedor = document.querySelector(".contenedor");

button.addEventListener("click", (e) => {
    alert("Button");
});
contenedor.addEventListener("click", (e) => {
    alert("Container");
});
```

Esto ejecutaria button, container. Pero si añadimos true al final del evento de container este se ejecutara primero y luego button.

Si queremos que el evento no se propague a los demas elementos usamos lo siguiente:

```javascript
button.addEventListener("click", (e) => {
    alert("Button");
    e.stopPropagation();
});
```

#### Eventos del Mouse

-   **click** - ocurre con un click
-   **dblclick** - ocurre con un doble click
-   **mouseover** - ocurre cuando el puntero se mueve sobre un elemento o sobre uno de sus hijos.
-   **mouseout** - ocurre cuando se mueve el puntero fuera de un elemento o de sus elementos secundarios

/ - / - / otros / - / - /

-   **contextmenu** - ocurre con un click en el boton derecho en un elemento para abrir un menú contextual.
-   **mouseenter** - ocurre cuando el puntero se mueve sobre un elemento.
-   **mouseleave** - ocurre cuando el puntero se mueve fuera de un elemento.
-   **muusedown** - ocurre cuando un usuario apreta un boton del mosuse sobre un elemento.
-   **mouseup** - ocurre cuando un usuario suelta un botón del mouse sobre un elemento.
-   **mousemove** - ocurre cuando el puntero se mueve mientras está sobre un elemento.

#### Eventos del Teclado

-   **keydown** - ocurre cuando una tecla se presionar
-   **keypress** - ocurre cuando una tecla se presiona y suelta
-   **keyup** - ocurre cuando una tecla se deja de presionar

#### Eventos de interfaz

-   **error** - ocurre cuando sucede un error durante la carga de un archivo multimedia.
-   **load** - ocurre cuando un objeto se ha cargado
-   **beforeunload** - ocurre antes de que el documento esté a punto de descargarse
-   **unload** - ocurre una vez que se ha descargado una página
-   **resize** - ocurre cuando se cambia el tamaño de la vista del documento
-   **scroll** - ocurre cuando se desplaza la barra de desplazamiento de un elemento
-   **select** - ocurre después de que el usuario selecciona algún texto de \<input> o \<textarea>

[MUCHOS MAS EVENTOS](https://www.w3schools.com/jsref/obj_events.asp)

<br>

## Temporizadores

---

-   `setTimeout({function}, {tInMs})`

    Funcion para ejecutar una funcion despues de que pase un tiempo t en milisegundos

Para detenerlos los asignamos a una variable y los pasamos a la siguiente funcion: `clearTimeout({var})`

-   `setInterval({function}, {t})`

    Ejecuta la function cada t en milisegundos. (`clearInterval` para eliminar el intervalo)

Hay una forma interezante para usar, esta ejecutara la funcion cierta cantidad de veces y se cortara, esta es uniendo el intervalo y el timeout.

```javascript
const intervalo = setInterval(() => {
    document.write("Hola ");
}, 1000);

setTimeout(() => {
    clearInterval(intervalo);
}, 3000);
```

> Esto es preferible no utilizarlo ya que utiliza muchos recursos

## Switch

Antes de ver los switch tenemos que aprender que son los bloques, los bloques se definen com {} y todo lo que este dentro de ellos es parte del bloque.

Podemos hacer bloques para hacer un nuevo conjunto de variables locales.

```javascript
let fruta = "coco";
{
    let fruta = "pera";
}
```

Esto no nos daria error ya que la variable let es local y se vulve a crear ("sobreescribir").<br>
Si esto lo hicieramos sin el bloque nos diria que fruta ya ha sido declarada.

**Ahora si switch**

Switch es una "funcion" a la que le pasamos una variable y ejecuta trosos de codigo dependiendo del valor de la variable, para cada caso usamos la palabra clave _case_ seguido del valor que queremos evaluar.

Tenemos que poner _break_ al final de cada caso para que los demas no se ejecuten.

En caso de que no sea singun caso usamos la sentencia _default_

Ejemplo:

```javascript
let fruta = "coco";

switch (fruta) {
    case "banana":
        document.write("Es amarilla");
        break;
    case "coco":
        document.write("Es cafe");
        break;
    case "pera":
        document.write("Es verde");
        break;
    default:
        document.write("No es ninguna");
        break;
}
```

Se podria hacer esto mas facil con if y else...

```javascript
let fruta = "coco";

if (fruta == "banana") document.write("Es amarilla");
else if (fruta == "coco") document.write("Es cafe");
else document.write("Es verde");
```

Switch no es muy usada, ademas if else tiene mejor rendimiento que este.<br>
Este solo se usa en casos de que la variable sea algo compleja y se quiera un codigo mas legible...

<br>

## Manejo de errores

---

`try` y `catch`:
Es para estar preparados ante cualquier error que pueda aparecer en nuestro codigo.
_catch_ actuaria como lo que se ejecutaria en caso de un error, este error se guarda en el parametro del _catch_.

```javascript
try {
    sdsefwsef;
} catch (error) {
    document.write(error); // error es un objeto
}
```

[Todos las excepcciones](https://developer.mozilla.org/es/docs/Web/API/DOMException/) <br>
[Todos los errores](https://developer.mozilla.org/es/docs/Web/API/DOMError/)

`finally` Es un bloque final que se ejecuta incondicionalmente haya error o no.

```javascript
try {
    sdsefwsef;
} catch (error) {
    document.write(error); // error es un objeto
} finally {
    console.log("Me ejecuto igual :D");
}
```

`finally` Se ejecuta sin importar que, si hay un `return` en el try le da igual y se ejecuta...

Finalmente tenemos la sentencia `throw` que esta nos lanza un error que le especificamos en una string.

`throw 'Error unico :D'`

Con throw podemos mandar todos las variables que querramos ([], {}, '')

Y como extra tenemos la sentencia `typeof` que le ponemos como siguiente algo a lo que le queremos saber el typo de variable que es.

`console.log(typeof 'a')`

<br>

## CallBack

---

Un callback es una funcion que que se pasa como parametro a otra funcion para ejecutarla, esto puede servir para hacer pruebas y otras cosas

```javascript
const modify = (arr, cb) => {
    arr.push(2);
    cb();
};

const arr = [10, 2, 3];

modify(arr, () => {
    console.log("Se modifico el array");
});
```

<br>

## Promesas

---

Las promesas son un objeto al cual tenemos que instanciarlo, pasandole una funcion, a esa funcion le pasaremos como parametros `resolve` y `reject` correspondientemente, estos son para devolver los datos correspondientemente, o podemos abreviarlo con `res` y `rej`.

Para acceder al valor que nos devuelve `res` utilizamos el metodo `then`, a este le pasaremos como parametro una funcion que a la vez le pasaremos un parametro que ocupara el valor de la respuesta de la promesa, esto para acceder a nuestro valor.

En cambio si tenemos un error con `rej` este directamente nos dara un error que podemos utilizar como parametro en el metodo `catch`, a este le pasamos una funcion como parametro y a la funcion le pasaremos el el error que se convertira en la respuesta del `rej`. (Este puede ser lo que sea, string, objeto, array, boolean, etc)

```javascript
const personas = [
    {
        nombre: "Lucas Dalto",
        instagram: "@SoyDalto",
    },
    {
        nombre: "Robertico",
        instagram: "@Robertico",
    },
    {
        nombre: "Rancio Rancio",
        instagram: "@Rancio",
    },
    {
        nombre: "Camila Nesa",
    },
];

const obtenerPersona = (id) => {
    return new Promise((res, rej) => {
        if (personas[id] == undefined) rej("No se encontro la persona");
        else res(personas[id]);
    });
};

const obtenerInstagram = (id) => {
    return new Promise((res, rej) => {
        if (personas[id].instagram == undefined)
            rej("No se encontro el instagram");
        else res(personas[id].instagram);
    });
};

let id = 4;

obtenerPersona(id)
    .then((persona) => {
        document.write(persona.nombre);
        return obtenerInstagram(id);
    })
    .then((instagram) => {
        document.write(instagram);
    })
    .catch((e) => {
        document.write(e);
    });
```

Hay que tener en cuenta que si hay un solo error el catch actuara y dejara de ejecutar todo lo demas que siga.

<br>

## Async y Await

---

La asincronia espera a que las demas funciones tengan el resultado, ya que si le pedimos informacion a un servidor este puede tardar en darnos la respuesta a nuestra peticion.

`await` Necesita obligatoriamente una funcion asincrona para poder ejecutarse.

El await funciona como un `.then` ya que al asignarlo a la variable ya no es una promesa si no el resultado que esperabamos.

Hay 2 formas de declarar una funcion asincrona:

```javascript
async function funcion1() {}
const funcion2 = async () => {};
```

Dentro de estas clases de funciones usaremos el `await`, el await no pasa a la siguiente linea de codido si esta no ha resivido los datos aun...

```javascript
const obtenerInfo = (text) => {
    return new Promise((res, rej) => {
        setTimeout(() => {
            res(text);
        }, 1000);
    });
};

const mostrarData = async () => {
    d1 = await obtenerInfo("a");
    d2 = await obtenerInfo("b");
    d3 = await obtenerInfo("c");
    document.write(d1);
    document.write(d2);
    document.write(d3);
};

mostrarData();
```

<br>

## Peticiones HTTP

---

Pedir datos a un servidor para luego servirlos en nuestro sitio web, esto sigue el modelo cliente servidor.

<br>

### **Datos estructurados - Javascript Object Notation (JSON)**

La principal diferencia entre los JSON y los objetos de JS es que las variables del objeto se escriben en comillas, ya que no se pueden enviar al servidor datos sin comillas, porque traeria muchos problemas.

```javascript
const objeto = {
    nombre: "Mauricio",
    apellido: "Martínez",
};

const json = {
    nombre: "Mauricio",
    apellido: "Martínez",
};
```

Hay 2 dipos de JSON:

-   **Los serializados**: que son JSON con formato su respectivo formato de JSON, pero estos son un string, `'{"nombre":"Mauricio"}'`, cuando enviamos y recibimos datos este sera el formato que deberia de tener para evitar problemas.

-   **Los deserializados**: son los JSON con su formato como que si fuera un objeto.

Para tratar con JSON tenemos un objeto llamado JSON en JS. <br>
Este tiene un metodo llamado `stringify()` que nos combierte un objeto JSON a un JSON serializado.

```javascript
const deserializado = {
    v1: "Pedro",
    v2: "Juan",
};
const serializado = JSON.stringify(deserializado);
document.write(serializado);
```

Luego para deserializar el JSON utilizamos el metodo `parse()` del objeto JSON.

```javascript
const serializado = '{"v1": "Pedro", "v2": "Juan"}';
const deserializado = JSON.parse(serializado);
document.write(serializado);
```

<br>

### AJAX - Asynchronous JavaScript And XML

Normalmente si solicitamos informacion y nos llega una respuesta esta actualiza la pagina completa.

Esto si lo hacemos con AJAX, solo nos actualizara la parte de la pagina que nosotros le ordenemos.

Para hacer peticiones usamos el objeto `XMLHttpRequest()` esto se lo asignamos a una variable para poder trabajar con ella.

Tenemos que añadirle un listener a la peticion para poder trabajar con ella cuando obtenga nuestros datos.

Cuando hayamos asignado la peticion añadimos el listener y despues decimos que datos queremos enviar o solicitar a que servidor con un metodo `open()` que tiene nuesta peticion, le pasamos como parametro el tipo de peticion (GET o POST), luago al servidor o archivo a quien le queremos solicitar info.

Al final de esto usamos el metodo `send()` que tiene nustra peticion, esto para enviar nuestra peticion.

Vamos a ver la forma antigua en que se hacia.

```javascript
const request = new XMLHttpRequest();

request.addEventListener("readystatechange", () => {
    if (request.readyState == 4 && request.status == 200) {
        console.log(peticion.response);
    }
});

request.open("GET", "informacion.txt"); // Solicitamos un archivo de nuestro servidor

peticion.send();
```

`.readyState` Tiene 4 valores (1-4), que tienen distinto significado:

-   `1` La solicitud se creo correctamente.
-   `2` La solicitud se envio correctamente.
-   `3` Se esta prosesando la informacion en nuestro script.
-   `4` Se nos dio una respuesta y ya se puede utilizar.

El atributo `response` tiene valor desde que `readyState` tiene valor de 3 pero se utiliza el valor de 4.

El atributo `status` nos da el estado de la solicitud siendo:

-   `200` Solicitud exitosa.
-   `404` No se encontro el archivo.
-   `403` No se tiene acceso al archivo.
-   Muchos otros mas...

En la actualidad se hace de otra forma con el evento "load" que actua cuando el readyState es 4.

Ahora solo tenemos que validar el estado de la respuesta

```javascript
const request = new XMLHttpRequest();

request.addEventListener("load", () => {
    if (request.status == 200) {
        console.log(peticion.response);
    }
});

request.open("GET", "info.json");
peticion.send();
```

Esto nos da un JSON serializado que esta en nuestro servidor.

Estas peticiones tampoco se hacen asi ahora, ahora se utiliza `fetch` que lo veremos mas adelante.

Una recomedacion.
En internet explorer no existe el objeto para hacer peticiones, asi que tenemos que igualarlo a un objeto que especifica internet explorer.

```javascript
let request;

if (window.XMLHttpRequest) request = new XMLHttpRequest();
else request = new ActiveXObject("Microsoft.XMLHTTP");
```

**- - - POST - - -**

En el post es todo casi igual solo que el servidor al que le mandamos los datos nos devulve un status 201 y a la peticion le tenemos que setear un header, que diga que es lo quequeremos de ese servidor. En el ejemplo aparese que el tipo de contenido que queremos es un JSON con charset UTF8.

Luego le mandamos el JSON serializado.

```javascript
const request = new XMLHttpRequest();
request.addEventListener("load", () => {
    if (request.status == 200 || request.status == 201) {
        let response = JSON.parse(request.response);
        console.log(response);
    }
});
request.open("POST", "https://reqres.in/api/users");

request.setRequestHeader("Content-type", "application/json;chatset=UTF8");

request.send(
    JSON.stringify({
        name: "morpheus",
        job: "leader",
    })
);
```

> Todo lo anterior es AJAX, pero este fue reemplazado por fetch.
> Por ser mas Rapido u facil de implementar.

<br>

## Fetch

---

Esta basado en promesas, este siempre nos devuelve una promesa encapsulada.

El metodo por defecto de `fetch` es GET, no nesecitamos especificarlo.

fetch es una funcion de JS, y podemos asignarla a una variable para poder tratar con ella pero hay una forma mas sensilla de tratar con ella:

```javascript
fetch("https://reqres.in/api/unkown/2")
    .then((res) => res.text())
    .then((res) => console.log(JSON.parse(res)));
```

`fetch` nos devuelve una promesa encapsulada, hay varios metodos para desencapsularla:

```javascript
fetch("https://reqres.in/api/unkown/2")
    .then((res) => res.text()) //Aqui iran los metodos de desencapsulamiento
    .then((res) => console.log(JSON.parse(res)));
```

> Todos estos metodos devuelven una promesa. Por lo tanto usaremos el metodo `then` para trabajar con ellas.

-   `text()`
    Devuelve el JSON en formato serializado por lo tanto hay que deserializarlo.

-   `json()`
    Devuelve el JSON en formato deserializado.

-   **INVESTIGAR**
-   `blob()`
-   `formData()`
-   `arrayBuffer()`

**Como hacemos un POST?**

Al fetch le pasamos un segundo parametro que va a ser un objeto con toda la informacion que le vamos a pasar a el servidor, que va a ser:

> method: "POST"
> body: // El objeto JSON serializado que le mandaremos
> headers: {"Content-type": "application/json"}

Ejemplo:

```javascript
fetch("https://reqres.in/api/users", {
    method: "POST",
    body: '{"nombre":"Mauricio","apellido":"Martinez"}',
    headers: { "Content-type": "application/json" },
})
    .then((res) => res.json())
    .then((res) => console.log(res));
```

Dependieno del tipo de informacion que mandemos la cabecera

<br>

## Manejo de errores de fetch

---

Los errores 4XX y 5XX siempre pasan al `then` y tenemos que tratar con ellos usando los valores de la respuesta `.ok` para saber si fue un exito y `.status` que nos dice el estado HTTP.

```javascript
const getName = async () => {
    await fetch("info.json")
        .then((res) => {
            if (!res.ok) {
                throw new Error("Error HTTP: " + res.status);
            }
            return res.json();
        })
        .then((res) => {
            console.log(res);
        })
        .catch((e) => console.error(e));
};

getName();
```

O en su lugar usando `await`:

```javascript
const getName = async () => {
  const res = await fetch("info.json")
  
  try {
    
    if (!res.ok) {
      throw new Error('Error HTTP: ' + res.status)
    }

    const json = await res.json()
    console.log(json);
    
  } catch (e) {
    console.error(e)
  }
}

getName()
```


<br>

## Biblioteca Axios

---

Una biblioteca optimizada para realizar peticiones, si vamos a hacer muchas peticiones es recomendable usar Axios.

Pero si solo vamos a hacer unas pocoas peticiones en especifico es mejor utilizar `fetch`.

Axios esta basado en promesas.

Para ver el codigo hay un reposirotio en GitHub [Aqui](https://github.com/axios/axios)

```html
<script src="https://cdn.jsdelivr.net/npm/axios@1.1.2/dist/axios.min.js"></script>
```

Este codigo lo llamamos antes de nuestro codigo de JS

Con axios los datos no nos vienen encapsulados. podemos trabajar directamente con ellos.

```javascript
axios("info.json").then((res) => console.log(res.data));
```

Por defecto trabaja con peticiones GET.

**- - Con Axios hay varias formas de mandar informacion - -**

La defecto que vimos anteriormente.

Un POST como metodo.

```javascript
axios
    .post("https://reqres.in/api/users", {
        nombre: "Mauricio",
        apellido: "Martinez",
    })
    .then((res) => console.log(res.data));
```

O estableciendo nosotro los datos:

```javascript
const json = {
    nombre: "Mauricio",
    apellido: "Martinez",
};

axios("https://reqres.in/api/users", {
    method: "post",
    data: json,
}).then((res) => console.log(res.data));
```

Para mandar la informacion no debemos serializar el JSON ya que axios lo hace por nosotros y si lo serializamos estaremos mandando una string al servidor no un JSON serializado.

<br>

## Async y Await con Fetch y Axios

---

```javascript
const getName = async () => {
    let request = await fetch("info.json");
    let resultado = await request.json();
    console.log(resultado);
};

getName();
```
