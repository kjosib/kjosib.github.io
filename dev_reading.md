# Reading List for Software Developers / "Engineers"

## Getting Started?

Thirty years ago, I would have told you to learn Pascal.
It remains a considerable improvement over most of its successors,
but for a variety of reasons it's no longer the top choice for an introduction to the field.

If you don't know a programming language, you could do a lot worse than this edition of
[How to think like a computer scientist](https://openbookproject.net/thinkcs/python/english3e/).
In fact, read that anyway if you're new-ish to the field -- say, less than a few years experience.
You'll also learn Python along the way, if you haven't already.

## Software as an Engineered Product

Starting in this section,
I'm assuming you are reasonably fluent in some general-purpose programming language,
and you can make it do a decent variety of cute tricks.
However, seventeen syllables do not a haiku make.

Edsger Dijkstra infamously quipped that software engineering is *how to program when you cannot*.
I do believe that software can be an engineered product, but often it is merely designed.
A good place to start, though, is with his treatise on programming:
[EWD 249](https://www.cs.utexas.edu/users/EWD/ewd02xx/EWD249.PDF).
Fair warning: It is at times tedious, dense, or guilty of the occasional outdated stereotype or
cultural reference. On the plus side, it's broken into meaningful and mostly-independent chapters.

David L Parnas's seminal contribution on modularity:
[On the Criteria To Be Used in Decomposing Systems into Modules](https://www.win.tue.nl/~wstomv/edu/2ip30/references/criteria_for_modularization.pdf).
TL;DR: Separate *concerns*, not *jobs*, and you will do reasonably well.

* The proper domain of a module is abstract data types and the operations among them.
There's a paper I mean to track down which explains this.

[Why Functional Programming Matters](https://www.cs.kent.ac.uk/people/staff/dat/miranda/whyfp90.pdf)
will both *motivate* and familiarize you with the benefits of truly *functional* programming.
Read it: you'll crave referential transparency and maybe even lazy evaluation.

[Simple Made Easy](https://www.infoq.com/presentations/Simple-Made-Easy/) is a web-hosted presentation.
(It has a video feed and a separate portion of the browser window used for slides.)
The hour you invest to watch this presentation will be repaid ten thousand times
in terms of increased quality of life for yourself and your colleages.

I wrote down a few [thoughts on code quality](code_quality.md) some time back. So have many others.
That's why I linked to several primary sources. Speaking of:

One of the all-time classics has got to be
[Thinking Forth](http://thinking-forth.sourceforge.net/)
which you can either read online, download a PDF, or get a paper copy.
Although the source language is peculiar if not arcane,
I count this a strength and not a weakness:
Software development principles transcend any particular programming language,
so the extra few brain cells engaged in groking the examples will be gainfully employed.

Anyone concerned with concurrency should read Charles Anthony R. Hoare's article
[Communicating Sequential Processes](https://www.cs.cmu.edu/~crary/819-f09/Hoare78.pdf).

[Don't Fear the Monad](https://www.youtube.com/watch?v=ZhuHCtR3xq8) is about an hour long,
and it will leave you actually understanding monads.
That's not to say you'll be all set to design great ones,
but at least you'll truly understand what they are, how they're put together,
and (with any luck) why you want them.

[The Codeless Code](http://thecodelesscode.com/contents): *An illustrated collection of (sometimes violent) fables concerning the Art and Philosophy of software development, written in the spirit of Zen kōans.*
You'll have to poke at the interface to read from the beginning.
And also read *The Applicant*, and every other scrap on that same web site.

[WAT](https://destroyallsoftware.com/talks/wat) packs grand wisdom about design
into less than five hilarious minutes of biting satire.

[On the Maintenance of Classic Modula-2 Compilers](https://arxiv.org/pdf/1809.07080.pdf)

## A focus on testing

**Let's begin at the beginning:**
Circa 1971, Edsger Dijkstra, the grand-daddy of formal methods, wrote in
[On the reliability of programs](https://www.cs.utexas.edu/users/EWD/transcriptions/EWD03xx/EWD303.html)
not only of the "software crisis", but also gave the first *and only* viable path to reliable software:
* Consider a program to be a *mathematical artefact*.
* Demand a (more or less formal) proof-of-correctness.
* Develop said proof hand-in-hand with the program.
* Eliminate all possible *sources* of error.
* Apply the right kinds of abstractions and stick to what we can understand.
* Testing and debugging are hopelessly inadequate for software quality, although they may uncover clerical errors.

**Point:**
[Integrated Tests Are A Scam](https://vimeo.com/80533536) is a 65-minute video presentation
in which J. B. Rainsberger:
* lays out the problem with "integration tests" (in common practice),
* sketches a clear solution for how to do testing the *isolated* way,
* illuminates the positive impact this makes on architecture and design,
* and finally gives a straightforward proof, in terms of mathematical induction, that the method is reliable.

Rainsberger's approach is a solid one: define interfaces, test contracts and collaboration, and then
*[it's turtles all the way down](https://en.wikipedia.org/wiki/Turtles_all_the_way_down)*
until you reach a trusted boundary. At that point, you can work to minimize the surface area of that boundary.

**Counterpoint:**
In [Mocking is a Code Smell](https://medium.com/javascript-scene/mocking-is-a-code-smell-944a70c90a6a),
Eric Elliot surveys from the opposite extreme: a quagmire of too many defined, tested, and *mocked* APIs,
which collectively paralyze efforts to respond to changing requirements -- generally due to coupling.
His central tenet might be this quote: *Mocking is required when our decomposition strategy has failed.*
He then proceeds to lay out a panoply of techniques and prescriptions for removing various design errors.

**Synthesis:**
Naturally I have my own [Vehement words about software testing](code_test.md).
These words are far from being an exhaustive treatise, but they hit the main issues I see in practice.
Topics include:
* The nature, purpose, and promise of tests
* Designing programs with effective testing in mind
* Designing effective tests with program flexibility in mind
* Testing practices and culture

**Humor:** Embedded near the beginning of
[The Sixth Stage of Debugging](https://levelup.gitconnected.com/the-sixth-stage-of-debugging-20d245172ffd)
comes the mentioned list of six stages. Fair warning: the rest is psychobabble of dubious profundity.

## Software as a way of life

[Things you should never do, Part 1](https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/)
is Joel Spolski's experiential rant about the terrible idea it usually is to wipe the slate and start from scratch
when you already have a functioning (if perhaps crufty) system.
* Joel's advice on this topic is almost always correct. In particular, it is probably correct for your current project.
* It may seem at odds with Fred Brooks' advice to [Build one to throw away](https://wiki.c2.com/?PlanToThrowOneAway).
  Rapid prototyping has value, but Joel writes of production-stage projects. You know: the ones in danger of
  [Second Second Effect](https://wiki.c2.com/?SecondSystemEffect).
* Joel has a good head on his shoulders: Most of the rest of https://www.joelonsoftware.com is worth reading too, or maybe spring for his book.
* [Rob Landley's Reply](https://www.landley.net/writing/stuff/2007-05-14.html) has a few good counterpoints,
  but he does not reverse the main thrust.

[Two Is An Impossible Number](https://wiki.c2.com/?TwoIsAnImpossibleNumber) starts with some good advice about
design in the face of optionality: Once *A* and *B* are allowed, then *C..Z* are not far behind.
As with any proverb, you have to apply common sense: If you squint just right,
you can almost make out a case for premature generalization. But that would be premature.

## The Industry

Anyone who's thought about teaching the subject should read
[On the cruelty of really teaching computing science (EWD 1036)](https://www.cs.utexas.edu/~EWD/transcriptions/EWD10xx/EWD1036.html)
which pulls no punches but is absolutely on point.

*The Mythical Man-Month*, by Fred P. Brooks Jr., is to software engineering what
*[The Wealth of Nations](https://www.gutenberg.org/ebooks/3300)*
is to economics. The author had a unique position of oversight in IBM's systems division
at a time when dinosaurs walked the earth. Er, mainframes ruled the computer room, that is.
He was probably the first to write and publish from a perspective of actually understanding the nature
of large software projects and the coordinated efforts of groups to create them. You can find
[an early edition](https://web.eecs.umich.edu/~weimerw/2018-481/readings/mythical-man-month.pdf)
online if you poke around long enough, but do yourself a favor and
[buy the book.](https://www.amazon.com/Mythical-Man-Month-Software-Engineering-Anniversary/dp/0201835959)

## Updates

I will add to this list as things occur to me.

