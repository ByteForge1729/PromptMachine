# Contributing

The skill gets better in three ways: sharper questions, more project types, and fresher
facts. All three follow the same rule the skill follows: **every claim is labelled, dated
and sourced.**

## Add or improve a question

Questions live in `skills/ultimate-prompt-engine/references/dimensions/` (lenses that
apply to every project) and `references/archetypes/` (one project type each). Every entry
uses this format:

```markdown
### W3: the in-app browser trap `[must-ask, when links are shared on social or chat apps]`
**Ask:** the question in plain words, one idea, with its stakes inside it.
**Options:** seeds for 2 or 3 options, recommendation first. Taste questions (feel,
look, motion, sound, voice) get four or more directions and no recommendation.
**Skip if:** when the question does not apply (optional)
**Opens:** what an answer cascades into; feeds the review step
**Evidence:** source and label, for anything that can change
```

Tag it `[must-ask]`, `[should-ask]` or `[nice-to-have]`. The tag only sets the order of
asking: must-ask when a wrong guess is costly or hard to undo, nice-to-have when a
sensible default is nearly always right. Keep technical terms out of the **Ask** line;
they belong in **Opens** and in the spec.

A question is worth adding only if it passes the five tests at the top of
`references/antipatterns.md`. The short version: a stranger could not answer it without
knowing the project, and the user learns something by reading it. Every question must
change the spec. If you cannot name the line it changes, leave it out.

The single-file edition in `editions/single-file/SKILL.md` carries every question as a
one-line stem. Add yours there too.

Also add a row to the file's **cascade table** if your question is opened by another
answer.

## Add a project type

1. Copy `references/archetypes/mobile-app.md` as a model.
2. Write the **governing rule**: the one thing this medium forces on every project.
3. Pick an unused ID prefix (in use: P, F, E, S, O, M, W, WS, C, I, L, X, G, GA, SM).
4. Research the platform's current rules and label every fact.
5. End with **defaults** (assume these, don't ask) and a **cascade table**.
6. Add a row to the archetype table in `SKILL.md`.
7. Run a dry run (below) before opening a pull request.

## Fix a stale default

Entries in `references/defaults.md` carry a review date. When you find one that has
changed, update the row, keep the reasoning, add the source, and change the date.

## Dry-run protocol

Before changing `SKILL.md` or adding a pack, run the skill on a real idea and note:

- questions the user had to ask you to rephrase (plain-language failures);
- places where the spec's look was left to a default instead of a decision;
- clashes it caught and any it missed;
- gaps found only while writing the spec;
- bugs the self-check caught.

Put the findings in the pull request. [docs/dry-runs.md](docs/dry-runs.md) shows the format.

## Style

- Plain words, named people, concrete moments.
- No em dashes.
- Keep `SKILL.md` under 200 lines; detail belongs in `references/`.
