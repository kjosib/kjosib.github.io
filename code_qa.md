# What about a QA Department?

I've mentioned that some shops distinguish coding from testing, and strictly delegate testing to a Quality Assurance department.
The argument is that people are crummy at writing tests for their own code, in comparison to what you might get for the same
resources (money, time, etc.) if someone else does the testing.

I'll get back to that, but please first remind yourself that [quality depends on context](code_quality.md).

Personally, my experience with Quality departments comes primarily from working in the company of more-traditional engineers.
You know the sort: Mechanical, Civil, Chemical, Piping, etc. etc. etc. Specifically not software. I'll get back to that too,
but please permit me to push one more digression onto the cognitive stack.

----

In comparison other kinds of engineering, *software* engineering as a discipline is still in its infancy.
Coincidentally, *engineering in general* as we know it today is also fairly young on the scale of human history:
Originally just about anyone with a pencil and a shingle could call himself an engineer and get work designing things
that people would then build. If your bridges fell down and killed people in Anno Domini 900, that was just too bad.
The situation changed unevenly over the last couple centuries: Precise details vary from place to place, but broad patterns apply:

* An engineer and his employer are held legally liable for harms caused by his designs
  (but typically insulated if construction diverges significantly from design).
* A *professional engineer* (by whatever nomenclature) must hold a license to practice in or for a given jurisdiction.
* An apprenticeship period of several years is required, during which a candidate must work under the supervision of a PE.
* Violation of an official code of professional ethics results in sanctions such as losing one's license to practice.
* The output of an engineering activity is expect to describe, in sufficient detail, a solution which is
  *fit-for-purpose*, *safe* for the general public, and which *complies* with applicable laws and regulations.
  (If these cannot be achieved, the engineer withdraws from the engagement.)
  In contrast, *economical* is on a best-effort basis subordinate to the hard mandates.

On the other hand, if you look around the average software development shop over the decades from, say, 1970 - 2010
or even the shrink-wrap (or click-wrap) labels on commercial software, you find the opposite.
Liability is disclaimed. Warranties are disclaimed. Fitness for any particular use is disclaimed.
In this kind of environment, it's no wonder that quality suffers.
(It's almost as if the industry, unfamiliar with quality workmanship,
collectively chose instead to shirk its moral duties.)

In time it became customary in many shops, whether outsource contractors or in-house staff, to have a QA department.
But remember that software engineering was immature.

----

It's time I pop the stack and return to the topic of how the *Quality* department works in an engineering and construction company.

*Quality Assurance* on the task force knows full well they can't read a P&ID or a plot plan, and won't try to evaluate one.
On the other hand, they'll watch people work, ask questions, and report back to management on how well or poorly
the task force is complying with its defined work-processes. They'll make *observations* (think "near miss") and
*findings* (think "violation") which the other teams are then compelled to address meaningfully.

In theory, there's another layer: when deficiencies come to light, someone needs to track the ultimate cause back and improve the process.
In practice there's generally a serious threat of expensive litigation, so there's a sense in which QA is also CYA. (But that's tangential.)

*Supplier Quality Survey* is a different discipline, often more associated with the procurement department.
That's the group of people who travel to watch procured components get built and tested,
to make sure vendors do as they're contracted and meet the specifications to which they've agreed.
SQS people are very well trained and coordinate with a sizeable network of specialists.
But they are themselves subject to the same quality-assurance process as every other team.

----

Popping the stack once more, let's get back to the alleged duties of a QA department in a software shop.

If you follow the SEI CMM model, you probably have someone checking to make sure that each element of
your organization is either following the written procedures or updating them to match practice according
to another defined process for organizational learning. But let's face it: unless you're a space agency,
you're probably not running CMM level five. For that matter, level three is darn good as indie shops go.

The more usual hearsay about QA in software is that they orchestrate, develop, and run tests.

Tests.

Let that percolate for a moment.

In other words, these shops are separating *production* and *evaluation* into two different departments.

Time for another digression. The conversational-context stack is getting some exercise.

----

There's a *manufacturing* concept of *quality control* where you look for defects in stream of products
in order to identify what about your production line needs to be fixed. This is naturally a separate
department from manufacturing *production*, but hold on a second.

Let's say, through random sampling and destructive testing,
your QC department finds that all the blue jeans coming off sewing machine #5 have loose buttons.
Then of course you'll go see what's up with machine #5. Is it the machinery or the supplies or the working conditions?
Only rarely is it the operator, but it's a hypothesis you can test nevertheless. Long story short,
pretty soon you've troubleshot the situation and quality is back up to where it needs to be.

Anyway, the sexy part of quality control isn't tearing apart and inpspecting all those blue jeans.
It's the entire creative engineering discipline of figuring out what categories of things might possibly go wrong,
and how we might catch those things at reasonable cost, and then once caught, how to investigate and fix problems.

----

OK, enough about that. Popping back into software land.

Clearly, the manufacturing metaphor is the wrong one.
Developing software is much more like engineering than like manufacturing.
Software developers do not churn out a stream of identical interchangeable widgets.
Neither do we, however skillfully, convert effort and supplies into a precise manifestation of a precisely specified form.
Software developers are inventing: bringing ideas and concepts to bear in an organized but still organic process
to turn abstract ideas into more-precisely-specified, less-abstract ideas. Our work-product is pure thought-stuff.
At best, we can follow a process that promotes and facilitates good ideas.
Maybe Frank needs more RESTful sleep(1), or Jill might benefit from a quieter and more comfortable working environment.
Maybe *(and this is my central claim)* outside of situational hygiene factors like those just mentioned,
a certain structured approach to development can bring out the global optimum in everyone.
If true, an engineering-style QA department would be pushing for that approach to be documented, validated, and verified.

So, what's actually happening with these test-oriented software QA departments?
I've never personally had the pleasure of dealing with them,
but a gestalt summary of my impressions from many different accounts is roughly this:

Software quality professionals tend to be very talented people with a very particular skill set.
They understand not only the overt requirements,
but also how interactions and trade-offs make fertile ground for mistakes.
They know how to create scenarios and test cases that give the test-subject every reasonable opportunity to fail,
without pointless exhaustive repetition.
They can make tests that test a large part of the system, or a very small and isolated part of the system, depending on your situation.
If they do their job well, you'll end up with a nice piece of ancillary software:
a test suite, which you can run and tell whether your main product meets certain codified criteria under a variety of situations.
In short, they perform a manufacturing-style quality-*control* operation in an environment where no two components
should be held to the same description or criteria. It sounds like a pretty thankless arrangement.

As such, I shall henceforth refer to the software test/break department as QC, not QA.
Now I ask you: **How does your QC department earn its pay?**

*Assume the product passes all tests.*
Then what? Does that mean it's ready to ship?
Well, you have to trust that your QC department did a good job covering every category of flaw
that someone might stumble into, except the ones you don't care about (say, for business reasons).
I can tell you right now that they did not, if they're only writing whole-system integration tests.
If your program does anything more complicated than convert Celcius to Fahrenheit,
then there are simply too many cases to contemplate, much less enumerate.
(Briefly ponder how you might test just the addition operation.
Decide what fraction of all possible inputs you'd consider,
and how long that might take on a modern machine with, say, a 64-bit word length.)
To get any comfortable level confidence that a system works correctly,
you need to be confident of two things:
* all the parts are correct in terms of what they do, and
* all the connections between the parts are correct in terms of how they interact.
As such, if you want reasonable assurance of a properly tested system,
you need to be testing individual small components and very small groups *in isolation* from the remainder,
both for happy-path and weird corner-cases. **That is called unit-testing.**
And clearly it has to evolve in parallel with the invention of all those small components.
Yes, you also want a show-and-tell with the customer to make sure you're building the right product,
but that's a small fraction of the overall effort.

*Assume that the product does not pass all tests.*
Then presumably that means two things:
Some flaw escaped Dev and made it into a build, and also now we can't ship.
*Now what?*
Well, clearly you file a defect ticket and route it back to a developer who's vaguely familiar with the affected module --
*if* you can even figure out which module is affected at this late stage,
and *if* you even have a coherent modular strategy that separates concerns rather than, say, tasks or authors.

The point is that **QC earns its pay by finding flaws well and giving good feedback** to the dev team about said flaws.
*Here's the key takeaway:* the feedback loop between Dev and QC is the inner loop of a quality product.
Whatsoever tightens that loop gives you more quality, faster, and cheaper. *Quality is Free!*

Your better QC engineers are some of the best developers,
because they know how to anticipate the way things might go wrong.
And vice-versa.

----

One last digression out of software and into, of all things, manufacturing.
There's a fun and educational novel called *The Goal*. It is a thinly-veiled introduction to the theory of constraints.
At the end is a brief reiteration of main points, and how to apply them in a wide variety of business contexts.
The big ideas are roughly recalled:

1. *Your throughput is limited by your slowest operation.*
   That's your hot path: the only place worth optimizing.
   This is the fundamental theorem in the theory of constraints.
2. *That same limit sets the maximum worthwhile pace for other operations.*
   Moving any faster only creates a backlog of incomplete work-in-progress.
   Beyond your batch size, that backlog doesn't do you any good, because of rule 1 above.
3. *Put the slowest walker at the head of the line, and the fastest at the end.*
   This is metaphor. The image is of a tight line of hikers who do not spread out.
   In concept, this is about minimizing even the space available for work-in-progress to pile up
   by making the slowest process also the *authority* over the overall pace of production.
4. *Applying the preceeding insights tends to shake loose some excess capacity.*
   Machine time and manpower are generally the first to show up.
   You might even trade down on some of your overpowered systems to free up capital.
5. *As much as possible, that excess capacity should be used to supplement the hot-path.*
   Even if it costs more per unit than the ordinary process,
   it's better than wasting time and money on literally any other manufacturing process.
6. *Obeying the rules above lets you allocate both creativity and resources in the most efficient way.*

Passing comments:
* There's a related concept in the deployment of troops to primary and secondary military objectives.
  The standard model is you put enough force to assure a primary win, but not too much more, because the rest
  is better spent on secondary objectives.
* Point five above is specifically relevant to a certain someone's numbers and data. He knows who he is.

----

I claimed, without proof, that the feedback loop between DEV and QC is the inner loop of your quality process.
If you have no such loop, then I don't know why you bother with a separate QC department.
But if you do have such a loop, if it's the inner loop then clearly you have some other,
smaller loop not involving the QC department.
I don't know how you run your shop, but there is only so much scope for creativity in this particular regard.
I'm inclined to invoke the principle of the excluded middle.

How, then, can we optimize that DEV/QC feedback loop?

I want an simple button that any developer can press,
which will promptly report on three things for *every* known or planned component (or small assemblage thereof):
1. Which detailed functional requirements are currently working or failing tests, and
2. For the failing tests, how is the failure detected? e.g. a wrong return value, an incorrect exception raised, etc.
3. Any stack traces collected along the way from unexpected exceptions. (Current state variables wouldn't hurt either.)

That easy-button provides repeatability, reliability, and convenience.
If the results come back in less time than a coffee break,
the easy-button also provides a serious productivity improvement:
the developer need not lose the state of flow, or deep mental context.

**Quality Comes First.**
That easy-button needs to exist, at least in rudimentary form, even before the first line of production code is written.

It is not long before this turns into test-driven design,
and you fold the QC department back into your dev team -- but with titles like *senior software engineer* or *software architect*.
Maybe they still spend most of their time translating requirements into tests,
but they're doing so in a way that makes quality lead the effort, rather than constantly be chasing a runaway train.
Before you know it, your junior developers pick up on habits-of-mind that make them great software quality people.

Oh yeah. The easy-button? It's usually called *xUnit*, where the *x* is the initial letter or syllable of your programming language.

----

*Epilogue: You should probably keep the dog-and-pony show. Customers really eat that up.*
