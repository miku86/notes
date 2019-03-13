# Test-Driven Development By Example

## Random Thoughts

Another mental picture—programming is like exploring a dark house. You go from room to room to room. Writing the test is like turning on the light. Then you can avoid the furniture and save your shins (the clean design resulting from refactoring). Then you’re ready to explore the next room.

Make it run, make it right, make it fast.

## Preface

Test-Driven Development:

- Don’t write a line of new code unless you first have a failing automated test.
- Eliminate duplication.

Some of the technical implications are:

- You must design organically, with running code providing feedback between decisions
- You must write your own tests, since you can’t wait twenty times a day for someone else to write a test
- Your development environment must provide rapid response to small changes
- Your designs must consist of many highly cohesive, loosely coupled components, just to make testing easy

The two rules imply an order to the tasks of programming:

- Red: write a little test that doesn’t work, perhaps doesn’t even compile at first
- Green: make the test work quickly, committing whatever sins necessary in the
  process
- Refactor: eliminate all the duplication created in just getting the test to work

Red/green/refactor. The TDDs mantra.

It might be possible to dramatically reduce the defect density of code and make the subject of work crystal clear to all involved. If so, writing only code demanded by failing tests also has social implications:

- If the defect density can be reduced enough, QA can shift from reactive to proactive work
- If the number of nasty surprises can be reduced enough, project managers can estimate accurately enough to involve real customers in daily development
- If the topics of technical conversations can be made clear enough, programmers can work in minute-by-minute collaboration instead of daily or weekly collaboration
- Again, if the defect density can be reduced enough, we can have shippable software with new functionality every day, leading to new business relationships with customers

So, the concept is simple, but why would a programmer take on the additional work of writing automated tests? Why would a programmer work in tiny little steps when their mind is capable of great soaring swoops of design? Fear.

## Fear

TDD is a way of managing fear during programming. I mean fear in the legitimate, this-is-a-hard-problem-and-I-can’t-see-the-end-from-the-beginning sense. If pain is nature’s way of saying “Stop!”, fear is nature’s way of saying “Be careful.”

The problem is that fear has a host of other effects:

- Makes you tentative
- Makes you want to communicate less
- Makes you shy from feedback
- Makes you grumpy

None of these effects are helpful when programming, especially when programming something hard. So, how can you face a difficult situation and:

- Instead of being tentative, begin learning concretely as quickly as possible.
- Instead of clamming up, communicate more clearly.
- Instead of avoiding feedback, search out helpful, concrete feedback.
- (You’ll have to work on grumpiness on your own.)

Imagine programming as turning a crank to pull a bucket of water from a well. When the bucket is small, a free- spinning crank is fine. When the bucket is big and full of water, you’re going to get tired before the bucket is all the way up. You need a ratchet mechanism to enable you to rest between bouts of cranking. The heavier the bucket, the closer the teeth need to be on the ratchet. The tests in test-driven development are the teeth of the ratchet. Once you get one test working, you know it is working, now and forever. You are one step closer to having everything working than you were when the test was broken. Now get the next one working, and the next, and the next. By analogy, the tougher the programming problem, the less ground should be covered by each test. TDD is an awareness of the gap between decision and feedback during programming, and control over that gap. You could have only application-level tests and be doing TDD. The gap between decision and feedback would be large — days, even —but for extremely skilled programmers that might be enough feedback. TDD gives you control over feedback. When you are cruising along in overdrive and the snow begins to fall, you can shift into 4WD Low and keep making progress. When the road clears, you can up shift and away you go.

That said, most people who learn TDD find their programming practice changed for good. “Test Infected” is the phrase Erich Gamma coined to describe this shift. You might find yourself writing more tests earlier, and working in smaller steps than you ever dreamed would be sensible. On the other hand, some programmers learn TDD and go back to their earlier practices, reserving TDD for special occasions when ordinary programming isn’t making progress. There are certainly programming tasks that can’t be driven primarily by tests (or at least, not yet).

Once you are finished reading this book, you should be ready to:

- Start simply
- Write automated tests
- Refactor to add design decisions one at a time

This book is organized into three sections.

1. An example of writing typical model code using TDD. In it you will learn to write tests before code, grow a design organically, and fail with grace.
2. An example of testing more complicated logic, including reflection and exceptions, by developing a framework for automated testing. In the second example you will learn to work in even smaller steps than in the first example, including the kind of self-referential hooha beloved of computer scientists.
3. Patterns for TDD. Included are patterns for the deciding what tests to write, how to write tests, and a greatest hits selection of the design patterns and refactorings used in the examples.

########################################################

## Section 1: Money Example

In this section we will develop typical model code completely driven by tests.

My goal is for you to see the rhythm of test-driven development:

1. Quickly add a test
2. Run all tests and see the new one fail
3. Make a little change
4. Run all tests and see them all succeed
5. Refactor to remove duplication

The surprises are likely to be:

- How each test can cover a small increment of functionality
- How small and ugly the changes can be to make the new tests run
- How often the tests are run
- How many teensy tiny steps make up the refactorings

## Money Example

What is the set of tests which, when passed, will demonstrate the presence of code we are confident will compute the report correctly?

- We need to be able to add amounts in two different currencies and convert the result given a set of exchange rates.
- We need to be able to multiply an amount (price per share) by a number (number of shares) and receive an amount.

We’ll make a to-do list to remind us what all we need to do, keep us focused, and tell us when we are finished:

To do:

- $5 * 2 = $10
- $5 + 10 CHF = $10 if CHF:USD is 2:1

What object do we need first? Trick question. We don’t start with objects, we start with tests. Try again. What test do we need first? Start small or not at all. Multiplication, how hard could that be? We’ll work on that first. When we write a test, we imagine the perfect interface for our operation. We are telling ourselves a story about how the operation will look from the outside. Our story won’t always come true, but better to start from the best possible API and work backwards than to make things complicated, ugly, and “realistic” from the get go.

Here’s a simple example of multiplication:

```java
public void testMultiplication() {
  Dollar five= new Dollar(5);
  five.times(2);
  assertEquals(10, five.amount);
}
```

We have a failing test and we want it to go green as quickly as possible.
The test we just typed in (I’ll explain where and how we type it in later) doesn’t even compile. That’s easy enough to fix. What’s the least we can do to get it to compile, even if it doesn’t run? We have four compile errors:

- No class “Dollar”
- No constructor
- No method “times(int)”
- No field “amount”

Let’s take them one at a time.

We can get rid of one error by defining the class Dollar:

`class Dollar`

Now we need the constructor, but it doesn’t have to do anything just to get the test to compile:

`Dollar(int amount) {}`

We need a stub implementation of times(). Again we’ll do the least work possible just to get the test to compile:

`void times(int multiplier) {}`

Finally, we need an amount field:

`int amount;`

Now we can run the test and watch it fail.

You are seeing the dreaded red bar. Our testing framework has run the little snippet of code we started with, and noticed that although we expected “10” as a result, we saw “0”. Sadness. No, no. Failure is progress. Now we have a concrete measure of failure. That’s better than just vaguely knowing we are failing. Our programming problem has been transformed from “give me multi-currency” to “make this test work, and then make the rest of the tests work.” Much simpler. Much smaller scope for fear. We can make this test work.

You probably aren’t going to like the solution, but the goal right now is not to get the perfect answer, the goal is to pass the test. We’ll make our sacrifice at the altar of truth and beauty later.

Here’s the smallest change I could imagine that would cause our test to pass:

`int amount= 10;`

Now we get the green bar, fabled in song and story.

Oh joy, oh rapture! Not so fast. The cycle isn’t complete. There are very few inputs in the world that will cause such a limited, such a smelly, such a naïve implementation to pass.

We need to generalize before we move on. Remember, the cycle is:

1. Add a little test
2. Run all tests and fail
3. Make a little change
4. Run the tests and succeed
5. Refactor to remove duplication

But where is the duplication? Usually you see duplication between two pieces of code.
Here the duplication is between the data in the test and the data in the code. Don’t see
it? How about if we write?

`int amount= 5 * 2;`

That “10” had to come from somewhere. We did the multiplication in our heads so
fast we didn’t even notice. The “5” and “2” are now in two places, and we must
ruthlessly eliminate duplication before moving on.

There isn’t a single step that will eliminate the 5 and 2. However, what if we move the setting of the amount from object initialization to the times() method?

```java
int amount;
void times(int multiplier) {
  amount= 5 * 2;
}
```

The test still passes, the bar stays green. Happiness is still ours.

Defensiveness aside, where were we? Ah, yes, we were getting rid of duplication
between the test code and the working code. Where can we get a 5? That was the
value passed to the constructor, so if we save it in the amount variable:

```java
Dollar(int amount) {
  this.amount= amount;
}
```

we can use it in times():

```java
  void times(int multiplier) {
amount= amount * 2;
}
```

The value of the parameter “multiplier” is 2, so we can substitute the parameter for the constant:

```java
void times(int multiplier) {
  amount= amount * multiplier;
}
```

To demonstrate our thorough-going knowledge of Java syntax, we will want to use the “\*=” operator (which does, it must be said, reduce duplication):

```java
void times(int multiplier) {
  amount *= multiplier;
}
```

We can now mark off the first test as done.

## Degenerate Objects

We got one test working, but in the process we noticed something strange—when we
perform an operation on a Dollar, the Dollar changes.

Our guesses about the right interface are no more likely to be perfect than our guesses about the right implementation.

```java
public void testMultiplication() {
  Dollar five= new Dollar(5);
  Dollar product= five.times(2);
  assertEquals(10, product.amount);
  product= five.times(3);
  assertEquals(15, product.amount);
}
```

The new test won’t compile until we change the declaration of Dollar.times():

```java
Dollar times(int multiplier) {
  amount *= multiplier;
  return null;
}
```

Now the test compiles, but it doesn’t run. Progress! Making it run requires that we return a new Dollar with the correct amount:

```
Dollar times(int multiplier) {
  return new Dollar(amount * multiplier);
}
```

These are two of the three strategies for quickly getting to green:

- Fake It — return a constant and gradually replace constants with variables until you have the real code
- Obvious Implementation — type in the real implementation

When I use TDD in practice, I commonly shift between these two modes of implementation. When everything is going smoothly and I know what to type, I put in obvious implementation after obvious implementation (running the tests all the time to ensure that what’s obvious to me is still obvious to the computer). As soon as I get an unexpected red bar, I back up, shift to faking implementations, and refactor to the right code. When my confidence is back, I go back to obvious implementations. There is a third style of driving development, triangulation, which we will demonstrate in the next chapter. However, to review, we:

- Translated a design objection (side effects) into a test case that failed because of the objection
- Got the code to compile quickly with a stub implementation
- Made the test work by typing in what seemed like the right code

The translation of a feeling (disgust at side effects) into a test (multiply the same Dollar twice) is a common theme of TDD. The longer I do this, the better able I am to translate my aesthetic judgements into tests. When I can do this, my design discussions become much more interesting. First we can talk about whether the system should work like this or like that. Once we decide on the correct behavior, we can talk about the best way of achieving that behavior. We can speculate about truth and beauty all we want over beers, but while we are programming we can leave airy-fairy discussions behind and talk cases.

## Equality for All

If I have an integer and I add 1 to it, I don’t expect the original integer to change, I expect to use the new value. Objects usually don’t behave that way. If I have a Contract and I add one to its coverage, the Contract’s coverage should change.

We can use objects as values, as we are using our Dollar now. The pattern for this is Value Object. One of the constraints on Value Objects is that the values of the instance variables of the object never change once they have been set in the constructor.

There is one huge advantage to using value objects—you don’t have to worry about aliasing problems. Say I have one Check and I set its amount to $5, and then I set another Check’s amount to the same $5. Some of the nastiest bugs in my career have come when changing the first Check’s value inadvertently changed the second Check’s value. This is aliasing.

When you have value objects, you don’t have to worry about aliasing. If I have $5, I am guaranteed that it will always and forever be $5. If someone wants \$7, they have to make an entirely new object.

One implication of Value Object is all operations must return a new object, as we saw in the previous chapter. Another implication is that value objects should implement equals(), since one \$5 is pretty much as good as another.

## Privacy

Now that we have defined equality, we can use it to make out tests more “speaking”. Conceptually, the operation Dollar.times() should return a Dollar whose value is the value of the receiver times the multiplier. Our test doesn’t exactly say that:

```java
public void testMultiplication() {
  Dollar five= new Dollar(5);
  Dollar product= five.times(2);
  assertEquals(10, product.amount);
  product= five.times(3);
  assertEquals(15, product.amount);
}`
```

We can rewrite the first assertion to compare Dollars to Dollars. That looks better, so we rewrite the second assertion, too. Now the temporary variable “product” isn’t helping much, so we can inline it:

```java
public void testMultiplication() {
  Dollar five= new Dollar(5);
  assertEquals(new Dollar(10), five.times(2));
  assertEquals(new Dollar(15), five.times(3));
}
```

This test speaks to us more clearly, as if it were an assertion of truth, not a sequence of operations. With these changes to the test, Dollar is now the only class using its “amount” instance variable, so we can make it private:

`private int amount;`

And we can cross another item off the list.

## Franc-ly Speaking

How are we going to approach the first test on that list?

`$5 + 10 CHF = $10 if CHF:USD is 2:1`

That’s the test that’s most interesting. It still seems to be a big leap. I’m not sure I can write a test that I can implement in one little step. A pre-requisite seems to be having an object like Dollar, but to represent Francs. If we can get Francs working like Dollars work now, we’ll be closer to being able to write and run the mixed addition test.

We can copy and edit the Dollar test:

```java
public void testFrancMultiplication() {
  Franc five= new Franc(5);
  assertEquals(new Franc(10), five.times(2));
  assertEquals(new Franc(15), five.times(3));
}
```

What short step will get us to a green bar? Copying the Dollar code and replacing
“Dollar” with “Franc”. Stop. Hold on. I can hear the aesthetically inclined among you sneering and spitting. Copy and paste reuse? The death of abstraction? The killer of clean design? If you’re upset, take a cleansing breath. Now, our cycle has different phases:

1. Write a test
2. Make it compile
3. Make it run
4. Remove duplication

The different phases have different purposes. They call for different styles of solution, different aesthetic viewpoints.

The first three phases need to go by quickly, so we get to a known state with the new functionality. You can commit any number of sins to get there, because speed trumps design, just for that brief moment. Now I’m worried. I’ve given you a license to abandon all the principles of good design. Halt. The cycle is not complete.

The first three steps of the cycle won’t work without the fourth. Good design at good times. Make it run, make it right. There, I feel better. Now I’m sure you won’t show anyone except your partner your code until you’ve removed the duplication. Where were we? Ah, yes. Violating all the tenets of good design in the interest of speed.

```java
class Franc {
  private int amount;
  Franc(int amount) {
    this.amount= amount;
  }
  Franc times(int multiplier) {
    return new Franc(amount * multiplier);
  }
  public boolean equals(Object object) {
    Franc franc= (Franc) object;
    return amount == franc.amount;
  }
}
```

Because the step to running code was so short, we were even able to skip the “make it compile” step. Now we have duplication galore, and we have to eliminate it before writing our next test. We’ll start by generalizing equals(). However, we can cross off an item, even though we have to add two more:

Reviewing, we:
· Couldn’t tackle a big test, so we invented a small test that represented progress
· Wrote the test by shamelessly duplicating and editing
· Even worse, made the test work by copying and editing model code wholesale
· Promised ourselves we wouldn’t go home until the duplication was gone
