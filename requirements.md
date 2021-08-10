# Requirements Capture and Tracking for Humans

These days, [Agile Development](agile_the_terrible.md) is all the rage, so let's assume:

* Lax process controls relying on human (un)reliabilty.
* Minimal if any documentation.
* No clearly-delineated relationship between client and development team.
* Regular and frequent unplanned change.
* Also, unit tests.

That would never fly in a mature organization, right? So let's lay off those assumptions and instead suppose we're in one of those many organizations subject to regulatory engineering controls, but which fancies itself agile anyway. New assumptions:

* Strict enforcement of testing and code coverage requirements through complex and powerful tools.
* Barely enough internal documentation to get by most of the time.
* Well-defined if casual working relationship between devs and (internal) clients.
* Quarterly outlook reports resulting in new multi-year initiatives to replace the ones from last quarter.
* Occasional random new requirements of priority levels varying between *now* and *yesterday*. Because sales.
* A significant installed-base leading to overriding concern for backwards compatibility.
* Never enough time, concentration, or caffeine.
* Being seen as a cost center, not a profit center, despite literally making the goods to be sold.
* Scott Adams using your organization as inspiration for the next Dilbert anthology.
* Also, unit tests.

*With any luck, you'll be slightly better off.*

## What the heck is really going on here?

Project Controls people will tell you that *any job whatsoever* has (at least) ten things, at least implicitly:

* required scope (of services, facilities, deliverables, etc. to be completed on behalf of the client.)
* the context (into which new scope must integrate: systems, facilities, market conditions, places, etc.)
* the estimate (calculated based on the scope and progressively refined as details are filled in.)
* the budget (of money, labor, materials, supplies, equipment: what the client is willing to fund.)
* the schedule (when things *might* be done, and when they *must* be done for various benefits to acrue.)
* the plan (to varying degrees of detail, for each aspect of the scope.)
* the forecast (incorporating actual results to-date and a reasonable strategy for making projections.)
* applicable codes and standards: what absolutely must be true of the project *at all times* without fail.
* contingency plans (allocating actions and responsibilities in the face of every imaginable hazard.)
* some sort of working relationship between client and supplier, such as a prime contract spelling out all of the above.

**If any of those get out of control, the project is at serious risk.**

In a big engineering company with a focus on doing major projects, there's a certain fraction of effort devoted to understanding and tracking all those project-controls bits. That's because any time the project gets out of parameters, someone needs to figure out how to adjust performance and expectations in a timely manner. (That someone is typically called a "project manager" but I digress.) If these adjustments are not made, troubles can quickly magnify.

Furthermore, any time either the real world or the client imposes a nontrivial deviation from any measure of the current forecast, it means various documents are fated to be updated and various people will be informed.

These are meant to keep the task force working productively and efficiently toward the best current understanding of the requirements.

But in many of the *agile software development* efforts my brother and I have seen, there's a certain something lost to the process. Most of the project-controls items are considered informally if at all. And as such, even though coders may be knocking out stories left and right, there's still a danger of getting lost in organizational troubles.

## What's my prescription?

The key idea is to have a record of both *where we are* and *how we got here* for each of the ten control items on the list above. Some will be fine with a few cursory notes. Others could benefit from an expository essay or even a tree-stuctured codified and versioned document, depending on how complex the topics are and your tolerance for different risks.

What risks? *What risks indeed!* Consider the kinds of things that could possibly happen. If something has happened before, it's a good indication it might happen again. You'll bring new people into your project if it's at all successful, and these new people will need to learn the ropes. And you'll probably have some turn-over just because. Perhaps some sort of disaster befalls your primary data center. Perhaps there's a drill.

Be creative and think up reasonable scenarios. Think through how you'd like handle them if perfectly prepared. And then think what preparation you'd need. Jot this down; it will inform your next step.

Now, since you don't have infinite time, you need to prioritize your preparation. You're basically doing risk management in this phase. 

*Inaction is always more expedient until catastrophe strikes. Winter is coming.*

## An ideal world?

Gee, it might be nice to have tool support for the requirements capture and tracking alluded to above, and a culture with systemic impetus to apply the tool to its fullest.

I'm not quite sure what such a tool would look like. Perhaps a word processor?

