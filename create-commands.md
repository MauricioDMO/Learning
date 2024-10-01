Aprender como funciona doskey/batch

doskey commandName=path\to\file.bat
setx PATH "%PATH%;ruta_del_archivo"

# Parametros / Argumentos

Para pasar argumentos en un archivo bat, puedes usar el signo %
seguido de un número del 1 al 9 para permitir pasar parámetros.
Por ejemplo, si tienes un archivo saludo.bat con la línea `echo Hola %1`,
si lo invocas tecleando archivo.bat jose, presentará en pantalla Hola jose

Se pude seguir encadenando todos los que se quiera.

if "%1"=="" (
    echo El argumento es requerido.
    goto :eof // Manda al final del batch: terminar ejecucion
)

// doskey /macrofile=path\to\file.bat

# Condicionales

if [not] ERRORLEVEL <número> comando [else expresión]
if [not] <cadena1>==<cadena2> comando [else expresión]
if [not] exist <nombre_archivo> comando [else expresión]

if condición1 (
    comando1
) else if condición2 (
    comando2
) else (
    comando3
)

## Ejecucion condicional

&: command1 & command2. Se usa para ejecutar el primer comando y después el segundo.
&&: command1 && command2. Se ejecuta el primer comando y solo se ejecuta el segundo si el primero termina con éxito.
||: command1 || command2. Se ejecuta el primer comando y ejecuta el segundo únicamente si el primero no termina con éxito1

# "Funciones"

goto <funcion> para ir a una funcion o mejor dicho a la parte de codigo.

Para declarar una funcion o nombrer una parte del codigo se utiliza el prefijo de :

`:<funcion>`

pata ir al final del archivo usamos `:eof`
