# PromptMachine

**A library of prompts and skills that turn rough ideas into instructions an AI can
actually execute.**

The first skill in the library is **Ultimate Prompt Engine**: plan mode on steroids.
Give it an idea of any size, from one line to a page, and it interviews you like a
senior engineer and a product designer would. It surfaces the decisions you have not
thought about, asks them as plain questions with the stakes spelled out, never decides
silently, and ends with a `spec/` folder a coding agent can build from without inventing
anything.

---

## What an interview looks like

From a real run on a bill-splitting app idea:

> **Amit installs the app later and wants to claim the ghost "Amit" in your group. How does
> the app know it is really him?** If anyone can claim any ghost, someone could claim one to
> wipe a debt or read someone's history.
>
> a) Personal claim link *(recommended)*: someone in the group sends Amit a link made only
>    for that ghost, on WhatsApp
> b) Phone number match
> c) Pick from a list: easiest, but anyone can pick anyone
> d) Decide for me

Every question works this way:

- **Plain words**, with named people and concrete moments instead of jargon.
- **The stakes are in the question**, so you learn what the choice decides.
- **Options are anchored** to products you have used ("glassmorphism, like Apple's
  Control Centre").
- **One recommendation, and always "Decide for me".** Anything decided for you is logged
  with its reason and how hard it is to reverse.
- **"Show me instead"** for anything about looks: send screenshots and it extracts the
  palette and style.

## What makes it different

| Most spec prompts | Ultimate Prompt Engine |
|---|---|
| Ask generic questions ("What's your tech stack?") | Bans 9 generic questions by name and asks what you have not thought of |
| Decide quietly when you don't answer | Logs every assumption with reasoning, evidence and reversibility |
| Accept contradictions | Checks every answer against every earlier one and names clashes out loud |
| Work from the model's memory | Searches online for the facts that change (pricing, platform rules, shutdowns) and labels each as documented, widely reported or judgment |
| Stop at a summary | Writes a full spec, then verifies it: every requirement traced to a decision, every formula tested with real numbers |

## Install

### Claude Code

Clone or download this repository, then from its folder:

```bash
mkdir -p ~/.claude/skills
cp -r skills/ultimate-prompt-engine ~/.claude/skills/
```

That makes it available in every project. For one project only, copy it into
`.claude/skills/` inside that project instead. Invoke it with
`/ultimate-prompt-engine`, or just describe something you want to build.

### Claude app (claude.ai, desktop, Cowork)

1. Zip the `skills/ultimate-prompt-engine` folder (or download the zip from the latest
   release).
2. Go to **Customize > Skills**, click **+**, then **Create skill > Upload a skill**.
3. Upload the zip. Code execution must be enabled.

### Single-file edition

[`editions/single-file/SKILL.md`](editions/single-file/SKILL.md) carries the loop, the rules,
the defaults and all 169 question stems in one file (about 470 lines, ~15k tokens), for setups that can
only hold one instruction file. The full edition in `skills/` is sharper: it loads the
detailed packs only when needed.

### Other agents (Cursor, Codex, anything that reads instructions)

Point the agent at `skills/ultimate-prompt-engine/SKILL.md` as its instructions, with the
rest of the folder available to read. Without a question tool, the skill switches to a
numbered question block you answer in one message (`1a 2c 3d`).

## Use

```
/ultimate-prompt-engine I want to build a web app where our astronomy club logs what
we observed each night, and it tells members when the sky will be worth going out for.
```

It will:

1. **Read back** your idea in its own words and check the risky assumptions with scenario
   questions.
2. **Classify** the project (web app, mobile app, CLI tool, API service, ML system,
   browser extension, game, or anything else) and ask how deep to go: Quick (3 rounds),
   Standard (5) or Deep (8).
3. **Research** comparable products, how projects like this fail, and current facts about
   your stack.
4. **Interview** you, at most 4 questions a round, reviewing every answer for clashes,
   new questions it opened, and conflicts with the tools you named.
5. **Gate**: it will not write the spec while required questions are open. When the
   rounds run out, you choose: decide the rest, one more round, or go deeper.
6. **Write `spec/`** and check it before handing it over.

Run it again on a project that already has `spec/state.json` and it updates the spec
instead of starting over, asking only about what changed.

## What you get

```
spec/
  SUMMARY.md            one screen: what, for whom, v0, must-never, decisions to review
  00-brief.md           your idea verbatim, the corrected read-back, principles
  01-scope.md           v0 / v1 / later, non-goals, success number
  02-users-and-flows.md named people, step by step, with failure branches
  03-data-model.md      entities, invariants, exact formulas
  04-features/          one file per feature, each with acceptance checks
  05-architecture.md    stack, what runs where, integrations, cost
  06-experience.md      look, screens, words, asset delivery spec
  07-decisions.md       every decision: yours, assumed, found while writing
  08-risks.md           including warnings you chose to accept
  09-open-questions.md  deferred and unverified items
  10-build-plan.md      milestones in build order
  AGENTS.md             rules the coding agent must follow
  state.json            for resuming and updating
```

## Examples

Three complete specs produced during testing:

| Example | Brief | Mode | What it shows |
|---|---|---|---|
| [SplitEasy](examples/spliteasy/spec/SUMMARY.md) | A gamified bill-splitting app | Standard, question tool | 14 gaps found while writing; balance maths tested over 10,000 random cases; then [updated](examples/spliteasy/amendment-2026-09-21.diff) with 5 new decisions |
| [Skylog](examples/skylog/spec/SUMMARY.md) | One line: an astronomy club's logbook and sky forecast | Quick | Research turning a thin brief into specific questions; two bugs caught by the self-check |
| [PYQ Coach](examples/pyq-coach/spec/SUMMARY.md) | A detailed brief: a past-paper bank with AI practice questions | Standard, plain chat | Traps found inside the brief; a formula bug caught by testing its edges |

## Repository layout

```
skills/ultimate-prompt-engine/   the skill (install this folder)
  SKILL.md                       the loop and rules, always loaded
  references/                    loaded only when needed
    archetypes/                  8 project types
    dimensions/                  5 lenses: product, feature, experience, systems, operations
    question-craft.md            how to write and ask questions
    research.md                  how to research and label facts
    defaults.md                  dated "when X, use Y, because Z" tables
    anchors.md                   jargon translated into products people use
    antipatterns.md              banned questions and the questions nobody asks
  templates/                     spec templates and the state.json schema
examples/                        three specs produced by the skill
docs/                            how it works, and what testing changed
```

## Status and honest limits

- Version 1.0. Tested in three dry runs plus one update run, across mobile, web and ML
  projects, with and without the question tool. [What each run changed](docs/dry-runs.md).
- **Not yet tested cold:** in every run, the model that wrote the skill also ran it. A fresh
  session loading it from scratch is the next real test. Reports welcome.
- `defaults.md` goes stale. Every entry carries a review date; the skill is told to verify
  anything older than a year before relying on it.
- Anything touching law is labelled "not legal advice".

## Contributing

New archetypes, sharper questions, and corrections to stale defaults are all welcome. See
[CONTRIBUTING.md](CONTRIBUTING.md).

## Credits

Inspired by [hboon's spec skill](https://hboon.com/build-a-spec-skill-for-your-coding-agent/)
and [GitHub Spec Kit](https://github.com/github/spec-kit) (the `[NEEDS CLARIFICATION]`
marker and the split between what and how), with lenses borrowed from the roles in the
BMAD method.

## License

[MIT](LICENSE)
