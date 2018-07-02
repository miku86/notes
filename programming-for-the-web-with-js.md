# Programming for the Web with JavaScript

# Week 1: Web Programming Basics

- Internet - network of machines (servers, clients, routers etc.) connected by media (fiber, wifi etc.), that allows communication among devices => HARDWARE
- WWW or Web - an application, that operates over the internet to transfer data => SOFTWARE
- URI - address to uniquely identify a resource
- Content - static (HTML, CSS) vs. dynamic (JS)
- Browser - software used to access web content
  - Rendering Engine (HTML, CSS): static content
  - JavaScript Engine (JS): dynamic content
- HTTP(S) - protocol to transfer data between browser (client) and www (server)
  - Client sends request: Line (Verb, URI, Protocol) + Headers + Blankline + Body
  - Server sends response: Line (Protocol, Status Code) + Headersvv + Blankline + Body

---

# Week 2: Using JavaScript to Create Dynamic, Data-Driven Web Pages

## JS

- event-driven/async: waits for eventsyy
- main types: primitives, array (indexed), object (named)
- primitive args passed by value: a function cannot change them
- object args passed by reference: af function CAN change them
- string methods: `includes()`, `search()`
- `localStorage` to store data in the browser
- `JSON.stringify(obj)` to convert JS object to JSON string
- `JSON.parse(jsonString)` to convert JSON String to JS object

## Regex:

- `.search(/very/i)` ignore upper/lowercase
- `.search(/[012]/)` any 0 or 1 or 2
- `.search(/[a-z]/)` any lowercase character
- `.search(/[0-9]/)` any digit
- `.search(/[0-9][a-z]/)` any combination of digit and lowcase char
- `.search(/[^0-9]/)` any char NOT digit
- `.search(/^[0-9]/)` starts with any digit
- `.search(/[0-9]$/)` ends with any digit
- `.search(/^[a-z][a-z0-9]*[0-9]$/)` starts with a lowercase letter, followed by 0 or more lowercase letters and digits, ends with a digit

---

# Week 3: Client-Side Frameworks for Developing Modular Web Page Components

## React

- recyclable, reusable components with lifecycles: Modularity, Lifecycles, JSX
- Components: the nodes of the VirtualDOM, have an independent state that changes with events
- VirtualDOM: selectively (re-)renders subtrees of nodes based on state changes, efficient because it oddes the least amount of DOM changes to update components
- diff: identify nodes that have changed
- reconciliation: identify nodes that are affected by the change
- re-render only affected nodes

### Component

- Render function
- Properties: attributes and values that are set when the component is created, should never be modified after init
- States: attributes and values that represent the current state of the component, can be modified during component's lifecycles
- Lifecycles: Mounting, Updating, Unmounting

## SaaS

- no installation needed, user's pc doesn't matter
- less likely to lose data
- easier collaboration
- easier upgrading
- microservices put each functionality into separate service and scales by distributing these services across servers, replicatiing as needed
- services interact through REST-API

## Create-React-App

- start with create-react-app
- add every component in a separate file in `src/`

## Testing

- Mocha: testing framework
- Chai: assertion library for Behaviour Driven Testing
- Enzyme: testing React Component state and output

## D3

- D3 = Data Driven Documents
- SVG elements are part of the DOM, so JS can manipulate them
- D3 can manipulate HTML based on data
  => generate HTML tables, SVG charts and graphs etc

---

# Week 4: Building Scalable Web Apps with Server-Side JavaScript

## What does the Web Server do?

- listen for and accept incomming HTTP requests
- parse the HTTP request to determine what is requested
- locate or create the resource being requested
- construct and send back the HTTP response

## Node

- async, event-driven JS runtime for building web apps
- treats HTTP request as events that invoke callbacks that construct the HTTP response

## Express

- web app framework that sits on top of Node server
- helps to modularize and streamline web app
- handles routes
- functions as middleware

- Node and Express represent HTTP requests and responses using JS Objects
- we can use these objects' properties and functions to dynamically generate the content that is sent in reponse to a request
- handles HTTP Request Object (`.method`, `.url`, `.headers()`, `.get()`, `.send()`)
- handles HTTP Response Object (`.status()`, `.type()`, `.write()`, `.end()`)

### Express Middleware

- is a function that is invoked in the handling of a HTTP request
- is used in the middle between receiving a request and sending a response
- multiple middlewares can be chained on the same request
- take three parameters: req, res, next
- standard middleware usage: `app.use(urlroute, middlewarefunction);`
- Routing allows us to specify different functionality for different HTTP requests
- Routing uses middleware functions, each handles a different part of the functionality
- Routers allow us to combine middleware functions into subroutes
  => `const myRoute = express.Router(); myRoute.use(header, greeter, footer);`

- how to get data from user:
  - http request queries: key/value pairs from URL, using "get" method
  - http request param: key/value pairs from parameterized URL
  - http request body: input data from form, using "post" method => body-parser

## EJS

- a view engine that uses data and JS to produce HTML
- allows webpages to be developed statically and rendered dynamically serverside
- templates usually in `/views/`
- `<%= %>` to display as HTML, `<% %>` to run JS

## MongoDB/NoSQL

- a NoSQL database, that is designed for use with JS apps
- stores collections of documents
- we can access MongoDB using Mongoose
- we define a Schema and then create new documents using the save function
