---
layout: book-chapter
title: Measuring Success
prev: '<a href="maintainability.html">Prev: Maintainability</a>'
next: '<a href="promote-yourself.html">Next: Promote Yourself</a>'
---

# Measuring Success

_By [Christopher Gilbert](#about_me)_

What is a suitable measure of success in software development?

When I was at University, the measure was simple: I was awarded a pass, a merit or a distinction, depending on how much of the assessment criteria I achieved. When I finished an assessment, I simply progressed onto the next one. Generally speaking, this process was repeated each time.

It was with this mindset that I embarked on my first job as a graduate software developer. My first job was perhaps a little unusual, in that I worked for a game development company, and I was very fortunate to be accepted for a graduate role. As it turns out, despite having put in many thousands of hours of extra-curricular development time, I was still unprepared for commercial development.

In game development, the quality of your software is assessed by the platform vendor in their quality assurance labs, in accordance with the Technical Certification Requirements. Absolutely no software will be released without certification from the platform vendor, and the criteria is remarkably strict. If the software crashes at all whilst under assessment, you get an automatic fail. When that happens, you are expected to fix the crash bugs and resubmit, with the caveat that resubmission will cost a rather large sum of money, in the region of several thousands of pounds.

In addition to technical certification, the publisher is paying your development costs, and expects regular progress. A project is divided into milestones, and for each milestone the requirements are laid out. Every month, the software is delivered as an installable package. This is checked by their quality assurance team, who also assist in finding and reporting bugs. You are expected to fix anything they find in time for the next deliverable milestone, along with the rest of your deliverables.

In the world of commercial software development, there is no merit and distinction. You are expected to achieve 100% of the criteria every time, and you are expected to deliver software which is free from defect. It is very rare that a defect or missing functionality is acceptable from a user experience point of view, and this is reflected in employers' expectations. An experienced developer knows this expectation, and plans to deliver right from the beginning of the project.

Fortunately, there exists today a huge number of tools that allow developers to improve their ability to deliver high quality software as standard. As a professional, I do not like to leave the success of my software down to luck, or hope that nobody notices. I actively search for defects, and when I find a defect I do not wait for someone else to fix it for me. I fix it immediately _and_ I find a way to automate its discovery so I can ensure that it does not happen again. This mindset of preventing mistakes before anyone else notices I feel is the primary distinction between an amateur and professional, and is surely something that every developer learns the hard way.

There is a term given to issues that are not fixed properly, known as _technical debt_. Technical debt is the result of implementing a change that does not address a core issue, and introduces a discreet limitation for yourself or other developers. The reasons for accruing technical debt can be many, but more frequently it will be the result of a time constraint. Instead of solving the core issue, the developer writes a hack, something that seemingly fixes the problem for now. In the short term, you are able to release your software, but now your software is less reliable, or takes longer to develop. Code has a habit of being passed along to other developers, and it is frequently the case that those developers will pay a price for having to work around your hack, and maybe even write a few hacks of their own. Every time developer hours are spent working around the problem, they are paying the price of the technical debt, until the debt is repaid by fixing the core issue.

In the real world, you will rarely work alone. It is not uncommon to work in teams of 20 developers or more, often spanning a range of levels of experience. When you work alone, a defect affects only yourself, but if a defect costs 1 hour of wasted time and if you work with a team of 20 developers who each waste 1 hour of time, then you have quickly wasted several man-days of development time.

These problems can get even worse. If your defect isn't caught by anyone else and a customer notices, then it could cost you that customers' business, which might be worth more than your salary!

At University, obtaining 75% is considered a distinction; in the commercial world, professional developers consistently score 99% all the time. Success should be repeatable by automating testing, and by using development tools and processes that support the goal of creating a fantastic software product that is free from defects. They should also allow other developers to contribute and collaborate with ease.

This alone was the single most important lesson that I learned in my first year of employment, but knowing is only half the battle.

## About Me

Chris currently works as a C++ developer for [DataSift](http://datasift.com).