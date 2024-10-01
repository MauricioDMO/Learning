# Instalando y configurando ESlint



Una vez iniciado el proyecto podemos usar el siguiente comando para ejecutar la configuracion de eslint:
`npm init @eslint/config`

Tenemos que ir a la raiz del proyecto y descargar standard como dependencia de desarrollo.
`npm install standard -D`

Ahora en el package.json escribimos en la raiz:

```json
"eslintConfig": {
    "extends": ["standard"]
}
```