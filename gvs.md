# Graph Versioning System
This brief paper explores the ideas and issues surrounding a version-control
system applied to graphs (in the computer science / graph-theory sense)
and graph-like documents.

## Quick refresher: Foundations

A graph is a structure consisting of nodes/vertices and edges/arcs between them.
Often the edges have a sense of direction. Usually the nodes and/or edges have
additional associated data (often called 'label' or 'color') either with respect
to some particular graph-algorithm or as an application-specific annotation.

You can have all sorts of complex variations on the general idea, including:
* Different sets of arcs for different semantic purposes.
* Arc-like things where more than two nodes participate (perhaps with defined roles).
* Nodes in different categories, with rules about how categories may connect.

Applications of graph-like structures abound. A few examples include
hypertext systems, technical diagrams, and relational database schemata.

For any given application with graph-like structure, I refer to "the graph" as
the state of that structure in the moment, as viewed by some particular user.

## Graphs are everywhere. Now what?

Typically today, our applications work with a snapshot of the graph, with no
particular concept of the past, or of parallel development efforts. Either
you have the whole banana, or you have nothing.

I'd like to add a layer of indirection.

Rather than editing the graph directly, let us edit a *proposed graph*
which is defined as *the original graph plus the effects of your changes.*
Such a system would have to keep track of the actual changes (and presumably
the functional relationships between them).

In concept, two or more "proposed graphs" could exist at once. The higher-level
application could be switched among them and be none the wiser.

At the application level, you might wish to view the effect of multiple sets of
changes taken together, either in parallel or in sequence. Things get really
interesting when you make the application aware of where in the change history
different portions of the graph are coming from: perhaps you can see them in
different colors.

Change management requires some sort of "commit" and "merge" activities. The
former is presumably straightforward. The latter requires application support
for reconciliation at the semantic, rather than syntactic, level.

Taking this one step more meta: It's often worthwhile to bundle up a group
of change sets under a name, such as "Client Acceptance Test".

## What are the operations?

It's useful to think about this sort of system as a (relatively complex)
abstract data type. I might not get this exactly right the first time around,
but here's what I think we need:

### Create-Application:

One of the more complicated activities is creating the schema for an application.

Let edge-type be defined as a coherent ordered sequence of two (or occasionally more)
roles. These roughly correspond to "foreign key relationships" in the relational model.

Each edge type has a name, and each role has a name.

Let node-type be defined sort of like an entity table in a relational database:
along with identity (primary key), a node of a given type has a consistent set of
attributes and relationships. It's also eligible to play defined roles in edges.

Each node type has a name. Each attribute has a name and a "primitive" type.
Each "primitive" type has a name and perhaps other bits relating to concrete storage.

An application may declare additional constraints, broadly corresponding to the idea of
unique indices in relational systems. A typical example might be that two children of the
same parents ought not have the same name. Along with a formal definition, constraints
should have a severity level (perhaps "curiosity", "warning", "error") and some sort of
plain-language description.

More thought may be necessary.
For instance, hypertext documents seem to have special issues.

### Querying:

It will be necessary or desirable to query the graph in myriad ways. A reasonable query
language will make this much nicer. We'll probably want a plug-in interface. There's
a graph query language standard. It would probably do OK.

### Alteration:

The bit that makes this whole mess interesting is the way alteration behaves, so that
natural change management can apply.

The key idea is to always distinguish between the sign and the signified.
This is not always easy to explain. A rude and politically-charged example may clarify:

* In October of 1968, Columbia Records released the album *Switched-on Bach* under the byline
  *Walter Carlos.* (I have a copy of the original vinyl. It says *Walter*.)

* 24 years later, in 1992, another album *Switched-on Bach 2000* was released with a different
  byline: *Wendy* Carlos.

* Naively one might suppose *Wendy* to be *Walter*'s talented daughter. I certainly made this assumption in 1992.

* Today, wing-nuts everywhere want to tell me how right or wrong this is. Morality is entirely
  beyond the scope of this example. But anyway, there was a surgery and a name-change involved.

* If all you know is a name and not the person behind it, how can you know what the *bleep* is going on?


To understand a change in context, one must distinguish between the oft-conflated acts of:

* changing a node's label/attribute data
* changing some or all of the edges in which one node participates, to point at another node

To that end, the abstract data type for the *historical record* needs a way to say:
* Node X, attribute Y (which had value A) changes to value B.
* The edge of type W between nodes X and Y shall now point between nodes X and Z.
* A given node or edge comes into existence, or departs from the realm unreferenced.

This has one particular implication for hypertext (and by the way, computer code is uber-hyper):
on the inside it should not contain names, but rather references to nodes. Only the presentation
layer can convert those node-references to something legible, and when making an entry one ought
to clarify any ambiguity. On input, the user-interface should provide for automatic inference in
most cases, with a simple dialog to decide among reasonable alternatives. So that means we need a
way to get the possible referents of a sign, perhaps weighted according to topic-hints.


### Create-View:

One is always working in some "proposed graph" which may be understood by analogy to old
celluloid animation techniques: You have a stack of transparent *cels* each with some feature
painted on, and you can move the cells independently of the background (or of each other).

To bring the analogy home, consider that each *cel* specifies a list of changes to apply.
As long as the changes from one *cel* to the next are functionally compatible, one can quite
reasonably stack them. Otherwise, such stacking will require a *merge-resolution* operation.

Thus one makes application-level changes to individual *cels*, but also there is a defined
process for managing, reviewing, combining, and incorporating these proposed-change sets.

Let's say that *cels* have various meta-information, including a symbolic name and possibly
some token for rights management.

### Create-Snapshot / Create-Stack:

From time to time, one may wish to combine the effects of several *cels* into one.
There are two reasonable ways to do this: By copy or by reference. Both have use-cases.
Both should be allowed and supported.

### Release:

A *release* is much like a read-only snapshot that includes the previous release as background.
There is room for a bit more sophistication: Ideally you'd have a true *configuration-management*
process, where specific change-sets can be added or removed consistent with the functional
dependencies between them. But that process only helps you build a *release candidate*.
At some point, you have to draw a line in the sand. Possibly this is about timestamps in a
transactional release system. In fact, you could have many such lines: one for each different concern.

Urgencies may compel you to make last-minute adjustments to the lines-in-the-sand.

# Meta-Circular Considerations

Part-way through reading this, you realize that this model of *cels* and snapshots and so on
define a meta-application which also relies on the very same notion of *strongly-typed graph*.

This inductive tower needs a base case. Actually the base-case isn't too complicated. It's
the "create-application" step up front, along with some UI to drive things.

The inductive case is a bit more difficult. It requires carefully defining the API from
the *graph-as-seen* to the base-level application, so that the fact of version control is
well hidden -- except in those places where the abstraction absolutely must leak. (After
all, deliberate abstraction-leaks into the presentation layer are how you understand the nature
of a *proposed-change* as distinct from the *thing-to-be-changed*.

**Oh by the way**, there's probably some industry-standard set of colors and patterns that
mean things like *add/change/delete* which our applications could adopt.
