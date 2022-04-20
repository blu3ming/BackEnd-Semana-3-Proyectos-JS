# I Crear nuevo proyecto de JS

1. Crea un directorio vacío llamado `my_launchx_app`.
2. Dentro de este directorio vacío ejecuta el comando `npm init`. Este ejecutara un cliente que te preguntará algunos datos de tu proyecto. Es indiferente esta información de momento, puedes darle `enter` hasta que termine. Al finalizar te creará el archivo `package.json`. A partir de ahora nuestro directorio es un proyecto de JS. (Así se crea desde cero.) **Recuerda siempre VERSIONAR tus apps.**

# II Agregar dependencias

> Una vez que se creó un proyecto de js, podemos proceder a agregar dependencias, es decir, bibliotecas de js que nos ayudarán a hacer ciertas acciones.

1. Vamos a agregar pruebas de unidad a nuestro proyecto recién creado. Para ello es necesario rectificar que tenemos ya el archivo `package.json`.
2. Para agregar una dependencia, se necesita indicar directamente en el `package.json`, este archivo es el corazón de cualquier app de js. Podemos hacer uso de un comando de npm para agregar la última versión de cualquier dependencia: `npm install --save-dev jest`. (Esto indica que se agrega la dependencia `jest`, y que se agrega para el ambiente de desarrollo `--save-dev`). 
3. Verifica que después del punto anterior, se haya creado un directorio `node_modules`, este contiene todos los scripts de js de las dependencias. IMPORTANTE NUNCA VERSIONAR ESTO. Para no versionar esta carpeta, crea en la RAÍZ de tu proyecto un archivo llamado `.gitignore` y agrega la siguiente línea: `**/node_modules
`, con esto vamos a decirle a git que excluya este directorio.

# III Creación de una clase y modularización 

> Diseña una clase y realiza una prueba de unidad de la creación de un objeto de esta clase.

4. Crea dos directorios llamados `app` y `test`. 
5. En el directorio `app` crea un archivo llamado `missionCommander`. Crea una clase llamada `MissionCommander`, junto a un constructor que reciba un parámetro y lo agregue en el atributo `name`. No olvides exportar esta clase:

```js
class MissionCommander {
  constructor (name) {
    this.name = name
  }
}

// Esta línea nos permite exportar nuestra clase
module.exports = MissionCommander
```

6. Crea un archivo en la raíz de tu proyecto que se llame `index.js`. Este será el archivo principal de este proyecto.

7. En el archivo `index.js` importa tu clase, instancia al menos tres objetos e imprime los atributos `name` de todos.

`index.js`
```js
const MissionCommander = require('./app/missionCommander');
const carlo = new MissionCommander("Carlo")
console.log(carlo.name)
```

8. Ve al archivo `package.json`, debajo de la línea de `"scripts":{` agrega la siguiente línea:

```js
"start": "node index.js"
```

Con esto vamos a habilitar el comando `npm start` para que al llamarlo ejecute `node index.js`. 

9. Ahora en tu línea de comando ejecuta `npm start` y verifica que imprima lo que necesitas.

# IV. Agregar una prueba de unidad de tu clase

10. En la carpeta de `test` agrega un archivo llamado `missionCommander.test.js`.
11. En este archivo agrega lo siguiente (esta es una prueba básica de Jest):

```
describe("Esto es una suite de pruebas", () => {
  test('Caso de prueba 1', () => {
    const result = 1 + 2 
    expect(result).toBe(10);
  });
})

```

12. Ve a tu archivo `package.json`, y modifica la línea que inicia con `"test"` por:

```
Para Linux:
"test": "node ./node_modules/.bin/jest"

Para Windows:
"test": "node --experimental-vm-modules ./node_modules/jest/bin/jest.js"
```

1.  Corre la prueba que acabas de crear:

```
npm test  test/missionCommander.test.js
```

Verifica que esta prueba este tronando ya que lo que indicamos en el ejemplo es un caso que debe fallar. Modifica este archivo sustituyendo `10` por `3` y vuelve a correr tu prueba, verifica que ahora no haya fallos.

1.  En tu prueba de unidad `test/missionCommander.test.js`, al inicio en la línea #1 importa tu clase:

```
const MissionCommander = require('./../app/missionCommander');
```

Vamos a agregar una prueba de unidad para probar esta clase.

15. Modifica las descripciones de la prueba:

```
describe("Unit Tests for Mission Commander Class", () => {
  test('1) Create a mission commander objet', () => {
```

16. Ahora instancia un objeto de la clase importada:

```
const myMissionCommander = new MissionCommander("Woopa")
```

17. En la línea donde se usa `expect`, en el primer parámetro agrega la propiedad que quieres probar, el siguiente paréntesis es para indicar el valor que esperas obtener.

```
expect(myMissionCommander.name).toBe("Woopa");
```

18. Ejecuta la prueba nuevamente, y verifica que no haya fallos.