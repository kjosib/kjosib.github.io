# Hypergol: A programming paradigm for the future

* Insipration from Algol, Hypercard, Python, TempleOS, Haskel, Dijkstra, Forth, Ruby, Smalltalk, Erlang, and maybe some abstract algebra thrown in. Oh, and maybe decaf, depending on your brew.

# Some Specific Ideas

## The need for radical novelty

We have experienced the century of radical novelty in terms of what computers can be and do:
the nature of discrete logic and programmable generality being the chief drivers of that novelty,
with ever-increasing hardware performance and the development of software marketplaces following closely behind.
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

Perhaps "disaster" is too strong a word. Perhaps not?

### Python:

For an imperative language, Python gets a lot right, but it does have a few major design face-palms:

**Strings as collections of length-one strings**

Strings should be considered as atomic by default, but perhaps expose a read-only view as a collection of characters.
On a related note, characters should be considered distinct from length-one strings.
Both of the above prescriptions feed back to Python's idea of what's iterable-by-default.

**iterable-by-default**

The language tries way too hard to make things iterable. If you implement the `__getitem__` magic-method,
but not `__iter__`, then the language will invent a trivial `__iter__` based on `range`,
which if you'd wanted you would have written down because it's so trivial.
In consequence, an oversight can mean really strange error messages about integers you never mentioned.

**Dictionary iterations by key**

In Python, `for x in someDictionary` iterates over keys. But a dictionary does not contain keys. It contains key-value pairs.
You can write `for k,v in someDictionary.items()` but it's extra noise in the usual case.
You can also write `for x in someDictionary.keys()` which is perfectly clear and explicit,
or even `for x in someDictionary.values()` for to fill out the options.

Given that one of Python's own laws is *explicit is better than implicit*,
iterating over a dictionary should require naming your choice to iterate specifically the keys, or the pairs, or the values.
Simply naming a dictionary to a for-loop should be considered an error.

(Corrolary: perhaps list iteration should require the use of an `.each()` method/view for iteration?)

**Conflating Chronologic Typology**

Semantically, a date-and-time *is not* a date, and vice-versa. Rather, a datetime *has* a date, and a time, and maybe a time zone.
But Python's `isinstance(...)` routinely gives the *wrong* answers about these ideas. If you want to know a date from a datetime,
you'll need to use something like `type(foo) is date`.

On a related note, time zones and time arithmetic in Python are anything other than intuitive.
To be fair, you do get correct results if you know your way around `import pytz`,
but the very need for such a library is a miss.

### Ruby:

**Raise and Throw**

Ruby allows you to raise exceptions, but also to throw symbols.
This means there are two distinct sets of non-local action-at-a-distance semantics to wrap your head around,
which is both a burden and fertile ground for terrible choices.

**Bizarre Booleans**

In Ruby, the only false-ish values (in conditional context) are `false` and `nil`.
This is a terrible semantic miss:
People writing in dynamic-typed languages generally like to exploit the false-ish nature of empty strings,
empty containers, the number zero, and so forth.
You design-in the an opinion that such tests should be written to explicitly state the condition rather than rely on contextual promotion,
but the right way is to simply say that these other data types are ineligible in that context:
i.e. not to have any automatic Boolean promotion at all.
This even extends to `nil`: an undefined (or absent) value isn't strictly false either. At best, you don't know. At worst, it's a bug.
