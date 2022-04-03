# Hypergol: A programming paradigm for the future

* Insipration from Algol, HyperCard, Python, Haskell, Dijkstra, Forth, Ruby, Smalltalk, Erlang, and maybe some abstract algebra thrown in. Oh, and maybe decaf, depending on your brew.

## Some Specific Ideas

### What made ALGOL great?

The algorithmic programming language ALGOL came on the scene in 1958 with a number of true innovations.
For instance, it was the first with a formally-defined syntax.
(This aspect contributed to a Turing Award for both John Backus and Peter Naur: see also BNF.)
Now most people can't conceive of a programming language syntax being described any other way.

I want to focus on two aspects.

**First,** ALGOL is *block-structured.* At the time, this was considered a marvelous idea.
Today, it's perfectly ordinary and expected, at least in a limited form.
In practice, it means that you can nest functions inside other functions, and sensible scope-rules apply.
It also sparked a lot of thinking about what those scope-rules ought to be.

In principle, a block-structured language also allows data-type definitions private to nested sub-functions.
Pascal allows this also, but in the years I spent programming Pascal I don't recall being tempted to do this much.
Typically, by the time I'm defining record types, I'm also moving them into a unit (a separately-compiled module).
Then again, those were some of my earlier years.
Looking back, I can see the appeal of at least being *able* to define structured data that only one function or procedure uses or sees.
Given that dynamic languages tend to require (and even allow) quite a bit less ceremony (and therefore, clarity)
around data types, and given that most of my professional work is with a dynamic language,
I'll just say this is a concept worth keeping -- at least in principle.

**Second,** and perhaps more directly relevant, ALGOL had actually *two* syntaxes.
According to the official definition of the language,
there was a typeset syntax for what you'd see in a fancy publication,
and then separately there was the punch-card syntax you might feed to a compiler.
(Don't forget, this was the time before interactive terminals.)
The former syntax would specify things like font face and weight,
indicating for example that keywords should be in bold (don't quote me on this exactly)
whereas the latter made all the allowances for the truly terrible text input mechanisms of the day.

### How do we get from here to HyperCard?

The product officially known as HyperCard (TM) was a commercial mediocrity at best,
but it did bring about the general public's first realistic exposure to the *idea* of hyper-media.
In fact, the world-wide-web is largely an outgrowth of ideas that had their first broad public display through HyperCard.

What I mean by hyper-media in this context is that you have a collection of inter-linked multi-media pages (or documents, if you prefer)
each of which may be composed of intermixed text, graphics, video, and audio.
The actual HyperCard (TM) application added scripting and animation for a truly generalized interactive user-experience.
On the web, we call that *JavaScript* in the browser.
But critically, the HyperCard deck development environment gave an interactively-editable view of the page elements.
The graphical resources attached to a deck were like first-class citizens of the source code.

I now hereby invoke a strained analogy between punched-cards and hyper-cards.

Briefly: in a conventional programming language, it's normal to spend some fraction of your code
either directly solving the problem of loading assets (resources) into process space,
or else delegating the problem to a library.
Also, you have the mirror-image problem to keep the correspoonding assets organized in some way
convenient to both the artists who create them and the programmers who must integrate them into the application.
And last, there's a question of bundling these assets along with whatever deployment technology you use.
This last adds even more complexity to the asset-loading problem.

I believe that:

* Assets -- shapes, colors, pictures, video, audio, nontrivial GUI component hierarchies, and random other data -- are critically important for the modern application.
  Therefore, we should take seriously their proper integration into the development environment.
* Asset-bundling should transparently happen in real-time directly in the program editor.
* Assets should effectively bind directly like literal constants in lexical scope. (Or perhaps named constants; we'll see. Depends on the block structure.)
* In the editor, you should see an asset thumbnail, not a file-name, at the point of "definition": Maybe click to open a registered viewer/editor for the asset.
* In current environments, it may be necessary to play games with filesystems behind the scenes to make the important use-cases work properly.
* There may be a temptation to compare this with SceneBuilder/FXML or Visual Basic. The comparison is entirely warranted, but neither is a perfect match:
  SceneBuilder is slick, but still requires significant manual symbolic binding efforts.
  VB is a *little* bit better about name bindings, but imposes rigid organizational constraints that don't exactly lend themselves to highly-dynamic interfaces.

### How does Python slither in?

It has a solid standard library, great documentation online, and a thriving community.
Zero of these are a direct consequence of the language itself, but rather come from over 40 years of the creator's ceaseless promotion in well-connected contexts.
Still, that's the preferred model if you want to stick around.

Also, to the extent we retain a notion of textual notation, Python's succinct style strikes a well-respected balance.

### What do we take from Haskell?

Haskell put Hindley-Milner Type Inference on the map. Sure, there were earlier examples. But Haskell solved a number of usability quirks.

Haskell demonstrates that a lazy-evaluation strategy can lead to excellent program-structuring conventions.
In Haskell, your computation-sequencing discipline is exactly functional dependency, not the incidental accidentals of lexical sequence.
There is, in short, no semicolon operator in the pure-functional context.

On the downside, Haskell's absolute uncompromising functional purity does mean certain other compromises.
For example, you genuinely cannot write QuickSort in Haskell, mistaken assertions to the contrary notwithstanding.
(The oft-referenced two-liner is not a true QuickSort, and it may not even be O(n log n), if I recall.)

### Why Erlang?

Erlang seems to get CSP exactly right. Its concepts for asynchronous computing and coordination are just about ideal.

It also has an excellent I/O model, with a native concept of something like ropes-but-better:
Virtually all string concatenation (and much string-conversion) is pushed right to the system boundary, which is really helpful in applications
where you can't afford to get stuck in a quadratic (or worse) operation because of multiple layers of string re-concatenation.

Despite supporting a few notions similar to assignment, the referential transparency is equivalent to that of a pure-functional language and means garbage collection can be much simpler.

The one thing I would criticize is that it plays super fast and loose with compile-time type checking. Basically, there is only arity.

### Dijkstra, Forth, Ruby, Smalltalk, Decaf, maybe abstract algebra

Um... More to say here.

### Aspect-Oriented Data Structuring

Functions are the obvious candidate for the fundamental unit of program composition.
However, consider graph theory.
The data structures and algorithms are interesting enough on their own in an academic context,
but I care about using them on real problems *seen through the lens* of a graph-structure interpretation.

In many cases, a graph algorithm needs to attach extra data to each node as it goes along.
Afterwards, I may care about that extra per-node data, or I want to take some reading from it and be done.
So, I may want space for the intermediate and final results either pre-allocated in the node,
or conveniently located nearby, or whatever -- and this does not really change the algorithm in the abstract.

I think it's important to be able to expose a sort of graph-algorithm constructor set,
capable of meeting all these ideas, and then also not only for graphs but every similar kind of operational domain.

### Same name, Same Type of Thing

There's a balance to be struck between all-inferred types and the way manifest-types are usually done.
I've an idea we should decouple the type assertion from the declaration of parameters and variables.
This enables independent reuse of the effect of that type assertion, simply by re-using a type-constrained name in a new context.
This may require some motivating examples. The mathematics textbook is the most familiar.

## Semantic disasters

Perhaps "disaster" is too strong a word. Perhaps not?
Anyway, these are some specific pain-points drawn from existing languages.
I'd like to avoid or overcome them in whatever's next.

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
