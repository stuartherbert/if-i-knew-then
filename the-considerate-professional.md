The Considerate Professional - Adrian Hardy
===========================================

Background
----------

As developers, we're more likely to be subjected to *"Software Politcs"* than traditional *"Office Politics"*. As an eager graduate seeking employment, I assumed that all of my would-be colleagues would be on the same page. Unfortunately, that's not always the case. While it's very rare that someone is maliciously counter-productive, cynicism can breed bad habits and turn an enthusistic coder into dead weight. In fact, worse than dead weight - someone who creates work for other people. 

By my nature, I'm a people pleaser. I strive for the approval of others. At the supermarket, I end up putting *other customers'* trolleys back. I can only hope that my penchant for trolley parking is what makes me a more considerate professional and not just satisfying some under-the-radar OCD compulsion. Although there'll be similar ground to other chapters (such as "Maintainability"), this chapter's focus is different. It's about ensuring your team members enjoy working with you on both a technical *and professional* level.

Reading and working with someone else's code should be a fun experience. There is no better example of active collaboration than producing a functional system with other people. But, at the risk of sounding hackneyed, small teams need to be able to work together. Let's go through some of the traits of a courteous professional and by implication, tell-tale signs that you're working with a inconsiderate prick.

Accepting Criticism
-------------------

*Learn something every day and, more importantly, be prepared to learn from others.*

In my very first commercial role, an internship at the tender age of 18, I was asked to do my best to learn a completely unfamiliar language called *Pike* (I was using obscure languages before it was cool). My line manager took a look at my work and said 4 words that I'll never forget:

> No. This is crap.

Uhh, ouch? But every developer needs to hear these words once in a while. It's like a sobering slap in the face. You are never at the top of your game and there is always more to learn. The very best in this industry are those who are constantly learning and finding out how to improve.

As a developer, you'll be tempted into accepting the commonly held belief that you are the weaver of magic and you alone are the key to profitability. Unfortunately, software development seems to attract people with a superiority complex, so if you or your team are unable to muster some modesty, you will not work effectively together. Teams need to be able to be honest with each other. Developers who cannot take criticism are the recalcitrant hemmorrhoid on the butthole of software development. They are, in other words, a pain in the ass. In my experience, there are two clear stereotypes of developers who cannot take criticism. There are those that crumble under criticism and let it ruin their day/week/career, then there are those who are invulnerable to criticism because they see themselves as infalliable. Two opposite ends of the spectrum, but both equally frustrating for everyone else. 

Revisiting Basic Principles
---------------------------

*Software development basics aren't just about protecting yourself, they're there to help others too.*

DRY (Don't Repeat Yourself) will be mentioned time and time again in software development. People say that it reduces bugs, lowers maintenance overhead and it's universally accepted as a Good Thing. I've recently had sight of a project where the original author not only created a userland implementation of PHP's explode method (DRY violation #1), but he copied and pasted it all over the codebase (DRY violation #2). Again, ignoring the maintenance angle, the original author just made someone else's life very hard because they were either lazy or ignorant or both. The adoptive author must deal with and understand your commentless implementation, but they also have to see it sprinkled across your entire codebase, like little functionally-redundant rabbit droppings. I'm experienced enough to deal with the maintenance overhead of this (and its immediate refactoring) but the lack of consideration riles me.

The "Not Invented Here" syndrome DRY's pernicious little cousin. An arrogant developer will decide not to re-use an existing public library because they believe their implementation will be better (Also note that in situations like this, said deveolper will be unable to qualify "better"). Unfortunately, this developer ignores the fact that the public library benefits from documentation, collective wisdom and public scrutinty. If I use something from a StackOverflow page (for example), then I quote that URL.

Don't attempt to impress colleagues by replicating functionality locally, impress them by getting the problem solved in a fraction of the time and in such a way that they don't need to speak to you everytime they want to understand your precious black box library. Become indespensible by being a good team player, not by planning obscurity into your code.

Strive to better yourself
-------------------------

*You have the luxury of working in a constantly moving industry - embrace that fact*

I have come across many a project which has suffered at the hands of a lazy programmer. Of course, there is the "regular lazy" programmer, but I'm talking about the guy who "knows enough". I will never forget this *actual quote* from a *real person*.

> I got to about page 40 in the [Learn PHP in 24 hours] book and decided I knew enough

This gem wasn't from a master craftsman programmer who was just transitioning to PHP from a wealth of programming experience. This was from someone who "knew enough". Such comments should aggravate you, because you take pride on your work, right?. And here's this cowboy ruining the good name of Software Engineering. If you don't immediately take issue with that stance, ask yourself this: At what page number would such a comment be justified? After how many books? After how many years?

Trick question - never. Something like web development is a very young craft and fortunately (or unfortunately, depending on how you see it) it's a moving goal. Now that means there's a lot of trends that don't stand the test of time, but that doesn't mean to say you shouldn't take an interest in new developments. Let's take another quote which I noted down while discussing PHP with someone (who admittedly wasn't really a professional programmer):

> Oh, they haven't put that object-oriented crap in there have they? I prefer to do it the old way ...

Professional or not, OO or otherwise, his dissmissive attitude is wrong. This isn't about OO, this is about being prepared to learn.

Naming things
-------------

*Putting thought into naming helps convey behaviour at first glance for the new programmer on the project.*

I won't decree specific naming conventions here, just don't be lazy. For example, "$data" is very rarely a meaningful variable name and the same goes for "$arr", "$foo" and "$temp". It takes no effort to avoid "$data[$i]['name']" in a for loop and instead use "$employee['name']" in a foreach. Why would you call a database field "date" when we have such a rich vocabulary; "created", "last updated", "activated" or anything must be better than "date". I know it's a date because it looks like a date. Give me something else. 

Giving a name to something in code should be like giving a surprise gift to a colleague. It remains unseen and unappreciated until a developer is fortunate enough to happen across it. I once worked with a multi-million pound system which revolved around "doit". "doit" wasn't just a variable name, it was a complete control structure for the application.

	if ($_GET['doit'] == 34345) {
		// 2,000 lines of code
	} elseif ($_GET['doit'] == 239746) {
		// another 2,000 ...
	} // and repeat this structure many, many more times

Want to add some new functionality? Simple, just add a new elseif, mash the numberpad, hope for a unique number (no, I'm **not even joking**) and start polluting global namespace. Enjoy debugging your magic number-infested hell, assholes!

This system - nay monster - was conceived because the person who wrote it at the very beginning "knew enough" (to use his words) and decided not to learn anything new. To paraphrase a previous section in this chapter, you should be learning something new every day.

Comments
--------

*Comments should describe motivation and decisions, not just functionality and problem domain.*

WHY have you introduced indirection at this point? WHY have you not implemented this third party API fully? If I know WHY you've done something in a specific way, I won't get distracted by confusion over your decisions. Even if the answer to all these questions is "because it's the quickest route to Minimum Viable Product" that's still very helpful.

In one of the very first projects I delivered in my commercial career (back in 2002), I replaced an explode() with a preg_match(). So the conscientious go-getter in me added a comment above the regex:

	// filenames sometimes have dots in them

These sorts of comments piss me off. Programmers who put lacklustre comments into some code may as well not bother. Hands up if you've ever seen a comment that looks like this:

	// loop over entries and insert them into the database

I've found myself writing such comments and then deleting them. They add no value. If your code needs such a comment to explain what's going on, we have a more significant problem to do with your general coding style and apporach. With the benefit of hindsight, perhaps my uninformative comment should've been a little more verbose:

	/*
 	 * @since 2002-12-03
 	 * Updated the regex to not assume a single suffix, because supplier X
 	 * has started to give us data in the format "img003.xyz.jpg"
 	 */

It's a trivial example, but the comment explains the motivation for the change. I would accept the argument that such documentation should go in a commit message, but I don't like the assumption that the developer should have to go away and read up on the entire commit history for a file. 

Regular expressions can be pretty tricky to decypher. A habit I picked up a few years ago was to try and break down the regex into separate, discrete parts. Each component had its own line and supporting comment and then it was simply stitched together and executed. 

	$regex = array('/');
	$regex[] = '[a-zA-Z]{4}'; 		// supplier code prefix
	$regex[] = '\d{4}-\d{2}-01';	// date of dispatch
	$regex[] = '[A-G][BXCG][\d]';	// shipping code
	$regex[] = '/';

	preg_match(implode("", $regex), $item_log_entry);

Long-winded? Perhaps. Certainly overkill for this example but in the case of a a beastly regex, if it can stop a few developer's heads exploding as they try to figure out where and why we used a negative look behind, it's worth the extra bytes on disk.

Transparency and Predictability
-------------------------------

*"Affordance" should be applied to source code and not just limited to those studying HCI or UX.*

Even if you're unfamiliar with the term, you will have experienced the benefit of "affordance". When entering a public building, the brass plate on the door invites you to place your hand and push. In UI design, a button looks "clickable", and so immediately users want to click it. Let's apply this to code. Is the behaviour and responsibilty of your class or function predictable? As an example, the principle of "Command/Query Separation" dictates that a function should either perform an action, or return a value. If you call a method "getResult" and it modifies the class, that's hidden behaviour. Can you call "getResult" repeatedly and expect the class' state remains immutable? Of course, we're assuming you have the luxury of classes and methods, but the same should apply to procedural code.

Whenever someone is working with your code, it should be a fun experience and opaque code is not fun. This section goes hand in hand with *naming things*. If your function name starts to look a little like a sentence ("do_this_if_that_and_that") then maybe you're pushing too much into a function. I'm paraphrasing (perhaps very obviously) Martin Fowler's Refactoring, but pushing too much responsibility onto a function is a code smell. 

Write better code *and* help a teammate. Wow, you *are* considerate.


Initiative - the double-edged sword
-----------------------------------

*There's a fine line between demonstrating initiative and making up jobs that no-one needs done*

"Initiative" is a tough one. It's exceptionally difficult to quantify and even moreso on paper. Here's an example.

I loved Martin Fowler's book on refactoring. You should read it. Now. 

However, upon reading and digesting the book, the temptation is to go around improving all these crappy codebases. "Look at all this smelly code" you'll say to yourself. "I'll just go ahead and fix this. Once the guys see what I've done, they'll carry me out on their weak, programmer shoulders! At the same time, I will impress my manager with my newfound contempt for sub-standard code". 

The code will sit there, mocking you. You should resist changing it. Just because you can do something doesn't mean you should. What are your reasons for refactoring it? Now, what are your commercially valid reasons? If there's a difference, it's not time to refactor yet. 

So this is a catch 22: You *must* be able to work without direct supervision and yet, you can't consider yourself off-the-leash until you've earned that trust. There is no magic bullet for this, you just need to be aware of any personal tendencies to either show off or look for safety blankets.

Code Conventions
----------------

*Be consistent and adhere to standards.*

As an absolute bare minimum, be consistent. Do you have a stance on indentation, braces or underscores? Set yourself some personal standards and stick to them. For example, I have the rather archaic habit of keeping my doc blocks less than 80 characters wide. I think it looks neat and easy on the eye, but that's a personal preference. Even if it aggravates others, at least I'm consistently aggravating.

Some might say the answer is to set out a team-wide standard. I've seen all sorts of coding standards; some span a dozen pages and some just don't exist. If your team has documented conventions, stick to them. If you disagree with underscored Hungarian notation, don't protest in your code. People will not respect your principles, they'll just roll their eyes whenever they need to work with you. My very first professional role mandated the number of empty new lines after a method definition. My distaste for such a rule was irrelevant, as that was the standard set. For the greater good and all that business.

In conclusion
-------------

Don't be an asshole. It's that simple. 

Accept that you can be wrong sometimes. Be prepared to learn all the time. Be courteous both technically and personally. Take pride in your work. Be a valued team member, but not through protectionist over engineering.

About Me 
--------

I'm the Development Team Lead at Magma Digital. My day to day job involves every aspect of the software development life cycle, from shaking hands with the client at the very first meeting to marvelling with my team members as we hit the big, figurative launch button. My first commercial job was in 2002 as a PHP developer and PHP has stuck with me to this day.
