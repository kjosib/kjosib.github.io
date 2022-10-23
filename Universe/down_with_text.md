# Down With Text Files!

An early draft of this document was a long and meandering ramble.
The basic issue is that I have a collection of interconnected ideas about a system of interconnected issues.
Collectively, this gestalt leads me to a set of mutually-supporting conclusions and proposals,
but no single idea here stands on its own in an *all other things held constant* sort of context.

There's no obvious *best* way to structure such a gestalt vision of an alternative system.
(Perhaps Tim Burton's "The Nightmare Before Christmas" represents the best cinematic exploration of this exact problem, so go see it if you haven't. Despite appearances, it's *not* just for children.)
Therefore, I give you a long and meandering ramble.
But first, I will attempt an executive summary.

## Executive Summary:

Our software systems have long since grown far beyond our effectiveness to keep track of their many parts using conventional tools.
Our industry has developed a crufty ecosystem of clever hacks and trickery by which we try to cope.
These institutionalized monstrosities of duct-tape and bailing-wire realy ought to be replaced from the ground up
with an engineered solution to the complete landscape of problems inherent in a mature software development life cycle.
Existing tool-chains apply conformance-pressure at their interface boundaries,
making stepwise incremental change a difficult proposition.
If we want to remodel an edifice, we cannot simply replace the stones one-by-one:
only near-perfect copies of the originals would fit back in place.
Rather, we must knock out whole walls and probably cut new stone.
We also need temporary supports for the duration, so that the remainder does not come crashing down.

I propose a paradigmatic change to the way we organize the labor and artifacts of software development.
This is nothing to do with computer science,
but everything to do with the workflow around solving hard problems
(and keeping them solved as the environment evolves)
through the medium of programmable computer systems.

No longer should we view our code as some grand biblical document elevating a preisthood to comprehend its nuance,
but as the accumulated and codified transcriptions of myriad small engineering-level conversations between maintainer and machine.
I propose to study the nature and content of those conversations with an eye to optimize their bandwidth and productivity.
Actually, having been one of those maintainers for quite some time, I have some ideas as to what might help.
Still, there's probably a research thesis or two in this topic alone.

At any rate: I see our insistence upon the medium of plain-text for computer code,
and the *file* of plain-text as its overriding (versionable) organizational unit,
as cause for much avoidable pain. I now call for the downfall of this particular status quo.

I do have some specific ideas for how to re-invent the universe of software development,
but I think I should save them for a separate document.



## Chapter 0: *Accident* and Accident in Software Engineering

In his essay *No Silver Bullet - Essence and Accident in Software Engineering,*
Fred Brooks lays out a view of the difference between essential and accidental complexity.
I quote from his paper:

> The essence of a software entity is a construct of interlocking concepts:
> data sets, relationships among data items, algorithms, and invocations of functions.
> This essence is abstract, in that the conceptual construct is the same under many different representations.
> It is nonetheless highly precise and richly detailed.
> 
> I believe the hard part of building software to be the specification, design, and testing of
> this conceptual construct, not the labor of representing it and testing the fidelity of the
> representation. We still make syntax errors, to be sure; but they are fuzz compared to
> the conceptual errors in most systems.
> 
> If this is true, building software will always be hard. There is. inherently no silver bullet.

Today, the commonplace wisdom is that most of the accidental complexity of software development
had already been taken care of by the simple act of adopting high-level languages (HLLs):
The remaining complexity is (held to be) mostly essential,
so that no single artifact or technique would yield a major improvement in productivity.

**I'm going to make a new claim:** Accidental complexity comes not chiefly from your language or platform choices.
(Heaven knows some are better than others, but decades of research into languages have not produced a philosopher's stone.)
Rather, let us refer back to what accidental complexity *is:* precisely the management
of arbitrary extra detail, not about the essential issue, but without which no actual thing can manifest.
To put that another way, *manifestation is accident.* Fully 100% of the code is *accidental.* Why?
Because *alternative solutions also exist* for every requirement, every line of code,
indeed even for every single decision a programmer makes.
Arbitrary choices are inextricably intertwined with forward progress.
At least, they're arbitrary as far as the computer is concerned.
The day-to-day work of a programmer is to make these choices in a professional manner,
balancing numerous competing forces, and all the communication and coordination
that makes this possible. Also, on occasion, some code coincidentally gets written.

The real reason HLLs feel so much more productive -- and so much less accidental --
is because *they are* precisely these things, for one *essential* reason:
They require a lot less code to solve the same problems.
*In consequence, we attempt larger problems.*
The common use of HLLs did not, and will not, truly solve the complexity problem.
Rather, it enabled us to make bigger messes, and faster, with more people along the way.

So here we are: Software systems are growing in complexity for a number of the wrong reasons.
Cast your eye upon industrial codebases across the realm and see for yourself how programmers spend their time:
Are they casting essential verities into the spare notation of lambda calculus,
or do they instead scramble to upgrade log4j to patch remote-execution vulnerabilities?
Do they retain functional purity through the medium of the monad,
or do they swim through reams of API documentation to get an image to appear on the screen of a cell phone?
Do they utter words of wisdom to a silent silicon servant, or do they swear like sailors when their build won't merge?

-----

In industry, software is not some perfect crystaline artifact that you carefully grow under ideal conditions to best express a cool idea.
(I mean, we need those things too, but we just take them from academia and then get them dirty, dented, cracked, and debauched.)

Rather, software gets treated as a means to an end.
And just like that, the whole development life-cycle, as-experienced,
can also be understood as a means to an end.

Neither is a program considered a static document, fired and forgotten.
Rather, it's a massive collection of interconnected and interacting clumps of both functionality and state, and it changes.
Indeed, a system spends most of its time in maintenance mode.
Even the production of new features means working in the context of the bits already written.
It's like the old joke that you can't eat more than one bite on an empty stomach.

So here we have it: requirements come and go; maintainers come and go.
The product is always changing, and change tends to add complexity.
In order to reduce complexity, someone's got to understand an entire aspect of that complexity so as to refactor it sensibly.
Thus, I claim our chief practical opportunity for improvement would come from making large code-bases easier to grasp,
navigate, and understand the parts relevant to some given concern. (After all, this is most of a maintainer's day.)


## Chapter 1: The need for radical novelty

Fred Brooks was right about one thing:
The lowest-hanging fruit has already been plucked.
Nothing will take away so much accident, and so quickly, as the adoption of HLLs has already done.
Again I quote:

> Surely the most powerful stroke for software productivity,
> reliability, and simplicity has been the progressive use of high-level languages for
> programming. Most observers credit that development with at least a factor of five in
> productivity, and with concomitant gains in reliability, simplicity, and comprehensibility.
> 
> What does a high-level language accomplish? It frees a program from much of its
> accidental complexity. An abstract program consists of conceptual constructs:
> operations, data types, sequences, and communication. The concrete machine program is
> concerned with bits, registers, conditions, branches, channels, disks, and such. To the
> extent that the high-level language embodies the constructs wanted in the abstract
> program and avoids all lower ones, it eliminates a whole level of complexity that was
> never inherent in the program at all.

I would argue that in fact HLLs were in fact a radical novelty unto themselves:
They substituted a completely new paradigm into the computing landscape.
Previously, it had been the task of programmers to instruct the computers in their own native language.
With HLLs, it becomes the task of the computer to execute our programs expressed in the language of our choosing.
It is impossible to overstate the significance of this change: It was completely revolutionary.

-----

Brooks claimed that the concrete program is concerned with bits, registers, conditions, branches, channels, disks, and such.
Certainly those many items are arbitrary details with no *essential* meaning unto themselves:
there's nothing special about register R3 except inasmuch as it contains some value of significance to the computation.

Well and good, but let's recast the premise into world in which HLLs are de rigueur.
Now the *concrete program* is expressed in an HLL.
The miracle of compiling and linking and loading and so forth is no longer to be considered miraculous.
It's just part of the package, *sine qua non.*
We're way better off dealing with variables and functions rather than addresses and registers,
but it's still very much a solution-domain distinct from a problem-domain.
There are still plenty of arbitrary details to hide the devil in.

Brooks argues convincingly that the elaboration of HLLs can only go so far:
Soon enough, new and esoteric features become a cognitive burden all their own.
I think it's fair to consider libraries along similar lines:
Good and relevant ones may save you tons of time, but they aren't all good or relevant.

So that's about it. Brooks' essay also contemplates and rejects several other ideas.

-----

But wait. At one point, while dismissing graphical programming, Brooks has this to say:

> More fundamentally, as I have argued above, so ftware is very difficult to visualize.
> Whether we diagram control flow, variable scope nesting, variable cross-references, data
> flow, hierarchical data structures, or whatever, we feel only one dimension of the
> intricately interlocked software elephant. If we superimpose all the diagrams generated
> by the many relevant views, it is difficult to extract any global overview.

Hopefully at this point an idea is starting to take shape.
Let me repeat part of the first quote:

> The essence of a software entity is a construct of interlocking concepts:
> data sets, relationships among data items, algorithms, and invocations of functions.
> This essence is abstract, in that the conceptual construct is the same under many different representations.
> It is nonetheless highly precise and richly detailed.

We have experienced the century of radical novelty in terms of what computers can be and do:
the nature of discrete logic and programmable generality being the chief drivers of that novelty,
with ever-increasing hardware performance and the development of software marketplaces following closely behind.
And yet, despite advances in IDE technology,
we still consider the least-common-denominator of code as regular files containing only plain text.
(All that highlighting and cross-linking your IDE presents is a sophisticated magic-act enabled by
partially re-interpteting the *text* along similar (but not identical) lines to whatever the compiler ultimately will do.)

**It's time that we create radical novelty in terms of how software gets made.**

If we expect people to be able to grasp, learn, and competently modify a software system,
then necessarily we need to represent its artifacts as *a construct of interlocking concepts* rather than mere text,
no matter how colorfully-decorated.

Ordinary plain-text computer code, and our traditional ways of working with it, are the wrong answer.
(So is a low-code platform, but that's a different rant.)

Modern IDEs do help a little bit with some aspects (e.g. with jump-to-definition),
but they do not make all problems go away.
Current visual source editors (PyCharm, NetBeans, etc) work by keeping the file primary and
building a database of annotations about what's where.
Still, they very much feel primarily like fancy text-file editors.

I say we should do the opposite: edit the database as such,
and only build files when strictly necessary as a way to cope with archaic technology.
To be sure, we can still have lines of code, but maybe each function, method, or class is a record in a database?
Maybe here-documents and nested functions are edited in separate views; represented only by compact placeholders in the outer view?
Structure, cross-reference and index-search become primary means to navigate the code, not some 60s-vintage file hierarchy.

Going further, maybe non-textual constants (i.e. resources, like graphics and sound) can become part of your code,
directly referenced and indexed according to where they're used? Certainly *some* measure of boilerplate might go away.

Systems become institutions because they represent a sort of local-optimum: the nail that sticks out gets hammered down.
Existing assumptions about how to interface with and collaborate on code tend to push us back toward text files and parsing.
Changing this would require retooling that. So there's a significant amount of work to make something like this take off.
I think the pay-off is worth it.

-----

Let me moderate the message slightly:
I'm not looking for a five-fold increase in productivity, quality,
or the like stemming from a fancy new code-organizational technique alone.
What I do expect is to optimize the experience for developers and maintainers,
giving them happier lives,
which will ultimately translate into faster and more nimble programming shops.

I also expect that a database-backed store operating on a more finely granular level than a whole file can therefore do a
much better job of cooperating with a product management system. That prospect alone should stimulate management interest.

# Chapter 2:

## What is our proper concern?

What we need is to focus our tooling (and our practices) on the sole and exclusive task of keeping our systems
*intellectually manageable.*
That specifically means enabling journeyman programmers to join a team and get up to speed rapidly,
even with unfamiliar sections of the codebase that nobody has looked at in a while.

You can't do that while you're still arguing over the question of curly-braces vs. significant-whitespace.
It's so much the wrong question; I can't even begin to express how much the wrong question it is.
This much is not controversial.

There are methodologists: these people claim that if you follow correct practice, things will work out.
And in the toy examples, things do indeed work out after one or two orders of magnitude too much code.
(See, for example, the enterprise-grade hello-world in your favorite search engine.) But as should be apparent,
things aren't so clean when the real world bites you on the knee. Failure can always be blamed on imperfect practice,
or upon the failure to incorporate the contents of the *next* revelation from on high into the practice of the day.
For this reason alone, methodology is not especially falsifiable.
Combined with the usual institutional distaste for the cost of exercising the scientific method and collecting relevant data along the way,
you have a recipe for silicon snake-oil.


What *are* the right things to be concerned with?

Personally, I'm a fan of the theory of affordances: We grab a door by its knob because a knob affords holding.
Similarly, traditional-concept IDEs afford copy/paste/modify, so we tend to see a lot of that.
(As a thought-experiment, imagine if you *could not paste code.* What would happen to your designs?)
However, I must confess a touch of the same guilt: Although affordances are a well-studied feature of industrial design,
I have little in the way of formal data to support my specific hunches as they relate to connecting said industrial design to the craft and practice of software development.

What I'd like to do is conduct some sort of experiment. Sadly, precise controls are usually cost-prohibitive.
However, the field of astronomy gives another inspiration: the observational study.



