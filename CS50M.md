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

### User Input

- Controlled vs uncontrolled components: Where is the source of truth for the value of an input?
- React recommends always using controlled components
- Pass value and onChangeText props

### Handling multiple inputs

- <form> exists in HTML, but not in React Native
- With controlled components, we maintain an object with all inputs’ values
- We can define a function that handles the data to submit

### Validating Input

- Conditionally set state based on input value
- Validate form before submitting
- Validate form after changing single input value
- this.setState() can take a callback as the second argument
- componentDidUpdate()

### KeyboardAvoidingView

- Native component to handle avoiding the virtual keyboard
- Good for simple/short forms
- The view moves independent of any of its child TextInputs

### Debugging

- React errors/warnings
- Chrome Developer Tools (devtools)
- React Native Inspector
- react-devtools

### React Errors and Warnings

- Errors show up as full page alerts
- Trigger with consssole.error()
- Warnings are yellow banners
- Trigger with console.warn()
- ○n production mode

### Chrome Devtools

- Google Chrome has amazing developer tools (debugger)
- We can run the JavaScript inside a Chrome tab
- Separate threads for native and JavaScript
- Communicate asynchronously through bridge
- No reason that the JavaScript needs to be run on device

### React Native Inspector

- Analogous to the Chrome element inspector
- Allows you to inspect data associated with elements, such as margin, padding, size, etc.
- Does not allow you to live-edit elements

### react-devtools

- “Inspect the React component hierarchy, including component props and state.”
- Install with `npm install -g react-devtools`
- Run with `react-devtools`

### External Libraries

- Libraries are code written outside the context of your project that you can bring into your project
- Since React Native is just JavaScript, you can add any JavaScript library
- Install using `npm install <library>`
- Use the --save flag for npm@"<5"
- Use the -g flag to install things globally
- Import into your project: import React from 'react

---

## Navigation

### What is navigation?

- Navigation is a broad term that covers topics related to how you move between screens in your app
- Web navigation is oriented around URLs
- Mobile apps do not use URLs for navigating within the app
- Navigation APIs completely different on iOS and Android
- Several React Native libraries provide a platform agnostic alternative
- We will talk about one of them today, React Navigation

### React Navigation and alternatives

- Two distinct approaches
  1.Implement mainly in JavaScript with React
  2.Implement mostly in native, expose an interface to JavaScript for existing native navigation APIs
- React Navigation takes approach #1

### Navigators, routes, and screen components

- A navigator is a component that implements a navigation pattern (eg: tabs)
- Each navigator must have one or more routes.
- A navigator is a parent of a route.
- A route is a child of a navigator.
- Each route must have a name and a screen component.
- The name is usually unique across the app
- The screen component is a React component that is rendered when the route is active.
- The screen component can also be another navigator

### Switch Navigator

- Display one screen at a time
- Inactive screens are unmounted
- The only action a user can take to switch from one route to another

### Higher order components

- createSwitchNavigator is a Higher Order Component: it is a function that returns a React component.
- “A higher-order component (HOC) is an advanced technique in Reactfor reusing component logic.”
- This is similar to higher order functions, which are functions that either take functions as arguments or return a function as a result.

### Stack Navigator

- Display one screen at a time
- The state of inactive screens is maintained and they remain mounted
- Platform-specific layout, animations, and gestures○Screens are stacked on top of each other
- iOS: screens slide in from right to left, can be dismissed with left to right gesture. Modal screens slide in from bottom to top, can be dismissed with top to bottom gesture.
- Android: screens fade in on top of each other, no dismiss gesture. Hardware back button dismisses the active screen.
- Users can push and pop items from the stack, replace the current item, and various other

### Composing navigators

- Navigators can be composed when one type of navigation visually appears to be inside another navigator
- A navigator can be the Screen Component of another navigator
- The app should only contain one top-level navigator
- You can navigate() to any route in the app●goBack() works for the whole app, supports Android back button

### Tab navigators

- Display one screen at a time●The state of inactive screens is maintained
- Platform-specific layout, animations, and gestures
- The navigate() action is used to switch to different tabs
- goBack() can be called to go back to the first tab
- The tab navigator goBack behavior is configurable

---

## Data

### Data

- Not all apps are self-contained
- Any app that wants to rely on information not computed within the app needs to get it from somewhere
- Communicate with other resources using an API

### API

- “Application Programming Interface”
- A defined set of ways with which a resource can be interacted
- React components have APIs; you interact by passing props
- A class has an API; you interact by invoking methods
- A web service has an API; you interact by making network requests
- Providers often get to decide on the API, but sometimes it’s decided for them
- Consumers have to read docs to know how to use an API

### Making Network Requests

- fetch() is polyfilled
- It’s not natively part of JavaScript, but it is implemented to match the usage of the browser fetch()
- fetch() expects an URL and optionally some config
- fetch() returns a Promise, which is fulfilled with a Response object

### Promises

- Allows writing asynchronous, non-blocking code
- Allows chaining callbacks and/or error handlers
- .then() - executed after the previous Promise block returns
- .catch() - executed if the previous Promise block errors

###Async/Await

- Allows writing async code as if it were synchronous
- Still non-blocking
- A function can be marked as async, and it will return a Promise
- Within an async function, you can await the value of another async function or Promise
- Use try/catch to handle errors

### Transforming Data

- Sometimes the shape of the data returned by an API isn’t ideal
- Where should we do this “transformation?”
- Doing it early gives us an abstraction barrier and is more efficient

### Authentication

- A process to determine if a user is who they say they are
- Generally done using a name and password
- But how do we send the name and password in the request?

### HTTP Methods

- GET
- The default in browsers and in fetch()
- Add parameters in the url by appending a ? and chaining key=valuepairs separated by &
- POST
- Submit data (e.g. a form) to an endpoint
- Parameters are included in the request body
- If POSTing JSON, must have content-type: application/json header and body must be JSON string

### HTTP Response Codes

- Every network response has a “code” associated with it
- 200: OK
- 400: Bad Request
- 404: Not Found
- 500: Internal Server Error

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
