---
layout: book-chapter
title: The Perils Of Design Patterns
prev: '<a href="continuous-integration.html">Prev: Continuous Integration</a>'
next: '<a href="life-will-change.html">Next: Life Will Change</a>'
---

# The Perils Of Design Patterns

_By [Craig Marvelley](#about_me)_

When I started my degree course I thought that software development was pretty much all about writing code. It's an essential part, to be sure, but it was only a couple of years after graduating and finding employment that I realised the _design_ of my programs had just as much impact on my applications as the actual code I wrote.

That it took me a while to learn this lesson may have been because my course put more emphasis on the science of computing (algorithms, data structures, etc.) than on the art, including design and documentation. I have spoken to some recent graduates to whom this thankfully did not apply; however I'd hate to think that it's still possible for students to complete their degrees without being exposed to fundamental patterns of software design like the Singleton, or the Event Dispatcher.

The lesson I wish I'd learned sooner though, is that there's a time to lean on patterns, and a time to strike out alone. There are safe patterns, and there are patterns that can really compromise a project if used incorrectly. I'd like to share the experiences that brought me to that conclusion and prevent others from repeating my mistakes. How can we put patterns into practice while avoiding the common mistake of over-engineering?

## What Are Design Patterns, Exactly?

Before we go any further it's important you understand a little about design patterns. If you already do, skip this bit!

The [Wikipedia article on software design patterns](http://en.wikipedia.org/wiki/Software_design_pattern) describes them thus:

> In software engineering, a design pattern is a general reusable solution to a commonly occurring problem within a given context in software design. A design pattern is not a finished design that can be transformed directly into source or machine code. It is a description or template for how to solve a problem that can be used in many different situations.

Patterns have been around as a concept since the late 1970s, but the release of '[Design Patterns: Elements of Reusable Object-Oriented Software](http://books.google.co.uk/books/about/Design_Patterns.html?id=6oHuKQe3TjQC)' by the affectionately titled 'Gang of Four' proved something of a watershed. The book defined a bunch of patterns that have since been reused in countless systems, in all manner of languages. Have a skim of [this page](http://en.wikipedia.org/wiki/Design_Patterns#Patterns_by_Type) to get an idea of the patterns described, including [Singleton](http://en.wikipedia.org/wiki/Singleton_pattern), [Iterator](http://en.wikipedia.org/wiki/Iterator_pattern) and [Facade](http://en.wikipedia.org/wiki/Facade_pattern), which have since become key elements of software engineering.

Subsequent to the book's release design patterns were quickly applied in 'enterprise' systems like those constructed in Java or C++, where they brought clarity to gigantic, complex codebases. In recent times they've also found a place in more agile systems, like web frameworks built in PHP or Ruby, so these days you don't have to look far to see a pattern in use.

If you want to learn more specifics, try the Gang of Four book, or alternatively [Head First Design Patterns](http://shop.oreilly.com/product/9780596007126.do) covers the same principles but is considered by many to be a more accessible read.

## Why Use Them?

OK, so we know what patterns are. Before we get into the pitfalls, let's quickly consider why we bother to use them at all. What advantages do we gain by employing them?

For me, the most important benefit is easy communication of ideas. Say I'm discussing with my workmates how best to approach implementing a system - by referencing patterns we can debate the options without having to write illustrative pseudocode. For example I can say to [Gav](https://twitter.com/gavd_uk) "If we introduce a facade then we don't have to worry about changing the original implementation, so we can maintain backwards compatibility with third parties" and he'll be able to picture how I plan to implement it.

This ease of communication is also handy further down the line - being able to document an implementation in terms of patterns means that system design can be expressed very simply - a statement like "A facade class provides an easy way to communicate with the legacy API" should let any developer new to the system know that they should use the simpler class rather than tangle with the nasty old stuff.

It's not just communication of ideas that's improved though - ideas themselves can arise from an acquaintance with patterns. Just like rifling through shelves of CDs at your [favourite record shop](http://www.spillersrecords.co.uk/) to find new tunes to explore, I've often found design inspiration by reading through the patterns in the GoF book. The code I wrote after leaving uni was horrible, hacky stuff that was technically functional, but suffered from a lack of planning and structure. The sort of code you wouldn't want to come back to a year later, or gives you the sweats when you think about another developer having to work on it. I was guilty of focusing on the language I was working with and not incorporating ideas from other, more mature languages. A knowledge of patterns helped me address that failing, which I'm very grateful for.

Finally I've found that employing patterns in my code has often sped up development - I've spent less time procrastinating over what names to give to classes and how to relate them to each other, and just followed the blueprint of the patten. This can sometimes lead to problems though, as we'll discuss in the next section.

## When Patterns Go Wrong

We've established that patterns can certainly aid software development, but I've first hand experience of how they can negatively impact our projects. Patterns of this ilk are commonly known as [anti-patterns](http://en.wikipedia.org/wiki/Anti-pattern#Software_engineering), because they do more harm than good.

I've worked on straightforward, simple codebases, like migration tools or throwaway prototypes, where the use of patterns has led to [over-engineering](http://discuss.joelonsoftware.com/default.asp?joel.3.392075.30), meaning code that is more complex, and of greater size, than it needs to be. We can justify an increase in complexity or size to a point if it makes the system easier to comprehend for ourselves and our colleagues, but in all projects, and especially disposable ones which will not require long term maintenance, it's pretty much [a cardinal sin](http://en.wikipedia.org/wiki/Accidental_complexity).

By way of example, I once wrote a migration program to which I added plugin functionality using the [Template method pattern](http://en.wikipedia.org/wiki/Template_method_pattern), spending a few days on the implementation. It turned out that the system was never extended, so the facility was redundant and considerable time had been wasted - I quickly learned to only introduce patterns [if the situation calls for them](http://en.wikipedia.org/wiki/Cargo_cult_programming). [This post by Jeff Atwood](http://www.codinghorror.com/blog/2005/09/head-first-design-patterns.html) sums that sentiment up nicely.

I previously stated that a knowledge of patterns can be a blessing when it comes to development by reducing procrastination, but this blessing can also be a curse. The flipside is twofold. Firstly there's a danger that creativity can be impaired, because we can become [fixated on reusing the same approaches](http://en.wikipedia.org/wiki/Golden_hammer) rather than thinking each problem through and designing an appropriately individual solution. I've been guilty of that in the past, and so it's important to not think of the patterns as a finite catalogue of design techniques.

I was once working on a web app to be used as an administration tool, and one of the first decisions made was to use the [composite pattern](http://en.wikipedia.org/wiki/Composite_pattern) to model the way that each feature within the system was comprised of a chain of standalone sub-components. Convinced that this was the right approach, we immediately began implementing it in PHP. Shortly afterward, with the implementation finished, we realised that while the approach was sound, it actually needed to be implemented on the *client* in JavaScript, rather than on the *server* - another example of how a preoccupation with patterns can cause us to lose sight of more important decisions.

Overall though, in my experience the most dangerous application of patterns is when their use plain compromises a codebase. The best example I can give here is one I've seen repeated by many developers; using patterns that serve to increase coupling within the system until it becomes inflexible and untestable. The Singleton pattern is infamous for often causing such a problem (and [justifiably so](http://stackoverflow.com/a/1020384/198846)), but any pattern which can make it more difficult for us to write code and do our jobs has to be used carefully. There are some patterns (like [Observer](http://en.wikipedia.org/wiki/Observer_pattern) or [Mediator](http://en.wikipedia.org/wiki/Mediator_pattern)) which work to make our code more modular and so are relatively harmless - if used in error, the worst case will be an excessive separation of concerns and code bloat - but others like the Singleton, or even [class inheritance itself](http://craigpardey.com/wp/2012/07/anti-pattern-re-use-through-inheritance/), can be abused such that they render a system unmaintainable. In my experience, the [technical debt](http://en.wikipedia.org/wiki/Technical_debt) that results leaves us with little option than either an extensive [refactoring](https://en.wikipedia.org/wiki/Code_refactoring) of the codebase, or a [major rewrite](http://onstartups.com/tabid/3339/bid/97052/How-To-Survive-a-Ground-Up-Rewrite-Without-Losing-Your-Sanity.aspx) - neither of which come cheap.

## In Conclusion

If you're embarking on a career in object oriented programming you'll inevitably soon find yourself in similar situations to those I've described above, and hopefully you'll also be inclined to take care when employing patterns in your solutions. Even if you're working in more functional languages like Scala or Clojure, the same principles apply - before you employ a pattern, think first whether you actually need to use it, and whether it's the correct one for the circumstances. Be pragmatic, sensible and smart, and your applications and products will surely follow suit.

## About Me

I'm a software developer living in Cardiff and working at [Box UK](http://www.boxuk.com), where I mainly develop web and mobile applications in all manner of technologies. Together with a few friends I run [Unified Diff](http://unifieddiff.co.uk), a popular monthly meetup for anyone interested in software development in South Wales.


