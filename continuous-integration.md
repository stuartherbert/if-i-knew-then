---
layout: book-chapter
title: Continuous Integration
prev: '<a href="coding-standards.html">Prev: Coding Standards</a>'
next: '<a href="productivity.html">Next: How To Be More Productive</a>'
---

# Continuous Integration

_By [Steffan Harries](#about_me)_

## What is Continuous Integration?

When I first heard of "*Continuous Integration*" all I could think was "*That's just committing your code often right?*". No, no, no. CI is so much more. CI is about:

* Building your project (in a shared environment) in an automated way
* Running unit, functional, integration tests
* Preventing integration pain
* Constant feedback
* Every change made rebuilds the project
* Building in a production-like environment

In order to use CI your code repository needs some integration to a CI Server (more on that later) so that the CI Server can check out your code and do it's thing. The idea is that every time you commit a change to the codebase your CI Server is able to checkout the project at that revision so it can build your project and test for integration pain. If it's all good, great. If not, you'll get notified immediately so you can fix it. It sucks spending ages writing a feature only for you to re-integrate it and find it doesn't work. With CI, you get near instant feedback letting you know saving you time and effort.

CI Servers aren't magic though, they'll only do what you tell them to do. A good way to do that is to use the build tools we can easily re-use. For instance, you can write a ``build.xml`` configuration file and use ``ant`` or ``phing`` to run it. In your build file you can specify how tests are run, what static analysis to use, fixtures to run and anything else you want to happen when your project is built. The other upshot for you is that it makes it easy for you to get a working environment setup quickly. All you need to do is checkout the latest code and run ant to build the project.

## Why Should I Care?
CI lets you know if and where changes that could break your application were introduced.

### Alice and Bob
Here's a scenario: Alice and Bob are working on an a program together, each committing code into their own feature branches using git as their version control software. Before either of them merges code into master they check each other's code to make sure they're not introducing bugs or problems they will have to overcome. They do this by checking out each other's code and running unit and integration tests, a code sniffer and perhaps also use other tools to check code coverage, etc.

At the start of a project that might be fine. But what about 2 months later? Alice and Bob are getting grumpy now by getting constantly interrupted by the other wanting to merge code into master but their process demands they must manually check each other's code before merging. As their frustration grows things are only going to end badly.

### Alice, Bob and Travis/Jenkins
Travis and Jenkins are both great CI products. I've used Jenkins extensively at work and Travis a bit at home too. Let's try that scenario again using Jenkins as an example.

Alice and Bob create a build configuration file to use Jenkins as their CI server. Now when either of them wants to merge their code into master they simply have to trigger a build which will run all their tests, code coverage, checkstyle and linting for them. Now they be reasonably confident that whatever code they are about to introduce into master will be stable and won't break their application. All they have to do now is give each other's code a quick read, check the build light for their branch is green and hit that merge button. They've automated their builds and now Alice and Bob don't see getting code into master as an obstacle, now it's just a box ticking exercise!

## CI Servers and Slaves
The great thing about CI is that the CI servers don't do any of the work themselves. They're just a front end that delegates to their workers (or slaves) to do the work in checking out the code and running the build tools against it.

Let's say FooBar Software Ltd. are using Jenkins as their CI platform, and that FooBar Software Ltd. write web applications in whatever language is best suited for the job (be that PHP, Ruby or Python or something else). This means one client's production environment could be very different to another of their client's production environment depending on what languages they used.

That's no problem for Jenkins. They can use a slave running a Ruby environment here and another running PHP or Python over there. If you're using a cloud provider like Amazon Web Services you could clone and spin up more instances should you need them at any point as well. So if you find builds are being queued for a longer time than is reasonable you can create more slaves for your projects to use and Jenkins will delegate the next job it has to run to the available slave.

## Pros & Cons

### Pros
* CI scales up well, add more slaves to run multiple builds at a time
* Configuration files are easy to create and maintain (see ref. #1)
* It will save you time through automation
* Continuous feedback as you commit code can also save you time
* Putting a TV/monitor on the wall in your office as a build screen allows everyone to see the project status (see ref. #2)

### Cons
* Creating new slaves costs money, so does hosting it yourself if your code isn't open source
* If builds take longer than 10 minutes then you need to see what you're doing that takes so much time and maybe schedule a nightly job to perform those checks \[or consider breaking your code up into smaller, independent modules - Ed.\]
* CI servers and their slaves require maintenance, if you don't have people in your team capable of doing this you could find your process blocked if CI stops working

## So CI Will Save Me?
CI is great. Had I known what I know about CI now whilst I was at Uni I would have made great use of it during group projects. University group projects put half a dozen or so students into groups of people they don't know and ask them to build a program to solve a particular problem. In this situation Travis CI thrives. Travis is used mostly by open source projects and is free to use. There is no better way to impress potential employers other than making code available to them and showing how much you care about your code quality by using CI to test it for you.

## About Me

I'm [Steffan Harries](http://www.steffanharries.me.uk), I recently graduated from [Aberystwyth University](http://www.aber.ac.uk/en/cs/) and I'm now working in Cardiff city centre. In my short time in industry I've picked up loads of useful info and best practices from new colleagues and a variety of events in Cardiff. My interests lie in web development, photography and motorsport.

---

## Resources

1. So easy that you can even copy and paste template config files - <http://jenkins-php.org/>
2. This is what your build screens look like right now - <http://www.boxuk.com/blog/pragmatic-wall-displays-for-ci/>
3. Travis CI <http://about.travis-ci.org/docs/user/getting-started/>
4. Jenkins CI <http://jenkins-ci.org/content/about-jenkins-ci>
5. phpci <http://www.phptesting.org/>