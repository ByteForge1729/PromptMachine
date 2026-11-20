# Question craft

Load once, before the first round. `SKILL.md` lists these rules as a checklist; this
file explains them with examples. A question that fails any rule is a bad question.

---

## The rules, explained

**Plain language first.** Write for someone thinking out loud who has never built
software. They must understand every question on one read. Use a named person and a
concrete moment (*"Amit installs the app later..."*) instead of a category (*"identity
reconciliation"*). Describe the thing, do not name it: *"a 3D scene that turns as you
scroll"*, not *"a scroll-driven WebGL camera"*. A technical word may appear only inside
an option, and only with its everyday explanation from `anchors.md`. The technical
detail goes in the spec. If the user asks you to rephrase, the question failed this rule:
rephrase every remaining question in that batch, not just the one.

**One idea per question.** *"How should it look and move?"* is two questions and gets
half an answer. If the word "and" joins two decisions, split them.

**Feel and why before how.** Ask what it should be like before anything that narrows it.
The one-minute feeling (E19) comes before colours; what a player's hit should feel like
(GA14) comes before the list of effects; what should click (SM1) comes before the list
of sliders. A "how" question asked first quietly answers the "why" for them.

**Never narrow early.** A taste question (feel, look, movement, sound, voice) gets at
least four directions that are different from each other, not four shades of one, and
no recommendation. Putting your favourite first on a taste question is choosing for
them. Vary the anchors by project; the same four examples every time produce the same
four products.

**Every question carries its stakes.** Not *"What database?"* but *"Postgres or SQLite?
This decides whether two people can edit the same split at the same time, and switching
later means rewriting every query."* The user should finish reading the question knowing
something they did not know before.

**Every option is anchored to something real.** Not *"glassmorphism"* but
*"glassmorphism, the frosted translucent panels Apple uses in Control Centre and
visionOS"*. Not *"optimistic UI"* but *"the action looks done instantly, like liking a
post on Instagram, and quietly rolls back if the server rejects it"*. Pull from
`anchors.md`; add to it when you coin a good one.

**Every non-taste question offers a recommended default.** Put it first and suffix the
label with `(Recommended)`. On questions with a better and a worse answer, staying
silent is not neutrality; it is abdication. Watch for a streak: if the user accepts
every recommendation for two rounds, check that they are choosing, not deferring, by
making the next round's stakes especially explicit.

**Taste questions accept references.** For anything about looks, feel or voice, one
option is always "Show me instead": the user uploads screenshots or pastes links, and
you extract palette, shapes, density and mood, play it back, and confirm. Full procedure
in `dimensions/experience.md`. Fixed menus alone make every project look generic.

**Freeform answers outrank your options.** When the user answers with their own idea,
treat it as the real design: restate it in one line, then run it through every Phase 3
check. Their idea usually opens more follow-up questions than your options would have.
(In the first dry run, a freeform answer invented a seven-level rank system and opened
four new questions.)

**Every question offers "Something else" and "Not sure, suggest one".** Always.
"Something else" is their own answer in their own words. On "Not sure, suggest one": say
what you would pick and why in one line, log it as `ASSUMED` with a reversibility
rating, and move on. They can object; do not ask them to confirm. For a taste question,
suggest from what they have already said about the feeling, never from what is common.

**Ask about the non-obvious.** The user already knows they need login. They have not
thought about what happens when someone leaves mid-settlement, what the first screen
shows with no data, or who pays when the free tier fills up. Mine the dimension packs
and the "unasked questions" list in `antipatterns.md` for exactly these.

**Suggest features in one place.** Not inside ordinary rounds. The delight step
(`delight.md`) proposes 2 to 4 ideas once, each with its reason and rough cost, and the
user takes or leaves each one.

**Order by tag.** `[must-ask]` before `[should-ask]` before `[nice-to-have]`. The tags
are not levels of thoroughness and nothing is locked behind them; they only decide what
is asked while the user still has patience. A question an answer opens goes into the
queue at its own tag. When the user says "enough", stop in the middle of a round if
need be.

---

## Phase 0: checking the read-back

Do not ask "which of my assumptions are wrong?" as a checklist; it reads like a form and
users bounce off it. Turn the riskiest assumptions into small scenarios:

> Rahul owes you ₹200 and pays you back. How does that happen?
>
> - a) He pays on GPay, then someone taps "settled"
> - b) He pays inside the app
> - c) The app opens GPay for him with the amount filled in

Offer the brainstorm in the same batch, once.

---

## Asking mechanics

Prefer the richest mechanism the harness offers.

**Interactive question tool available** (Claude Code, Cowork, anything exposing
`AskUserQuestion`): use it for non-taste questions. It allows 4 questions per call and 4
options per question, and adds "Other" for free text automatically, which is "Something
else". So each question gets **at most 3 real options plus "Not sure, suggest one"**.
Stakes go in the question text; anchors go in each option's description; keep headers to
12 characters.

**Taste questions, and any harness with no question tool** (plain chat, Cursor, Codex, a
web UI): emit one compact block the user answers in a single message. The tool's four
slots would leave a taste question two real options, and two is already a narrowing.

```
**Q1. <the question>**
<its stakes, in one or two sentences>

- a) **<option> (recommended)**. <anchor>   ← recommended: non-taste questions only
- b) **<option>**. <anchor>
- c) **<option>**. <anchor>
- d) **<option>**. <anchor>
- e) Show me instead: send pictures or links   ← taste questions only
- f) Something else
- g) Not sure, suggest one

Reply like: 1a 2c 3g 4b, or write freely.
```

**Layout is part of the question.** The question in bold on its own line, the stakes on
the next, a blank line, then **every option as its own markdown bullet** (`- a) ...`).
Never run options together in a sentence or on plain lines: chat apps join plain lines
into one paragraph, and a paragraph of options is hard to read. The same goes for any
other list inside a question (yes/no items, extras to accept or skip): one bullet each,
never a `·`-separated line. A blank line between questions.

Either way: **at most 4 questions visible at once**, no walls of text, no restating
what they just told you. Terse is respectful.

---

## Reporting a review (Phase 3)

Three short blocks at most, in plain words, before the next questions:

- **Clash found:** the two answers and why they fight, concretely.
- **New questions opened:** one line listing them.
- **Closed:** what just became irrelevant.

Then the meter, then the questions. Never narrate your reasoning process.
