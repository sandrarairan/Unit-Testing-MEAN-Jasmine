# Unit-Testing-MEAN-Jasmine
Unit Testing para MEAN con Jasmine Curso Platzi
# TABLA DE CONTENIDO
- [Creando un framework de pruebas básico](#Creando-un-framework-de-pruebas-básico)
- [Análisis estático de código](#Análisis-estático-de-código)
- [Trabajando con Jasmine en el frontend](#Trabajando-con-Jasmine-en-el-frontend)
- [Probando Nodejs apps con Jasmine](#Probando-Nodejs-apps-con-Jasmine)
- [Probando Angular apps con Jasmine](#Probando-Angular-apps-con-Jasmine)
- [Pruebas de integración de Angular apps con Jasmine](#Pruebas-de-integración-de-Angular-apps-con-Jasmine)
<!-- toc -->

## Creando un framework de pruebas básico
# Mi primera prueba unitaria en JavaScript
Características de las pruebas unitarias:

Aunque los resultados deben ser específicos de cada test unitario desarrollado, los resultados se pueden automatizar, de forma que podemos hacer las pruebas de forma individual o en grupos.

El proceso consta de pequeños test sobre parte del código, pero al final, se debe comprobar su totalidad.

En el caso de repetir las pruebas de forma individual o grupal, el resultado debe ser siempre el mismo, dando igual el orden en que se realicen los test, los tests se almacenan para poder realizar estas repeticiones o poder usarlos en otras ocasiones.

Es un código aislado que se ha creado con la misión de comprobar otro código muy concreto, no interfiere en el trabajo de otros desarrolladores.

A pesar de lo que muchos desarrolladores opinen, el código de los tests unitarios no debe llevar más de 5 minutos en ser creado, están diseñados para hacer que el trabajo sea más rápido.
**index.html**
```
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <script src="./prueba.js"></script>
  </head>
  <body></body>
</html>
```
**prueba.js**
```
const saludar = nombre => `Hola ${nombre}`;

console.log(saludar('Platzi'));

const resultado = saludar('Platzi');
const esperado = 'Hola Platzi';

if (resultado === esperado) {
  console.log('Prueba exitosa');
} else {
  console.log('Prueba no exitosa');
}
```
# Las funciones expect() y it()
Los errores en tiempo de ejecución también tienen como resultado un nuevo objeto Error que es creado y lanzado.

Normalmente los objetos de Error se crean con la intención de lanzarlos utilizando throw. Es posible manejar el error mediante try catch:

try {
    throw new Error("Algo salió mal!");
} catch (e) {
    alert("Bien hecho");
}
La función it() define una prueba de jasmine. Se llama así porque su nombre hace que las pruebas de lectura sean casi como leer en inglés.

El segundo argumento de la función it() es en sí mismo una función, que cuando se ejecute probablemente ejecutará un número de funciones _expect().

Las funciones expect () se utilizan para probar realmente las cosas que “espera” que sean ciertas.

**Prueba,js**
```
const saludar = nombre => `Hola ${nombre}`;

console.log(saludar('Platzi'));

function expect(actual) {
  return {
    toBe(expect) {
      if (actual !== expect) {
        throw new Error('Prueba no existosa');
      }
    }
  };
}

function it(title, callback) {
  try {
    callback();
    console.log('Prueba exitosa');
  } catch (error) {
    console.error('Prueba no exitosa');
  }
}

it('La función saluda', () => {
  expect(saludar('Platzi')).toBe('Hola Platzi');
});
```
# Organizando el código para correr en la web
El término refactorización se usa a menudo para describir la modificación del código fuente sin cambiar su comportamiento, lo que se conoce informalmente por limpiar el código.

La refactorización es la parte del mantenimiento del código que no arregla errores ni añade funcionalidad. El objetivo, por el contrario, es mejorar la facilidad de comprensión del código o cambiar su estructura y diseño y eliminar código muerto, para facilitar el mantenimiento en el futuro.

Añadir nuevo comportamiento a un programa puede ser difícil con la estructura dada del programa, así que un desarrollador puede refactorizarlo primero para facilitar esta tarea y luego añadir el nuevo comportamiento.

```
const saludar = nombre => `Hola ${nombre}`;

console.log(saludar('Platzi'));

function expect(actual) {
  return {
    toBe(expect) {
      if (actual !== expect) {
        throw new Error('Prueba no existosa');
      }
    }
  };
}

function it(title, callback) {
  try {
    callback();
    console.log(`✅ ${title}`);
  } catch (error) {
    console.log(`❎ ${title}`);
  }
}

it('La función saluda', () => {
  expect(saludar('Platzi')).toBe('Hola Platzi');
  
  ```
  **se organiza el código**
  **index.js**
  ```
  <html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
    <script src="./framework.js"></script>
    <script src="./app.js"></script>
    <script src="./app.spec.js"></script>
  </head>
  <body></body>
</html>
```
**frameworj.js**
```
function expect(actual) {
  return {
    toBe(expect) {
      if (actual !== expect) {
        throw new Error('Prueba no existosa');
      }
    }
  };
}

function it(title, callback) {
  try {
    callback();
    console.log(`✔ ${title}`);
  } catch (error) {
    console.error(`× ${title}`);
  }
}
```

**app.js**
```
const saludar = nombre => `Hola {nombre}`;
```
**app.spec.js**

```
console.log(saludar('Platzi'));

it('La función saluda', () => {
  expect(saludar('Platzi')).toBe('Hola Platzi');
});
```

# Organizando el código para correr utilizando nodejs
Node.js es un entorno en tiempo de ejecución multiplataforma, de código abierto, para la capa del servidor (pero no limitándose a ello) basado en el lenguaje de programación ECMAScript

Fue creado con el enfoque de ser útil en la creación de programas de red altamente escalables, como por ejemplo, servidores web.

Ejemplo de un hola mundo de un servidor HTTP escrito en Node.js:

const http = require('http');

const hostname = '127.0.0.1';
const port = 1337;

http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello World\n');
}).listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});

**framework.js**
``` 
function expect(actual) {
  return {
    toBe(expect) {
      if (actual !== expect) {
        throw new Error('Prueba no existosa');
      }
    }
  };
}

function it(title, callback) {
  try {
    callback();
    console.log(`✔ ${title}`);
  } catch (error) {
    console.error(`× ${title}`);
  }
}

module.exports = {
  expect,
  it
};
```
**app.js**
```
const saludar = nombre => `Hola ${nombre}`;

module.exports = saludar;
```

**pp.spec.js**

```
const it = require('./framework').it;
const expect = require('./framework').expect;
const saludar = require('./app');

it('La función saluda', () => {
  expect(saludar('Platzi')).toBe('Hola Platzi');
});
```
## Análisis estático de código
# Herramientas de análisis estático de código
Linters: Herramientas de alertas. Nos ayudan a seguir las reglas o convenciones de nuestros equipos sin tener que memorizar todo el libro de reglas; solo debemos programar y asegurarnos de que estas herramientas revisen nuestro código.

Por ejemplo: ESLint, JSHint, CSSComb o scsslint.

Corrección automática: Herramientas que nos ayudan a revisar y arreglar nuestro código sin importar si usamos un editor de código u otro; funcionan para todos los casos y gustos de la comunidad. Por ejemplo: Prettier.

Tipado: JavaScript es lenguaje de tipado dinámico, podemos cambiar el tipo de variables cada vez que queramos o necesitemos. Pero, podemos usar diferentes herramientas para implementar el tipado fuerte, es decir, que podamos usar variables con tipos diferentes al que definimos inicialmente (a menos que hagamos una conversión).

La herramienta de tipado más popular en JavaScript es TypeScript pero tambien existen algunas alternativas como Flow y React PropTypes.

Respuesta a:
Herramientas de análisis estático de código
https://eslint.org
https://prettier.io
http://csscomb.com
https://jshint.com
https://github.com/brigade/scss-lint
https://www.typescriptlang.org
https://flow.org
https://reactjs.org/docs/typechecking-with-proptypes.html

# ESLint: Agregando alertas a nuestro código con ECMA Script
ESLint es una herramienta que identifica y reporta patrones y errores en código ECMAScript/JavaScript. Es similar a JS-Lint y JSHint con algunas diferencias:

ESLint usa Espree para analizar JavaScript.
ESLint usa un AST para evaluar patrones en código.
ESLint soporta plugins, cada regla es un plugin y puedes agregar más en desarrollo.

https://eslint.org/
https://github.com/standard/eslint-config-standard/blob/master/eslintrc.json

# Herramientas de corrección de estilo
Prettier es un formateador de código opinado. Aplica un estilo coherente al analizar su código y reimprimirlo con sus propias reglas que toman en cuenta la longitud máxima de la línea, envolviendo el código cuando sea necesario.

Puede ejecutarse en su editor al guardar, en un gancho de confirmación previa o en entornos CI para garantizar que su base de código tenga un estilo coherente sin que los desarrolladores tengan que publicar un comentario minucioso sobre una revisión de código.

Ofrece soporte para:

JavaScript, including ES2017
JSX
Angular
Vue
Flow
TypeScript
CSS, Less, and SCSS
HTML
JSON
GraphQL
Markdown, including GFM and MDX
YAML
Por ejemplo tenemos éste codigo de JavaScript mal formateado:

foo(reallyLongArg(), omgSoManyParameters(), IShouldRefactorThis(), isThereSeriouslyAnotherOne());
Al pasar Prettier nos lo deja de una manera más legible:

foo(
  reallyLongArg(),
  omgSoManyParameters(),
  IShouldRefactorThis(),
  isThereSeriouslyAnotherOne()
);

https://prettier.io/

# TypeScript es un lenguaje de programación libre y de código abierto desarrollado y mantenido por Microsoft.

Es un superconjunto de JavaScript, que esencialmente añade tipado estático y objetos basados en clases.

TypeScript extiende la sintaxis de JavaScript, por tanto cualquier código JavaScript existente debería funcionar sin problemas.

Está pensado para grandes proyectos, los cuales a través de un compilador de TypeScript se traducen a código JavaScript original.

https://www.typescriptlang.org/


## Trabajando con Jasmine en el frontend

# Profundización en SpyOn: Comandos más utilizados y cómo ponerlos a prueba
asime spyOn
La separación de responsabilidades es una de las buenas prácticas que encontramos en un proyecto de software. Separar responsabilidades significa agrupar código de tal manera que cada conjunto se encargue de una tarea específica.

Hablemos ahora de las pruebas unitarias. Cuando probamos un componente, queremos probar las responsabilidades que le estamos delegando al componente y no todo el código ejecutado. Es decir, si el componente A utiliza la función b(), lo que queremos probar es la lógica propia del componente y no el código de la función.

Veamos el siguiente ejemplo:

function GetMonthApi() {
  this.currentMonth = function () {
    return 'May';
  }
  this.nextMonth = function () {
    return 'June'
  }
}
export function MonthCalculator() {
  this.api = new getMonthApi();
  this.getNextMonth = function() {
    return this.api.nextMonth();
  }
  this.getCurrentMonth = function() {
    return this.api.currentMonth();
  }
}
La clase MonthCalculator nos permite calcular el valor del mes actual y el siguiente. Cómo puedes ver, la función getMonthApi es utilizada dentro de la clase. Si ejecutas el set de pruebas asociadas a nuestra clase se ejecuta en Mayo el valor del siguiente mes sería Junio, o si las corres en Enero el siguiente mes sería Febrero. ¿Ves el problema?.

Si ejecutamos código que se encuentre fuera del domino de un componente, nos podemos encontrar con resultados inesperados. Es por ello, que jasmine cuenta con un sistema de espías (spyOn), cuyo objetivo principal es interceptar la ejecución de una función y simular su resultado.

Veamos un poco de código:
El primer método que vamos a probar es el de obtener el mes actual currentMonth. Si la prueba la creamos en mayo, el código debería ser:

describe('MonthCalculator', () => {
  it('returns the current month', () => {
    // Arrange
    const monthCalculator = new MonthCalculator();  
    // Act
    const month = monthCalculator.currentMonth();
    // Assert
    expect(month).toBe('May');
  });
});
Este código tiene un problema. La función currentMonth va a retornar un valor que depende del mes actual.

Como ya te podrás imaginar, el uso de espías resulta bastante útil en este caso debido a que podemos controlar el valor del mes retornado.

Es decir:

describe('MonthCalculator', () => {
  it('returns the current month', () => {
    // Arrange
    const monthCalculator = new MonthCalculator();
    const spy = spyOn(
                 monthCalculator.api,
                 'currentMonth'
               ).and.returnValue('Cristian Month');
    // Act
    const month = monthCalculator.currentMonth();
    // Assert
    expect(month).toBe('Cristian Month');
    expect(spy).toHaveBeenCalled();
  });
});
La instancia del API la tenemos almacenada en la variable this.api de nuestra clase.
Jasmine nos permite interceptar el llamado a nuestro API utilizando la función spyOn. Para ello, como primer parámetro debemos pasar el objeto que contiene el método que vamos a interceptar y como segundo parámetro el nombre del mismo.

Una vez creado nuestro espía, para poder controlar el valor retornado debemos concatenar lo siguiente: .and.returnValue().
Finalmente Jasmine nos permite verificar la ejecución de la función por medio del operador .toHaveBeenCalled().

Cómo reto ve al siguiente enlace, has un fork del proyecto y realiza las pruebas relacionadas con el método nextMonth(). Recuerda crear un espía para eliminar la dependencia con nuestra API.

Finalmente, te dejo un listado de preguntas y respuestas sobre todo lo que puedes hacer con espías:
¿Cómo se crea un espía?
spyOn(obj, 'method') // obj.method es una función
¿Cómo verificar que un método fue llamado?
const ref = spyOn(obj, 'method');
expect(ref).toHaveBeenCalled();
// O directamente
expect(obj.method).toHaveBeenCalled()
¿Cómo verificar que un método fue llamado con un parámetro específico?
const ref = spyOn(obj, 'method');
expect(ref).toHaveBeenCalledWith('foo', 'bar');
// O directamente
expect(obj.method).toHaveBeenCalledWith('foo', 'bar')
¿Cómo puedo verificar el número exacto de ejecuciones de un método?
expect(obj.method.callCount).toBe(2)
¿Cómo espiar en un método sin modificar su comportamiento?
spyOn(obj, 'method').andCallThrough()
¿Cómo puedo cambiar el valor retornado por un método?
spyOn(obj, 'method').andReturn('value')
¿Cómo puedo sobreescribir un método?
spyOn(obj, 'method').andCallFake(() => 'this is a function');
Reportar un problema

# Configurar un ambiente de trabajo para trabajar con el framework jasmine
Jasmine es un framework de Desarrollo dirigido por comportamientos (Behavior Driven Development) para realizar nuestras pruebas unitarias con JavaScript.

Puede ser ejecutado en el navegador pero también podemos usar un headless browser para automatizar mejor las pruebas. Por ejemplo, con PhantomJS, CasperJS o ZombieJS.

Tampoco necesitamos un DOM; por lo que, es posible hacer pruebas en cualquier Javascript Engine como Rhino o V8 (como Node.js).

¿Cómo funciona?

Las funciones principales de Jasmine para hacer pruebas son las siguientes:

describe(a, b) donde “a” es la descripción de nuestra suite y “b” la función anónima donde se incluirá toda la suite o serie de especificaciones.
it(a, b) donde “a” es la descripción de la especificación y “b” la función anónima donde se incluirán las expectativas (expectations) que debe cumplir la aplicación.
expect(a) donde “a” es un valor que será probado, mediante argumentos en cadena (method chaining). Por ejemplo: expect(true).not.toBe(false).
beforeAll(a) donde “a” será la función que se ejecutará antes de iniciar las pruebas.
afterAll(a) donde “a” será la función que se ejecutará después de iniciar las pruebas.
beforeEach(a) donde “a” será la función que se ejecutará antes de cada prueba.
afterEach(a) donde “a” será la función que se ejecutará después de cada prueba.

**specRunner.html**
```
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>

  <link rel="shortcut icon" type="image/png"
    href="https://cdnjs.cloudflare.com/ajax/libs/jasmine/3.3.0/jasmine_favicon.png">
  <link rel="stylesheet" type="text/css" href="https://cdnjs.cloudflare.com/ajax/libs/jasmine/3.3.0/jasmine.css">

  <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jasmine/3.3.0/jasmine.js"></script>
  <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jasmine/3.3.0/jasmine-html.js"></script>
  <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jasmine/3.3.0/boot.js"></script>
  <script src="./app2.js"></script>
  <script src="./app2.spec.js"></script>
</head>

<body>

</body>

</html>
```
**app.js**
const saludar = nombre => `Hola ${nombre}`;

module.exports = saludar;

**app2.spec.js**
```
it('La función saluda', () => {
  expect(saludar('Platzi')).toBe('Hola Platzi');
});
```

# Configurar Jasmine utilizando Node.js
Gracias a Node.js obtenemos algunas ventajas para desarrollar y probar nuestras aplicaciones. Necesitamos un archivo package.json, en caso de que tu proyecto no lo tenga todavía, puedes crearlo ejecutando el siguiente comando:

Vamos a necesitar un archivo package.json

npm init
Debemos ejecutar los siguientes comandos para instalar e iniciar Jasmine en nuestro proyecto con Node.js:

npm install --save-dev jasmine
node node_modules/jasmine/bin/jasmine init
Por último, para correr las pruebas que vamos a crear en las próximas clases, debemos agregar un nuevo script en nuestro package.json y ejecutarlo con el comando npm test:

"scripts": {
    "test": "jasmine"
}

https://jasmine.github.io/

```
JASMINE FOR NODE.JS
Add Jasmine to your package.json

npm install --save-dev jasmine
Initialize Jasmine in your project

node node_modules/jasmine/bin/jasmine init
Set jasmine as your test script in your package.json

"scripts": { "test": "jasmine" }
Run your tests

npm test

``` 

En la carpeta spec que se creo se ingrean las pruebas unitarias
**app.spec.js**
```
const saludar = require('../app');

it('La función saluda', () => {
  expect(saludar('Platzi')).toBe('Hola Platzi');
});
```
**app.js**
```
const saludar = nombre => `Hola ${nombre}`;

module.exports = saludar;
```
# Primer set de pruebas con Jasmine
Funciones de Jasmine con las cuales podremos experimentar:

expect(x).toEqual(y) verifica si ambos valores son iguales.
expect(x).toBe(y) verifica si ambos objetos son iguales.
expect(x).toMatch(pattern) verifica si el valor pertenece al patrón establecido.
expect(x).toBeDefined() verifica si el valor está definido.
expect(x).toBeUndefined() verifica si el valor es indefinido.
expect(x).toBeNull() verifica si el valor es nulo.
expect(x).toBeTruthy() verifica si el valor es verdadero.
expect(x).toBeFalsy(); verifica si el valor es falso.
expect(x).toContain(y) verifica si el valor actual contiene el esperado.
expect(x).toBeLessThan(y) verifica si el valor actual es menor que el esperado.
expect(x).toBeGreaterThan(y) verifica si el valor actual es mayor que el esperado.

# Diccionario Jasmine

```
Esta lectura te servirá de referencia para las cosas que puedes hacer con Jasmine:

Creando un set de pruebas
describe("Componente", () => {
  it("debería ...", () => {
    expect(true).toBe(true);
  });
});

Agrupando por funcionalidad
describe("Componente", () => {
  describe("Funcionalidad uno", () => {
    it("debería ...", () => {
      expect(true).toBe(true);
    });
  });
});
Matchers

expect(false).not.toBe(true); // Prueba negativa
comparación con ===, ejemplo: 1 === 1 1 !== '1'

expect(thing).toBe(realThing);
El valor no es undefined 

expect(result).toBeDefined();
El valor actual es falso, ejemplo:0, '', false

expect(result).toBeFalsy();
El valor actual es verdadero, ejemplo: 'sd', 1, true

expect(thing).toBeTruthy();
El valor actual es mayor al esperado

expect(result).toBeGreaterThan(3);
El valor actual es mayor o igual al esperado

expect(result).toBeGreaterThanOrEqual(25);
El valor actual es menor al esperado

expect(result).toBeLessThan(0);
El valor actual es menor o igual al esperado

expect(result).toBeLessThanOrEqual(123);
El valor actual es NaN

expect(thing).toBeNaN();
El valor actual es -Infinity 

expect(thing).toBeNegativeInfinity();
El valor actual es Infinity

expect(thing).toBePositiveInfinity();
El valor actual es null 

expect(result).toBeNull();
El valor actual continue una cadena. Ejemplo:

 'Hola mundo'.toContain('Hola') // true
['Hola', 'mundo'].toContain('Hola') // true
expect(array).toContain(anElement); expect(string).toContain(substring);
El valor actual es igual utilizando una comparación profunda

expect(bigObject).toEqual({"foo": ['bar', 'baz']});
El espía fue llamado

expect(mySpy).toHaveBeenCalled(); expect(mySpy).not.toHaveBeenCalled();
El espía fue llamado antes que otro

expect(mySpy).toHaveBeenCalledBefore(otherSpy);
El espía fue llamado n veces:

expect(mySpy).toHaveBeenCalledTimes(3);
El espía fue llamado con los siguientes parámetros

expect(mySpy).toHaveBeenCalledWith('foo', 'bar', 2);
Verificar si un elemento tiene una clase

const el = document.createElement('div');
el.className = 'foo bar baz';
expect(el).toHaveClass('bar');
El valor actual comparado con una expresión regular

expect("my string").toMatch(/string$/); 
expect("other string").toMatch("her");
Ciclos de vida
describe("Component", () => {
  // Shared variables
  var foo = 0;
beforeAll(() => {})
  beforeEach(() => {})
  afterEach(() => {})
  afterAll(() => {})
});
Deshabilitando pruebas
xdescribe("A spec", () => {
  it("waiting to be enable", function() {
    expect(true).toEqual(true);
  });
});
describe("A spec", () => {
  it("this run", () => {
    expect(true).toEqual(true);
  });
  xit("this is skipped", () => {
    expect(true).toEqual(true);
  });
});
Utilizando spyOn
describe('A spy', () => {
  let foo,
    bar = null;
  beforeEach(() => {
    foo = {
      setBar: value => {
        bar = value;
      },
    };
    spyOn(foo, 'setBar');
    foo.setBar(123);
    foo.setBar(456, 'another param');
  });
  it('tracks that the spy was called', () => {
    expect(foo.setBar).toHaveBeenCalled();
  });
  it('tracks that the spy was called x times', () => {
    expect(foo.setBar).toHaveBeenCalledTimes(2);
  });
  it('tracks all the arguments of its calls', () => {
    expect(foo.setBar).toHaveBeenCalledWith(123);
    expect(foo.setBar).toHaveBeenCalledWith(456, 'another param');
  });
});
Crear espía cuando desconocemos si la función existe
describe("Create a 'bare' spy", () => {
  let notSure;
  beforeEach(function() {
    notSure = jasmine.createSpy('notSure');
    notSure("I", "am", "a", "spy");
  });
  it("tracks that the spy was called", function() {
    expect(notSure).toHaveBeenCalled();
  });
});
Creando multiples espías en un mismo objeto
describe("Multiple spies", () => {
  const tape;
  beforeEach(() => {
    tape = jasmine.createSpyObj('tape', ['play', 'pause', 'stop']);
    tape.play();
      tape.pause();
      tape.rewind(0);
    });
  it("creates spies for each requested function", () => {
    expect(tape.play).toBeDefined();
    expect(tape.pause).toBeDefined();
    expect(tape.stop).toBeDefined();
  });
});
Verificar una propiedad de un objeto
describe("jasmine.objectContaining", () => {
  let foo;
  beforeEach(() => {
    foo = {
      a: 1,
      b: 2,
      bar: "baz"
    };
  });
  it("matches objects with the expect key/value pairs", () => {
    expect(foo).toEqual(jasmine.objectContaining({
      bar: "baz"
    }));
    expect(foo).not.toEqual(jasmine.objectContaining({
      c: 37
    }));
  });
});
Verificar una propiedad dentro de un objeto pasado como parámetro a una función
describe('jasmine.objectContaining', () => {
  it('is useful for comparing arguments', () => {
    const callback = jasmine.createSpy('callback');
    callback({
      bar: 'baz',
    });
    expect(callback).toHaveBeenCalledWith(
      jasmine.objectContaining({
        bar: 'baz',
      })
    );
  });
});
Verificar un valor dentro de un arreglo
describe("jasmine.arrayContaining", () => {
  let foo;
  beforeEach(function() {
    foo = [1, 2, 3, 4];
  });
  it("matches arrays with some of the values", () => {
    expect(foo).toEqual(jasmine.arrayContaining([3, 1]));
    expect(foo).not.toEqual(jasmine.arrayContaining([6]));
  });
});
Verificar un valor dentro de un arreglo pasado como parámetro a una función
describe('jasmine.arrayContaining', () => {
  it('is useful when comparing arguments', () => {
    const callback = jasmine.createSpy('callback');
    callback([1, 2, 3, 4]);
   expect(callback)
     .toHaveBeenCalledWith(jasmine.arrayContaining([4, 2, 3]));
   expect(callback)
     .not.toHaveBeenCalledWith(jasmine.arrayContaining([5, 2]));
  });
});
Usando regex para comparar comparar cadenas de texto
describe('jasmine.stringMatching', () => {
  it("matches as a regexp", () => {
    expect({foo: 'bar'})
      .toEqual({foo: jasmine.stringMatching(/^bar$/)});
    expect({foo: 'foobarbaz'})
      .toEqual({foo: jasmine.stringMatching('bar')});
  });
   describe("when used with a spy", () => {
    it("comparing arguments", () => {
      const callback = jasmine.createSpy('callback');
      callback('foobarbaz');
      expect(callback)
        .toHaveBeenCalledWith(jasmine.stringMatching('bar'));
      expect(callback)
        .not.toHaveBeenCalledWith(jasmine.stringMatching(/^bar$/));
    });
  });
});
```

## Probando Nodejs apps con Jasmine
# Introducción al módulo de testing del lado del servidor
Vamos a crear las pruebas unitarias de una aplicación construida con el Stack MEAN: Node.js y Express.js en el backend, MongoDB como base de datos y Angular (con TypeScript) en el frontend.

Vamos a probar la interacción del frontend (Angular) con el servidor o con los clientes y cómo interactúa el servidor con el framework que hace las consultas a la base de datos y con el cliente que hace las peticiones. NO vamos a probar la base de datos directamente.

# Configurando el proyecto Jasmine utilizando npm
La diferencia entre dependencies (dependencias) y devDependencies (dependencias de desarrollo) es que las dependencias normales las instalamos siempre, en desarrollo o en producción. En cambio, las devDependencies son módulos que solo se vamos a necesitar en la etapa de desarrollo, no en producción.

Algunos buenos ejemplos de dependencies que se requerirían en tiempo de ejecución son, por ejemplo, React, Redux, Express y Axios.

Algunos buenos ejemplos de cuándo instalar devDependencies serían Nodemon, Babel, ESLint y marcos de prueba como Chai, Mocha, Enzyme, entre otros.

Luego instalan Jasmine npm install jasmine --save-dev

Luego comenzar los archivos de configuración de Jasmine: ./node_module/jasmine/bin/jasmine.js init

**se crea una carpeta spec/support/jasmin.json
```
{
  "spec_dir": "spec",
  "spec_files": [
    "../server/**/*[sS]pec.js",
    "**/*[sS]pec.js"
  ],
  "helpers": [
    "helpers/**/*.js"
  ],
  "stopSpecOnExpectationFailure": false,
  "random": true
}
```
- Dentro de la carpeta server se crea un archivo de pruebas server.spec.js

```
it('funciona', () => {
  expect(true).toBeTruthy();
})
```
**package.json**
```
"test:server": "./node_modules/jasmine/bin/jasmine.js",
```
# Agregando Plugins a Jasmine
Vamos a usar el plugin jasmine-console-reporter para obtener un resultado un poco más agradable y dinámico cuando corremos nuestras pruebas en la consola de comandos.

Para añadir este y otros plugins de Jasmine debemos crear un nuevo archivo llamado specs.js en la carpeta /spec con la siguiente configuración:

const Jasmine = require('jasmine');
const JasmineConsoleReporter = require('jasmine-console-reporter');

const jasmine = new Jasmine();
jasmine.loadConfigFile('spec/support/jasmine.json');

const jasmineConsoleReporter = new JasmineConsoleReporter({
    colors: 1,
    cleanStack: 1,
    verbosity: 4,
    listStyle: 'indent',
    timeUnit: 'ms',
    timeThreshold: { ok: 500, warn: 1000, ouch: 3000 },
    activity: false,
    emoji: true,
    beep: true
});

jasmine.addReporter(jasmineConsoleReporter);
jasmine.execute();
Y, por ultimo, agregar un nuevo campo en el la sección de scripts del package.json ejecutando archivo que acabamos de crear:

"scripts": {
  ...
  "test:server:covegare": "node spec/specs.js",
  ...
}

https://github.com/onury/jasmine-console-reporter

npm i jasmine-console-reporter --save-dev

**package.json**
"test:server:coverage": "node spec/specs.js",

# Configurando nuestro reporter
Los sistemas de reportes nos ayudan a navegar entre la información para saber cuánta cobertura tiene nuestro código con la red de seguridad que estamos programando.

Vamos a usar la librería IstanbulJS:

npm install --save-dev nyc
"scripts": {
  ...
  "test:server:coverage": "nyc node spec/specs.js",
  ...
}

https://istanbul.js.org/

- 
$ npm install --save-dev nyc
Now, simply place the command nyc in front of your existing test command, for example:
{
  "scripts": {
    "test": "nyc node spec/specs.js"
  }
}

https://github.com/istanbuljs/nyc

y en el package.json

nyc": {
    "report-dir": "./spec/istanbul/report",
    "temp-dir": "./spec/istanbul",
    "reporter": [
      "text",
      "text-summary",
      "html"
    ],
    "exclude": [
      "spec/**/*",
      "server/*.spec.js"
    ]
  }
  
  # Pruebas en el servidor: Verificando un status 200 en GET
Los “espías” son funciones de prueba que interceptan las llamadas a una función y recolectan datos sobre lo que sucede dentro ella: el número de veces que se llama una función, con qué parámetros y los valores de retorno de la función (o, si lanzó excepciones, los mensajes y la información del error).

Vamos a configurar un servidor exclusivo para ejecutar las pruebas unitarias de nuestra aplicación. Recuerda que NO vamos a probar la conexión con la base de datos, solo la interacción del servidor con la aplicación Front End. Por lo tanto, vamos a crear un servidor con la mínima configuración posible para hacer peticiones y probar que funcione correctamente.

Recuerda que usamos el método HTTP GET para solicitar datos de nuestra aplicación, no para borrar, actualizar oagregar información; solo visualizarla.

en la carpeta server/server.spec.js
```
const express = require('express');
const logger = require('morgan');
const http = require('http');
const PinsRouter = require('./routes/pins');
const Pins = require('./models/Pins');
const request = require('request');
const app = express();

app.use(logger('dev'))
app.use(express.json())
app.use('/api', PinsRouter.router);
app.set('port', 3000);

describe('Testing Router', () => {
  let server;

  beforeAll(() => {
    server = http.createServer(app);
    server.listen(3000);
  })

  afterAll(() => {
    server.close();
  });

  describe('GET', () => {
    // GET 200
    it('200 and find pin', done => {
      const data = [{ id: 1 }];
      spyOn(Pins, 'find').and.callFake(callBack => {
        callBack(false, data);
      });

      request.get('http://localhost:3000/api', (error, response, body) => {
        expect(response.statusCode).toBe(200);
        expect(JSON.parse(response.body)).toEqual([{ id: 1 }]);
        done();
      })
    })

    // GET 500
  })
})
```
https://www.npmjs.com/package/morgan

# Pruebas en el servidor: Probando el método GET y Reto con FindByID
En la clase anterior probamos el código 200, lo que significa que todo está bien y nuestro servidor responde correctamente. En esta clase vamos a probar que nuestro servidor no funcione, nuestra prueba solo debe pasar si devuelve un error con el código 500, un error del servidor.

El reto de la clase es volver a probar el método get pero, esta vez, recibiendo parámetros. La lógica es casi la misma pero la ruta va a ser diferente y tenemos que cambiar algunos métodos como el find por el findById.


# Pruebas en el servidor: Probando el método POST (request to server)
Vamos a usar axios: una librería que nos ayuda a consultar y enviar datos a las URLs que le indiquemos con una sintaxis un poco diferente a la de la librería request. Podemos usarla, por ejemplo, para hacer consultas a nuestra propia aplicación para comprobar que obtenemos la información que esperamos.

Instalación de axios:

npm install axios --save-dev
Vamos a probar el caso de éxito del método POST de nuestra API: la aplicación debe responder correctamente cuando los usuarios envían URLs de archivos PDF o páginas con código HTML común y corriente.

En este caso, vamos a utilizar datos “falsos” para correr las pruebas: en vez de descargar los recursos para consumir un PDFs o una páginas web, nosotros mismos vamos a escribir los datos con los que interactúa nuestro código para comprobar que la aplicación responde correctamente.

# Pruebas en el servidor: Probando el método POST (request to PDF)

## Pruebas en el servidor: Probando el método POST (request to PDF)
# Tipos de pruebas
Existen cinco tipos de pruebas, las cuales son:

Unitarias: es una forma de comprobar el correcto funcionamiento de una unidad de código.
Integración: son aquellas que se realizan en el ámbito del desarrollo de software una vez que se han aprobado las pruebas unitarias y lo que prueban es que todos los elementos unitarios que componen el software, funcionan juntos correctamente probándolos en grupo.
Funcionales: es una prueba de tipo caja negra basada en la ejecución, revisión y retroalimentación de las funcionalidades previamente diseñadas para el software.
Carga/estrés: la prueba de carga prueba de rendimiento utilizado para evaluar cómo actúa el sistema con una carga variable de usuarios pero dentro de los niveles esperados de la aplicación. Una prueba de estrés evalúa el sistema sometiéndolo a una carga creciente hasta que este falle.
Aceptación: pertenecen a las últimas etapas previas a la liberación en firme de versiones nuevas a fin de determinar si cumplen con las necesidades y/o requerimientos de las empresas y sus usuarios.

# Pruebas en el frontend: Probando el componente principal (App)
Vamos a crear algunas pruebas para nuestro componente principal en el frontend: un conjunto de archivos que encontramos en la carpeta src/app.

El archivo app.component.ts se encarga de definir la lógica de nuestra aplicación. Por ahora, no tenemos nada, solo la referencia a otros componentes con tareas muy concretas que vamos a ir probando en las siguientes clases:

app.component.html: Se encarga de renderizar el componente de navegación, router-outlet.
app.component.spec.ts: Tiene todas las pruebas del componente App. Algunas de las pruebas por defecto no son muy útiles en este momento y vamos a reemplazarlas por algunas pruebas en el archivo app.component.html para confirmar que se incluye el componente render-oulet y la navegación funciona correctamente.


## Pruebas de integración de Angular apps con Jasmine
# Ejecutando funciones a través de eventos en el template
Las pruebas de integración son pruebas que dependen de otras clases para obtener resultados en nuestros componentes.

Vamos a ejecutar algunas de estas pruebas en nuestros templates pero dependiendo de los resultados de los componentes marcados como clases. Además, vamos a probar algunos de nuestros servicios con la herramienta de simulación de eventos HTTP que nos provee el equipo de Angular.






