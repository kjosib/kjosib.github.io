# Thoughts on Code Quality

I was frustrated at my own speechlessness when a colleague asked me what was wrong with a certain module which I'd spent an alarming fraction of the past week straining to comprehend. (Needless to say, I spent then next few minutes being gob-smacked by how completely differently the two of us seemed to see the module's code quality.) That evening I resolved to give the man a proper answer regardless. In some sense, this page is that answer.

## Perceiving Quality: an Introductory Allegory

### In vino veritas.

In my neighborhood, good wine gets you drunk.
In Millionaire Acres, good wine has a high numerical score
from some oenological institute that I've never heard of.

I had a friend-of-a-friend in college who used to make trash-can wine in
the dorm room closet. It had funny flavors, odd smells, unpleasant aftertaste,
a cloudy appearance, and it left you with strange intestinal phenomena the next
day, but boy oh boy *it got you drunk*.

I think, even in my neighborhood, that would be considered bad wine.
Let me be clear: The Rubbermaid Brute that served as fermentation vessel
was not *the thing* that made the wine *bad*. However, said sanitation
equipment certainly did not help matters. Other contributing factors included
poor temperature stability, slipshod procedures and equipment generally,
dubious ingredients, hard water, and a general lack of concern for the
experience of savoring a fine beverage. In that one brewer's own opinion,
he was making perfectly good wine: It got him drunk when he chugged it.

### Objective Quality: Fitness for Purpose

It's easy to dismiss the question of wine quality as a matter of taste,
but there some things that we should all agree are bad wine.
For instance, wine that makes people blind is terrible wine,
regardless of how it may taste.
Any objective measure of quality needs to take purpose into account.

The purpose of wine is manifold:
* It gets you drunk.
* It refreshes.
* It lubricates social gatherings.
* It takes part in religious rituals.
* It is safer than the dubious water from which it was made centuries ago.

Wine can be measured by its ability to do any or each of those things.
Wine which fails on too many counts is objectively not very good.


## Desiderata

In his article [What Does Good Code Look Like?](https://spin.atomicobject.com/2015/03/04/good-code/ ),
Jesse Hill gives brief but insightful commentary on the following desirable characteristics of good code:

* Lucid / Easy-to-Read
* Organized
* Testable
* Simple

To these I would add:

* Solves the right problem
* Sensibly [documented](/documenting.html)
* Clean and Tidy

## Rationale


I mostly subscribe to the [Dijkstra school](https://www.cs.utexas.edu/users/EWD/), which is a bit purist:

* Code is not for machines to execute, but a symbolic representation of classes of possible computations.
* Only incidentally, we have these wonderful machines which can perform those computations at blinding speed.
* Our job is not to *write code per-se*, but to develop **classes of computations** which serve our employers' needs.
* Our chief difficulty is the human mind's extremely limited ability to keep track of interlocking details.

However, unlike Dijkstra (who infamously called software engineering "how to program when you cannot"):

* Software can be an *engineered product* subject to standards of
[professional ethics](https://ethics.acm.org/code-of-ethics/software-engineering-code/).

From day to day we make our living by changing existing code.
(Only rarely will that *existing code* be an empty module.)
Activities involved in this task include:

* reading (both code and documentation) for comprehension
* exploration and navigation
* quality assurance
* adjustment to accommodate new requirements
* all the collaborative [metawork](https://quadrabits.com/2016/11/15/metawork/) involved in the development process

Therefore, the elusive measure of *code quality* is whatever influences the cost of those activities on an ongoing basis.
The same can be said of the quality of the development process overall.

An entire essay could be written about each point, and some of their consequences.
I might do that someday. Today is not that day.
Meanwhile, if you read Dijkstra, you're off to a pretty good start.
In particular, his [class notes](https://www.cs.utexas.edu/users/EWD/ewd02xx/EWD249.PDF) gives a pretty good
overview (despite embedding some outdated cultural assumptions).

## Techniques

Mark Jordan writes in
[How to actually write good code](https://medium.com/ingeniouslysimple/how-to-actually-write-good-code-b355b3f9e4ae)
about a number of specific techniques. Among them are:

* Constraints, such as:
  * Strongly typed languages
  * Immutable value-objects
  * Pure functions
  * Single-assignment
* Design tenets, such as:
  * Composition over inheritance
  * Decision/Action Boundaries
  * [Dependency Injection](https://en.wikipedia.org/wiki/Dependency_injection)
* Heuristics, such as:
  * Respecting and acting on code smells

To these I would add:

* Read-me driven development.
* Proof-driven development.
  (See [correctness by construction](https://www.google.com/search?q=correctness+by+construction)
  for the logical extreme of this idea.)
* Top-down elaboration.

## Case Study: Short Methods

Once again, I begin with an allegory:

* The Supreme Court of the United States is considered legally infallible.
* This causes great consternation among lay people familiar with Plessy v. Ferguson.
* SCOTUS is also legally final: they have the *last word* on any question
  that comes before the judicial system of the United States.
* SCOTUS is not final *because* it is infallible. It is infallible *because* it is final.
* Apparently, SCOTUS is only *mostly* final in practice. But this is a digression.

Search, and ye shall find no end of different ideas on how long a method may
become before it must be broken up. It's almost as if people believe method
size determines how easy it is to work on code.

* The code is clear and pliable **not because** it has short methods.
* Rather, the code **has short methods because it is clear and pliable.**

Probably the most extreme short-method coding is common in APL and its closest cousins.
(If you're curious, [this book by Kenneth Iverson](http://www.softwarepreservation.org/projects/apl/Books/APROGRAMMING%20LANGUAGE)
is the definitive source on APL.)
In practice, though, most people find APL to be inscrutable.
So instead, let me refer you to the book
[Thinking Forth](http://thinking-forth.sourceforge.net/), by Leo Brodie.
It truly deserves to be considered a software-engineering classic.

Let me restate one of the design tenets from the Brodie book, gently adapted to
the languages popular in industry today:

If you set out to write methods that clearly express both their
intent and function, with but a single level of abstraction between the *what*
and the *how*, then **in consequence** you wind up with short methods.
You also end up with a **lexicon** of words related to the topic of ... whatever
it is your program or module happens to do. We do not set out to golf the code.
Rather, we golf the *level of effort required* to understand and modify it.

Sometimes, during incremental maintenance, you find a method of such size
and complexity that it is hard to comprehend. The time you spend trying
to understand it anew will be much better repaid if you close the loop by
casting your new comprehension in the form of a few well-chosen words added
to the lexicon and corresponding adjustments to the original method to use
the new words appropriately.

## One Final Exhortation

Code as if your tired colleague will have to explain everything to a new-grad in
six months, after you've had time to forget the details and stumbling blocks.

* If the project goes well, something like this will happen.
* Regardless, you'll have a much lower
  [WTF/minute](http://reviewthecode.blogspot.com/2016/01/wtf-per-minute-actual-measurement-for.html)
  metric.
