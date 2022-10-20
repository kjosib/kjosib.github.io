Subverting Standish
====================

Or:

**How we Beat the Odds and Succeeded in a Significant Software Evolution**

## Abstract

What is the contribution?

Summarize the document with about one sentence per section of the overall document.
Focus on the contribution, not prior art or references.
Write it last. Or perhaps first (with intent to revise), RDD-style.

* Checklist: motivation, problem statement, approach, results, and conclusions.

## Introduction

*Business* wants new features, and *Business* does not care about our problems.
But we have problems. The usual ones, in fact. And those problems bring us down.

We are software developers.
Developers do a lot of things, but one of those things that makes us happy is writing code.

In the beginning, some of our forebears wrote some code, and that code made *Business* very happy too.
But *Business* did not remain happy forever. Before long, *Business* demanded more and better features.
This gave ample opportunity for our forebears to write mode code, so more code they wrote,
and there were more and better features, and everybody was happy.

The cycle continued, faster and faster: There was never time enough for everything.
The code grew and grew. As the years passsed, our forebears burned out and were replaced.
No single person understood the whole system. Some parts, nobody understood.
New features took longer and longer, with smaller and smaller scopes.

If this sounds like your product, you are not alone.

This was my product when I joined the company.

And according to the prevailing wisdom, this is pretty much the normal state of affairs in the software industry.

It doesn't have to be this way. What's more, it doesn't have to *stay* this way if it already has gotten this way.

Our team had the experience of climbing out of just such a hole and delivering a major new and flexible subsystem on a compressed timeline.
It's flexible, easy to work with, ready for the future, and functioning in production today.

The rest of this talk is about what tropes we subverted and how we did the deed.
Maybe our experience can inspire your team.

## Prior Art / Prevailing Conception

In the late 1990s, Extreme Programming was just starting to gain recognition among the plugged-in.
It works well if you adopt the whole enchilada, but extreme programming was just flat out too extreme
for the PHBs of the era. They balked. They wanted change, but they could not stomach the perception of risk.

This was a problem with a solution baked in: Consultants. Over a season or two,
a new industry sprang up hawking every variation and combination of practices and procedures.
This was the age of the *methodology,* which is a Greek word meaning the word "method" sounds too hum-drum
so I'll put a feather in its cap and make it sound all high-class.
We got the XP-lite, we got the Rational Unified Process, we got Scrum,
and we got a thousand other flavors of the month.
If the point was to sell consulting hours, then it worked masterfully.
But as for successful software? Well, that's always been a touchy subject.
Methodologies are like magic. If they don't work, then maybe you didn't cast the spell just right.
And if you're wondering, it's no accident that all the big methodology players
update their materials periodically. There is no magic.

At this point, the word "agile" has become like the eff word: it means everything and nothing,
depending on who says it, and how they say it, and when they say it, and who's in the audience.

So that is the last you'll hear me use that word in this talk.

## Approach / Methods / Solution

We may not know how to guarantee success in a software project,
but we do know lots of ways how to guarantee failure.

### Let's Don't Guarantee Failure!

When I joined, my first goal was situational awareness: What's what and who's who?
But my second goal was to impress upon our practices a disciplined philosophy.
I mean things weren't exactly bad, but we certainly had room for improvement.
As the new guy -- even a guy with experience elsewhere, but still new --
I had to develop a certain rapport with the team; a reputation for not having
too many terrible ideas at the same time.

It was fully a year before the big project I mentioned in the introduction.

-----

Have you ever wondered what makes some code easier to work on, and other code harder?
Luminaries in the field of software engineering wondered those same things around 1960.
They did research; they found answers; they published their answers in books;
and we promptly ignored the research.

* Visual Aid: Mythical Man-Month.

It's magical thinking to suppose that angry gods are to blame for your software difficulties.
And while we don't explicitly say the words "angry gods" in conjunction with software very often,
we have plenty of epithets for the same. "Code rot". "Decay". "Technical debt" is one of the more creative ones,
because at least it hints at some kind of obligation, but if we managed our money the way we managed our
technical debt then we'd all lose our clearances and be forced to stock toilet paper and office supplies
in the warehouse until the end of our enlistments.

It's magical thinking to suppose that we can keep on doing what we've always done and things will somehow work differently this time.

It's magical thinking to ignore the principles that the luminaries discovered and wrote about.

What I did for most of the first year was slowly introduce everyone around me to a philosophy.
That philosophy will not tell you which boxes to check in Jira, or how to trick SDLC into pushing your code.
It has nothing to do with tools or procedures or practices.

The philosophy is simple. It says these things:

1. Professional ethics are non-negotiable.
2. Respect your limits, and the limits of those around you.
3. Start with why. Then figure out what. And make darn sure the stakeholders are aligned on what. How is last, and code.
4. Respect the principles that make software easier and more difficult to work with.
5. The group is what must learn. It matters not what any individual member knows.

I'll elaborate on each of those just a bit, and then I'll get back to talking about the project success.

### Professional Ethics are Non-Negotiable.

Does this sound like a venture onto a tangent?
If so, then you're the person that most needs to hear this section.

We can talk all week long about the evils of fraternization or corruption.
We can make speeches about social responsibility or environmental consciousness.
But those are generic to *all* professions.
Software developers know of a particular set of evils unique to software.
We know how to create unmaintainable systems.

The software development team gets paid to design and deliver correctly-functional *classes-of-computation*
as part of a larger system that involves people and machines. The business does not care *or know* how this is done.
It's up to us to keep that process rolling smoothly.
We are the only people who know what *must be done* in order to keep ourselves effective.

Sometimes, what *must be done* is to spend time cleaning a module of the waste that haste made.

Sometimes, what *must be done* is to get a nice meal and a good night's sleep.

Sometimes, what *must be done* is to get seven dysfunctional directors around a table (or zoom call) to
so they can get aligned on what problem they're even trying to solve.

In any case, we're not going to leave a right mess for the next person to clean up.


### Respect your limits, and the limits of those around you.

Who's heard of "seven, plus or minus two"?

The fact is that we meatbags have severely limited brains. They're downright excellent at avoiding being eaten by tigers,
but when it comes to designing functional classes-of-computation that exist in a domain of pure rational logic,
human beings start out at a severe disadvantage.

That means we must:

1. Take good care of our brains: The right sleep, nutrition, hyrdation, occasional breaks, and a bit of exercise go a long way here.
2. Take good care of each other: We know a little of what's going on in our peers lives, and that of our subordinates. We are consulted.
3. Keep things simple: We should not need special knowledge or deep context to understand a bit of code, so no global effects.
4. Promote our most effective forms of reasoning: logic and abstraction chief among them, while enumeration of cases is worsted only by magic.

### Start with Why. Then figure out What. How is last, and code.

We are not clerics typing god-given code into the machines.
We are here to discern just which code must eventually be typed.
We are doing soemthing more like design and engineering, and less like construction.
The rule with engineering is that you provide what the customer needs, consistent with law and public safety, or else you disengage.

To have any hope of doing this well, you need clear advance communication and alignment.

Before you engage, you need to establish clearly and on record the
nature of the problem to be solved and the general concept of solution.
You need a clear-enough shared vision, recorded in plain language,
with only just-enough detail, knowing that crystal balls are always hazy.
You need to know who benefits and how, and you must also consider negative consequences
even to parties not present or unable to stand up for themselves, such as the public or the environment.

You will not solve the problem before you solve it.
Part way through, people may decide to change course.
Requirements change. Context change. Priorities change.
But none of that matters if you're awash in a sea storm of misplaced expectations and crossed purposes.

That is why, for nontrivial efforts, we settle on some kind of requirements document or plan.
Typical so-called "agile" practices would have you forego all such documentation.
But that's overkill. Some modicum of shared vision,
recorded for posterity and the far side of that week of vacation I have lined up,
will save the project considerably more trouble than the effort to create it.

As development proceeds, this planning documentation can grow to cover specific modules or features in greater detail.

Within the team, we benefit if more than one person has reviewed a design before implemetation starts.
With XP we'd solve that latter with pair-programming, but that's a separate rant.
At any rate, this practice has helped coordinate us in ways that a ticket-tracker like Jira certainly cannot.

### Respect the principles that make software easier and more difficult to work with.

Here are a few examples:

#### Progress, not perfection.

Noted speaker Dylan Beatie occasionally points out in his lectures that Software Development is the
only addiction you can get paid for being good at.
If Software Development is an addition, we can borrow a phrase from the addiction-recovery industry.

The other phrasing is the "Boy Scout Rule", which says to leave every place a little bit better than you found it.
You don't have to save the world before bedtime, but you pack out your trash and a little bit more.
Over time, this slowly changes the world, and not in a bad way.
Of course, we do have to agree on what means trash.
And we have to balance this against the notion of targeted commits for easy reviews.
But there's almost always some little thing you can do to make the code nicer while you're there.

By contrast, if you set to some massive clean-up job, you're delaying the creation of value and thereby creating strife.

#### Principle of Least Astonishment

That design which will surprise your colleagues the least is probably the wisest.

Games, puzzles, and entertainment are welcome to surprise and astonish.
Not so the tools we use and make daily. Of these we expect reliability and consistency.
Code-for-hire is not meant to be an adrenaline-packed adventure.

The largest expectation we have is that code means what it says it means.
So, when you go and dynamically replace the implementation of a method on an instance of an object
(as is common with certain frameworks that shall not be named)
you are undermining the maintainer's ability to reason about the code.

Unable to reason, we are reduced to using the debugger to step through a particular run of the code.
But what are we looking for when stepping? Clearly we know what to expect, for we read the code!
The only thing that could stop our stepping is when the debugger shows something surprising.

Now, here it where it gets horribly dangerous.

You see that surprising turn of events; how you have a new puzzle. This starts to get fun.
You're on hunt; sleuthing and solving a puzzle. You get a hit of neurotransmitters and
begin to associate the debugger with pleasure.

But here's what makes that mind-altering drug so dangerous:

By the time you've fired up the debugger, you've given up on logic and abstraction;
you are reduced to the least-efficient form of reasoning: enumeration of cases.

Let that sink in. Debuggers promote *and encourage* the least-efficient form of reasoning.
That should be a last resort! If you need a debugger to figure this <bleep> out,
someone <bleeped> the <bleep> up a long time ago.
And if you find yourself reaching for the debugger out of *habit?*
Stand by to stand by, let me tell you.

Avoid the clever hack. Someone is going to have to figure this <bleeping> <bleep> out.
(It might even be you six weeks later.) Make it clearly obvious, or document the <bleep> out of it.

(Meditation: Mythical creatures in your code are prone to mischief, and are a bad idea.)

#### Separation of Concerns (not tasks), a.k.a. "information hiding"

How many times have you seen a function rely on precise implementation details defined
halfway across town? Did you realize that's a problem? Did you refactor the function?

Written in 1971 and published the following year,
[this 50 year old paper by David Parnas](https://www.win.tue.nl/~wstomv/edu/2ip30/references/criteria_for_modularization.pdf)
is the primary source *par excellence* for how to divide up a system and design APIs.
His team performed actual scientific experiments
by putting teams up to solving the same set of problems according to different modularity strategies
to determine which methods win or lose on which accounts.

So read it. And then, if you're not sure where a function goes, read it again.

We lacked quite a lot of now-common shared vocabulary in 1971.
For example, Parnas spent fully two paragraphs inventing and describing the concept
of inline-compiled functions. But that's not important.
The important part is the conclusion. Here's an excerpt:

	We propose instead that one begins with a list of
	difficult design decisions or design decisions which are
	likely to change. Each module is then designed to hide
	such a decision from the others. Since, in most cases,
	design decisions transcend time of execution, modules
	will not correspond to steps in the processing.

We can run with this conclusion, as follows:

Ian's Aphorism:
	The art of software design is to delay decisions as long as possible.
	When we can make no further progress but to finally make some decision,
	we choose that decision which least forces our hand on the subject of others.

Often, the least-constraining decision is one which leaves out some fragment of functionality,
to be supplied later. Modern programming languages make this pattern easy:
You can pass functions around as data into other functions.
When you design with this strategy, you'll sometimes find a group of functions that hang together.
That's how you discover an object. And no, you don't want getters or setters. They violate the abstraction.

#### Composition in preference to inheritance

Several months in, someone observed that I tend not to use class inheritance much.
That's a fact. Generally speaking, most of the classes I write are what you'd call `final` in Java.
They may still have abstract slots to fill in, but these would be composed of other objects passed to a constructor.

The pat answer is that inheritance only works for filling in one aspect of variation.
Or rather, if you attempt to use this for more than a single aspect (or "decision", to use Parnas's word,)
then the result is an unavoidable entanglement of these otherwise-distinct concerns.
With composition, one object can define several points for variation and potential future definition.
If you follow the software-patterns community, you can think of it as an application of the strategy-pattern.

#### Et Cetera

I won't fit a complete course in software engineering into this talk.
The point is there are known principles,
and there are known consequences for when you adhere to them or violate them.
These consequences extend beyond some etherial notion of "code quality".
These consequences reach right down into the question of whether you have a good experience of work,
or whether each day is a depressing slog.

There is no excuse to apply influence in the direction of making each day worse than the last.

### The group is what must learn. It matters not what any individual member knows.

We're still working on this. Fortunately there's an awareness, and people do volunteer to write what they know.
It's handy if your documentation tool puts you through as little red-tape as possible.
A wiki-style system is pretty good for this. There are also some nice integrated content-management systems.
The point is rapid turn-around, not the complete raft of features.

## Results / Data / Findings / Proof / Discussion

### Or: What's about that project then?

Right. So I'd spent a year preparing the soil, priming fertile minds with stimulating ideas,
and taking what oppotunities came to remove awkward things.
Productivity, happiness, and team cohesion slowly improved.
By the time *the big request* came down from *Business*,
we were ready. Or rather, we were considerably *more* ready than we had been a year previously.
Some might call that a state of agility.

* We had the practices.
* We held the kick-off, and agreed on why development was necessary.
* We wrote up a few design ideas.
* We kept the code functional, and as functionally-pure as it was feasible to do.
* We used the "spike solution" technique to resolve the most concerning feasibility questions early on.

Fred Brooks wrote "Plan to throw one away. You will, anyway." That's basically spike-solution in a nutshell.
Our first version was a pure-functional non-real-time simplistic solution for one day's data.
This was never going to resemble the final code, but it helped clarify a lot of the interface boundaries
between what could be framework code and what could be per-application code.

Early on, we decided on a catalog of problems we wanted to solve,
and -- just as David Parnas advised 50 years ago -- a list of difficult design decisions which are prone to change.
Each of these became first a chapter in a design document, where we spent a few days working out the obvious kinks.
Next, we set to work on some code corresponding to that chapter -- but with advice and review from a responsible adult.

We held review sessions periodically. There were several various vacations mixed in,
but since we had several people on the team who were well-versed in the concepts, it was not too crazy.

On several occaions, the initial code that came out of a chapter worked, but was not to the team's general satisfaction.
A bit of talking about it, and we identified the concern that was missed. So a number of modules got some significant redesign.

The effort to compose design documentation for a subsequent chapter nestled snugly between coding and review on the existing ones,
so it was very much an example of trying carefully not to overconstrain things too early.

It should not come as a surprise that some few modules got lots of edits.
A central driver module, for example, saw significant changes each and every time a new subsystem came online.
Sometimes this was because of new insights about how better structure and organize the driver,
but most times it was to thread some new parameter into the system.
This is because we simply didn't write code to support the concept of a feature until that feature was up for implementation.
So each new feature had to be integrated in a few places,
but the vast bulk of the code for any given feature was confined to a corresponding module.

Along the way, each thing needed tests. Most of the features are tested together in the same unified test script.
The tests complete in less time than it takes to spin up a fresh interpreter. By keeping the bulk of system tests together in a script,
it means every change runs all the tests, so nothing gets forgotten or left to the continuous-integration server.
We get the few-seconds run-time because everything was designed for test.

We do not use `mock.patch`. All inter-subsystem dependencies are "injected" via parameters to constructors or functions.
There are effectively no global interfaces, except in the master job-control scripts that literally have no other task
but to select and wire up real components into a running process. For unit tests, we just pass test-doubles as parameters.
This means we do not suffer from brittle monkey-patching.

During the development of each feature, there's generally a framework API involved.
We have a variety of realistic fake applications for each API.
These realistic-fakes are the direct result of the experimentation necessary to see how the API might be used in practice.
So we just didn't throw those artifacts away.
They may have needed a touch of grooming, but they are now important parts of the test infrastructure.
Now and then they grow another greeble to support some further test.
This is usually way easier than a `MagicMock` based approach.

The testing is mostly based on state assertions. That's because I mostly want to assert outcomes, not particular behaviors.
If I call a `getCoffee` method, I expect the result to be coffee; I do not care if it's from the break room or the coffee shop.
Unless I do so care -- in which case I'd pass the coffee shop in as a formal parameter!

If I had to characterize the process, I'd say that it vaguely resembles running a release train of short overlapping sprints.
Except when someone comes back from vacation with a lot of suggestions.
In that case, we stop the train for a week and respond by incorporating the good ideas.

There are still sub-features in progress as I write this. But we've reached the point of usability.
An important step is periodically holding a show-and-tell with *Business*.
Because at some point, they stopped us and told us to change gears.
A subfeature that had been scheduled for several weeks out became the last thing between us and hoovering up vast coin by making a sale.
So we adjusted. And everyone was happy.

Like any software project, the bulk of its history has yet to be written.
What we have for sure is a proven reliable and flexible framework for a new kind of
product that fits well with the direction *Business* wants to go,
now and for the foreseeable future. And more important, we have job satisfaction.

## Interpretation / Significance

To me, this *successful software project* is just the way things are supposed to be.
But to other members of the team, it was remarkable.
I know it was remarkable because they remarked upon it.
The boss, and even the boss's boss, wrote back about it.
So, to the best of my severely limited understanding and perspective,
we did something right.

It's hard to get good quality repeatable statistically-significant scientific data out of this kind of experience,
because *by definition* corporate America does not run controlled, double-blind,
simultaneous, *duplicative, redundant* development experiments. This makes the study of software engineering
into mostly an observational science, similar to astronomy.

What we have here is, strictly speaking, anecdote. By itself, N=1 and there are many confounding variables.
The most pedantic statisticion would insist that no meaningful conclusion could be drawn.
But I can infer that my peers and my chain-of-command have seen enough to know something exceptional when they see it.
I don't think our success was an accident. Proving it more conclusively would be the subject of further research.

## Future Steps

We could take this in a few directions.

Chiefly, I think there's value in a focus on what our team does differently on a day-by-day,
hour-by-hour basis vs. other teams with average or sub-par performance.
These differences may not be obvious to an outside observer,
so it may be necessary to shuffle some personnel to gather this data.
If we go that route, it's important to carefully consider the effect of culture transmission.
Different cultures may be more or less resilient to disruption.
In particular, dysfunctional subcultures remain dysfunctional precisely by effectively fending off curative influences.
So it would be catastrophic to do a 50/50 swap. Maybe we do like an exchange-student program,
and then afterwards debrief the participants.

Another thing we could do is deliberately glamorize and promote different subsets of our putative formula-for-success
amongst different random subsets of the larger tech organization.
A longitudinal study could then positively attribute cause and effect.

## Conclusion

One thing is clear: Our team succeeded at a difficult software-development task on an aggressive schedule.
It was definitely not magic and it almost certainly was not luck either.
We have a panoply of practices and attitudes (but no detailed procedures) which collectively
seem to explain that success. Unfortunately, the explanatory power remains tentative, pending confirmatory studies.
But it is an important first step and I hope other teams can be inspired to experiment for themselves with our approach.

## References

Available upon request ;-}
