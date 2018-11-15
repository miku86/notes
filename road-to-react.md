# Road to React - Summary

## Hot Module Replacement:

- a tool for reloading your application in the browser without the page refresh
- you can keep the application state after the application reloads
- add to index.js

```js
if (module.hot) {
  module.hot.accept();
}
```

## Class methods can be auto-bound using JavaScript ES6 arrow functions

```js
handleClick = () => {
  console.log(this);
};
```

Use this method if the repetitive binding in the constructor annoys you. The official React
documentation sticks to the class method bindings in the constructor.

## Higher Order Functions

The following code wouldn’t work, because the class method would be executed immediately when you open the application in the browser: `onClick={this.onDismiss(item.objectID)}`

When using `onClick={doSomething()}`, `doSomething()` executes immediately when the application is opened in a browser. The expression in the handler is evaluated. Since the returned value of the function isn’t a function anymore, nothing would happen when you click the button. But using `onClick={doSomething}`, where `doSomething` is a function, would only be executed if the button is clicked.

However, using `onClick={this.onDismiss}` wouldn’t suffice, because the `item.objectID` property needs to be passed to the class method to identify the item that should be dismissed.

We wrap it into another function to sneak in the property: `onClick={() => this.onDismiss(item.objectID)}`

## Controlled Components

An HTML `input` tag comes with a `value` attribute. The value attribute usually contains the value shown in the input field. Form elements hold their own state in plain HTML. They modify the value internally once someone changes it from the outside. In React, that’s called an uncontrolled component, because it handles its own state. We want to make sure those elements are controlled components instead.

To do this, we set the `value` attribute of the `input` field, which is already saved in the state property, so we can access it from there.

## Reusable Components

Reusable and composable components empower you to come up with capable component hierarchies, the foundation of React’s view layer. It might seem redundant to declare components like this, but it’s not.

We use a Button component instead of a button element, which spares only the type="button". It might not seem like a huge win, but these measures are about long term.
Imagine you have several buttons in your application, and you want to change an attribute, style, or behavior for just one. Without the component, you’d have to change (refactor) each one. The Button component ensures that the operation has a single source of truth, or one Button to refactor all the others at once.

## Component Declarations

Functional Stateless Components:

- are functions that take input and return an output
- the inputs are the props, and the output is a component instance in plain JSX
- functional stateless components are functions (functional) and they have no local state (stateless)
- you cannot access or update the state with this.state or this.setState() because there is no this object
- have no lifecycle methods except for the render() method which will be applied implicitly in functional stateless components

ES6 Class Components:

- extend from the React component, the extend hooks all the lifecycle methods of the React component API to the component
- you can store and manipulate state in ES6 class components using this.state and this.setState()

What to use:

- rule of thumb: use functional stateless components when you don’t need local state or component lifecycle methods
- usually, we implement components as functional stateless components, but once access to the state or lifecycle methods is required, we have to refactor it to an ES6 class component

## Lifecycle Methods

### Mounting: the component gets instantiated.

The mounting process has 4 lifecycle methods, invoked in the following order:

- constructor(): is called when the component gets initialized. You can set an initial component state and bind class methods during that lifecycle method.
- getDerivedStateFromProps(props, state): should return an object to update the state, or null to update nothing. It exists for rare use cases where the state depends on changes in props over time.
- render(): returns elements as an output of the component. The method should be pure, so it shouldn’t modify the component state. It gets an input as props and state, and returns an element.
- componentDidMount(): called once, when the component mounted. Perfect time to do an async request to fetch data. The fetched data is stored in state to display it in the render() lifecycle method.

### Updating: when the state or the props change.

The updating process has 5 lifecycle methods, invoked in the following order:

- getDerivedStateFromProps(props, state): should return an object to update the state, or null to update nothing. It exists for rare use cases where the state depends on changes in props over time.
- shouldComponentUpdate(nextProps, nextState): called when the component updates due to state or props changes. Depending on this return from this lifecycle method, you can prevent the render lifecycle method of a component.
- render(): returns elements as an output of the component. The method should be pure, so it shouldn’t modify the component state. It gets an input as props and state, and returns an element.
- getSnapshotBeforeUpdate(prevProps, prevState): invoked before the most recently rendered output is committed to the DOM. Enables the component to capture information from the DOM before it is potentially changed.
- componentDidUpdate(prevProps, prevState, snapshot) is a lifecycle method that is invoked immediately after updating, but not for the initial render. You can use it as to perform DOM operations or to perform more asynchronous requests. If your component implements the getSnapshotBeforeUpdate() method, the value it returns will be received as the snapshot parameter.

### Unmounting lifecycle

- componentWillUnmount() is called before you destroy your component. You can use this lifecycle method to perform any clean up tasks.

## Client Cache

Each search submit makes a request to the API. You might search for “redux”, followed by “react” and eventually “redux” again. In total it makes 3 requests. But you searched for “redux”
twice and both times it took a whole asynchronous roundtrip to fetch the data. In a client-sided cache, you would store each result. When a request to the API is made, it checks if a result is already there and uses the cache if it is. Otherwise an API request is made to fetch the data.

To have a client cache for each result, you have to store multiple results rather than one result in your local component state. The results object will be a map with the search term as key and the
result as value. Each result from the API will be saved by the search term (key).

## Error Handling

We introduce an efficient solution to add error handling for your application in case of an erroneous API request. We have learned the necessary building block to introduce error handling
in React: local state and conditional rendering. The error is just another state, which we store in the local state and display with conditional rendering in the component.

## Axios instead of Fetch

The browser allows you to use this native fetch API. However, not all browsers support this, older browsers especially. Once you start testing your application in a headless browser environment, there can be issues with the fetch API. One alternative is to substitute the native fetch API with a stable library such as axios, which performs asynchronous requests to remote APIs.

You can use axios instead of fetch() , and its usage looks almost identical to the native fetch API. It takes the URL as argument and returns a promise. You don’t have to transform the returned response to JSON anymore, since axios wraps the result into a data object in JavaScript.

## Snapshot Tests with Jest

Testing source code is essential to programming, and should be seen as mandatory. We want to keep the quality of your code high and make sure everything works before using it in production.

We will use the testing pyramid as our guide. The testing pyramid includes end-to-end tests, integration tests, and unit tests.

A unit test is for an isolated and small block of code, such a single function. However, sometimes units work well in isolation but not in combination with other units, so they need to be tested as a group. That’s where integration tests can help us figure out if units work well together. An end-to-end test is a simulation of a real-life scenario, such as the automated setup of a browser simulating the login flow in a web application. Where unit tests are fast and easy to write and maintain, end-to-end tests are at the opposite of the spectrum.

We want to have many unit tests covering the isolated functions. After that, we can use several integration tests to make sure the most important functions work in combination as expected. Finally, we may need a few end-to-end tests to simulate critical scenarios.

The foundation for testing in React are component tests, generalized partly as unit tests and partly as snapshot tests.

Jest is used for component tests by the React community. Fortunately, create-react-app already comes with Jest, so you don’t need to set it up. Before you can test your first components, you have to export them from your src/App.js file.

These tests make a snapshot of your rendered component and runs it against future snapshots. When a future snapshot changes, you will get notified in the test. You can either accept the snapshot change, because you changed the component implementation on purpose, or deny the change and investigate for the error. It complements unit tests very well, because you only test the differences of the rendered output. It doesn’t add big maintenance costs since you can accept snapshots for intentional changes.

Jest stores snapshots in a folder so it can validate the diff against a future snapshot. This also lets use share snapshots across teams when having version control such as git in place. Before writing your first snapshot test with Jest, you have to install its utility library: `react-test-renderer`.

```js
test('has a valid snapshot', () => {
  const component = renderer.create(<App />);
  const tree = component.toJSON();
  expect(tree).toMatchSnapshot();
});
```

Run your tests again and observe how they succeed or fail. Once you change the output of the render block in your App component, the snapshot test should fail. Then you can decide to update
the snapshot or investigate in your App component. The renderer.create() function creates a snapshot of your App component. It renders it virtually, and then stores the DOM into a snapshot. Afterward, the snapshot is expected to match the previous version from the last test. This is how we make sure the DOM stays the same and doesn’t change anything by accident.

Snapshot tests usually stay pretty basic. You only want to make sure the component doesn’t change its output. Once it does, you have to decide if you accept the changes, otherwise you have to fix the component.

## Unit Tests with Enzyme

Enzyme is a testing utility by Airbnb to assert, manipulate, and traverse React components. It is used to conduct unit tests to complement snapshot tests in React. First we have to install it along
with its extension, since it doesn’t come with create-react-app.

Shallow renders the component without its child components, so you can dedicate the test to one component.

Enzyme has three rendering mechanisms in its API. You already know shallow() , but there is also mount() and render() . Both instantiate instances of the parent component and all child components.
mount() gives you access to the component lifecycle methods. These are the rules of them as to when to use each mechanism:

- Always begin with a shallow test
- If componentDidMount() or componentDidUpdate() should be tested, use mount()
- If you want to test component lifecycle and children behavior, use mount()
- If you want to test a component’s children rendering with less overhead than mount() and you are not interested in lifecycle methods, use render()

Continue to unit test your components, but be sure to keep the tests simple and maintainable. Otherwise you will have to refactor them once you change your components. This is one the main reason Facebook introduced snapshot tests with Jest.

## Component Interface with PropTypes

A typed language is less error prone because the code gets validated based on its program text. Editors and other utilities can catch these errors before the program runs. React comes with a built-in type checker to prevent bugs. You can use PropTypes to describe your component interface. All the props passed from a parent component to a child get validated based on the PropTypes interface assigned to the child.

Essentially, we want to take every argument from the function signature and assign a PropType to it. The basic PropTypes for primitives and complex objects are: PropTypes.array, PropTypes.bool, PropTypes.func, PropTypes.number, PropTypes.object, PropTypes.string.

Example: `className: PropTypes.string.isRequired`

## Ref a DOM Element

Sometimes you need to interact with your DOM nodes in React. The ref attribute gives you access to a node in your elements. That is usually an anti pattern in React, because you should use its declarative way of doing things and its unidirectional data flow. But there are certain cases where you need access to the DOM node: to use the DOM API (focus, media playback etc.), to invoke imperative DOM node animations, to integrate with a third-party library that needs the DOM node (e.g. D3.js).

We’ll use the Search component as an example. When the application renders for the first time, the input field should be focused. This is one case where we need access to the DOM API. The ref attribute can be used in both functional stateless components and ES6 class components. In this example, we need a lifecycle method, so the approach is showcased using the ref attribute with an ES6 class component.

## Higher-Order Components

Higher-order components (HOC) are an advanced concept in React. HOCs are an equivalent to higher-order functions. They take any input, usually a component, but also optional arguments, and return a component as output. The returned component is an enhanced version of the input component, and it can be used in your JSX.

HOCs are used for different use cases. They can prepare properties, manage state, or alter the representation of a component. One case is to use a HOC as a helper for a conditional rendering.

Imagine you have a List component that renders a list of items or nothing, because the list is empty or null. The HOC could shield away that the list would render nothing when there is no list. On the other hand, the plain List component doesn’t need to bother anymore about an non existent list, as it only cares about rendering the list.

Let’s do a simple HOC that takes a component as input and returns a component.

Higher-order components are an advanced pattern in React. They have multiple purposes: improved reusability of components, greater abstraction, composability of components, and manipulations of props, state and view. I encourage you to read gentle introduction to higher-order components (https://www.robinwieruch.de/gentle-introduction-higher-order-components/). It gives you another approach to learn them, shows you an elegant way to use them in a functional programming way, and solves the problem of conditional rendering with higher-order components.

## Advanced Sorting

Since you have a Table component, it makes sense to enhance it with advanced interactions. Next, we’ll introduce a sort functionality for each column by using the column headers of the Table. It is possible to write your own sort function, but I prefer to use a utility library like Lodash for these cases.

Now we have several columns in Table: title, author, comments and points columns. You can define sort functions where each takes a list and returns a list of items sorted by a specific property. Additionally, you will need a default sort function that doesn’t sort, but returns the unsorted list. This will be the initial state.

Two of the sort functions return a reversed list. That’s to see the items with the highest comments and points, rather than the items with the lowest counts when the list is sorted for the first time. The SORTS object allows you to reference any sort function now. Again, the App component is responsible for storing the state of the sort. The initial state will be the default sort function, which doesn’t sort at all and returns the input list as output.

Once we choose a different sortKey, like the AUTHOR key, we sort the list with the appropriate sort function from the SORTS object. Now we define a new class method in App component that sets a sortKey to the local component state, then sortKey can be used to retrieve the sorting function to apply it to the list.

Each Sort component gets a specific sortKey and the general onSort() function. Internally, it calls the method with the sortKey to set the specific key.

As you can see, the Sort component reuses your common Button component. On a button click, each individual passed sortKey is set by the onSort() method, so the list is sorted when column headers are selected.

## State Management in React

### Lifting State

Only the App component is a stateful ES6 component in your application. It handles a lot of
application state and logic in its class methods. Moreover, we pass a lot of properties to the Table component, most of which are only used in there. It’s not important that the App component knows about them, so the sort functionality could be moved into the Table component.

Moving substate from one component to another is known as lifting state. We want to move
state that isn’t used in the App component into the Table component, down from parent to child component. To deal with state and class methods in the Table component, it has to become an ES6 class component. The refactoring from functional stateless component to ES6 class component is straightforward.

Since you want to deal with state and methods in your component, you have to add a constructor and initial state.

Now you can move state and class methods with the sort functionality from your App component down to your Table component.

You can also make the Table component more lightweight. To do this, we move props that are passed to it from the App component, because they are handled internally in the Table component.

We made a crucial refactoring by moving functionality and state closer into another component, and other components got more lightweight. Again, the component API of the Table got lighter because it deals internally with the sort functionality.

Lifting state can go the other way as well: from child to parent component. It is called as lifting state up. Imagine you were dealing with local state in a child component, and you want to fulfil a requirement to show the state in your parent component as well. You would have to lift up the state to your parent component. Moreover, imagine you want to show the state in a sibling component of your child component. Again, you would lift the state up to your parent component. The parent component deals with the local state, but exposes it to both child components.

### Revisited: setState()

So far, we have used React setState() to manage your internal component state. We can pass an object to the function where it updates partially the local state.

But setState() doesn’t take only an object. In its second version, you can pass a function to update the state.

There is one crucial case where it makes sense to use a function over an object: when you
update the state depending on the previous state or props. If you don’t use a function, the local state management can cause bugs. The React setState() method is asynchronous. React batches setState() calls and executes them eventually. Sometimes, the previous state or props changes between before we can rely on it in our setState() call.

```js
const { oneCount } = this.state;
const { anotherCount } = this.props;
this.setState({ count: oneCount + anotherCount });
```

Imagine that oneCount and anotherCount, thus the state or the props, change somewhere else
asynchronously when you call setState(). In a growing application, you have more than one
setState() call across your application. Since setState() executes asynchronously, you could rely in the example on stale values.

With the function approach, the function in setState() is a callback that operates on the state and props at the time of executing the callback function. Even though setState() is asynchronous, with a function it takes the state and props at the time when it is executed.

```js
this.setState((prevState, props) => {
  const { oneCount } = prevState;
  const { anotherCount } = props;
  return { count: oneCount + anotherCount };
});
```

### Taming the State

Previous chapters have shown that state management can be a crucial topic in larger apps, as React and a lot of other SPA frameworks struggle with it. As applications get more complex, the big challenge in web applications is to tame and control the state.

Compared to other solutions, React has already taken a big step forward. A unidirectional data flow and a simple API to manage state in components is indispensable. These concepts make it easier to reason about your state and your state changes. It also makes it easier to reason about it on a component level and on an application level to a certain degree.

It is possible to introduce bugs by operating on stale state when using an object over a function in setState(). We lift state around to share or hide necessary state across components. Sometimes a component needs to lift up state, because its sibling component depends on it. Perhaps the component is far away in the component tree, so the stated needs to be shared across the whole component tree. Components are more involved in state management, as the main responsibility of components is representing the UI.

Because of this, there are standalone solutions to take care of state management. Libraries like Redux or MobX are both feasible solutions in a React application. They come with extensions, react-redux and mobx-react, to integrate them into the React view layer. Redux and MobX are outside of the scope of this book, but I encourage you to study the different ways to handle scaling state management as your React applications become more complex.

https://www.robinwieruch.de/redux-mobx-confusion/

### Where can you go from here?

If you are looking for more extensions for your application, I recommend several learning paths after you’ve mastered the basics:

- Connecting to a Database and/or Authentication: In a growing React application, you may want to persist data eventually. The data should be stored in a database so it can survive after a browser session, and so it can be shared across different users using your application. The simplest way to introduce a database is Firebase. In this tutorial, you will find a step-by-step guide on how to use Firebase authentication in React. Beyond that, you can use Firebase’s realtime database to store user entities.
https://www.robinwieruch.de/complete-firebase-authentication-react-tutorial/

- State Management: You have used React this.setState() and this.state to manage and access local component state. That’s a good start. In a larger application, however, you will experience the limits of React’s local component state. It is imperative you learn to use third-party state management libraries like Redux or MobX.
https://www.robinwieruch.de/learn-react-before-using-redux/

* Tooling with Webpack and Babel: We used create-react-app to set up the application we created for this book. At some point you may want to learn the tooling around it, which enables you to setup your own project without create-react-app. I recommend a minimal setup with Webpack and Babel, after which you can apply additional tooling on your own. For instance, you could use ESLint to follow a unified code style.
https://www.robinwieruch.de/minimal-react-webpack-babel-setup/

- Code Organization: Recall if you will the chapter about code organization. You can apply these changes now, if you haven’t already. It will help organize your components in structured files and folders (modules), and it will help you understand the principles of code splitting, reusability, maintainability, and module API design. Your applications will eventually grow and need to be structured into modules, so it’s better to start now.

- Testing: The book only scratched the surface of testing. You should dive deeper into unit testing and integration testing, especially with React applications. I would recommend to stick to Enzyme and Jest for implementations, to refine your approaches with unit and snapshot tests.

- React Component Syntax: The best practices for implementing React components evolve over time. You will find many ways to write your React components, especially React class components, in other learning resources. A GitHub repository called react-alternative-
class-component-syntax is a great way to learn alternative ways to write React class components. By using class field declarations, you can write them even more concisely in the future.

- UI Components: Many beginners make the mistake of introducing UI component libraries too early in their projects. It is more practical to learn how to implement and use a dropdown, checkbox, or dialog in React with standard HTML elements. Most of these components will manage their own local state. A checkbox has to know whether it is checked or unchecked, so you should implement them as controlled components. After we covered the foundational implementations, introducing a UI component library with checkboxes and dialogs as React components should be easier.

- Routing: You can implement routing for your application with react-router. So far, there is only one page in your application. React Router helps manage multiple pages across multiple URLs. When you introduce routing to your application, you don’t make any requests to your web server to request the next page. The router will do everything for you on the client-side. So get your hands dirty and introduce routing in your application.

- Type Checking: Earlier, we used React PropTypes to define component interfaces. It is a good practice to prevent bugs, but the PropTypes are only checked on runtime. You can go further by introducing static type checking at compile time. TypeScript and Flow are popular type systems for React.

- React Native: React Native brings your application to mobile devices, such as iOS and Android applications. Once you’ve mastered React, the learning curve for React Native shouldn’t be that steep, as they share the same principles. The only difference with mobile are the layout components.

- Other Projects: There are plenty of tutorials out there that use only React to build exciting applications, which provide good practice to apply what you’ve learned in this book before you move on to intermediate projects. Here are a few of my own:

## Shorties

- destruct all used state properties for the render function and delete the `this.state.` in the render
- `this.props.children` is the child node content of the created React Component: `<MyComponent>Hello</MyComponent>` => "Hello" is `this.props.children`
- https://www.robinwieruch.de/react-pass-props-to-component/
