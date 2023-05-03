**Abstract:** Effect systems are a hot area of current research. Outside of toys, I don't see the benefits.

-----

# Algebraic Effects: *Another* mistake carried through to perfection.

Effect systems are all the rage these days.
Naturally, I had a look around to see what I could see about the topic.
Honestly, I think the Ivory Tower is making a big fat mistake.

Industry codebases grow to gargantuan propotions and last for a very long time. 50-year-old code still runs in banks today.
Maintainers come and go, passing the torch -- *but not their accumulated deep knowledge* -- to their successors at odd intervals.

Effect systems deliberately elide the interprocedural relationships between cause and effect.
This obscures some of the most important information a maintainer needs
in order to be able to reason effectively *and locally* about a given bit of code.
I may be so lucky as to know *that* something happens, but not *when, where, or why* it happens.
But sensible OO architecture represents all of those essential elements of information directly in the code.
(In fact, you could encapsulate the meaning of "sensible OO architecture" by this dictum.)

## Quick digression to explain what all the hype is about

Think of exceptions. You know: try/catch/finally like in Java, C++, Python, Ruby, or your other favorite conventional language.

Now think of *resumable* exceptions. A `catch` clause can return to the code what raised the exception,
and possibly with an argument. Perhaps the handler got a record from a database, or used a GUI, or pulled it right out my anatomy.
Matters not. Subprogram resumes, happy with its answer.

How's it work? You install handlers in the call stack, dynamic-scoped, with purpose-built syntax.


Now, do you remember *checked* exceptions from Java? Yeah, everybody loved to hate on checked exceptions.
The creator's heart was in the right place, but the execution didn't work out. Checked exceptions are contagious.
So the designers of effect systems say "Don't worry about that; the computer will *infer* the `throws` clause."

Oh, and you have to handle everything at *some* level or else the compiler gets cross.


## Now back to the program

I'm not a programming language researcher by trade.
Rather, I'm one of those dirty nasty so-called "software engineers" with more grey whiskers than I'd care to admit.
What Dijkstra said about how to program when one cannot? Yes. All of that. Guilty as charged.
But you play the cards you're dealt. I'm pleased to work with some very smart people.
Many of them are more academically advanced than myself.
But also, about half of them have a non-CS background.
We have physicists, economists, and geochemical engineers.
We have a short bus that fetches old ladies from *the home* to teach our young whipper-snappers to maintain the COBOL systems those same ladies wrote before the Hula Hoop was cool.

*The Company* considers all of this a good thing.
After all, sweet careers are made of this, so who am I to disagree?
Compile the world; Java Python C. Everybody's looking for some bug.
Some of them want to maintain you. Some of them want to be maintained.

*I'd better stop before the parody police try to extract royalties.*

-----

Where was I? Oh yes. *Effect types.* Right.

So it *appears* that, as a user of an effect language, I can yield control (and maybe arguments) to an ambient handler and maybe get an answer back at some point, depending on the semantics of the handler in question.
This is sort of like the `yield` keyword in Python, except there's a *whole dynamically-scoped forest* of things that might step in to snatch control from halfway across the call stack (or the codebase).

Hold that thought.

> Decades ago, the CLU language had resumable exceptions.
> The people behind Exception Handling in CLU (Barbary Liskov and Alan Snyder) determined not to let exceptions from deep in an implementation leak through the boundaries of a procedural-abstraction:
> Callers at every level must either *handle* or *explicitly re-raise* every exception the callee might raise, perhaps translating or decorating it along the way.
> It's a bit more ceremony in the source code, but it means you can always understand and predict the system's control-behavior through local reasoning alone.
> It seems modern languages haven't got a CLU.

Conventional languages in industry all have this pattern where, if I want to open a file and write, I just open a file and write.
Or whatever. It's all there for the taking, in the global scope, any time, any place.

Now, the fact is we in industry have learned that dialing out to the operating system (from deep in the statically-scoped bowels of some unrelated module) is a terrible idea.
We've been burned too many times, and so we've rejected the *ability* to make this particular kind of mess. Foresworn it even.
Provide the proper tools to the objects which work for you; Do not expect those objects to make their own tools.
This approach yields small composable units that are easy to test in isolation from the dirty, dangerous, and difficult parts of the system.
Some call it by the elevated name of "dependency injection". I call it "passing parameters".

Occasionally someone -- typically in the 5-10 years experience range -- will complain about the alleged burden of passing all these parameters every which way.

-----

*The Company* had taken the mistake of dynamic-scope and carried it through to its perfect logical extreme,
which meant that you cannot trust a class-definition to describe the code that runs when you call a method.
Someone might have tweaked it. And then you could pass around sets of tweaks on different objects,
and layer these tweak-sets one atop the next, or package them up like used boogers and save them for later.
God help you to reason about the text of that code.
You have to understand *everything at once* to understand *anything at all*.

But lo, we *only* had eight gigabytes of source code. *Compressed.* So what's the problem?

-----

When I first joined *The Company,* I found myself on a team that had drank a bit of that kool-aid.
My first order of business, once I established a bit of street cred, was ending all this dynamic-scoped mutation garbage.
I said from this day forth, if you write a function or class that needs a service,
we're going to pass in an object that can provide that service.
We shall *not* grab services directly out of the global environment!
The only exception is the main-functions of executable process,
for the obvious reason that we don't control the caller.

That's when my new friend-in-another-time-zone spoke up, objecting to the alleged burden of all these "extra" parameters.

The thing is, the call graphs involving any particular service-object are never both very deep and very wide.
It's not a big deal to update some constructor's signature and its few callers.
Conversely, if some new parameter needs to flow all over many functions, then probably it *really* needs to ride along on some `self` or `this` (pick your flavor).
So time went by and new parameters threaded through as attention fell upon any bit of the application.
Before long, particular groups of parameters suggested themselves to represent coherent new object-types.
That's when the parameter lists began to *shrink* to shorter than they'd been originally.

> If you have a procedure with 10 parameters, you probably missed some.
>     -- Alan Perlis

Fast forward. It's two years later. Our team has no more tweak-layers in our application.
Evertything takes the parameters it needs for to do its job.
*And the developers are happy!* More productive, too.

-----

Proponents argue that the effect-type system has everything under control,
and I should just look at the inferred types to understand my program.

I'd argue that some Zen-of-Python rules apply here:

* **2: Explicit is better than implicit.**  An object understands a small, controlled vocabulary of messages. Pass it one of these messages, and you've just yielded the CPU. You might even get the CPU back later.
  There's the *effect* in your effect system.
* **3: Simple is better than complex.**  Parameter passing is a simple, obvious mechanism that everyone already understands.
* **8: Special cases aren't special enough to break the rules.** Internal-node in the call-graph involving a service-object aren't all that special, but they aren't such a big problem either.
  By threading a service-parameter through, I have an obvious tickler to understand where all the functional dependencies are. (Perhaps thence the word "dependency" in *dependency injection.*)
* **13: There should be one-- and preferably only one --obvious way to do it.** Parameters work.
* **17: If the implementation is hard to explain, it's a bad idea.** Enough said.

-----

# Conclusion:

This has been a smattering of vaguely connected notions. 

Perhaps it's had an effect?
