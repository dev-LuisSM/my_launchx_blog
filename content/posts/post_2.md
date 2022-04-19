---
title: "Backend: Semana 1 🚀"
date: 2022-04-19
description: 'Primera semana en la misión Backend: Exportación de módulos'
---

Llevo unos días sin escribir en el blog debido a que no se me ha hecho costumbre, pero nunca es tarde para volver a iniciar. :)
La primera semana en la misión Backend fue una gran semana de inicio, para retomar un poco las clases y objetos que ví en la universidad así como un tema nuevo **Exportación de módulos con CommonJS y ESM(EcmaScript Modules)**

## Un vistazo rápido a los objetos

Los objetos en Javascript como en otros lenguajes, se pueden comparar con objetos de la vida real.
MDN nos [menciona](https://developer.mozilla.org/es/docs/Web/JavaScript/Guide/Working_with_Objects) que 'En JavaScript, un objeto es un entidad independiente con propiedades y tipos'. 
Los objetos son bastante útiles a la hora de programar y de obtener o crear información, hay diversas maneras de tratar con ellos y dependiendo de lo que se necesite hacer.

### ¿Cómo crear un objeto?
Un objeto se conforma de dos partes, una **llave** y un **valor**. En nuestro ejemplo de abajo se puede visualizar de manera simple:
```
const fruits = {
  // "key": "value" <-- Sintaxis
  
  "fruit": "🍎",
  "fruit_bowl": ["🍊", "🍍", "🍓"],
  "favorite_fruits": {
    "me": "🍑",
    "mySister": "🍐",
    "myBrother": "🥝"
  }
}
```
Las llaves son quienes contienen el valor, múltiples valores y objetos (con más llaves y valores).

### ¿Qué hay sobre las clases?
Hablar de clases en algún lenguaje de programación es hablar de Programación Orientada a Objetos.

Las clases fueron introducidas a Javascript con ECMAScript 2015, la sintaxis es muy similar a un objeto, además de ser una manera más fácil de lidiar con herencia.
A la hora de hacer una clase, se necesita crear un constructor donde se recibirán ciertos parámetros.

```
class car = {
  constructor(make, model, year){
    this.make = make
    this.model = model
    this.year = year
  }
}
```
Para instanciarlo (o llamarlo), se realiza el siguiente código

```
const myCar = new car('Nissan', 'Versa', 2015)

```
En el post de la semana 2 hablaré más sobre clases y objetos debido a que es un tema bastante grande.

## Exportación de módulos
### CommonJs (CJS)

CommonJs fue creado en el 2009 para poder trabajar Javascript con Node fuera del navegador (por lo cuál, no se puede soportar en estos mismos pero sí en aplicaciones de escritorio o servidores).

Al utilizar CommonJs se deben de tomar en cuenta dos palabras reservadas **exports** y **require**.

- exports: Como lo sugiere su nombre, sirve para exportar cierto código que quieres reutilizar en algún otro archivo de Js.
- require: Es la forma de importar el código anteriormente exportado.

Esto es muy utilizado para importar módulos exportados desde node_modules.

Ejemplo de cómo utilizar CJS:
```
// class.js

class Pokemon { /* ... */ }
module.exports = Pokemon


// module.js

method(){ /* ... */ }
module.exports = method()


// main.js

const Pokemon = require('./class.js')   // Importando módulo clase
const imported_module = require('./module.js')  // Importando otro módulo sin clase

const pikachu = new Pokemon('') // <-- Instanciando clase
imported_module.method() // Llamando método del módulo

```

### EcmaScript Modules (ESM)

ESM vino con la creación de EcmaScript 2015 (ES6) y junto con ello, una manera de traer módulos dentro de los navegadores más fácil.
Esta manera de exportar módulos es utilizado por diversos frameworks.

Al igual que CJS tiene dos palabras reservadas importantes **export** e **import**.

- export: De igual manera, exporta las clases, médotos o variables que se desean trabajar en otros archivos Js.
- import: Se encarga de importar las exportaciones.
- default: Esto se escribe después de export, su función es para exportar únicamente ese método, clase o variable de todo el archivo

La manera de utilizarlos es la siguiente:

```
// class.js
export default class Pokemon { /* ... */ }
dummyFunction() { /* ... */ }

// module.js
export const number = 384
export const method = () => console.log('Hello')
export const otherNumber = 40

// index.js
import MyPokemon from './pokemon.js'

import { number, method } from './module.js' // Para exportar codigo en específico)
// import * as utils from './module.js' // Para exportar todo el código que tiene la palabra "export" en el módulo

```

Para finalizar, he de decir que al inicio me revolví con el tema a la hora de trabajarlo ya que sin querer conocía la forma de exporat ESM y pensé que era la única manera, pero llegó CJS y tuve problemas con node.js, por lo cual, recomiendo bastante revisar este [artículo](https://lenguajejs.com/automatizadores/introduccion/commonjs-vs-es-modules/).

La semana dos será más específica sobre los objetos, clases y algunos otros métodos para tratarlos, mientras tanto, buen día. :)
