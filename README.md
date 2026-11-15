# PromptMachine

**Turn a rough idea into a clear plan that an AI can actually build.**

You have an idea: "an app for splitting bills with friends" or "a website for our
astronomy club". If you hand that one line straight to an AI coding tool, it has to
guess hundreds of small things, and it usually guesses the boring, common answer.

PromptMachine fixes that. Its main tool, the **Ultimate Prompt Engine**, is a *skill*
(a set of instructions you add to Claude or another AI assistant). Once it's installed,
the AI stops guessing. It **interviews you** the way a good designer and a senior
engineer would, asks about the things you haven't thought of yet, and then writes a
complete plan, called a **spec**, that a coding AI can follow step by step.

You don't need to be technical to use it. If you can answer "a, b or c", you can use it.

---

## How it works, in short

1. **You describe your idea** in a sentence or a page. Either works.
2. **It repeats the idea back** in its own words, so you can fix anything it got wrong.
3. **It offers a quick brainstorm** (optional) with at least eight different directions
   your idea could go, some of them unusual.
4. **It asks you questions**, a few at a time, most important first. It starts with how
   the product should *feel* and gets to features and technology later.
5. **It suggests a few "delight" ideas**: small touches that would only fit your
   product. You keep the ones you like.
6. **You say "enough" whenever you want.** It writes the plan from what you've told it
   and lists everything it had to assume, so nothing is decided behind your back.
7. **It writes a `spec/` folder** and checks it for mistakes before handing it over.

## What the questions look like

The questions are in plain words, and each one says what's at stake. Here is the kind of
question it asked in a test run on a website for a college astronomy club:

> **The weather forecasts disagree about Saturday night. What should the app show?**
> If it calls the night good and the sky clouds over, the club travels to a dark site
> for nothing.
>
> a) Rank the nights and show how much the forecasts agree *(recommended)*
> b) Show the raw forecast and let members judge
> c) Name the single best night
> d) Something else
> e) Not sure, suggest one

A few things are true of every question:

- **It explains why the question matters**, so you know what you're deciding.
- **You can always say "Something else" or "Not sure, suggest one".** When it picks for
  you, it writes down what it picked and why.
- **You can show instead of tell.** For anything visual, send screenshots or links and
  it works out the colours and style from them.
- **It catches contradictions.** If a new answer clashes with an earlier one, it tells
  you.
- **It checks facts online**, such as prices or app store rules, instead of relying on
  old memory.

## Why not just ask the AI directly?

| Asking an AI directly | Using the Ultimate Prompt Engine |
|---|---|
| It asks generic questions, like "What's your tech stack?" | It asks about the things you haven't thought of |
| It quietly decides things for you | It writes down every guess, with the reason |
| It doesn't notice when your answers contradict each other | It checks each answer against the earlier ones |
| It ends with a short summary | It writes a full plan and tests it, including any maths |
| Everything ends up looking like every other AI-made app | It asks what your product should feel like first, then plans the look around that |

---

## Install it

### Option 1: Claude Code (the command-line tool)

1. Download this project. Either click the green **Code** button on this page and
   choose **Download ZIP** (then unzip it), or run:

   ```bash
   git clone https://github.com/ByteForge1729/PromptMachine.git
   cd PromptMachine
   ```

2. Copy the skill into your Claude skills folder:

   ```bash
   mkdir -p ~/.claude/skills
   cp -r skills/ultimate-prompt-engine ~/.claude/skills/
   ```

That's it. The skill now works in every project. Type `/ultimate-prompt-engine`, or
just describe something you want to build.

### Option 2: The Claude app (claude.ai or the desktop app)

1. Download this project with **Code → Download ZIP** and unzip it.
2. Open the unzipped folder, go into `skills`, and zip just the
   `ultimate-prompt-engine` folder.
3. In Claude, go to **Customize → Skills**, click **+**, then
   **Create skill → Upload a skill**.
4. Upload the zip you made. Code execution needs to be turned on in your settings.

### Option 3: Other AI tools (Cursor, Codex, ChatGPT and others)

Give the AI the file `skills/ultimate-prompt-engine/SKILL.md` as its instructions, and
let it read the rest of that folder.

If your tool only takes **one** instruction file, use
[`editions/single-file/SKILL.md`](editions/single-file/SKILL.md) instead. It packs
everything into one file. The full version is a bit sharper, because it loads detailed
notes only when it needs them.

If the tool can't show clickable options, the questions come as a numbered list, and you
reply in one message, like `1a 2c 3d`.

## Try it

Start with something like:

```
/ultimate-prompt-engine I want to build a web app where our astronomy club logs what
we observed each night, and it tells members when the sky will be worth going out for.
```

Then just answer the questions. Say **"enough"** whenever you want it to stop asking and
write the plan.

Already have a plan from an earlier run? Run it again in the same project. It updates the
existing plan and only asks about what changed.

## What you get at the end

A folder called `spec/` with everything a coding AI needs:

| File | What's in it |
|---|---|
| `SUMMARY.md` | The whole plan on one screen. **Start here.** |
| `00-brief.md` | Your original idea, word for word, plus the corrected version |
| `01-scope.md` | What goes in the first version, what comes later, what's left out |
| `02-users-and-flows.md` | Who uses it and what they do, step by step, including when things go wrong |
| `03-data-model.md` | What information the app stores, and any exact formulas |
| `04-features/` | One file per feature, each with a checklist for "is it done?" |
| `05-architecture.md` | What technology to use and what it costs |
| `06-experience.md` | How it should look, move and feel, and the words it uses |
| `07-decisions.md` | Every decision: the ones you made and the ones it assumed |
| `08-risks.md` | What could go wrong, including warnings you chose to accept |
| `09-open-questions.md` | Things still to decide or check |
| `10-build-plan.md` | The order to build things in |
| `AGENTS.md` | Rules the coding AI must follow |
| `state.json` | Saved progress, so it can pick up where it left off |

When it's done, hand the `spec/` folder to any coding AI and ask it to build from it.

## Examples

Here are three real plans the tool produced. They were made with version 1.0, so the
look-and-feel sections are thinner than what the current version writes.

| Example | The idea | What's interesting |
|---|---|---|
| [SplitEasy](examples/spliteasy/spec/SUMMARY.md) | A fun bill-splitting app | Found 14 gaps while writing; the money maths was tested on 10,000 random cases |
| [Skylog](examples/skylog/spec/SUMMARY.md) | A one-line idea: an astronomy club logbook | Turned a very short idea into a detailed plan |
| [PYQ Coach](examples/pyq-coach/spec/SUMMARY.md) | A long brief: a past exam paper bank with AI practice | Found hidden problems inside the brief itself |

---

## What's in this project

```
skills/ultimate-prompt-engine/   the skill itself (this is the folder you install)
  SKILL.md                       the main instructions
  references/                    extra notes it reads only when needed
                                 (project types, question guides, research rules, ...)
  templates/                     the layout for each spec file
editions/single-file/            the whole skill in one file, for simpler tools
examples/                        three finished plans made by the skill
docs/                            how it works, test notes, and research sources
```

## Honest limits

- **This is version 2.0.** Version 1.0 was tested on several real projects (mobile,
  web, and machine learning). The new parts in 2.0 (the brainstorm, the feel-first
  questions and the delight ideas) have only been walked through on paper so far. Real
  runs are the next step.
- **It hasn't been tested by a stranger yet.** So far, every test was run by the same AI
  that helped write the skill. If you try it, please share how it went.
- **Some facts go out of date.** Prices and recommendations in the notes carry a date,
  and the skill is told to double-check anything more than a year old.
- **It isn't legal advice.** Anything about law is clearly marked that way.

More detail: [how it works](docs/how-it-works.md) · [what testing changed](docs/dry-runs.md) ·
[research sources](docs/research-notes.md) · [changelog](CHANGELOG.md)

## Want to help?

Ideas for new project types, better questions, and fixes for out-of-date facts are all
welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

## Credits

Inspired by [hboon's spec skill](https://hboon.com/build-a-spec-skill-for-your-coding-agent/)
and [GitHub Spec Kit](https://github.com/github/spec-kit), with ideas borrowed from the
BMAD method.

## License

[MIT](LICENSE). Free to use, change and share.
