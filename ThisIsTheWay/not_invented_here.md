# Not Invented Here

**A tale of long-lived software**

Banks are (in)famous for keeping bleeping-old software running.
Mine has kept COBOL running on mainframes and minicomputers continuously from the 1960s through the present day,
with no end in sight. And nobody is writing any new systems from scratch in COBOL. *And that is OK.*

You see, those old COBOL systems work. Every so often someone asks for some or another minor adjustment,
and of course there was the Y2K kerfuffle a few years back (was it 20 already? My how the time does fly!)
but for the most part those bits don't rot.

As it happens, COBOL programmers come in two flavors.
There are the geriatric wizards who are putting off retirement on account of significant inducements,
and there are the fresh-out-of-college kids who stumbled into COBOL by happenstance of hiring practices.
For some reason the COBOL team doesn't seem to have any journeyman programmers.

As it also happens, I think I know the reason why.

## Why no middle-aged COBOL programmers?

Back in the early 90s, all the college CS programs taught modern languages like Pascal, Ada, Scheme, or Haskell.
If you were diligent you got to use some C or C++.
Java wasn't even on the menu until some massive marketting efforts by Sun Microsystems.
Nobody'd heard of Python or Ruby or indeed any of the languages we'd consider sexy today.

On the other hand, MIS programs typically taught some COBOL and a bit of Fortran for reasons nobody explained to the CS students.

In retrospect, the reason for the difference is obvious. COBOL and Fortran were used in industry,
but they had long since passed out of the realm of what this still-young "discipline" of
computer-science considered interesting as an object of study.
MIS programs were designed as an industrial training pipeline,
but undergraduate CS programs -- or at least the one where I went -- held themselves up to be a proper academic displine.
The computer -- and by extension the programming language -- is to the computer-scientist as the telescope is to the astronomer.
For the same reasons each always wants to use the latest and greatest but will make do with what they can afford.

The big difference between computists and astronomers who grew up in the age of the personal computer is that (interesting) programming languages are basically free,
not counting the time spent learning them. This was especially true in the age of Gnu and Linux and burgeoning Internet access.
So while the astronomy students might occasionally head a couple hours out of town for a night at the university observatory,
the comp-sci kids left the modem running for an hour *just once* and got the Gnu Compiler Collection on a fresh distribution of Slackware.

There may also have been some language snobbery going on. And I may or may not have been affected by said snobbery.

The moral of the story is that if, in the early 90s, you went the MIS route, then the Y2K bug made you very *very* rich and then you promptly retired.
But for those of us who wanted to write code *for a living,* we gained a sweet-tooth for the newest and best thing.

## Instead of COBOL, What?

A lot of things. Java and Python are the heavy hitters.
I happen to pay the bills with Python at the moment, so let's pick on Python.

Put yourself in the late 90s, early 2000s. And remember that the number of programmers is (still!) doubling about every five years.
So at this point, the majority of the programmers in your organization have this mental comparison of what it was like to code at university,
against what it's like to code for work. And chances are, some of those former whipper-snappers have wiggle-wormed their way into having the
power to make some technical decisions. Someone uses Python for a minor outlying and unimportant report or whatever.
And they're done like instantly.  Or rather, that's what it seems, because actually they did part of the work on their own time
in order to make Python look attractive to management. Well, management was convinced to allow Python hither and yon,
but not everywhere because all the serious code has to be written in a serious language.

Fast forward a few more years. Serious new things are done in Python. Quite a lot of the old systems are still around.
In fact, some will never die. But now Python is entrenched, and you can't kill it either. But that's not a problem.
You can actually hire Python programmers, and they sort of come pre-trained.

Around this time, standard libraries are young and the fields are fertile for the growth of new ideas.

## Invented Here!

In 2000, a fairly standard web site ran on Linux, Apache, MySQL, and PHP or Perl or Perhaps Python.
It even has a cute name: the LAMP stack. But the internet was still new-ish and so lots of people had lots of problems to solve.
With no central authority, most problems got solved a multitude of times and ways.
A few of those solutions bubbled up and eventually became standard,
but often as not each shop had its own local "special sauce" that the techies had sold to management under the guise of "competitive advantage".

> **Aside:** You cannot buy a competitive advantage off the shelf.
> But that does not mean to build when you might buy.
> There is *no profit* in building what you might buy.
> It means you should focus your creative efforts on aspects of your business that
> differentiate you *in your customer's eye* from your nearest alternatives.
> Make your product or service *worth the money* and otherwise control costs.

Anyway, in those days much code had yet to be written for the new networks and the new machines in the new languages.
Shops often built what they needed, understanding they'd maintain it into the future.

And then the future happened.

## In the Future, Your Code is a Liability

Let's pick on Python again. Perhaps you noticed that Python -- out of the box -- is not especially great with crunching lots of numbers.
Today, you'd install `numpy` and maybe `pandas` and you'd be on your merry way with GPU-enabled vector operations and nice
convenient relation-like objects that expose data parallelism through the red magic of operator overloading.

In the early 2000s, you were S.O.L. *Simply* Outa Luck.

Or, if you were a large institution, perhaps you cooked up a Python extension in C.
In due course, you cooked up an entire witch's brew of extensions,
each targeting aspects of your system that ran too slow and couldn't be optimized any other way.
But let's stick to the Data Scientist's favorite Swiss-Army knife.

Now at some point, NumPy and Pandas become pretty much the standard way of doing things everywhere.
Well, everywhere except your walled garden. And the number of programmers continues to grow exponentially.

You don't have the staff to compete with Pandas.
Your homegrown subsystem is *objectively* just fine -- maybe even better -- but the rest of the world is contributing Pandas either in kind or in money
because *they* have the wisdom to buy-not-build and *they* came along after Pandas was already a thing.

You'll recall how Python took root in your organization? Yeah. Pandas just did the same thing.

## And then there were two. Twice.

First it was the new shiny language. Then it was the new shiny library. Tomorrow it will be something else.

There will always be another shiny thing, and although growth in the coding field must eventually saturate its market,
that inflection point does not seem to be near on the horizon. So the pressure to chase the latest shiny thing may
someday decrease a little bit, but it will never go away. With each passing year the oldest of the old guard retires,
and another round of the technology treadmill becomes de-rigueur.

All technology adoption goes through a set of stages. The difference between the popular and unpopular is a matter of degree, not kind.

* Lunatic Fringe -- Tries anything and everything.
* Early Adopters -- Encouraged by the lunatic fringe, with a higher tolerance for risk.
* General Population -- Seeing social proof from the early adopters, these form the high-growth period.
* Stragglers -- These are governed by "wait and see" attitudes and value stability, but don't want to be left behind.
* Complete Luddites -- Deplore change and only migrate to satisfy a regulatory requirement.
* Non-Market Participants -- For whom the product is irrelevant.

I don't think anyone would argue that a large bank should be at the lunatic fringe of anything at all.
Even early adoption is pushing it. Your very largest organizations could be forgiven for falling into the "straggler" category,
but I'll argue that *Complete Luddism* is conduct unbecoming of a capitalist.

## Heads: Carrot

Programmers, as a rule, do not concentrate the dumb.
In fact, you're hiring programmers precisely because they are at least smart enough to mix requirements with caffeine and produce code.
This may be a low bar, but it's not *that* low.

And what's more, working programmers these days are increasingly concerned with quality-of-life.
It's a topic of conversation amongst not only the youngest generation,
but also those who've survived a few rounds of garbage collection and even the occasional tenured professor.

Programmers (and indeed all employees) these days are concerned with gaining transferable skills.
The days of defined-benefit (pension) plans are all but forgotten,
and with them the idea that employees will work decades for a single employer.
Perhaps counterintuitively, if you want to keep your employees *or your customers,* you need to make it easy for them to leave!
People just don't tolerate a prison cell anymore, even if it is lined with gold and has free internet access.

You *do not* need to be constantly chasing the latest trend.
You *do* need to have a reasonable uptake of widely-accepted standard solutions to problems,
even if you have your own perfectly-good proprietary solutions.

## Tails: Stick

As such, if you do not want your turnover numbers to be the laughingstock of glassdoor.com,
then I submit to you the cautionary tale at [A Case of the MUMPS](https://thedailywtf.com/articles/a_case_of_the_mumps)
wherein our hero -- a young developer -- stumbles into a job with an obscure cryptic language and skills that don't transfer.
When he finally took stock of his situation after two solid years, he got the heck out of dodge and never looked back.

I can hire a Python developer with SQL skills and experience with Pandas.
I cannot hire someone with experience on a proprietary in-house system.
And nobody will hire *me* on the strength of experience with said proprietary in-house system.
Faced with too much historical baggage and not enough corresponding benefits,
your best programmers will be easily tempted to take their talents elsewhere.
Therefore, proprietary in-house systems are a competitive *disadvantage* if you
believe a high-talent work-force is worth the trouble of keeping around.

> The impossibility of a skill-set has not totally stopped recruiters from trying to hire for it.
> Once upon a time, I had a recruiter tell me he was looking for people with five years experience on Itanium assembly language for a confidential client.
> But at the time, Itanium systems were still vaporware and, in case you hadn't noticed,
> Itanium never did make it to the consumer market where some learning could be had.
> My best guess in retrospect is that Intel was expanding their compiler team so `icc` would be ready in time for Itanium's launch,
> and that the recruiter was the confused victim of repeated re-tellings of the job requisition.

## A Way Out Of This Mess

Code is not an asset. Code is a liability.
Code that (nearly, merely) duplicates the function of an off-the-shelf component is a liability that doesn't even pay its own rent.
It's the worst, most insidious form of vendor lock-in: to ourselves and our own unwillingness to let the past go.

To be fair, change is hard. But change we must. All life is change, and stagnation is death.

The key to all nontrivial life (say, more than single-celled organisms) is controlled death.
In the realm of biology we call it apoptosis:
The controlled, programmed cell-death of parts that have outlived their usefulness.
Apoptosis during gestation is the reason we don't have webbed hands, and can thus move our fingers independently.
During a viral outbreak apoptosis limits the damage an infected cell can do.
The failure of the apoptosis mechanism is the key ingredient in what we call "cancer".

If we want to keep our codebase, and the people who work on it, healthy and vigorous,
then we must not lose sight of our obligation to kill off the parts that aren't pulling their weight anymore.
Proprietary "invented-here" subsystems that have mature open-source alternatives are chief among the candidates for removal.

Again, change is hard. And change should not be too sudden. We need a process and a plan. Here's a candidate:

1. Non-critical projects allowed to use the new toy.
2. A simple translation-layer or storage-abstraction for data formats between old and new toys.
3. No new projects shall rely on the old toy. (Enforced through convention and strong leadership.)
4. No new modules (created after day XYZ) shall rely on the old toy. (Enforced through version control pipeline.)
5. It becomes a lint warning to mention the old toy. You are strongly encouraged to upgrade everything you touch.
6. It becomes a lint error to mention the old toy. You must upgrade what you commit.
7. Remaining mentions of the old toy are audited to determine if the associated code is even still used / maintained. Obsolete code is archived and removed.
8. Recalcitrant old-toy afficionados are made an offer they cannot refuse. Well, not if they want to keep working here anyway.

This sounds a bit harsh and *that's OK.* It keeps your codebase and your people sharp.
People subject to this process cannot fail to learn the new toy.
And in some reasonable amount of time, you're back to the nice and tidy situation of having one solution per problem.

## Will Management Go For It?

Look. We've figured out that we must hide the details of sausage manufacture from sausage consumers.
We do not have a story (much less a sprint) for "refactoring". That's just part of the process.
It's built into the estimate because it's a process *we know we must perform* in order to keep a healthy
codebase and *thereby* an acceptable project velocity. You aren't done until the math is expressed in lowest terms.

Management will never agree to pay for something that they don't understand why it's *absolutely necessary right this minute.*
If they can *name* it, they can *cut funding* for it. (Incidentally, this is also why security tends to get overlooked until there's a breach.)

If you are a software professional, do not tell the management things they can use to undermine your ability to do professional-level work.

## On the Other Hand...

Don't go overboard. You still need to deliver.

**Implications are left as an exercise for the reader.**

## And in Conclusion...

I've personally followed this plan (not counting aid from lint) and managed to rid my employer of some obsolete modules,
support for which was holding back progress on other fronts. It took many moons but I got it done using less than 5% of working hours,
or a couple hours per week. The other 95% + was normal progress on normal things.

If we cannot budget 5% of time for cleaning out the old dead weeds, they shall overgrow our walled garden.
