- [Learning Astro!!](#learning-astro)
  - [Creando un proyecto](#creando-un-proyecto)
  - [Estructura](#estructura)
  - [Astro Pages](#astro-pages)
  - [Astro Extension](#astro-extension)
  - [Componentes](#componentes)
  - [Layouts](#layouts)
  - [Markdown](#markdown)
  - [Integraciones de Astro](#integraciones-de-astro)
  - [Renderizado condicional con directiva](#renderizado-condicional-con-directiva)
  - [404](#404)
  - [Rutas/paginas Dinamicas](#rutaspaginas-dinamicas)
  - [View Transitions](#view-transitions)
  - [Persistir informacion](#persistir-informacion)

# Learning Astro!!

<br>

## Creando un proyecto

Usamos el comando:

`npm create astro@latest`

Respondemos todas las preguntas que nos haga la instalacion.

<br>

## Estructura

.vscode/        # Configuracion de code
node_modules/   # Librerias de JS 
public/         # Archivos a que el navegador pueda acceder
src/            # Codigo de desarrollo
  pages/
  components/
  layouts/

<br>

## Astro Pages

Dento de la carpeta **pages** crearemos las distintas paginas con su correspodiente nombre.
Con el formato: `<name>.astro`

<br>

## Astro Extension

En el archivo **.astro** podemos escribir html (jsx) y al final del todo podemos usar la etiqueta style para darle los estilos a nuestro documento/componente, este no es global si no que es unico del componente en el que se escribe.

La estructura seria la siguiente:

```astro
// Codigo que pasara a ser estatico
---
const title = "Mi genial titulo!!!"
---

// HTML
<h1>{title}</h1>

// JS
<script>
const variable = 123 
</script>

// CSS
<style>
h1 {
  color: blue;
}
</style>
```

<br>

## Componentes

Se crea dentro de la carpeta `src` otra carpeta llamada `components`.

Y dentro de esta carpeta podemos crear todos nuestros componentes de astro nombrándolos como `<name>.astro` y podemos importarlos de la siguiente manera:

```astro
---
import MiComponente from '../components/MiComponente.astro'
---

<MiComponente/>
```

> Todo el css dentro de cada componente es aislado de todo el proyecto no tenemos que preocuparnos de que sobre escriban los estilos.

**Props** <br>

Astro nos otroga una variable global llamada `Astro` que podemos llamar para acceder a determinados valores

```astro
---
const {a, b, c} = Astro.props
---
``` 

Para pasar las propiedades se hace lo siguiente:

```astro
---
import Component from '../components/Component.astro'
---

<Component a="hola" b="Mundo" c="!!!" />
```

<br>

## Layouts

Creamos la carpeta `Layouts` dentro de `src` y podemos crear nuestro `Layout.astro`.

Dentro del Layout ponemos la etiqueta especial llamada `<slot/>` que sera lo que haya dentro de nuestra etiqueta Layout pasara a ser reemplazado por el `<slot/>`

Y dentro de este podriamos pasarle propiedades.

Ya teniendo nuestro componente vamos a ejemplificar como funcionan los slots:

```astro
<div>

  <slot name="before"> <!-- Nombramos el slot para poder colocar un elemento en este espacio -->
  <slot /> <!-- Donde se colocara el contenido por defecto -->
  <slot name="after">  <!-- Si colocamos elementos dentro del slot este sera el contenido por defecto -->
    <span class="default">Un texto por defecto</span>
  </slot>

</div>
```

<br>

## Markdown

Podemos usar markdown en astro por defecto.
Dentro de la carpeta `pages` podemos colocar nuestro markdown, astro soporta varias extensiones de archivo refiriéndose a markdown las cuales son:

- markdown
- md
- mdown
- mkdn
- mkd
- mdwn

Y podemos escribir dentro de de ese archivo normalmente markdown.

Podemos crear sub rutas creando simplemente carpetas dentro de `pages`

Si colocamos los 3 guiones al principio de un markdown se le conoce como meta informacion.
Este no puede ejecutar *JS* asi que tenemos que usar pares de clave valor.

Para inportar el Layout hacemos lo siguiente:

```markdown
---
layout: ../../Layouts/Layout.astro
---
```
> A esto se le conoce por frontmatter


Dentro de cada sub ruta/carpeta podemos colocar un `index.astro` para acceder a el directamente.

**Obtener Rutas de archivos** <br>

La variable Astro tiene un metodo que es para obtener todos los archivos de una carpeta este es `glob()` a este le pasamos una expresion regular para localizar los archivos.

Se utiliza asi:

```astro
---
const Archivos =  Astro.glob('./posts/*.md')
---
```

Esto devuelve un array de objetos que tiene diferentes métodos y atributos.

Podemos colocar un titulo a cada markdown asi como importamos el Layout.

Para acceder a esto cada objeto que nos devuelve `glob` tiene un objeto llamado `frontmatter` que tiene todas las variables que colocamos al markdown.

Quedaría de la siguiente forma: `archivo.frontmatter.title`

<br>

## Integraciones de Astro
---

Estas agregan nuevas funcionalidades a el proyecto.
Podemos usar React, Vue, Svelte, Solid, y más.
Integrar herramientas como Tailwind.
Agregar funcionalidades como la generación de sitemaps.

correcciones ortográficas

Para poder integrar React usamos el comando: `npx astro add react`

Claro pero *Astro* no devuelve js por defecto en nuestros componentes, por eso hay unos marcadores que tenemos que usar en nuestros componentes para decirle cuando lo va a ejecutar y/o descargar el codigo js.

Estos marcadores se les reconoce como directivas:

- `client:idle`
- `client:load` Cuando cargue la pagina se descargara
- `client:media` 
- `client:only`
- `client:visible` Cuando vaya a ser visible el componente descarga.

Esto es para componentes, pero tambien hay directivas para estilos y esta es `is`:

- `is:global` Para que se apliquen los estilos en todo el documento.
- `is:inline` Para dejar el estilo en el html
- `is:raw` Procesa y lo convierte a un archivo *css* aparte. **Defecto**

Estos se aplican en las etiquetas o componentes de la siguiente manera:

```astro
---
import {MiComponente} from '../compoments/Micomponente.astro'
---

<MiComponente client:visible>

<style is:global>
:root {
  font-size: 16px;
}
</style>
```

<br>

## Renderizado condicional con directiva
---

Podemos utilizar una directiva para poder ahorrarnos un poco de logica y hacer el renderizado mas declarativo.

Existe una directiva para las clases llamada `:list` a el cual le pasamos un array con strigs u objetos que seran nuestras clases se utiliza de la siguiente forma:

```astro
---

const miCondicional = True

---
<div
class:list={[
  'clase1 clase2',
  {
    "clase3 clase4": miCondicional,  // Dependiendo de nuestro condicional siendo true se renderizara el atributo
    "Clase5 clase6": !miCondicional
  }
]}
>
  Mi querido texto
</div>

```

<br>

## 404
---

Podemos crear un 404 muy pero muy facilmente, simplemente nombrando un documento de astro `404.astro` en la carpeta `pages`, funciona como una pagina normal solo que se mostrara cuando no exista una pagina.

<br>

## Rutas/paginas Dinamicas 
---

Estas se crean colocando entre corchetes la variable con la que queremos crear/nombrar las paginas dinamicas, esto se haria de la siguiente forma: `[id].astro`

Esta pagina recibira como parametro la id con la que queremos generara dinamicamente.

Pero esto para ser estatico necesita que le pasemos todas las rutas que seran posibles acceder, esto se hace exportando una funcion que la llamaremos *getStaticPaths*.

Esta debe devolver un array de objetos que contengan los parametros que queremos usar en la pagina este quedaria de la siguiente forma:

```javascript
[
  {parans: {id: '138472asd33'}},
  {parans: {id: '82w37rwef38'}}
]
```

<br>

## View Transitions
---

Solo tenemos que importar en el *Layout* (ya que queremos que conecte/afecte a todas nuestras paginas) importamos `ViewTransitions` desde `astro:transitions`, luego usamos el componente en el `<head>` del layout, quedaria de la siguiente manera:

```astro
---
import { ViewTransitions } from 'astro:transitions'
---

<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mis Grandiosas Notas</title>
  <ViewTransitions>
</head>
<body>
  <slot>
</body>
</html>

```

<br>

## Persistir informacion
---

Podemos persistir informacion entre paginas usando la directica `transition:persist` en nuestro elemento u componente, para que este persista su estado/informacion entre paginas.

Pero para esto tenemos que tener importado las `ViewTransitions`

```astro
---
import { MiComponente } from '../compoments/MiComponente.jsx'
---

<MiComponente transition:persist client:visible />

```

