# Sense and Nonsense in Identifiers

Part of making good code is making code that reads well, and part of making code read well is choosing good names.

## General Patterns

Be clear and concise. Avoid problematic words. Use conventions to clarify, not constrain.

Let's distinguish between *functions* and *procedures*.

Function
	returns a meaningful value that the caller uses for some legitimate purpose.

Name a function with a noun or noun-phrase for the *meaning* of what it returns.
For example, you could name a function `solution_of_N_queens_problem(N)`.

Functions that return a *true/false* value are called *predicates*.
Name them with the `is` prefix, as in `isPredicate(clause)`. 

Procedure
	causes an action to happen in the world.

Name procedures with verbs or verb-phrases.

## Common Noise-Words

Noise-words just take up space in names.
They add nothing of value.
Get rid of them.
The remaining code will be cleaner and easier to read.

Here are some examples:

* `get`, as in `getColor`
* `fetch`, as in `fetchColor`

In English, these imply action. For example, if I *get* money, someone else *gave* me that money.
If I am going to *fetch* the newspaper, I will have to go outside, which would make me unhappy.
If I *get* food poisoning, I will *get* sick and very unhappy indeed.

`get` in particular appeared in the *Enterprise Java Beans* framework (along with `set`)
and a generation of misguided programmers thought that was a good idea
because they saw it in a book and did not know any better.
It is not. It was a clever trick to make Java Server Pages work a certain way.
We do not need that clever trick in ordinary code.


* do
* perform

These strongly imply action. Often misguided programmers prefix them to procedure names.
It's much better to name a procedure for the thing it does. `ring_bell` is better than `do_ring_bell`
or the much worse `do_bell`.

* compute
* calculate

Just leave these out. They're completely implied by the fact that your code is running on a computer.
These words are verbs indicating that a computer must be involved in working out the result.

## Common Bad Words

Bad words actively make code harder to understand.
They obscure meaning or mislead the reader.
They come in several categories.

* verify
* validate
* check

These suggest a 



* manage
* handle
