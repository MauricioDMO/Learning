# Learning React!

- [Learning React!](#learning-react)
  - [Inicializacion desde 0 (vanilla to React)](#inicializacion-desde-0-vanilla-to-react)
  - [Creando un componente](#creando-un-componente)
  - [Hooks](#hooks)
  - [Crear un estado (useState)](#crear-un-estado-usestate)
  - [Renderizado condicional](#renderizado-condicional)
  - [Ejemplo de contador](#ejemplo-de-contador)
  - [Propagacion de renderizado/cambios](#propagacion-de-renderizadocambios)
  - [Renderizado de Listas](#renderizado-de-listas)
  - [useEffect](#useeffect)
  - [Como hacer un fetching](#como-hacer-un-fetching)
  - [Custom Hooks](#custom-hooks)
  - [Hacer Testing](#hacer-testing)
  - [Frameworks CSS classless](#frameworks-css-classless)
  - [useRef](#useref)
    - [Comprobar formularios](#comprobar-formularios)
  - [useMemo](#usememo)
  - [useCallback](#usecallback)
  - [Funcion Debounce desde cero](#funcion-debounce-desde-cero)
  - [useId](#useid)
  - [useContext](#usecontext)
  - [UseReducer](#usereducer)
  - [React Router](#react-router)
    - [Rutas](#rutas)
    - [Link](#link)
    - [Rutas dinamicas](#rutas-dinamicas)
    - [Rutas anidadas](#rutas-anidadas)
    - [Enlaces activos](#enlaces-activos)
    - [Redirecciones](#redirecciones)
    - [Navegacion programatica](#navegacion-programatica)
    - [Navigate state](#navigate-state)


<br>

## Inicializacion desde 0 (vanilla to React)
---

Instalamos el plugin de react en vite
`npm i @vitejs/plugin-react -E`

Ahora de instalan las dependencias de react
`npm i react react-dom -E`

Ahora se crea un archivo con la configuracion de vite el cual contendra
`vite.config.js`

```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()]
})

```

Ahora en el `main.js` tenemos renombrarlo a `main.jsx` que importar `createRoot` e inicializar la root.

Tambien lo tenemos que renombrar en el archivo HTML.

```javascript
import { createRoot } from 'react-dom/client'

const root = createRoot(document.getElementById('app'))
root.render(<h1>Hola Mundo!</h1>)

```


<br>

## Creando un componente
---

Creamos una funcion, su nombre debe de empezar con mayuscula ya que todos los componentes tienen que iniciar de esta manera para evitar colisiones con HTML.

Los parametros que son llamados "props", en este caso solo es uno, el cual sera un objeto con todos los "atributos" que usemos a la hora de usar el componente. 

Este es bueno desestructurar el objeto que viene como parametro, todo atributo que pasemos en el componente va a ser la key del objeto que viene como parametro.

```javascript
const Avatar = ({name = 'Julia', id =  1, size=''}) => {
  return <div>{name}{id}{size}</div>
```

De esta manera tambien podemos utilizar valores por defecto.

Si queremos que un componente pueda contener hijos tenemos que usar la prop de `children`, esta coontendra el contenido/ hijos que tienen nuestro componente.

```javascript
const MiComponente = ({children}) => {
  return (
    <h2>Hola<h2>
    {children}
  )
}

<MiComponente>
  Hijo
  <span>multiple</span>
</MiComponente>

```

<br>

## Hooks
---

Todos los hook son funciones...

|                Hook                | Descripcion                                                  |
| :--------------------------------: | ------------------------------------------------------------ |
|         `useState(<init>)`         | El estado inicial puede ser cualquier cosa hasta una funcion |
| `useEffect(<func>, <dependecies>)` | La funcion se ejecuta una vez al montarse el componente      |

NUNCA se puede tener un hook dentro de un condicional, while, for, etc. Siempre tienen que estar en la raiz del componente. 

<br>

## Crear un estado (useState)
---

Tenemos que importar `useState` de `react`, lo podemos hacer de la siguiente forma:
`import {useState} from 'react'`

Ahora para crear un estado usamos esta funcion que nos debuelve un array con dos valores, el primero que es el estado actual y la segunda es una funcion que nos permite modificarlo.

Vamos a ponerlo como que si esta activado o des activado.

El valor que le pasamos a useState es el estado inicial.

```javascript
const [enabled, serEnabled] = useState(false)
```

Con esto podemos verificar si hay un estado activo o no y ademas poder cambiar su estado y mostrarlo.

Con todo lo anterior podemos hacer lo siguiente:

```javascript
const Avatar = ({name = 'Julia', id, size}) => {
  const src = `https://randomuser.me/api/portraits/women/${id}.jpg`
  const [enabled, setEnabled] = useState(true)
  const className = enabled ? '' : 'disabled'
  const imgClassName = size ? size : ''


  return (
    <picture className={imgClassName}>
      <img  className={className} onClick={() => setEnabled(!enabled)} src={src} alt="User Image" />
      <b>{name}</b>
    </picture>
  )
}
```

El atributo `onClick` que esta en el elemento img no es el mismo de HTML si no que es un metodo detecta si hay un click en ese elemento y ejecuta una funcion que le especifiquemos. en este caso setear el activado a lo contrario que esta en este momento.

El atributo `className` es simplemente para poner nombres de clases ya que la palabra class es reservada de JS.

Si la prop que queremos usar tendra el mismo nombre que el estado usamos el prefijo initial- para asi poder ser mas claros.

Si se utiliza una prop para iniciar el estado, este solo se inicia una sola vez.
Esto por si queremos que un estado cambie las propiedades de un hijo y esta prop la utilizamos para inicializar otro estado.

Los datos del nuevo estado usando `setEstado(nuevoEstado)` tienen que ser totalmente nuevos, siempre hay que pasarle un nuevo elemento, array o lo que sea.
Y nunca hay que modificar el estado directamente, SIEMPRE se tiene que tratar como inmutable y se tiene que cambiar usando la funcion propia del estado.

Los estados siempre tienen que estar en el cuerpo de la funcion, nunca dentro de un if, while, for, lo que sea.

Si de estado inicial le pasamos una funcion esta se ejecutara y omara el valor de lo que devuelva la funcion.

Es buena practica inicializar el estado con el tipo de dato que vamos a utilizar, si lo tenemos muy pero muy claro ponemos usar `null` para decir que ese dato no lo tenemos.

En los estados no es recomendable setear todo de usa sola vez, lo que s etiene que setear es lo minnimo posible para que funcione el estado.

<br>

## Renderizado condicional
---

Podemos hacer un return rapido que si no tenemos algun dato se renderize algo por defecto.

O tambien hacer las evluaciones dentro del return de la siguiente manera.

```javascript
return (
  <picture className={size}>
    {
      id ? <img  className={className} onClick={() => setEnabled(!enabled)}
        src={src} alt="User Image" />
        : <b>Sin Imagen</b>
    }
    <b>{enabled ? name : 'Desactivada'}</b>
  </picture>
)
```

Cuando renderizamos algo con react solo se puede uno a la vez, no importa si este tiene mas elementos dentro...

Si no queremos añadir un elemento de por gusto a nuestro DOM podemos uzar la siguiente forma:

```javascript
return (<>
<h1>Hola</h1>
<p>Mundo</p>
</>)
```

Tambien podemos sustituirlo con el componente.

```javascript
<React.Fragment>
  <Contenido>
</React.Fragment>
```

<br>

## Ejemplo de contador
---

```javascript
import React from 'react'
import { useState } from 'react'

export const Contador = () => {
  const [count, setCount] = useState(0)

  return (<div>
    <h1>La cuenta es de {count}</h1>
    <button onClick={() => setCount(count+1)}>Incrementar</button>
    <button onClick={() => setCount(count-1)}>Decrementar</button>
  </div>)
}
```

<br>

## Propagacion de renderizado/cambios
---

Cuando en un componente padre surgen cambios todos los componentes hijos se vuelven a cambiar sin importar que sus propiedades hayan cambiado o no.

En el DOM no vuelve vuelve a renderizarse, porque React DOM observa que no hay ningun cambio, pero todo el codigo que hay dentro de los componentes hijos se vuelve a ejecutar.

**Actualizacion** <br>

La actualizacion de los estados es asincrona, (no bloquea la ejecucion del script)

<br>

## Renderizado de Listas
---

Si renderizamos una lista tenemos que pasar una prop llamada `key` que va a ser un identificador unico, ni puede repetrise en ningun otro elemento, si este va a ser el index, tenemos que estar seguro que esa lista no va cambiar,ya que pueden haber michos errores dentro de los datos, colisiones y futuros errores que nos vamos a querer evitar.

```javascript
const users =  [
  {
    isFollowing: false,
    name: 'Mauricio Martínez',
    userName: 'MauricioDMO'
  },
  {
    isFollowing: true,
    name: 'Miguel Ángel Durán',
    userName: 'midudev'
  }
]

export default function App() {
  return (
    <>
      {users.map(({isFollowing, userName, name})=>(
        <TwitterCard
        initialIsFollowing={isFollowing}
        userName={userName}
        name={name}
        key={userName}
        />
      ))}
    </>
  )
}

```

<br>

## useEffect
---

`useEffect(<func>, <dependecies>)` Se ejecuta una vez al montar el componente, si a este no le pasamos el parametro de las dependencias este se ejecutara cada vez que se renderice el componente.

El parametro de las dependencias es un array.

Si queremos que nuestro efecto solo se ejecute una vez tenemos que pasarle un array vacio al use effect.

```javascript
useEffect(() => {
  console.log('render')
}, [dependencia, uOtradependencia])
```

Las suscripciones las tenemos que limpiar, se le conoce como "cleanUseEffect".
Se devuelve una funcion se devuelve como limpiar el efecto, Esto se ejecuta siempre que se desmonta el componente (Se deja de renderizar) y tambien cuando cambian las dependencias, limpia el efecto anterior para asi poder ejecutar el nuevo efecto.

Si no se limpian las suscripciones el navegador empieza a saturarse y a ir mal.

Si se quire ver que las suscripciones van bien se puede ejecutar una funcion a la cual se le pasa el elemento al cual quieres ver los listeners que tiene:
(solo funciona en Chromiun)

`getEventListeners(<element>)`

El effect se ejecuta 2 veces por el modo estricto de react, este evalua si estas escribien mal o bien el codigo de react. Esto lo hace para que veas rapidamente los errores que podria tener el efecto.
En produccion el strictMode no tiene efecto alguno. 

```javascript
import { useState, useEffect } from 'react'

export default function FollowMouse () {
  const [enabled, setEnabled] = useState(false)
  const [position, setPosition] = useState({ x: 0, y: 0 })

  useEffect(() => {
    const handleMove = (e) => {
      const { clientX, clientY } = e
      setPosition({ x: clientX, y: clientY })
    }

    if (enabled) {
      window.addEventListener('pointermove', handleMove)
    }

    return () => {
      removeEventListener('pointermove', handleMove)
      setPosition({ x: 0, y: 0 })
    }
  }, [enabled])
}

```

<br>

## Como hacer un fetching
---

Tenemos que usar el useEffect, esto seria con .then():

```javascript
useEffect(() => {
    fetch(CAT_ENDPOINT_RANDOM_FACT)
      .then(res => res.json())
      .then(json => setFact(json.fact))
  }, [])
```

y con async await:

```javascript
useEffect(() => {
  async function getRandomFact () {
    const res = await fetch(CAT_ENDPOINT_RANDOM_FACT)
    const json = await res.json()
    setFact(json.fact)
  }

  getRandomFact()
}, [])
```

Es mas codigo y es mas recomendable el then.

Es buena prectoca que los efectos solo tengan una responsabilidad a la hora de ejecutar nuestro código.

Algo interesante es que tambien podemos separar la logica no solo los componentes.

lo mas intuitivo de separar la logica y pedor los datos requeridos como parametros esta mal.

Pasar los seteadores de los estados dentro de otro componenete, lo correcto es devolver lo que la funcion quiere hacer.
El estado no tiene que salir de donde se creo.

<br>

## Custom Hooks
---

Es reutilizar logica de nuestros componentes en diferentes componentes y para esto tenemos que abstraerlo en otro documento.

**Como se crean?**

Tenemos que crear a primera instancia una funcion que inicie con la palabra "use" ya que esto hara entender a react que es un custom hook.

La diferencia entre una fncion normal y una custom hook es que adentro de ella podemos utilizar los hooks de react.

```javascript
function useCatImage ({ fact }) {
  const [imageUrl, setImageUrl] = useState()

  useEffect(() => {
    if (!fact) return
    const threeFirstWords = fact.split(' ', 3).join(' ')

    fetch(`https://cataas.com/cat/says/${threeFirstWords}?size=50&color=red&json=true`)
      .then(res => {
        console.log(res)
        if (!res.ok) {
          throw new Error('No se pudo cargar la imagen.')
        }
        return res.json
      })
      .then(response => {
        const { url } = response
        setImageUrl(`https://cataas.com${url}`)
      })
  }, [fact])

  return { imageUrl }
}
```

Es muy recomendable nombrar los fact sin la implementacion que tienen dentrol, la incorrecta seria "useFetchCatFact", la forma correcta seria "useCatFact"

Siempre que se mira un useEffect en un componente en React es bueno cuestionarse si este no puede ser un custom hook.

Los custom hooks se utilizan para extraer logica de los componentes en resumen.

<br>

## Hacer Testing
---

Ejecutamos el siguiente comando:
`npm init playwright@latest`

Respondemos todas las preguntas.
Esto nos creara una carpeta llamada test y un ejemplo de test, eliminamos el ejemplo, nos metemos en la carpeta de test y nos vamos al example.spec.js

Este es el test mas importante, el end to end.

ver el final de [este video](https://www.youtube.com/watch?v=x-LcbVw99o8&list=PLUofhDIg_38q4D0xNWp7FEHOTcZhjWJ29&index=5)

(Tener Espacio En El Disco Principal)

<br>

## Frameworks CSS classless
---

Son estilos css sin clases

[Water.css](https://watercss.netlify.app/)
[Bolt.css](https://boltcss.com/)

<br>

## useRef
---

`useRef` crea una referencia de un elemento para poder conseguir "facilmente" sus valores u atributos.

Una referencia es un valor que persiste entre renderizados, al `useRef` podemos asignarle un valor y este sera siempre el mismo, a menos que accedamos y modifiquemos con `ref.current`.

Tambien se pueden usar como banderas, ya que en el primer render va a ser true la referencia y luego la podemos setear a false y nunca volvera a true, solo si se vuelve a cargar la pag.

Para poder hacer la refercia del elemento usamos el atributo `ref` en el elemento, y le pasamos el nombre que le asignamos a la referencia.

Un ejemplo:

```javascript
const inputRef = useRef()

const handleClick = (e) => {
  e.preventDefault()
  const inputElement = inputRef.current
  const value = inputElement.value
  console.log(value)
}


return (
  <form>
    <input ref={inputRef} />
    <button onClick={handleClick} >Buscar</button>
  </form>
)
```

Esta seria una forma incorrecta de usarlo ya que si tenemos 10 inputs tendriamos que crear 10 referencias...

una forma correcta pero sin usar `useRef` seria:

### Comprobar formularios

```javascript
const handleSubmit = (e) => {
    e.preventDefault()
    const data = new FormData(e.target)
    const query = data.get('query')
  }

return (
  <form className='form' onSubmit={handleSubmit}>
    <input name='query' placeholder='Avengers, Star Wars, The Matrix ...' />
    <button>Buscar</button>
  </form>
```

Esto usando el objeto FromData que nos obtiene diversas cosas del formulario, entre ellas todos los inputs nombrados dentro del formulario.

A este objeto le tenemos que pasar el elemento form al que queremos extraer los datos.
Al tener la instancia del objeto FormData tenemos un metodo el cual es `get(<name>)`, a este le pasamos el nombre del input al que queremos recuperar su valor.

Si usamos el `Object.fromEntries()` y le pasamos el valor de la instancia este nos devolvera un objeto que contendra los valores de los inputs nombrados, si no este objeto estara vacio.

Todo esto es accener a el formulario de forma no controlada (Esta recomenda midu), la manera controlada es que react gestione todo el proceso, cuando validar, que es lo que se escribe, como lo hace, todo esto lo hara con un estado.

Lo siguiente seria de forma controlada.

```javascript
const [query, setQuery] = useState('')

const handleChange = (e) => {
  setQuery(e.target.value)
}

return (
  <form className='form' onSubmit={handleSubmit}>
    <input onChange={handleChange} name='query' value={query} placeholder='Avengers, Star Wars, The Matrix ...' />
    <button>Buscar</button>
  </form>
)
```

El problema de esto es que en cada cambio del imput se vuelve a renderizar todo el componente/app

Las ventajas de ser controlado es que puedes evitar que escriba cosas que no quieres como que si inicia con el espacio no se actualice, o que si cimple ciertas condiciones salga un error, muchas cosas mas para la validacion de ese formulario en vivo.

Tambien esta el atributo `onInvalid={}` al cual le pasamos una funcion en la cual se ejecuta cuando el formulario es invalido.

<br>

## useMemo
---

Memoriza el contenido el valor de algo que ya hemos calculado, ya que si esto no se hace se estubiera haciendo tareas innesesareamente, este tiene dependencias como el `useEffect` pero estas cambian el valor de lo que hemos memorizado si cambian estas dependencias.

```javascript
const sortedMovies = useMemo(() => {
  return sort
    ? movies.toSorted((a, b) => a.title.localeCompare(b.title))
    : movies
}, [movies, sort])
```

Pero antes de usar use memo en todos los sitios es mejor asegurarse de que lo que queremos memorizar nos traera problemas de rendimiento.'

Tambien podemos memorizar funciones, para que no se vuelvan a crear tras cada renderizado.

Algunas funciones dependen de un valor externo, pero si no  le ponemos esse valor externo como dependencia no podra ejecutarse correctamente, pero en cambio se volvera a crear la funcion, lo que podemos hacer es que este valor externo se lo pasamos por parametros, de esta manera siempre estara actualizado el valor.

*Las dependencias funcionan igual a `useEffect`*

<br>

## useCallback
---

Es lo mismo que useMemo pero pensado para funciones, a este solo le tenemos que pasar la funcion ue queremos memorizar y listo.

En cambio el useMemo tenemos que retornar la funcion que queremos memorizar.

<br>

## Funcion Debounce desde cero
---

Al escribir en un formulario se consulta constantemente la Api, no queremos que al estar escribiendo pase esto, queremos q ue despues de un corto tiempo este se actualice solo, ya que si no pasa esto puede que la api tarde distintos tiempos en responder, y el valor de la ultima consulta resuelta sera el que nos mostrara. 

Ya hay pequeñas librerias que nos pueden solucionar este problema.

- lodash _.debounce(). metodo de libreria
- useDebounce, custom hook de react

Midu recoimienda la libreria de `just-debounce-it`

La instalamos con:

`npm i just-debounce-it -E`

[Documentacion](https://www.npmjs.com/package/just-debounce-it)

300ms Es una buena medida para el debounce, ya que de media se tarda de 100-250ms a escribir cada letra.


<br>

## useId
---

Un hook que crea un identificador unico ara un elemento, este nunca cambia y nos pueda servir para connectar elementos a travez de un id, ejemplo un label.

El identificador unico se genera por el orden de llamada de los elementos que hace react.

```javascript
const categoryId = useId()
```

<br>

## useContext
---

Los valores del contexto puede ser cualquier cosa, desde elementos estaticos o estados. 

Es algo que esta separado totalmente de nuestro arbol de componenetes pero que cualquier elemento puede acceder a el.

Tenemos que encerrar a todos los componentes que queremos que tengan acceso a este contexto.

Hay 3 pasos obligatorios del contexto

1. Crear el contexto.

2. Crear el Provider.

El cual delimita el rango a todos los elementos/componentes que englove nuestro Provider.

3. Consumir el contexto.

Importamos el contexto y lo usamos.



```javascript
import { createContext, useState } from 'react'

// 1 - Crear el contexto
export const FiltersContext = createContext()

// 2 - Crear el Provider
export function FiltersProvider ({ children }) {
  const [filters, setFilters] = useState({
    category: 'all',
    maxPrice: 2500
  })

  return (
    <FiltersContext.Provider value={
      { filters, setFilters }
    }>
      {children}
    </FiltersContext.Provider>
  )
}
```

En el Componente contexto.Provider le asignamos al atributo value los valores que queremos que sean accedidos a nuestro contexto.

Para delimitar y usar el Provider de nuestro contexto tenemos que encerrar los elementos a los que queremos que contengan el contexto.


En este caso sera la App completa:
```javascript
import { FiltersProvider } from './context/filters.jsx'

ReactDOM.createRoot(document.getElementById('root')).render(
  <FiltersProvider>
    <App />
  </FiltersProvider>
)
```

Ahora desde cualquier elemento hijo apartir del componente App tendra acceso a este contexto. 

```javascript
import { useContext } from 'react'
import { FiltersContext } from './context/filters'

// 3 - Consumir el contexto
const { filters, setFilters } = useContext(FiltersContext)
```

Siempre que se pueda se tiene que evitar tener un estado global / contexto.

Usar los contextos en el menor rango posible, entre mas pequeño el scope mejor sera.

<br>

## UseReducer
---

El `UseReducer` hace que el estado sema mas escalable y se pueda manerjar mas facilmente, este es una funcion la cual recibe el estado actual y la accion que tiene que hacer para, esta devulelve esl estado nuevo, este puede estar totalmente separado del componente del provider o del customhook.

Lo mas tipico para usar a la hora de distinguir la accion es un switch, pero se podria utilizar el `if else`.

```javascript
const reducer = (state, action) => {
  const { type: actionType, payload: actionPayload } = action

  switch (actionType) {
    case 'ADD_TO-CART': {
      const { id } = actionPayload
      const productInCart = state.findIndex(item => item.id === id)

      if (productInCart >= 0) {
        const newState = structuredClone(state)
        newState[productInCart].quantity += 1

        return newState
      }

      return [
        ...state,
        {
          ...actionPayload,
          quantity: 1
        }
      ]
    }

    case 'REMOVE_FROM_CART': {
      const { id } = actionPayload
      return state.filter(item => item.id !== id)
    }

    case 'CLEAR_CART': {
      return initialState
    }
  }

  return state
}
```

Esto es un ejemplo de como se utilizaria un reducer.

Se le pasa el estado a modificar, en este caso un array de elementos de un carrito (`state`), y la accion (`action`), que es un objeto que tiene el atributo type, que es un string diciendo la accion que queremos realizar ("ADD_TO_CART", "REMOVE_FROM_CART", "CLEAR_CART"), y un valor (`payload`) el cual queremos añadir o realizar una accion segun querramos, en este caso un elemento de nuestro ecommerce

Todo esto es para crear el `reducer`, ahora procederemos a ocuparlo.

Para esto usamos el hook `useReducer`, el cual e pasamos la funcion que creamos anteriormente y el estado inicial (lo definimos anteriormente) este no es un estado creado sino un simple valor.

```javascript
const [state, dispatch] = useReducer(reducer, initialState)
```

Esto parece una especie de useState, pero tenemos de segundo elemento un `dispatch` es cual es una funcion que se encrgara de enviar las acciones al reducer.

Quedaria de la siguiente forma:

```javascript
  const [state, dispatch] = useReducer(reducer, initialState)

  const addToCart = product => dispatch({
    type: 'ADD_TO_CART',
    payload: product
  })

  const removeFromCart = product => dispatch({
    type: 'REMOVE_FROM_CART',
    payload: product
  })

  const clearCart = () => dispatch({
    type: 'CLEAR_CART'
  })
```

**¿Por que o cuando vale la pena usar reducer?** <br>

Vale la pena porque hemos extraido la logica de actualizar el estado en una funcion separada.
Ademas de poder hacer test de los reducer sin la necesidad de renderizar nada.

cuando se tiene muchos useState encadenados, muchas vev=ces quiere decir que quieres actualizar cosas y podrias hacerlo mas facilmente si pones una accion que realice algo, como al escribir entonces se hara tal cosa.

Otra cosa muy intesezante es que puedes sacar el reducer fuera del customHook, context u componente creando una carpeta llamada `reducers` y creas tu propio reducer para luego importarlo.

Ya con mejores practicas como eliminando las magic strings quedaria de la siguiente manera en un archivo aparte.

```javascript
export const cartInitialState = []

export const CART_ACTION_TYPES = {
  ADD_TO_CART: 'ADD_TO_CART',
  REMOVE_FROM_CART: 'REMOVE_FROM_CART',
  CLEAR_CART: 'CLEAR_CART'
}

export const cartReducer = (state, action) => {
  const { type: actionType, payload: actionPayload } = action

  switch (actionType) {
    case CART_ACTION_TYPES.ADD_TO_CART: {
      const { id } = actionPayload
      const productInCart = state.findIndex(item => item.id === id)

      if (productInCart >= 0) {
        const newState = structuredClone(state)
        newState[productInCart].quantity += 1

        return newState
      }

      return [
        ...state,
        {
          ...actionPayload,
          quantity: 1
        }
      ]
    }

    case CART_ACTION_TYPES.REMOVE_FROM_CART: {
      const { id } = actionPayload
      return state.filter(item => item.id !== id)
    }

    case CART_ACTION_TYPES.CLEAR_CART: {
      return cartInitialState
    }
  }

  return state
}

```

Ademas de pasarlo a un doc aparte tambien podemos crear un custom hook para aun simplificarlo mas:

```javascript
function useCartReducer () {
  const [state, dispatch] = useReducer(cartReducer, cartInitialState)

  const addToCart = product => dispatch({
    type: CART_ACTION_TYPES.ADD_TO_CART,
    payload: product
  })

  const removeFromCart = product => dispatch({
    type: CART_ACTION_TYPES.REMOVE_FROM_CART,
    payload: product
  })

  const clearCart = () => dispatch({
    type: CART_ACTION_TYPES.CLEAR_CART
  })

  return { addToCart, removeFromCart, clearCart, state }
}

```
<br>

## React Router
---

Es una libreria que nos permite hacer rutas en nuestra aplicacion, es muy util para hacer SPA (Single Page Application).

`npm i react-router-dom -E`

React-router es simplemente lo principal de react-router-dom, pero react-router-dom tiene mas que son para utilizarlo en el navegador.

Para poder usarlo tenemos que envolver nuestra aplicacion con el componente `BrowserRouter` el cual nos permite usar las rutas.
Este lo tenemos que importar de `react-router-dom`.
Es preferible que este componente este en el main.jsx ya que asi todas las rutas que esten dentro de este componente tendran acceso a las rutas.

### Rutas

Ya en nuestro componente `App` importamos `Route` de `react-router-dom` y creamos las rutas que queremos que se renderizen y lo utilizamos de la siguiente manera.

```javascript
import { Route } from 'react-router-dom'

function App () {
  return (
    <div>
      <Route path='/'>
        <Home />
      </Route>
      <Route path='/about'>
        <About />
      </Route>
    </div>
  )
}
```

O tambien de la siguiente manera:

```javascript
import { Route } from 'react-router-dom'

function App () {
  return (
    <div>
      <Route path='/' element={<Home />}>
      <Route path='/about' element={<About />} />
    </div>
  )
}
```

Anteriormente se usaba el elemento `Switch` este funcionaba talcual un switch decidia de arriba para abajo cuel elemento se tenia que renderizar, este ya no se usa, ahora se usa el elemento `Routes` el cual es un contenedor de rutas, este tiene que estar dentro del `BrowserRouter`.

Quedando de la siguiente manera:

```javascript
import { Routes, Route } from 'react-router-dom'

function App () {
  return (
    <div>
      <Routes>
        <Route path='/' element={<Home />}>
        <Route path='/about' element={<About />} />
      </Routes>
    </div>
  )
}
```

### Link

Aunque esto paresca una SPA no lo es, ya que hace falta una manera de navegar entre paginas, para esto tenemos que usar el componente `Link` el cual nos permite navegar entre paginas.

En lugar de un `a` usamos un `Link` y en lugar de un `href` usamos un `to`.
Esto devido a que el `a` recarga la pagina y el `Link` no. Esto rerenderiza la pagina y no es lo que queremos.

```javascript
function App () {
  return (
    <>
      <header>
        <h1>Tu increible pagina</h1>
        <nav>
          <ul>
            <li><Link to='/'>Home</Link></li>
            <li><Link to='/search-page'>Search Page</Link></li>
          </ul>
        </nav>
      </header>
      <Routes>
        <Route path='/' element={ <Home /> } />
        <Route path='/search-page' element={ <SearchPage /> } />
        <Route path='*' element={ <h1>404</h1> } />
      </Routes>
    </>
  )
}
```

### Rutas dinamicas

Para hacer rutas dinamicas tenemos que usar el caracter `:` y el nombre de la variable que queremos que sea dinamica, esto en el elemento `Route`.

```javascript
function App () {
  return (
    <>
      <header>
        <h1>Tu increible pagina</h1>
        <nav>
          <ul>
            <li><Link to='/'>Home</Link></li>
            <li><Link to='/search-page'>Search Page</Link></li>
          </ul>
        </nav>
      </header>
      <Routes>
        <Route path='/' element={ <Home /> } />
        <Route path='/search-page' element={ <SearchPage /> } />
        <Route path='/movie/:id' element={ <Movie /> } />           // Ruta dinamica
        <Route path='*' element={ <h1>404</h1> } />
      </Routes>
    </>
  )
}
```

Para poder acceder a esta ruta dinamica tenemos que usar el hook `useParams` el cual nos permite acceder a los parametros de la ruta.

```javascript
import { useParams } from 'react-router-dom'

function Movie () {
  const { id } = useParams()

  return (
    <div>
      <h1>Movie {id}</h1>
    </div>
  )
}
```

### Rutas anidadas

Para hacer rutas anidadas tenemos que usar el elemento `Outlet` el cual nos permite renderizar las rutas hijas de la ruta padre.
Esto loque hce es decirle que en este lugar se renderizen las rutas hijas.

```javascript
import { Link, Outlet, Route, Routes, useParams } from 'react-router-dom'

const Product = () => {
  const { id } = useParams()
  return <>
    <h1>Product {id}</h1>
    <Link to='details'>Details</Link>
    <Outlet />
  </>
}

const ProductDetails = () => {
  const { id } = useParams()
  return <>
    <p>Product Details of product {id}</p>
    <Link to="../">close</Link>
  </>
}

function App () {
  return (
    <>
      <header>
        <h1>mauchollo 💵</h1>
        <nav>
          <ul>
            <li><Link to='/'>Home</Link></li>
            <li><Link to='/search-page'>Search Page</Link></li>
          </ul>
        </nav>
      </header>
      <Routes>
        <Route path='/' element={ <Home /> } />
        <Route path='/search-page' element={ <SearchPage /> } />
        <Route path='/product/:id' element={ <Product /> }>
          <Route path='details' element={ <ProductDetails /> } />
        </Route>
        <Route path='*' element={ <h1>404</h1> } />
      </Routes>
    </>
  )
}
```

> La seleccion de la ruta se hace dependiendo quien se considere que sea mas especifico sin importar el orden en el que se encuentren.
> La ruta /product/:id/details es menos especifica que /product/producto-1.

### Enlaces activos

Para los enlaces de una barra de navegacion existe un componente especifico de el react-router-dom el cual es `NavLink` el cual es un enlace que nos permite añadir clases si esta activo o no, si esta pendiente o se esta transicionando.

Por defecto el NavLink añade la clase `active` si esta activo, pero se puede cambiar con el atributo `activeClassName`.

Para añadir clases si un enlace esta activo se utiliza con el atributo `className` pero en lugar de un texto se le pasa una funcion que recibe un objeto con el atributo `isActive` el cual es un booleano que nos dice si esta activo o no.

El atributo `end` es para que solo se active si es exactamente esa ruta entonces se le pasa el valor de `true`.

```javascript
import { NavLink } from 'react-router-dom'

function App () {
  return (
    <>
      <header>
        <h1>Tu increible pagina</h1>
        <nav>
          <ul>
            <li><NavLink to='/' end>Home</NavLink></li>
            <li><NavLink to='/search-page'>Search Page</NavLink></li>
          </ul>
        </nav>
      </header>
      <Routes>
        <Route path='/' element={ <Home /> } />
        <Route path='/search-page' element={ <SearchPage /> } />
        <Route path='/movie/:id' element={ <Movie /> } />           // Ruta dinamica
        <Route path='*' element={ <h1>404</h1> } />
      </Routes>
    </>
  )
}
```

Podriamos añadir el los estilos un pointer-events: none; para que no se pueda hacer click en el enlace activo.

### Redirecciones

Para hacer redirecciones tenemos que usar el componente `Navigate` el cual nos permite hacer redirecciones.

```javascript
import { Navigate } from 'react-router-dom'

function App () {
  return (
    <>
      <header>
        <h1>Tu increible pagina</h1>
        <nav>
          <ul>
            <li><NavLink to='/' end>Home</NavLink></li>
            <li><NavLink to='/search-page'>Search Page</NavLink></li>
          </ul>
        </nav>
      </header>
      <Routes>
        <Route path='/' element={ <Home /> } />
        <Route path='/search-page' element={ <SearchPage /> } />
        <Route path='/movie/:id' element={ <Movie /> } />                       // Ruta dinamica
        <Route path='/movie/:id/details' element={ <MovieDetails /> } />        // Ruta dinamica
        <Route path='/movie/:id/*' element={ <Navigate to='/movie/:id' /> } />  // Redireccion 
        <Route path='/404' element={ <h1>404</h1> } />
        <Route path='*' element={ <Navigate to='404' /> } />                    // Redireccion
      </Routes>
    </>
  )
}
```

### Navegacion programatica

Para hacer una navegacion programatica tenemos que usar el hook `useNavigate` el cual nos permite hacer una navegacion programatica.

```javascript
import { useNavigate } from 'react-router-dom'

function App () {
  const navigate = useNavigate()

  const handleClick = () => {
    navigate('/search-page')
  }

  return (
    <>
      <header>
        <h1>Tu increible pagina</h1>
        <nav>
          <ul>
            <li><NavLink to='/' end>Home</NavLink></li>
            <li><NavLink to='/search-page'>Search Page</NavLink></li>
          </ul>
        </nav>
      </header>
      <Routes>
        <Route path='/' element={ <Home /> } />
        <Route path='/search-page' element={ <SearchPage /> } />
        <Route path='/movie/:id' element={ <Movie /> } />                       // Ruta dinamica
        <Route path='/movie/:id/details' element={ <MovieDetails /> } />        // Ruta dinamica
        <Route path='/movie/:id/*' element={ <Navigate to='/movie/:id' /> } />  // Redireccion 
        <Route path='/404' element={ <h1>404</h1> } />
        <Route path='*' element={ <Navigate to='404' /> } />                    // Redireccion
      </Routes>
    </>
  )
}
```

### Navigate state

El navigate tiene un atributo llamado `state` el cual nos permite pasarle un objeto con datos que queremos que se pasen a la ruta a la que estamos navegando.

No solo podemos pasarle un objeto, tambien podemos pasarle un string, un numero, un booleano, etc.
Y tambien `state` no es exclusivo de `Navigate` tambien lo podemos usar en `Link` y `NavLink`.

```javascript
import { useNavigate } from 'react-router-dom'

function App () {
  const navigate = useNavigate()

  const handleClick = () => {
    navigate('/search-page', { state: { from: 'home' } })
  }

  return (
    <>
      <header>
        <h1>Tu increible pagina</h1>
        <nav>
          <ul>
            <li><NavLink to='/' end>Home</NavLink></li>
            <li><NavLink to='/search-page'>Search Page</NavLink></li>
          </ul>
        </nav>
      </header>
      <Routes>
        <Route path='/' element={ <Home /> } />
        <Route path='/search-page' element={ <SearchPage /> } />
        <Route path='/movie/:id' element={ <Movie /> } />                       // Ruta dinamica
        <Route path='/movie/:id/details' element={ <MovieDetails /> } />        // Ruta dinamica
        <Route path='/movie/:id/*' element={ <Navigate to='/movie/:id' /> } />  // Redireccion 
        <Route path='/404' element={ <h1>404</h1> } />
        <Route path='*' element={ <Navigate to='404' state={} /> } />            // Redireccion
      </Routes>
    </>
  )
}
```

Con esto podemos pasar datos de una pagina a otra.
Con el hook `useLocation` podemos acceder a estos datos.
Este hook lo asignamos a una constante y esta constante tiene un atributo llamado `state` el cual es el objeto que le pasamos al navigate.

El hook por defecto devuelve la ruta en la que estamos.

```javascript
import { useLocation } from 'react-router-dom'

function SearchPage () {
  const { state } = useLocation()

  return (
    <div>
      <h1>Search Page</h1>
      <p>From: {state.from}</p> // from es parte del objeto que le pasamos al navigate
    </div>
  )
}
```