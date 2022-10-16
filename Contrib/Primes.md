# Computing primes efficiently in a pure lazy functional language

I have a side project which involves trying to discover ways of putting programming-language design elements together in interesting ways.
Part of that means having some set of notions about what programs someone might write in such language concepts.
One idea that should work pretty much anywhere is a simple prime-number lister program.

The *brute-force and ignorance* method is of course to simply do something like:

```
primes(max) = filter(is_prime, 2..max) where
	is_prime x = not any [ y mod x == 0 for y in 2..floor(sqrt(x)) ];
end primes;
```

This assumes a few reasonable stock characters but demonstrates no concern for efficiency.
Naturally I'd rather derive something a touch closer to the elegant pearl Knuth produced in his classic illustration of literate programming.

Knuth supposed that square-roots and division were expensive on his abstract machine.
I'm not going to bother with the full treatment of expensive division,
but I will suppose that taking square-roots is off limits.
Here's a verison in Python of this less-restricted form:

```
def primes(max):
	def square_of(x): return x * x
	if max < 2: return []
	known_primes = [2]
	candidate_prime = 3
	squared_prime = 4
	next_square_index = 1
	while candidate_prime <= max:
		if candidate_prime > squared_prime:
			squared_prime = square_of(known_primes[next_square_index])
			next_square_index += 1
		if all(candidate_prime % known_primes[i] for i in range(1, next_square_index)):
			known_primes.append(candidate_prime)
		candidate_prime += 2
	return known_primes
```

The key to the poetry is that candidate-primes are compared against a growing list of `known_primes` to which the trial-division aspect has access.
Represented functionally, the trial-division itself is straightforward in a lazy-functional pseudocode:

```
is_prime(candidate, odd_primes, bound) = all [ candidate mod p for p in take(bound, odd_primes) ];
```

But the outer loop of the imperative function requires a considerably more care. A first and incorrect try might start down this garden path:

```
next_prime(odd_primes, bound, squared_prime, candidate_prime) = CASE
	WHEN candidate_prime > squared_prime THEN next_prime(odd_primes, bound+1, square(odd_primes[bound]), candidate_prime);
	WHEN is_prime(candidate, odd_primes, bound) THEN candidate;
	ELSE next_prime(odd_primes, bound, squared_prime, candidate_prime+2);
ESAC;
```

Immediately there is trouble. The second line increments `bound`, while the fourth increments `candidate_prime`.
But the function only returns one number: the subsequently-found prime.
So any outer driving function loses track of when the bound increases.
This is not the answer.

After considerable thought, I came up with the following:

```
primes(max) = NIL IF max < 2 ELSE cons(2, odd_primes) where
	odd_primes = more_primes(0, cons(4, map(square, odd_primes)), 3);
	more_primes(bound, squares, candidate_prime) = CASE
		WHEN candidate_prime > max THEN NIL;
		WHEN candidate_prime > head(squares) THEN more_primes(bound+1, tail(squares), candidate_prime);
		WHEN is_prime THEN cons(candidate, successors);
		ELSE successors;
	ESAC where
		is_prime = NOT any [ candidate MOD p == 0 FOR p IN take(bound, odd_primes) ];
		successors = more_primes(bound, squares, candidate_prime+2);
	end more_primes;
end primes;
```

Now let's take a close look at the damage this does.

1. That `more_primes` function is plainly self-recursive in three ways. In each case, it only changes one of the arguments.
2. The output of `more_primes` feeds back into its own input, ouroboros-style, by way of a recursion expressed only in `odd_primes`.
3. The correctness of this *thing* relies on the subtle fact that the number `bound` is never more than the number of already-determined entries in the `odd_primes` list.

The third point bears special examination. There is a corresponding observation from the original imperative implementation:
Expressions involving `next_square_index` must never reach past the defined portion of the `known_primes` array/list/thing.
However, it's easy enough to prove this fact because I can point to exactly the instruction where `known_primes` gets portions defined,
as the denotational semantics of that instruction. In the lazy-functional verison by contrast, I see no clear denotational semantics of time.

I conjecture that a bugged variant of the imperative verison, which bungled the `next_square_index`,
would promptly result in some exception akin to `IndexError` in Python.
(Except in C, which would presumably just sabotage your wardrobe and then
[plan the conquest of Liechtenstein](https://abcnews.go.com/International/story?id=2921407).)
But mishandle the `bound` in a lazy-functional language and I conjecture an infinite loop of some kind,
with the run-time unable to make forward progress.
Perhaps a sophisticated run-time could detect such a situation -- some of the time.
Perhaps it would be similar to a stack overflow.
In any case, lazy-functional is clearly no panacea.

I would also like to comment on the experience of writing the lazy-functional verison.
I was able to work an expression out for `primes(max)` *eventually* with time and patience.
For me it was dramatically easier to write the Python version.
I do not know whether to attribute this difference to:

1. My comparative lack of practice with lazy-functional programming
2. Some inherent complexity of a higher order
3. Operational thinking, perhaps stimulated by the imperative verison

At any rate, the lazy-functional version is no mere translation.
It's also not the first thing I wrote down that (I convinced myself) represented a solution.
I almost regret losing that original mud brick, if only to show the contrast.

What I do not see is a clear path of successive refinement from the definition of a prime number to an efficient *and lazy* expression for a list of them.
Rather (and this bugs me) I started with an algorithm which had itself already been derived by successive refinement,
and then tried to re-cast that algorithm in terms of functional expressions which cleverly exploit a lazy evaluation strategy.
If I start from the definition of a prime, I get no further than brute-force trial-division.
I believe the reason is that the predicate `is_prime(x)` has no context,
and the typical built-in `filter` function provides for no context that might evolve in parallel to the filtration.
So that represents a conceptual stumbling block. By contrast, the imperative paradigm makes a point of evolving state.

The pure-functional paradigm can absolutely deal with evolving interrelated computations:
One need only write a function that takes all of its "state" as parameters.
I conjecture that this would be a fairly common pattern, especially with the guarantee of tail-recursion elimination.
But as things stand, it's a touch ungainly especially if the state is nontrivial.
To that end, I would like to postulate some sort of syntax and semantics specifically to deal well with this pattern.

The language *Elm* has a syntax feature which means *a copy of record X, but with field Y replaced by value Z.*
Actually, it allows multiple replacements in the same copy. This allows code to elide a tedious list of trivial field assignments,
which also has some desirable side benefits in Elm's type-inference system. But for the moment I'm mainly concerned with the tedium.

Suppose a syntax form that means *call X using, for its named arguments, exactly the values those same names have in the current scope, except for...*
This might go a long way towards unifying the realm of *algorithm* with that of *lazy-evaluation.*
A varation could provide expressly for *initial state* which does not appear in the external interface to the function,
but which is available internally for recursive calls to update.
Although it's not too far from there to objects.

I think the general idea is sound and merits experimentation.

