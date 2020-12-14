# Tabs and Spaces are Both Broken: It's time for Encapsulated Text.


## Abstract:

Tabs or spaces? I say neither! We need a new line discipline specifically
for things like computer programs. What's old is new again, if you squint.

*This is still a work in progress. Please make comments and suggestions.*


## Introduction:

For historical reasons we typically define programming languages in terms
of plain text (ASCII or Unicode) with various implicit assumptions about
how people will relate to that text. For instance, we assume that people
will apply indenting and visual alignment for legibility, except for in
offside-rule languages (like Python) where indenting is directly significant
to the syntax.

ASCII and Unicode both share two commonly-used horizontal whitespace codes:
code number 32 is the "space" normally used between words, and code 9 is the
"tab" which, in early printers, caused the print head to move rightwards to
the next available tab-stop. Early printers and video terminals all had
monospace fonts, and tab stops were typically defined as eight character-cells
wide. Therefore, a generation of programmers felt in their bones that "tab"
is an abbreviation for eight spaces.

Later systems allowed the user to reconfigure the tab width, encouraging its
use as a sort of "semantic indent" character. This way, different people with
different aesthetics could look at the same file and see it presented as they
felt it should be indented. All well and good, but it could still break
alignment if someone mixed tabs and spaces. 

In fact, the issue extends further. Coders sometimes exploit the physical
layout characteristics of monospace fonts to achieve presentation effects
like multi-column data read-outs or boxes around comments. It's no accident
that every major programming and text editor now defaults to monospace:
Proportional fonts look great for poetry and prose, but they break ASCII art!

Unfortunately, the historical use of physical layout "control characters"
and reliance on monospace conventions means:

* We get arguments about the relative merits of tabs and spaces.
* We can't reformat things to meet our tastes without breaking version control.
* Python has TabNanny. (Or is it tab_nanny? But that's a different rant.)

On a vaguely related note, every programming language needs to include some
consideration for how to include commentary in the running text of a program.
This complicates both the definition and the translator for the language.
It might be nice to use a standard library to read a comment-free version of
program text, regardless of programming language.

## Prior Art:

It turns out that the UCSD P-System had an interesting feature. Its integrated
code editor understood that most lines of Pascal were indented a good number of
spaces. To save bytes (a precious resource in those days) it prefixed each line
of text with a single byte indicating the indent level, in spaces. The language
definition of Pascal doesn't care about whitespace formatting (except that it
separates tokens), so the compiler's parser can simply ignore these bytes as
part of the "line discipline".

Among many firsts, the algorithmic language ALGOL had one (pretty) format for
publication and another (plain-text) format for entry into computers which,
in the days of ALGOL, were generally fed punched cards instead of operated
with interactive terminals.

In the "comment fork", I'd draw the reader's attention to the way computer
programming languages have settled on relatively few styles of offsetting
commentary -- these days generally with punctuation. 

* Most of the assemblers use a semicolon for line-level comments.
* All of C, C++, Java, C#, Javascript, and even PHP use the slasherix/astroslash for block-comments and double-slash for line comments.
* Most of the "dynamic" languages with Unix heritage follow the shell-convention of hash-marks for line comments.
* SQL and a few random other languages use the double-minus-sign for line comments.

## Desiderata:

Let us define a line discipline: a sort of "text container format" with a
relationship to ASCII or UTF8 analogous to the way media container formats
relate to video and audio codec streams.

The line discipline should:

* intersperse the bare minimum of structuring information,
* have a well-defined mapping to conventional "plain" text,
* be easy to distinguish from truly-plain text while remaining mostly legible,
* support popular semantic structures that ASCII art commonly illustrates,
	* Indenting
	* Block-comments (and perhaps line-comments)
	* Columnar tables of figures or expressions
* allow for a measure of configurable presentation without looking atrocious,
* be easy to integrate with parsing and version control, and
* become popular as a format in which to save program-code files.

Additionally, it might be nice to define translations to (La)TeX for
direct publication of high-quality printed versions of programs.


## Proposal: Encapsulated Text (E-Text) Files

We can reasonably define several levels of **encapsulated text**.


### Level One: The Super-Basics

Level one is super-simple: prefix each line of text
with a single byte (say, in the range 0-127, or $00-$7F hexadecimal)
which gives the level of semantic indentation for that line.
Also, the beginning of the file gets a distinguishing "magic prefix" that
wouldn't be found in a typical text file. (Perhaps 

Conversion to plain text is a simple matter of replacing that one byte
with the corresponding number of tabs or spaces.

Why the arbitrary limit of 127 indents? Because it's an order of magnitude more than
I've ever seen in practice.

This level can be generated deterministically using a simple "off-side rule"
from plain text with ordinary indents, assuming whitespace nesting is consistent.


### Level Two: Columnar Alignment

Level two adds support for columnar alignment, as follows:

First, characters in the range 27-31 ($1B-$1F) are reserved for special purposes.
In the unlikely event a literal reserved-character is desired, escape it with the
escape character 27 ($1B).

Lines of text may be broken into "fields" by the insertion of character 31 ($1F)
which in ASCII is called "US: Unit Separator". Fields may be devoid of other text.

In presentation, contiguous groups of lines with US characters should have
corresponding fields align vertically. Also, fields which contain numeric but no
alphabetic characters (except in the first row) should align to the right, or
on their decimal point.

These presentation-specific guidelines are not part of the specification per-se.
Instead they are stylistic choices left to the end user who wishes to work with
nicely formatted program code.


### Level Three: Structured Commentary

Programmers have historically used various bits of ASCII-art to highlight
block comments with varying levels of emphasis, generally in some kind of
outline structure. Semantically the indentation level of these lines
isn't so important as the level of emphasis given to the block.

Therefore, let us allocate a small range of the negative (twos-complement) bytes
to a handful of such highlight-levels. The formatting for presentation would be
a configurable matter, generally with higher levels of outline standing out more
than the lower levels.

* -1 - -6 ($FF - $FA) : Semantically similar to the H1-H6 outline levels in
HTML. -1 ($FF) is the most pronounced, and -6 ($FA) is the least pronounced.

* -7 ($F9) : For the copyright block normally found at the top of a file.

Contiguous groups of lines with the same "block comment level" would be formatted
together as a single block. If you want to present two separate similar blocks, a
non-indented blank line between them will suffice to separate them.

Additionally, the character 30 ($1E) "RS: Record Separator" may be used before
line-end "running" commentary. Contiguous lines with running commentary should
appear left-aligned, with space made where necessary.

Some languages (C and Pascal, for instance) allow the programmer to open and close
a comment on the same line, with code on either side. Thus, we can
treat the RS character as *inline comment delimiter* with
the convention that line-endings also end inline comments (making them line-end comments).

One could also reasonably define a few negative line-class bytes as thematic
breaks of various intensities. This might normally be presented as vertical
whitespace, possibly with graphical separation such as with a partial or full
horizontal rule or even as much as starting a new chapter heading.

At this level, one could conceivably leave the normal language-specific comment
delimiting syntax out of the encapsulated text stream. What's more, a language
designed with encapsulated-text in mind need not concern itself with comment
syntax at all. However, for presentation to existing translators, we have a dilemma:

* Do we expect a preprocessor to strip out comments?
* For presentation as plain text, can we put the comments back in correctly?
* Do the delimiters help people?

At this point, I'm partial to leaving the traditional delimiters in place and
just using encapsulation as language-agnostic semantic advice, but I could
totally see going the other way if e-text becomes directly acceptable to a
translation toolchain.


### Level Four: Embedded Documents

Going a bit further, consider the following:

* POD in Perl
* DocStrings in Python
* JavaDoc
* "Here Documents" in a variety of languages like Perl, Ruby, Python, and Shell

Each of these languages have special syntax for these ideas. They're actually
rather good ideas even for languages that don't support them natively, and they
complicate the definitions of languages that do support them. It might be nice
if encapsulated text could provide different views of the same program code for
documentation generators and other nice things.

Conventionally, automatic documentation generators have to parse through comments
and decide which ones count toward their content. Could the encapsulation format
help? Absolutely! We can define a few more line classes to participate in each
of several different purposes.

At the moment, I don't think a comprehensive compendium list of possible line
classes is even possible. However, a few of the more common ones might be:

* API: "How does one use this thing?"
* Algorithm: "How does this thing work?"
* Explanatory: "Why does this thing work?"
* Reference: "What does this thing even do?"
* Historical: "How, when, and why did this thing come to be this way?"
* Cautionary: "What happens if I press this button?"
* Obligatory: "We should really do this thing some time." (a.k.a. fix-me comments)
* Embedded: "A multi-line string to which this thing refers."

Of these, most can be treated as special kinds of comments and filtered out in front
of a translator/compiler/interpreter, but embedded documents need to be left in.
On the other hand, one may reasonably wish to tag embedded documents with a
subordinate syntax (such as SQL or HTML) for appropriate syntax highlighting.
On the third hand, it's really annoying when the editor interrupts your flow by asking
you what language you're about to write in.


### Level Aleph-Null: Things this proposal does not contemplate (yet)

In the extreme limit, one could imagine working with a pre-tokenized
file so that, for instance, all copies of the same identifier were replaced
with an index number into a table, or even a pre-parsed file so that all
syntactic structure was done with value-numbering.

As technically cute as those ideas sound, they're still just a bit too far out
in mad-scientist design space to pass the version-control sniff test (yet).

Besides, the lexical analysis of a C file requires the C preprocessor.


## Big Challenges:

The hard parts are never technical. There's no question the general
idea is cool. I predict objections coming in these major categories:

* What we have is good enough. Why bother?

	In fact what we have is barely good enough for the way things were in 1970.
	We do not make progress by standing still. Plain text is a physical layout
	medium, but acceptable layout of programs has its own semantic structure
	which, if respected, can lead to a more pleasant relationship between
	populations of people and the program code they work on. Semantic layout
	is just better than physical layout, but we're going to need tools that
	respect that.

* It is too hard.

	Currently we have rather impressive systems (e.g. refactoring IDEs,
	diff/patch/merge tools, etc.) built up around the foundation of plain text.
	Changing that foundation would mean a relatively enormous amount of work.

	On the other hand, a devoted community could add support little-by-little to
	various places so that, in several years time, e-text becomes de rigueur.

* It does not do enough.

	This is either another way to ask "why bother" or a tactless introduction to
	a useful suggestion. In any event, *enough* will always be a moving target.

* It does too much.

	Too much for what? Are you really saying it's too hard?

* I don't want format lock-in.

	You already have format lock-in. That format is ASCII or Unicode.
	Just make sure the format stays open and clearly defined so that anyone
	who wants "out" can easily convert back to plain text.

* It does bad things.

	That's a matter of opinion.

* The standard text-oriented API won't support it.

	They should not. The semantics of presentation mean that code is not plain text.
	A long tradition of pretending has left us with some uncomfortable saddle sores.

* The specification is incomplete.

	Darn right. Please help.

* The specification is not promulgated by a respected standards body.

	Darn right. Please help.


## One Path Forward:

The first thing is the world needs an encoder and decoder. The decoder should
respect a set of formatting preferences (call it a stylesheet), while the encoder
should be able to infer most of that from the plain text document (perhaps also
writing out a stylesheet).

As a result, it should become possible to use the two in conjunction to
reformat existing plain-text to different preferences. That creates a
minimum viable product: a simple, language-agnostic code reformatter.

The second phase is a three-pronged attack:

* Code editors: Emacs is the obvious choice, but Notepad++ also comes to mind.
* File comparison utilities like "diff", "patch", and "merge".
* The GNU C preprocessor, which automatically buys support in a sizable ecosystem.

The third phase is to improve support in one or more popular version control
systems such as Git, Mercurial, and SubVersion, presumably by reference to
the utilities described above. In the specific case of Git this is more
about ecosystem than anything else.

Fourth is to promote support for encapsulated text to the major script-language communities. In most cases it would probably be a trivial modification to the scanner,
but in an indent-sensitive language like Python it would be a little more involved.

Last is to convince the big IDE players that they need to support encapsulated text.
All things considered, they're probably doing something similar on the inside anyway.


## Last Words

I won't take offense if you tell me this is crazy-talk. But I think attempting
something on this scale would have two nice side effects:

1. We get the conversation about the abstract notion of what even is a line of program code as distinct from its physically-formatted manifestation on paper or screen.

2. We begin to move our concept of software change management that one iota closer to processing in semantic, rather than physical, terms.

3. We finally have a chance to end the holy wars between the adherents of tabs and spaces without one side having to obliterate the other.
