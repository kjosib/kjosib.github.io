# Error-Reporting for Humans

Error-reporting is a complex and error-prone topic of critical importance to
many applications. It is a domain of delight and agony. Therefore, let us
contemplate error-reporting as a field of battle in its own right.

## Preliminaries

First of all, let's be clear that logging and diagnostics are
completely different topics. Logging is about organizing, filtering,
and redirecting a flow of data about the goings-on within a system.
Error reporting is about illustrating the underlying reasons why
something went wrong, as clearly and usefully as possible.

Error conditions have varying consequences corresponding to an idea of severity.
For example, it may be possible for an algorithm to limp along injured despite
some flaws in the inputs, or it may be appropriate to see what other errors
turn up (within reason). On the other hand, some error-state make meaningful
progress impossible. And on the third hand, just because progress may be possible
doesn't make it the application's policy to proceed.

Thus, the portion of a system that *detects* an error condition
is best positioned to to respond properly to the error's severity
and consequence. However, it should not have to worry
about *how* to display the error. Thus, a good error reporting
framework ought not define or raise any exceptions directly,
but rather leave all such policy to the application.

Blame is a transitive relationship subject to lenses of perception
and perspective. Thus, the subsystem that detects an error condition
knows which of its own inputs are incompatible with success, but
may not be best placed to trace the root cause. It must gripe on its
own terms. Ergo, a subsystem interface must specify those terms.

These interfaces form a partial order. We can thus refer to "deeper"
and "shallower" layers as being more or less removed from the
detailed structure of user input. For the example of a language translator:
the lexical analysis is shallow; the parse tree is intermediate; and
semantic analysis is rather deeper. Along this scale, the translated
result happens at the *deepest* layer precisely because it's the
farthest removed structurally from the input, which has nothing to
do with the modular structure of the application. It only means that
an error finally detected at this layer will take the most explaining.

Nine times in ten, we think of error reporting as how to assign
blame to (portions of) input data and the environment. It also
makes sense to give credit: "Success" is the best error code.
Therefore, rather than "errors" let's talk of "messages", which
incidentally also hints at the structure of a suitable solution.

The severity of an error message naturally falls into one of a few categories:
- Success: i.e. no errors; it worked perfectly.
- Advice: Input is legal but violates good taste. You shouldn't do that.
- Warning: Input is legal but probably does not mean what you want. You should check into this.
- Error: Input is clearly broken and the output is doomed, but the application may continue until a natural stopping point.
- Fatal: Input is too badly broken for the application to proceed on this work-unit, but it may switch to another.

Finally, let's don't confuse errors with exceptions:

* The user is responsible for input data. Errors come from and refer to input data.
* The programmer is responsible for code. Exceptions come from running code and have stack traces.
* Errors are not exceptional. They aren't even unusual. So don't throw them.
* An erroneous condition may preclude a computation. In that case,
	* First, report the error where it's detected.
	* Then, return nil, a [null-object][nop], an [error-object][gigo], or raise an exception according to your normal development practice.


## Architecture Considerations

For the rest of this document, I'm assuming we have an object-
oriented programming language such as Java or Python.

Let each subsystem (or layer) define its own suitable error-reporting
*handler interface*. In Java, that would be an `interface` definition.
In Python, the interface could be simply documented but it's better to 
write it as something which can be type-checked statically. That suggests
to subclass `typing.Protocol` in the manner of [PEP 544][proto].

At any rate, the defined interface will have methods corresponding to
each sort of problem which might be detected within the deeper processing
layer. Parameters to these methods represent the object-of-blame
associated with the erroneous condition as detected in the deeper layer.

At the subsystem API boundary, calling code will be expected to provide an
implementation of the error-handling interface. In general, this should
translate the deeper-perspective blame into a shallower
perspective for eventual use in explaining the problem to the user.
An intermediate-layer handler will then further delegate blame back
to the ever-shallower layers until there's nothing left but presentation.


## Number One, Make it Show!

> Misquote Picard if it helps, but top priority with error reporting is to
> put helpful and meaningful information in front of the end-user.

Given the architecture explained above, most of an application will rely
on a chain-of-responsibility, but that chain needs an end. There are a
million ways to do it, but a few common patterns prevail in many domains.

If you can localize where an error came from within a particular source document,
you'd generally like to include context with the error report.
The usual strategy is to show the offending line, ideally
with a specific portion highlighted somehow.

Let's generalize this idea just a bit:

We can decide on an abstract interface for finally presenting error
messages to the end user, and then provide a "convenience" implementation
or two. For example, these days command-line consoles can usually display
color text and thus beautiful error messages, but if you're forwarding errors
to a logging subsystem then chances are you want plain and terse.

In a journeyman-class implementation, a good error message needs text to explain
what went wrong as well as context that shows the root cause of the problems.
Each element of that context has a specific (and named) role in stimulating
the conflict between actuality and validity.

Often a context will refer to a specific bit of an input file. When two or more
targets appear very close to each other in the same file, it's nice if the
display shows a single contiguous context rather than repeating the overlap.

Sometimes context will refer to some sort of environmental factor or
internal application limitation. In these cases, it may not be possible to
show context but the matter still has some sort of textual expression.

In master-class implementation, a more complete error-message structure may also denote subsystem, severity, and general category. It may have short-form and long-form text used for different purposes. It may have all this information keyed to error codes in some
data table. (Please note: Error codes have nothing to do with exceptional return-values.)


## "Enterprise-Class" System Integration Considerations

Much of what follows restates and amplifies [this answer on StackExchange][ecodes].

Error codes can be absolutely precise. Therefore, use a different one for each
and every distinguishable fault, even if it's the same problem detected in a
different line of code.

If the help desk asks you to split an error code on some condition, do so. Test
the condition to decide which code to yield.

Error codes should be searchable, terse, easy to notice, and hard to mess up.
A good structure is probably a short alphabetic prefix, a (non-significant) dash,
and a sequence number starting at 1000. The prefix should identify which
subsystem detected the error so that teams can work independently.

The decision to keep the error-code registry out of the codebase is more a
question of distribution. If the system is used in different organizations,
they each need access to their matching version of the list. Consider a CSV
file that rides along with the application, and also whether your application
would benefit from message translation.


## One Simple Sample Design

Let a module provide some key toys:

* Two kinds of "blame" objects:
	* One points into a user file (with an offset and length).
	* One just contains a string, used for environmental facts.
* An "error-gloss" structure gets a short mnemonic, a severity, and a string-formatting template.
* An "error-message" refers to a particular error-gloss and a list of blame objects.
* Two functions that format short-form and long-form error messages to the console.
* A few typical error-gloss objects that describe common problems with scanning and parsing.

So at the end of the day, the last link in the chain of responsibility is a procedure
which accepts an "error-message" object and does whatever it takes to inform the user.



[proto]: https://www.python.org/dev/peps/pep-0544/
[ecodes]: https://softwareengineering.stackexchange.com/a/209720/57502
[nop]: https://en.wikipedia.org/wiki/Null_object_pattern
[gigo]: https://www.google.com/search?q=gigo

