- [Learning Astro!](#learning-astro)
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
  - [Rutas/paginas Dinámicas](#rutaspaginas-dinámicas)
  - [View Transitions](#view-transitions)
  - [Persistir información](#persistir-información)

# Learning Astro!

<br>

## Creando un proyecto

Usamos el comando:

`npm create astro@latest`

Respondemos todas las preguntas que nos haga la instalación.

<br>

## Estructura

.vscode/        # Configuración de code
node_modules/   # Librerías de JS 
public/         # Archivos a que el navegador pueda acceder
src/            # Código de desarrollo
  pages/
  components/
  layouts/

<br>

## Astro Pages

Dentro de la carpeta **pages** crearemos las distintas paginas con su correspondiente nombre.
Con el formato: `<name>.astro`

<br>

## Astro Extension

En el archivo **.astro** podemos escribir html (jsx) y al final del todo podemos usar la etiqueta style para darle los estilos a nuestro documento/componente, este no es global si no que es único del componente en el que se escribe.

La estructura seria la siguiente:

```astro
// Código que pasara a ser estático
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

Astro nos otorga una variable global llamada `Astro` que podemos llamar para acceder a determinados valores

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

Y dentro de este podríamos pasarle propiedades.

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

Si colocamos los 3 guiones al principio de un markdown se le conoce como meta información.
Este no puede ejecutar *JS* asi que tenemos que usar pares de clave valor.

Para importar el Layout hacemos lo siguiente:

```markdown
---
layout: ../../Layouts/Layout.astro
---
```
> A esto se le conoce por frontmatter


Dentro de cada sub ruta/carpeta podemos colocar un `index.astro` para acceder a el directamente.

**Obtener Rutas de archivos** <br>

La variable Astro tiene un método que es para obtener todos los archivos de una carpeta este es `glob()` a este le pasamos una expresión regular para localizar los archivos.

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

Estas agregan nuevas funcionalidades a el proyecto.
Podemos usar React, Vue, Svelte, Solid, y más.
Integrar herramientas como Tailwind.
Agregar funcionalidades como la generación de sitemaps.

correcciones ortográficas

Para poder integrar React usamos el comando: `npx astro add react`

Claro pero *Astro* no devuelve js por defecto en nuestros componentes, por eso hay unos marcadores que tenemos que usar en nuestros componentes para decirle cuando lo va a ejecutar y/o descargar el código js.

Estos marcadores se les reconoce como directivas:

- `client:idle`
- `client:load` Cuando cargue la pagina se descargara
- `client:media` 
- `client:only`
- `client:visible` Cuando vaya a ser visible el componente descarga.

Esto es para componentes, pero también hay directivas para estilos y esta es `is`:

- `is:global` Para que se apliquen los estilos en todo el documento.
- `is:inline` Para dejar el estilo en el html
- `is:raw` Procesa y lo convierte a un archivo *css* aparte. **Defecto**

Estos se aplican en las etiquetas o componentes de la siguiente manera:

```astro
---
import {MiComponente} from '../components/MiComponente.astro'
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

Podemos utilizar una directiva para poder ahorrarnos un poco de lógica y hacer el renderizado mas declarativo.

Existe una directiva para las clases llamada `:list` a el cual le pasamos un array con strings u objetos que serán nuestras clases se utiliza de la siguiente forma:

```astro
---

const miCondicional = True

---
<div
class:list={[
  'clase1 clase2',
  {
    "clase3 clase4": miCondicional,  // Dependiendo de nuestro condicional siendo true se renderizará el atributo
    "Clase5 clase6": !miCondicional
  }
]}
>
  Mi querido texto
</div>
```

<br>

## 404

Podemos crear un 404 muy pero muy fácilmente, simplemente nombrando un documento de astro `404.astro` en la carpeta `pages`, funciona como una pagina normal solo que se mostrara cuando no exista una pagina.

<br>

## Rutas/paginas Dinámicas

Estas se crean colocando entre corchetes la variable con la que queremos crear/nombrar las paginas dinámicas, esto se haría de la siguiente forma: `[id].astro`

Esta pagina recibirá como parámetro la id con la que queremos generara dinámicamente.

Pero esto para ser estático necesita que le pasemos todas las rutas que serán posibles acceder, esto se hace exportando una función que la llamaremos *getStaticPaths*.

Esta debe devolver un array de objetos que contengan los parámetros que queremos usar en la pagina este quedaría de la siguiente forma:

```javascript
[
  {params: {id: '138472asd33'}},
  {params: {id: '82w37reef38'}}
]
```

<br>

## View Transitions

Solo tenemos que importar en el *Layout* (ya que queremos que conecte/afecte a todas nuestras paginas) importamos `ViewTransitions` desde `astro:transitions`, luego usamos el componente en el `<head>` del layout, quedaría de la siguiente manera:

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

## Persistir información

Podemos persistir información entre paginas usando la directica `transition:persist` en nuestro elemento u componente, para que este persista su estado/información entre paginas.

Pero para esto tenemos que tener importado las `ViewTransitions`

```astro
---
import { MiComponente } from '../components/MiComponente.jsx'
---

<MiComponente transition:persist client:visible />

```

