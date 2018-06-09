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

---

# Week 4: Building Scalable Web Apps with Server-Side JavaScript
