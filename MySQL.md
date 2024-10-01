- [MySQL](#mysql)
  - [Mostrar las bases de datos disponibles](#mostrar-las-bases-de-datos-disponibles)
  - [Crear y usar una base de datos](#crear-y-usar-una-base-de-datos)
  - [Tipos de datos](#tipos-de-datos)
  - [Crear una tabla](#crear-una-tabla)
  - [Mostar datos](#mostar-datos)
  - [Funciones](#funciones)
  - [Apodar nombres](#apodar-nombres)
  - [Condicionales](#condicionales)
    - [LIMIT](#limit)
  - [JOIN](#join)
    - [INNER JOIN](#inner-join)
  - [Editar tabla](#editar-tabla)
  - [Comentarios](#comentarios)
  - [Respaldar en consola](#respaldar-en-consola)
  - [Eliminar una base de datos](#eliminar-una-base-de-datos)
  - [Cambiar nombres](#cambiar-nombres)
  - [Añadir clave foranea](#añadir-clave-foranea)


# MySQL

## Mostrar las bases de datos disponibles

`show databases`

## Crear y usar una base de datos

Usamos la palabra reservada create, esta sirve para crear diversas cosas entre ellas una base de datos y tablas.

`create database clinica`
`use clinica`

## Tipos de datos

| Tipo de dato | Descripción                                                                                                                                                                                    |
| :----------: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|   TINYINT    | Un número entero que puede almacenar valores entre -128 y 127. Si se define como UNSIGNED (sin signo), puede almacenar valores entre 0 y 255.                                                  |
|   SMALLINT   | Un número entero que puede almacenar valores entre -32768 y 32767. Si se define como UNSIGNED (sin signo), puede almacenar valores entre 0 y 65535.                                            |
|  MEDIUMINT   | Un número entero que puede almacenar valores entre -8388608 y 8388607. Si se define como UNSIGNED (sin signo), puede almacenar valores entre 0 y 16777215.                                     |
|     INT      | Un número entero que puede almacenar valores entre -2147483648 y 2147483647. Si se define como UNSIGNED (sin signo), puede almacenar valores entre 0 y 4294967295.                             |
|    BIGINT    | Un número entero que puede almacenar valores entre -9223372036854775808 y 9223372036854775807. Si se define como UNSIGNED (sin signo), puede almacenar valores entre 0 y 18446744073709551615. |
|    FLOAT     | Un número de coma flotante que puede almacenar hasta siete dígitos decimales.                                                                                                                  |
|    DOUBLE    | Un número de coma flotante que puede almacenar hasta quince dígitos decimales.                                                                                                                 |
|   DECIMAL    | Un número decimal que puede almacenar hasta treinta dígitos decimales.                                                                                                                         |
|     DATE     | Una fecha en formato AAAA-MM-DD.                                                                                                                                                               |
|     TIME     | Una hora en formato HH:MM:SS.                                                                                                                                                                  |
|   DATETIME   | Una fecha y hora en formato AAAA-MM-DD HH:MM:SS.                                                                                                                                               |
|  TIMESTAMP   | Una marca de tiempo en formato AAAA-MM-DD HH:MM:SS.                                                                                                                                            |
|     YEAR     | Un año en formato AAAA.                                                                                                                                                                        |

<!-- ! Pendiente -->

<br>

## Crear una tabla
---


```console
create table pacientes (
  id_paciente int primary key auto_increment,
  nombres varchar(30) not null,
  apellidos varchar(30) not null,
  estado int(1) not null default 1,
  direccion varchar(200) default null,
  telefono varchar(8) default null,
  email varchar(40) default null,
  dui varchar(9) default null,
  creado datetime default current_timestamp(),
  modificado datetime default null,
) engine=InnoDB default charset=utf8;
```

<br>

## Mostar datos
---

Mostrar tablas.
`show tables from <database>` || `show tables`


<br>

## Funciones
---

|   Funcion   | descripcion                            |
| :---------: | -------------------------------------- |
| MIN(column) | Devuelve el valor minimo de la columna |
| MAX(column) | Devuelve el valor maximo de la columna |
| AVG(column) | Devuelve el promedio de la columna     |


<br>

## Apodar nombres
---

`SELECT column AS miColumna from table;`

o simplemente despues de la columna sin necesidad del `AS`

`SELECT column MiColumna from table;`

---

Tambien podemos apodar las tablas

`SELECT t.id, t.name nombre from table t;`


<br>

## Condicionales
---

En algunos de los condicionales se tendra que poner la palabra clave `WHERE` (donde) algunos de ellos son:

`<, >, <=, >=, <>, !=`

### LIMIT

Limitar la cantidad de resultados

<!-- ? Investicar HAVING -->


<br>

## JOIN
---

Reglas especiales para unir tablas

### INNER JOIN

Devuelve "La interseccion" de dos tablas.

`SELECT table1.id, table1.name, table2.name FROM table1 INNER JOIN table2 ON table1.id = table2.id;`

Podemos concatenar varios `INNER JOIN` despues de otro.

`select ct.name as ciudad, ct.population as poblacion, c.name `

<br>

## Editar tabla
---

No es necesario borrar una tabla para modificarla como era obvio.
Para esto usamos la siguiente palabra reservada `ALTER`

Añadir propiedades.
`ALTER TABLE departamentos ADD PRIMARY KEY (id_departamento)`
`ALTER TABLE nombre_tabla CHARACTER SET utf8;`

Añadir campo.
`ALTER TABLE nombre_tabla ADD COLUMN nombre_columna tipo_dato;`
`ALTER TABLE nombre_tabla ADD COLUMN columna1 tipo_dato, ADD COLUMN columna2 tipo_dato;` <!-- Varias columnas -->

Modificar un campo.
`ALTER TABLE nombre_tabla MODIFY COLUMN nombre_campo tipo_dato(longitud) valor_por_defecto auto_increment;`

`ALTER TABLE <table> ADD <propiedad> (<campo>);`

Podemos usar la palabra clave `AFTER <campo>` para decir que se inserte despues de un campo

Añadir charset a toda la base de datos.
`ALTER DATABASE nombre_base_datos CHARACTER SET utf8;`

<br>

## Comentarios
---

`--` Para despues de una linea
`#` Inicio de una linea
`/**/` Multilinea

<br>

## Respaldar en consola
---

`mysqldump -u root <database> > <name>.sql`

usar el respaldo:

`use <database>`
`source <pathToRestore>`

<br>

## Eliminar una base de datos
---

Para eliminar todos los registros de una tabla.
`TRUNCATE TABLE departamentos;`

Sin estar usando ni una base de datos.
`drop <nameDataBase>`

Cuando estamos usando una batabase
`drop database <nameDataBase>`

<br>

## Cambiar nombres
---

**De un campo**
`ALTER TABLE nombre_tabla CHANGE nombre_anterior_campo nombre_nuevo_campo tipo_dato;`

**De una tabla**
`RENAME TABLE nombre_actual TO nombre_nuevo;`

<br>

## Añadir clave foranea
---

`ALTER TABLE <tabla> ADD FOREIGN KEY (<campoAAñadirle>) REFERENCES <table> (<campoConLaLlave>)`


## Inner Join
---

Hacemos una interseccion de los datos de las 2 tablas

`SELECT * FROM table1 t1 INNER JOIN table2 t2 ON t1.id = t2.id`

LEFT y RIGHT JOIN es para darle una prioridad a un lado de la tabla, la primera es la izq y la segunda es la der.

Podemos encadenar multiples JOIN

```console
SELECT * FROM table1 t1
INNER JOIN table2 t2 ON t1.id = t2.id
INNER JOIN table3 t3 ON t2.id = t3.id
...
INNER JOIN tableN tN ON tn.id = tN.id
```


