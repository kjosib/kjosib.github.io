# Decorative Instrumentation: A response to "Domain-Oriented Observability"

Background: A little bluebird recently forwarded me
[this article](https://martinfowler.com/articles/domain-oriented-observability.html)
by Pete Hodgson on Martin Fowler's excellent web site.

## Point (Summary of Background Article)

The article begins with a widely-understandable shopping-cart example.
We have some method, and maybe it works, but now we want instrumentation.
But that adds so much noise about logging and metrics that it's hard to find the original code in what's left over.
(Some sources suggest this scenario is depressingly-common in industry.)

Pete then treats us to a *before-and-after* view of a refactoring operation to isolate the concern of *instrumentation* into its own class,
injected as a dependency into the original.
The resulting drastic improvement to the signal-to-noise is offered as a virtue of this approach, and it's given a name: *domain probe*.
Next, the article illustrates various corrolaries derived from the axiom that *separated concerns may be considered separately*:

* You can test the instrumentation itself independently.
* You can substitute light-weight *test-spies* as instrumentation for shopping cart tests.
* Domain-oriented code may remain oblivious to metadata of interest only to instrumentation.

Finally, Pete develops the idea in a few more directions and mentions some alternatives.


## Counterpoint

At root, Pete's notion is dependency-injection toward the admirable goal of
disentangling instrumentation (i.e. logging, metrics, etc.) from business logic.

The decision to *declare and rely upon an abstraction* (in this case, of instrumentation)
is one of the fundamental skills of software architecture.
It is *the way* to keep a lid on complexity.
(A full exploration of abstraction in software is beyond the scope of this document.)

Now, let's have a closer look at the *after* example:

```
class ShoppingCart…

	applyDiscountCode(discountCode){
		this.instrumentation.applyingDiscountCode(discountCode);

		let discount; 
		try {
			discount = this.discountService.lookupDiscount(discountCode);
		} catch (error) {
			this.instrumentation.discountCodeLookupFailed(discountCode,error);
			return 0;
		}
		this.instrumentation.discountCodeLookupSucceeded(discountCode);

		const amountDiscounted = discount.applyToCart(this);
		this.instrumention.discountApplied(discount,amountDiscounted);
		return amountDiscounted;
	}
```

Evidently, the *ShoppingCart* constructor requires an *instrumentation* object,
to which this method passes messages. So far, pretty normal dependency-injection.

But lo! The constructor must also require, for example, a *discountService* object.
So I claim that we are yet to fully succeed in our proper goal.
Recall that the *before*-before actually had no noise whatsoever:
every character focused tightly on the singular concern to *fetch and apply discount if possible.*
It was even well-modularized: For example, discounts are the product of sales-think,
and thus we account for the consequent infinite-variability by delegating the detail-work
to the *discount* object itself. Now, even with instrumentation's *how* factored out,
still about 50% of lines of code are concerned with the *when and what* of instrumentation.
Spend one line doing a thing, and another line saying so. **That is still noisy.**

Furthermore, even with the *domain probe* idea used as directed,
an instrumentation call such as *discountCodeLookupSucceeded* is *functionally disconnected*
from the actual *discountCode* look-up to which it refers.
To wit, a broken method could possibly send all the right instrumentation events yet
neglect to perform important subtasks (say, calling *discount.applyToCart*). **That would be bad.**

Ideally, we would like the *subtask itself* to be the functional impetus that emits an instrumentation event.
Oh, and also I *would* like fries with that.

## Synthesis

On some level, you can't get completely back to zero-overhead and yet still have instrumentation.
So let's have a think: We'd like to instrument individual meaningful units of functionality.
Also, there's a standard way to talk about an individual meaningful units of functionality.
We call them *functions* (or methods, or procedures, or subroutines, or letrecs...) and we give them names.

Suppose we set a rule that a function can emit at most one instrumentation message,
and only when the function enters. That would mean at most one line of overhead per function,
but it would also enforce this nice boundary that if a single function is doing enough
different things to merit separate instrumentation messages,
then it's taking on too many different responsibilities and must be factored into separate sub-functions.

This influence toward smaller functions cannot fail to improve matters.
Directly, you get individual functions that are easier to read, understand, test, diagnose, and prove correct.
Indirectly, when you factor a larger special-purpose function into a composition of smaller parts,
many of the resulting btis turn out to be quite generic and can thus be re-used as shared common components.
This effect is greatly magnified when you allow yourself the luxury of higher-order functions.

## Getting There

Your options depend on the language you use.
in Python, the decorator concept seems promising.
Suppose:

``` python
class ShoppingCart:
	...
	...
	@probe
	def applyDiscountCode(self, discountCode):
		try: discount = self.discountService.lookUp(discountCode)
		except KeyError: return 0
		else: return discount.applyDiscountCode(self)
	
class DiscountService:
	...
	...
	@probe
	def applyDiscountCode(self, shoppingCart):
		...
		...
```

Now we have regained almost the original fluency of domain-only code.
The question is how to implement that crazy `@probe` decorator.
As a first (and very naive) cut, we could do something like:

``` python
def probe(fn):
	def wrapper(*args, **kwargs):
		logger.debug("calling %s %s %s", fn.__name__, args, kwargs)
		metrics.increment(fn.__name__)
		try: result = fn(*args, **kwargs)
		except:
			logger.warn("Failed %s", fn.__name__)
			raise
		else:
			return result
	return wrapper
```

This is very consistent, transparent, and easy to apply, but it does have one major draw-back:
It takes additional plumbing to regain the benefits of dependency-injection.
Part of our problem is that `def probe` is defined in global scope,
with no way to inject logging or metrics behavior. On the other hand,
many software design challenges can be solved by adding a layer of indirection.
Let's once again factor the mechanism out of the policy by interposing a *publish/subscribe* pattern.

``` python
class Channel:
	def __init__(self, name):
		...
	def subscribe(self, listener):
		...
	def publish(self, message):
		...

class Probe(Channel):
	def __call__(self, fn):
		def wrapper(*args, **kwargs):
			self.publish(callMessage(fn.__name__, args, kwargs))
			try: result = fn(*args, **kwargs)
			except:
				self.publish(failMessage(fn.__name__))
				raise
			else:
				return result
		return wrapper

# ... then later ...

class ShoppingCart:
	probe = Probe("ShoppingCart")
	
	@probe
	def applyDiscountCode(self, discountCode):
		...
		pass

# ... and finally, the coup d'etat: ...

loggingListener = ...
metricsListener = ...

ShoppingCart.probe.subscribe(loggingListener)
ShoppingCart.probe.subscribe(metricsListener)
```

Et voila! Well, sort of. We get near-perfectly transparent business logic,
and late-binding to whatever arbitrary instrumentation you like.
*In fact, this could form the basis of a heinous aspect-oriented-programming library... I should look into that.*

## Application to Testing

Our solution so-far does still have a point or two in the *minus* column,
even leaving aside the technical minutae of Python-decorator best-practices.
Chiefly, it relies on some amount of mutable global state:
the set of listeners currently attached to any given probe.
This means *the set of attached listeners* becomes a non-reentrant property.
For the specific use-case of monitoring instrumentation that's probably not a genuine problem,
but if you plan to make this infrastructure do double-duty as a behavior-verification framework for unit testing,
then you probably end up adding a dynamic-scope facility to the *listeners* set.
I usually advocate against this sort of thing, but I may have a justification for an exception:
The business-logic remains *absolutely* oblivious to the concern of instrumentation,
so shenanigans in the one domain do not impinge upon the purity or correctness of the other.

## Application to Distributed Computing and/or Microservices

One more thing yet to be considered is *travelling context*.
This becomes interesting in a more event-driven system possibly with various and distributed streams of processing.
In this case, it becomes necessary to connect the many sets of instrumentation events which ultimately stem from the same
user-visible transaction -- perhaps even in some sort of network or hierarchy.

If we think about solving this problem naively, we end up passing a transaction ID around from one service to the next.
This ends up in a formal parameter. If we agree to always use the same parameter name for the transaction ID,
then your log analysis tool knows exactly where to look in the messages to bring everything together.
However, deeper layers of business logic in your sub-services probably don't especially care about the transaction ID.
Ideally, a crash in just such code would still be properly associated to the
transaction even though it appears nowhere in nearby formal signatures. But how?

Google Cloud Functions provides one possible answer.
Each concurrent cloud-function runs in its own separate process,
and each invokation has its own log.
So long as you can associate a log to an overall transaction,
you get the so-called *through-line* view that we seek.

Let us factor out the concept of a transaction ID and handle it at the remote-procedure-call (RPC) layer.
That is, business-logic should not send RPCs directly, but through a properly-decorated interface which
passes transaction-IDs around transparently. (The precise details are beyond the scope of this document.)
Now, if for some reason instrumentation-listener needs to know what transaction is active,
that becomes a matter between the listener and the RPC layer's management interface.


