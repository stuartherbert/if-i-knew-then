---
layout: book-chapter
title: Coding Standards
prev: '<a href="maintainability.html">Prev: Maintainability</a>'
next: '<a href="continuous-integration.html">Next: Continuous Integration</a>'

---
Coding Standards - Steffan Harries
==================================

## What are Coding Standards?

Coding Standards (AKA: Coding Conventions) are a method of imposing simple rules and to follow when you're writing code. These "standards" are not enforced by compilers or interpreters but are run by using build tools, like [ant](http://ant.apache.org/) or [phing](http://www.phing.info/), and continuous integration servers like [Jenkins](http://jenkins-ci.org/) and [Travis](https://travis-ci.org/) CI. Coding Standards are a style guide that tells you whether you should put your curly braces on the same or a new line, or remind you those methods should be typed in camelCase()?

There's a bit of a debate as to whether you should indent your code with tabs or spaces, and if you use spaces is it two of them or four? Does white space matter? What about file naming conventions? Obviously there are a lot of variables (bad pun) here that may affect the way you work. If you're working on a project with other developers and you all start coding in your own *style*, you'll quickly find your source code is a mess and becomes unreadable. And [readability](http://shop.oreilly.com/product/9780596802301.do) really does [matter](http://books.google.co.uk/books/about/Clean_Code.html?id=_i6bDeoCQzsC)! 

## Why Should I Care?

When you start working on a project with other developers, it's important to agree on a coding standard. Some software houses will have their own standard that you must use, but many open standards like [PSR](https://github.com/php-fig/fig-standards) already exist. 

Here are some interesting points (see ref. #1 for source):

* 40-80% of the lifetime cost of a piece of software goes into maintenance.
 
* Hardly any software is maintained for its whole life by the original author.

Think how many young open source projects would die if when the original author left and nobody wanted to pick up the project anymore because the source code was in bad shape? Nobody wants to buy a home that's been badly looked after and the same goes for code. That's how projects die. There's nothing worse than coming along to use a library on a project only to find that it's been badly maintained and nobody wants to work on it. 

This point is also raised in [The Cathedral and the Bazaar](http://www.catb.org/esr/writings/cathedral-bazaar/cathedral-bazaar/) where Eric S. Raymon takes over, quite by accident, a dead project after the original author had lost interest. Initially through small patches and bugfixes, he took over maintaining the project and the code base started evolving again. In this open source world of code sharing it's easy to get the ball rolling on a project and have it live on long after the original author has lost interest. The easier you make it for people in later years to come and pickup your code again the better you are for it as they'll respect you and your work more instead of starting again from scratch. I would much rather develop code for a dead code and inherit the position as a maintainer versus [re-invent the wheel](http://sourcemaking.com/antipatterns/reinvent-the-wheel).

I have the pleasure of working with some very clever chaps like Gavin, whose written an excellent blog post on [trusting the libraries](http://www.boxuk.com/blog/trusting-the-libraries-you-use) you use. A good way to do this is to see how often code gets contributed to it. That will give you an idea about whether this code is actually being used by people in the wild and how well it's being maintained. I would be willing to bet that the projects being actively developed for are also the ones backed up by good coding standards. Imagine the pain you'd have for investing days/weeks worth of time integrating the use of a library in your project only to find that there's a big bug preventing you from doing what you want with it, but because the project isn't being maintained you have nobody to send a bug report or fix to. On the other hand, that could be your opportunity to take over the project give it a new lease of life.

## PSRs
I'm using PSR as an example because I'm a PHP developer by trade right now and that's what I know best although the concepts are mostly interchangable between languages. 

So far [PHP Framework Interoperability Group](http://www.php-fig.org/) (PHP-FIG) have introduced three "standards":

### Autoloading Standard: PSR-0
PSR-0 drescribed requirements to be adhered to for autoloader interoperability. For example: 

* Each namespace must have a top-level namespace ("Vendor Name").
* Each namespace separator is converted to a DIRECTORY_SEPARATOR when loading from the file system.
* Alphabetic characters in vendor names, namespaces, and class names may be of any combination of lower case and upper case.

If you've used Symfony and Composer, you're probably already familiar with PSR-0 namespaces if you look at a bundle's composer.json file but the concept is much broader than that. The [Composer documentation](http://getcomposer.org/doc/04-schema.md#psr-0) has a pretty good example of how you can use libraries/bundles that comply with PSR-0.

You might be asking: *why does this matter?* OK, I agree that initially this might seem a little anal. But say you put weeks or months of effort into building a library for your project. You built it in mind with the framework you're using. All of a sudden, you learn that a competing framework is much more efficient. Efficiency matters for your project, so you switch. Lucky for you, your library complies to PSR-0 so you don't even have to make any changes to autoload your code! 

Not only that but because the two frameworks both adopted PSR-0 it means you can use parts of either framework in your project and that kind of interoperability is something that just didn't exist at this level a few years ago. When I wrote my dissertation I didn't know any of this so I was stuck using a heavy weight framework and limited myself to it. Big mistake!

### Basic Coding Standard: PSR-1
PSR-1 is just what it says on the tin: it's the basic coding for "*what should be considered the standard coding elements that are required to ensure a high level of technical interoperability between shared PHP code.*" Amongst the typical things most people agree on like camelCase method signatures and StudlyCase Class names you'll find other, more specific rules. 

* PHP code MUST use only UTF-8 without BOM.
* Constants must be declared in upper case with underscore separaters
* A file should declare symbols (classes, functions, constants) or declare side effects

#### What Are 'Side Effects'?
This is an interesting (read: weird) point raised in PSR-1. 

>A file SHOULD declare new symbols (classes, functions, constants, etc.) and cause no other side effects, or it SHOULD execute logic with side effects, but SHOULD NOT do both.

What "side effects" means is the running of code not directly related to declaring classses, functions, constants, etc. Examples of side effects are: modifying global or static variables,  reading/writing a file, modifying php.ini settings, etc. 

This example is taken from the php-fig documentation on PSR-1: 

```
<?php
// side effect: change ini settings
ini_set('error_reporting', E_ALL);

// side effect: loads a file
include "file.php";

// side effect: generates output
echo "<html>\n";

// declaration
function foo()
{
    // function body
}
?>
```

When I first read this I was trying to understand why it was necessary. OK, some stuff I get: modifying php.ini settings on the fly isn't a good idea and echoing out HTML can get sloppy and should be kept away (separation of concerns) whenever you can. But including files I didn't get right off: why was that so bad? 

The reason: when your class is loaded, [the state of the application should not change](http://stackoverflow.com/a/13299008/694629). Anything which changes the state (environment) in which your code runs should be kept and loaded somewhere else. If you're including a file that executes code (which, let's be honest, is the only reason you would be) then that will modify the state of your application and cause unreliable results. 

There are other reasons why this isn't a great idea either:

* What if Disk I/O is reaching critical levels when you run an include/require?
* What happens when the file is modified outside of the state of your application?

That's pretty much all I'm going to say on PSR-1. You could go further but I don't think it's necessary as it's fairly self explanatory and it's what most are already doing anyway without even realising it.


### Coding Style Guide: PSR-2
Here comes the good stuff. PSR-2 is what you *always* should aim for. PSR-2 exists to ensure that your code reduces confusion when being contributed to by multiple authors. They say: "*It does so by enumerating a shared set of rules and expectations about how to format PHP code*".

PSR-2 compliant code must (amongst other things) do the following:

* Follow PSR-1.
* Use 4 spaces for indenting, not tabs.
* Must not be a hard limit on line length; the soft limit is 120 chars.
* Place opening braces for classes on a new line, closing braces must go on the next line after the body (no white space).
* Visibility must be declared on all properties and methods.
* Control structure keywords (if, while, etc) must have one space after them; methods must not.

Here's another example from the docs, see which of the above rules you can apply:

```
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleFunction($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
?>
```

As you can see, PSR-2 provides for very readable code. We can see from that example that the namespace complies to PSR-1, there's a nice blank line between the namespace before the ```use``` declarations and that the class and function curly braces go on a new line for added clarity. Note however that the if/else block places the opening curly brace on the same line! Some would criticise PSR-2 here for inconsistency, and maybe they're right.

I honestly don't know the reason for this. I would like to think it's because classes and functions can be long and can sometimes extend longer than your IDE can show you at once, so putting it on a new line improves clarity. However control structures like if/else blocks are very common and shouldn't be long or unweildy and so it would be overkill to put those on a new line - but that's just me talking. I haven't covered everything here, there's a lot more to the PSR-2 standard so check it out!

One more thing: the documentation for PSR-2 doesn't give justification for these rules. They were gathered from studying well run projects and looking for commonalities to adopt as a practice. They kept their survey data and results and published them too: <https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md#appendix-a-survey> 

### Logger Interface: PSR-3
This is new to me: I don't know it and I haven't used it. PSR-3's goal is to allow libraries to receive a LoggerInterface object and write logs in a simple and universal way. By providing a standard for doing so the hope is aim is that third party code can easily write to the centralised application logs. PSR-3 has only recently (5/1/2013) moved from a proposed standard to an accepted one. A quick search found that [Monolog](https://github.com/Seldaek/monolog/tree/1.3.0) has adopted PSR-3 compliance as of version 1.3 The project's docs say: "*This library implements the PSR-3 interface that you can type-hint against in your own libraries to keep a maximum of interoperability. You can also use it in your applications to make sure you can always use another compatible logger at a later time.*"

## Why This Matters To Me?
Coding standards matter to me because the way I'm working at the moment means that CI jobs will fail if the build if PSR-2 compliance isn't met. If the the code in the Pull Request fails the build then it won't get merged in. By ensuring my code meets the PSR-2 coding style I'm making sure that my code is of a good quality, readability and thus (hopefuly) maintainabile. I don't want to be known as *that* guy whose code is hard to work with. Git/SVN blame makes it easy to trace down who and when lines of code were added. I don't want any crazy developers hunting me down in years to come!

I found very quickly after leaving University that what I knew about programming was just the tip of the iceberg. I'm lucky to work with some very, very clever guys and the amount of information I pick up off them through osmosis is huge and sometimes too much to handle. I'm the type of person who learns by doing, so by meeting the PSR-2 levels of coding standards I'm achieving a standard that's been set by very clever people, much clever than you and I.

I can say for certainty that if you attend a job interview and get talking about coding standards you will get your interviewer's attention. Developers are a common breed, there are lots of us. In 2011, the [UK Higher Education Statistics Agency](http://www.hesa.ac.uk/index.php?option=com_content&task=view&id=2546&Itemid=278) stated for fact that: 

>The highest unemployment rate is seen amongst those who studied Computer Science, at 14.6%.

You have competition, my friends. Rise up and beat it. Interviews are crucial to this. By talking about and using practices like coding standards you're leveling up on your competition who don't. Computer Science graduates have a reputation for being sloppy and hap-hazard coders. Don't let yourself be that person! Prove them wrong! If you get people's attention by using best practices you'll stick in their memory with a positive note and that's the best thing you can achieve in a job interview. That's your foot in the mental doorway to a career with that company.

Coding standards matter to me because they'll make your life easier in the long run in your projects, they'll get you kudos from fellow developers and because they'll make you a better developer. Any thing that makes me better at coding, no matter how small, is a win for me. Eventually coding standards will become almost second nature - I'm not quite there yet but I'm seeing positive improvements all the time. 

I've definitely seen a change in the way I write code for the better since adopting coding standards. I used to write code and if it worked I didn't care, I may not have even written tests for it. That's the type of mindset being at a coder at university forces you into through working on 6 different projects at once, each with their own ridiculous deadline, whilst you're desperately trying to cling onto a social life. That *has* to change when you get to industry. I'm really happy with how much my coding has improved in the last six months since I left university. I'm a much better developer and that's in no short thanks to coding standards, I owe my new colleagues a big thank you for introducing me to things like this that make me a better a developer.

## So How Do I Check My Code Conforms?
There's a pear package called [PHP_CodeSniffer](http://pear.php.net/package/PHP_CodeSniffer/) which will provide you with the CLI tool ```phpcs``` which you can use to check your code's compatability. You can also control it's output format if you only want a summary or a full output depending on your needs. Integrating PHP_CodeSniffer into your Continuous Integration tasks will automate this task for you, I'll cover that a little in my next chapter!

## Bio

I'm [Steffan Harries](http://www.steffanharries.me.uk), I recently graduated from [Aberystwyth University](http://www.aber.ac.uk/en/cs/) and I'm now working in Cardiff city centre. In my short time in industry I've picked up loads of useful info and best practices from new colleagues and a variety of events in Cardiff. My interests lie in web development, photography and motorsport.

---

## Resources
On top of the hyperlinks used in this chapter here's some other useful sources of info I used writing this chapter: 

1. Robert L. Glass: Facts and Fallacies of Software Engineering; Addison Wesley, 2003.
2. PHP Framework Interoperability Group - <http://www.php-fig.org/>
3. PHP_CodeSniffer - <http://pear.php.net/package/PHP_CodeSniffer/>
