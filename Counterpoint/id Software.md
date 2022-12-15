# Analysis of John Romero's talk about early id Software

["The Early Days of id Software: Programming Principles"](https://www.youtube.com/watch?v=IzqdZAYcwfY)
by John Romero (Strange Loop 2022)

## Principle #1: No prototypes

**Point:** No prototypes; Just make the game. Polish as you go; Do not depend on polish to happen later.

**Counterpoint:** By the time id Software came together,
each individual member had ten years of game dev experience separately.
They were already expert in a tightly focused field.
They *had the skills* to know what needed to be done, largely in advance.

In less rarefied circles, most working programmers have rather less than five years of experience.
Even those with more are likely to have worked on a much wider variety of things.

So, I appreciate the "no-prototypes" mindset once you know how to do the thing,
but often you need to figure out how to even do the thing.

## Principle #2: Your team can run your game.

**Point:**
It's incredibly important that your team can always run your game.
Bulletproof your engine by providing defaults upon load failure.

He gave examples: Failed sprite -> show a bagel. Failed music -> play something obnoxious.

**Counterpoint:**
There are fields where the wrong answer is far, far worse than no answer at all.
If your software influences or reports on money, machinery, people's health and safety,
or anywhere else that decent ethics would motivate an engineering mindset,
then you need to be extra careful how you define your bagels.

**Synthesis:**
I agree with the motivation: It should always be possible to test everything and see that it all works.
But the question of what to do about bad data needs to take the business into account.

Game development is a bit of an unusual field.
Games tend to have a very compact "business model" and quite a lot more of what fundamentally amounts to art.
There is no meaningful way to unit-test art. You need to be able to make it so people can experience that art, all the time.
You don't want a hiccup in one part of the art to ruin someone's experience of the remainder -- but you do want it to be noticed (and quickly).

We now have strong practices for keeping code in a shippable state.
Version control, continuous integration, automated testing, and small increments are among these practices.
Ask what goes wrong in your field, and then figure out how cope with those failures in a smart, risk-driven manner.

## Principle #3: Absolute Simplicity.

**Point:**
Keep your code absolutely simple. Keep looking at your functions and figure out how you can simplify further.

**Counterpoint:**
None.


## Principle #4: Great Tools

**Point:**
Great tools make great games. Spend as much time on tools as possible.

Example given was a tile editor which saw use on 33 games.

**Counterpoint:**
Game shops are art shops. Art assets are the better part of most games newer than PacMan.
Great tools are a boon to artists. It keeps them gainfully and efficiently employed.
Computer games in particular are a young art form, so it's natural that we'd need to invent suitable tools.
Nobody needs a Doom level editor unless they're working with the Doom engine.

For those of us in more prosaic programming positions, chances are that we need a good IDE and a fast turn-around time on testing.
For these, you can usually throw money at the problem and win. Of course that's not everything, but it's a good start.

**Synthesis:**
You need to understand what you're actually producing, and then optimize for that.
What's consuming time, and what's blocking people's progress or productivity?
Those are the things to fix. Maybe that means hacking together some ancillary scripts or tools.
Your team, collectively, should be able to figure this out. Make sure that happens.

## Principle #5: Programmers Test

**Point:**
We ... should never allow anyone else to experience bugs or crashes. Don't waste others' time; Test thoroughly before you check in.

**Counterpoint:**
Automate your tests and then you don't waste *anyone's* time. Not even your own.


## Principle #6: Fix it *NOW!*

**Point:**
As soon as you see a bug, fix it. Do not continue on. If you don't fix your bugs,
your new code will be built on a buggy codebase and ensure an unstable foundation.

**Counterpoint:**
Normally I would completely agree with the point. However, I'd like to add a bit of context.
What I think is a bug, might be someone else's idea of mission-critical backward compatibility.

**Synthesis:**
When you think you see a bug, the first question needs to be why it's there.
Do not foolishly "fix" what is only "broken" in the eyes of a fool.
Certainly do not move on until you have gained understanding.

Once you know whether it's a bug or a feature;
Once you know why it came to be in the codebase;
Then and *only* then may you fix not only the bug, but also the underlying cause.

After you've implemented the process improvements that are going to stop that kind of bug (or misunderstanding),
then you may return to your regularly scheduled programming.

## Principle #7: Overspec the dev machines

**Point:**
Use better machines to develop on that what the game's ultimately going to run on.

In context: Early MS-DOS games were written using MS-DOS computers. But when they started working on Doom, they switched up to NeXT workstations,
and promptly became much more efficient. Which makes great sense, because at that time, MS-DOS machines were still painfully slow at big jobs,
and meanwhile NeXT machines provided an excellent foundation to slap tools together atop.

**Counterpoint:**
What if you write code to simulate universes on supercomputers? It's really bleeping expensive to spend time on those machines,
so you do your hacking on a desktop workstation. You might deploy a few limited test jobs to the department's Beowulf cluster.

I had the privilege to play with some NeXT machines when they were briefly on the market.
They were a significant upgrade over the typical desktop,
but today your cell phone is probably a beefier machine.
They really stood out for their operating system and development toolchain.

**Synthesis:**
Use the right tool for the job.
And don't be afraid to spend some money to get the right tool.

## Principle #8: Zero Foresight!

**Point:**
Write your code for this game only -- not for a future game. You're going to be writing new code later because you'll be smarter.

Romero brings up that Quake shared none of Doom's code, just as Doom shared none of Wolfenstein 3D's code.
The culture was to throw everything out and start over for each new game.

**Counterpoint:**
In a game shop you may well invent new things all the time,
but most software development work is maintenance work -- adding features to an existing system,
or integrating existing systems together in new ways.
It is a rare privilege to write a completely new foobar-engine, and it will not happen every few months.
Google search "Things you should never do, part one" for a point-by-point argument why not to throw out the codebase and start over.

**Synthesis:**
It's probably better form to say that tomorrow's requirements are hard to predict exactly,
so we should build only today's features. The key is to keep your designs and code well-factored,
decoupled, and cohesive. You will not get this perfect up front. Good enough for today is good enough for today.

Every few months someone (maybe you) will decide between keeping, adapting, or reinventing any particular wheel, module, or function.
It's absolutely good form to make that decision as simple as possible. Don't try to be future-proof, but do try to be comprehensible in the future.
And if you've done a good job of keeping coupling low (or lowering it when you can) then you'll find the changes stay localized;
You won't be throwing much away at once.

## Principle #9: Encapsulate Functionality For Design Consistency.

**Point:**
This minimizes mistakes and saves design time.

Examples given included treating graphics and sound entities as indivisible in the game,
or playing the water sound whenever water was rendered to the screen vice making it be an entity that could be misplaced.

**Counterpoint:**
None.

## Princple 10: Transparency.

**Point:**
Broadcast how you're going to solve each task, then get advice and feedback.
Do not let individuals be black boxes.
This will prevent train wrecks.

**Counterpoint:**
None.

## Princple 11: Results matter; Style is insubstantial.

**Point:**
Programming is a creative art form based in logic.
Every programmer is different and will code differently.
Don't waste time focusing on a rigid coding style;
It's really the output that matters.

**Counterpoint:**
Individuality must not excuse opacity.
It's valuable to write in such a way that others will be able to read, understand, and contribute.
If you're doing a good job, and you get suddenly put out of commission,
then someone else should be able to pick up roughly where you left off without undue hardship.

Also, there's often a benefit in running code through a beautifier as part of your version-control scripts.
The benefit does *not* come from the enforcement of a particular style. (That's a mere side effect.)
What makes a beautifier valuable is that all the programmers can completely forget about code formatting.
It becomes a non-thing, consuming zero brain-cells worth of attention. As such, the programmers are free
to place greater attention on the important things that actually require human attention.

**Synthesis:**
There are more and less helpful things for a team to worry about.
*Don't care* and *Automate-and-forget* are two perfectly valid ends of an ideological landscape on code formatting.
Either endpoint can work (given the right culture) but most of the middle is a waste of time.
Personally I'm tired of seeing *don't-care* turn into unreadable line noise, so I prefer the automation.
But as to which precise choices the automation makes? I could not care less if I tried.
In any event, some people need leadership.
