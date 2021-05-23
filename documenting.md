# Writing Documentation:

Much has been, and will be, written on how to document computer programs.
What follows is my own feeble contribution to the mix.


## Why We Write

Maybe we've all had the experience of coming back to some bag-nasty forgotten code we wrote six months ago. Maybe you cursed the anonymous author until you realized who it was. Maybe you flailed about in flabbergasted disbelief. Maybe you hung your head in shame.

Maybe you even resolved to do something about it, but never felt like you had time?

> There's a case to be made that new graduates won't actually have had this experience just yet. Why? Well, they work on a project for a semester and then it's history. Next semester; next project. Very little motivation to look back at old code.
>
> Later, after you stay at the same project for a while, you eventually hit that milestone of identifying with the proverbial "maintainer".



## How to Get Actually Started (For Real This Time)


In point of fact, documentation is an investment. Like our retirement account, it works best if we:

* consistently put a defined (sustainable, non-zero) fraction of our efforts toward the investment, and
* apply a sensible investing strategy based on our current situation.

Can we leverage that investment to reap rewards of speed, quality, reliability, and maintainability? *Yes, we can.*

The sections that follow are organized from low-level to high-level.
You'll find low-level documentation easier to work on in very small bites.
The higher-level stuff will require greater collaboration with team-members but will probably have a proportionally higher pay-off for progress made.


## Functions/Methods/Procedures/Subroutines

Most languages these days have some sort of convention for API documentation extracted
directly from the source code. That's a good place for it, because you don't have to
switch tools and anyway the commentary is right there next to the code. Let's call
this the *doc-comment*, regardless of how it's physically done in your favorite programming contraption.

The effort to compose documentation at this level *as you write the code* is rather akin to that of "developing proof and program in tandem" which Dijkstra advocated.
In my eyes, the "correctness criteria" for a subroutine is given in the doc-comment and then the body code is required to behave as advertised.

I'm asking that you write a quality doc-comment in synchrony with writing any new function. (You'll often find it's easier and more informative than writing a unit test.)
For modifications to existing functions, it's sufficient to leave things even slightly better than you found them: maybe improve the aspect of the doc-comment that most
pertains to the change you made. And for bug-hunts? Well, if you learn something along the way, this is a good time to write it down.


### What about the saying *"trust only code"*?

You can argue the point of code/comment getting out of sync: the "trust only code"
idea. That's wrong: The code is the code. The doc-comment is the requirement, stated
in human language, which the code is meant to implement. The requirement is law. The
code is behavior. If they disagree, the fault lies most probably in the code.
Still, you should trace your requirements and testing before making changes willy-nilly.


### What should the doc-comment look like?

It should probably have a structure like this:

| Element | Examples/Cases/Details |
| --- | --- |
| Plain English *Command Form* | Tell what the function does *from the caller's perspective*. "Fetch a pail of water." or "Return twice the argument." |
| Optional Hyperlink | If the function implements something published in an academic paper or book, link to a reference. If it's an xUnit test case related to a bug or feature request, link to the corresponding ticket in your tracking system. |
| Signature Clarifications | Semantics of parameters and return values/exceptions. |
| Contract | Preconditions, postconditions, or performance guarantees. |
| Fine Print |  Any further nuance that must be kept in mind when calling this function. (e.g. Remember to later call XYZ.) |
| Policy * | If the function *implements a defined policy*, then explain *what* that policy is, and *why* that policy applies (or link to a canonical reference). |
| Background | Any help to understand why this function exists or why you might want to call it. (e.g. it was found to reflect a common pattern of control and factored out.) |

Where it makes sense, `doctest`-style examples may be interspersed into the above structure to illustrate points.

Two things are important to leave out:

* Noise: Anything blindingly-obvious from either the function's formal signature or preceding sections -- but error on the side of helping the new guy out.
* Internals: The doc-comment is about *interface, not implementation*. The place for implementation commentary is -- well -- ordinary comments in the code.

Now you have a clear specification. The corresponding code should follow naturally.

### Define "Policy"?

The real meaning of "policy" in the doc-comment is for when the behavior of a function is specifically dictated by some system requirement. For instance, if you're never supposed to have more than six people in the fitting room because the corporate loss prevention department said so in circular A-12-26-B, then somewhere between *[event:let-me-in]* and *[event:right-this-way]* is the number 6, and *that number implements policy* so the surrounding function (or module, etc...) had best link back to circular A-12-26-B!

Policy should be distinguished from the arbitrary or design-driven selection of mechanism.

For instance: Suppose you're writing a function to assign players to teams. Do you:

* Select randomly?
* Try to equalize the strength of the teams?
* Try to minimize interpersonal conflict?

Sometimes it's up to you. The caller doesn't care; she just needs teams and the mechanism is up to you. In this case, *the callee decides mechanism*. As such, you've got some thinking to do: Which way of allocating teams is best in this context? Why? Is there a source or standard behind your reasoning? Document it -- but where? If you consider this a private implementation detail subject to possible change, then put it as a normal comment, and explain as much. If you consider this to be a done decision which clients may potentially rely on, then it's part of the postcondition. And if there's a local rule that says you have to do this a certain way, then mention that rule in the *policy* section of the doc-comment.

There are going to be cases where the caller expects you to specifically follow one of these strategies. If so, then that expectation forms a part of the API and *choice of mechanism comes from the caller*, so you are implementing mechanism (not policy). Again, include the choice as part of the postcondition in the contract. Incidentally, you may also want to name the function in some way that reflects the expectation.



### What about body-code comments?

Assuming your doc-comment is written decently, remaining code comments have basically two purposes:

1. Clarify *what* (some section of code) is doing, explained at a higher level.

In this case, stop and see if you can extract a function.
It doesn't matter how small, or whether it's only called once ever.
You've identified a meaningful unit of abstract computation.
Stop worrying and learn to love functional abstraction.
It's our primary means to conquer complexity.


2. Clarify *why* (some section of code) is designed this particular way, either in contrast to something (apparently) simpler or just as pure educational content.

First, decide if the added complexity is worthwhile. If the answer is yes, then GREAT! Leave this in.
Don't go overboard, but this is the kind of commentary that makes maintainers happy.

3. There is no *how*. The *how* is in the code, and the code only -- although you may be confusing this with case #1, above.

## Documenting (Object-Oriented) Classes

Things like these should go in a class's docstring:

* What's its responsibility? (Free clue: A class should have a clear and simple purpose or responsibility.)
* What roles does it play? (E.G. does it participate in a well-known [design pattern](https://en.wikipedia.org/wiki/Software_design_pattern)?)
* What other classes (or interfaces) does it collaborate with?
* What observable guarantees does the class make? (I.E. the external class-invariant)
* What external conditions does the class rely on for its own correct behavior?

Additionally, just below the docstring you should probably make note of any internal class-invariants which your implementation relies on for correctness, because these are not always obvious just from looking at method body code. 


## Interfaces, Abstract Classes, and Type Classes.

In modern functional programming, you hear of "type-classes". This concept is more like an abstract data type, but expressed in terms of the operations any concrete manifestation of that type must support. You can think of them as roughly equivalent to what Java calls an "interface". To that end, they appear in this section.

Most of the documentation needs will be similar between the abstraction and the concrete implementation, because in any event the caller treats either as an abstraction. However, these overt abstractions have an additional audience: those who are implementing a derived concrete class.

Therefore, please include (if not obvious from context):

* All the same things you'd write about a concrete class.
* The reason for, and nature of, the abstraction.
* Known implementations, or examples of the kind of implementations one might reasonably expect to encounter.



## Documenting Modules (Libraries)

The key to understanding a module's role in a larger system is to understand the API it presents, for that API is an abstraction boundary.

### API-Centric Module Documentation

A module's API is best understood as a collection of abstract data-types (ADTs) and the operations between them, which collectively the module implements and exports.
(A concise, coherent, orthogonal set of such abstractions reflects a high-quality API.)

Therefore, module-level documentation should:

* Summarize the purpose for the module's existence within the program or library.
* Tell the organizing principle or general nature of the module.
	* For example, does it reflect a well-known [design pattern](https://en.wikipedia.org/wiki/Software_design_pattern)?
* Postulate and give an overview of the ADTs and operations which this module exports/implements.
	* This is a general guide. The full details are in the function- and class-level docstrings.
	* Be organized according to concept, not just alphabetically.
	* Highlight convenience methods and the common use-cases they apply to.
	* Don't forget a section on exceptions that may burble out. These, too, are part of the interface.
* Refer to authoritative sources for relevant bodies of academic theory.
	* Oh, and **thou shalt** use standard vocabulary for standard concepts.
	* This applies both to documentation and indentifiers.
* Ideally, give some examples of how you'd use the different operations together.
* Note any general constraints, limitations, etc.


### Design Hints for Modules

I can't resist throwing in a little advice:

The seminal primary source on modularity is probably
[On the criteria to be used in decomposing systems into modules](https://prl.ccs.neu.edu/img/p-tr-1971.pdf), David L. Parnas, 1971, Carnegie Mellon University, Pittsburgh, PA
It's a fine read as an academic paper, not too long, and the points are every bit as valid 50 years later despite the archaic notation in the examples.

TL;DR: divide module boundaries according to [separation of concerns](https://en.wikipedia.org/wiki/Separation_of_concerns), *not jobs*, and you'll have a flexible, sustainable system.

(One comment: In 1971 there were still people worried about the overhead of a subroutine call, and Parnas spent a paragraph or two addressing that fear. In modern systems, that overhead is the least of your worries.)


## Documenting Projects

### Orientation / Project Citizenship:

What's the overall mission, and our relationship to it?
* Define "success" for the project, and for the team.
* Is it attainable?
* Sustainable?
* Any special considerations or caveats?

What principles and values are core to project success?
* Stability above all?
* Move fast and break things?
* Correctness first, performance later?

How do we think about, and balance:
* cost, schedule, and scope?
* capacity, performance, reliability, availability, and correctness?

Interpersonal: *Free clue: Meet these people.*
* Who are the stakeholders?
* What sibling projects or infrastructure teams will you need to be on good terms with? 
* How shall the team communicate with other teams, and about what kinds of things?

### Technical Overview:

What are the major "system metaphors"?

Note any confusing vocabulary or words overloaded with many definitions. Do you have jargon specific to your company, task force, project, or team?

Describe the system boundary: What systems and actors provide and consume the inputs and outputs?

In what environment must the system work? Linux? The surface of another planet?

### High-Level Functional Breakdown:

A project might reasonably be broken into sub-projects based on scope, technology, or other factors.
At this level, pretty pictures (e.g. functional block diagram) are nice but not absolutely necessary.
Note how the team talks about these distinctions.


What subprojects are there? What are they for, and how do they communicate?

For each ``(sub-)*box`` in the functional-block diagram, ask and answer the following questions:

* What's it do? Explain like to the new guy.
* In 25 words or less, what's its raison d'être?
* What kind of architecture is the service?
	* e.g. is there a supervisory process and a bunch of per-$foo child processes?
	* Explain $foo to me like I'm 5. What's the life-cycle of a $foo?
	* What's the general flow of work between different castes of subprocess?
	* How are each of the castes represented? What modules, classes, and methods, define each of these?
* Describe its I/O and API boundary: What promises does it make? What does it demand?
* What are its specific endpoints of communication (with other processes, and with data storage)?
* Semantically, what sorts of messages come or go across each channel?
* What are the formats of messages passed across these channels? (Don't just say "pickles"; say where to find the structure definitions.)
* Are there any unusual storage, communication, or other APIs unique to this service, or does it strictly rely on project-wide standard practice?
* What additional naming conventions (or such details) apply to the code, storage, and communications resources associated with this service?

### Dynamics:

For each intelligible subprocess:

* How would you describe it as a state-machine?
	* For each state, what events result in what state transitions?
	* What's the happy-path?
	* The less-happy paths?
	* What's the meaning and consequence of every conceivable input message or event?

Between subprocesses:

* What kinds of "dances" to these (sub)processes engage in?
	* Examples: protocol negotiations, synchronization requirements; etc.
	* What are these dances meant to accomplish?
	* What happens if the dance partner dies or gets rebooted?
	* What about extra partners stepping in?
	* What about delayed, duplicated, missing, or out-of-order messages?

* Are there any Byzantine-Generals problems in all of the above? If so, how do we cope?

### Data at Rest:

What schemas, structures, and file formats are particularly relevant? How do they fit into the system?

For relational databases, you probably want two views:

* a conceptual/categorical management view which groups general concepts, and might index the...
* detailed entity-relationship diagrams for quick reference by working developers.

For non-relational and/or document-oriented data stores, you will have some concept of an accessor key
for a chunk of related data. That key might look like a pathname, or it may have no particular structure,
but one way or another you have a mental model of navigating from zero to data. Effective documentation
for a given data store must answer these questions:

* Given an accessor key following this pattern, what schema of document will I find there?
* Given a document of this schema, what sort of information can I extract (or store)?
* Given some sort of information, what schemas are relevant and where should I expect such documents to live?

Also, you'll want to note:

* Which data stores are meant to hold which sorts of data?
* What sorts of retention and archiving policies apply?
* Capacity and performance restrictions and requirements

### Data in Motion:

* What APIs and abstraction layers does the team use for storage and interprocess communication (IPC)?
* How to read/write to storage, and up/download; publish/subscribe; etc. using the project's chosen abstraction layer?
* What naming conventions, data formats, credentials, and APIs will you need to know for storage/retrieval/communication?
* What sorts of records do the different submodules store and retrieve, send and receive? And under what circumstances does this happen?

### Design and Code Conventions:

* Dependency inversion strategy: We'd like to be able to "mount a scratch monkey" in many ways, so how are real and mock bits constructed and composed, as far as each caste of sub-process?

* What about process management: creating, monitoring, signaling, and collecting results of child processes? Is there a utility API for this?


## Documenting Project Teams

This is the kind of thing you'll have in a slide deck. Most teams might not think to write it down, but the culture of a team is worth recording. Here are some questions to ask:

Overall group dynamics:

* What sort of leadership style and/or decision procedures are commonly expected? e.g. benevolent-dictator or consensus-model?
* Are there specific people or sub-teams with special responsibilities, rights, privileges, powers, or influence?
* How do small groups form and gel for joint design and/or coding tasks? How do they know when to dissolve?
* By what process is knowledge usually shared? Are there different categories of knowledge with different dissemination processes?
* What kinds of rhythms does the team have? Weekly scrums? Daily stand-up/zoom chat? Times when people are more or less available for consultation? Does this differ greatly for subgroups?
* What are the usual intra- and extra-group lines of communication? Are any particular lines of communication particularly strained or excessively open?
* Is there any particular subject matter that isn't as widely known as you think it should be?

Specific to development teams:

* Talk to me about the various dances of interpersonal coordination for the "code, test, review, commit, stage, package, deploy" development cycle?
* What does a person need to know to integrate smoothly into your "line of dance"?
* What steps close distance, and what steps create space?
* What's the right "measure and tension", so to speak?
* What sort of "lead/follow" dynamic exists in this dance?
* What factors influence that dynamic, and how?
* Do we tend often to dance with the same partner for a while, or are there frequent rotations?
* What stimulates or suppresses such rotation? For instance, do people regularly "cut in" during particular times? 

Also, an interesting interview would be to ask each member of the team

* (a) what they think the answers to the above questions currently are, and
* (b) how satisfied they are with that aspect of the status quo.


