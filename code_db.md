# Computer Programs as Databases, not Plain Text

Normally we write our programs in the form of text files. This unfortunate historical accident makes sense in context: a text-only language requires no special technology
to edit, parse, or collaborate on.

At the level of a single function definition, a stream of text is probably a fine way to interact, but in the larger view there's all this rich interconnected semantic structure which logically ought to exist as a proper database with a public query API.

Consider a typical programming language: the set of functions defined within a module have an accidental sequence imposed upon them by the linear structure of a text file. This sequence implies things for the version control system which make it impolitic to alphabetize the functions in an existing module. But in truth, the order in which definitions appear is not only arbitrary but meaningless to both compiler and programmer.

Ideally a programming environment should reflect the useful abstractions about code's organization. For instance, the SmallTalk system does well with its system browser. Even Microsoft got it right with QuickBasic, wherein the editor showed only the text of one function and you pressed a hot-key to switch to another. But neither of these systems solved the version-control and difference-comparison problem. Oh, sure, you could save your work as a text file, but it might have a different component ordering from one save to the next. That pretty much foils the whole diff/patch/comparison/versioning ecosystem that's built up around plain-text files.

So how do you do (branching, merging) version control and semantic comparison on a thing with graph-like or database-like structure? It's not so simple as it sounds. I think it's a problem worthy of study, because more generally there are other applications beyond program code for wanting a (branching, merging) graph/database/etc. Maybe some good project planning and management tools can come out of it.

Assuming you manage to structure your code as a database, then suddenly it appears you're locked into using the officially-appointed code editor. This can be absolutely catastrophic. You'd like all the other nice features of a modern IDE which basically means you need IDE companies to compete on features and support, but they're all looking at text-only languages for now -- except for SmallTalk.

Then there's the problem of adoption. We could conceivably define an altogether new language (like SmallTalk?) for use with the new file format, but it seems more marketable to go with an existing language (or group of languages) for which reasonable database schemata are possible. Macros or dynamically-composed functions add another layer of difficulty, but they're clearly a benefit to (and widely used in) the languages where they appear.

Language translators (that is, compilers) presently expect plain text. It would be possible to compose a front-end that ate databases instead, but in the short run it's simpler to fall back to the "save-as-text" route that got us here in the first place.

One final idea comes from the observation that current language-specific "refactoring IDEs" are actually syntax-tree editors in text-editor clothing -- and with a heavy dose of "error-production" voodoo. This works OK in Java and tolerably in Python, but it may be a different story with macro-heavy C.

## Conclusion:

It's probably a valuable research direction to see how to unify branch/merge version-control with the semantics of graphs and relational databases. That would at least bring some of the other ideas within reach.
