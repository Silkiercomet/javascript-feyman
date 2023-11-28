# you dont know javascript yet

es un libro dirigido a presentar todos las cosas extrañas y comportamientos de javascript, tanto para programadores que desean dominar el lenguaje como para aquellos que quieren empezar a aprenderlo, aunque ambos desean lo mismo 

el auto reconoce que muchos temas tratados en este libro son densos y muy complicados, recomienda no solo leer un capitulo y saltar al siguiente, si no, leer, re-leerlo, practicarlo e investigar para poder sacarle el maximo provecho al contenido

# first chapter

JS es backwards compatible, esto significa que no importa qué tan antiguo sea el código script, este deberá todavía correr en un ambiente de JavaScript. ECMA no puede romper la web y esto garantiza a cualquier desarrollador que su código será válido y no se romperá a mediano-largo plazo. Aun así, hay preprocesadores como Babel que traducen el JS a una versión compatible con todas las versiones de JS.

JavaScript es un lenguaje multiparadigma, esto significa que se puede utilizar cualquier paradigma para encontrar la solución deseada, ya sea procedural, OOP o FP. Estos pueden coexistir en el mismo ambiente.

Ambientes como las dev-tools, console, alert (funciones y métodos del navegador) no son JavaScript. A pesar de lo que puede parecer a primera vista, estas funciones y métodos no funcionarían en un ambiente 100% JS, ya que pertenecen a los navegadores y están orientadas a la DX (developer experience).

JavaScript es un lenguaje de programación parsado, más cercano a un lenguaje compilado que a un script, debido a la forma en que es procesado para la web. Este es primero parsado a bytecode, que es entregado a la máquina virtual del navegador, y esta lo procesa a binario para luego ejecutarlo. También durante el parsado del documento se pueden encontrar errores de parsado o de variables, es decir, errores dinámicos que en un lenguaje de script no se podrían encontrar debido a cómo se comportan estos lenguajes. Para encontrar un error en la línea 5, se deben ejecutar primero las líneas 1, 2, 3, 4.

# como usar JS

cada documento que termine en .js es considerado un programa de javascript incluso si todos operan en la misma aplicacion, ya que todos los documentos representan un solo espacio llamada "global scope" asi que pueden interactuar los unos con los otros, lo unico que podria cambiar esto seria que se haga desde "type=module" donde cada documento solo compartira los valores exportados y recibira los que importe de otros modulos

## tipos de datos

los datos primitivas son definidos normalmente como valores puros, es un valor asignado a una variable, y estos pueden ser string, number, boolean, undefined, null (SYMBOL tambien se usa para definir un valor unico pero muy poco comun fuera de low-code)

* string : se define usando "" o '' todo valor en medio de los puntos sera evaluado como una cadena de texto, tambien se puede usar `` que tiene una funcion especial y es que valores dinamicos pueden ser definidos dentro de la cadena usando la sintaxis ${valorDinamico} solo se deben usar cuandos es apropiado y para cadenas normales es recomendable escoger un metodo de definirlas y mantenerlo todo el programa

* number : todos los caracteres alfa numericos entran en esta categoria

* boolean : una condicion a la que puede asignarsele dos valores true o false

* undefined - null : estos valores usualmente representan la ausencia de un valor, es recomendable usar solo undefined ya que null puede traer bugs

* bigint : usado para definir grandes integrales arbitrarias 

y los tipos de datos o estrucuturas especiales que son Object, y Function 

* object: una estructura de datos en la que puede definirse cada una de sus llaves que serviran de referencia para cada valor almacenado en ellas

* array : es un objeto cuyas llaves son numericas asendentes y en el se pueden guardar cualquier tipo de valor

* function : un objeto especial que ejecuta un bloque de codigo y devuelve un valor o no

## declaradores

estos son palabras claves especificas y solo permitidas para la declaracion de variables, estas son var , let, const

- var : declara la variable en el scope global de la aplicacion, lo que la hace accesible en cualquier parte del programa (con cuidado porque dependiendo del nombre podria traer problemas al coincider con otras variables ya que es giardada en el objeto global del navegador).

- let : este define la varaible y lo restringe al block scope en que se encuentra, un block scope es el bloque de codigo que se encuentra entre un par de corchetes {} esta variable solo existira y sera accesible en su bloque.

- const : una variable constante que tiene que ser inicializada con un valor y no permite reasignarlo a diferencia de las alternativas anteriores, si se le asigna a un objeto si se le permite mutar los valores del objeto pero no el objeto o arreglo en si

```js
const actors = [
    "Morgan Freeman", "Jennifer Aniston"
];

actors[2] = "Tom Cruise";   // OK :(
actors = [];                // Error!
```

funciones declaradas con el constructor function se comportan como si fueran declarados con var y son accesibles en la scope global 

```js
function nombre(parametro){
    // sin embargo parametro es solo accesible en la block scpo de esta funcion nombre()
}
```

## functions

en javascript funciones tiene una definicion mas amplia que en otros lenguajes, esta aplica a procesos matematicos o operaciones complejas, hay varia formas de definirlas

declaracion de funcion
```js
function nombre(parametro){
   console.log(parametro)
}
nombre("hola")
```

declarada como una expresion
```js
const nombre = function(parametro){
   console.log(parametro)
}
nombre("hola")
```

cada funcion puede retornar un solo valor, de ser necesario retornar mas se puede popular un objeto con funciones

```js
var whatToSay = {
    greeting() {
        console.log("Hello!");
    },
    question() {
        console.log("What's your name?");
    },
    answer() {
        console.log("My name is Kyle.");
    }
};

whatToSay.greeting();
// Hello!
```

## comparaciones

Js nos permite comparar dos expresiones con el uso de ciertos simbolos como "===" esta es una comparacion estricta, evalua el tipo del dato y el dato de la expresion, el simbolo "==" tambien compara el tipo y el dato de la expresion pero este permite convertir el tipo de una de las expresiones para que estas puedan ser evaluadas

```js
//igualdad estricta
3 === 3.0;              // true
"yes" === "yes";        // true
null === null;          // true
false === false;        // true

42 === "42";            // false
"hello" === "Hello";    // false
true === 1;             // false
0 === null;             // false
"" === null;            // false
null === undefined;     // false

// igualdad coerciva

42 == "42";             // true
1 == true;              // true
```

hay casos particulares en los que JS esta diseñado para mentir que son los siguientes

```js
NaN === NaN;            // false
0 === -0;               // true
```

ambos casos son excepciones y cuando se necesiten evaluar esos numeros debemos usar metodos que estan diseñados para no mentir

```js

Number.isNaN(NaN) // true
Object.is(0,-0) // false ! este es el comparador definitivo ya que no miente nunca (menos mutacion o ref)

```

### comparacion de valores no primitivos

en JS cuando se van a comparar dos valores no primitivos iguales podria encontrarse con una sorpresa como esta

```js
[ 1, 2, 3 ] === [ 1, 2, 3 ];    // false
{ a: 42 } === { a: 42 }         // false
(x => x * 2) === (x => x * 2)   // false
Object.is([1,2],[1,2])          //false
```

esto ocurre porque JS guarda los valores objeto por referencia y no por valor, que se quiere decir con esto, es que al declararse un objeto este es asignado un espacio especifico en la memoria del ambiente js, por lo tanto cada arreglo, objeto o expresion estan depositados en distintas partes de la memoria por ende la comparacion no es de su contenido si no de su identificador en la memoria esto se le llama ecualidad estructural

```js
let x = [1,2]

let y = x

x === y // true: señala al mismo espacio en la memoria
y === [ 1, 2 ];    // false
x === [ 1, 2 ];    // false
```

### comparacion coerciva

como ya defini anteriormente, comparacion coersiva es cuando durante la comparacion una de las expresiones es convertida para que ambas compartan el mismo tipo y asi poder comparar solo los valores de las expresiones, esto podria considerarse superfluo o hasta indeseado pero es imposible evitarlo, ya que los otras operacion comparativas como ">, <, >=, etc" utilizan este metodo comparativo

```js
false < 1 // true
5 > "1" // true
-14 < true // true
false != 0 // false

var x = "10";
var y = "9";

x < y // true, watch out! si ambos valores comparten el mismo tipo no se realizara ninguna conversion
```

## Como organizar JS

### clases

las clases son una estructura que guarda variables y metodos en un solo ambiente, es solo una estructura y no cuenta con valores propios para hidratarla es necesario inicializar con la keyword "new", tambien necesitara un "constructur" que es basicamente los datos/variables que manejara la estructura, a los que podremos acceder usando la keyword "this" (la cual hace referencia a la instancia de la estructura en la que se usa) seguido del nombre de la variable  

```js
class Book {
    constructor(author,name){
        this.author = author
        this.name = name
    }
    print() {
        console.log(this.author,this.name)
    }
}

let YDKJS = new Book("kevin levin", "you dont know js")
YDKJS.print()
//"kevin levin", "you dont know js"
```

tambien se puede mutar valores que pertenezcan a la estructura, asi como es posible inicializar otras clases como partes de otra estructura (solo se puede inicializar una estructura ya creada no anidar clases) como veremos a continuacion

```js
// creamos la estrucutura de la clase Page
class Page {
    //esta al momento de iniciarse tomara una expresion llamada texto
    constructor(text) {
        // al ponerla en lo alto de la cadena protipica esta variable estara al alcance de toda la estructura
        this.text = text;
    }

    print() {
        // print accede a la variable text y la muestra en consola
        console.log(this.text);
    }
}

class Notebook {
    constructor() {
        // se crea un arreglo vacio al momento de su creacion al alcance de toda la estructura
        this.pages = [];
    }

    addPage(text) {
        // se toma una expresion llamada texto y se inicializa la clase Page que crea 
        var page = new Page(text);
        // se agrega la clase al arreglo page
        this.pages.push(page);
    }

    print() {
        // por cada valor en en el arreglo page 
        for (let page of this.pages) {
            // se llama al metodo print del arreglo definido en la estructura page 
            page.print();
        }
    }
}
// se inicializa
var mathNotes = new Notebook();
// se invoca el metodo addPage
// cada invocacion creara una instancia de la clase Page que tendra que sera guardada en este formato: Page {text: 'Arithmetic: + - * / ...'}
mathNotes.addPage("Arithmetic: + - * / ...");
mathNotes.addPage("Trigonometry: sin cos tan ...");

// se imprimen todas las entradas de texto por orden den llegada
mathNotes.print();
// ..
```

### herencia de clases

cuando requerimos los valores de una clase en otra podemos hacer que esta clase funcione como una extension de la clase original de esta manera heredara las mismas variables que le sean asignadas
```js
class Publication {
    constructor(title,author,pubDate) {
        this.title = title;
        this.author = author;
        this.pubDate = pubDate;
    }

    print() {
        console.log(`
            Title: ${ this.title }
            By: ${ this.author }
            ${ this.pubDate }
        `);
    }
}
```
heredar o polymorfismo
```js
// usamos la palabra clave extends señalando a la estructura de la que queremos heredar sus variables
class Book extends Publication {
    constructor(bookDetails) {
        // usamos la palabra clave super() i hacemos referencia a las variables que queremos heredar
        // a la hora de inicializar una instancia de la clase necesitaremos dar estar variables
        super(
            bookDetails.title,
            bookDetails.author,
            bookDetails.publishedOn
        );
        this.publisher = bookDetails.publisher;
        this.ISBN = bookDetails.ISBN;
    }

    print() {
        super.print();
        console.log(`
            Publisher: ${ this.publisher }
            ISBN: ${ this.ISBN }
        `);
    }
}

class BlogPost extends Publication {
    constructor(title,author,pubDate,URL) {
        super(title,author,pubDate);
        this.URL = URL;
    }

    print() {
        // super.metodo() se hereda uno de los metodos de la clase padre
        super.print();
        console.log(this.URL);
    }
}
```
### modulos

Comparte el mismo objetivo que la strucutura de las clases, organizar y encapsular codigo en una estructura definida solo que este caso la capsula en si no es una clase o la instancia de una, si no, un archivo en si este exportara lo que se necesite del modulo

#### modulo clasico

hay dos tipos de modulos que son distintos no solo de la manera en que funcionan si no tambien en como se definen, el modulo clasico tiene una estructura muy similar a la de las clases 

```js
function Publication(title,author,pubDate) {
    var publicAPI = {
        print() {
            console.log(`
                Title: ${ title }
                By: ${ author }
                ${ pubDate }
            `);
        }
    };

    return publicAPI;
}
```

como se puede apreciar, el constructor de la clase es remplazado por los parametros otorgados a la funcion, para acceder a estos no es necesario usar la keyword "this" ya que son accesibles en la scope de la funcion, un objeto es devuelto con los metodos que usemos dentro de la funcion

```js
function Book(bookDetails) {
    // tampoco es necesario utilizar la palabra clave new para invocar una instancia nueva
    var pub = Publication(
        bookDetails.title,
        bookDetails.author,
        bookDetails.publishedOn
    );

    var publicAPI = {
        print() {
            // al retornarse un objeto de la funcion Publication tenemos acceso a los metodos usando la dot notation aunque pub["print"]() funcionaria igual
            pub.print();
            console.log(`
                Publisher: ${ bookDetails.publisher }
                ISBN: ${ bookDetails.ISBN }
            `);
        }
    };

    return publicAPI;
}

function BlogPost(title,author,pubDate,URL) {
    var pub = Publication(title,author,pubDate);

    var publicAPI = {
        print() {
            pub.print();
            console.log(URL);
        }
    };

    return publicAPI;
}
```
para acceder a los modulos fuera de la scope de un archivo se debe usar el el metodo require("direccion del modulo") y para exportar codigo de dicho modulo se usa module.export = {entradas} 
```js
const math = require('./math');

module.exports = {
  add,
  subtract
};
```

#### modulo ES

a diferencia de los clasicos estos cargan de manera asyncrona solo cargan al ser requeridos e diferencia de los clasicos que cargan todos los modulos al iniciarse el programa la sintaxis sobre todo en como importar y exportar codigo

```js
import { add, subtract } from './math.js';

export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;
```
# Capitulo 3, Escavando javascript

este capitulo abarca en profundidad el funcionamiento basico de javascript en ciertos conceptos que una asumiria como tipicos y sencillos de hecho hay mucha azucar sintatica y lo que ocurre dentro del lenguaje es un poco mas complicado

## itaracion

ua iteracion es la accion de recorrer un grupo de datos pertenecientes a una coleccion o estructura de datos, si se tratara de pocos datos podriamos modificarlos uno por uno pero de ser muchos esto tomaria muchisimo tiempo y recursos, tampoco seria conveniente si cada vez que se fuera a realizar una iteracion se tuviera que definir la estuctura que la hara esto afectaria la lectura del codigo, con esto en mente se crearon los iteradores estandar que aseguran que todo el mundo que use el lenguaje este en la misma pagina a la hora de iterar una estructura de datos como son los arreglos, sets, maps, strings, objetos


```js
// an array is an iterable
var arr = [ 10, 20, 30 ];

for (let val of arr) {
    console.log(`Array value: ${ val }`);
}
// Array value: 10
// Array value: 20
// Array value: 30
```

## clousures

