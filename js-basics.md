# JS Basic Knowledge

### 7 Data Types
-  6 primitive data types: Boolean, Null, Undefined, Number, String, Symbol
- and Objects (Indexed Collections (Arrays), Keyed Collections (Sets, Maps), Dates)

### Equality
- When you use `==` or `!=`, JavaScript first converts each value to the same type (type coercion).  
  This is often not the behavior you want, and it’s actually considered bad practice to use `==` or `!=`  
  when comparing values for equality.
- `==` equality by value (implicit type coercion)
- `"1" == 1 // => true`: Number `1` (right side) becomes String `"1"` and the value of `"1" == "1"` equals to true
- `"Peter" + 1 // => Peter1`: Number `1` (right side) becomes String `"1"`, then `"Peter"` and `"1"` get concatenated

- null: has the value null: `var count = null;`
- undefined: no value: `var count;`
- NaN: Not a Number: `"Hello" / 10`: To perform a division, "Hello" is coerced into the Number data type.  
  When "Hello" is converted into a number, the result is NaN (Not a Number). (attention: + and *)

### Strict equality
- Better to use strict equality to see if numbers, strings, or booleans, etc. are identical in type and value  
  without doing the type conversion first. 
- `===` or `!==` 
- `"1" === 1` // => false: string "1" is not the same type AND value as the number 1
- `0 === false` // => false: number 0 is not the same type AND value as the boolean false

### Ternary operator 
- a shortcut alternative for writing lengthy if...else statements
- `conditional ? (if condition is true) : (if condition is false)`

```js
var isGoing = true;
var color = isGoing ? "green" : "red";
console.log(color);
// => "green"
```

### 6 Falsy Values
- the Boolean value false
- the null type
- the undefined type
- the number 0(.0...)
- the empty string ""
- the odd value NaN

### Scopes
- global, function and block scope
- let variable for block scope {...}, for example to exist within an if statement.
- This is useful because it provides another scoping layer for variables. Variables using the var keyword
  are accessible to the whole function’s scope. 
- For temporary variables, such as the i in a loop (which  get thrown away as soon as the loop is done) the variable would normally hang   around until the end of the function’s life. 
- With a let variable this is very effectively solved, as the let variable only exists for the life of the loop, and is then nicely       cleaned up.   
- global: can be accessed anywhere in the program
- function: can be accessed anywhere in its function
- Shadowing: Scope Overriding: function overrides global variable
- When trying to access an identifier, the JavaScript Engine will first look in the current function.   
  If it doesn't find anything, it will continue to the next outer function to see if it can find the identifier there.   
  It will keep doing this until it reaches the global scope.
- Global identifiers are a bad idea. They can lead to bad variable names, conflicting variable names, and messy code.

### Closures
- to come

### Hoisting
- before execution, all declarations (function and variable) get hosted to the top (NOT the assignments!)

```js
sayHi("Peter");
function sayHi(name) {
  console.log(greeting + " " + name);
  var greeting = "Hello";
}
// => var greeting gets declared, but assignment stays at the bottom
sayHi("Peter");
function sayHi(name) {
  var greeting; //declaration
  console.log(greeting + " " + name);
  greeting = "Hello"; //assignment
}
```

### Function Expressions
```js
Anonymous:
var simonVar = function(){console.log("hello simon");}
simonVar; // ƒ (){console.log("hello simon");}
simonVar(); // hello simon

Named:
var simonVar = function simonFunction(){console.log("hello simon");  }
simonVar; // ƒ simonFunction(){console.log("hello simon"); }
simonVar(); // hello simon
simonFunction(); // Uncaught ReferenceError: simonFunction is not defined at <anonymous>
```

### Callbacks
-  A function that is passed into another function is called a callback

### Inline Function Expression
```js
// Function declaration with arguments
function movies(messageFunction, name) { messageFunction(name); }

// Call the movies function, pass in the function and name of movie
movies(function displayFavorite(movieName) { console.log("My favorite movie is " + movieName);}, "Finding Nemo");

// messageFunction = function displayFavorite(movieName) { console.log("My favorite movie is " + movieName);}
// name of function (displayFavorite) is optional (anonymoous)
// name = "Finding Nemo"
```

- Anonymous inline function expressions are often used with function callbacks that are not going to be reused elsewhere to save many     lines of code to just define it.
  

### Event Handling
- onload, onfocus, onclick, onchange, onsubmit
- onmouseover, onmouseout, onmousedown, onmouseup
- onkeydown, onkeyup, unkeypress
- setTimeout

### OOP
- reuse code => factor out similar patterns
- Class Patterns: functional, prototypal, pseudoclassical

#### this
- generelly bound to the object on the left of the dot/brackets
- without dot/brackets: global

#### Prototype Chains
````js
var obj1 = {a:1};
var obj2 = extend({}, obj1); // one-time copy of obj1
var obj3 = Object.create(obj1); // ongoing lookup from obj1

obj1.b = 2;

console.log(obj2.b) // undefined => obj2 was copied before obj1 created its b
console.log(obj3.b) // 3 => obj3 has no b, but falls through to its prototyp, obj1
````

- obj.prototype: default function with every object
````js
var Car = function(loc){
  var obj = Object.create(Car.prototype);
  obj.loc = loc;
  return obj;
};
Car.prototype.move = function(){
    this.loc++;
};
````

- keyword `new` insert: `this = obj.create(.prototype)` and `return obj`
````js
var Car = function(loc){
  this.loc = loc;
};
Car.prototype.move = function(){
    this.loc++;
};

var car1 = Car(1); // undefined - obj.create and return obj missing through new
var var2 = new Car(1) // Car {loc: 1}
````

- Summary
````js
var Car = function(loc){this.loc = loc;}; // how all instances are different, not every obj has the same loc
Car.prototype.move = function(){this.loc++;}; // how all instance are similar
````

### Superclasses and Subclasses
````js
var Car = function(loc){
  this.loc = loc;
};
Car.prototype.move = function(){
  this.loc++;
};
var Van = function(loc){
  Car.call(this, loc);
};
Van.prototype = Object.create(Car.prototype);
Van.prototype.constructor = Van;
Van.prototype.grab = function(){...};
````

### Strings
- length
- indexOf, lastIndexOf // first, last
- toLowerCase, toUpperCase
- replace

### Math
- Pi, sqrt, pow
- floor (down), ceil (up), round (up/down)

### Arrays
- standard data structure to store multiple values organized
- [MDN: Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- [Wikipedia: Array](https://en.wikipedia.org/wiki/Array_data_structure)
- [Big-O](http://bigocheatsheet.com/)
- `var arr = []; // create empty array`
- useful properties and methods:
  - push(): add to the end
  - pop(): remove from the end
  - splice(i, n, a): remove n items at index i and add a
  - delete arr[i]: delete at index i
  - join(''): combine the elements in an array to form a string
  - concat(b): add the array b to the end of the array
  - length: returns the number of elements in that array
  - reverse(): reverse order
  - sort(): sort unicode // 10 before 2
  - unshift(): add to the front
  - shift(): remove from the front
  - map(): perform some operation on each element of the array, and return a new array
  
#### for ... in / for ... of
````js
let arr = ["dog", "cat", "mouse"];

for (let i in arr) {
   console.log(i); // "0", "1", "2" => name of property
}

for (let i of arr) {
   console.log(i); // "dog", "cat", "mouse" => value of property
}
````



### Recipes
- undefined; declared, but not assigned
- check if declared: `typeof a !== 'undefined';`
- null: declared and assigned null
- check if value is null: `!a;`
- current date: `Date();`
- check if is a is an instance of b: `a instanceof b;`
- String formating: `console.log("Hello ${name}!");`

`
