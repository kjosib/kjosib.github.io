# Vehement words about software testing

These vehement words come in no particular order. Yet.

Please also know there are whole books, and good ones, on this subject. Maybe these words will tempt you to find and read one.

## The Highest and Best Qualities of Tests

Tests are one element in the software component of an engineered system.

> That's three or four things to unpack as it stands.
> With luck, we get to them all in turn.

### Tests should be technically suitable.

* Clerical error have not been introduced into the translation from concept to code: Code coverage is sufficient.
* The concept is sound, and means what I think it does: Concept coverage is sufficient.
* Errors that might bring down production are caught with sufficient probability: The tests are powerful.
* Things that do not actually matter, are free to vary: The tests are robust.

I concede there are bits of code in the world where a simple smoke-test is fit-for-purpose.
The code running medical, aerospace, and infrastructure systems *is not that code*.
You'll need to choose wisely on the basis of your own project.

### Tests must inspire comfort and confidence.

In other words, tests are meant to cure anxiety and improve quality-of-life.

* The tests run quickly enough that people do not shrink from running them frequently during a coding session.
* The tests are reliable enough that people take the results seriously every time. (i.e. no "random" failures).
* Failure results are clear enough that people can understand what exactly went wrong and what they need to fix.
* The test code is clear and meaningful enough about what's ad-hoc, what's asserted, and why.

Passing tests are fundamentally an argument from lack-of-evidence.
Good tests exhibit a wisely-guided and diligent search for such evidence.
Bad tests can pass or fail, but are no real help either way.

## Tests Are Not Documentation.

At any rate, tests are unsatisfactory as a sole medium of documentation.

Documentation needs to say what is, what was,
and what shall come to be. Tests deal only in the present.
At best, a test specifies how things were expected to
be at the moment when it was created. But plans and specifications have
their own lifecycle, independent of the code and its tests.
So too with documentation.

It's fine to have a documentation format from which test cases may be extracted.
Indeed, this is an excellent idea, especially for API usage examples.
But too many unwholesome forces apply to the production of tests generally,
and especially in the *enterprise environment* where different people have
different agendas. 

## Tests Are Not Requirements.

That's not to say you can't encode a requirement into a test.
This too is an excellent idea *where it makes sense*.
It just has a limited domain of applicability.

* By the way, special tools and languages exist just for this purpose.
  They are typically founded on a *given / when / then* semantic framework,
  with enough syntactic sugar as to be readable (though not necessarily writable)
  by non-technical people.

It's to say that the Platonic essence of a *requirement* is categorically different from that of a *test*.
* They change for different reasons, and they carry different amounts of weight in a conflict.
* Requirements give *direction*. Tests give *assurance*.
* If a current requirement and a current test disagree, *the requirement wins* and the test has to change.

## Testing for Reliability

Everyone wants flawless code. *Tests do not provide that.*
Tests can demonstrate the presence, but not the absence, of flaws.
Nevertheless, test remain an important part of an *engineered product*.
Testing provides a benefit. Good testing strikes a good balance between
cost and benefit.

Each test represents a hypothesis that some particular tiny category of flaw
may exist or come into being, that would invalidate assertion(s) in the test.
Therefore, good testing *in the name of reliability* requires to understand
what sorts of flaws are likely, given human nature and programmer psychology.

* Example: off-by-one errors are common, so we test near size thresholds.

## (Good) Unit Tests Are Not "Double-Coding", But An Inductive Argument.

* You need not assert that your code does what it obviously says that it does.

Mr. C___ K___ once complained that unit-tests merely restate what's obviously written down in the function under test,
and thus add no value; only consuming developer time and resources. A pathological situation was evident.

After a bit more conversation, I believe he been seeing what's known as "behavior-based" assertions:
the idea that the test-subject clearly needs to perform X, Y, and Z actions, so assert that it does indeed call
methods X, Y, and Z. However, if the test-subject also manifests the principle of stepwise refinement,
then chances are `X;Y;Z` is the entire text of its code. So yes, if that's how you code (and it should be) then
you can probably skip the behavior-based assertions in favor of the sensible code review you're already doing.
(You *are* doing code-review, right?)

* Instead, assert about things that legitimately might be -- or later become -- *wrong despite code review:*
  mistaken notions, broken/changed contracts, or the subtleties around corner cases.
* This is the art of testing.

The far-distant end of the pendulum from behavior-based assertions is end-to-end integration testing:
where you feed a workload through a system and assert that everything came out alright. Any given test case
thereby exercises more parts of the system (an advantage), but it takes exponentially longer *and* it
requires *factorially*-more test cases to excercise every single thing in this manner (a much more serious disadvantage)
so it's not viable as a primary quality control layer **unless** you have *very* few components and a *very* small system.

*So that's what we'll do.*

The general idea is to form tiny compositions of just one or a tiny handful of components,
using realistic-mock objects as necessary and prudent,
then feed in a suitable set of test cases tailored to exercise the contract-under-test,
and finally conclude that the component-under-test -- the outermost -- is therefore assured (not strictly proven) to (still)
fulfill its contract.

In short, my tests don't (generally) concern themselves with how we got to the answer;
they are instead concerned with showing that the answer comes out correct,
given a severely restricted subset of the overall system.

Assurance of overall quality comes from a two-phase inductive argument over the set of all components in the system.

Phase One: Establishing the Inductive Criterion
* If I use all my dependencies correctly (code review),
* and if quality unit-tests reasonably probe my contract (test review),
* then: the fitness of my dependencies gives sufficient assurance of my own fitness.

Phase Two: Exploiting the Inductive Criterion
* Assume there are no cyclic dependencies. (If you have them, you need to get rid of them.)
* Let all units be properly tested in accordance with phase one.
* Some units have no (relevant) dependencies;
  these form level 0 and are trivially fit-for-purpose.
* Level N+1 contains all remaining units which depend only on those in levels 0..N;
  by the inductive criterion these too are fit-for-purpose.
* There are finitely many levels(*), so the system in aggregate is fit-for-purpose.

You do have to separately convince yourself that any mocks you use are of sufficient fidelity,
but this is generally a much easier problem.

(*) ...in a directed acyclic (dependency) graph with finitely many nodes...

## Testing for Regressions

Regression testing is one of the most mature testing strategies.
It also comes with the easiest business case for providing long-term value.
The fundamental assumptions are:
* We're going to make mistakes. These will lead to product failure modes.
* We're not too good at predicting them (or we wouldn't make them!)
* We will have to reproduce a failure mode to fix the underlying mistake.
* That act constitutes the creation of a test case.
* By keeping these around in an automated suite, our process can learn from the mistakes of the past
  and avoid accidentally re-introducing a flaw we've fixed before.

Theory says that if you have kept good data about the sorts of regression tests
you end up with over time, then you'll start to get better about predicting the
kinds of cases where bugs are likely to happen, and that's how you get good
QA/Test Engineers who can be productive writing tests for reliability,
possibly even before the function-under-test is quite complete.

* **Clarification:** I'm being deliberately abstract about the nature of these mistakes.
  They might be low-level function flaws or high-level integration snafus.
  I'll get to organizing your test cases some other time.

* **Digression:** I find this section to be a compelling argument for a certain approach
  to the practice of programming, but that's [an entirely different rant.](./code_practice.md)

## Testing for Coverage

As metrics go, test coverage is one of the most confounding.
Perhaps this because of how little nuance a percentage conveys.

Testing specifically *in the name of coverage* will catch
most typos and simple clerical errors, but it does nothing to
improve confidence that the code does the right thing.

* High coverage is one consequence of, but unable to cause,
  thorough testing *combined with and enabled by* suitable design-for-test.
* High coverage can also come about through gaming the system, so a low coverage metric
  does not mean anything conclusive on its own. It's more like a smell: you can
  spray the room with air freshener, but that doesn't eliminate the poop in the corner.

Developers may be driven to nefarious duplicity in the name of mandatory test-coverage checks.
* What counts as a line of code? If we coalesce lines without changing their meaning, does it improve things?
* What counts as coverage? If we mock out the CPU, the disk, the memory, and the network card, did we test anything?

If you have the uncompromising discipline of a strict 1:1 correspondence
between requirements and test cases, low coverage numbers can inform you of
when application code is no longer required.
More commonly, you should interpret this as a multi-way disconnect between:

* requirements (what should be done)
* specifications (how it should be done)
* application code (how it is actually done)
* test code (how we know that it is done)

In other words, low coverage is like a baby's yowling cry:
something is definitely wrong, but it takes loving care, patience,
and persistence to figure out just what to do in all cases.

By contrast, high coverage is like silence from the same baby:
it may grant brief relief to the senses, but a good parent
is soon anxious if baby is too quiet for too long.

**Absolute 100% coverage is a fool's errand.**

There will always be some core of bits we have to take at face value.
We should try to make that core very small, simple, and obvious,
so that it's easy to trust by inspection
and easy to know where this extra inspection is needed.

In zones of low test coverage, there's a good chance the affected code is either
* configuration specific to a deployment environment (so ought not be code) or
* for weird scenarios that should never happen in a well-behaved system (so should be fault-injected), or
* strongly coupled and thus hard to test in isolation (so should be decoupled/refactored).

# Design for Test

If I may [appeal to authority](https://youtu.be/pAX8GAsRaYk?t=785) you might
take someone else's word that design-for-test is a good idea. (The rest of the
video is about continuous-integration, which is a different rant.)

The executive summary is that code *designed with testing in mind* naturally
ends up displaying a host of other positive qualities that make it easier to
get high-quality results more quickly. (Quality and speed go hand-in-hand.)

How, then, can we design for test?

I'm going to invoke a super-ancient acronym here: **CIPO.** That stands for
* Control
* Input
* Process
* Output

The insight here is that any given function should be involved in at most one of these activities,
at least with respect to whatever layer of abstraction you're thinking on at the time.
I'll deal with these in reverse order. There's also a secret item on this menu which I'll get to in time.

*Process* is pure-functions. These are the easiest to test, because they have only a signature:
no observable side effects and no external dependencies.
You should still strive to compose these simply from well-factored interchangeable parts,
because that is *the method* by which we have any hope to master complexity. But I digress.
Point is, you give some parameters and assert about the return values.

*Input* and *output* (or I/O) are meant to stand for whatever means you rely upon to get real-world
data into and back out of your process. Critically, it does depend on the level of abstraction
at which you're presently working. It can be the ``.read()`` method of a file handle,
or it can be the library call to save the updated browser session state in a web framework.
These are still functions which have signatures, but the function calls have
externally visible effects or temporal sequencing dependencies.
Calling ``write`` changes the result of calling ``read``.

There's a very good chance you don't have to provide your own input/output functions,
but you probably do provide parameters to the library functions you depend on. It's
important your code gets those parameters right, so keep that in mind for later.
On the other hand, if you're providing an API for others to use, then some of that
API will count as I/O, at least as far as the caller is concerned.
More about testing these in a bit.

*Control* is a deceptively-simple concept:
it is about taking input, making a decision, and invoking action.
That's all. It's literally a function from inputs to outputs, just like *process*.
But I've seen (and made) way too many messes in this arena.

Why is this hard?

My hypothesis is that people trained principally on conventional/imperative programming languages
tend to make poor architectural choices around control functions.
In fact, I would venture a guess that, as an industry, we've done a poor job of teaching
people how to design control functions.

* Digression: Haskell and similar languages are only really usable once
  you figure out how to design control-functions properly. These are, incidentally, what monads are for.
  [Don't Fear the Monad](https://www.youtube.com/watch?v=ZhuHCtR3xq8)

One approach that seems to work reasonably well in the Algol/Lisp phylum (which includes Python)
is to take input and output methods as parameters to the control function.
Maybe they're callable objects in Python, or maybe they satisfy an interface in (older) Java.
But the point is they're dependencies and you inject them via the function signature
(or perhaps a constructor signature, in case of OO design).

This makes your control function a higher-order function,
because it takes other functions as parameters and decides how to call them.
It also makes you a functional programmer,
but you can tell your boss the alternative is being dysfunctional.

In consequence, testing in isolation becomes rather easier: You provide real-I/O functions
in production code, and provide fake-I/O functions (what you can inspect and assert about) in test harness code.

----

I/O comes in layers. And more like an onion than an ogre! Let me 'splain.

Think for a moment about that library call that saves session state in the cache.
This is a non-trivial operation that needs to read, make decisions, and possibly write various things.
In order for that operation to work properly, it needs various configuration information.
Let's assume you have a "state cache" object. One way to handle that is to tell it which
database DSN and password it should use. But that's terrible because then you need a full-on database
just to run unit tests. A better alternative is given by what we these days call "dependency injection":
pass in an object that implements a (slightly) lower-level interface, which the cache object drives.

*But this is exactly the pattern I just described for control!*

And that brings me to the secret menu: *Configuration.*

Part of bringing up any system is configuring all the layers. We first configure the foundation,
and then pass a functioning foundation as part of the configuration of the subsequent higher layer.
At the end, this means there's an irreducible "germ-line" of configuration information which
controls how a functioning system is composed either for real work, demonstration, development, or test.
*Since we built it compositionally,* this is straightforward and easy to verify. 

In consequence, you're going to see a variety of things passed down the call stack which,
in college or your last job, you might have left sequestered in the global scope.
This gives some people heartburn.

Caller-supplies-tools is an industrial-strength architecture though.
* In a factory assembly line, the people who do the work are supplied all the tools and equipment they need.
  Nothing comes from, or goes, home with the employees.
* On a construction job site, equipment and tools are leased separately from the people who operate them.
* In a parcel delivery company, the drivers do not own or garage the trucks.

You can't exactly unit-test configuration per-se. It amounts to an integration exercise.
You can absolutely write isolated per-interface integration tests that use your real configuration methods,
but they fit in a different part of the deployment and reliability pipeline.
By definition these can only test the cases that correspond to the environments in which they run.
Your continuous-test server can not get a meaningful result from the production-integration-validation test case.

## Drawing the Line on Dependencies

Extending the session-cache example from above:

You might decide that a session cache needs to be able to:
* read and write the current session, and
* invalidate idle sessions periodically

Maybe you go on to define:
* "current" in terms of browser cookies, IP address, and a unique ID.
* "read and write" in terms of opaque objects known only to the application layer.
* "periodically" in terms of time.

In that case, you have several dependencies:
* the browser's cookies (to read, but also to write in case of a new session)
* a source of unique IDs
* some sort of persistence layer, which supports a two kinds of queries and one update
* a concept of time, which applies to all session operations

You want to be able to phrase your unit testing as follows:

* **Given** that all of my dependencies work as advertised,
* **When** my caller invokes feature X,
* **Then** feature X works as advertised.

When all the modules in a system provide that particular style of assurance,
then there's a neat inductive proof that the whole system works as advertised.

----

You're probably mumbling to yourself that it's impractical to to incorporate a web browser
and a database into the unit tests for some server-site session-management system.
That's why (and when) we create mocks.

The proper concept and application of mock objects are clearly explained at
[the Wikipedia page on the subject](https://en.wikipedia.org/wiki/Mock_object).

In short, the mock should exhibit an API that is *similar enough* to a real implementation,
but it should also have other characteristics (such as simplicity, speed, and instrumentation)
which make it *fit for purpose* in the context of the test.

An interesting software-engineering consequence is that you nail down an API even if you haven't done yet.
That means there are good and bad ways to make and use mock objects,
corresponding roughly to good and bad ways to design an API.

## `unittest.mock` is not your friend. `mock.patch` may even be the enemy.

In Python's standard library, ``unittest.mock`` exposes a few kinds of "magic-mock" objects.
They're "magic" in that they respond favorably to just about any conceivable (mis)treatment,
constructing new magic-mocks along the way.
This is held up as an example of saving the programmer time.

It has its place, but it is no magic wand.

Just for a simplistic example: Suppose your module-under-test makes an invalid API call against
a dependency. A magic-mock will report no errors. But a realistic-mock would throw the missing-method
exception you need to see right then.

* Clarification: Yes, the auto-spec feature solves some of this, but not all.

In [To Kill a Mocking-Nest](https://www.rea-group.com/blog/to-kill-a-mockingtest/),
Ken Scambler points out a number of problems surrounding the use of mocks and
stubs as typically seen in enterprise unit-testing.
His thesis is roughly:
* They are promiscuous with implementation details in ways that stifle change.
* They test the wrong things: `getCoffee()` should return coffee (not tea). I don't care if it calls `visitCoffeeShop()` or `activateCoffeePot()`.
* They introduce a contagious and complicated web of subtle deception, embrittling the works: you mocked this thing, so now you have to mock that other thing or the tests fail.
* The ground-state is a check in the *code-coverage* box and a rigid, inflexible code base.
* The problem monkey-patches supposedly "solve" need not exist in the first place. (It's an architecture mistake.)

He also gives a couple of illuminating case studies exploring why people are tempted to mock, along with simple design fixes that **assert what he means** about API behavior.

## Assert what you mean.

Every so often, I see someone's wrapped a log-capturing patch around a call to some function-under-test.
They call the function and then assert the log contains some string or another.
On a good day when I haven't gone full drill-instructor, I'll politely ask the perpetrator
what the intended purpose of that function-under-test was. Invariably, they *do not* say anything
about logging a message. *Then why,* I ask, *do you assert in a unit test that it logs a message?*
Typically, I'm next told "That's how I know it worked." 👎😞

I'm not even going to try anymore to understand this obvious double-think.

Oh by the way, there's also a very good chance that the offending function violated the CIPO boundary.

Mark Sands gives a more impassioned expression of similar ideas in
[Mocking is tautological.](http://marksands.github.io/2014/05/14/mocking-is-tautological.html)

# Calming the Maelstrom

A this point it seems not everyone uses words like "mock" and "patch" in exactly the same way.
I've argued *for* dependency injection and mock-objects, and then I've turned around and argued
apparently *against* the very same thing! Where do I stand? What color are my test boxes?

One size does not fit all. 
We are called to make (and sometimes defend) technical choices and trade-offs in support of strategy goals.
There will always be encouragement to shift things this way or that.

The whole point of testing is [quality](code_quality.md), which is subjectively defined by
whoever is paying for the product to be built and supported.
Those quality requirements should determine how much time, energy, and creativity will be
devoted to testing, and how deeply/thoroughly that testing will be done.

A good testing approach acheieves the required level of assurance at reasonable cost,
both in terms of
* the effort to test,
* the opportunity cost (e.g. new functionality),
* and the presumed systemic slow-down to adjust tests for details that change.

If you're in a mature organization, many of those decisions will already be a matter of culture.
If you feel the project you're working on merits a different level of care than it seems to be attracting,
it's probably a good time to apply your people skills.

## What about test-driven development?

Does anyone remember XP? Extreme Programming?
It started with the notion that practices are a system, meaningless in isolation.
And then it turned a lot of dials up to eleven.
Writing the test *before* the code was one of those dials.
Mandatory pair-programming was another.

I think the average corporate environment undermines these original XP practices,
and probably others besides. It feels like that clash between two different songs playing at once.

To write a test before the corresponding code exists, you must first decide on an API and a scenario.
Now chances are your commit rules won't let you check in a failing test, so you have to implement something.
You can either do it for real, or *do the simplest thing that could possibly work* which presumably just spits out the expected result.
According to TDD dogma, you're meant to do the latter, check it in, and then go back to adding scenarios until...

Do you have a clearly defined stopping condition?

Because I think you need one. And that condition is the actual API contract.
And you might easily be able to cast such a contract into a modicum of illustrative test cases.
But if you do this, then you have a fat wad of test code which prevents you from checking in partial progress on your module.

I think the *feasible* way is to develop tests and code in parallel,
much the same way you might develop proof and code in parallel.
You start with a quantum of API design, considering *design for test* as explained earlier.
From the API flows the pre- and post-conditions, the dependencies, and so forth.
These in turn *dictate* both proof obligation and code,
but they leave the writing of actual test cases to judgment and discipline as a risk mitigation activity.

## Testing and SQL

Thus spake Noel Darlow: http://aperiplus.sourceforge.net/testing-data-access-classes.php

The gist is: Your mocking framework cannot understand SQL, and so it cannot tell if SQL code is even valid, much less sensible.
Nothing short of an actual instance of the database server should be trusted to parse or interpret your queries in test context.
It is dangerous and irresponsible to even try to mock out a SQL connection.
Rather, treat *persistence* as an injectable dependency with a clearly-demarcated API.
Test business logic with a mock persistence layer that doesn't involve SQL at all,
and test the real SQL-based persistence layer against a real database server in a test environment.

Yes, this portion of your test suite will run a bit slower than average.
Yes, it requires some extra IT work to set up external resources.
Yes, some people will insist on calling these "integration tests" -- although clearly not end-to-end integration.
But this is what it takes to test your SQL code in any meaningful way.

Noel also gives some advice and ideas on making sure that your tests do not trip over their own shoelaces or scribble on production data.
The article is not long, and completely worth a read.

# Superfund Projects: Adding Tests to Legacy Systems

When *The Management* gets [Test-Infected](https://wiki.c2.com/?TestInfected), things sometimes get a bit out of control.
Management loves metrics. Code coverage is a metric. It's not a particularly useful one by itself, as earlier explained,
but hey we're not too far advanced from measuring programmer productivity by lines-of-code written. So here we are.
You're the unlucky chap standing nearest to some arcane legacy system when *The Management* decrees that coverage must increase from,
say, 16% to 70% over the coming six months. So here we go.

**First:**
When *The Management* complains about test coverage, I want you to replace that in your mind by a statement
that management is afraid for the reliability of the system, especially in the face of coming change or even general maintenance.
So that means you need to set the discussion back on track of how to achieve fit-for-purpose quality assurance,
and what that might entail as change is seriously considered. Remember: The legacy system has a track record.
It may be good or bad, but ultimately it's the track record -- past and future -- that *The Management* actually cares about.

*Key point:* When you talk to management, try not to even acknowledge code coverage as a metric. (It's certainly not
a reliable proxy for reliability; you know that but clearly management is three furlongs down the garden path.)
You want to speak the language of mean-time between failures, the costs and consequence of different failure modes,
and so forth.

This is totally at odds with a lot of published literature about how to build high-reliability systems, but that's OK.
We're not doing that. We're here here to engineer a *fit-for-purpose solution* to the problem management actually has,
which is again the *anxiety about technical risk* embodied in a legacy system that was not built with modern ideas
in mind about how to assure quality or reliability.

In other words, we're trying to make the fewest and least expensive changes to the status quo,
which will:
1. Diminish the *actual* cost and probability of encountering the conditions which *would* cause the system to fail,
   to an *acceptably low level*.
2. Convince management that what we've done achieves that aim *without* sacrificing either our values or our sanity.

The mutual understanding you gain from *speaking management* will pay massive dividends when it comes time to prioritize risks.

**Second:**
If you have *test* coverage analysis,
you might also be able to get *runtime* coverage analysis against either production or simulacrum workloads.
That would allow you to see what code is running without tests, and could form part of a basis for proioritizing efforts.
If that's not available, or if coverage is really low (say, less than 33% perhaps)
then you might achieve an early bump by adding a few simple end-to-end regression
test cases to the suite. You'll at least get a quick guide to the common-case code,
which by the way is now covered in some manner. It's not the ideal scenario by any stretch,
but that's not the point. You now have data and can prioritize.

At this point you'll probably find code falling into these categories:

* Mainline code does the usual work. It's therefore probably also the most correctness-critical, and oh yes it's now tested, so *WIN!*
* Defensive code deals with scenarios that should never happen; as such they cannot easily be stimulated.
* Alternative code coincidentally is not reached by the particular test cases you've chosen.
  Don't try too hard to fix this just yet; at this stage adding test cases has quickly diminishing returns.
  Instead, just note the cause and consequence.

**Third:**
At this point, your goal is to enumerate, evaluate, and prioritize the real risks remaining in the legacy code base.
There's always way too much code for anyone to understand it all in detail at once, so don't try:
you'd sacrifice your sanity as well as the schedule. Instead, try for an approximate gestalt.
If you have any reliable guides to the system architecture, that's great! Read them first.
Afterwards, quickly skim or glance through a random selection of different files in different packages.
Look for broad architectural (anti)patterns, major code smells, and overall themes in technical debt.

* Big-ball-of-mud? (i.e. giant methods/objects with too many responsibilities on too many layers of abstraction?)
* Inscrutable ravioli? (i.e. "collaborating" objects playing long volleys of control-flow ping-pong?)
* Tight coupling? (i.e. strong assumptions about specific arbitrary details scattered hither and yon?)
* Copy Pasta? (i.e. many nearly-identical blocks of code that do almost the same thing, perhaps with minor details changed?)
* Etc. Etc. Etc. [A good list is here.](https://wiki.c2.com/?CodeSmell)

**Finally:**
The last step is *refactoring* -- with exceeding care, and following best practices.
Remember, the key idea here is that each change needs to be self-contained and simple enough to be obviously-correct.
Get a skilled colleague to review each change with a critical eye, and don't feel bad if you have a few false starts.
Begin around the margins with the low-hanging fruit, and slowly work your way into the deeper mysteries.
As you go along,
* new functions will consolidate, simplify, or replace old code-blocks; these will of course be unit-tested.
* the architecture and your understanding of it will both improve, giving more weight to the risk/reward balance.
* new opportunities for easily testing old components will reveal themselves as a consequence of both points above.
* you may even find bugs. Actually, be very careful how you proceed: some of these so-called bugs may be features in disguise.

You can always leave this process aside while dealing with some other priority,
because it's designed around making a long train of small incremental improvements
while always keeping the system ready for prime time.

**One Last Thing:**
Do not for a minute worry the process creates no value.
Even if the legacy code was perfect and you never find a single bug,
you're still wiping the *perception* of risk from the company balance sheet.
That perception can drive much bigger costs than whatever you spent on refactoring the system into a (more) tested state.

On that very account, make sure to keep up dialogue with *The Management*.
When they understand how you've improved the risk profile of continuing to operate the legacy system,
they're much more likely to relent sooner and let you work on something sexier -- or at least give you due credit.

## Parting Observations

Test quality is much more important than quantity:
For any given module, the first few tests you write will have the greatest impact.

You seem to get the most (impact, code coverage, etc) the fastest by testing with realistic (if abridged)
scenarios and, where necessary for practicality, realistic mocks.

