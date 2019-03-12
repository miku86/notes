# Test-Driven Development By Example

## Random Thoughts

Another mental picture—programming is like exploring a dark house. You go from room to room to room. Writing the test is like turning on the light. Then you can avoid the furniture and save your shins (the clean design resulting from refactoring). Then you’re ready to explore the next room.

Make it run, make it right, make it fast.

## Preface

Test-Driven Development:
· Don’t write a line of new code unless you first have a failing automated test.
· Eliminate duplication.

Some of the technical implications are:
· You must design organically, with running code providing feedback between decisions
· You must write your own tests, since you can’t wait twenty times a day for someone else to write a test
· Your development environment must provide rapid response to small changes
· Your designs must consist of many highly cohesive, loosely coupled components, just to make testing easy

The two rules imply an order to the tasks of programming:
· Red: write a little test that doesn’t work, perhaps doesn’t even compile at first
· Green: make the test work quickly, committing whatever sins necessary in the
process
· Refactor: eliminate all the duplication created in just getting the test to work

Red/green/refactor. The TDDs mantra.

It might be possible to dramatically reduce the defect density of code and make the subject of work crystal clear to all involved. If so, writing only code demanded by failing tests also has social implications:
· If the defect density can be reduced enough, QA can shift from reactive to proactive work
· If the number of nasty surprises can be reduced enough, project managers can estimate accurately enough to involve real customers in daily development
· If the topics of technical conversations can be made clear enough, programmers can work in minute-by-minute collaboration instead of daily or weekly collaboration
· Again, if the defect density can be reduced enough, we can have shippable software with new functionality every day, leading to new business relationships with customers

So, the concept is simple, but why would a programmer take on the additional work of writing automated tests? Why would a programmer work in tiny little steps when their mind is capable of great soaring swoops of design? Fear.

## Fear

TDD is a way of managing fear during programming. I mean fear in the legitimate, this-is-a-hard-problem-and-I-can’t-see-the-end-from-the-beginning sense. If pain is nature’s way of saying “Stop!”, fear is nature’s way of saying “Be careful.”

The problem is that fear has a host of other effects:
· Makes you tentative
· Makes you want to communicate less
· Makes you shy from feedback
· Makes you grumpy

None of these effects are helpful when programming, especially when programming something hard. So, how can you face a difficult situation and:
· Instead of being tentative, begin learning concretely as quickly as possible.
· Instead of clamming up, communicate more clearly.
· Instead of avoiding feedback, search out helpful, concrete feedback.
· (You’ll have to work on grumpiness on your own.)

Imagine programming as turning a crank to pull a bucket of water from a well. When the bucket is small, a free- spinning crank is fine. When the bucket is big and full of water, you’re going to get tired before the bucket is all the way up. You need a ratchet mechanism to enable you to rest between bouts of cranking. The heavier the bucket, the closer the teeth need to be on the ratchet. The tests in test-driven development are the teeth of the ratchet. Once you get one test working, you know it is working, now and forever. You are one step closer to having everything working than you were when the test was broken. Now get the next one working, and the next, and the next. By analogy, the tougher the programming problem, the less ground should be covered by each test. TDD is an awareness of the gap between decision and feedback during programming, and control over that gap. You could have only application-level tests and be doing TDD. The gap between decision and feedback would be large — days, even —but for extremely skilled programmers that might be enough feedback. TDD gives you control over feedback. When you are cruising along in overdrive and the snow begins to fall, you can shift into 4WD Low and keep making progress. When the road clears, you can up shift and away you go.

That said, most people who learn TDD find their programming practice changed for good. “Test Infected” is the phrase Erich Gamma coined to describe this shift. You might find yourself writing more tests earlier, and working in smaller steps than you ever dreamed would be sensible. On the other hand, some programmers learn TDD and go back to their earlier practices, reserving TDD for special occasions when ordinary programming isn’t making progress. There are certainly programming tasks that can’t be driven primarily by tests (or at least, not yet).

Once you are finished reading this book, you should be ready to:
· Start simply
· Write automated tests
· Refactor to add design decisions one at a time

This book is organized into three sections.

1. An example of writing typical model code using TDD. In it you will learn to write tests before code, grow a design organically, and fail with grace.
2. An example of testing more complicated logic, including reflection and exceptions, by developing a framework for automated testing. In the second example you will learn to work in even smaller steps than in the first example, including the kind of self-referential hooha beloved of computer scientists.
3. Patterns for TDD. Included are patterns for the deciding what tests to write, how to write tests, and a greatest hits selection of the design patterns and refactorings used in the examples.
