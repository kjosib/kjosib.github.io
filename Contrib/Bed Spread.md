# Bed Spread: an Expression-Oriented Code-in-Database System

## Abstract

This project represents an attempt to do for general-purpose programming
what Visicalc did for most common forms of data modelling and analysis.
Drawing inspiration from many corners, we build a reasonable functional
programming system with principle representation in terms of a ubiquitous,
unencumbered, and semantically-empowered storage format: the SQLite
relational database (structured as records for each declaration) rather
than conventional text-files. Existing generic database editors thus
make powerful interim tooling for bootstrapping an ecosystem.

Results are in progress, and conclusions are to be determined.

## Introduction

In 1979, Visicalc (the first spreadsheet program) changed the world.
Its interactive nature, consistent model, comfortable learning curve,
and natural applicability represent a conceptual leap that computing
may never see again. The grid-based interface and library of built-in
mathematical functions made computers into something the masses could
actually use for real work. For over 40 years, spreadsheets have
been *the answer* for run-of-the-mill data modelling and analysis.

**Software developers should be so lucky.**
But mostly, we're not.
We still use a file-oriented interface for working on code and for sharing it among colleagues.
To some degree, this is a consequence of the popular programming languages we use.
Even the ones with an interactive REPL expect modules as files,
and thus implicitly expect that someone will supply a fancy editor for said files.

**Files are not the fundamental abstraction** in software: *That honor goes to functions.*
Files only enter the picture as a clumsy storage-and-retrieval technology
with continuous backward compatibillity to a stack of punched cards.
Yet we build towering edifices such as IDEs and version control systems
atop this semantically-impoverished foundation.

Human factors suffer from our unwillingness to advance our conception of code into the era of Smalltalk or Logo.
**We can and should do better.** We owe it to ourselves.
We have plenty of good and bad examples if we'll only pay attention.

So let's get to work.


## Prior Art / Prevailing Conception

In 1991, Lotus released the first version of [Improv](https://en.wikipedia.org/wiki/Lotus_Improv).
It was a great idea, but commercially unsuccessful for reasons unrelated to merit.
One of its major improvements over conventional spreadsheets was the way formulas
were a separate domain from data, essentially attached to columns instead of cells.
It took a moment to explain the concept, but it's much more powerful and effective
for modelling when your data has any meaningful repetetive structure.
In contrast to the present idea, Improv kept all data within its own walled garden,
acting as the primary U/I for all data modelling, manipulation, entry, and analysis.

Even earlier, the Smalltalk system from Xerox Parc would give up on source files:
all code was in the system image, and the only way to get at it was this original
integrated development environment. The Smalltalk-80 *system browser* heavily
influences the present idea.

Another significant influence is Forth, and in particular the book
[Thinking Forth](http://thinking-forth.sourceforge.net/)
by Leo Brodie. The language itself is mind-altering,
but what's more significant is the overall approach of
building a *composable lexicon with short definitions* that generally fit on one line.

As a kid, I used the Logo programming language on Apple ]\[ computers.
Unlike Applesoft, Logo sported a full screen editor for named functions.
It didn't click at the time, but seeing only one function at any given time
and *not* scrolling around in a document had an important psychological consequence:
it meant I could never be lost.

Later, I had the experience of using [QBasic](https://en.wikipedia.org/wiki/QBasic).
Two concepts stuck with me: the language didn't care about things like the order in which
functions were declared, so the IDE just kept everything in alphabetical order without
you having to do anything. Change the name of a function; it just shows up in the new spot.
And critically, it also had no artificial spacial dimension: at any given time you saw
only the one function you were working on. It wasn't a *folding* editor;
It was a *focusing* editor.

## Approach / Methods / Solution

### Start with an Acheivable Goal
For proof of concept, let's keep it simple and begin with the REPL in mind.
And by "simple" I'm referring for now to a simplistic lisp:
you get strings, numbers, cons cells, and lambdas.
Each time through the REPL maybe you keep local variable assignments,
but user-defined-function bindings are flushed and reloaded from the DB on demand.
That provides immediate feedback for all changes, including via db editors.

The first few built-in functions can be typical string and number operations.
Then some simplistic functions to read and write files.

Such a language remains seriously in "toy" status.
But we can enhance the schema, perhaps, to support some kind of match clause at the top level,
and perhaps data definitions. That leaves implicit run-time type checks,
but it might be enough to write interesting programs.
This early, such a schema change should not be catastrophic on the interpreter.

At this point, it would be auspicous to have some ideas for "interesting" programs:

* Numerical Integration.
* Synthetic (polynomial) division.
* Producing a simple graph of a function, perhaps on the vertical.

The next stage would be some sort of "foreign function" interface.
If integrating to Python, this is near trivial, but might motivate some added syntax.
One downside is access to mutable state, but this remains somewhat in proof-of-concept mode.

Eventually, I anticipate sensible bindings to whatever U/I library originally hosts the REPL,
and then it becomes largely self-hosting except for the runtime core.

By this point, constant use of a database management console would probably get quite old.
So maybe we create a proper freestanding application that has as its core function to edit applications.
This could be applied to the grand unified database, but suddenly there's a motivation for things like shared libraries.

### Bootstrapping

The initial design step identifies four principle concerns:

* Textual: consisting for now of a simple parser for functional expressions.
* Database: a schema for stored functions, organized for the moment into a tree corresponding to a concept of lexical scope.
* Runtime: establishes and implements the semantics of the language.
* Workbench: The interface a programmer uses for both development and ad-hoc interactive queries.

There are a number of side questions. The two most obvious are:

**How do I share code with others?** For example, could I host an open-source project on this ... thing?

* I am deliberately choosing to postpone this decision.
* At some point, I want to layer in a nice collaboration system and library concept.

**How does one build a workbench without already having a workbench?**

* The same way a woodworker does:
  Sequence the project according to functional dependencies and adapt each step to the resources thus far avaialble.

To that end, I started with the parser. My first goal was a read-parse-print loop: evaluation can come later.

### Early Progress

Before long I'd built for myself a simple REPL which initialized by reading function definitions from a database.
Then, I enhanced it by adding support for documents, templates, and records, all stuffed into the same `symbol` table.
It works well enough to demo the concept, but it's not enough to express solutions to interesting problems.

By this point, the apparent major deficiencies were:

* No support for a process concept, and thus no I/O.
* No sum-types, and correspondingly no type-case dispatch, meaning high-order functions basically don't exist.
* No lazy-evaluation, which is pretty useless without some of the above.
* No syntax for literal collections, and indeed no proper collection types.
* No analogue to static nested scope: all declarations are effectively global.
* No type judgments, so that run-time type is all there is.
* No convenient interface: although SQLiteStudio does work, it's far from elegant.
* No clear sense of priorities for the next steps.

On the other hand, there's a PyPI entry called *bedspread* and a perfectly cromulent set of documentation.

### Some Design Ideas

Laziness is super nice to have, but can be postponed until strictly necessary. Pun intended.

Sum-types, type-case dispatch, and a message-passing process abstraction all seem to need a similar concept of
distinct clauses subordinate to a main clause which provides for more general characteristics.

In the particular case of sum-types, the sub-clauses presumably define constructors whereas the main-clause (the symbol)
becomes a generic name for a related group of constructors. Name clashes become possible:
They may be resolved by designs to be determined later.

Function clauses would presumably require a type-case, a guard, and a body (possibly along with a comment).
The same table could be used for sum types and processes, assuming a suitable syntax for type-case and maybe destructuring bind.

For a process concept, I will take inspiration from various sources.
To create a process evidently there are some parameters, and among these are channels.
Let channels be broadcast to all connected listeners, IRC-style.
Delivery is best-effort, non-deterministic, async, and one message at a time.
(i.e. every individual process is effectively single-threaded.)
Let messages on channels be sent with a particular data type.
Listeners are expected to have *receive* clauses to match, or they expire.
(Process lifecycle management can come later, probably in terms of channels.)

The content of a *receive* clause is presumably a tiny procedural element.
To keep things from getting out of hand, I imagine a restricted procedural grammar
catering for *conditional*, *output*, and *become* operations.
Incidentally, the non-*clause* body of a process can be seen as an initiialization procedure.

## Results / Data / Findings / Proof / Discussion

## Interpretation / Significance

## Future Steps

Having all the user-defined code in a proper database opens up vistas to explore:

* Improvements to the Workbench
* Real-Time Collaboration
* Version Management
* Static Analysis Tooling
* Code-Librarian / Packaging Facility

## Conclusion

## References

