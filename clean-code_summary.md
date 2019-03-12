# Clean Code

## ToC
- Clean Code
- Meaningful Names
- Functions
- Comments
- Formatting
- Objects and Data Structures
- Error Handling
- Boundaries
- Unit Tests/TDD
- Classes
- Systems
- Emergence
- Concurrency
- Successive Refinement
- JUnit Internals
- Refactoring SerialDate
- Smells and Heuristics

## Foreword
- small things matter
- attentiveness to detail is critical
- practice in the small gains proficiency in the large
- a door not closing tightly dispels the charm of the larger whole
- focus is on quickly bringing product to market
- 80% of work is maintenance - or its avoidance
- think about software engineering like home repairman
- 5S: sort, systematize, shine, standards, self-discipline
- inspect the machines every day and fix parts before they break
- quality is the result of a milliopn selfless acts of care
- be honest, because code is never perfect

## Introduction
- craftmanship: knowledge and work
- knowledge: principles, patterns, practices and heuristics
- work: grid it into your fingers, eyes and gut
- find the relationship between the heuristics and the discrete decisions


###################################################################
## Clean Code

### There Will Be Code
- code represents the details of the requirements
- specifying requirements in such details that a machine can execute them is 
programming, such a specification is code
- well-specified requirements are as formal as code
- code is really the language in which we ultimately express the requirements

### Bad Code
- bad code can bring companies down
- rushing and anxiety can lead to bad code
- Leblanc's law: later equals never

### Total Cost of owning a mess
- the degree of slowdown by messy code can be significant
- no change is trivial
- as productivity decreases, more staff gets added
- the new staff isn't into the code, is under pressure and therefore the 
productivity decreases further down

### Grand Redesign in the Sky
- management bends to the demands for a redesign
- now two teams, one creating the new redesign, one maintaining the old
- new team has to build the new system and include the new changes of the old 
system

### Attitude
- we are too unprofessional
- don't be shy about telling what you think about promises and commitments
- it's your job to defend the code with passion
=> be the doctor that washes his hands also it takes up time

### Primal Conundrum
- you won't make the deadline by making the mess, the mess will slow you down
- the only way to go fast is to keep the code as clean as possible at all 
times

### The Art of Clean Code?
- writing clean code requires the disciplined use of many little techniques

### What Is Clean Code?
- elegant: pleasing to read
- efficiency: wasted cycles are inelegant, bad code tempts the mess to grow
=> broken windows theory
- exhibits close attention to detail
- does one thing well
- should read like well-written prose
- should containt only what is necessary, not speculative
- easy for other people to enhance it
- code without tests is not clean
- has been taken care of
- expressive
- does what you pretty much expected

### We Are Authors
- remember you are an author, writing for readers
- we are constantly reading old code as part of writing new code, ~10:1
- if you want to go fast & want your code easy to write, make it easy to read

### The Boy Scout Rule
- the code has to be kept clean over time
- continuous improvement as intrinsic part of professionalism

#############################################################
## Meaningful Names

### Use Intention-Revealing Names
- be really serious about it
- change name when you find a better one
- the name should answer all the big questions
- if a name requires a comment, then the name does not reveal its intent
- why does it exist? what does it do? how it is used?
- what is being measured, the unit of that measurement
- `int elapsedTimeInDays`, `int daysSinceCreation`, `int fileAgeInDays`

### Avoid Disinformation
- avoid words whose meanings vary from our intended meaning
- `accountList`: `list` is something specific to a programmer, is it a list?
- beware of using names which vary only in small ways: `ABCD` vs. `ABDC`

### Make Meaningful Distinctions
- don't use number series (`a1`, `a2`)
- don't use noise words (`ProductInfo` vs. `ProductData`, `Money` vs. 
`MoneyAmount`)

### Use Pronounceable Names
- we speak about code
- `genymdhms` vs. `generationTimestamp`

### User Searchable Names
- `e` will likely show up in every line of code when searching
- longer names trump shorter names
- the length of a name should correspond to the size of its scope (bigger 
scope => longer name)

### Avoid Encodings
- encoding type or scope information into names adds an extra mental burden
- `phoneString`, `moneyNumber`
- don't prefix member variables

### Avoid Mental Mapping
- readers shouldn't have to mentally translate your names into other names
- a single-letter name in a loop has to be mentally mapped to the actual 
concept

### Class and Object Names
- yes: a noun or noun phrase like `Customer`, `Account`
- no: a verb
- no: something noisy like `Data`, `Info`

### Method Names
- yes: a verb or verb phrase like `deletePage`, `saveCustomer`
- yes: prefixes like `get`, `set`, `is` for accessors, mutators and predicates

### Don't Be Cute
- clarity over entertainment
- `DeleteItem` vs. `HolyHandGrenade`
- say what you mean
- everyone should understand it

### Pick One Word per Concept
- pick one word for one abstract concept
- `fetch`, `get`, `retrieve` => choose one and use it everywhere
- `delete`, `remove`, `splice` => choose one and use it everywhere

### Don't Pun
- avoid using the same word for two purposes
- if the semantics are different, use another word
- `add` vs. `append`

### Use Solution Domain Names
- people who read your code are programmers, so use CS terms
- we don't want our co-worker to have to run to the customer asking what a name 
means

### Use Problem Domain Names
- when there is no CS term, use one from the problem domain
- separating solution and problem domain concepts is part of the job
- code that has more to do with problem domain concepts should have names from 
the problem domain

### Add Meaningful Context
- most names are not meaningful in and of themselves
- instead you need to place them in context by enclosing them in well-named 
classes, functions, namespaces
- `street`, `houseNumber`, `zipcode`, `city`, `state` => `state` is meaningful 
in the context

### Don't Add Gratuitous Context
- add no more context to a name than is necessary
- shorter names are generally better, so long as they are clearer

### Final Words
- the hardest thing about choosing a good name is that it requires very good 
descriptive skills and a shared cultural background
- change names, if they are better

#########################################################
## Functions
- functions are the first line of organization 
- "functions should do one thing. they should do it well. they should do it 
only."

### Small!
- make them small, even smaller
- hardly ever 20 lines, better max. 3 or 4
- each should tell a story
- blocks within if/else statements should be one line long, probably a function 
call, keeping the enclosing function small and adding documentary value
- indent level should not be greater than one or two

### Do One Thing
- one thing = one level of abstraction
- the reason to write functions is to decompose a larger concept into a set of 
steps at the next level of abstraction
- if you can extract another function from it with a name that is not merely a 
restatement of its implementation, it is doing more than one thing

### One Level of Abstraction per Function 
- make sure that the statements within a function are all at the same level of 
abstraction
- mixing levels of abstraction within a function is always confusing
- the code should read like a top-down narrative, we want every function to be 
followed by those at the next level of abstraction => TO paragraphs: "To do x, 
we do y" (one level of abstraction deeper)

### Switch Statements
- try to make each switch statement buried in a low-level class and never 
repeated, by using polymorphism
- can be tolerated if they appear only once, are used to create polymorphic 
objects and are hidden behind an inheritance relationship so that the rest 
can't see them

### Use Descriptive Names
- the name describes what the function does
- each routine should do what you expect it to do
- a long descriptive name is better than a short enigmatic
- hunting for a good name can result in a favorable restructuring of the code
- be consistent in your names, use the same phrases, nouns, verbs
- `includeSetupPage`, `includeSuiteSetupPage`, `includeTeardownPage`

### Function Arguments
- the ideal number of arguments is 0, next comes 1 (monadic)
- arguments are even harder from a testing standpoint, testing various 
combinations of arguments is hard
- common monadic forms: asking a question about it (does it exist?), 
transforming and returning it
- flag arguments: passing a boolean into a function is terrible practice
- dyadic: problems like ordering =>try to convert them into monads
- triadic: be very careful
- more than 2 or 3 arguments: wrap them into an object, this concept should 
deserve an own name
- verbs and keywords: a monad should form a nice verb/noun pair, e.g. 
`writeField(name)` (the name is written and name is a field), so we know what 
the argument is

### Have No Side Effects
- side effects are lies: your function promises to do one thing, but also does 
other hidden things
- temporal coupling: if you must have it, make it clear in the function name 
(function still doing only one thing?)
- outputa arguments: input or output? `appendFooter(s)` => does it append `s` 
as the footer to something? or does it append some footer to `s`?

### Command Query Separation
- function should either do something or answer something, never both
- `public boolean set(String attribute, String value)` => do something 
(setting) and answering something (return value boolean)
- `if (set("username", "bob"))`: check if previously set (adjective) or 
if attribute successfully set (verb)? => confusion
=> separate the command from the query

### Prefer Exceptions to Returning Error Codes
- use exceptions instead of returned error codes
- extract the bodies of the try and catch blocks into functions on their own
- a function that handles errors should also do nothing else

### Don't Repeat Yourself
- duplication is a problem, root of all evil
- it bloats the code and will require x-fold modification

### Structured Programming 
- in large functions, every function and every block within should have one 
entry and one exit
=> one return statement, no break or continue in a loop, and never any goto

### How Do You Write Functions Like This?
- first draft might be clumsy and disorganized, so restructure and refine it 
until it reads the way you want it to read

### Conclusion
- think of systems as stories to be told rather than programs to be written
- never forget that your real goal is to tell the story of the system and that 
the functions you write need to fit cleanly together into a clear and precise 
language that help you with that telling
- functions are the verbs
- classes are the nouns

#######################################################
## Comments

- don't comment bad code - rewrite it
- comments are, at best, a necessary evil
- comments compensate for our failure to express ourself in code
- when you find yourself writing a comment, see whether there is a way to 
express yourself in code
- inaccurate comments are far worse than no comments

### Comments Do Not Make Up for Bad Code
- clear and expressive code with few comments is far superior to cluttered and 
complex code with lots of comments
- don't write the comments, clean up the mess in the code

### Explain Yourself in Code
- it's simply a matter of creating a function that says the same thing as the 
comment you write

### Good Comments
- some comments are necessary
- legal comment
- informative comment: but better to use the name of the function to convey the 
information
- explanation of intent
- clarification: but better to find a way to make the value clearer in its own 
right
- warning of consequences
- todos
- amplifications
- javadocs in public api

### Bad Comments
- mumbling: any comment that forces you to look in another module for the 
meaning has failed to communicate
- redundant comment: `int processorDelay = 1; // the processor delay for the 
component`
- misleading comment
- mandated comment
- journal comment: nowadays we have git
- noise comment
- position marker
- closing brace comment: try to shorten your function instead
- attribution and bylines: we have git
- commented-out code
- html comment
- nonlocal information
- too much information
- inobvious connection
- function header: use a well-chosen name
- javadocs in nonpublic api
- don't use a comment when you can use a function or variable

#######################################################
## Formatting

### The Purpose of Formatting
- formatting is about communication

### Vertical Formatting
- small files are usually easier to understand than large files
- bigger projects typically 200 lines per file, upper limit 500 lines
- newspaper: many small articles, each with synopsis, details, minutia

#### Vertical Openness between Concepts
- openness separates concepts
- blank lines separate thoughts
- left to read, top to bottom
- each line represents an expression or a clause
- each group of lines represents a complete thought

#### Vertical Density
- density implies close association

#### Vertical Distance
- concepts that are closely related should be kept vertically close to each 
other
- variables should be declared as close to their usage as possible
- control variables for loops should be declared within the loop statement
- instance variables should be declared at the top of the class
- if one function calls another, they should be vertically close and the caller 
should be above the callee
- the stronger the conceptual affinity, the less vertical distance there should 
be between them

#### Vertical Ordering
- we want function call dependencies to point in the downward direction, from 
high to low, as in a newspaper article

### Horizontal Formatting: 
- prefer short lines, ~ upper limit 120 chars
- Horizontal Openness and Density: horizontal white space to associate things that are strongly related
- Horizontal Alignment: look closely what it emphasizes
- Indentation: we indent to make the hierarchy of scope visible

### Team Rules
- a team should agree upon a single formatting style, be consistent
- encode those rules into the code formatter of your IDE
- good software is composed of a set of documents that read nicely

##################################################
## Objects and Data Structures

### Data Abstraction 
- hiding implementation is about abstractions
- a class exposes abstract interfaces that allows its users to manipulate the 
essence of the data, without having to know its implementation
- we do not want to expose the details of our data
- we want to express our data in abstract terms
- serious thought needs to be put into the best way to represent the data that 
an object contains

### Data/Object Anti-Symmetry
- objects hide their data behind abstractions and expose functions that operate 
on that data
- data structures expose their data and have no meaningful functions
- notice the complimentary nature of these two definitions, they are virtual 
opposites, this has far-reaching implications
- fundamental dichotomy between objects and data structures: Procedural code 
makes it hard to add new data structures because all the functions must change. 
OO code makes it hard to add new functions because all the classes must change.
=> the things that are hard for OO are easy for procedures and vice versa
- if we want to add new data types, objects and OO are most appropriate
- if we want to add new functions, data structures and procedural code are 
most appropriate

### The Law of Demeter
- a module should not know about the innards of the objects it manipulates
=> talk to friends, not to strangers
- train wrecks: violations depends on whether objects or data structures
- hybrids: half object, half data structure: doing things & having public 
variables or accessors => hard to add new functions and data structures => 
avoid them

### Data Transfer Objects
- the quintessential form of a data structure is a class with public variables 
and no functions => a data transfer object, DTO
- Bean: private variables manipulated by getters and setters
- Active Record: have also navigational methods like `save` and `find`

### Conclusion
- objects expose behavior and hide data, easy to add new kinds of objects 
without changing existing behavior
- data structures expose data and have no significant behavior, easy to add new 
behavior to existing data structures, but harder to add new data structures to 
existing functions
=> choose the approach that is best for the job at hand

#######################################################
## Error Handling
- input can be abnormal, devices can fail
- important, but if it obscures logic, it's wrong

### Use Exceptions Rather Than Return Codes 
- throw an exception, harder to forget

### Write Your Try-Catch-Finally Statement First
- start with a try-catch-finally statement to help you define what the user of 
that code hould expect 

### Use Unchecked Exceptions
- violates the Open/Closed Principle

### Provide Context with Exceptions
- provide enough contect to determine the source and location of the error
- create informative error messages and pass them along with the exception
- mention the operation that failed and the type of failure

### Define Exception Classes in Terms of a Caller's Needs
- define how they are caught
- wrapping third-party APIs is best practice
- often a single exception class is fine for a particular area of code

### Define the Normal Flow
- Special Case Pattern: create a class or configure an object so that it 
handles a special case for you encapsulated

### Don't Return Null
- consider throwing an exception or returning a Special Case object instead

### Don't Pass Null
- avoid it whenever possible
- forbid passing null by default

###############################################
## Boundaries 

### Using Third-Party Code 
- providers of third-party packages strive for broad applicability
- users want an interface focused on their particular needs
- don't passing interfaces at a boundary around your system
- keep it inside the class or close family of classes, where it is used

### Exploring and Learning Boundaries
- write some tests to explore our understanding of the third-party code
=> learning tests

### Learning log4j
- example
- read docs
- write tests
- google

### Learning Tests Are Better Than Free
- positive return on invest
- when there are new releases, we run the learning tests again to see 
differences

### Using Code That Does Not Exist Yet
- there is a boundary that separates the known from the unknown, where our 
knowledge drops of the edge
- e.g. create an interface and work out the details later
- is under own control, no blocking

### Clean Boundaries
- interesting things happen at boundaries, change is one
- good software design accomodates change without huge investments and rework
- code at boundaries needs clear separation and tests
- it's better to depend on something you control

#############################################
## Unit Tests

### The Three Laws of TDD
- write unit tests first
1. You may not write production code until you have written a failing unit test
2. You may not write more of a unit test than is sufficient to fail, and not 
compiling is failing
3. You may not write more production code than is sufficient to pass the 
currently failing test
- the sheer bulk of those tests can lead to a daunting management problem

### Keeping Tests Clean
- the dirtier the tests, the harder they are to change
- test code is just important as production code
- unit tests keep the code flexible, maintainable and reusable
- if you have tests, you do not fear making changes!
- without tests every change is a possible bug
- the higher your test coverage, the less you fear
- tests enable change

### Clean Tests
- readability, readability, readability
- Build-Operate-Check Pattern: three parts: Build up the test data, Operate on 
that test data, Check that the operation yielded the expected results

### One Assert per Test
- the number of asserts in a test ought to be minimized
- test a single concept in each test function

### FIRST
- Fast: tests should be fast or you won't run them 
- Independent: tests should not depend on each other
- Repeatable: tests should be repeatable in any environment
- Self-Validating: tests should return a boolean, either they pass or fail
- Timely: tests need to be written in a timely fashion, just before the 
production code that makes them pass

#########################################################
## Classes

### Class Organization 
- stepdown rule
- a class should begin with a list of variables: public static constants, 
privat static, private instance
- then public functions
- then private utilities called by a public function
- encapsulation: keep variables and utility functions private

### Classes Should Be Small
- first rule: keep them small
- second rule: keep them smaller than that
- measurement: responsibilites
- the name of a class should describe what responsibilites it fulfills
- if we cannot derive a concise name, then it's likely too large
- brief description in about 25 word, no "if", "and", "or", "but"
- Single Responsibility Principle: a class should have only one reason to 
change
- getting software to work and making software clean are two very different 
activities
- many of us think that we are done once the program works, therefore we fail 
to switch from working code to clean code
- the primary goal in managing complexity is to organize it so that the reader 
knows where to look to find things and only need to understand the directly 
affected complexity at any given time
- cohesion: the more variables a method manipulates, the more cohesive 
that method is; should be high, meaning that the methods and variables are 
co-dependent and hang together as a logical whole
- maintaining high cohesion leads to many small classes
- when a class loses cohesion, split them

### Organizing for Change
- change is continual 
- every change subjects us to the risk of system failure
- we want to reduce this risk by organizing

##########################################################
## Systems

### How Would You Build a City
- cities have teams of people who manage particular parts of the city 
- some people are responsible for the big picture
- some focus on the details
- cities have evolved appropriate levels of abstraction and modularity

### Separate Constructing a System from Using It
- construction is a different process from use 
- separation of concerns is one of the most important design techniques
- the startup process is a concern any application must address
- separation of Main: the main function builds the objects necessary for the 
system, then passes them to the application, which simply uses them
- factory, dependency injection
- Inversion of Control: moves secondary responsibilities from an object to 
other objects that are dedicated to the purpose, thereby supporting SRP 

### Scaling Up
- cities grow from towns, which grow from settlements
- we can get systems right the first time, we should only implement today's 
stories, then refactor => iterative

### Java Proxies
### Pure Java AOP Frameworks
### AspectJ Aspects

### Test Drive the System Architecture
- use POJOs, decoupled from any architecture concerns
- it is not necessary to do a Big Design Up Front

### Optimize Decision Making
- give responsibility to the most qualified person
- make informed choices with the best possible information

### Use Standards Wisely, When They Add Demonstrable Value

### Systems Need Domain-Specific Languages
- a good DSL minimizes the communication gap between a domain concept and the 
code that implements it

################################################
## Emergence

### Simple Design Rule 1: Runs All the Tests
- a design must produce a system that acts as intended 

### Simple Design Rule 2-4: Refactoring
- incrementally refactoring 
- having tests eliminates the fear that cleaning will break the code

### No Duplication
- Template Method Pattern 

### Expressive
- majority of the cost of software is in long-term maintenance
- good names
- small classes and methods
- patterns
- tests

### Minimal CLasses and Methods

###############################################
## Concurrency

### Why Concurrency? 
- a decoupling strategy for what gets done from when it gets done 
- no user wants to wait

### Challenges

### Concurrency Defense Principles
- SRP 
- Limit the scope of data
- Use copies of data
- Threads should be as independent as possible

### Know Your Library
- thread-safe collections

### Know Your Execution Models
- producer-consumer
- readers-writers
- dining philosophers

### Beware Dependencies Between Synchronized Methods 
- avoid using more than one method on a shared object

### Keep Synchronized Sections Small
- keep your synchronized sections small

### Writing Correct Shut-Down Code Is Hard
- think about shut-down early and get it working early

### Testing Threaded Code
- write tests that have the potential to expose problems and run them 
frequently
- treat spurious failures as candidate threading issues
- get your nonthreaded code working first
- make your threaded code pluggable
- make your threaded code tunable
- run with more threads than processors
- run on different platforms
- instrument your code and try and force failures
- hand-coded
- automated

###############################################
## Successive Refinement

###############################################
## JUnit Internals

###############################################
## Refactoring SerialDate

###############################################
## Smells and Heuristics

### Comments 
- inappropriate information: author, date etc. 
- obsolete comment: old, irrelevant or incorrect
- redundant comment: repeats what the code is saying 
- poorly written: grammar, punctuation
- commented-out code: pollutes and creates fear

### Environment
- build requires more than one step 
- tests require more than one step

### Functions
- too many arguments: 0 < 1 < 2 < 3 
- output arguments: counterintuitive, should only be inputs
- flag arguments: do only one thing
- dead function: complexity

### General
- multiple languages in one source file 
- obvious behavior is unimplemented: principle of least surprise, lose of trust
- incorrect behavior at boundaries: don't rely on your intuition, test it
- overridden safeties
- duplication: DRY: abstract it
- code at wrong level of abstraction
- base classes depending on their derivates 
- too much information
- dead code 
- vertical separation
- inconsistency
- clutter
- artificial coupling
- feature envy
- selector arguments
- obscured intent
- misplaced responsibility
- inappropriate static 
- use explanatory variables
- functions names should say what they do
- understand the algorithm
- make logical dependencies physical
- prefer polymorphism to if-else and switch-case
- follow standard conventions 
- replace magic numbers with named constants
- be precise
- structure over convention
- encapsulate conditionals 
- avoid negative conditionals
- functions should do one thing
- hidden temporal couplings
- don't be arbitrary 
- encapsulate boundary conditions
- functions should descend only one level of abstraction
- keep configurable data at high levels
- avoid transitive navigation

### Java
- avoid long import lists by using wildcards 
- don't inherit constants
- constants versus enums

### Names
- choose descriptive names 
- choose names at the appropriate level of abstraction
- use standard nomenclature where possible
- unambigious names
- use long names for long scopes
- avoid encodings
- names should describe side-effects 

### Tests
- insufficient tests 
- use a coverage tool
- don't skip trivial tests
- an ignored test is a question about an ambiguity
- test boundary conditions
- exhaustively test near bugs
- patterns of failure are revealing
- test coverage patterns can be revealing 
- test should be fast











