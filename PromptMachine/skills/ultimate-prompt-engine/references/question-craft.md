# Question craft

Load once, before the first round. `SKILL.md` lists these rules as a checklist; this
file explains them with examples. A question that fails any rule is a bad question.

---

## The rules, explained

**Plain language first.** A first-year student with no software background must
understand every question on one read. Use a named person and a concrete moment
(*"Amit installs the app later..."*) instead of a category (*"identity
reconciliation"*). Technical words may appear only inside an option's description, and
only with an anchor. If the user asks you to rephrase, the question failed this rule:
rephrase every remaining question in that batch, not just the one.

**Every question carries its stakes.** Not *"What database?"* but *"Postgres or SQLite?
This decides whether two people can edit the same split at the same time, and switching
later means rewriting every query."* The user should finish reading the question knowing
something they did not know before.

**Every option is anchored to something real.** Not *"glassmorphism"* but
*"glassmorphism, the frosted translucent panels Apple uses in Control Centre and
visionOS"*. Not *"optimistic UI"* but *"the action looks done instantly, like liking a
post on Instagram, and quietly rolls back if the server rejects it"*. Pull from
`anchors.md`; add to it when you coin a good one.

**Every question offers a recommended default.** Put it first and suffix the label with
`(Recommended)`. Staying silent is not neutrality; it is abdication. Watch for a streak:
if the user accepts every recommendation for two rounds, check that they are choosing,
not deferring, by making the next round's stakes especially explicit.

**Taste questions accept references.** For anything about looks, feel or voice, one
option is always "Show me instead": the user uploads screenshots or pastes links, and
you extract palette, shapes, density and mood, play it back, and confirm. Full procedure
in `dimensions/experience.md`. Fixed menus alone make every project look generic.

**Freeform answers outrank your options.** When the user answers with their own idea,
treat it as the real design: restate it in one line, then run it through every Phase 3
check. Their idea usually opens more follow-up questions than your options would have.
(In the first dry run, a freeform answer invented a seven-level rank system and opened
four new questions.)

**Every question offers "Decide for me".** Always. When chosen: pick, log it as
`ASSUMED` with reasoning and a reversibility rating, and move on without discussion.

**Ask about the non-obvious.** The user already knows they need login. They have not
thought about what happens when someone leaves mid-settlement, what the first screen
shows with no data, or who pays when the free tier fills up. Mine the dimension packs
and the "unasked questions" list in `antipatterns.md` for exactly these.

**Suggest features sparingly.** At most one per round, framed with its cost: *"Worth
adding X? It costs roughly Y and solves Z. In or out for v1?"*

---

## Phase 0: checking the read-back

Do not ask "which of my assumptions are wrong?" as a checklist; it reads like a form and
users bounce off it. Turn the riskiest assumptions into small scenarios:

> Rahul owes you ₹200 and pays you back. How does that happen?
> a) He pays on GPay, then someone taps "settled"
> b) He pays inside the app
> c) The app opens GPay for him with the amount filled in

Ask the depth-mode question in the same batch.

---

## Asking mechanics

Prefer the richest mechanism the harness offers.

**Interactive question tool available** (Claude Code, Cowork, anything exposing
`AskUserQuestion`): use it. It allows 4 questions per call and 4 options per question,
and adds "Other" for free text automatically. So each question gets **at most 3 real
options plus "Decide for me"** (or "Show me instead" for taste questions, with "Decide
for me" as the fourth). Stakes go in the question text; anchors go in each option's
description; keep headers to 12 characters.

**No question tool** (plain chat, Cursor, Codex, a web UI): emit one compact block the
user answers in a single message:

```
**Q1. <question with its stakes>**
  a) <option>: <anchor>  (recommended)
  b) <option>: <anchor>
  c) <option>: <anchor>
  d) Decide for me

Reply like: 1a 2c 3d 4b, or write freely.
```

Either way: **at most 4 questions visible at once**, no walls of text, no restating
what they just told you. Terse is respectful.

---

## Reporting a review (Phase 3)

Three short blocks at most, in plain words, before the next questions:

- **Clash found:** the two answers and why they fight, concretely.
- **New questions opened:** one line listing them.
- **Closed:** what just became irrelevant.

Then the meter, then the questions. Never narrate your reasoning process.
