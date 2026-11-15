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
> d) Something else
> e) Not sure, suggest one

And a question about feel, which comes before any question about colours or features:

> **Someone spends one minute with this and then closes it. What do you want them to feel
> in that minute?** This decides almost everything about how it looks and moves.
>
> a) Calm and in control, like a tidy desk
> b) A small thrill, like opening a parcel
> c) Impressed, like walking into a gallery
> d) At home, like a friend's kitchen
> e) Show me instead: send pictures or links
> f) Something else
> g) Not sure, suggest one

Every question works this way:

- **Plain words**, with named people and concrete moments instead of jargon.
- **The stakes are in the question**, so you learn what the choice decides.
- **Options are anchored** to products you have used ("glassmorphism, like Apple's
  Control Centre").
- **Always "Something else" and "Not sure, suggest one".** Anything suggested or assumed
  for you is logged with its reason and how hard it is to reverse.
- **Feel before mechanics.** Questions about look and feel come first, offer several
  different directions, and carry no recommendation, so nothing narrows early.
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
| Leave the look to the builder, who picks the most common one | Asks what it should feel like first, writes down the lettering, colours and movement that follow, and checks the spec against the marks of a default AI-built page |
| Offer two or three safe options | Offers an open brainstorm first if you want one, and later proposes 2 to 4 delight features made for your product, each with its cost |
| Run for a fixed number of questions | Asks the most important questions first; say "enough" at any point and it builds from what it has, listing what it assumed |

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
the defaults and all 202 question stems in one file (about 560 lines), for setups that can
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
2. **Offer a brainstorm**, once. Say yes and it throws out at least eight different
   directions, odd ones included, with nothing decided, then sums up what pulled you.
   Say no and it goes straight to the questions.
3. **Classify** the project: website, web app, mobile app, CLI tool, API service, ML
   system, browser extension, game, simulation, or anything else.
4. **Research** comparable products, how projects like this fail, and current facts about
   your stack.
5. **Interview** you, at most 4 questions a round, the most important first and feel
   before mechanics, reviewing every answer for clashes, new questions it opened, and
   conflicts with the tools you named.
6. **Propose delight features**, once: 2 to 4 small ideas that could only belong to your
   product, each with a reason and a rough cost. You accept, edit or reject each.
7. **Stop when you say so.** There are no modes and no fixed length. Say "enough" and it
   builds the spec from what you answered and lists everything it had to assume, the
   hard-to-undo ones first.
8. **Write `spec/`** and check it before handing it over.

Run it again on a project that already has `spec/state.json` and it updates the spec
instead of starting over, asking only about what changed.

## What you get

```
spec/
  SUMMARY.md            one screen: what, for whom, v0, must-never, what was assumed, decisions to review
  00-brief.md           your idea verbatim, the brainstorm summary, the corrected read-back, principles
  01-scope.md           v0 / v1 / later, delight features taken and declined, non-goals, success number
  02-users-and-flows.md named people, step by step, with failure branches
  03-data-model.md      entities, invariants, exact formulas
  04-features/          one file per feature, each with acceptance checks
  05-architecture.md    stack, what runs where, integrations, cost
  06-experience.md      point of view, lettering and colour, movement, weak devices, words, assets
  07-decisions.md       every decision: yours, assumed, found while writing
  08-risks.md           including warnings you chose to accept
  09-open-questions.md  deferred and unverified items
  10-build-plan.md      milestones in build order
  AGENTS.md             rules the coding agent must follow
  state.json            for resuming and updating
```

## Examples

Three complete specs produced during testing of version 1.0. They predate the
brainstorm, the feel-first questions and the delight step, so their `06-experience.md`
files are thinner than what 2.0 writes.

| Example | Brief | Run | What it shows |
|---|---|---|---|
| [SplitEasy](examples/spliteasy/spec/SUMMARY.md) | A gamified bill-splitting app | Five rounds, question tool | 14 gaps found while writing; balance maths tested over 10,000 random cases; then [updated](examples/spliteasy/amendment-2026-09-21.diff) with 5 new decisions |
| [Skylog](examples/skylog/spec/SUMMARY.md) | One line: an astronomy club's logbook and sky forecast | Three rounds | Research turning a thin brief into specific questions; two bugs caught by the self-check |
| [PYQ Coach](examples/pyq-coach/spec/SUMMARY.md) | A detailed brief: a past-paper bank with AI practice questions | Five rounds, plain chat | Traps found inside the brief; a formula bug caught by testing its edges |

## Repository layout

```
skills/ultimate-prompt-engine/   the skill (install this folder)
  SKILL.md                       the loop and rules, always loaded
  references/                    loaded only when needed
    archetypes/                  10 project types
    dimensions/                  5 lenses: product, feature, experience, systems, operations
    brainstorm.md                the optional open session before the questions
    delight.md                   how it proposes features made for your product
    question-craft.md            how to write and ask questions
    research.md                  how to research and label facts
    defaults.md                  dated "when X, use Y, because Z" tables
    anchors.md                   jargon translated into products people use
    antipatterns.md              banned questions, the generic look, the questions nobody asks
  templates/                     spec templates and the state.json schema
examples/                        three specs produced by the skill
docs/                            how it works, what testing changed, design research notes
```

## Status and honest limits

- Version 2.0. Version 1.0 was tested in three dry runs plus one update run, across
  mobile, web and ML projects, with and without the question tool.
  [What each run changed](docs/dry-runs.md).
- **Version 2.0 has only been run on paper.** The brainstorm, the feel-first questions,
  the delight step and the website and simulation packs were traced through three
  scenarios with the answers invented by the author, not by a real user. A real run is
  the next test.
- **Not yet tested cold:** in every run, the model that wrote the skill also ran it. A fresh
  session loading it from scratch is the next real test. Reports welcome.
- The design guidance (what makes work look generic, movement, speed) comes from the
  sources in [docs/research-notes.md](docs/research-notes.md), which also lists what
  could not be verified.
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
