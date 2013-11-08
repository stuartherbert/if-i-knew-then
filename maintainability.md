---
layout: book-chapter
title: Maintainability
prev: '<a href="life-will-change.html">Prev: Life Will Change</a>'
next: '<a href="measuring-success.html">Next: Measuring Success</a>'
---

# Maintainability

_By [Damian Gostomski](#about_me)_

A typical software project will be in active use for several times longer than the initial development period, if not more. During this time, bugs will be found, environments will change, performance issues will occur and new features will be requested. In order for these changes to be made quickly and efficiently, the software needs to be maintainable, which is a contributing factor to the long term success of a software project.

Maintainable software has several key characteristics:

1. It is easy to locate the section of code required for a change.
1. The purpose and functionality is easy to identify, and how it fits into the larger system.
1. Changes can be made without fear of causing side effects, or these can easily be identified.

> Always code as if the guy who ends up maintaining your code will be a violent psychopath who knows where you live.

## Why I Wish I'd Known

Although I was never naive enough to think I'd never work on a project with an existing code base, I was unprepared when it finally happened. Despite several years of programming as a hobby and 3 years of programming at University, I'd never come across any issues with maintaining code, until I started working as a developer in an agency.

This wasn't a coincidence, and it wasn't because the code that *I* wrote was so perfect and well structured - it was due to the types of projects that I worked on and the way I learned programming.

### Why Universities Fail To Teach This Fundamental Skill

If the ability to write maintainable code is so important, and you will almost certainly have to maintain an existing software project at some point, why is it not covered in every University course related to programming?

There are lots of ways to learn programming, with most Universities opting to use a variation of the following process:

1. Pick a small topic, construct, language feature or design pattern.
1. Cover the theory of the chosen subject.
1. Set a short, very focused practical exercise to cement the new knowledge.
1. Repeat.

Each time you repeat the process, your knowledge increases and you can build more complex systems by combining everything you've learned. The problem is, you're learning in isolation.

After completing a practical exercise, you'll almost certainly never look at it again, yet alone build on top of it. Because of this, you'll miss out on the valuable experience of extending legacy software, fixing bugs in your code, and learning the hard way about maintainability while the stakes are low.

A solution to this would be to build one or two large scale systems throughout a course, with each iteration of the above cycle not only focusing on teaching something new, but also requiring updating existing code, fixing bugs, adapting to changing requirements or new dependencies.

## Making Code More Maintainable

You may not have the luxury of starting a project from the beginning, but when you do, ensure that you set out with the aim of writing maintainable code. If you're maintaining an existing project, be it one you've previously written or one created by another team of developers, these points are still relevant going forwards.

Even if you think the project has a short lifespan or will only be maintained by you, follow these tips, as in most cases, throw away projects are rarely thrown away, and even if you *are* the only person maintaining a project, this will still help you.

You may find that by applying the following tips, you increase the initial development time, but that's normal the first time you apply them. It's an investment which will save you time in the future maintaining the system, and each time you apply them to a new project, the initial overhead will continue to shrink and the rewards will continue to grow.

### Write Code For Humans, Not Machines

Although the code you write will ultimately be compiled / interpreted by a computer, you should always set out to write code for humans first. The computer will stop you writing code that won't work (compile time errors, runtime exceptions etc), but it won't stop you writing unmaintainable code.

Always write the simplest code that you can to achieve the correct result, but don't confuse simple with short, as sometimes the simplest code to follow is more verbose.

There are 3 key rules to follow to make your code easy to follow:

1. Have meaningful class, method and variable names.
1. Have lots of short, single purpose methods instead of long blocks of code I need to follow to understand.
1. Have up to date comments that explain why, not what.

### Documentation and Comments

As an extension of writing code for humans, you should also write documentation and comments for humans as well. These can take various forms including end user documentation, architectural designs, API references, DocBlocks and inline comments. Each of these serves an important purpose, but I will focus on code level documentation (DocBlocks and inline comments).

The purpose of code comments should be to explain what a block of code does and why, not what, which can easily be inferred from reading the relevant block of source code.

Any non trivial functionality should be documented to clearly explain what the block of code does, as it's not immediately obvious. As you would only resort to a non trivial implementation if all the obvious solutions failed, document the reasons for this, such as *"Unable to use Solution X as it causes an infinite loop under condition Y, so have to use recursion with an additional check Z"*.

Lastly, ensure that any documentation and comments is also maintained and kept up to date, as out of date documentation / comments can cause bigger problems than none in the first place.

### Don't Repeat Yourself (DRY)

Every time you go to copy and paste a block of code, you're introducing a potential maintenance nightmare. All future bug fixes and updates will need to be made in multiple places, and the more times you've duplicated the code, the higher the chance of missing one in an update. Over time, this will introduce bugs and inconsistencies into the codebase.

Instead, you can take the code and place it into a generic helper function which can be called from anywhere else in the codebase. Alternatively, if multiple classes share similar functionality, you can create a base class which they extend, and each class only need to add specific functionality to that class.

As well as reducing the number of occurrences of code that need to be maintained to one, doing this will reduce the size of the codebase, meaning there is less code to maintain.

### You Ain't Gonna Need It (YAGNI)

More often than not, the scope of a software project will change throughout the duration of the initial development, and will continue to change after the project has been completed. It is therefore common for developers to anticipate potential functionality, or include logic for something that might happen in the future.

Although this is done with the best intentions, of making it easier to add / change this functionality in the future, it often makes both the initial development and maintenance more complex.

In many cases, the potential functionality will never go ahead, resulting in additional logic serving no purpose, other than to make maintenance more complex.

In a well designed, *maintainable* system, adding and changing functionality is easier than in a system full of assumptions about what it might do. Fewer assumptions paired with well written code means there is less to maintain, but it's also easier to maintain.

### Automated Tests

An automated test suite allows you to easily verify that your code functions as expected. This is invaluable when maintaining existing code, as running the test suite will check if your updates have caused any existing tests to fail, therefore preventing the introduction of bugs. Without an automated test suite, you'd need to manually test the system to check if you introduced any bugs. This is both time consuming and error prone.

A common methodology for writing automated tests, especially in agile development processes, is Test Driven Development (TDD). In TDD, the tests are written *before* the code, and then the minimal amount of code is written to make the tests pass (minimal in terms of scope and complexity, not lines of code). A common side effect of TDD is more modular, maintainable code.

If the system you're maintaining doesn't have an existing test suite, and you don't have time to write unit tests for every piece of code (you will almost certainly not have time to do this), you can build up the test suite over time.

Every time a bug is found, write a test to verify the existence of the bug, and then write the code to make the test pass, resolving the bug. The same should apply every time you need to update a section of working code: write a test which passes, make the required changes, and ensure the test still passes.

### Excessive Configuration Options

Every time you introduce an option into a software project, you add an additional execution path. Even a simple system with 10 options, each of which can be yes or no, you've introduced over 1000 possible execution paths. This additional complexity not only means more testing is required and possible edge cases, but a maintenance nightmare as you're now relying on user input.

It's unreasonable to develop a large scale system with no configuration or options. You should aim to minimise the number of options that control the execution flow by favoring decisions over options.

### Refactoring

You won't always have the luxury of working on a project from its inception. You may join a project part way through, or maintain a legacy system written by someone else or yourself from previous years. If the code has been written with complete disregard of the above, there is still hope. You can improve the quality and maintainability of the code base over time by refactoring.

> Code refactoring is a "disciplined technique for restructuring an existing body of code, altering its internal structure without changing its external behavior", undertaken in order to improve some of the nonfunctional attributes of the software.

You can use refactoring to achieve the above, as long as you don't change the external behavior of the system:

* Simplify the implementation of a method and make it easier to understand by using descriptive variable names.
* Abstract out repetitive code into a sub routine.
* Remove redundant code.
* Break down long, complex methods into a series of smaller methods, each serving a single purpose.

As you refactor your code, you may need to change method signatures or remove them all together. In this case, you should deprecate the old method. This means it will continue to function, but will be removed in a later version of the software. The method should be tagged as deprecated (via docblocks), so developers know not to rely on it any more, and the deprecated code can act as a wrapper for the new implementation of the functionality.

If the code that you're refactoring doesn't already have automated tests for it, now is a prime time to add them. Write them before you refactor the code and ensure they pass. Run the tests again after your updates, and if the tests no longer pass, you changed the external behavior of the code, and should resolve the issue.

## Final Thoughts

Software systems are living, evolving creatures, and approaching them thinking otherwise will land you in a world of pain. Every time you have to maintain an existing bit of code, aim to leave it in better condition then when you started - Write some test, refactor it, document it.

And lastly, if you pick up someone else's code and it looks an unmaintainable mess, don't get mad or insult their abilities. You don't know what constraints or pressure they were under when it was written, all you can do, is make it better.

## About Me

I am the lead developer at Manchester based [MC2](http://mcmc.co.uk), and despite studying Computer Science at the University of Manchester, I had to learn many of the lessons in this book the hard way. I spend half my time maintaining existing systems, and half the time writing new ones to be maintained in the future.

You can find me on Twitter as [@damiangostomski](https://twitter.com/damiangostomski) or my website [7degrees.co.uk](http://7degrees.co.uk).
