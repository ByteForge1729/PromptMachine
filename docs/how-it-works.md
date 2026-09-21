# How it works

## The loop

```
Phase 0  Read-back       your idea in its own words, checked through scenario questions
Phase 1  Classify        project type, depth, active lenses
Phase 1b Research        comparable products, failure modes, current platform facts
Phase 2  Round           at most 4 questions, from at least two lenses
Phase 3  Review          clashes, cascades, closures, stack check, coverage
Phase 4  Gate            no spec while required questions are open
Phase 5  Write           spec/, then a self-check
Phase 6  Update          patch an existing spec, never regenerate
```

## Why it is built this way

**Progressive loading.** `SKILL.md` holds only the loop and the rules. Question packs load
when the project type and lenses are known, so the model never reads 169 questions to ask
12.

**Lenses, not topics.** Every project is seen through five fixed lenses: product, feature,
experience, systems, operations. A fixed set stops the model asking random questions and
makes coverage measurable.

**Cascade tables.** Every question lists what its answer opens. "Yes, two people can edit
it" opens conflict handling, history and undo. The review step does not rely on the model
noticing this; the tables say so.

**Clash detection.** Every answer is compared with every earlier one. The dry runs caught
14 clashes this way, several introduced by the user changing their mind mid-interview.

**Honest decisions.** "Decide for me" is always available, and every decision made for you
lands in `07-decisions.md` with its reason, its evidence and whether it can be undone. The
one-way ones are listed first.

**The must-never rule.** Every project names one thing that must never happen. Any default
that conflicts with it loses. If the rule cannot be guaranteed by software (forecasts are
sometimes wrong), the skill says so and restates it as something the build can promise.

**Writing is a check.** Gaps found while writing the spec are decided and listed ("found at
emit"), or asked about if they are costly. Before handover the skill checks that every
requirement traces to a decision, every invariant has an acceptance test, and every formula
holds on real numbers, including the edge cases.
