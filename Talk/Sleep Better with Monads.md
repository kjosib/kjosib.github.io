# Sleep Better with Monads

# Who is this talk for?

This talk is for anyone interested in

* Reducing the mental effort to read, understand, modify, and test code.
* Solving finicky problems without adding an overhead of complexity.
* Trying something different.
* Ending the cycle of anxiety and uncertainty.

# Learning Objectives

You will learn to design small, pure, composable functions in a monad-friendly style.
This will help you to read, understand, modify, and test such code with significantly
greater confidence and less stress. You will understand these benefits and why they accrue.

This module is composed of three major parts:

1. What actually is a monad? (For Programmers)
2. What can a composable/monadic style do for you?
3. How do I adopt this style in e.g. Python or Java?

# Who am I to talk?

I've been coding in one form or another since the Carter administration,
with an increasing emphasis on Python over the last fifteen years.
For most of that time, I've also kept my ear to the ground about issues
and developments in software engineering practice.

My early years as software professional were mostly on PHP and SQL before AJAX,
with a few clients on Java, and just enough perl to be dangerous.
I also picked up several other languages for school, fun, or both along the way.
I refuse to program in ADA unless it's for a space agency.

I learned to train people and give instructional classes in the US Navy.
It has been a while and you aren't Sailors, but the princples are timeless
so we should do alright.

# What actually is a monad? (For Programmers)

Let's approach this in baby steps.

* I'll meet you where you are.
  * No weird vocabulary.
  * Terms common to Java and Python.
  * Syntax will be clear from context.
* Let's talk about types.
  * Data Type.
  * Function Type.
  * The difference between syntactic and semantic type.
* Composable Functions.
  * Lego analogy: the signature is the shape of the pegs.
  * 1980 and Star Wars; "Build an X-Wing" had weird irregular bricks.
  * In contrast, MAXX-brand plug-compatible bricks can make anything!
* Pure Stateless Functions.
  * No external or implicit state -> Same question, same answer.
  * Are you allowed to cache? I'll leave this question on the table.
* Pure Functions *with* State.
  * Map / Reduce / Unfold (Yes, think big-data)
  * Obvious recursive implementations of the same

Now, we can talk about the two fundamental operations that make a monad:

* *bind:* Perform some operation while determining a subsequent intermediate-state.
* *return:* Create an initial-state, possibly from a pure value.

Canonical Examples of Monads:

* maybe: *nothing -> nothing* and *something -> maybe something.*
* either/or: like *maybe,* but with a *reason* in place of the nothing.
* list: *bind* operation can be spelled *map*, but see also *reduce* and *filter*.
* I/O: stands in for the state of the world; treated like part of a function's signature.

Compare the Map/Reduce concept: How does *reduce* relate to *bind?* Where is *return?*

# What can the composable/monadic style do for you?

## Claims

Easy to reason about (i.e. prove "correct"):

* Example from Coding Interview Question.
  * Things in either input list but not both.
* Begin with the proof; elaborate into code.
  * Lemma concept.
  * Keep it Simple, Simon!
  * Name a function.
  * Expression-Oriented Code
  * Divide and Rule.
* Code is *structurally isomorphic to its own proof.*
  * This one fact is worth how many years of experience?
* Small artifacts have comparatively small specifications.
* When concerned with function X, *presume* that function Y works as advertised. And conversely.

Easy to modify:

* Example: only one place to mention *set* (not two) and we're off to the races.

Easy to test:

* Code is a conjecture. Test accordingly.
* Test small parts in isolation.
* 100% of the code can be exercised by passing in arguments -> no frustrating external dependencies.
* 0% monkey-patching -> never forget to (or struggle to) update a monkey patch.
* No global state -> no problems with concurrency.
* Isolated bit of functionality -> isolated testing, with all the benefits.

## Caveats

**The Inconvenient Truth of Eager Evaluation**

Often you can leave a natural recursive definition as-is,
but there are cases where the eager-evaluation rule of a language like Python or Java
consumes unbounded stack or otherwise causes a problem.
This can tempt you to go right for an iterative solution.

The first rule is don't optimize before you measure.
Most inefficiencies are insignificant to the larger picture, and should be left alone.
The cost to clarity must be weighed against a clear-eyed assessment of potential performance or capacity gain.
Remember: Silicon is usually cheaper than programmers.

If you do decide to make a change, the original recursive version is still a valid design document:
it's a way someone thought about the issues.

**The System Boundary**

You will eventually need to deal with external dependencies in some real way.
If you play your cards right, this part will shrink way down.
It might not be so convenient, for example, to test your DB connection credentials,
but perhaps these may be considered *configuration*,
different on each deployment. Not everything is a unit-test.
Connecting to the dev database is an integration test, and probably doesn't need to run on every single commit.


# Adopting a Functional and Monadic Style

There is a bit of a discipline to master. Here are some hints:

* Learn to write recursive definitions.
* Focus your attention where it matters:
  tricky logic, complicated requirements, etc.
* Treat algorithm-state as a first-class immutable object:
  Accept a *current* state, and return a *next* state.
* Rely on formal parameters, not global access or aliasing.
* Do not wear a hair shirt, but keep simple things simple.

## Python Example: Andrea's support-rota improvements

* Yes, time-constrained examples are *necessarily* toy-sized.
  I can't change it. I'm going to try to make the best of it.

Consider Andrea's *assign* method, which has several self-recursive calls.
How does it break hard problems into simpler instances of the same *general* problem?
Compare and Contrast the *get-days-off* method:

* How are they built/structured?
* What do they return?
* What external resources do they depend on?

Let's also look at the unit tests for these, and production call-sites: Why are they like this?

Note the *State* object used in the *assign* method. It's a *namedtuple*.
How much work is it to jump the algorithm directly to a situation of our choosing?
How does that impact testing? How does it interact with recursive and external calls to *assign?*

What's going on with *assign*'s handling of Friday?
Can you see a way to carve out that concern?
What would have to change, were we to also have someone that worked Tuesday through Saturday?

The outer caller of *assign* contains a for-loop and an assignment of state.
This part is not pure-functional, but how complex is that loop to read and understand?

In the *assign* example, what plays the role of *bind?* What plays the role of *return?*

## Java Example:

Sorry; you fellows are on your own. I don't have any Java code to show you.
I'm actually going to use this pulpit to ask for contributions if anyone knows of anything.

# Wrap up / Summary

1. What actually is a monad? (For Programmers)
2. What can small, pure, composable functions do for you?
3. How do I adopt this style in e.g. Python or Java?

# Questions

* Yes, you in the back. What's your question?


-----------


# Random other bits that didn't make the cut:

Do not break methods for the sake of length;
Break them to isolate concerns from one another.
Length will take care of itself.

> Example: Washing Machine. Thematic vs. temporal vocabulary; high and low level controls.
  
If a thing might differ from one call to the next, make it a *formal* parameter.
Extend this idea to test scenarios and you get (explicit/static) dependency injection.

> Consider a bulldozer driver. If she brings her own bulldozer, it's the only bulldozer she'll ever drive.
> But if *I* provide the bulldozer, she can drive any contraption that satisfies the bulldozer interface.
> The *last* thing we should want is to sneak onto the jobsite just after her arival, distract her,
> sub out the bulldozer, and then try to switch it all back before she goes home. That's disingenuous:
> it means you can no longer trust the source code to mean what it says. That way lies madness.

Don't ask for data. Accept help.

> This object-oriented design principle absolutely applies in a functional realm.
> It's really about separation of concerns, which we can express in a few different ways.
> In an OO context, a cluster of queries on a local variable smacks of feature envy,
> which is a form of tight coupling: chances are, that local variable needs a method
> devoted to handling whatever task that cluster of queries is about.
> 
> In the functional style, separation of concerns is still a top organizing principle.
> You can look at *self* or *this* as a first parameter to a function and see if things make sense.

If you have a function of ten parameters, you've probably forgotten a few.

> https://www.cs.yale.edu/homes/perlis-alan/quotes.html number 11.

Finally, be practical.

