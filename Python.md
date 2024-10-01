# Variables

x, y, z = "Naranja", "Banana", "Cereza"

## Constantes

*Todo en mayusculas*
```python
PI = 3.1416
```

## Convenciones

| Convencion | Descripcion |
| ---------- | ----------- |
| snake_case | Variables   |
| PascalCase | Clases      |
| camelCase  | Funciones   |

# Recibir valores en terminal
res = input("")

# Tipando variables?

Python es un lenguaje de tipado dinamico
No se especifica el tipo
de dato
Para esto se necesita un linter que nos ayude a identificar errores de tipado y demas

adress: str = "Calle 123"

# Comparaciones alfabeticas

print("abb" >= "aaa")
print("abb" >= "abc")

# operadores logicos

print(True and True)
print(True or False)
print(not True)

# Caracteres especiales

| Caracter | Descripcion |
| -------- | ----------- |
| \n       | Nueva linea |
| \t       | Tabulador   |
| \b       | Retroceso   |
| \r       | Retorno     |
| \\       | Backslash   |

# Operadores de asignacion

| Operador | Descripcion |
| -------- | ----------- |
| =        | Asignacion  |
| +=       | Suma        |
| -=       | Resta       |
| *=       | Multiplicar |
| /=       | Dividir     |
| %=       | Modulo      |
| //=      | Piso        |
| **=      | Exponente   |

```python
x = 5
x += 3
print(x) # 8

x = 5
x -= 3
print(x) # 2

x = 5
x *= 3
print(x) # 15

x = 5
x /= 3
print(x) # 1.6666666666666667

x = 5
x %= 3
print(x) # 2
```

# formateo de strings

```python
age = 36
txt = "My name is John, and I am {}"
print(txt.format(age))

quantity = 3
itemno = 567
price = 49.95
pieces = "pieces"
print("I want %d %s of item %d for %.2f dollars." %(quantity, itemno, price))

print(f"I want {quantity} {pieces} of item {itemno} for {price} dollars.")
```

# Divicion de strings

```python
txt = "hello, my name is Peter, I am 26 years old"
x = txt.split(", ")
print(x) # ['hello', 'my name is Peter', 'I am 26 years old']

print(txt[0:5]) # hello
print(txt[7:17]) # my name is
print(txt[-3:-1]) # ol
print(txt[7:]) # my name is Peter, I am 26 years old
print(txt[:5]) # hello
print(txt[-5:]) # years old
print(txt[::2]) # hlo ynm sPte a 6yasod
print(txt[::-1]) # dlo sraey 62 ma I ,reteP si eman ym ,olleh
```

# Funciones de strings

| Funcion        | Descripcion                                                        |
| -------------- | ------------------------------------------------------------------ |
| capitalize()   | Convierte el primer caracter en mayuscula                          |
| lower()        | Convierte todo el string en minuscula                              |
| upper()        | Convierte todo el string en mayuscula                              |
| swapcase()     | Convierte las mayusculas en minusculas y viceversa                 |
| title()        | Convierte la primera letra de cada palabra en mayuscula            |
| strip()        | Elimina los espacios en blanco al inicio y al final                |
| replace()      | Reemplaza un string por otro                                       |
| split()        | Divide el string en subcadenas                                     |
| count()        | Cuenta cuantas veces aparece un caracter en el string              |
| find()         | Busca un caracter en el string y devuelve la posicion              |
| startswith()   | Devuelve True si el string empieza con el caracter especificado    |
| endswith()     | Devuelve True si el string termina con el caracter especificado    |
| isalnum()      | Devuelve True si todos los caracteres son alfanumericos            |
| isalpha()      | Devuelve True si todos los caracteres son alfabeticos              |
| isdecimal()    | Devuelve True si todos los caracteres son decimales                |
| isdigit()      | Devuelve True si todos los caracteres son digitos                  |
| isidentifier() | Devuelve True si el string es un identificador                     |
| islower()      | Devuelve True si todos los caracteres estan en minuscula           |
| isnumeric()    | Devuelve True si todos los caracteres son numericos                |
| isspace()      | Devuelve True si todos los caracteres son espacios                 |
| istitle()      | Devuelve True si el string sigue las reglas de un titulo           |
| isupper()      | Devuelve True si todos los caracteres estan en mayuscula           |
| join()         | Une una lista de strings en un solo string                         |
| ljust()        | Devuelve un string justificado a la izquierda                      |
| rjust()        | Devuelve un string justificado a la derecha                        |
| center()       | Devuelve un string centrado                                        |
| lstrip()       | Devuelve un string con los espacios en blanco al inicio eliminados |
| rstrip()       | Devuelve un string con los espacios en blanco al final eliminados  |
| partition()    | Devuelve una tupla donde el string es separado en tres partes      |
| rpartition()   | Devuelve una tupla donde el string es separado en tres partes      |
| maketrans()    | Devuelve una tabla de traduccion                                   |
| translate()    | Devuelve un string traducido                                       |
| zfill()        | Rellena el string con ceros a la izquierda                         |
| format()       | Formatea el string                                                 |
| format_map()   | Formatea el string                                                 |
| encode()       | Devuelve un string codificado                                      |
| expandtabs()   | Establece el tamaño de la tabulacion                               |


