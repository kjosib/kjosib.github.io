# Hypergol: A programming paradigm for the future

* Insipration from Algol, Hypercard, Python, TempleOS, Haskel, Dijkstra, Forth, Ruby, Smalltalk, Erlang, and maybe some abstract algebra thrown in. Oh, and maybe decaf, depending on your brew.

# Some Specific Ideas

## The need for radical novelty

We have experienced the century of radical novelty in terms of what computers can be and do:
the nature of discrete logic and programmable generality being the chief drivers of that novelty,
with every-increasing hardware performance and the development of software marketplaces following closely behind.
And yet, despite advances in IDE technology,
we still consider the least-common-denominator of code as regular files containing only plain text.
(All that highlighting and cross-linking your IDE presents is a sophisticated magic-act enabled by
partially re-interpteting the *text* along similar (but not identical) lines to whatever the compiler ultimately will do.)

It's time that we create radical novelty in terms of how software gets made.

In industry, software is not some perfect crystaline artifact that you carefully grow under ideal conditions to best express a cool idea.
(I mean, we need those things too, but we just take them from academia and then get them dirty, dented, cracked, and debauched.)

Rather, software gets treated as a means to an end.
And just like that, the whole development life-cycle, as-experienced,
can also be understood as a means to an end.

The key idea is that a software system (in industry) is not a static document, fired and forgotten.
Rather, it's a massive collection of interconnected and interacting clumps of both functionality and state, and it changes.
Indeed, a system spends most of its time in maintenance mode.
Even the production of new features means working in the context of the bits already written.
It's like the old joke that you can't eat more than one bite on an empty stomach.

There's a sort of political-economy space:
How do our decisions about practices and tooling influence (each other and) the end for which they are the means?
As an interesting academic exercise, we can run studies to investigate these things in fine detail,
perhaps with an eye to improving the state of the art.
Or, you could just take my word on faith.
Not exactly a stellar argument I know,
but I hope to formulate a compelling vision of sufficient novelty to motivate a call to action.

Software systems are growing in complexity for a number of the wrong reasons.
Let's be clear: complexity is always a negative, but sometimes it buys you something positive.
Since Fred Brooks wrote in *The Mythical Man-Month* of the difference between essential and accidental complexity,
the commonplace wisdom is that all the worst accidental complexity had already been taken care of with the simple
act of adopting high-level languages: The remaining complexity is mostly essential,
so that no single artifact or technique would yield a ten-fold improvement in productivity.

We can look at where complexity is coming from, and see if we still agree that it's mostly essential.
To that end, cast your eye upon industrial codebases across the realm and see for yourself if programmers are
spending their time casting essential verities into the spare notation of lambda calculus,
or if rather they are upgrading log4j to patch remote-execution vulnerabilities,
scratching their heads over quadruple-quoting the backslashes in a regular expression contained in a constant string,
and swimming through reams of API documentation just to get an image to appear on the screen of a cell phone.

The common use of high-level languages did not and will not solve the software crisis.
Rather, it enabled us to make bigger messes, and faster, and with more people along the way.

Ordinary plain-text computer code, and our traditional ways of working with it, are the wrong answer.

(So is a low-code platform, but that's a different rant.)

What we need is to focus our tooling (and our practices) on the sole and exclusive task of keeping our systems
*intellectually manageable.*
That specifically means enabling journeyman programmers to join a team and get up to speed rapidly,
even with unfamiliar sections of the codebase that nobody has looked at in a while.

You can't do that while you're still arguing over the question of curly-braces vs. significant-whitespace.
It's so much the wrong question; I can't even begin to express how much the wrong question it is.
This much is not controversial.

Then, there are the methodologists: these people claim that if you follow correct practice, things will work out.
And in the toy examples, things do indeed work out after one or two orders of magnitude too much code.
(See, for example, the enterprise-grade hello-world in your favorite search engine.) But as should be apparent,
things aren't so clean when the real world bites you on the knee. Failure can always be blamed on imperfect practice,
or upon the failure to incorporate the contents of the *next* revelation from on high into the practice of the day.

The question of the day, then, is *what are the right things to be concerned with,* when we have such silicon snake-oil flowing so freely?

Personally, I'm a fan of the theory of affordances: We grab a door by its knob because a knob affords holding.
Similarly, traditional-concept IDEs afford copy/paste/modify, so we tend to see a lot of that.
(As a thought-experiment, imagine if you *could not paste code.* What would happen to your designs?)

## Semantic disasters

### Python:

Strings as collections of length-one strings.
	Strings should be considered as atomic by default, but expose a view of a collection of characters.
	
* Random note #2: Date-time objects are not dates, and vice-versa. Rather, a datetime has a date, and a time, and maybe a time zone.
* Not-so-random corrolary: Date-time work in Python is a disaster. It's 
