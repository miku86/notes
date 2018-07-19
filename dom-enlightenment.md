# DOM Enlightenment

# Introduction

This book is not an exhaustive reference on DOM scripting or JS. It may be the most exhaustive book written about DOM scripting without the use of a library/framework. The lack of authorship around this topic is not without good reason. Most technical authors are not willing to wrangle this topic because of the differences that exist among legacy browsers and their implementations of the DOM specifications (or lack thereof).

For the purpose of this book, I'm going to sidestep the browser API mess and dying browser discrepancies in an effort to expose the modern DOM. That's right, I'm going to sidestep the ugliness in an effort to focus on the here and now. After all, we have solutions like jQuery to deal with all that browser ugliness, and you should definitely be leveraging something like jQuery when dealing with deprecated browsers.

While I am not promoting the idea of only going native when it comes to DOM scripting, I did write this book in part so that developers may realize that DOM libraries are not always required when scripting the DOM. I also wrote for the lucky few who get to write JS code for a single environment (i.e. one browser, mobile browsers, or HTML+CSS+JS-to-native via something like PhoneGap). What you learn in this book may just make a DOM library unnecessary in ideal situations, say for example, some light DOM scripting for deployment on a Webkit mobile browser only.

## Who should read this book

I specifically had two types of developers in mind. I assume both types already have an intermediate to advanced knowledge of JS, HTML, and CSS. The first developer is someone who has a good handle on JS or jQuery, but has really never taken the time to understand the purpose and value of a library like jQuery (the reason for its rhyme, if you will). Equipped with the knowledge from this book, that developer should fully be able to understand the value provided by jQuery for scripting the DOM. And not just the value, but how jQuery abstracts the DOM and where and why jQuery is filling the gaps. The second type of developer is an engineer who is tasked with scripting HTML documents that will only run in modern browsers or that will get ported to native code for multiple OS's and device distributions (e.g. PhoneGap) and needs to avoid the overhead (i.e. size or size v.s. use) of a library.

# Preface

## This book is not like other programming books

The book is written in a style that favors small, isolated, immediately executable code over wordy explanations and monolithic programs. One of my favorite authors, C.S Lewis, asserts that words are the lowest form of communication that humans traffic in. I totally agree with this assertion and use it as the basis for the style of these books.

I feel that technical information is best covered with as few words as possible, in conjunction with just the right amount of executable code and commenting required to express an idea. The style of this book attempts to present a clearly defined idea with as few words as possible, backed with real code.

Because of this, you should execute and examine the code, thereby forming the foundation of a mental model for the words used to describe the concepts. Additionally, the format of these books attempts to systematically break ideas down into their smallest possible form and examine each one in an isolated context. All this to say that this is not a book with lengthy explanations or in-depth coverage on broad topics.

---

# Chapter 1 - Node Overview

## 1.1 The Document Object Model (aka DOM) is a hierarchy/tree of JS node objects

When you write an HTML document you encapsulate HTML content inside of other HTML content. By doing this you setup a hierarchy that can be expressed as a tree. Often this hierarchy or encapsulation system is indicated visually by indenting markup in an HTML document. The browser when loading the HTML document interrupts and parses this hierarchy to create a tree of node objects that simulates how the markup is encapsulated.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<title>HTML</title>
</head>
<body>
<!-- Add your content here-->
</body>
</html>
```

The above HTML code when parsed by a browser creates a document that contains nodes structrured in a tree format (i.e. DOM).

For example, the `body` element is an element node and an instance of the `HTMLBodyElement` interface.

What you should take away here is that html documents get parsed by a browser and converted into a tree structure of node objects representing a live document. The purpose of the DOM is to provide a programatic interface for scripting (removing, adding, replacing, eventing, modifiying) this live document using JS.

## 1.2 Node object types

The most common types of nodes one encounters when working with HTML documents are:

- DOCUMENT_NODE (e.g. window.document)
- ELEMENT_NODE (e.g. `<body>, <a>, <p>, <script>, <style>, <html>, <h1>` etc...)
- ATTRIBUTE_NODE (e.g. `class="funEdges"`)
- TEXT_NODE (e.g. text characters in an html document including carriage returns and white space)
- DOCUMENT_FRAGMENT_NODE (e.g. `document.createDocumentFragment()`)
- DOCUMENT_TYPE_NODE (e.g. `<!DOCTYPE html>`)

I've listed the node types above formatted exactly as the constant property is written in the JS browser environment as a property of the `Node` object. These `Node` properties are constant values and are used to store numeric code values which map to a specific type of node object. For example, `Node.ELEMENT_NODE` is equal to 1. And 1 is the code value used to identify element nodes.

What I hope you take away is that the `nodeType` value (i.e. 1) is just a numeric classificaiton used to describe a certain type of node constructed from a certain JS interface/constructor. For example, the `HTMLBodyElement` interface represents a node object that has a node type of 1, which is a classification for `ELEMENT_NODE`'s.

## 1.3 Sub-node objects inherit from the Node object

Each node object in a typical DOM tree inherits properties and methods from `Node`. Depending upon the type of node in the document there are also additional sub node object/interfaces that extend the `Node` object. Below I detail the inheritance model implemented by browsers for the most common node interfaces (< indicates inherited from).

- Object < Node < Element < HTMLElement < (e.g. HTML\*Element)
- Object < Node < Attr (deprecated in DOM 4)
- Object < Node < CharacterData < Text
- Object < Node < Document < HTMLDocument
- Object < Node < DocumentFragment

It's important not only to remember that all nodes types inherit from `Node` but that the chain of inheritance can be long. For example, all `HTMLAnchorElement` nodes inherit properties and methods from `HTMLElement, Element, Node, and Object` objects.

`Node` is just a JS constructor function. And so logically `Node` inherits from `Object.prototype` just like all objects in JS.

You will see a long list of properties that are available to the element node object. The properties & methods inherited from the `Node` object are in this list as well as a great deal of other inherited properties and methods from the `Element, HTMLElement, HTMLAnchorElement, Node, and Object` object.

It's not my point to examine all of these properties and methods now but simply to point out that all nodes inherit a set of baseline properties and methods from its constructor as well as properties from the prototype chain.

## 1.4 Properties and methods for working nodes

Like we have been discussing all node objects (e.g `Element, Attr, Text` etc...) inherit properties and methods from a primary `Node` object. These properties and methods are the baseline values and functions for manipulating, inspecting, and traversing the DOM.

In addtion to the properties and methods provided by the node interface there are a great deal of other relevant properties and methods that are provided by sub node interfaces such as the `document, HTMLElement, or HTML*Element` interface.

Below I list out the most common `Node` properties and methods inherited by all node objects including the relevant inherited properties for working with nodes from sub-node interfaces.

Node Properties:

- `childNodes`
- `firstChild`
- `lastChild`
- `nextSibling`
- `nodeName`
- `nodeType`
- `nodeValue`
- `parentNode`
- `previousSibling`

Node Methods:

- `appendChild()`
- `cloneNode()`
- `compareDocumentPosition()`
- `contains()`
- `hasChildNodes()`
- `insertBefore()`
- `isEqualNode()`
- `removeChild()`
- `replaceChild()`

Document Methods:

- `document.createElement()`
- `document.createTextNode()`

HTML \* Element Properties:

- `innerHTML`
- `outerHTML`
- `textContent`
- `innerText`
- `outerText`
- `firstElementChild`
- `lastElementChild`
- `nextElementChild`
- `previousElementChild`
- `children`

HTML element Methods:

- `insertAdjacentHTML()`

## 1.5 Identifying the type and name of a node

Every node has a `nodeType` and `nodeName` property that is inherited from `Node`. For example Text nodes have a `nodeType` code of 3 and `nodeName` value of '#text'. As previously mentioned the numeric value 3 is a numeric code representing the type of underlying object the node represents (i.e. Node.TEXT_NODE === 3).

It makes sense to simply memorize these numeric code's for the more common nodes given that we are only dealing with 5 numeric codes.

## 1.6 Getting a nodes value

The `nodeValue` property returns null for most of the node types (except Text and Comment). It's use is centered around extracting actual text strings from Text and Comment nodes.

## 1.7 Creating element and text nodes using JS methods

When a browser parses an HTML document it constructs the nodes and tree based on the contents of the HTML file. The browser deals with the creation of nodes for the intial loading of the HTML document. However it's possible to create your own nodes using JS. The following two methods allow us to programatically create Element and Text nodes using JS:

- `createElement()`
- `createTextNode()`

```js
var elementNode = document.createElement('div');
console.log(elementNode, elementNode.nodeType); //log <div> 1, and 1 indicates an element node

var textNode = document.createTextNode('Hi');
console.log(textNode, textNode.nodeType); //logs Text {} 3, and 3 indicates a text node
```

## 1.8 Creating and adding element and text nodes to the DOM using JS strings

The `innerHTML, outerHTML, textContent and insertAdjacentHTML()` properties and methods provide the functionality to create and add nodes to the DOM using JS strings.

```js
//create a strong element and text node and add it to the DOM
document.getElementById('A').innerHTML = '<strong>Hi</strong>';

//create a div element and text node
document.getElementById('B').outerHTML = '<div id="B">Whats Shaking</div>';

//create a text node and update the #C with the text node
document.getElementById('C').textContent = 'dude';
```

The `insertAdjacentHTML()` method, which only works on Element nodes, is a good deal more precise than the previously mentioned methods. Using this method it's possible to insert nodes before the beginning tag, after the beginning tag, before the end tag, and after the end tag.

## 1.9 Extracting parts of the DOM tree as JS strings

The same exact properties (`innerHTML, outerHTML, textContent`) that we use to create and add nodes to the DOM can also be used to extract parts of the DOM (or really the entire DOM) as a JS string. In the code example below I use these properties to return a string value containing text and html values from the HTML document.

```js
console.log(document.getElementById('A').innerHTML); //logs '<i>Hi</i>'
console.log(document.getElementById('A').outerHTML); //logs <div id="A">Hi</div>
// all text is returned even if it's in child element nodes (i.e. <strong> !</strong>)
console.log(document.getElementById('B').textContent); //logs 'Dude !'
```

## 1.10 Adding node objects to the DOM using appendChild()& insertBefore()

The `appendChild()` and `insertBefore()` Node methods allow us to insert JS node objects into the DOM tree.

The `appendChild()` method will append a node(s) to the end of the child node(s) of the node the method is called on. If there are no child node(s) then the node being appended is appended as the first child.

In the code below we are creating a element node (`<strong>`) and text node (Dude). Then the `<p>` is selected from the DOM and our `<strong>` element is appended using `appendChild()`. Notice that the `<strong>` element is encapsulated inside of the `<p>` element and added as the last child node. Next the `<strong>` element is selected and the text 'Dude' is appended to the `<strong>` element.

```js
//create a blink element node and text node
var elementNode = document.createElement('strong');
var textNode = document.createTextNode(' Dude');

//append these nodes to the DOM
document.querySelector('p').appendChild(elementNode);
document.querySelector('strong').appendChild(textNode);
```

When it becomes necessary to control the location of insertion beyond appending nodes to the end of a child list of nodes we can use `insertBefore()`.

```js
//create a text node and li element node and append the text to the li
var text1 = document.createTextNode('1');
var li = document.createElement('li');
li.appendChild(text1);

//select the ul in the document
var ul = document.querySelector('ul');

// add the new li element to the DOM using ul.firstChild
ul.insertBefore(li, ul.firstChild);
```

## 1.11 Removing and replacing nodes using removeChild() and replaceChild()

Removing a node from the DOM is a bit of a multi-step process. First you have to select the node you want to remove. Then you need to gain access to its parent element typically using the `parentNode` property. It's on the parent node that you invoke the `removeChild()` method passing it the reference to the node to be removed.

```js
//remove element node
var divA = document.getElementById('A');
divA.parentNode.removeChild(divA);
```

```js
//replace element node
var divA = document.getElementById('A');
var newSpan = document.createElement('span');
newSpan.textContent = 'Howdy';
divA.parentNode.replaceChild(newSpan, divA);
```

## 1.12 Cloning nodes using cloneNode()

Using the `cloneNode()` method it's possible to duplicate a single node or a node and all its children nodes.

`var cloneUL = document.querySelector('ul').cloneNode();`

To clone a node and all of its children nodes you pass the `cloneNode()` method a parameter of of true.

`var cloneUL = document.querySelector('ul').cloneNode(true);`

## 1.13 Grokking node collections (i.e. Nodelist & HTMLcollection)

When selecting groups of nodes from a tree or accessing pre-defined sets of nodes, the nodes are either placed in a `NodeList` (e.g. `document.querySelectorAll('*')`) or `HTMLCollection` (e.g. document.scripts). These array like (i.e. not a real Array) object collections that have the following characteristics:

- A collection can either be live or static. Meaning that the nodes contained in the collection are either literally part of the live document or a snapshot of the live document.
- By default nodes are sorted inside of the collection by tree order. Meaning the order matches the liner path from tree trunk to branches.
- The collections have a length property that reflects the number of elements in the list

## 1.14 Gettting a list/collection of all immediate child nodes

Using the `childNodes` property produces an array like list (i.e. `NodeList`) of the immediate child nodes. Below I select the `<ul>` element which I then use to create a list of all of the immediate child nodes contained inside of the `<ul>`.

`var ulElementChildNodes = document.querySelector('ul').childNodes;`

## 1.15 Convert a NodeList or HTMLCollection to JS Array

Node lists and html collections are array like but not a true JS array which inherits array methods. We programtically confirm this using `isArray()`.

`console.log(Array.isArray(document.links));`

Converting a node list and html collection list to a true JS array can provide a good deal of advantages.

First it gives us the ability to create a snapshot of the list that is not tied to the live DOM considering that `NodeList` and `HTMLCollection` are live lists.

Secondly, converting a list to a JS array gives access to the methods provided by the Array object (e.g. `forEach, pop, map, reduce` etc...).

In ES6 we have `Array.from` to look forward to which converts a single argument that is an array-like object or list (eg. arguments, NodeList, DOMTokenList, NamedNodeMap) into a `new Array()` and returns it.

## 1.16 Traversing nodes in the DOM

From a node reference (i.e. `document.querySelector('ul')`) it's possible to get a different node reference by traversing the DOM using the following properties:

- `parentNode`
- `firstChild`
- `lastChild`
- `nextSibling`
- `previousSibling`

If you have been around the DOM much then it should be no surprise that traversing the DOM includes not just traversing element nodes but also text and comment nodes, and this is not exactly ideal. Using the following properties we can traverse the DOM ignoring text and comment nodes:

- `firstElementChild`
- `lastElementChild`
- `nextElementChild`
- `previousElementChild`
- `children`

## 1.17 Verify a node position in the DOM tree with contains() & compareDocumentPosition()

It's possible to know if a node is contained inside of another node by using the `contains()` Node method.

```js
// is <body> inside <html lang="en"> ?
var inside = document
  .querySelector('html')
  .contains(document.querySelector('body'));
```

If you need more robust information about the position of a node in the DOM tree in regards to the nodes around it you can use the `compareDocumentPosition()` Node method. Basically this method gives you the ability to request information about a selected node relative to the node passed in. The information that you get back is a number.

## 1.18 How to determine if two nodes are identical

Two nodes are equal if and only if the following conditions are satisfied:

- The two nodes are of the same type.
- The following string attributes are equal: `nodeName, localName, namespaceURI, prefix, nodeValue`. That is: they are both null, or they have the same length and are character for character identical.
- The `attributes NamedNodeMaps` are equal. That is: they are both null, or they have the same length and for each node that exists in one map there is a node that exists in the other map and is equal, although not necessarily at the same index.
- The `childNodes NodeLists` are equal. That is: they are both null, or they have the same length and contain equal nodes at the same index. Note that normalization can affect equality; to avoid this, nodes should be normalized before being compared.

Calling the `isEqualNode()` method on a node in the DOM will ask if that node is equal to the node that you pass it as a parameter.

---

# Chapter 2 - Document Nodes

## 2.1 document node overview

The `HTMLDocument` constructor (which inherits from `document`) when instantiated represents specifically a DOCUMENT_NODE (i.e. `window.document`) in the DOM. To verify this we can simply ask which constructor was used in the creation of the `document` node object.

```js
console.log(window.document.constructor); //logs function HTMLDocument()
console.log(window.document.nodeType); //logs 9, which is mapping to DOCUMENT_NODE
```

The code above concludes that the `HTMLDocument` constructor function constructs the `window.document` node object and that this node is a `DOCUMENT_NODE` object.

## 2.2 HTMLDocument properties and methods (including inherited)

To get accurate information pertaining to the available properties and methods on an `HTMLDocument` node it's best to ignore the specification and to ask the browser what is available.

The available properties are many even if the inherited properties were not considered. Below I've hand pick a list of noteworthy properties and methods for the context of this chapter:

- `doctype`
- `documentElement`
- `implementation.*`
- `activeElement`
- `body`
- `head`
- `title`
- `lastModified`
- `referrer`
- `URL`
- `defaultview`
- `compatMode`
- `ownerDocument`
- `hasFocus`

## 2.3 Getting general HTML document information (title, url, referrer, lastModified, compatMode)

The `document` object provides access to some general information about the HTML document/DOM being loaded with `document.title, document.URL, document.referrer, document.lastModified, and document.compatMode` properties to gain some general information about the document. Based on the property name the returned values should be obvious.

## 2.4 document child nodes

`Document` nodes can contain one `DocumentType` node object and one `Element` node object. This should not be a surprise since HTML documents typically contain only one doctype (e.g. `<!DOCTYPE html>`) and one element (e.g. `<html lang="en">`). Thus if you ask for the children (e.g. `document.childNodes`) of the Document object you will get an array containing at the very least the documents `doctype/DTD` and `<html lang="en">` element.

## 2.5 document provides shortcuts to <!DOCTYPE>, <html lang="en">, <head>, and <body>

Using the properties listed below we can get a shortcut reference to the following nodes:

- `document.doctype` refers to `<!DOCTYPE>`
- `document.documentElement` refers to `<html lang="en">`
- `document.head` refers to `<head>`
- `document.body` refers to `<body>`

## 2.6 Detecting DOM specifications/features using document.implementation.hasFeature()

It's possible using `document.implementation.hasFeature()` to ask (boolean) the current document what feature and level the browser has implemented/supports. For example we can ask if the browser has implemented the core DOM level 3 specification by passing the name of the feature and the version to the hasFeature() method.

```js
// ask if the browser has implemented the Core 2.0 specification
console.log(document.implementation.hasFeature('Core', '2.0'));
```

## 2.7 Get a reference to the focus/active node in the document

Using the `document.activeElement` we can quickly get a reference to the node in the document that is focused/active.

## 2.8 Determing if the document or any node inside of the document has focus

Using the `document.hasFocus()` method it's possible to know if the user currently is focused on the window that has the HTML document loaded.

## 2.9 document.defaultview is a shortcut to the head/global object

You should be aware that the `defaultView` property is a shortcut to the JS head object or what some refer to as the global object. The head object in a web browser is the `window` object and `defaultView` will point to this object in a JS browser enviroment.

## 2.9 Getting a reference to the Document from an element using ownerDocument

The `ownerDocument` property when called on a node returns a reference to the `Document` the node is contained within.

---

# Chapter 3 - Element Nodes

## 3.1 HTML\*Element object overview

Elements in an html document all have a unique nature and as such they all have a unique JS constructor that instantiates the element as a node object in a DOM tree. For example, an `<a>` element is created as a DOM node from the `HTMLAnchorElement()` constructor.

Each element in the DOM is constructed from a unique JS intefaces/constructor. Each `HTML*Element` inherits properties and methods from `HTMLElement, Element, Node, and Object`.

## 3.2 HTML\*Element object properties and methods (including inherited)

To get accurate information pertaining to the available properties and methods on an `HTML*Element` node it's best to ignore the specification and to ask the browser what is available.

The available properties are many even if the inherited properties were not considered. Below I've hand pick a list of note worthy properties and methods (inherited as well) for the context of this chapter:

- `createElement()`
- `tagName`
- `children`
- `getAttribute()`
- `setAttribute()`
- `hasAttribute()`
- `removeAttribute()`
- `classList()`
- `dataset`
- `attributes`

## 3.3 Creating Elements

`Element` nodes are instantiated for us when a browser interputs an HTML document and a corresponding DOM is built based on the contents of the document. After this fact, it's also possible to programaticlly create `Element` nodes using `createElement()`.

```js
// create a <textarea> element node and then inject that node into the live DOM tree
var elementNode = document.createElement('textarea');
document.body.appendChild(elementNode);
```

The value passed to the `createElement()` method is a string that specifices the type of element (aka `tagName`) to be created.

## 3.4 Get the tag name of an element

Using the `tagName` property we can access the name of an element. The `tagName` property returns the same value that using `nodeName` would return.

## 3.5 Getting a list/collection of element attributes and values

Using the `attributes` property (inherited by element nodes from `Node`) we can get a collection of the `Attr` nodes that an element currently has defined. The list returned is a `NameNodeMap`.

## 3.6 Getting, Setting, & Removing an element's attribute value

The most consistent way to get, set, or remove an elements attribute value is to use the `getAttribute(), setAttribute(), and removeAttribute()` method.

## 3.7 Verifying an element has a specific attribute

The best way to determine if an element has an attribute is to use the `hasAttribute()` method.

`console.log(document.querySelector('a').hasAttribute('href'));`

## 3.8 Getting a list of class attribute values

Using the `classList` property available on element nodes we can access a list (i.e. `DOMTokenList`) of class attribute values that is much easier to work with than a space-delimited string value returned from the `className` property. The `classList` is an array like collection.

```js
console.log(elm.classList); // big brown {0="big", 1="brown", length=2, ...}
console.log(elm.className); // logs 'big brown'
```

## 3.9 Adding & removing sub-values to a class attribute

Using the `classList.add()` and `classList.remove()` methods it's extremely simple to edit the value of a class attribute.

```js
elm.classList.add('cat');
elm.classList.remove('dog');
```

## 3.10 Toggling a class attribute value

Using the `classList.toggle()` method we can toggle a sub-value of the class attribute. This allows us to add a value if it's missing or remove a value if it's already added.

## 3.11 Determining if a class attribute value contains a specific value

Using the `classList.contains()` method it's possible to determine if a class attribute value contains a specific sub-value.

`console.log(elm.classList.contains('brown')); // logs true`

## 3.12 Getting & Setting data-\* attributes

The `dataset` property of a element node provides an object containing all of the attributes of an element that starts with data-\*. Because it's a simply a JS object we can manipulate `dataset` and have the element in the DOM reflect those changes

`dataset` contains camel case versions of data attributes. Meaning `data-foo-foo` will be listed as the property `fooFoo` in the dataset `DOMStringMap` object. The `-` is replaced by camel casing.

---

# Chapter 4 - Element Node Selecting

## 4.1 Selecting a specific element node

The most common methods for getting a reference to a single element node are:

- `querySelector()`
- `getElementById()`

The `getElementById()` method is pretty simple compared to the more robust `querySelector()` method. The `querySelector()` method permits a parameter in the form of a CSS selector syntax. Basically you can pass this method a CSS 3 selector (e.g. `'#score>tbody>tr>td:nth-of-type(2)'`) which it will use to select a single element in the DOM. `querySelector()` will return the first node element found in the document based on the selector.

## 4.2 Selecting/creating a list (aka NodeList) of element nodes

The most common methods for selecting/creating a list of nodes in an HTML document are:

- `querySelectorAll()`
- `getElementsByTagName()`
- `getElementsByClassName()`

The methods create a list (aka `NodeLists`) of elements that you can select from.

`getElementsByTagName() and getElementsByClassName()` are considered live and will always reflect the state of the document even if the document is updated after the list is created/selected.

`querySelectorAll()` does not return a live list of elements.The list created from `querySelectorAll()` is a snap shot of the document at the time it was created and is not reflective of the document as it changes. The list is static, not live.

## 4.3 Selecting all immediate child element nodes

Using the `children` property from an element node we can get a list (aka `HTMLCollection`) of all the immediate children nodes that are element nodes. Notice that using `children` only gives us the immediate element nodes excluding any nodes (e.g. text nodes) that are not elements.

```js
// create a selection/list of all of the <li>'s contained wiithin the <ul>
document.querySelector('ul').children;
```

## 4.4 Contextual element selecting

The methods `querySelector(), querySelectorAll(), getElementsByTagName(), and getElementsByClassName()` typically accessed from the `document` object are also defined on element nodes. This allows for these methods to limit its results to specific vein(s) of the DOM tree. Or said another, you can select a specific context in which you would like the methods to search for element nodes by invoking these methods on element node objects.

```js
//select a div as the context to run the selecting methods
document.querySelector('div').querySelectorAll('li');
```

## 4.5 Pre-configured selections/lists of element nodes

You should be aware that there are some legacy, pre-configured arrays-like-lists, containing element nodes from an HTML document.

- `document.all` - all elements in HTML document
- `document.forms` - all `<form>` elements in HTML document
- `document.images` - all `<img>` elements in HTML document
- `document.links` - all `<a>` elements in HTML document
- `document.scripts` - all `<script>` elements in HTML document
- `document.styleSheets` - all `<link> or <style>` objects in HTML document

## 4.6 Verify an element will be selected using matches()

Using the `matches()` method we can determine if an element will match a selector string.

`document.querySelector('li').matches('li:first-child'); // true`

---

# Chapter 5 - Element Node Geometry & Scrolling Geometry

## 5.1 Element node size, offsets, and scrolling overview

DOM nodes are parsed and painted into visual shapes when viewing html documents in a web browser. Nodes, mostly element nodes, have a corresponding visual representation made viewable/visual by browsers. To inspect and in some cases manipulate the visual representation and gemometry of nodes programatically a set of API's exists and are specified in the CSSOM View Module. A subset of methods and properties found in this specification provide an API to determine the geometry (i.e. size & position using offset) of element nodes as well as hooks for manipulating scrollable nodes and getting values of scrolled nodes.

Most of the properties from the CSSOM View Module specification are read only and calculated each time they are accessed. In other words, the values are live.

## 5.2 Getting an elements offsetTop and offsetLeft values relative to the offsetParent

Using the properties `offsetTop` and `offsetLeft` we can get the offset pixel value of an element node from the `offsetParent`. These element node properties give us the distance in pixels from an elements outside top and left border to the inside top and left border of the `offsetParent`. The value of the offsetParent is determined by searching the nearest ancestor elements for an element that has a CSS position value not equal to static. If none are found then the `<body>` element or what some refer to as the "document" (as opposed to the browser viewport) is the offsetParent value.

## 5.3 Getting an elements top, right, bottom and left border edge offset relative to the viewport using getBoundingClientRect()

Using the `getBoundingClientRect()` method we can get the position of an elements outside border edges as it's painted in the browser viewport relative to the top and left edge of the viewport. This means the left and right edge are measured from the outside border edge of an element to the left edge of the viewport. And the top and bottom edges are measured from the outside border edge of an element to the top edge of the viewport.

## 5.4 Getting an elements size (border + padding + content) in the viewport

The `getBoundingClientRect()` returns an object with a top, right, bottom, and left property/value but also with a height and width property/value. The height and width properties indicate the size of the element where the total size is derived by adding the content of the div, its padding, and borders together.

## 5.5 Getting an elements size (padding + content) in the viewport excluding borders

The `clientWidth` and `clientHeight` properties return a total size of an element by adding together the content of the element and its padding excluding the border sizes.

## 5.6 Getting topmost element in viewport at a specific point using elementFromPoint()

Using `elementFromPoint()` it's possible to get a reference to the topmost element in an html document at a specific point in the document.

## 5.7 Getting the size of the element being scrolled using scrollHeight and scrollWidth

The `scrollHeight` and `scrollWidth` properties simply give you the height and width of the node being scrolled.

## 5.8 Getting & Setting pixels scrolled from the top and left using scrollTop and scrollLeft

The `scrollTop` and `scrollLeft` properties are read-write properties that return the pixels to the left or top that are not currently viewable in the scrollable viewport due to scrolling.

## 5.9 Scrolling an element into view using scrollIntoView()

By selecting a node contained inside a node that is scrollable we can tell the selected node to scroll into view using the `scrollIntoView()` method.

---

# Chapter 6 - Element Node Inline Styles

## 6.1 Style Attribute (aka element inline CSS properties) Overview

Every HTML element has a style attribute that can be used to inline CSS properties specific to the element.

`document.querySelector('div').style;`

That what is returned from the style property is a `CSSStyleDeclaration` object and not a string. Additionally note that only the elements inline styles (i.e. excluding the computed styles, computed styles being any styles that have cascaded from style sheets) are included in the `CSSStyleDeclartion` object.

## 6.2 Getting, setting, & removing individual inline CSS properties

Inline CSS styles are individually represented as a property (i.e. object property) of the style object available on element node objects. This provides the interface for us to get, set, or remove individual CSS properties on an element by simply setting an objects property value.

```js
// get
document.querySelector('div').style.backgroundColor;
// set
document.querySelector('div').style.backgroundColor = 'red';
// remove
document.querySelector('div').style.backgroundColor = '';
```

The style object is a `CSSStyleDeclaration` object and it provides not only access to inidividual CSS properties, but also the `setPropertyValue(propertyName), getPropertyValue(propertyName,value), and removeProperty()` methods used to manipulate individual CSS properties on a element node.

```js
// get
document.querySelector('div').style.getPropertyValue('background-color'));
// set
document.querySelector('div').style.setProperty('background-color','red');
// remove
document.querySelector('div').style.removeProperty('background-color'));
```

## 6.3 Getting, setting, & removing all inline CSS properties

It's possible using the `cssText` property as well as the `getAttribute() and setAttribute()` method to get, set, and remove the entire (i.e. all inline CSS properties) value of the style attribute using a JS string.

## 6.4 Getting an elements computed styles (i.e. actual styles including any from the cascade) using getComputedStyle()

The `style` property only contains the css that is defined via the style attribute. To get an elements css from the cascade (i.e. cascading from inline style sheets, external style sheets, browser style sheets) as well as its inline styles you can use `getComputedStyle()`. This method provides a read-only `CSSStyleDeclaration` object similar to `style`. Make sure you note that `getComputedStyle()` method honors the CSS specificity hierarchy.

## 6.5 Apply & remove css properties on an element using class & id attributes

Style rules defined in a inline style sheet or external style sheet can be added or removed from an element using the `class` and `id` attribute. This is a the most common pattern for manipulating element styles.

---

# Chapter 7 - Text Nodes

## 7.1 Text object overview

Text in an HTML document is represented by instances of the `Text()` constructor function, which produces text nodes. When an HTML document is parsed the text mixed in among the elements of an HTML page are converted to text nodes.

## 7.2 Text object & properties

To get accurate information pertaining to the available properties and methods on an Text node, it's best to ignore the specification and to ask the browser what is available.

The available properties are many even if the inherited properties were not considered. Below I've hand pick a list of note worthy properties and methods for the context of this chapter:

- `textContent`
- `splitText()`
- `appendData()`
- `deleteData()`
- `insertData()`
- `replaceData()`
- `subStringData()`
- `normalize()`
- `data`
- `document.createTextNode()` (not a property or inherited property of text nodes)

## 7.3 White space creates Text nodes

When a DOM is contstructed either by the browser or by programmatic means text nodes are created from white space as well as from text characters. After all, whitespace is a character. A paragraph containing an empty space has a child Text node.

Don't forget that white space and text characters in the DOM are typically represented by a text node. This of course means that carriage returns are considered text nodes.

The reality is if you can input the character or whitespace into an html document using a keyboard then it can potentially be interputed as a text node. If you think about it, unless you minimze/compress the html document the average html page contains a great deal of whitespace and carriage return text nodes.

## 7.4 Creating & Injecting Text Nodes

Text nodes are created automatically for us when a browser interputs an HTML document and a corresponding DOM is built based on the contents of the document. After this fact, it's also possible to programatically create Text nodes using `createTextNode()`.

```js
var textNode = document.createTextNode('Hi');
document.querySelector('div').appendChild(textNode);
```

Keep in mind that we can also inject text nodes into programmatically created DOM structures as well.

```js
var elementNode = document.createElement('p');
var textNode = document.createTextNode('Hi');
elementNode.appendChild(textNode);
document.querySelector('div').appendChild(elementNode);
```

## 7.5 Getting a Text node value with .data or nodeValue

The text value/data represented by a `Text` node can be extracted from the node by using the `data` or `nodeValue` property. Both of these return the text contained in a Text node.

## 7.6 Maniputlating Text nodes with appendData(), deleteData(), insertData(), replaceData(), subStringData()

The `CharacterData` object that Text nodes inherits methods from provides the following methods for manipulating and extracting sub values from Text node values:

- `appendData()`
- `deleteData()`
- `insertData()`
- `replaceData()`
- `subStringData()`

## 7.7 When mulitple sibling Text nodes occur

Typically, immediate sibling Text nodes do not occur because DOM trees created by browsers intelligently combines text nodes, however two cases exist that make sibling text nodes possible.

The first case is rather obvious. If a text node contains an Element node (e.g. `<p>Hi, <strong>cody</strong> welcome!</p>`) than the text will be split into the proper node groupings. The contents of the `<p>` element is not a single Text node, it is in fact 3 nodes, a Text node, Element node, and another Text node.

## 7.8 Remove markup and return all child Text nodes using textContent

The `textContent` property can be used to get all child text nodes, as well as to set the contents of a node to a specific Text node.

When it's used on a node to get the textual content of the node it will returned a concatenataed string of all text nodes contained with the node you call the method on. This functionality would make it very easy to extract all text nodes from an HTML document.

Notice that `textContent` gathers not just immediate child text nodes but all child text nodes no matter the depth of encapsulation inside of the node the method is called.

When `textContent` is used to set the text contained within a node it will remove all child nodes first, replacing them with a single Text node.

## 7.9 The difference between textContent & innerText

Most of the modern browser support a seemingly similiar property to `textContent` named `innerText`. However these properties are not the same. You should be aware of the following differences between `textContent & innerText`:

- `innerText` is aware of CSS. So if you have hidden text `innerText` ignores this text, `textContent` will not
- Because `innerText` cares about CSS it will trigger a reflow, whereas `textContent` will not
- `innerText` ignores the Text nodes contained in `<script>` and `<style>` elements
- `innerText`, unlike `textContent` will normalize the text that is returned. Just think of `textContent` as returning exactly what is in the document with the markup removed. This will include white space, line breaks, and carriage returns
- `innerText` is considered to be non-standard and browser specific while `textContent` is implemented from the DOM specifications

## 7.10 Combine sibling Text nodes into one text node using normalize()

Sibling Text nodes are typically only encountered when text is programaticly added to the DOM. To eliminate sibling Text nodes that contain no `Element` nodes we can use `normalize()`. This will concatenate sibling text nodes in the DOM into a single `Text` node.

## 7.11 Splitting a text node using splitText()

When `splitText()` is called on a `Text` node it will alter the text node it's being called on (leaving the text up to the offset) and return a new Text node that contains the text split off from the orginal text based on the offset.

---

# Chapter 8 - DocumentFragment Nodes

## 8.1 DocumentFragment object overview

The creation and use of a `DocumentFragment` node provides a light weight document DOM that is external to the live DOM tree. Think of a `DocumentFragment` as an empty document template that acts just like the live DOM tree, but only lives in memory, and its child nodes can easily be manipulated in memory and then appended to the live DOM.

## 8.2 Creating DocumentFragment's using createDocumentFragment()

Using a `documentFragment` to create node structures in memory is extrememly efficent when it comes time to inject the `documentFragment` into live node structures.

You might wonder what is the advantage to using a `documentFragment` over simply creating (via `createElement()`) a `<div>` in memory and working within this `<div>` to create a DOM structure. The follow are the differences:

- A document fragment may contain any kind of node (except `<body>` or `<html>`) where as an element may not
- The document fragment itself is not added to the DOM when you append a fragment. The contents of the node are. As opposed to appending an element node in which the element itself is part of the appending.
- When a document fragment is appended to the DOM it transfers from the document fragment to the place it's appended. It's no longer in memory in the place you created it. This is not true for element nodes that are temperately used to contained nodes briefly and then are moved to the live DOM.

## 8.3 Adding a DocumentFragment to the live DOM

By passing the `appendChild()` and `insertBefore()` node methods a `documentFragment` argument the child nodes of the `documentFragment` are transported as children nodes to the DOM node the methods are called on.

## 8.4 Using innerHTML on a documentFragment

Creating a DOM structure in memory using node methods can be verbose and laboring. One way around this would be to created a `documentFragment`, append a `<div>` to this fragment because `innerHTML` does not work on document fragments, and then use the `innerHTML` property to update the fragment with a string of HTML. By doing this a DOM structure is crafted from the HTML string.

When it comes time to append a DOM structure created using a `documentFragment` and `<div>` you'll want to append the structure skipping the injection of the `<div>`.

## 8.5 Leaving a fragments containing nodes in memory by cloning

When appending a `documentFragment` the nodes contained in the Fragment are moved from the Fragment to the structure you are appending too. To leave the contents of a fragment in memory, so the nodes remain after appending, simply clone using `cloneNode()` the `documentFragment` when appending.

---

# Chapter 9 - CSS Style Sheets & CSS rules

## 9.1 CSS Style sheet overview

A style sheet is added to an HTML document by either using the `HTMLLinkElement` node (i.e. `<link href="stylesheet.css" rel="stylesheet" type="text/css">`) to include an external style sheet or the `HTMLStyleElement` node (i.e. `<style></style>`) to define a style sheet inline. In the HTML document below both of these Element node's are in the DOM and I verify which constructor, constructs these nodes.

Once a style sheet is added to an HTML document it's represented by the `CSSStylesheet` object. Each CSS rule inside of a style sheet is represent by a `CSSStyleRule` object.

## 9.2 Accessing all style sheets (i.e. CSSStylesheet objects) in the DOM

`document.styleSheets` gives access to a list of all style sheet objects (aka `CSSStylesheet`) explicitly linked (i.e. `<link>`) or embedded (i.e. `<style>`) in an HTML document.

In addtion to using `styleSheets` to access a documents styles sheets it's also possible to access a style sheet in an HTML document by first selecting the element in the DOM (`<style>` or `<link>`) and using the `sheet` property to gain access to the `CSSStyleSheet` object.

## 9.3 CSSStyleSheet properties and methods

To get accurate information pertaining to the available properties and methods on an `CSSStyleSheet` node it's best to ignore the specification and to ask the browser what is available.

## 9.4 CSSStyleRule overview

A `CSSStyleRule` object represents each CSS rule contained in a style sheet. Basicly a `CSSStyleRule` is the interface to the CSS properties and values attached to a selector.

## 9.5 CSSStyleRule properties and methods

To get accurate information pertaining to the available properties and methods on an `CSSStyleRule` node it's best to ignore the specification and to ask the browser what is available.

## 9.6 Getting a list of CSS Rules in a style sheet using CSSRules

As previously discussed the `styleSheets` list provides a list of style sheets contained in a document. The `CSSRules` list provides a list (aka `CSSRulesList`) of all the CSS rules (i.e. `CSSStyleRule` objects) in a specific style sheet.

## 9.7 Inserting & deleting CSS rules in a style sheet using .insertRule() and .deleteRule()

The `insertRule()` and `deleteRule()` methods provided the ability to programatically manipulate the CSS rules in a style sheet.

Deleting or removing a rule is as simple as calling `deleteRule()` method on a style sheet and passing it the index of the rule in the style sheet to be deleted.

## 9.8 Editing the value of a CSSStyleRule using the .style property

Just like the `style` property that facilitates the manipulation of inline styles on element nodes there is a also `style` property for `CSSStyleRule` objects that orchestrates the same manipulation of styles in style sheets.

## 9.9 Creating a new inline CSS style sheets

To craft a new style sheet on the fly after an html page is loaded one only has to create a new `<style>` node, add CSS rules using `innerHTML` to this node, then append the `<style>` node to the HTML document.

## 9.10 Programatically adding external style sheets to an HTML document

To add a CSS file to an HTML document programatically a `<link>` element node is created with the appropriate attributes and then the `<link>` element node is appended to the DOM.

## 9.11 Disabling/Enabling style sheets using disabled property

Using the `disabled` property of a `CSSStyleSheet` object it's possible to enable or disabled a style sheet.

---

# Chapter 10 - JS in the DOM

## 10.1 Inserting & executing JS overview

JS can be inserted in to an HTML document in a modern way by including external JS files or writing page level inline JS, which is basically the contents of an external JS file literally embed in the HTML page as a text node. Don't confuse element inline JS contained in attribute event handlers (i.e. `<div onclick="alert('yo')"></div>`) with page inline JS (i.e. `<script>alert('hi')</script>`).

Both methods of inserting JS into an HTML document require the use of a `<script>` element node. The `<script>` element can contain JS code or can be used to link to external JS files using the `src` attribute.

## 10.2 JS is parsed synchronously by default

By default when the DOM is being parsed and it encounters a `<script>` element it will stop parsing the document, block any further rendering & downloading, and exectue the JS.

Because this behavior is blocking and does not permit parallel parsing of the DOM or exection of JavaScriopt it's consider to be synchronous. If the JS is external to the html document the blocking is exacerbated because the JS must first be downloaed before it can be parsed.

The default blocking nature of a `<script>` element can have a significant effect on the performance of the visual rendering of a HTML web page. If you have a couple of script elements at the start of an html page nothing else is happening (e.g. DOM parsing & resource loading) until each one is downloaded and executed sequentially.

## 10.3 Defering the downloading & exectuion of external JS using defer

The `<script>` element has an attribute called defer that will defer the blocking, downloading, and executing of an external JS file until the browser has parsed the closing `<html>` node. Using this attribute simply defers what normally occurs when a web browser encounters a `<script>` node.

## 10.4 Asynchronously downloading & executing external JS files using async

The `<script>` element has an attribute called `async` that will override the sequential blocking nature of `<script>` elements when the DOM is being constructed by a web browser.

By using this attribute, we are telling the browser not to block the construction (i.e. DOM parsing, downloading other assets e.g. images, style sheets, etc...) of the html page and forgo the the sequential loading as well.

What happens by using the async attribute is the files are loaded in parallel and parsed in order of download once they are fully downloaded.

## 10.5 Forcing asynchronous downloading & parsing of external JS using dynamic <script>

A known hack for forcing a web browser into asynchronous JS downloading and parsing without using the async attribure is to programatically create `<script>` elements that include external JS files and insert them in the DOM.

## 10.6 Using the onload call back for asynchronous <script>'s so we know when it's loaded

The `<script>` element supports a load event handler (i.e. `onload`) that will execute once an external JS file has been loaded and executed.

## 10.7 Be mindful of <script> 's placement in HTML for DOM manipulation

Given a `<script>` elements synchronous nature, placing one in the `<head>` element of an HTML document presents a timing problem if the JS execution is dependant upon any of the DOM that proceeds the `<script>`.

Many developers, myself being one of them, for this reason will attempt to place all `<script>` elements before the closing `</body>` element. By doing this you can rest assured the DOM in front of the `<script>`'s has been parsed and is ready for scripting. As well, this strategy will remove a dependancy on DOM ready events that can liter a code base.

## 10.8 Getting a list of <script>'s in the DOM

The `document.scripts` property available from the document object provides a list (i.e. an HTMLCollection) of all of the scripts currently in the DOM.

---

# Chapter 11 - DOM Events

## 11.1 DOM events overview

An event, in terms of the DOM, is either a pre-defined or custom moment in time that occurs in relationship with an element in the DOM, the document object, or the window object. These moments are typically predetermined and programaticlly accounted for by associating functionality (i.e. handlers/callbacks) to occur when these moments in time come to pass. These moments can be initiated by that state of the UI (e.g. input is focused or something has been dragged), the state of the enviroment that is running the JS program (e.g. page is loaded or XHR request has finished), or the state of the program itself (e.g. start monitor users ui interaction for 30 seconds after the page has loaded).

Setting up events can be accomplished using inline attribute event handlers, property event handlers, or the `addEventListener()` method.

```js
// inline attribure event handler pattern
<body onclick="console.log('fire/trigger attribure event handler')">

// property event handler pattern
document.querySelector('div').onclick = function(){...)};

//addEventListener method pattern
document.querySelector('div').addEventListener('click',function(){...}, false);
```

While all three of these patterns for attaching an event to the DOM programatically schedule the event, only the `addEventListener()` provides a robust and organized solution. The inline attribute event handler mixes together JS and HTML and best practices advise keeping these things seperate.

The downside to using a property event handler is that only one value can be assigned to the event property at a time. Meaning, you can't add more than one propety event handler to a DOM node when assigning events as property values.

Additionaly, using event handlers inline or property event handlers can suffer from scoping nuances as one attempts to leverage the scope chain from the function that is invoked by the event. The `addEventListener()` smooths out all of these issues, and will be used throughout this chapter.

## 11.2 DOM event types

In the tables below I detail the most common pre-defined events that can be attached to Element nodes, the document object, and the window object. Of course not all events are directly applicable to the node or object it can be attached too. That is, just because you can attach the event without error, and most likley invoke the event (i.e. bubbling events like onchange to window), does not mean that adding something like window.onchange is logical given that this event, by design was not meant for the window object.

[See List](http://domenlightenment.com/#11.2)

Most used:

- Document: `readystatechange`, `DOMContentLoaded`
- Mouse: `click`, `dblclick`, `mouseenter`, `mouseleave`
- Keyboard: `keydown`, `keyup`, `keypress`
- Focus: `blur`, `focus`
- UI: `load`
- Form: `submit`

## 11.3 The event flow

When an event is invoked the event flows or propagates through the DOM, firing the same event on other nodes and JS objects. The event flow can be programmed to occur as a capture phase (i.e. DOM tree trunk to branch, left to right) or bubbling phase (i.e. DOM tree branches to trunk, right to left), or both.

In the code below I set up 10 event listeners that can all be invoked, due to the event flow, by clicking once on the `<div>` element in the HTML document. When the `<div>` is clicked the capture phase begins at the window object and propagates down the DOM tree firing the click event for each object (i.e. `window > document > <html> > <body> > event target`) until it hits the event target. Once the capture phase ends the target phase starts, firing the click event on the target element itself. Next the propagation phase propagates up from the event target firing the click event until it reaches the window object (i.e. `event target > <body> > <html> > document > window`). With this knowledge it should be obvious why clicking the `<div>` in the code example logs to the console 1,2,3,4,5,6,7,8,9,10.

```js
/* notice that I am passing the addEventListener() a boolean parameter of true so capture events fire, not just bubbling events*/

// 1 capture phase
window.addEventListener(
  'click',
  () => {
    console.log(1);
  },
  true,
);

// 2 capture phase
document.addEventListener(
  'click',
  () => {
    console.log(2);
  },
  true,
);

// 3 capture phase
document.documentElement.addEventListener(
  'click',
  () => {
    console.log(3);
  },
  true,
);

// 4 capture phase
document.body.addEventListener(
  'click',
  () => {
    console.log(4);
  },
  true,
);

// 5 target phase occurs during capture phase
document.querySelector('div').addEventListener(
  'click',
  () => {
    console.log(5);
  },
  true,
);

// 6 target phase occurs during bubbling phase
document.querySelector('div').addEventListener(
  'click',
  () => {
    console.log(6);
  },
  false,
);

// 7 bubbling phase
document.body.addEventListener(
  'click',
  () => {
    console.log(7);
  },
  false,
);

// 8 bubbling phase
document.documentElement.addEventListener(
  'click',
  () => {
    console.log(8);
  },
  false,
);

// 9 bubbling phase
document.addEventListener(
  'click',
  () => {
    console.log(9);
  },
  false,
);

// 10 bubbling phase
window.addEventListener(
  'click',
  () => {
    console.log(10);
  },
  false,
);
```

# 11.4 Adding event listeners to Element nodes, window object, and Document object

The `addEventListener()` method is avaliabe on all Element nodes, the window object, and the document object providing the ability to added event listeners to parts of an HTML document as well as JS objects relating to the DOM and BOM (browser object model).

```js
//add a mousemove event to a <div> element object, invoking the event during the bubbling phase
document.querySelector('div').addEventListener('mousemove',() => {...},false);
```

The `addEventListener()` method used in the above code example takes three arguments. The first argument is the type of event to listen for. Notice that the event type string does not contain the "on" prefix (i.e. `onmousemove`) that event handlers require. The second argument is the function to be invoked when the event occurs. The third parameter is a boolean indicating if the event should be fired during the capture phase or bubbling phase of the event flow.

Typically a developer wants events to fire during the bubbling phase so that object eventing handles the event before bubbling the event up the DOM. Because of this you almost always provide a false value as the last argument to the `addEventListener()`. In modern browsers if the 3rd parameter is not specified it will `default to false`.

## 11.5 Removing event listeners

The `removeEventListener()` method can be used to remove events listeners, if the orginal listener was not added using an anonymous function. In the code below I add two events listeners to the HTML document and attempt to remove both of them. However, only the listener that was attached using a function reference is removed.
Anonymous functions added using `addEventListener()` method simply cannot be removed.

## 11.6 Getting event properties from the event object

The handler or callback function invoked for events is sent by default a parameter that contains all relevant information about an event itself. In the code below I demostrate access to this event object and log all of its properties and values for a load event as well as a click event. Make sure you click the `<div>` to see the properties assocaited with a click event.

```js
document.querySelector('div').addEventListener('click',(event) => {...},false);
```

Keep in mind that each event will contain slightly different properties based on the event type (e.g. MouseEvent, KeyboardEvent, WheelEvent).

The event object also provides the stopPropagation(), stopImediatePropagation(), and preventDefault() methods.

## 11.7 The value of this when using addEventListener()

The value of `this` inside of the event listener function passed to the `addEventListener()` method will be a reference to the node or object the event is attached too.

When events are invoked as part of the event flow the this value will remain the value of the node or object that the event listener is attached too.

Additionally it's possible using the event.currentTarget property to get the same reference, to the node or object invoking the event listener, that the this property provides.

## 11.8 Referencing the target of an event and not the node or object the event is invoked on

Because of the event flow it's possible to click a `<div>`, contained inside of a `<body>` element and have a click event listener attached to the `<body>` element get invoked. When this happens, the event object passed to the event listener function attached to the `<body>` provides a reference (i.e. `event.target`) to the node or object that the event originated on (i.e. the target).

The event.target can be extremely useful when an event that fires because of the event flow needs knowledge about the origin of the event.

## 11.9 Cancelling default browser events using preventDefault()

Browsers provide several events already wired up when an HTML page is presented to a user. For example, clicking a link has a corresponding event (i.e. you navigate to a url). So does clicking a checkbox (i.e. box is checked) or typing text into a text field (i.e. text is inputed and appears on screen). These browser events can be prevented by calling the preventDefault() method inside of the event handler function associated with a node or object that invokes a browser default event.

```js
// stop the default event for <a> which would be to load a url
document.querySelector('a').addEventListener(
  'click',
  (event) => {
    event.preventDefault();
  },
  false,
);
```

The `preventDefault()` methods does not stop events from propagating (i.e. bubbling or capture phases)

Providing a return false at the end of the body of the event listener has the same result as call the preventDefault() method.

## 11.10 Stoping the event flow using stopPropagation()

Calling `stopProgagation()` from within an event handler/listener will stop the capture and bubble event flow phases, but any events directly attached to the node or object will still be invoked.

Additionally using `stopPropagation()` does not prevent default events.

## 11.11 Stoping the event flow as well as other like events on the same target using stopImmediatePropagation()

Calling the `stopImmediatePropagation()` from within an event handler/listener will stop the event flow phases (i.e. `stopPropagation()`), as well as any other like events attached to the event target that are attached after the event listener that invokes the `stopImmediatePropagation()` method.

Using the `stopImmediatePropagation()` does not prevent default events. Browser default events still get invoked and only calling `preventDefault()` will stop these events.

## 11.12 Custom events

A developer is not limited to the predefined event types. it's possible to attach and invoke a custom event, using the `addEventListener()` method like normal in combiniation with `document.createEvent(), initCustomEvent(), and dispatchEvent()`.

## 11.13 Simulating/Triggering mouse events

Simulating an event is not unlike creating a custom event. In the case of simulating a mouse event we create a 'MouseEvent' using `document.createEvent()`. Then, using `initMouseEvent()` we setup the mouse event that is going to occur. Next the mouse event is dispatched on the element that we'd like to simulate an event on.

## 11.14 Event delegation

Event delegation is the programmatic act of leveraging the event flow and a single event listener to deal with multiple event targets. A side effect of event delegation is that the event targets don't have to be in the DOM when the event is created in order for the targets to respond to the event. This is of course rather handy when dealing with XHR responses that update the DOM. By implementing event delegation new content that is added to the DOM post JS load parsing can immediately start responding to events.

Imagine you have a table with an unlimited number of rows and columns. Using event delegation we can add a single event listener to the `<table>` node which acts as a delegate for the node or object that is the initial target of the event. In the code example below, clicking any of the `<td>`'s (i.e. the target of the event) will delegate its event to the click listener on the `<table>`. Don't forget this is all made possible because of the event flow and in this specific case the bubbling phase.

```js
document.querySelector('table').addEventListener(
  'click',
  function(event) {
    //make sure we only run code if a td is the target
    if (event.target.tagName.toLowerCase() === 'td') {
      //use event.target to gain access to target of the event which is the td
      console.log(event.target.textContent);
    }
  },
  false,
);
```

If we were to update the table in the code example with new rows, the new rows would responded to the click event as soon as they were render to the screen because the click event is delegated to the `<table>` element node.