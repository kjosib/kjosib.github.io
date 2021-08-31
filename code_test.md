# Vehement words about software testing

## Testing for Reliability

Everyone wants flawless code. Tests do not provide that.
Tests can demonstrate the presence, but not the absence, of flaws.
Nevertheless, test remain an important part of an *engineered product*.
Testing provides a benefit. Good testing strikes a good balance between
cost and benefit.

Each test represents a hypothesis that some particular tiny category of flaw
may exist or come into being, that would invalidate assertion(s) in the test.
Therefore, good testing *in the name of reliability* requires to understand
what sorts of flaws are likely, given human nature and programmer psychology.

* Example: off-by-one errors are common, so we test near size thresholds.


## Testing for Coverage

As metrics go, test coverage is one of the most confounding.
Perhaps this because of how little nuance a percentage conveys.

Testing specifically *in the name of coverage* will catch
most typos and simple clerical errors, but it does nothing to
improve confidence that the code does the right thing.

If you have the uncompromising discipline of a strict 1:1 correspondence
between requirements and test cases, low coverage numbers can inform you of
when application code is no longer required.
More commonly, you should interpret this as a multi-way disconnect between:

* requirements (what should be done)
* specifications (how it should be done)
* application code (how it is actually done)
* test code (how we know that it is done)

In other words, low coverage is like a baby's yowling cry:
something is definitely wrong, but it takes loving care, patience,
and persistence to figure out just what to do in all cases.

By contrast, high coverage is like silence from the same baby:
it may grant brief relief to the adults in the room, but a good parent
is soon anxious if baby is too quiet for too long.
We must beware of the nefarious duplicity sometimes used to
work around mandatory coverage checks. They are

You might want a mental aid for some of the intellectual effort involved.
Therefore,

## Assert what you mean.



## `unittest.mock` is not your friend.

In [To Kill a Mocking-Nest](https://www.rea-group.com/blog/to-kill-a-mockingtest/),
Ken Scambler points out a number of problems surrounding the use of mocks and
stubs as typically seen in enterprise unit-testing.
His thesis is roughly:
* They are promiscuous with implementation details in ways that stifle change.
* They test the wrong things: `getCoffee()` should return coffee (not tea). I don't care if it calls `visitCoffeeShop()` or `activateCoffeePot()`.
* They introduce a contagious and complicated web of subtle deception, embrittling the works: you mocked this thing, so now you have to mock that other thing or the tests fail.
* The ground-state is a check in the *code-coverage* box and a rigid, inflexible code base.
* The problem monkey-patches supposedly "solve" need not exist in the first place. (It's an architecture mistake.)

He also gives a couple of illuminating case studies exploring why people are tempted to mock, along with simple design fixes that **assert what he means** about API behavior.

Mark Sands gives a more impassioned but also more concise expression of similar ideas in
[Mocking is tautological.](http://marksands.github.io/2014/05/14/mocking-is-tautological.html)
He ends the

## Design for Test

The proper concept and application of mock objects are clearly explained at
[the Wikipedia page on the subject](https://en.wikipedia.org/wiki/Mock_object).


