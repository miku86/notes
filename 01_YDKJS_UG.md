# You Don't Know JS: Up & Going

- [Chapter 1 - Into Programming](#chapter-1---into-programming)
- [Chapter 2 - Into JavaScript](#chapter-2---into-javascript)
- [Chapter 3 - Into YDKJS](#chapter-3---into-ydkjs)

## Chapter 1 - Into Programming

*Up & Going* is an introduction to several basic concepts of programming.
This book will briefly explore what you need to get *up and going*.

Chapter 1 is a quick overview of the things you'll want to learn more about
and practice to get *into programming*.
Chapter 2 introduces what JavaScript is about, but again, it's not a comprehensive guide
- that's what the rest of the *YDKJS* books are for!

## Try It Yourself

### Output
`console.log(..)` and  `alert(..)` for output.

### Input
The most common way: HTML form elements and JS to read those values into your program's variables.

Easier way to get input for simple learning purposes: `prompt(..)`

## Values & Types
JavaScript has built-in types for each of these so called *primitive* values:

* When you need to do math, you want a `number`.
* When you need to print a value on the screen, you need a `string`.
* When you need to make a decision in your program, you need a `boolean`.

Values that are included directly in the source code are called *literals*.
`string` literals are surrounded by double quotes `"..."`.
`number` and `boolean` literals are just presented as is (i.e., `42`, `true`, etc.).

Beyond, it's common for programming languages to provide *arrays*, *objects*, *functions*, and more.

### Converting Between Types
If you have a `number` but need to print it on the screen, you need to convert the value to a `string`, this conversion is called "coercion.".

If someone enters a series of numeric characters into a form on an ecommerce page, that's a `string`, but if you need to then use that value to do math operations, you need to *coerce* it to a `number`.

```js
var a = "42";
var b = Number( a );

console.log( a );	// "42"
console.log( b );	// 42
```

Using `Number(..)` is an *explicit* coercion from any other type to the `number` type.

What happens when you try to compare two values that are not already of the same type,
which would require *implicit* coercion.

When comparing the string `"99.99"` to the number `99.99`, most people would agree they are equivalent.
It's the same value in two different representations, two different *types*.
JavaScript will sometimes kick in and *implicitly* coerce values to the matching types.

So if you use the `==` loose equals operator to make the comparison `"99.99" == 99.99`,
JavaScript will convert the left-hand side `"99.99"` to its `number` equivalent `99.99`.
The comparison then becomes `99.99 == 99.99`, which is of course `true`.

Implicit coercion is a mechanism that *should be learned* by anyone.

## Code Comments
One of the most important lessons you can learn about writing code is that it's not just for the computer.

You should strive not just to write programs that work correctly, but programs that make sense when examined.

But another important part is code comments, text in your program purely to explain things to a human.

But some observations and guidelines are quite useful:
* Code without comments is suboptimal.
* Too many comments is probably a sign of poorly written code.
* Comments should explain *why*, not *what*. They can optionally explain *how* if that's particularly confusing.

## Variables
Most useful programs need to track a value as it changes over the course of the program.
The easiest way is to assign a value to a symbolic container, called a *variable*.

JavaScript uses *dynamic typing*, meaning variables can hold values of any *type* without any *type* enforcement.

`var name = "Peter"`

A variable holds a running value that changes over the course of the program,
illustrating the primary purpose of variables: managing program *state*.

Another common usage of variables is for centralizing value setting.
This is more typically called *constants*, when you declare a variable with a value
and intend for that value to *not change* throughout the program.

You declare these *constants*, often at the top of a program,
so that it's convenient for you to have one place to go to alter a value if you need to.

## Conditionals
There are quite a few ways we can express conditionals (aka decisions) in our programs.

The most common one is the if statement. Essentially, you're saying, "If this condition is true, do the following...".

```js
var bank_balance = 302;
var amount = 99;

if (amount < bank_balance) {
	console.log( "I want to buy this phone!" );
}
```

The if statement requires an expression in between the parentheses `( )` that can be treated as either true or false. In this program, we provided the expression `amount < bank_balance`, which indeed will either evaluate to true or false depending on the amount in the bank_balance variable.

## Loops
Repeating a set of actions until a certain condition fails -- in other words, repeating only while the condition holds -- is the job of programming loops; loops can take different forms, but they all satisfy this basic behavior.

A loop includes the test condition as well as a block (typically as { .. }). Each time the loop block executes, that's called an iteration.

```js
while (numOfCustomers > 0) {
	console.log( "How may I help you?" );
	// help the customer...
	numOfCustomers = numOfCustomers - 1;
}
```

## Functions
Similarly, your program will almost certainly want to break up the code's tasks into reusable pieces, instead of repeatedly repeating yourself repetitiously. The way to do this is to define a function.

A function is generally a named section of code that can be "called" by name, and the code inside it will be run each time.

```js

function printAmount() {
	console.log( amount.toFixed( 2 ) );
}

var amount = 10;
printAmount(); // "10.00"
amount = amount * 2;
printAmount(); // "20.00"
```

## Scope
In JavaScript, each function gets its own scope. Scope is basically a collection of variables as well as the rules for how those variables are accessed by name. Only code inside that function can access that function's scoped variables.

A variable name has to be unique within the same scope -- there can't be two different a variables sitting right next to each other. But the same variable name a could appear in different scopes.

```js
function one() {
	// this `a` only belongs to the `one()` function
	var a = 1;
	console.log( a );
}

function two() {
	// this `a` only belongs to the `two()` function
	var a = 2;
	console.log( a );
}

one();		// 1
two();		// 2
```

## Practice
There is absolutely no substitute for practice in learning programming.
No amount of articulate writing on my part is alone going to make you a programmer.

* Write a program to calculate the total price of your phone purchase. You will keep purchasing phones until you run out of money in your bank account. You'll also buy accessories for each phone as long as your purchase amount is below your mental spending threshold.
* After you've calculated your purchase amount, add in the tax, then print out the calculated purchase amount, properly formatted.
* Finally, check the amount against your bank account balance to see if you can afford it or not.
* You should set up some constants for the "tax rate," "phone price," "accessory price," and "spending threshold," as well as a variable for your "bank account balance.""
* You should define functions for calculating the tax and for formatting the price with a "$" and rounding to two decimal places.

Here's my JavaScript solution for this exercise:

```js
const SPENDING_THRESHOLD = 200;
const TAX_RATE = 0.08;
const PHONE_PRICE = 99.99;
const ACCESSORY_PRICE = 9.99;

var bank_balance = 303.91;
var amount = 0;

function calculateTax(amount) {
	return amount * TAX_RATE;
}

function formatAmount(amount) {
	return "$" + amount.toFixed( 2 );
}

// keep buying phones while you still have money
while (amount < bank_balance) {
	// buy a new phone!
	amount = amount + PHONE_PRICE;

	// can we afford the accessory?
	if (amount < SPENDING_THRESHOLD) {
		amount = amount + ACCESSORY_PRICE;
	}
}

// don't forget to pay the government, too
amount = amount + calculateTax( amount );

console.log(
	"Your purchase: " + formatAmount( amount )
);
// Your purchase: $334.76

// can you actually afford this purchase?
if (amount > bank_balance) {
	console.log(
		"You can't afford this purchase. :("
	);
}
// You can't afford this purchase. :(
```

**Note:** The simplest way to run this JavaScript program is to type it into the developer console of your nearest browser.


## Review
There are just a few basic concepts you need to wrap your head around.
These act like building blocks.
To build a tall tower, you start first by putting block on top of block on top of block.

Here are some of the essential programming building blocks:
* You need *operators* to perform actions on values.
* You need *values and *types* to perform different kinds of actions like math on `number`s or output with `string`s.
* You need *variables* to store data (aka *state*) during your program's execution.
* You need *conditionals* like `if` statements to make decisions.
* You need *loops* to repeat tasks until a condition stops being true.
* You need *functions* to organize your code into logical and reusable chunks.

Code comments are one effective way to write more readable code,
which makes your program easier to understand, maintain, and fix later if there are problems.

Finally, don't neglect the power of practice.
The best way to learn how to write code is to write code.

---

## Chapter 2 - Into JavaScript
You can think of this chapter as an overview of the topics covered in detail throughout the rest of this series.

## Values & Types
The following built-in types are available:

* `string`
* `number`
* `boolean`
* `null` and `undefined`
* `object`
* `symbol`

JavaScript provides a `typeof` operator that can examine a value and tell you what type it is:

```s
var a = "hello world";
typeof a;				// "string"
```

### Objects {...}
The `object` type refers to a compound value where you can set properties (named locations) that each hold their own values of any type.

This is perhaps one of the most useful value types in all of JavaScript.

```js
var obj = {
	a: "hello world",
	b: 42,
};

obj.a;		// "hello world"
obj.b;		// 42

obj["a"];	// "hello world"
obj["b"];	// 42
```

#### Arrays [...]
An array is an `object` that holds values not in named properties/keys, but rather in numerically indexed positions. For example:

```js
var arr = [
	"hello world",
	42
];

arr[0];			// "hello world"
arr[1];			// 42
arr.length;		// 2

typeof arr;		// "object"
```

Because arrays are special objects, they can also have properties,
including the automatically updated `length` property.

You theoretically could use an array as a normal object with your own named properties,
or you could use an `object` but only give it numeric properties (`0`, `1`, etc.) similar to an array.

**The best and most natural approach is to use arrays for numerically positioned values
and use `object`s for named properties.**

#### Functions
The other `object` subtype you'll use all over your JS programs is a function:

```js
function foo() {
	return 42;
}

typeof foo;			// "function"
typeof foo();		// "number"
foo(); // 42
```

Again, functions are a subtype of `objects` -- `typeof` returns `"function"`.


### Built-In Type Methods
The built-in types and subtypes we've just discussed have behaviors exposed as properties and methods that are quite powerful and useful.

For example:

```js
var a = "hello world";
var b = 3.14159;

a.length;				// 11
a.toUpperCase();		// "HELLO WORLD"
b.toFixed(4);			// "3.1416"
```

The "how" behind being able to call `a.toUpperCase()` is more complicated than just that method existing on the value.

Briefly, there is a `String` (capital `S`) object wrapper form, typically called a "native," that pairs with the primitive `string` type;
it's this object wrapper that defines the `toUpperCase()` method on its prototype.

When you use a primitive value like `"hello world"` as an `object` by referencing a property or method (e.g., `a.toUpperCase()`), JS automatically "boxes" the value to its object wrapper counterpart (hidden under the covers).

### Comparing Values
There are two main types of value comparison that you will need to make in your JS programs: *equality* and *inequality*. The result of any comparison is a strictly `boolean` value (`true` or `false`), regardless of what value types are compared.

#### Coercion
Coercion comes in two forms in JavaScript: *explicit* and *implicit*.
Explicit coercion is simply that you can see obviously from the code that a conversion from one type to another will occur,
whereas implicit coercion is when the type conversion can happen as more of a non-obvious side effect of some other operation.

The majority of cases you can construct with type coercion are quite sensible and understandable,
and can even be used to *improve* the readability of your code.

*Explicit* coercion:

```js
var a = "42"; // "42"
var b = Number( a ); // 42 -- the number!
```

*Implicit* coercion:

```js
var a = "42"; // "42"
var b = a * 1;	// "42" implicitly coerced to 42 here
```

#### Truthy & Falsy
The specific list of "falsy" values in JavaScript is as follows:

* `""` (empty string)
* `0`, `-0`, `NaN` (invalid `number`)
* `null`, `undefined`
* `false`

Any value that's not on this "falsy" list is "truthy."

It's important to remember that a non-`boolean` value only follows this "truthy"/"falsy" coercion if it's actually coerced to a `boolean`. It's not all that difficult to confuse yourself with a situation that seems like it's coercing a value to a `boolean` when it's not.


#### Equality
`==` checks for value equality and `===` checks for both value and type equality.
`==` checks for value equality with coercion allowed,
`===` checks for value equality without allowing coercion;
`===` is often called "strict equality" for this reason.

Consider the implicit coercion that's allowed by the `==` loose-equality comparison and not allowed with the `===` strict-equality:

```js
var a = "42";
var b = 42;

a == b;			// true
a === b;		// false
```

In the `a == b` comparison, JS notices that the types do not match, so it goes through an ordered series of steps to coerce one or both values to a different type until the types match, where then a simple value equality can be checked.
`"42"` becomes `42`, to make the comparison `42 == 42`.

The `a === b` produces `false`, because the coercion is not allowed, so the simple value comparison obviously fails.
Many developers feel that `===` is more predictable, so they advocate always using that form and staying away from `==`.
I believe `==` is a powerful tool that helps your program, *if you take the time to learn how it works.*

* If either value (aka side) in a comparison could be the `true` or `false` value, avoid `==` and use `===`.
* If either value in a comparison could be of these specific values (`0`, `""`, or `[]` -- empty array), avoid `==` and use `===`.
* In *all* other cases, you're safe to use `==`. Not only is it safe, but in many cases it simplifies your code in a way that improves readability.

If you can be certain about the values, and `==` is safe, use it!
If you can't be certain about the values, use `===`.

You should take special note of the `==` and `===` comparison rules
if you're comparing two non-primitive values, like `object`s (including `function` and `array`).
Because those values are actually held by reference,
both `==` and `===` comparisons will simply check whether the references match, not anything about the underlying values.

For example, `array`s are by default coerced to `string`s by simply joining all the values with commas (`,`) in between. You might think that two `array`s with the same contents would be `==` equal, but they're not:

```js
var a = [1,2,3];
var b = [1,2,3];
var c = "1,2,3";

a == c;		// true
b == c;		// true
a == b;		// false
```

#### Inequality

```js
var a = 41;
var b = "42";
var c = "43";

a < b;		// true
b < c;		// true
```

If both values in the `<` comparison are `string`s (`b < c`),
the comparison is made alphabetically.
If one or both is not a `string` (`a < b`),
then both values are coerced to be `number`s.

The biggest gotcha you may run into here with comparisons between potentially different value types -- remember, there are no "strict inequality" forms to use -- is when one of the values cannot be made into a valid number, such as:

```js
var a = 42;
var b = "foo";

a < b;		// false
a > b;		// false
a == b;		// false
```

The `b` value is being coerced to the "invalid number value" `NaN` in the `<` and `>` comparisons,
and the specification says that `NaN` is neither greater-than nor less-than any other value.

The `==` comparison fails for a different reason.
`a == b` could fail if it's interpreted either as `42 == NaN` or `"42" == "foo"` --
as we explained earlier, the former is the case.


## Variables

### Function Scopes

#### Hoisting
Wherever a `var` appears inside a scope, that declaration is taken to belong to the entire scope and accessible everywhere throughout.

Metaphorically, this behavior is called *hoisting*, when a `var` declaration is conceptually "moved" to the top of its enclosing scope.

Consider:

```js
var a = 2;

foo(); // works because `foo()` declaration is "hoisted"

function foo() {
	a = 3;
	console.log( a );	// 3
	var a; // declaration is "hoisted" to the top of `foo()`
}

console.log( a );	// 2
```

#### Nested Scopes
When you declare a variable, it is available anywhere in that scope, as well as any lower/inner scopes.

```js
function foo() {
	var a = 1;

	function bar() {
		var b = 2;

		function baz() {
			var c = 3;

			console.log( a, b, c );	// 1 2 3
		}

		baz();
		console.log( a, b );		// 1 2
	}

	bar();
	console.log( a );				// 1
}

foo();
```

`c` is not available inside of `bar()`, because it's declared only inside the inner `baz()` scope, and `b` is not available to `foo()` for the same reason.

If you try to access a variable's value in a scope where it's not available, you'll get a `ReferenceError` thrown. If you try to set a variable that hasn't been declared, you'll either end up creating a variable in the top-level global scope (bad!) or getting an error, depending on "strict mode" (see "Strict Mode"). Always formally declare your variables.


#### Let
In addition to creating declarations for variables at the function level, ES6 lets you declare variables to belong to individual blocks (pairs of `{ .. }`), using the `let` keyword. Besides some nuanced details, the scoping rules will behave roughly the same as we just saw with functions:

```js
function foo() {
	var a = 1;

	if (a >= 1) {
		let b = 2;

		while (b < 5) {
			let c = b * 2;
			b++;

			console.log( a + c );
		}
	}
}

foo();
// 5 7 9
```

Because of using `let` instead of `var`, `b` will belong only to the `if` statement and thus not to the whole `foo()` function's scope. Similarly, `c` belongs only to the `while` loop. Block scoping is very useful for managing your variable scopes in a more fine-grained fashion, which can make your code much easier to maintain over time.


## Conditionals
Another form of conditional in JavaScript is the "conditional operator," often called the "ternary operator."
It's like a more concise form of a single `if..else` statement.

```js
var a = 42;
var b = (a > 41) ? "hello" : "world";

// similar to:
// if (a > 41) {
//    b = "hello";
// }
// else {
//    b = "world";
// }
```

## Strict Mode
ES5 added a "strict mode" to the language, which tightens the rules for certain behaviors. Generally, these restrictions are seen as keeping the code to a safer and more appropriate set of guidelines. Also, adhering to strict mode makes your code generally more optimizable by the engine.

**Strict mode is a big win for code, and you should use it for all your programs.**

If you turn on strict mode in your code, and you get errors, or code starts behaving buggy, your temptation might be to avoid strict mode. But that instinct would be a bad idea to indulge.

If strict mode causes issues in your program, almost certainly it's a sign that you have things in your program you should fix.

Not only will strict mode keep your code to a safer path, and not only will it make your code more optimizable, but it also represents the future direction of the language.

## Functions As Values
So far, we've discussed functions as the primary mechanism of *scope* in JavaScript.

```js
function foo() {
	// ..
}
```

Though it may not seem obvious from that syntax, `foo` is basically just a variable in the outer enclosing scope that's given a reference to the `function` being declared. That is, the `function` itself is a value, just like `42` or `[1,2,3]` would be.

This may sound like a strange concept at first, so take a moment to ponder it. Not only can you pass a value (argument) *to* a function, but *a function itself can be a value* that's assigned to variables, or passed to or returned from other functions.

As such, a function value should be thought of as an expression, much like any other value or expression.

Consider:

```js
var foo = function() {..};
var x = function bar() {..};
```

The first function expression assigned to the `foo` variable is called *anonymous* because it has no `name`.

The second function expression is *named* (`bar`), even as a reference to it is also assigned to the `x` variable.

*Named function expressions* are generally more preferable, though *anonymous function expressions* are still extremely common.


### Immediately Invoked Function Expressions (IIFEs)
In the previous snippet, neither of the function expressions are executed -- we could if we had included `foo()` or `x()`, for instance.

There's another way to execute a function expression, which is typically referred to as an *immediately invoked function expression* (IIFE):

```js
(function IIFE(){
	console.log( "Hello!" );
})(); // "Hello!"
```

The outer `( .. )` that surrounds the `(function IIFE(){ .. })` function expression is just a nuance of JS grammar needed to prevent it from being treated as a normal function declaration.

The final `()` on the end of the expression is what actually executes the function expression referenced immediately before it.

```js
function foo() { .. }
// `foo` function reference expression, then `()` executes it
foo();

// `IIFE` function expression, then `()` executes it
(function IIFE(){ .. })();
```

As you can see, listing the `(function IIFE(){ .. })` before its executing `()` is essentially the same as including `foo` before its executing `()`.

Because functions create variable *scope*, using an IIFE in this fashion is often used to declare variables that won't affect the surrounding code outside the IIFE:

```js
var a = 42;

(function IIFE(){
	var a = 10;
	console.log( a );	// 10
})();

console.log( a );		// 42
```

### Closure
**Closure will be one of the most important techniques in your JS skillset.**

You can think of closure as a way to "remember" and continue to access a function's scope (its variables) even once the function has finished running.

```js
function makeAdder(x) {
	// parameter `x` is an inner variable
	// inner function `add()` uses `x`, so it has a "closure" over it
	function add(y) {
		return y + x;
	};

	return add;
}
```

The reference to the inner `add(..)` function that gets returned with each call to the outer `makeAdder(..)` is able to remember whatever `x` value was passed in to `makeAdder(..)`. Now, let's use `makeAdder(..)`:

```js
// `plusOne` gets a reference to the inner `add(..)` function with closure
// over the `x` parameter of the outer `makeAdder(..)`
var plusOne = makeAdder( 1 );

// `plusTen` gets a reference to the inner `add(..)` function with closure
// over the `x` parameter of the outer `makeAdder(..)`
var plusTen = makeAdder( 10 );

plusOne( 3 );		// 4  <-- 1 + 3
plusTen( 13 );		// 23 <-- 10 + 13
```

More on how this code works:

1. When we call `makeAdder(1)`, we get back a reference to its inner `add(..)` that remembers `x` as `1`. We call this function reference `plusOne(..)`.
2. When we call `makeAdder(10)`, we get back another reference to its inner `add(..)` that remembers `x` as `10`. We call this function reference `plusTen(..)`.
3. When we call `plusOne(3)`, it adds `3` (its inner `y`) to the `1` (remembered by `x`), and we get `4` as the result.
4. When we call `plusTen(13)`, it adds `13` (its inner `y`) to the `10` (remembered by `x`), and we get `23` as the result.

**It's one of the most powerful and useful techniques in all of programming.
It's definitely worth the effort to let your brain simmer on closures for a bit.**


#### Modules
The most common usage of closure in JavaScript is the module pattern.
Modules let you define private implementation details (variables, functions) that are hidden from the outside world.

```js
function User(){
	var username, password;

	function doLogin(user,pw) {
		username = user;
		password = pw;

		// do the rest of the login work
	}

	var publicAPI = {
		login: doLogin
	};

	return publicAPI;
}

// create a `User` module instance
var fred = User();

fred.login( "fred", "12Battery34!" );
```

The `User()` function serves as an outer scope that holds the variables `username` and `password`, as well as the inner `doLogin()` function; these are all private inner details of this `User` module that cannot be accessed from the outside world.

**Warning:** We are not calling `new User()` here. `User()` is just a function, not a class to be instantiated. Using `new` would be inappropriate and actually waste resources.

Executing `User()` creates an *instance* of the `User` module -- a whole new scope is created, and thus a whole new copy of each of these inner variables/functions. We assign this instance to `fred`. If we run `User()` again, we'd get a new instance entirely separate from `fred`.

The inner `doLogin()` function has a closure over `username` and `password`, meaning it will retain its access to them even after the `User()` function finishes running.

`publicAPI` is an object with one property/method on it, `login`, which is a reference to the inner `doLogin()` function. When we return `publicAPI` from `User()`, it becomes the instance we call `fred`.

At this point, the outer `User()` function has finished executing. Normally, you'd think the inner variables like `username` and `password` have gone away. But here they have not, because there's a closure in the `login()` function keeping them alive.

That's why we can call `fred.login(..)` and it can still access `username` and `password` inner variables.

## `this` Identifier

If a function has a `this` reference inside it, that `this` reference usually points to an `object`.
But which `object` it points to depends on how the function was called.

It's important to realize that `this` *does not* refer to the function itself, as is the most common misconception.

```js
function foo() {
	console.log( this.bar );
}

var bar = "global";

var obj1 = {
	bar: "obj1",
	foo: foo
};

var obj2 = {
	bar: "obj2"
};

foo();				// "global"
obj1.foo();			// "obj1"
foo.call( obj2 );		// "obj2"
new foo();			// undefined
```

There are four rules for how `this` gets set, and they're shown in those last four lines of that snippet.

1. `foo()` ends up setting `this` to the global object in non-strict mode -- in strict mode, `this` would be `undefined` and you'd get an error in accessing the `bar` property -- so `"global"` is the value found for `this.bar`.
2. `obj1.foo()` sets `this` to the `obj1` object.
3. `foo.call(obj2)` sets `this` to the `obj2` object.
4. `new foo()` sets `this` to a brand new empty object.

**To understand what `this` points to, you have to examine how the function in question was called.**

## Prototypes
When you reference a property on an object, if that property doesn't exist, JavaScript will automatically use that object's internal prototype reference to find another object to look for the property on. You could think of this almost as a fallback if the property is missing.

```js
var foo = {
	a: 42
};

// create `bar` and link it to `foo`
var bar = Object.create( foo );

bar.b = "hello world";

bar.b;		// "hello world"
bar.a;		// 42 <-- delegated to `foo`
```

It may help to visualize the `foo` and `bar` objects and their relationship:

The `a` property doesn't actually exist on the `bar` object, but because `bar` is prototype-linked to `foo`,
JavaScript automatically falls back to looking for `a` on the `foo` object, where it's found.

## Old & New
There are two main techniques you can use to "bring" the newer JavaScript stuff to the older browsers: polyfilling and transpiling.

### Polyfilling
That is taking the definition of a newer feature and producing a piece of code that's equivalent to the behavior, but is able to run in older JS environments.

For example, ES6 defines a utility called `Number.isNaN(..)` to provide an accurate non-buggy check for `NaN` values, deprecating the original `isNaN(..)` utility. But it's easy to polyfill that utility so that you can start using it in your code regardless of whether the end user is in an ES6 browser or not.

```js
if (!Number.isNaN) {
	Number.isNaN = function isNaN(x) {
		return x !== x;
	};
}
```

The `if` statement guards against applying the polyfill definition in ES6 browsers where it will already exist.
If it's not already present, we define `Number.isNaN(..)`.

**Note:** The `NaN` value is the only one that would make `x !== x` be `true`.

Not all new features are fully polyfillable. You should be really, really careful in implementing a polyfill yourself, to make sure you are adhering to the specification as strictly as possible.

### Transpiling
The better option is to use a tool that converts your newer code into older code equivalents.
This process is commonly called "transpiling," a term for transforming + compiling.

Essentially, your source code is authored in the new syntax form, but what you deploy to the browser is the transpiled code in old syntax form. You typically insert the transpiler into your build process, similar to your code linter or your minifier.

There are several important reasons you should care about transpiling:
* The new syntax added to the language is designed to make your code more readable and maintainable. You should prefer writing newer and cleaner syntax, not only for yourself but for all other members of the development team.
* If you transpile only for older browsers, but serve the new syntax to the newest browsers, you get to take advantage of browser performance optimizations with the new syntax. This also lets browser makers have more real-world code to test their implementations and optimizations on.
* Using the new syntax earlier allows it to be tested more robustly in the real world, which provides earlier feedback to the JavaScript committee. If issues are found early enough, they can be changed/fixed before those language design mistakes become permanent.

Here's a quick example of transpiling. ES6 adds a feature called "default parameter values." It looks like this:

```js
function foo(a = 2) {
	console.log( a );
}

foo();		// 2
foo( 42 );	// 42
```

Simple, right? Helpful, too! But it's new syntax that's invalid in pre-ES6 engines.
So what will a transpiler do with that code to make it run in older environments?

```js
function foo() {
	var a = arguments[0] !== (void 0) ? arguments[0] : 2;
	console.log( a );
}
```

It checks if the `arguments[0]` value is `void 0` (aka `undefined`), and if so provides the `2` default value;
otherwise, it assigns whatever was passed.

The last important detail to emphasize about transpilers is that they should now be thought of as a standard part of the JS development ecosystem and process.

If you use a transpiler by default, you'll always be able to make that switch to newer syntax whenever you find it useful, rather than always waiting for years for today's browsers to phase out.

Use Babel (https://babeljs.io) to transpile ES6+ into ES5

## Non-JavaScript
The reality is that most JS is written to run in and interact with environments like browsers. A good chunk of the stuff that you write in your code is not directly controlled by JavaScript.

The most common non-JavaScript JavaScript you'll encounter is the DOM API. For example:

```js
var el = document.getElementById( "foo" );
```

The `document` variable exists as a global variable and is not provided by the JS engine, nor is it particularly controlled by the JavaScript specification. It takes the form of something that looks an awful lot like a normal JS `object`, but it's a special `object,` often called a "host object."

Moreover, the `getElementById(..)` method on `document` looks like a normal JS function, but it's just a thinly exposed interface to a built-in method provided by the DOM from your browser.

 `alert(..)` is provided to your JS program by the browser, not by the JS engine itself.
 The call you make sends the message to the browser internals and it handles drawing and displaying the message box.

The same goes with `console.log(..)`; your browser provides such mechanisms and hooks them up to the developer tools.

You need to be aware of them, as they'll be in every JS program you write!

## Review

The first step to learning JavaScript's flavor of programming is to get a basic understanding of its core mechanisms like values, types, function closures, `this`, and prototypes.

---

## Chapter 3 - Into YDKJS
I'm going to use this final chapter to briefly summarize what to expect from the rest of the books in the series, and how to most effectively go about building a foundation of JS learning on top of *YDKJS*.

## Scope & Closures
**One of the most fundamental things to learn is how scoping of variables really works in JavaScript.**

The JS engine compiles your code right before (and sometimes during!) execution. So we use some deeper understanding of the compiler's approach to our code to understand how it finds and deals with variable and function declarations. Along the way, we see the typical metaphor for JS variable scope management, "Hoisting."

This critical understanding of "lexical scope" is what we then base our exploration of closure on for the last chapter of the book. **Closure is perhaps the single most important concept in all of JS, but if you haven't first grasped firmly how scope works, closure will likely remain beyond your grasp.**

**The module pattern is perhaps the most prevalent code organization pattern in all of JavaScript; deep understanding of it should be one of your highest priorities.**

## this & Object Prototypes
**Perhaps one of the most widespread and persistent mistruths about JavaScript is that the `this` keyword refers to the function it appears in. The `this` keyword is dynamically bound based on how the function in question is executed, and it turns out there are four simple rules to understand and fully determine `this` binding.**

Closely related to the `this` keyword is the object prototype mechanism, which is a look-up chain for properties, similar to how lexical scope variables are found.

Unfortunately, the desire to bring class and inheritance design pattern thinking to JavaScript is just about the worst thing you could try to do, because while the syntax may trick you into thinking there's something like classes present, in fact the prototype mechanism is fundamentally opposite in its behavior.

What's at issue is whether it's better to ignore the mismatch and pretend that what you're implementing is "inheritance," or whether it's more appropriate to learn and embrace how the object prototype system actually works. The latter is more appropriately named "behavior delegation."

## Types & Grammar
Perhaps no topic causes more frustration with JS developers than when you talk about the confusions surrounding implicit coercion.

I'm asserting that coercion is an incredibly useful and totally underestimated tool that *you should be using in your code.* I'm saying that coercion, when used properly, makes your code better. I believe it's one of the main keys to upping your JS game.

## Async & Performance
The first three titles of this series focus on the core mechanics of the language, but the fourth title branches out slightly to cover patterns on top of the language mechanics for managing asynchronous programming.

Asynchrony is not only critical to the performance of our applications, it's increasingly becoming *the* critical factor in writability and maintainability.

We move into examining callbacks as the primary method of enabling asynchrony. But it's here that we quickly see that the callback alone is hopelessly insufficient for the modern demands of asynchronous programming. We identify two major deficiencies of callbacks-only coding: *Inversion of Control* (IoC) trust loss and lack of linear reason-ability.

To address these two major deficiencies, ES6 introduces two new mechanisms: promises and generators.

Promises are a time-independent wrapper around a "future value," which lets you reason about and compose them regardless of if the value is ready or not yet. Moreover, they effectively solve the IoC trust issues by routing callbacks through a trustable and composable promise mechanism.

Generators introduce a new mode of execution for JS functions, whereby the generator can be paused at `yield` points and be resumed asynchronously later. The pause-and-resume capability enables synchronous, sequential looking code in the generator to be processed asynchronously behind the scenes. By doing so, we address the non-linear, non-local-jump confusions of callbacks and thereby make our asynchronous code sync-looking so as to be more reason-able.

But it's the combination of promises and generators that "yields" our most effective asynchronous coding pattern to date in JavaScript. In fact, much of the future sophistication of asynchrony coming in ES7 and later will certainly be built on this foundation. To be serious about programming effectively in an async world, you're going to need to get really comfortable with combining promises and generators.

If promises and generators are about expressing patterns that let our programs run more concurrently and thus get more processing accomplished in a shorter period, JS has many other facets of performance optimization worth exploring.

The *Async & Performance* title is designed to give you all the tools and skills you need to write reasonable and performant JavaScript code.

## ES6 & Beyond
JavaScript is never going to stop evolving. This title is dedicated to both the short- and mid-term visions of where the language is headed, not just the *known* stuff like ES6 but the *likely* stuff beyond.

Since ES6 is nearly complete at the time of this writing, *ES6 & Beyond* starts by dividing up the concrete stuff from the ES6 landscape into several key categories, including new syntax, new data structures (collections), and new processing capabilities and APIs.

## Review
The *YDKJS* series is dedicated to the proposition that all JS developers can and should learn all of the parts of this great language. No person's opinion, no framework's assumptions, and no project's deadline should be the excuse for why you never learn and deeply understand JavaScript.