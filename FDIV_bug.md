
If you have attained a certain age, you'll remember the Pentium `FDIV` bug from the late 90s.
It's not like Intel's chip designers had forgotten how to perform long division.
Rather, the inputs are a couple of 64-bit words.
To test every possible combination of inputs at a gigahertz would take something like 1,600 years.
That's clearly infeasible -- or it was, until many millions of these chips had found their way into
the public square and *somebody noticed a problem*.

Clearly, the hardware people had never dreamt of an exhaustive-test strategy.
They must have a practice based on a system of logic that proves whole categories of inputs lead to correct outputs.
Perhaps they break the problem into sub-units and prove each sub-unit independently. The details aren't important.
The point is that formal methods are necessarily.

Formal methods, for all their power, only prove that the *conception* of the design is correct.

