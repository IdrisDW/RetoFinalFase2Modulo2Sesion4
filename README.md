Arrow function
 
Las funciones flecha o arrow funtions son funciones anónimas con una sintaxis más compacta y que aparte de la diferencia en la sintaxis también tienen algunas peculiaridades como que no vinculan su propio this o que no se pueden usar como constructores.Fueron introducidas en la especificación ES2015
 La declaración de una arrow function es muy muy sencilla:
const giveMeAMessage = () => 'hi arrow functions';
Cuando se componen de una única sentencia no necesitamos emplear la palabra clave return , y el valor que devuelven será aquel empleado como cuerpo de la función.
Por tanto, cuando invoquemos nuestra función giveMeAMessage , lo que obtendremos será el texto hi arrow functions :
const giveMeAMessage = () => 'hi arrow functions'; const aMessage = giveMeAMessage(); console.log(aMessage); // hi arrow functions
Si queremos devolver un objeto, deberemos emplear los paréntesis para rodear el cuerpo de la función:
INCORRECTO const giveMeADeveloper = () => { name: 'Gerardo', age: '33' };
CORRECTO  const giveMeADeveloper = () => ({ name: 'Gerardo', age: '33' });
Las arrow functions pueden componerse de más de una línea, lo cual ya nos obligará a emplear los paréntesis y a emplear return para, ahora sí, especificar el valor de retorno:
const giveMeAMessage = () => { const foo = 'hi arrow functions'; return foo; }
Argumentos en las arrow functions 

Por otra parte, cuando queramos pasar parámetros a este tipo de funciones podremos hacerlo de dos formas. En el caso de que nuestra función tenga un único argumento no será necesario especificar los paréntesis. Por ejemplo: 
const triple = x => x*3; const foo = triple(3); // 9
 En el resto de casos sí que necesitaremos especificar los paréntesis: 
const sum = (a, b) => a + b; const foo = sum(1, 2); // 3 
Por lo demás, esta clase de funciones también nos permite especificar valores por defecto: 
const pow = (a, b = 2) => Math.pow(a, b); const foo = pow(2); // 4 const bar = pow(3, 3); // 27
This y las funciones flecha

Supongamos que tenemos un objeto con el siguiente aspecto:
const foo = { log: function() { return function() { console.log(this); } } } 
Cuando ejecutemos lo siguiente lo que obtendremos en la consola será el objeto Window (si estamos dentro de un navegador, claro):
foo.log()(); // Window

Ya que la invocación de la función devuelta por el método log del objeto foo es realizada por window , por lo que no se respeta el valor de this tal y como esperaríamos.
const foo = {
  log: function() { 
    console.log(this); // 1. foo
    return function() {
      console.log(this); // 2. Window
    }
  }
}
const log = foo.log(); // 1. foo
log(); // 2. Window

Sin embargo, cuando trabajamos con arrow functions el comportamiento que obtenemos es esperado, ya que estas funciones tienen un alcance léxico, de modo que el valor de la variable this dentro de una arrow function viene determinado por el alcance que la rodea. Es decir:
 const foo = { log: function() { console.log(this); // 1. foo return () => { 
// this is lexically scoped to the surrounding scope,
 // ie, the foo object 
console.log(this); 
// 2. foo } } } const log = foo.log();
 // 1. foo log(); // 2. foo
Arrow functions y destructuring

Una característica con la que las arrow functions se llevan genial es con el destructuring assignment. 
De este modo, cuando pasemos un objeto a una función de este tipo, podremos acceder directamente a sus propiedades de una forma muy visual: 
const printAge = ({age}) => console.log(age); printAge({name: 'Gerardo', age: 33});
 Así como declarar parámetros por defecto empleando esta característica: 
const printAge = ({age} = {age: 20}) => console.log(age); printAge({name: 'Gerardo', age: 33}); // 33 printAge(); // 20

Limitaciones de las arrow functions
Sin embargo, las arrow functions tienen algunas limitaciones. Entre ellas me gustaría destacar las siguientes.
No podemos emplearlas para construir objetos.
Por tanto, si intentamos algo de este estilo: 
const MyClass = () => {}; const object = new MyClass(); 
Obtendremos un TypeError .
No poseen prototype 
Es decir, no podemos extender el prototipo de esta clase de objetos. 
const MyClass = () => {}; console.log(MyClass.prototype); // undefined
No pueden ser usadas como funciones generadoras 
Las arrow functions no admiten la palabra yield dentro de su cuerpo, por lo que si queremos crear una función generadora deberemos seguir recurriendo a la forma habitual: 
function* .
