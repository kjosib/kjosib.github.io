# Reading List for Software Developers / "Engineers"

I'm assuming you are reasonably fluent in some general-purpose programming language,
and you can make it do a decent variety of cute tricks.
If that's not true yet, probably read this edition of
[How to think like a computer scientist](https://openbookproject.net/thinkcs/python/english3e/).
In fact, read that anyway if you're new-ish to the field -- say, less than a few years experience.

Edsger Dijkstra infamously quipped that software engineering is *how to program when you cannot*.
I do believe that software can be an engineered product, but often it is merely designed.
A good place to start, though, is with his treatise on programming:
[EWD 249](https://www.cs.utexas.edu/users/EWD/ewd02xx/EWD249.PDF)

David L Parnas's seminal contribution on modularity:
[On the Criteria To Be Used in Decomposing Systems into Modules](https://www.win.tue.nl/~wstomv/edu/2ip30/references/criteria_for_modularization.pdf).
TL;DR: Separate *concerns*, not *jobs*, and you will do reasonably well.

* The proper domain of a module is abstract data types and the operations among them.
There's a paper I mean to track down which explains this.

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

[The Sixth Stage of Debugging](https://levelup.gitconnected.com/the-sixth-stage-of-debugging-20d245172ffd)

[Mocking is a Code Smell](https://medium.com/javascript-scene/mocking-is-a-code-smell-944a70c90a6a)
However, when reading this, please keep in mind a few points:

* The author is focused on unit tests, not integration tests.
* At least in Python, I've often seen both unit- and integration-tests use the same `unittest` framework.
* The corresponding sin for integration tests is excessive monkey-patching (e.g. ``mock.patch``).

I will add to this list as things occur to me.

