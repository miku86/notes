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
