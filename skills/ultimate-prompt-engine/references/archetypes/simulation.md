# Archetype: simulation

Load when the product is a model people watch or play with: a physics or maths
simulation, a "play with the numbers" page, a data picture that responds, a system
that runs on its own rules.

Read alongside the Experience lens, which is always active here.

**The governing rule of this archetype:** a simulation is only worth building if
someone comes away understanding something they did not before. A box of sliders is not
that. Most people will change one thing, or nothing, and leave, so what it shows before
anyone touches it matters more than everything it can do.

Question IDs use the prefix `SM`.

---

### SM1: what clicks `[must-ask]`
**Ask:** After five minutes with this, what should someone understand, or be able to do,
that they could not before? Not the topic, the realisation. "Pendulums" is a topic.
"A tiny change at the start becomes a huge difference later" is a realisation, and the
whole thing gets built to make that one visible.
**Options:** free text. Offer your read of it first and let them correct it.
**Opens:** SM2, SM3, what gets left out (P4), E19

### SM2: who is driving `[must-ask]`
**Ask:** Is the person led through it step by step, left free to play, or led first and
then set free? Left free with no guidance, most people poke twice and leave. Leading
them takes writing, and that writing is part of the build.
**Options:** led first, then free play (recommended) / led all the way, like a story /
free play only / something else
**Opens:** the words around it (SM13), the steps, what unlocks when
**Evidence:** guided structure over a bare sandbox (documented: Victor, "Explorable
Explanations"; Case, "Explorable Explanations").

### SM3: before anyone touches it `[must-ask]`
**Ask:** What is it doing the moment it opens? Many people never touch anything, so
this is all they will see.
**Options:** already moving, from a starting point chosen to be interesting
(recommended) / still, waiting for the person / it plays a short demonstration, then
hands over
**Opens:** the starting values (each one is a decision), the reset button, movement
switched off

### SM4: what people can change `[must-ask]`
**Ask:** Which things can someone change? Name them all. Each one is something to
build, explain and keep from breaking the picture, and three well-chosen ones teach more
than fifteen.
**Options:** propose the list from SM1, marked "needed for the realisation" and "extra",
and let them move items between the two
**Opens:** SM5, limits for each (smallest, largest, what happens at the edges), SM7

### SM5: how they change it `[should-ask]`
**Ask:** How does someone change those things?
**Options:** grab the thing itself and move it, like pulling the pendulum by hand /
sliders beside the picture / numbers inside a sentence that you drag / typing exact
values / something else / not sure, suggest one
**Opens:** touch behaviour (SM11), keyboard path, E24

### SM6: must it be right, or look right `[must-ask]`
**Ask:** Will anyone rely on the numbers, for homework, a decision or a published
figure, or does it only need to behave believably? Right means checking it against known
answers and sometimes running slower. Looks right is quicker to build and must say so on
the page.
**Options:** it must be right, and say how exact it is / believable is enough, and the
page says it is an illustration / decide for each number
**Opens:** S1 exactness, the calculation rules in 03-data-model.md, acceptance checks
with known answers, P8

### SM7: time `[should-ask]`
**Ask:** What can someone do with time: pause, slow down, step forward one tick, drag
backwards? Going backwards means it has to remember what happened, which uses memory
and takes a few days to build.
**Options:** play and pause only / play, pause, speed and single steps (recommended) /
all of that plus dragging backwards
**Opens:** how much history is kept, the time bar, SM10

### SM8: how much at once `[should-ask]`
**Ask:** How many things are on screen at the busiest moment: ten, a thousand, a
hundred thousand? That number, on the weakest phone you care about, decides how it has
to be drawn.
**Options:** tens (anything works) / thousands (needs care) / as many as possible (the
count adapts to the device)
**Opens:** drawing method in 05-architecture.md, E23, the weakest device named

### SM9: seeing it more than one way `[should-ask]`
**Ask:** Should the same thing show in more than one form at once, such as the moving
picture next to a graph of it, with a point on one lighting up on the other? Seeing both
is often where the understanding happens; it is also a second thing to build.
**Options:** the picture only / picture and a live graph, linked (recommended when SM1
is about a relationship) / picture, graph and the numbers
**Opens:** layout on a phone (they will not fit side by side), E6

### SM10: keeping and sending a moment `[should-ask]`
**Ask:** When someone finds an interesting setup, can they keep it or send it to
someone? A link that reopens exactly this setup needs no accounts and makes it useful
for teaching.
**Options:** a link that reopens this exact setup (recommended) / save a picture / both
/ nothing
**Opens:** what counts as "the setup" (every changeable thing in SM4, and the random
start), S10 link safety

### SM11: fingers `[should-ask, when it will be used on phones]`
**Ask:** On a phone a finger covers the thing it is moving, and dragging inside the
picture fights with scrolling the page. Is the phone a full way to use this, or a place
to watch it?
**Options:** full use on a phone, controls placed below the picture (recommended) /
watch on a phone, play on a laptop / laptop only, and say so
**Opens:** control layout, touch target sizes, W2

### SM12: where real data comes from `[must-ask, when it shows real-world data]`
**Ask:** Where do the real numbers come from, how old may they be, and are you allowed
to show them? A beautiful picture of wrong or borrowed data is worse than none.
**Options:** a named public source, with its date shown (recommended) / my own data /
made-up data, labelled as made up
**Opens:** S4 outside services, licences, the "last updated" label

### SM13: the words around it `[nice-to-have]`
**Ask:** Is there writing beside it that explains what is going on, or does it stand
alone? If there is writing, who writes it?
**Options:** short guiding lines only / a full written explanation with the simulation
inside it / none
**Opens:** E17 voice, content effort, SM2

---

## Defaults for this archetype

Assume these, log as `ASSUMED`, do not spend questions on them:

- The same setup always gives the same result, including anything random (the random
  start is stored with the setup).
- A reset button returns to the opening state.
- It pauses when the tab or app is not in view.
- Every number shown has a unit.
- Changing a control never makes the picture jump or flicker.
- Touch targets are larger than the thing drawn.
- With movement switched off on the device, it opens paused with a clear play button.
- Every control also works from the keyboard, using ordinary controls where they exist.
- It can be understood from the opening view alone.

## Cascade rules

| If the answer is | Add these |
|---|---|
| it must be right | S1, known-answer checks in the acceptance criteria, stated accuracy |
| believable is enough | an "illustration, not a calculation" line on the page |
| dragging time backwards | history length, memory limit, SM10 |
| thousands of things or more | SM8 drawing method, E23, the weakest device named |
| a link that reopens a setup | the full list of what a setup contains, S10 |
| led step by step | SM13 writing, who writes it, the steps in 02-users-and-flows.md |
| real-world data | SM12, S4, what shows when the source is down |
| used in a classroom | works on a projector, works with no accounts, O4 minors |
