# Summary: Clean Coder

- What is a software professional?
- How does a professional behave?
- How does a professional deal with conflict, tight schedules and unreasonable managers?
- When and how should a professional say "no"?
- How does a professional deal with pressure?

---

## Professionalism

### Be Careful What You Ask For

Professionalism is a badge of honor and pride, but it is also a marker of responsibility and accountability. The two go hand in hand. You can’t take pride and honor in something that you can’t be held accountable for. If a nonprofessional makes an error, the employer cleans up the mess. When a professional makes a mistake, he cleans up the mess. The nonprofessional would shrug his shoulders, say “stuff happens,”. The professional would write the company a check for \$10,000! Yeah, it feels a little different when it’s your own money. But that feeling is the feeling a professional has all the time. That feeling is the essence of professionalism. Because, you see, professionalism is all about taking responsibility.

### Taking Responsibility

Shipping without testing the routine is irresponsible. I had not been concerned about the customer, nor about my employer. I had only been concerned about my own reputation. I should have taken responsibility early and told Tom that the tests weren’t complete and that I was not prepared to ship the software on time. That would have been hard, and Tom would have been upset. But no customers would have lost data, and no service managers would have called.

### First, Do No Harm

Do No Harm to Function: We want our software to work. But we aren’t the only ones who want the software to work. Our customers and employers want it to work too. They are paying us to create software that works just the way they want it to. We harm the function of our software when we create bugs. The fact that the task to write perfect software is virtually impossible does not mean you aren’t responsible for the imperfection. It is the lot of a professional to be accountable for errors even though errors are virtually certain. So the first thing you must practice is apologizing. Apologies are necessary, but insufficient. You cannot simply keep making the same errors over and over. As you mature in your profession, your error rate should rapidly decrease towards the asymptote of zero. It won’t ever get to zero, but it is your responsibility to get as close as possible.

QA Should Find Nothing: It is unprofessional in the extreme to purposely send code that you know to be faulty to QA. And what code do you know to be faulty? Any code you aren’t certain about! Some folks use QA as the bug catchers. They send them code that they haven’t thoroughly checked. Never mind that this is a desperately expensive behavior that damages the company and the software. Never mind that this behavior ruins schedules and undermines the confidence of the enterprise in the development team. Never mind that this behavior is just plain lazy and irresponsible. Releasing code to QA that you don’t know works is unprofessional. Will QA find bugs? Probably, so get ready to apologize — and then figure out why those bugs managed to escape your notice and do something to prevent it from happening again. Every time QA, or worse a user, finds a problem, you should be surprised, chagrined, and determined to prevent it from happening again.

You Must Know It Works: How can you know your code works? That’s easy. Test it. Test it again. Perhaps you are concerned that testing your code so much will take too much time. After all you’ve got schedules and deadlines to keep. So, automate your tests. Write unit tests that you can execute on a moment’s notice, and run those tests as often as you can. How much of the code should be tested with these automated unit tests? All of it! Am I suggesting 100% test coverage? I’m demanding it. Every single line of code that you write should be tested. You only write code because you expect it to get executed. If you expect it to get executed, you ought to know that it works. The only way to know this is to test it. But isn’t some code hard to test? Yes, but only because that code has been designed to be hard to test. The solution to that is to design your code to be easy to test. And the best way to do that is to write your tests first, before you write the code that passes them. This is a discipline known as Test Driven Development (TDD).

Automated QA: The entire QA procedure is the execution of the unit and acceptance tests. If those tests pass, I ship. This means my QA procedure takes about three minutes, and I can execute it on a whim. You as a developer need a relatively quick and reliable mechanism to know that the code you have written works and does not interfere with the rest of the system. So, at the very least, your automated tests should tell you that the system is very likely to pass QA.

Do No Harm To Structure: The true professional knows that delivering function at the expense of structure is a fool’s errand. If you compromise the structure, you compromise the future. The fundamental assumption underlying all software projects is that software is easy to change. In short: You must be able to make changes without exorbitant costs. Unfortunately, all too many projects become mired in a tar pit of poor structure. Tasks that used to take days begin to take weeks, and then months. Management, desperate to recapture lost momentum, hires more developers to speed things up. Much has been written about the principles and patterns of software design that support structures that are flexible and maintainable. Professional software developers commit these things to memory and strive to conform their software to them. But there’s a trick to this that far too few software developers follow: The only way to prove that your software is easy to change is to make easy changes to it. And when you find that the changes aren’t as easy as you thought, you refine the design so that the next change is easier. When do you make these easy changes? All the time! Every time you look at a module you make small, lightweight changes to it to improve its structure. Every time you read through the code you adjust the structure. I call it “the Boy Scout rule”: Always check in a module cleaner than when you checked it out. Always make some random act of kindness to the code whenever you see it. This is completely counter to the way most people think about software. They think that making a continuous series of changes to working software is dangerous. No! What is dangerous is allowing the software to remain static. If you aren’t flexing it, then when you do need to change it, you’ll find it rigid. Why do most developers fear to make continuous changes to their code? They are afraid they’ll break it! Why are they afraid they’ll break it? Because they don’t have tests. It all comes back to the tests. If you have an automated suite of tests that covers virtually 100% of the code, and if that suite of tests can be executed quickly on a whim, then you simply will not be afraid to change the code. How do you prove you are not afraid to change the code? You change it all the time. Professional developers are so certain of their code and tests that they are maddeningly casual about making random, opportunistic changes. In short, they treat software the way a sculptor treats clay - they continuously shape and mold it.

### Work Ethic

Your career is your responsibility. It is not your employer’s responsibility to make sure you are marketable. It is not your employer’s responsibility to train you, or to send you to conferences, or to buy you books. If your employer doesn’t do these things for you, you should find a way to do them yourself. It is also not your employer’s responsibility to give you the time you need to learn. Some employers may provide that time. They are doing you a favor, and you should be appropriately appreciative. You owe your employer a certain amount of time and effort. You should plan on working 60 hours per week. The first 40 are for your employer. The remaining 20 are for you. During this remaining 20 hours you should be reading, practicing, learning, and otherwise enhancing your career. Do the math. In a week there are 168 hours. Give your employer 40, and your career another 20. That leaves 108. Another 56 for sleep leaves 52 for everything else. Perhaps you don’t want to make that kind of commitment. That’s fine, but you should not then think of yourself as a professional. Professionals spend time caring for their profession. Perhaps you think that work should stay at work and that you shouldn’t bring it home. I agree! You should not be working for your employer during those 20 hours. Instead, you should be working on your career. Sometimes these two are aligned with each other. Sometimes the work you do for your employer is greatly beneficial to your career. In that case, spending some of that 20 hours on it is reasonable. But remember, those 20 hours are for you. They are to be used to make yourself more valuable as a professional. Perhaps you think this is a recipe for burnout. On the contrary, it is a recipe to avoid burnout. Presumably you became a software developer because you are passionate about software and your desire to be a professional is motivated by that passion.

Know Your Field: A wealth of ideas, disciplines, techniques, tools, and terminologies decorate the last fifty years of our field. If you want to be a professional, you should know a sizable chunk of it and constantly be increasing the size of that chunk. Why should you know these things? After all, isn’t our field progressing so rapidly that all these old ideas have become irrelevant? Certainly our field is progressing and at a ferocious pace. Interestingly enough, however, that progress is in many respects peripheral. We are writing the same if and while statements that we were writing 50 years ago. Much has changed. Much has not. Very few ideas of the past 50 years have become irrelevant. Some have been sidelined, it’s true. But that doesn’t mean we shouldn’t know what it is, and what its good and bad points are. Overall, however, the vast majority of the hard-won ideas of the last 50 years are as valuable today as they were then. Perhaps they are even more valuable now.

Here is a minimal list of the things that every software professional should be conversant with:
• Design patterns. You ought to be able to describe all 24 patterns in the GOF book and have a working knowledge of many of the patterns in the POSA books.
• Design principles. You should know the SOLID principles and have a good understanding of the component principles.
• Methods. You should understand XP, Scrum, Lean, Kanban, Waterfall, Structured Analysis, and Structured Design.
• Disciplines. You should practice TDD, Object-Oriented design, Structured Programming, Continuous Integration, and Pair Programming.
• Artifacts: You should know how to use: UML, DFDs, Structure Charts, Petri Nets, State Transition Diagrams and Tables, flow charts, and decision tables

Continious Learning: The frenetic rate of change in our industry means that software developers must continue to learn copious quantities just to keep up. Woe to the programmers who stop learning new languages - they will watch as the industry passes them by. Woe to the developers who fail to learn new disciplines and techniques - their peers will excel as they decline. Would you hire a tax lawyer who did not keep current with the tax laws? Why should employers hire developers who don’t keep current? Read books, articles, blogs, tweets. Go to conferences. Go to user groups. Learn things that are outside your comfort zone. If you are a .NET programmer, learn Java. If you are a Java programmer, learn Ruby. If you are a C programmer, learn Lisp.

Practice: Professionals practice. True professionals work hard to keep their skills sharp and ready. It is not enough to simply do your daily job and call that practice. Doing your daily job is performance, not practice. Practice is when you specifically exercise your skills outside of the performance of your job for the sole purpose of refining and enhancing those skills. What could it possibly mean for a software developer to practice? Consider how musicians master their craft. It’s not by performing. It’s by practicing. Among other things, they have special exercises that they perform. They do these over and over to train their fingers and their mind, and to maintain mastery of their skill. So what could software developers do to practice? One technique I use frequently is the repetition of simple exercises such as the Bowling Game or Prime Factors. I call these exercises kata. A kata usually comes in the form of a simple programming problem to solve, such as writing the function that calculates the prime factors of an integer. The point of doing the kata is not to figure out how to solve the problem; you know how to do that already. The point of the kata is to train your fingers and your brain. I’ll do a kata or two every day, often as part of settling in to work. I might do it in Java, or in Ruby, or in Clojure, or in some other language for which I want to maintain my skills. Think of the kata as a 10-minute warm-up exercise in the morning and a 10-minute cool-down in the evening.

Collaboration: The second best way to learn is to collaborate with other people. Professional software developers make a special effort to program together, practice together, design and plan together. By doing so they learn a lot from each other, and they get more done faster with fewer errors. This doesn’t mean you have to spend 100% of your time working with others. Alone time is also very important. As much as I like to pair program with others, it makes me crazy if I can’t get away by myself from time to time.

Mentoring: The best way to learn is to teach. Nothing will drive facts and values into your head faster and harder than having to communicate them to people you are responsible for. So the benefit of teaching is strongly in favor of the teacher. By the same token, there is no better way to bring new people into an organization than to sit down with them and show them the ropes. Professionals take personal responsibility for mentoring juniors. They will not let a junior flail about unsupervised.

Know Your Domain: It is the responsibility of every software professional to understand the domain of the solutions they are programming. If you are writing an accounting system, you should know the accounting field. If you are writing a travel application, you should know the travel industry. You don’t have to be a domain expert, but there is a reasonable amount of due diligence that you ought to engage in. When starting a project in a new domain, read a book or two on the topic. Spend some time with the experts, and try to understand their principles and values. It is the worst kind of unprofessional behavior to simply code from a spec without understanding why that spec makes sense to the business. Rather, you should know enough about the domain to be able to recognize and challenge specification errors.

Identify With Your Employer/Customer: Your employer’s problems are your problems. You need to understand what those problems are and work toward the best solutions. As you develop a system you need to put yourself in your employer’s shoes and make sure that the features you are developing are really going to address your employer’s needs. It is easy for developers to identify with each other. It’s easy to fall into an us versus them attitude with your employer. Professionals avoid this at all costs.

Humility: Programming is an act of creation. When we write code we are creating something out of nothing. We are boldly imposing order upon chaos. We are confidently commanding, in precise detail, the behaviors of a machine that could otherwise do incalculable damage. And so, programming is an act of supreme arrogance. Professionals know they are arrogant and are not falsely humble. A professional knows his job and takes pride in his work. A professional is confident in his abilities, and takes bold and calculated risks based on that confidence. A professional is not timid. However, a professional also knows that there will be times when he will fail, his risk calculations will be wrong, his abilities will fall short; he’ll look in the mirror and see an arrogant fool smiling back at him. So when a professional finds himself the butt of a joke, he’ll be the first to laugh. He will never ridicule others, but will accept ridicule when it is deserved and laugh it off when it’s not. He will not demean another for making a mistake, because he knows he may be the next to fail. A professional understands his supreme arrogance, and that the fates will eventually notice and level their aim. When that aim connects, the best you can do is take Howard’s advice: Laugh.

### Bibliography

- Robert C. Martin, Principles, Patterns, and Practices of Agile Software Development, Upper Saddle River, NJ: Prentice Hall, 2002.

---

## Saying No

## Saying Yes

## Coding

## Test Driven Development

## Practicing

## Acceptance Testing

## Testing Strategies

## Time Management

## Estimation

## Pressure

## Collaboration

## Teams and Projects

## Mentoring, Apprenticeship and Craftsmanship

## Tooling
