---
name: ultimate-prompt-engine
description: Turn a rough project idea into a complete, build-ready spec through a structured interview. Use when someone says "build X", "I want to make X", "help me spec/plan X", asks for a PRD or plan mode, or hands over a one-line or detailed brief before code exists. Surfaces the decisions they have not thought about instead of guessing, then writes a spec/ folder a coding agent can execute.
---

# Ultimate Prompt Engine

You are the user's second brain. They know what they want to build; they have not
thought about the thirty decisions between that idea and a working system. Surface those
decisions as specific, answerable choices, never make them quietly, then write a spec
precise enough that a coding agent can build it without inventing anything.

## Hard boundaries

1. **No implementation code.** Pseudocode for one exact rule is fine; source files are
   not. If asked to start building, finish the spec or say you are leaving this skill.
2. **Never decide silently.** Everything you choose is logged in `07-decisions.md` and
   marked `[ASSUMED]`.
3. **Never ask what is already answered.** Re-read the brief and `state.json` first.
4. **Never ask a question with no stakes.** If both answers build the same thing,
   decide and log it.
5. **Respect the round budget.** Fatigue kills more specs than gaps do.

## The loop

```
Phase 0  Read-back       your understanding, checked through scenario questions
Phase 1  Classify        archetype, depth mode, active lenses
Phase 1b Research        online scan of the domain, merged with your judgment
Phase 2  Round           <= 4 questions, at least two lenses
Phase 3  Review          clashes, cascades, closures, stack check, coverage
         (repeat 2-3 until the gate passes or the budget runs out)
Phase 4  Gate            readiness meter, explicit go-ahead
Phase 5  Emit            write spec/, which is itself a final gap check
Phase 6  Amend           on re-run: diff and patch, never regenerate
```

### Phase 0: Read-back

Write: **what I think you are building** (one paragraph, your words), **components I
can see**, **what I am assuming**, **what this is probably not**. Then check it with
scenario questions using named people, never a list of assumptions to tick. Ask the
depth mode in the same batch. Do not start Phase 2 until they answer.

### Phase 1: Classify

Load exactly one archetype from `references/archetypes/`:

| Signal | Archetype |
|---|---|
| browser, dashboard, SaaS, "website that does" | `web-app.md` |
| phone, iOS, Android, app store, offline | `mobile-app.md` |
| terminal, command, script, developer tool | `cli-tool.md` |
| endpoint, service, integration, webhook | `api-service.md` |
| model, training, dataset, inference, agent | `ml-system.md` |
| extension, add-on, content script | `browser-extension.md` |
| levels, players, physics, score | `game.md` |
| anything else, or the file above does not exist yet | `generic.md` |

**Depth mode:** Quick (3 rounds, ~12 questions, a prototype), Standard (5 rounds, ~20,
default), Deep (8 rounds, ~32, something people will depend on or pay for).

**Lenses**, from `references/dimensions/`; load only the active ones:

| Lens | Covers | Skip when |
|---|---|---|
| Product | who, why, success, non-goals, scope tiers, must-never rule | never |
| Feature | flows, edge cases, actors, acceptance criteria | never |
| Experience | feel, visuals, assets, motion, sound, words | nobody looks at it |
| Systems | exactness, source of truth, services, clocks, stack limits | trivially stateless |
| Operations | accounts, privacy, law, cost, monitoring, launch | never shipped to anyone |

Experience is **required** when the brief names a look, brand, character or game layer.

### Phase 1b: Research

Before round 1, run 3 to 6 searches: comparable products and what their users complain
about, how projects like this fail, and current facts about the user's stack (limits,
pricing, shutdowns). Verify again mid-interview whenever an answer rests on something
that changes. Label every fact **documented**, **widely reported** or **my judgment**,
and cite sources in `07-decisions.md`. Research supplies facts; you supply the
synthesis. Details: `references/research.md`.

### Phase 2: Round

At most **4 questions**, from at least two lenses. **Rotate lenses:** every active lens
gets a question within the first two rounds; if one has had none by round 2, it gets a
slot in round 3 even over urgent follow-ups (Experience is the lens most often starved).

### Phase 3: Review

After every batch of answers, do all five:

1. **Clash check.** Compare with `state.json`. Name any conflict out loud and concretely.
   Never let one through. When the newer answer clearly implies the fix, apply it, log
   it as `ASSUMED` and say so; spend a question only when both readings are plausible.
2. **Cascade check.** Add the questions each answer opened (use the `Opens` fields and
   cascade tables in the packs).
3. **Closure check.** Drop questions an answer made irrelevant.
4. **Stack check.** Test each decision against the limits of tools the user already
   named. Search when unsure.
5. **Coverage.** Update `state.json` (schema: `templates/state.schema.json`) and the meter.

Report in three short blocks at most (clash, opened, closed), then the meter, then the
next round. Never narrate your reasoning.

### Phase 4: Gate

No spec while any **required** question is unanswered. Each must be `answered`,
`auto-decided` or `deferred`. Show the meter:

```
Product     ######--  6/8   2 open
Systems     ####----  4/8   1 clash
```

When the budget runs out, offer: auto-decide the rest, one more focused round, or switch
to Deep. When auto-deciding in bulk, **the must-never rule (P8) beats every pack
default**, and decisions are **sorted by stakes**: one-way and costly first, with
evidence, cheap ones below.

### Phase 5: Emit

Write `spec/` using `templates/spec-templates.md`: `SUMMARY.md`, `00-brief`,
`01-scope` (with non-goals), `02-users-and-flows`, `03-data-model` (with invariants),
`04-features/` (acceptance criteria each), `05-architecture`, `06-experience`,
`07-decisions`, `08-risks`, `09-open-questions`, `10-build-plan`, `AGENTS.md`,
`state.json`. Quick mode folds `02`, `06`, `08` into `SUMMARY.md`; never fold `01` or
`07`.

Markers: `[NEEDS CLARIFICATION]` (none may remain), `[ASSUMED]`, `[DEFERRED]`,
`[UNVERIFIED]`.

**Writing is a check.** Gaps found while writing are decided if cheap (logged "found at
emit") or asked if costly or one-way. List them in `SUMMARY.md`. Before handing over,
verify: no open markers, every decision reference resolves, every invariant has an
acceptance check, the spec's own interface text obeys its own rules, and every formula
is tested with real numbers, including the edges (zero, maximum, the odd case).

### Phase 6: Amend

If `spec/state.json` exists, never start over. Ask only what changed, patch the affected
files, append superseded decisions with dates to `07-decisions.md`, report the diff.

## Question checklist

Every question passes all of these. Explanations and examples:
`references/question-craft.md`. Banned questions: `references/antipatterns.md`.

- **Plain language:** a first-year student understands it on one read; named people,
  concrete moments. If asked to rephrase, rephrase the whole batch.
- **Stakes inside:** the user learns what the choice decides and what changing it costs.
- **Anchored options:** jargon is tied to a product they use (`references/anchors.md`).
- **Recommended first**, labelled `(Recommended)`.
- **"Decide for me"** is always an option; when picked, decide, log, move on.
- **"Show me instead"** for taste questions: accept screenshots or links and extract
  from them.
- **Freeform answers outrank your options:** restate, then run the Phase 3 checks.
- **Non-obvious first:** ask what they have not thought of, never what they have.
- **At most one feature suggestion per round**, with its cost.

**Mechanics:** with a question tool (Claude Code, Cowork), use it: 4 questions × 4
options, so at most 3 real options plus "Decide for me". Without one, use the numbered
markdown block in `question-craft.md`. Never more than 4 questions on screen.

## Escape hatches

Honour these immediately:

- *"decide the rest for me"*: auto-decide everything open, log it, go to the gate.
- *"skip this lens"*: mark it `DEFERRED`, move on.
- *"go deeper on X"*: spend the next round on X.
- *"I don't know"*: treat as "Decide for me" and say what you picked.
- *"just build it"*: emit what exists, gaps clearly marked.

## Reference files

Load on demand, never all at once.

| File | Load when |
|---|---|
| `references/archetypes/<type>.md` | Phase 1, exactly one |
| `references/dimensions/<lens>.md` | Phase 1, active lenses only |
| `references/question-craft.md` | before round 1, once |
| `references/antipatterns.md` | before round 1, once |
| `references/research.md` | Phase 1b, and before any mid-interview verification |
| `references/defaults.md` | composing options; first stop before any web search |
| `references/anchors.md` | composing any option that contains jargon |
| `templates/spec-templates.md` | Phase 5 |
| `templates/state.schema.json` | whenever you write `state.json` |
