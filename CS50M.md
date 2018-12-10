# CS50 Mobile

## Overview, JavaScript

### JavaScript is Interpreted

- Each browser has its own JavaScript engine, which either interprets the code, or uses some sort of lazy compilation: V8: Chrome and Node.js, SpiderMonkey: Firefox, JavaScriptCore: Safari, Chakra: Microsoft Edge/IE
- They each implement the ECMAScript standard, but may differ for anything not defined by the standard

### Prototypal Inheritance

- Non-primitive types have a few properties/methods associated with them, e.g. Array.prototype.push(), String.prototype.toUpperCase()
- Each object stores a reference to its prototype
- Properties/methods defined most tightly to the instance have priority
- Most primitive types have object wrappers: String(), Number() etc.
- JS will automatically “box” (wrap) primitive values so you have access to methods

- Why use reference to prototype?
- What’s the alternative?
- What’s the danger?

### Scope

- Lifetime: Lexical scoping (var): from when they’re declared until when their function ends
- Lifetime: Block scoping (const, let): until the next } is reached
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

### Classes

- Syntax introduced in ES6
- Simplifies the defining of complex objects with their own prototypes
- Classes vs instances
- Methods vs static methods vs properties
- new, constructor, extends, Super

### React

- Allows us to write declarative views that “react” to changes in data
- Allows us to abstract complex problems into smaller components
- Allows us to write simple code that is still performanT

### Imperative vs Declarative

- How vs What
- Imperative programming outlines a series of steps to get to what you want
- Declarative programming just declares what you want

### React is Declarative

- Imperative vs Declarative
- The browser APIs aren’t fun to work with
- React allows us to write what we want, and the library will take care of the DOM manipulation

### React is Easily Componentized

- Breaking a complex problem into discrete components
- Can reuse these components: Consistency, Iteration speed
- React’s declarative nature makes it easy to customize components

### React is Performant

- We write what we want and React will do the hard work
- Reconciliation
- the process by which React syncs changes in app state to the DOM:
- Reconstructs the virtual DOM
- Diffs the virtual DOM against the DOM
- Only makes the changes needed

### Writing React

- JSX:
- XML-like syntax extension of JavaScript
- Transpiles to JavaScript
- Lowercase tags are treated as HTML/SVG tags, uppercase are treated as custom components
- Components are just functions:
- Returns a node (something React can render)
- Receives an object of the properties that are passed to the element

### Props

- Passed as an object to a component and used to compute the returned node
- Changes in these props will cause a recomputation of the returned node (“render”)
- Unlike in HTML, these can be any JS value

### State

- Adds internally-managed configuration for a component
- `this.state` is a class property on the component instance
- Can only be updated by invoking `this.setState()`
- Implemented in React.Component
- setState() calls are batched and run asynchronously
- Pass an object to be merged, or a function of previous state
- Changes in state also cause re-renders

### React Native

- A framework that relies on React core
- Allows us build mobile apps using only JavaScript: “Learn once, write anywhere”
- Supports iOS and Android

---

## React Native

- A framework that relies on React core
- Allows us build mobile apps using only JavaScript: “Learn once, write anywhere”
- Supports iOS and Android

### How does React Native work?

- JavaScript is bundled: Transpiled and minified
- Separate threads for UI, layout and JavaScript
- Communicate asynchronously through a “bridge”
- JS thread will request UI elements to be shown
- JS thread can be blocked and UI will still work

### Differences between RN and Web

- Base components
- Style
- No browser APIs
- CSS animations, Canvas, SVG etc.
- Some have been polyfilled (fetch, timers, console etc.)
- Navigation

### React Native Components

- Not globally in scope like React web components
- Import from 'react-native'
- div → View
- span → Text: All text must be wrapped by a <Text /> tag
- button → Button
- ScrollView

### Style

- React Native uses JS objects for styling
- Object keys are based on CSS properties
- Flexbox layout: Default to column layout
- Lengths are in unitless numbers
- style prop can take an array of styles
- StyleSheet.create()
- Functionally the same as creating objects for style
- Additional optimization: only sends IDs over the bridge

### Event Handling

- Unlike web, not every component has every interaction
- Only a few “touchable” components: Button, TouchableOpacity, TouchableHighlight, TouchableWithoutFeedback, TouchableNativeFeedback (Android only)
- Web handlers will receive the event as an argument, but React Native handlers often receive different arguments

### Components

- Return a node (something that can be rendered)
- Represent a discrete piece of the UI
- “All React components must act like pure functions with respect to their props.”
- Two types: Stateless Functional Component (SFC) a.k.a. Pure Functional Component, React.Component

### Stateless Functional Component (SFC)

- Simplest component: use when you don’t need state
- A function that takes props and returns a node
- Should be “pure” (it should not have any side effects like setting values, updating arrays etc.)
- Any change in props will cause the function to be re-invoked

### React.Component

- An abstract class that can be extended to behave however you want
- These have additional features that SFCs don’t
- Have instances
- Maintain their own state
- Have lifecycle methods (similar to hooks or event handlers) that are automatically invoked
- Rendering now becomes a function of props and class properties

### Component Lifecycles

- Mount
- Update
- Unmount

### Mount

- constructor(props): Initialize state or other class properties (bound methods etc.)
- render(): The meat of a component, Return a node
- componentDidMount(): Do anything that isn’t needed for UI (async actions, timers etc.), Setting state here will cause a re-render before updating the UI

### Update

- componentWillReceiveProps(nextProps): Update any state fields that rely on props
- shouldComponentUpdate(nextProps, nextState): Compare changed values, return true if the component should rerender, If returned false, the update cycle terminates, Almost always a premature optimization
- render()
- componentDidUpdate(prevProps, prevState): Do anything that isn’t needed for UI (network requests etc.)

### Unmount

- componentWillUnmount(): Clean upe, e.g. Remove event listeners, Invalidate network requests, Clear timeouts/intervals

### Expo

- “The fastest way to build an app”
- Suite of tools to accelerate the React Native development process:
- Snack: runs React Native in the browser
- XDE: a GUI to serve, share, and publish your Expo projects
- CLI: a command-line interface to serve, share, and publish projects
- Client: runs your projects on your phone while developing
- SDK: bundles and exposes cross-platform libraries and API

### Import/Export

- Components are great for simplifying code
- We can split components into their own files: Helps organize project, Export the component from the file
- Import the component before using it in a file
- Default vs named import/export

### PropTypes

- React can validate the types of component props at runtime
- Development tool that allows developers to ensure they’re passing correct props
- Helps document your components’ APIs
- Only runs in development mod

### How to Read Docs

- Have a goal in mind
- See what the library/framework/API offers
- Find something that solves your problem
- Configure using the exposed API

---

## Lists, User Input

### Lists

- In web, browsers will automatically become scrollable for
  content with heights taller than the window
- In mobile, we need to do that manually: ScrollView, FlatList, SectionList

### ScrollVissew

- The most basic scrolling view
- Will render all of its children before appearing
- To render an array of data, use `map()`
- Components in an array need a unique key prop

### FlatList

- A performant scrolling view for rendering data
- “Virtualized:” only renders what’s needed at a time
- Only the visible rows are rendered in first cycle
- Rows are recycled, and rows that leave visibility may be unmounted
- Pass an array of data and a renderItem function as props
- Only updates if props are changed, Immutability is important

### SectionList

- Like FlatList with additional support for sections
- Instead of data prop, define sections: Each section has its own data array, Each section can override the renderItem function with their own custom renderer
- Pass a renderSectionHeader function for section headers

### User Input

- Controlled vs uncontrolled components
- Where is the source of truth for the value of an input?
- React recommends always using controlled components
- Pass value and onChangeText props

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
