# How it works

## The loop

```
Phase 0  Read-back       your idea in its own words, checked through scenario questions
Phase 0b Brainstorm      optional, offered once: many directions, nothing decided
Phase 1  Classify        project type, active lenses
Phase 1b Research        comparable products, failure modes, current platform facts
Phase 2  Round           at most 4 questions, must-ask first, feel before mechanics
Phase 3  Review          clashes, cascades, closures, stack check, coverage
Phase 3b Delight         once: 2 to 4 ideas made for this product, each with a cost
Phase 4  Check-in        what is left; "enough" at any point ends the questions
Phase 5  Write           spec/, then a self-check
Phase 6  Update          patch an existing spec, never regenerate
```

## Why it is built this way

**Progressive loading.** `SKILL.md` holds only the loop and the rules. Question packs load
when the project type and lenses are known, so the model never reads 202 questions to ask
12.

**Feel before mechanics.** A build agent given no point of view picks the most common
typeface, colour and layout it has seen, which is why so much AI-built work looks alike.
So the first experience question is what someone should feel in one minute, with several
different directions and no recommendation, and the spec records the lettering, colours
and movement that follow from the answer. Before handover the spec is checked against a
list of the marks of a default page. A list of things to avoid is not enough on its own:
ban one common typeface and the builder reaches for the next most common.

**A brainstorm, if wanted.** Questions narrow an idea. Offered once, the brainstorm
widens it first: at least eight directions from different angles, some deliberately odd,
nothing decided, then a five-line summary the questions start from.

**Delight, proposed once.** After the main action and the feel are known, the skill
proposes 2 to 4 small features that could only belong to this product, each with a
reason and a rough cost. Anything that could be pasted into another product unchanged
(dark mode, confetti, a streak) is dropped before the user sees it. Declined ideas are
written into the spec so the build agent does not add them.

**Order, not levels.** Every question is tagged must-ask, should-ask or nice-to-have.
The tags only decide what is asked first. There are no modes and no fixed length: the
user says "enough" whenever they like, and whatever was not asked is assumed, logged and
listed at the top of the summary, the hard-to-undo assumptions first.

**Lenses, not topics.** Every project is seen through five fixed lenses: product, feature,
experience, systems, operations. A fixed set stops the model asking random questions and
makes coverage measurable.

**Cascade tables.** Every question lists what its answer opens. "Yes, two people can edit
it" opens conflict handling, history and undo. The review step does not rely on the model
noticing this; the tables say so.

**Clash detection.** Every answer is compared with every earlier one. The dry runs caught
14 clashes this way, several introduced by the user changing their mind mid-interview.

**Honest decisions.** "Not sure, suggest one" is always available, and every decision made for you
lands in `07-decisions.md` with its reason, its evidence and whether it can be undone. The
one-way ones are listed first.

**The must-never rule.** Every project names one thing that must never happen. Any default
that conflicts with it loses. If the rule cannot be guaranteed by software (forecasts are
sometimes wrong), the skill says so and restates it as something the build can promise.

**Writing is a check.** Gaps found while writing the spec are decided and listed ("found at
emit"), or asked about if they are costly. Before handover the skill checks that every
requirement traces to a decision, every invariant has an acceptance test, and every formula
holds on real numbers, including the edge cases.
