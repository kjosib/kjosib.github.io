# Programming with the Functional Process Abstraction

Let a process consist of the following parts:

* Initialization
	* parameter (creator provides this once; it sticks around)
	* plan (function of parameter; computed once and saved)
	* initial-state (function of the parameter and the plan)
	* process-factors (mutually-recursive functions of all of the above)
* Queries
	* Exported functions allowed to read current process state
	* Local private factors also allowed
* Operation
	* input (creator provides these channels)
	* old-state (managed; initally equal to initial-state)
	* event-factors (mutually-recursive functions of all of the above)
	* new-state (function of all of the above; becomes old-state upon next event)
	* output (function of all of the above)
* Termination
	* condition (predicate over current-state and Initialization)
	* result (function of current-state and Initialization)

Figure on one *operation* section for each sort of event the process senses.

This abstraction needs a suitable notation for composing processes.
Then it will finally be possible to describe asynchronous processes naturally.

One key criterion is not to saddle the design with any improper notions,
such as a global system clock -- at least in the usual sense.
We can take non-deterministic input only on defined channels.
That also extends to the operating-system interface,
so clearly it will be necessary to treat processes as first-class data.

Open question: Do we clearly distinguish process from function?

I argue that you can implement a function by means of a process,
so long as the process declare no external communication channels.
But the creator of a process that *does* declare communication
obviously gets the other end of that channel.

How, then, to drive a process?
Well, you need to be able to answer the "ready" event.
If you have an array of processes,
you can get a "ready" event associated with an index (or key) into that array.

We say that any given process runs at most one event at once:
The runtime is responsible for mutual exclusion.
Thus, we can think of our processes as a single-threaded beast,
at least inasmuch as state updates are concerned.
However, the runtime is welcome to implement distinct processes
using whatever level of parallellism it likes.

Oh yes, and like with erlang, all communication is *effectively*
by copy, because it's also purely-functional and so there's no
way to express updating something in-place. But anyway,
that's the intended semantic, if it ever comes up.

Certain specialized algorithms are impossible if you refuse in-place updates.
The natural work-around is for the system to handle the wacky bits as language features.

Consider a concept of process containment and field-access.
That is:
* channel writes provide push-mode communication.
* channel reads await just such a push.
* exports queries provide pull-mode examination.

Given both queries and results, reconcile these in terms of information flow.
Do returns need to be plugged into a channel?
What happens to a member of a process array if a member finishes?
Arguably, the creator gets the result and then the channel evaporates,
but what does *the channel evaporates* even mean?

Probably borrow most of erlang's distribution and reliability model.

The point of all this is that there's plenty of room for creative
exploration of possible semantics and their consequences on the
human experience of developing interesting systems atop those semantics.

