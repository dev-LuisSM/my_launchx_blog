---
title: "Backend: Semana 2 🚀"
date: 2022-04-26
description: 'Segunda semana en la misión Backend: Más objetos, más clases y testing'
---

Hola de nuevo, hace unos días terminé la segunda semana de backend, la razón por la que escribo apenas son dos: Aún no me acostumbro a escribir semanalmente y puse en práctica estos temas en el trabajo.

## Aún más objetos y clases
En el post anterior, hablé sobre como crear una clase y objeto, que tienen ciertas similitudes pero hay más de ello.

### Métodos en objetos
Los métodos en los objetos son bastante útiles para tratar y retornar dartos previamente tratados o que simplemente se necesitan a la hora de utilizar esta información, la sintaxis es básica, agregando una llave y la función tomará el rol del valor devuelto:

```
const persona = {
    name: 'Luis',
    sayHello: function (){
        console.log(`Hola, soy ${this.name}`)
    }
}

persona.sayHello()
```
Así es como un método es utilizado con objetos.

### Métodos en clases, get y set, static, herencia y override 
Aun que comparten ciertas similitudes los objetos y clases, en este caso, los métodos son declarados como tal. Vimos en el post anterior que para crear una clase se necesita crear un constructor, bien, pues este constructor únicamente se encargará de establecer los datos o algunos datos.

Los métodos son creados fuera de este constructor, la sintaxis es la siguiente:

```
class PullRequest {
    constructor(repo, title, lines_changed) {
        this.repo = repo
        this.title = title
        this.lines_changed = lines_changed
        this.status = "OPEN"
        this.dateCreated = new Date()
    }

    getInfo (){
        return `This PR in the repo: ${this.repo} is (status ${this.status}) and was created on ${this.dateCreated}`
    }
}
```
Estos métodos al igual que en los objetos, se utilizan para tratar la información (en este caso) de la clase y la forma de mandar a llamar este método es la siguiente:
```
const myFirstPR = new PullRequest("LaunchX", "Mi primer PR", 105) // Instanciamos la clase
console.log(myFirstPR.getInfo()) // Una vez instanciado, se llama la función
```

### Getters y Setters
Los getters y setters son utilizados en cualquier lenguaje de programación que utiliza POO, como lo sugiere su nombre, se encargan de obtener (get) y establecer (set) datos.

```
class MissionCommander {
    constructor(name, mission){
        this.name = name
        this.mission = mission
        this.students = 0
        this.lives = 0
    }

    get getStudents(){
        return this.students
    }

    get getLives(){
        return this.lives
    }

    set setStudent(students){
        this.students = students
    }
    
    set setLives(lives){
        this.lives = lives
    }
}
```
**Set:** Basándonos en el ejemplo de arriba, 'set' es una palabra reservada que viene antes del método, se encarga que una vez instanciado el objeto ciertos parámetros puedan ser actualizados (esto debido a que no es correcto dejar algúna propiedad vacía, es mejor establecer un 0 o un "").
En la clase de MissionCommander, podemos observar que this.students y this.lives están en 0; una vez instanciado el objeto se podrá actualizar este número.

**Get:** Al igual que set, 'get' es una palabra reservada que viene antes del método, su trabajo es básicamente retornar un valor en específico con una simple línea 'return this.propiedad'. No es necesario establecer antes o después el set de alguna propiedad.
```
const MC = new MissionCommander("Carlo", "NodeJs")
console.log("Antes de los setters: ")
console.log("Students:",MC.getStudents) // 0 por default
console.log("Lives:",MC.getLives) // 0 por default

MC.setLives = 3
MC.setStudent = 100

console.log("Después de los setters: ")
console.log("Students:",MC.getStudents) // 100 students
console.log("Lives:",MC.getLives) // 3 lives
```

### Static (métodos estáticos)
Los métodos estáticos en pocas palabras, son funciones que pueden ser llamadas sin tener que instanciar una clase como tal, inclusive, lleva a fallar si se instancia. 
```
class Toolbox {
    static getUsefulTools(){
        return ["Command Line", "Git", "Text Editor"]
    }
}
console.log(Toolbox.getUsefulTools)

// Si se instancia, falla
// const toolbox = new Toolbox()
// console.log(toolbox.getMostUsefulTools()) // is not a function
```
*Nota: No confundir con clases estáticas.*

### Herencia y override
**Herencia** un tema que a algunas personas se les complica la primera vez que lo ven, a manera de resumen, las clases pueden heredar ciertos datos a otras clases hijas, para eso se utilza la palabra reservada *extends* después de la clase hija junto al nombre de la clase padre:
```
class Viajero extends Explorer {}
```
Bien, ahora podemos utilizar la información del padre según sea conveniente.

**Override** viene en conjunto con herencia, consiste en sobreescribir métodos que han sido heredados por una clase base/padre.

Para una mejor explicación, es mejor hacerlo con el código:

```
class Explorer {
    constructor(name, user, mission) {
        this.name = name
        this.user = user
        this.mission = mission
    }

    getNameUser(){
        return `Explorer ${this.name}, user ${this.user}`
    }
}

// Heredamos clase explorer

class Viajero extends Explorer {
    constructor(name, user, mission, cycle) {
        super(name, user, mission) // SUPER ayudará a llamar el constructor padre (herencia)
        this.cycle = cycle
    }

    getGeneralInfo() {
        let nameAndUser = this.getNameUser() // Llamada al método del padre y lo modifica (override)
        return `${nameAndUser}, ciclo ${this.cycle}`
    }
}

const viajero = new Viajero("Luis", "LaunchX", "NodeJs", "Abril 20220")
console.log(viajero.getNameUser()) // Llamada al método del padre
console.log(viajero.getGeneralInfo()) // Llamada al método de Overriding
```

## Testing
Como bien lo menciona nuestro [Mission Commander Carlo](https://github.com/carlogilmar), las pruebas de unidad son súper importantes para cualquier desarrollo, si no hay pruebas, no hay manera de saber que el desarrollo está bien hecho.

Nosotros utilizamos [Jest](https://jestjs.io/) como framework de pruebas de unidad.

Una vez téngamos nuestro package.json, utilizamos el comando ```npm i --save-dev jest``` para instalarlo y tenerlo en nuestra carpeta de node_modules. 
Para realizar pruebas, necesitamos exportar los módulos que queremos probar.

```
// Class - pokemon.js

// Creamos nuestra clase como siempre y la exportamos
export default class Pokemon{
    constructor(name, type, age) {
        this.name = name
        this.type = type
        this.age = age
        this.attacks = []
    }

    get getAttacks() {
        return this.attacks
    }

    set setAttacks(attacks) {
        return this.attacks = attacks
    }
}

// Test - pokemon.test.js

// Se importa el módulo
import Pokemon from "./pokemon.js";

// Usamos la palabra reservada 'test'
test("1) Create a new object pokemon", () => {
  const myPokemon = new Pokemon("Pikachu");
  // expect(myPokemon.name).toBe('Pikachuuuuuuuu'); // Debe de hacer match con el valor dado en la instanciación
  expect(myPokemon.name).toBe("Pikachu");
});

```

Las pruebas unitarias son otro mundo más dentro de este universo de programación, este tema será lo principal en el siguiente post.
Pasa un excelente día ☀️
