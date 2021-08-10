# Agile, the Great and Terrible

Classically (in a pre-agile world) you spend all this time trying to capture requirements,
and then get the client to sign off on them *before* you write any code.
That's supposed to mitigate the risk that you spend blood and treasure building the wrong thing.
It also means that when the client changes his mind (which happens) then you can bill for a change order.
Most software projects ended in failure: canceled, blown budgets, sweatshop management, or all three.

Then we had the Methodology Wars in the 90s, and now pretty much every shop wants to be *agile* in one or another flavor.

## *Agile*? You keep on using that word...

Go read the [Agile Manifesto](https://agilemanifesto.org/)
and the [principles behind it](https://agilemanifesto.org/principles.html).

Let me sum up: There are more or less extreme variants, but on balance *agile methods*:

* Accept late change as inevitable -- indeed, embrace it as customary -- and seek to reduce its cost.
* Try to organize people and work so that each increment of effort adds measurable and consistent value to an existing system in a defined and short time window.
* Focus on regular interpersonal communication rather than up-front specification and design.
* Advocate a varying number of technical practices such as refactoring, test-first development, and pair-programming.

### Sounds great! Where's the fire?

Make no mistake: Agile is good in some ways.
Done well, it keeps both client and developer dopamine receptors happy with a periodic rush of success.
The client enjoys a regular stream of working (and presumably well-tested) features in exchange for a predictable stream of money.
Priorities can change from month to month, and it does not cause a crisis.
Projects can still be canceled, but on better terms and with greater foresight.
From one perspective, Agile teams do a better job justifying their pay-check each month, and they tend to have more satisfactory working conditions, so environmental selective pressure applies to the job market and pretty soon Agile is all anybody wants to hear. *And that's just fine by me.*

But agile is also terrible.

## Terrible Documentation:

Someone important is going to get promoted and move to another department, or leave the company, or get hit by a bus. Or maybe the competitor down the street starts offering a 50% bump in salary and the whole team up and jumps ship. Now you’ve got a serious problem. You have the code, but that’s the least of your worries. You now need precisely that comprehensive documentation which your agile team could not be bothered to write.

Reading undocumented code is like archaeology: You might learn many useful and interesting things, but not in a useful order. If you keep good notes, eventually you come away with most of an understanding, but there are still plenty of things you can never know.

Well-documented code reads like a textbook. It explains not just *how*, but also *why* and *when*. It points you in the direction of the knowledge you seek, and it takes pains to anticipate your questions. Someone can come into a well-documented module, spend a little while reading, and know exactly how to adjust things to handle some new requirement. (Of course it then takes an ounce of discipline to update the docs at the same time.)

As of mid-2021, my sources tell me that agile teams don’t typically spend much time creating excellent documentation. *They’re not measured on it.* So any time you have a personnel change, you’re going to pay that cost again. And realistically, any time some feature hasn’t been touched in a few weeks, that might as well be staff turn-over: nobody remembers fine details that far back.

I’ll just point out that all the successful programming languages throughout time have had really effective documentation available either online or as an affordable book. Generally this means both tutorial and reference.

## Terrible Continuity:

In principle, *agile development* basically tells you not to put too much faith in, or spend too much time on, long-range plans. Rather, you break scope into a procession of small bites: *things we make this sprint* and *all else*. Then you treat each sprint as a little mini-project. You make it, and then hopefully you do a retrospective and learn from it. Oh, and there's one extra requirement: you're supposed to maintain (or regain) design flexibility by refactoring as you go along, so that progress does not slow to a low-crawl after a few sprints.

From one sprint to the next, we tend to lose track of context:

* What all have we built?
* What compromises did we accept along the way?
* What odd and surprising things did we agree to?
* Does this weird bit still need to exist?
* Is anybody even looking at that one report?
* This line of apparently-inconsistent code: is it a bug or a feature?
* What plans have we to rectify the iniquities of our haste?

Zealots will tell you to put it all in a test. But alas, not every aspect is amenable to testing. How do you write an automated test that asserts we are testing for all the right things?

## Terrible Execution:

One of the biggest difficulties with agile practices is that they are part of a system. The practices have synergies, but individual practices don't have outsized impact on their own, and they can often feel counterproductive in isolation. Yet few people are comfortable with sudden comprehensive change. That makes it very difficult to drive acceptance and adoption in a team that hasn’t thoroughly drank the proverbial kool-aid up front. That is, you want a religious order of zealots and acolytes for best results. I have deep spiritual reservations about this state of affairs. Reality doesn't care what you believe. Reality is most people don't love change. We don't have zealots aplenty. We have regular Janes and Joes banging out code, with that infuriatingly practical *definition of done* on the order of *works for me; checks in OK*.

We profess to love test-driven development. In practice we see developers write tests after-the-fact, aiming to satisfy the continuous-integration system about the level of code coverage.

We profess to love refactoring, but then get choked up about the time investment in making meaningful improvements to the design of our systems. Yet we habitually pay the cost of dealing daily with poorly factored code.

Some of us profess to love pair-programming, yet continue to work alone. (Perhaps we are indeed hopelessly alone in our profession...)

## It does not have to be this way.

Seek, and ye shall find story after story of teams and companies that claim great success with full-strength undiluted agility. I have no reason not to take them at their word. But I do have to believe that their success was attributable to more than just a fancy process.

# In Conclusion...

Things are better than before, but there remains
[no silver bullet](https://www.rbvi.ucsf.edu/Outreach/pc204/NoSilverBullet.html).
Key quote: *The hard thing about building software is deciding what one wants to say, not saying it.*
Software is hard to do at all, and rather more difficult still to do without making a mess of things along the way. The agile way is one way to organize the management, but not one without flaws.
