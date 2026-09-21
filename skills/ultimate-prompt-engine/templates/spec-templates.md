# Spec templates

Load in Phase 5 only. One section per output file. Instructions live in `<!-- -->`
comments; delete them in the emitted file.

## Rules for every file

- **Every line must be something a build agent could get wrong.** That is what makes it
  checkable. Delete adjectives that specify nothing ("beautiful", "intuitive", "robust").
- **Keep WHAT and HOW apart.** `01` to `04` and `06` describe behaviour and rules.
  Technology names belong in `05` and `10` only. (Borrowed from spec-kit.)
- **Trace everything.** Every requirement cites the decision it came from: `(D7)` for a
  user decision, `(A12)` for an assumed one. A requirement with no source is invented;
  either find its decision or add it to `07` as ASSUMED.
- **Markers:** `[NEEDS CLARIFICATION]` may not appear in an emitted spec. `[ASSUMED]`,
  `[DEFERRED]` and `[UNVERIFIED]` may, and each must also appear in `07` or `09`.
- **Pseudocode is allowed only for rules that must be exact** (a calculation, a state
  machine, a threshold table). Never source code.
- **Numbers carry units.** "₹500", "3 days", "under 10 seconds". Never "fast" or "soon".
- **Collapse for Quick mode:** fold `02`, `06`, `08` into `SUMMARY.md`. Never fold `01`
  or `07`.

## Emit is a check, not a printout

Writing the spec exposes gaps the interview missed: a state nobody defined, a person who
cannot perform a step, a number nobody chose. When you find one:

- cheap or reversible: decide it, log it in `07` as ASSUMED with reason **"found at
  emit"**;
- costly or one-way: stop and ask before finishing the spec.

List every "found at emit" item in `SUMMARY.md` so the user sees what the interview missed.

---

## SUMMARY.md

```markdown
# <Project>: spec

<!-- One screen. Someone reading only this file should know what is being built,
     for whom, what v0 contains, and what must never happen. -->

**What:** <one sentence>
**For:** <who, in the moment they open it>
**v0 contains:** <comma list>
**Not building:** <non-goals, comma list>
**Must never happen:** <the P8 rule>

## Readiness
<meter from Phase 4, final state>
Decisions: <n> yours · <n> assumed · <n> deferred

## Review these first
<!-- the one-way and costly ASSUMED decisions, one line each, linking 07 -->

## Found while writing the spec
<!-- gaps the interview missed, each with its A-number -->

## Files
<!-- one line per file: link + what it answers -->
```

## 00-brief.md

```markdown
# Brief

## Original idea, verbatim
<the user's words, unedited>

## Read-back, as corrected
<Phase 0 read-back after the user's corrections>

## Project principles
<!-- non-negotiables the user set; P8 first -->
```

## 01-scope.md

```markdown
# Scope

## v0: <what one person can finish and put in front of real users>
| Feature | Why it is in v0 | Source |

## v1
| Feature | Trigger to start it | Source |

## Later
<bullets>

## Non-goals
<!-- things this will deliberately never do, each with a one-line reason. Never empty. -->

## Success
<the P5 number, with a date>
```

## 02-users-and-flows.md

```markdown
# Users and flows

## Who
<!-- the person in the moment (P1), not a demographic -->

## Flows
### <Flow name>
<!-- numbered steps: actor, action, what the system does. Include the failure branch
     for every step that can fail. Name the people ("Rahul", "Priya"). -->
```

## 03-data-model.md

```markdown
# Data model

## Entities
### <Entity>
| Field | Type | Rule |
<!-- Types are conceptual (text, integer, timestamp, enum), not database-specific.
     Money is always an integer in minor units. IDs are UUIDs. Timestamps are UTC. -->
**Owned by:** <who may create, edit, delete>
**Lifecycle:** <states, and what moves it between them>

## Invariants
<!-- statements that must be true at all times; these become tests. -->

## Derived values
<!-- anything computed rather than stored, with exact pseudocode -->
```

## 04-features/<feature>.md

One file per feature.

```markdown
# <Feature>

**Tier:** v0 | v1 · **Sources:** <D/A numbers>

## Behaviour
<numbered rules>

## States
<!-- empty, loading, error, offline, success, each one defined -->

## Edge cases
<!-- from the Feature lens: undo, leaving, simultaneous edits, abuse -->

## Acceptance criteria
<!-- checks a person could run on a real phone. Given / when / then. -->
- [ ] Given ..., when ..., then ...
```

## 05-architecture.md

```markdown
# Architecture

## Stack
| Layer | Choice | Why | Source |

## Boundaries
<!-- what runs on the phone, what runs on the server, and why each thing lives
     where it does. Anything touching the P8 rule lives on the server. -->

## Integrations
| Service | Used for | Failure behaviour |

## Scale posture
<!-- designed-for number (P6 × 10); what breaks first beyond it -->

## Cost
<!-- free-tier limits hit first, and at what usage -->
```

## 06-experience.md

```markdown
# Experience

## Feel
<!-- E1 answer; if references were given, the moodboard: each reference, what was
     taken from it, extracted palette with hex values -->

## Screens
| Screen | Shows | Primary action | Empty state |

## Characters / game layer
<!-- tiers, what drives them, states per tier -->

## Asset delivery spec
| File name | What | Format | Size | Background | Variants | Layers | Source | Status |

## Motion, sound, haptics

## Voice
<!-- three sample lines in the chosen voice, including one hard message -->

## Accessibility
```

## 07-decisions.md

```markdown
# Decisions

## Yours
| # | Decision | Round |

## Assumed: review first
| # | Decision | Why | Reversibility | Evidence |

## Assumed: the rest
| # | Decision | Why | Reversibility |

## Superseded
| # | Was | Replaced by | Date |
```

## 08-risks.md

```markdown
# Risks

| Risk | Likelihood | Damage | Mitigation | Status |
<!-- Include warnings the user waved off, marked "accepted by user". -->
```

## 09-open-questions.md

```markdown
# Open questions

| Question | Status (DEFERRED / UNVERIFIED) | Revisit when | Owner |
```

## 10-build-plan.md

```markdown
# Build plan

<!-- Ordered milestones. Each is shippable to a phone, in order, with no milestone
     depending on a later one. -->

## M<n>: <name>
**Delivers:** <features>
**Depends on:** <milestones>
**Done when:** <acceptance criteria references>
```

## AGENTS.md

```markdown
# Instructions for the build agent

You are building <project> from the spec in this folder. The spec is the source of truth.

## Never
- <P8 rule, restated as an instruction>
- Relitigate a decision in 07-decisions.md. If one looks wrong, stop and ask.
- Build anything listed under Non-goals in 01-scope.md.
- Build v1 or Later items during v0.

## Always
- Stop and ask when you meet a [NEEDS CLARIFICATION] or a behaviour the spec does not
  cover. Do not invent it.
- Treat every item in 03-data-model.md "Invariants" as a test that must exist.
- Build milestones in the order of 10-build-plan.md.
- Cite the spec file and decision number in commit messages for behaviour changes.

## Principles
<!-- copied from 00-brief.md -->
```
