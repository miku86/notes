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
