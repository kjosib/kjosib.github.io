# Reading List for Software Developers / "Engineers"

## Getting Started?

Thirty years ago, I would have told you to learn Pascal.
It remains a considerable improvement over most of its successors,
but for a variety of reasons it's no longer the top choice for an introduction to the field.

If you don't know a programming language, you could do a lot worse than this edition of
[How to think like a computer scientist](https://openbookproject.net/thinkcs/python/english3e/).
In fact, read that anyway if you're new-ish to the field -- say, less than a few years experience.
You'll also learn Python along the way, if you haven't already.

## Think you know a few things?

Twenty-five years ago, someone pointed me to Structure and Interpretation of Computer Programs,
and said I should read it. This book is MIT's introductory computer-science text.

* [full text - front page] https://mitpress.mit.edu/sites/default/files/sicp/full-text/book/book.html
* [full text - table of contents](https://mitpress.mit.edu/sites/default/files/sicp/full-text/book/book-Z-H-4.html)
* [web site](https://mitpress.mit.edu/sites/default/files/sicp/index.html)

At the time, I was a cocky young hot-shot with two thirds of a degree and a bottle of PHP3 in my hand.
I didn't know the value of what I'd been told, and anyway the web wasn't yet so mature as to
let me read for free what I've linked above. So I didn't read it right away. Thankfully,
I eventually got around to reading it.

For context, the degree I had two thirds of would have been from the University of Texas at Austin,
back when Pascal was still *God's Gift to Introductory Programming* by way of the prophet Niklaus Wirth.
The point is I had a solid foundation -- or so I thought.

By the time I finally got around to reading this book, it really opened my eyes to the rest of the story.
Sure, it starts at the very *very* beginning ... but then picks up speed rapidly.
Exploiting the [andragogical](https://en.wikipedia.org/wiki/Andragogy) advantages and spartan minimalism of the language *Scheme*,
the authors take us on a deep and enlightening tour of the essence of software in a number of different paradigms
while completely bypassing such tangential gobbledygook as `public static void main(String[] argv) {`,
which really has no place usurping our attention from a theoretical overview.


* [Lambda? You keep on using that letter...](https://youtu.be/Y7StjYhXvpE)

## People First!

https://youtu.be/kamyxB-yKrc is the work of a man who does a lot of videos on aircraft near-misses.
This video is a little different, and highlights the importance of proper leadership.

## Stupid Human Tricks, Programming Edition

This section is pointers to articles on general good and bad practice.
(At the moment, very few.)

* This [Java-specific style guide](https://openjdk.java.net/projects/amber/guides/lvti-style-guide)
  on a specific feature nevertheless includes a lot of generally-good ideas regardless of language.
* [Single-letter names - a cautionary tale](https://hilton.org.uk/blog/single-letter-names-tale)
  hammers the gong on meaningful identifiers.
* [Object-Oriented Programming is Bad](https://www.youtube.com/watch?v=QM1iUe6IofM), by Brian Will,
* [On the Role of Scientific Thought](https://www.cs.utexas.edu/users/EWD/transcriptions/EWD04xx/EWD447.html)
  proposes a reason sound practice got off to a slow start, and debuts the phrase "separation of concerns".
* Dijkstra's [My hopes of computing science](https://www.cs.utexas.edu/users/EWD/transcriptions/EWD07xx/EWD709.html)
  deals with elegance, simplicity, programming as such, and indirectly why debuggers are a symptom not a cure.

[The Effective Arrangement of Logical Systems](https://www.cs.utexas.edu/users/EWD/transcriptions/EWD05xx/EWD562.html)
focuses on the value of and need for well-defined interfaces.
One logical consequence is that it's generally worthwhile to factor out
independently-meaningful sub-programs even when those sub-programs are only invoked once.

I was looking for something else and stumbled over
[this document about learning](https://fortelabs.co/blog/progressive-summarization-v-the-faster-you-forget-the-faster-you-learn/)
which proposes to elevate the importance of forgetting.
It's a sideways take on the subject, but there are some useful truths buried therein.

## Software as an Engineered Product

Starting in this section,
I'm assuming you are reasonably fluent in some general-purpose programming language,
and you can make it do a decent variety of cute tricks.
However, seventeen syllables do not a haiku make.

Edsger Dijkstra infamously quipped that software engineering is *how to program when you cannot*.
I do believe that software can be an engineered product, but often it is merely designed.

Take a moment to think about what *engineering* means in any other context than software.
What does a process engineer or a mechanical engineer do all day long?
The answer is a number of things, but among them you will find:
* Living up to a [professional code of ethics](https://www.acm.org/code-of-ethics).
* Applying technical knowledge to design solutions to hard problems.
* [Documenting the work thoroughly](documenting.md),
  and delivering that documentation to the client as part of the deal,
  for a laundry-list of excellent reasons.
* Taking [personal responsibility](https://www.acm.org/about-acm/risks-forum) for the work.

As an adjunct to the usual form of software documentation,
I would encourage anyone and everyone to have a look around http://www.literateprogramming.com/
for inspiration. Invented by [Donald Knuth](https://www.google.com/search?q=Donald+Knuth),
the idea is to put exposition foremost, with the idea that software is *read* much more often
than it is *written*. In a significant money-where-mouth-is way, this idea is vindicated
through Knuth's vaunted **TeX** computerized typesetting system. Along with **MetaFont**,
the two systems are written with literate programming and are subject to the first and
[most prestigious bug-bounty program ever](https://en.wikipedia.org/wiki/Knuth_reward_check),
but in over 40 years of their existence, they've netted a shockingly small quantity of bugs.
(Although it may be hypthesized this is a consequence less of the development methodology
and more of the fact that a *literal* God of Computer Science wrote it....)

A good place to start, though, is with his treatise on programming:
(I'm afraid I've lost track of the link. I'll find it eventually.)
Fair warning: It is at times tedious, dense, or guilty of the occasional outdated stereotype or
cultural reference. On the plus side, it's broken into meaningful and mostly-independent chapters.

If you're up for some heavy lifting, 
[EWD 249: Notes on Structured Programming](https://www.cs.utexas.edu/users/EWD/ewd02xx/EWD249.PDF)


David L Parnas's seminal contribution on modularity:
[On the Criteria To Be Used in Decomposing Systems into Modules](https://www.win.tue.nl/~wstomv/edu/2ip30/references/criteria_for_modularization.pdf).
TL;DR: Separate *concerns*, not *jobs*, and you will do reasonably well.

* The proper domain of a module is abstract data types and the operations among them.
[On representational abstraction](https://www.cs.utexas.edu/users/EWD/transcriptions/EWD03xx/EWD393.html),
just begins to hint at abstract data types, but doesn't fully develop them.
[This set of course notes](https://www.cs.princeton.edu/courses/archive/fall14/cos217/lectures/10_ModularityHistory.pdf)
attempts to trace some of the history behind this, but doesn't quite make that final leap.

[Why Functional Programming Matters](https://www.cs.kent.ac.uk/people/staff/dat/miranda/whyfp90.pdf)
will both *motivate* and familiarize you with the benefits of truly *functional* programming.
Read it: you'll crave referential transparency and maybe even lazy evaluation.

[Simple Made Easy](https://www.infoq.com/presentations/Simple-Made-Easy/) is a web-hosted presentation.
(It has a video feed and a separate portion of the browser window used for slides.)
The hour you invest to watch this presentation will be repaid ten thousand times
in terms of increased quality of life for yourself and your colleagues.

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

[On the Maintenance of Classic Modula-2 Compilers](https://arxiv.org/pdf/1809.07080.pdf).
This lays out the principles of design-for-maintainabillity.

[On Understanding Data Abstraction, Revisited](https://www.cs.utexas.edu/~wcook/Drafts/2009/essay.pdf),
by William R. Cook, University of Texas at Austin.
What is the relationship between *objects* and *abstract data types* (ADTs)?
This paper explains the differences between these forms of data abstraction in ways your textbook never mentioned.

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

**Something Simpler:**
Gary Bernhardt has a nice article entitled
[Test Isolation Is About Avoiding Mocks](https://www.destroyallsoftware.com/blog/2014/test-isolation-is-about-avoiding-mocks)
in which (among other things) he illustrates the connection between mock-nesting-depth and design-coupling-depth.
The overt theme is that better design (i.e. less-coupled, more flexible) automatically allows easier, simpler testing.
But along the way, he does not miss the opportunity to plug *functional-core, imperative-shell* as an architecture pattern.

**Synthesis:**
Naturally I have my own [Vehement words about software testing](code_test.md).
These words are far from being an exhaustive treatise, but they hit the main issues I see in practice.
Topics include:
* The nature, purpose, and promise of tests
* Designing programs with effective testing in mind
* Designing effective tests with program flexibility in mind
* Testing practices and culture

**Elements of Style:**
[Mocks Aren't Stubs](https://martinfowler.com/articles/mocksArentStubs.html)
is Martin Fowler's cogent explanation of two major styles of unit testing,
and the tools and philosophies that guide them. Personally, I find the classic
style more compelling in almost every case: *I do X, the result should be Y.*
That's a meaningful and falsifiable proposition. The result I want is usually
just a return value. If I/O is on the line, I'll pass in a fit-for-purpose fake
dependency and check the post-condition by interrogating the fake.
Yes, that means I have to verify that the fake API is sufficiently realistic.
Java has interfaces for that. Python has -- well -- the lesson is over for today.

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

[Getting Shit Done](https://www.rea-group.com/about-us/news-and-insights/blog/getting-shit-done/)
is one part bleary nostalgia, three parts cool reflection, and nine parts wise counsel of lessons
the author prays his colleagues might embrace from the excesses and vicissitudes of the past.


## The Industry
[Programming methodologies, their objectives and their nature](https://www.cs.utexas.edu/users/EWD/transcriptions/EWD04xx/EWD469.html)
begins with a critical look at how things once were,
then develops a case for a style of working amenable to formal treatment,
and finally looks to a future which, even five decades later,
may still have been a touch idealistic.
*To be fair, things have moved quite far in the right direction, but the dream is still in the distance.*

[Ctrl-Alt-Del: Learning to Love Legacy Code](https://youtu.be/wPjHuvulivM?t=627)
(link skips parody cover-song and movie clips)
turns an inevitable challenge in the computing industry into something we can actually appreciate.

*The Mythical Man-Month*, by Fred P. Brooks Jr., is to software engineering what
*[The Wealth of Nations](https://www.gutenberg.org/ebooks/3300)*
is to economics. The author had a unique position of oversight in IBM's systems division
at a time when dinosaurs walked the earth. Er, mainframes ruled the computer room, that is.
He was probably the first to write and publish from a perspective of actually understanding the nature
of large software projects and the coordinated efforts of groups to create them. You can find
[an early edition](https://web.eecs.umich.edu/~weimerw/2018-481/readings/mythical-man-month.pdf)
online if you poke around long enough, but do yourself a favor and
[buy the book.](https://www.amazon.com/Mythical-Man-Month-Software-Engineering-Anniversary/dp/0201835959)

Anyone who's thought about teaching the subject should read
[On the cruelty of really teaching computing science (EWD 1036)](https://www.cs.utexas.edu/~EWD/transcriptions/EWD10xx/EWD1036.html)
which pulls no punches but is absolutely on point.

## Fun Stuff

* [A Brief, Incomplete, and Mostly Wrong History of Programming Languages](https://james-iry.blogspot.com/2009/05/brief-incomplete-and-mostly-wrong.html)


## Updates

I will add to this list as things occur to me.

