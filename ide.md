+ Let's Design an IDE

First of all, let's get the obvious out of the way:

* This is a crazy idea;
* nobody should attempt this;
* there are already plenty of good solutions out there.

Yeah? **SO WHAT?**

Hobby projects were never meant to be profitable.
They're a way to put one's ideas into the world.
Maybe the world ignores that. Maybe not.

++ Anti-Requirements!

Before listing all the things it *should* be,
it's an excellent idea to list off some things I definitely want to *avoid!*

PS: I take full credit for eccentric, wacky ideas.
If I'm going to make a dent, the thing needs to be different.

* No pop-out drawers, trays, etc.
* No heavy reliance on precision mousing.
* No *file-tree + edit-window* look that virtually every IDE has.
* No debugger. Debuggers are for the weak who wish to remain so.
* --- ok ok maybe not *no* debugger, but certainly don't distract me with it. e.g. breakpoints in normal mode! I *said* "select line".
* No icons! Zero of them! I am the iconoclast!
* No funky fonts or styling! It should look like EGA text mode: easy, consistent, good contrast, and large enough to read.
* No tabs! Tabs are another form of oppression.

++ Concepts!

Attention is the foremost value. Attention and focus. Also, nobody expects the Spanish Inquisition. But I digress.

First of all, there are a lot of things for which *order does not matter* (or should not, at any rate).
For example, function definitions in a modern language.
So, let's take these over and say order is *not even a thing* in the IDE.
I mean sure, there is an order to any given sequence,
but for example that order could be 100% always alphabetical.

The point is, that let's say instead the screen is divided into zones of focus and attention.
Say, two or three adjustable columns with various sections.
This is starting to sound like Plan 9's system editor, but work with me.

I do appreciate the Mac theme of menu-bar smack against the top of the monitor.
I figure a windows dev will run the IDE in full-screen mode most of the time,
so we can cheat by putting the menu in the title bar on Windows,
the same way PyCharm does -- except with more cowbell. Er, space. More space.

So now what? Well, let's say any given section can serve any UI role transparently.
So, for instance, if you need to see the set of files in a project,
you hit a function key and *BOOM!* you're looking at the files in whatever section was active.
(i.e. either under the mouse, or last clicked, or whatever -- to be determined.)
This may sound annoying, but consider! Your attention is focused on an activity in a space.
In that space you see what you need to see for the activity at hand.
Other spaces contain the context for other activities, or remain on-screen for reference.
That context is not destroyed by whatever steps you take in the current space.

What about folding? I think it's the wrong model --
or at any rate not the only important way to hide the irrelevant.
Irksome are the parts I can't "fold".
I want to focus in on just one or a few functions,
and the entire rest of a file should just be cleanly out of view,
not some skeletal clutter.

To that end, if I want the skeleton, it's another hotkey. (Probably F2.)
And then I start typing and it's a search that narrows down the view.
Maybe the same intelligent narrowing applies to the file tree.
Get it down to a few options, and I can navigate with the keyboard or mouse.

For that matter, switching attention to another file should NOT close the one I have.
And there's not some damn god-forsaken tab-bar across the top of a section either.
The system knows full-well which files are open or modified; that information
is just another interface view I can quickly get to with another hotkey.
And it's global information too, not tied to any specific area.

By the way! The *escape* hotkey is the hottest one of all.
It means "Oops, I got here by mistake or didn't find what I'm looking for."
Therefore, each section has something like an activity-stack and *escape*
pops that stack -- with one exception: whatever file or function you're
editing in that section is the bottom of the stack.
Selecting a new file or function does replace the stack, but that's OK.
Oh, one nodda ting: Console, VCS, and e-mail count as base-activities too.
Sort of. Consoles in particular are a bit special. They merit separate discussion.

Attention comes in several levels of intensity and meaning. Let's say you open a file.
Now the system knows that file has your attention. But not what for.
Since one view in the system is sort of "what's on my mind",
I should be able to see that list sorted various ways,
such as how recently a file was opened.
And I should be able to pin files into groups based on the reason for my attention to those files.
I'm thinking something SOOOper simple here.
More than just pinned-or-not, and *definitely* not color-coding.
(At least, don't make *me* try to remember what the colors mean.)
So, the point is I should be able to select an entire interest group,
and do other things with group-selection such as close everything unique to the group.

I have this other idea, which I'm calling "agents":
Initially, named and saved groups of searches,
possibly with attached notes and references to specific (parts of) files.
The point is working an issue that takes many separate hack sessions:
you might save brain power not having to reconstruct your thoughts.
Another possible approach would be to be able to save and restore session context.

++ What's this about consoles being special?

Let's say every area/section has a certain amount of durable context,
The first part is which (if any) file is open.
(Search results count as a file in this sense.)
If you have that and you press *escape*, you'll flip back and forth with *something else*.
That *something* will be closely related to whatever else you had in that area.
For example, let's say you're looking at a script and press F5.
(That's the universal "run" command.) The console can run in the same zone,
taking up the *other side of the card* shown in that section.
Press *escape*, and you're looking at the script again. But press it again,
and you're back to the console.

The idea is that each tool/view has an affinity to either *heads*, *tails*, or *stack*.
For instance, the search interface might be *stack*,
while the search results are *tails*. Edit views are again *heads*,
so you can flip back and forth between hits and text by pressing *escape*.

++ Dealing with Sections. Also, Search. And Errors, Too.

Let's say every column has at least one section, with dividers above and below.
You can drag dividers up and down to resize sections. Do this at top or bottom,
and you create a new section in the process.

Drag a divider far enough horizontally, and you can move the corresponding section around.
Double-click to minimize a section down to a single line, or restore a minimal section.
In either of these events, other sections in the affected columns will resize proportionally.

Now let's consider a project-wide search. The hits are in different files.
Perhaps you drag a hit to a section to open that file in that section,
or to a divider to create a new section in the process.
Multi-select drags would open a stack of files in a column.

Oh yes. Now suppose you have multiple hits in the same file. From the get-go,
the *tails* side of that editor will be the set of hits in that file.
Speaking of *tails*, consoles are also *tails* and sometimes consoles contain
error messages with trace-back information. If your language plug-in of choice
can recognize filenames and line-numbers, then *BOOM!* there's a search result.
You should be able to double-click or drag the element just like ordinary search.
(Maybe these appear in a stacked activity? Maybe on F2, just like edit-navigate?)

Click anywhere in a section (or its upper divider) and it becomes active for the focus.
The currently-focused section will be given clear and noticeable prominence through
some combination of visual effects that *includes* the contents of the sections.
For example, we might show non-focused sections in sepia-tone vs the focus in full color.

Oh by the way, it's probably good if the section divider gives an indication of
what's currently shown on *both* heads and tails.
The label corresponding to the current side of the coin will be given noticeable prominence.
Click on either label, and you're shown that side of the coin.
This also closes any stacked activites in that area.

Stacked activities will be obvious what they are, but should probably include a prominent header nonetheless.

++ Language Integration

I'd argue that you get most of your value from a few simple capabilities:

* Some concept of a project.
  This probably means a root folder, some configuration,
  and some durable state such as which files have how much of your attention currently.
* Search within the project.
* Run a script. The console appears as part of the dev UI.
* Search for definitions and uses of identifiers. Smarter is better, but simple is not bad.
  Incidentally, there's something called a *language server*. Look into it.
* Run external tools, sending the output to a console.

Basically all of these concepts have to work by being cards --
same as editor cards as far as the UI is concerned, but with different implementation.

++ Syntax Folding: a Swing and a Miss

*(You might also see it called "code outlining".)*

Rather, the *skeletal identifiers* should be a stack-activity that lets you navigate
to focus an editor view on a specific portion of a file.
I described the general interaction concept earlier.
Fancy features like "recent attention history" are nice, but not essential.

The real reason not to be so worried about syntax-folding per-se is that
the desire to *fold* control-structures and the like comes from a failure to
properly *factor* the code. Move large blocks into sub-functions and be happy.

Now you say you want to look at several parts of the same file at once.
That's fine: open the same file in several view-ports and focus each port
on a different part of the file. To make that easy and discoverable,
let's have an edit-menu option to split the view.
The system needs to keep your changes in sync from one view to the next,
but this is easy enough: recall anyway that the set of open files is
completely separate from the list of edit-views, which simply *refer*
to an open file.

++ Implicit-Save / Checkpointing:

It's a common newbie mistake to edit code, forget to save, and then wonder what's wrong.
Implicit-save is nice from that angle, but it has a down-side, which is that there's no
longer any such thing as a transitory edit that you don't save.

It's probably smart to ask the user during set-up if they prefer one or the other style.
Reasonable people can disagree or change their mind.

Personally, I like the Notepad++ behavior of preserving unsaved changes across sessions.
An IDE enhancement to this would be that if you *run* with un-saved changes,
ask the user if (s)he'd like to save files first before *actually* running the code.
You can discuss refinements to this idea, but anyway I think it's fine.

++ Implementation Options

One idea is to start with an existing editor and hack it. *That's terrible.*
I won't do it. Not for a hobby project.

Another is to start with a cross-platform-platform, such as *electron*.
That's viable, except I'd have to (re)learn Javascript. That's viable too
for other reasons, but does represent a possible hurdle.

The third option is to explore using something like *tkinter*. That takes
care of the platform and language problem, but leaves a *subtractive*
design problem: TK widgets have all sorts of default bindings which are
absolutely fine in many applications, but there's no escape hatch:
if you can't find an easy way to compose existing widgets to do your thing,
you're hooped. In particular, I'm deeply concerned about managing the layout,
keyboard focus, and editor windows. I'm pretty sure it's theoretically
possible, but in practice would be forever beset by weird bugs.

The fourth option is a less-opinionated UI toolkit. For example,
Java Swing lets you write your own layout manager or implement
a custom widget's *draw* method. In concept, this provides the
most power and flexibility, but maybe also least convenience.
Often there are interface-builders available for typical bits.
With absolute power comes absolute responsibility, though.

From a "hobby project" perspective, the goal is not what's soonest,
or easiest, but what's most interesting and educational as well
as providing a reasonable chance of success.

++ Final Notes:

This project seems way less daunting than it probably should.
I don't know if that's good or bad.

It's not the first time I've done something along these lines.
The first was a tcl-editor in tcl/tk, which was dangerously
self-hosting and long-gone. (Incidentally, that's where I
developed the fear of default bindings.)

The interface framework I've described probably has value
in several other kinds of applications. For example, I've
also been meaning to describe a file manager/viewer
obeying similar principles, inspired by *Stereo Shell*.

Like with all projects, generating interst is a neat trick.
