# Software Testing, Volume Two

Recently I was talking to a development manager who told me he prohibits testing.
Was this a strict formal-methods shop? Nope! Just a completely different set of ideas.
And absolutely convinced that it was counterproductive (even worse than useless)
to have developers write test code. He had numbers and data to back it all up, too!


## Apparently *this* had to be said.

Since you're human and fallible, and you recognize the fact, you necessarily have
some process for trying to flush out development mistakes before calling yourself
done with some fragment of code that you *intend to ship.*

1. Maybe you run it manually and try a few cases.
2. Maybe you write a test script to put the artifact through its paces.
3. Maybe you hire an expert testing engineer and tell the mainline programmers to focus on function.
4. Or maybe you do nothing, in which case you are a danger to others and should change careers.

Regardless of how you do it, we call that process "testing".

Testing is a completely different skill from ordinary coding or design,
but it's got to be done because *people get things wrong* on every level.
* What if your proof of correctness is flawed? (Did you ever think of that?)
* What if your proof is fine, but the transcription into code is flawed?
* What if a camel spat upon the version control system?

In practice, we assess risk to determine how much paranoia we embed into the testing process.
Maybe the hazard is report layout cosmetics, so we can be satisfied with a quick glance.
Maybe the hazard is astronauts getting lost in space,
so we crank the entire development process [up to eleven](https://en.wikipedia.org/wiki/Up_to_eleven)
and achieve SEI CMM level five.

*PS:* No, you are *not* allowed to simply "get it right the first time".
Or at least, you can't assume you will. That would be a position of smugness and pride,
which goes before the autumn. Or the fall. You pick.

*PPS:* Trivial one-off commands don't fall under the heading of "intend to ship."


## What about that test-averse development manager?

Once we agreed on what *testing* fundamentally is, he then clarified: that he wants his
QA department doing integration testing, and specifically didn't want normal developers
*wasting time* writing unit tests.

I intend to convince you that -- well -- **certain practices which I call unit-testing**
are worth their while many times over if you care about releasing reliable software
systems. But the very smart and well-informed development manager thinks quite the reverse.

This turns out to be several interacting paradigmatic differences masquerading as a single idea.
Everyone wants to get a working system but the choices you make at one level influence the
effectiveness and value of later options. Impassioned arguments for doing task X a certain way
assume you also unmentioned predecessor task Y a certain corresponding way.
Rebuttals often take the form of naming task Y and assigning it a different approach,
which is then gets called unrealistic or out of touch etc.

Practices can only be understood as part of a coherent system.
The system may work beautifully, but each individual element is rarely *best-in-class*.
Rather, what survives the test of time is *collectively best-fit-together*: completely different.
As far as I can tell, the dev manager in the first paragraph is in a systemic local-optimum
where coders turn out code of a certain level and a separate department runs acceptance tests based on formal requirements.
I assume there's some sort of break/fix feedback cycle.
I am sure there's a better way in the grand scheme of things,
but perhaps out of reach from his segment of industry.

So the first communication hiccup was this: Absolutely they do test, but not by developers.
And also, he was convinced of nefarious things about unit tests: Basically, that people ordinarily cheat.
Now I'll be the first to admit: I've seen plenty of cheating on the test, but it seems to be cultural.
Not all teams are prone. Those few which seem most prone, seem to also have unhealthy norms and pressures too.
Fixing that involves cultural change.

## Digression on the subject of Statistical Data:

Surveys of development shops will give the most weight to the industry's modal configurations.
If you then take statistics from such a survey, you can only interpret that measure
in the context of whichever structures, conditions, and incentives are most prevalent.
Things do change as new ideas sweep across the land, so conclusions that were valid
ten years ago might not be valid today, or in an unconventional context.

A perfect example of this is given by the company SAS Software.
In an age when code was mostly built by command-and-control, with long-march tactics,
most software was late, over budget, and of poor quality if it even ever shipped.
SAS Software went the unconventional egalitarian and empowered route,
figuring that excellent work-life balance and shared ownership would yield excellent results.
It did, or so said the [article I read](https://www.google.com/search?q=sas+software+HBR)
in Harvard Business Review many years ago. (These days, it's probably behind a paywall. Sorry.)

So the point is, you can't manage by the industry averages unless you want to be average.
If you embrace a different system, expect wailing and gnashing of teeth in the short-run while people adjust,
even if the new system is globally better.


## On Organizational Change

Chances are, whatever environment you find yourself working in, it will be difficult
to make any change. Organizations tend towards local-optima as perceived by the
people who have the most influence. Any slight perturbation is a threat to the
status quo: Either the culture stamps it out or adopts it; there's not much
middle ground.

Yet change happens all the time.
You can make it happen, watch it happen, or wonder what happened.


## When Test?

Once code is written, testing is a risk-mitigation effort, not a harm-reduction effort.
You should therefore test *before* the risk is made manifest and the harm comes to pass.

Testing provides feedback. It's well-known that a programmer's efficiency is
inversely proportional to the length of her feedback cycle. So test early and often.
Ideally, it should be an easy-button any programmer can press whenever to
get prompt feedback (seconds to *at most* a couple minutes) and fix problems
while context is still fresh in mind.

Really, unit testing as I advocate is a design activity -- one that happens to also
yield a convenient artifact of independent value. It meshes perfectly
with the venerable process of top-down design by stepwise refinement. That puts the
construction of the test *before* the effort to make it pass.
It does not only validate the work: it also guides the work, allowing you to
spill details from your [conscious working memory](https://www.simplypsychology.org/short-term-memory.html)
and thus focus more deeply.


## Why Automate the Tests?

We've established that the purpose of *test* is not only to be a quality gate,
but also to provide feedback someone can use to repair defects.
A simple system-wide pass/fail may stop you from shipping garbage,
but it won't do your ship date any favors either. You need the detailed feedback.

The purpose of *automating* tests is to remove drudgery, variability, and delay.
Furthermore, test-code codifies your expectations. If your expectations are flawed,
the reviewer has another chance to catch that divergence while looking at your tests.
These should be uncontroversial benefits.

Most times, it's easier and less effort overall to take the extra few seconds and put
what you might otherwise test manually (say, at a REPL prompt) instead into a test module,
because it's then reliably repeatable.
It also forms a scaffolding to which more assertions may attach.

What about option three? I've never had the privilege. Some shops work that way.
Chances are, your dedicated test engineer is essentally doing option two under the
covers with . 

I do have some separate words on the subject of [quality assurance as a department](code_qa.md).

Here are some objections and counterpoints:

* *It's a waste of time; we have a QA department for testing:*
  Lucky you. But that's beside the point.
  Regardless of who does the testing, either the testing is manual or automated.
  That is, either some human being is following a detailed and comprehensive test
  plan *during the test*, or else they've codified the details of that plan into
  something a computer can check at the press of a button. Anyone competent to
  perform the latter counts as a programmer in my book, even if they're using
  some fancy test-automation tool. And maybe that's right for you. Your mileage may vary.

* *Code coverage ratios are no indication of test quality:*
  Non-sequitur. The question here is whether the tests you *do have*
  should be manual or automated, not how many or what kind.
  (That's a separate rant.)

* *My programmers habitually write perfunctory/useless/bad unit tests:*
  You have bigger problems. Such programmers habitually write
  perfunctory/useless/bad mainline code too,
  and thereby keep your integration-test people employed catching a
  constant stream of silly mistakes. Educate them or replace them.

* *My assertions are about whole-program interactions with the environment:*
  Non-sequitur. Anyway, we call these "integration tests". They're good for
  making sure your environment is set up correctly, but only minimally effective
  at flushing out mistakes. Perhaps this is one of those perfunctory/useless/bad
  tests from the previous bullet point?

* *We should be doing integration tests, not unit tests:*
  Non-sequitur. Later I hope to convince you that integration tests
  are wasteful (they take a long time to produce feedback)
  and feckless (they only catch the easy flaws, not the long-tail),
  but for now I'll refer you back to the question whether your
  *integration* tests are manual or automatic.

* *This is GUI code; you can't test that automatically:*
  Technically you can, but special tools help a lot.
  Still, keep busines logic out of the U/I layer like a grown-up.
  Code review and other quality gates will take care of the rest.



This is a completely different question from who creates the test, or when, or how big.

TDLR: The QA department, if you have one, is going to have a differ
