# CS50 Mobile

## Overview, JavaScript

### JavaScript is Interpreted
- Each browser has its own JavaScript engine, which either interprets the code, or uses some sort of lazy compilation:
	- V8: Chrome and Node.js
	- SpiderMonkey: Firefox
	- JavaScriptCore: Safari
	- Chakra: Microsoft Edge/IE
- They each implement the ECMAScript standard, but may differ for anything not defined by the standard

### Prototypal Inheritance
- Non-primitive types have a few properties/methods associated with them
	- Array.prototype.push()
	- String.prototype.toUpperCase()
- Each object stores a reference to its prototype
- Properties/methods defined most tightly to the instance have priority
- Most primitive types have object wrappers: String(), Number() etc.
- JS will automatically “box” (wrap) primitive values so you have access to methods

- Why use reference to prototype?
- What’s the alternative?
- What’s the danger?

### Scope
- Variable lifetime
	- Lexical scoping (var): from when they’re declared until when their function ends
	- Block scoping (const, let): until the next } is reached
- Hoisting: Function definitions are hoisted, but not lexically-scoped initializations
- But how/why?

### JavaScript Engine
- Before executing the code, the engine reads the entire file and will throw a syntax error if one is found
	- Any function definitions will be saved in memory
	- Variable initializations will not be run, but lexically-scoped variable names will be declare

### The Global Object
- All variables and functions are actually parameters and methods on the global object
	- Browser global object is the `window` object
	- Node.js global object is the `global` object

---

## JavaScript, ES6

### Closures
- Functions that refer to variables declared by parent function still have access to those variables
- Possible because of JavaScript’s scoping

### Immediately Invoked Function Expression
- A function expression that gets invoked immediately
- Creates closure
- Doesn’t add to or modify global object

### First-Class Functions
- Functions are treated the same way as any other value
	- Can be assigned to variables, array values, object values
	- Can be passed as arguments to other functions
	- Can be returned from functions
- Allows for the creation of higher-order functions
	- Either takes one or more functions as arguments or returns a function
	- map(), filter(), reduce()

### Synchronous? Async? Single-Threaded?
- JavaScript is a single-threaded, synchronous language
- A function that takes a long time to run will cause a page to become unresponsive
- JavaScript has functions that act asynchronously
- But how can it be both synchronous and asynchronous?

### Asynchronous JavaScript
### Execution Stack
- Functions invoked by other functions get added to the call stack
- When functions complete, they are removed from the stack and the frame below continues executing
- stack => queue

### Overflow
- stack and queue can run out of memory

### Asynchronous
- setTimeout()
- XMLHttpRequest(), jQuery.ajax(), fetch()
- Database calls

### Callbacks
- Control flow with asynchronous calls
- Execute function once asynchronous call returns value
	- Program doesn’t have to halt and wait for value

### Promises
- Alleviate “callback hell”
- Allows you to write code that assumes a value is returned within a success function
- Only needs a single error handler

### Async/Await
- Allows people to write async code as if it were synchronous

### this
- Refers to an object that’s set at the creation of a new execution context (function invocation)
- In the global execution context, refers to global object
- If the function is called as a method of an object, `this` is bound to the object the method is called on
- Setting `this` manually: bind(), call(), apply(), ES6 arrow notation

### Browsers and the DOM
- Browsers render HTML to a webpage
- HTML defines a tree-like structure
- Browsers construct this tree in memory before painting the page
- Tree is called the Document Object Model
- The DOM can be modified using JavaScript

---

## React, Props, State

---

## React Native

---

## Lists, User Input

---

## User Input, Debugging

---

## Navigation

---

## Data

---

## Expo Components

---

## Redux

---

## Async Redux, Tools

---

## Performance

---

## Deploying, Testing
