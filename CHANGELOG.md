# Changelog

## 2.0.1: 2026-11-20

- **Questions are laid out as bullets.** The question on its own line, the stakes under
  it, then each option as its own bullet. Lists inside a question (yes/no items, extras)
  are bulleted too. Before, chat apps joined the options into one long paragraph. The
  wording of questions and options is unchanged.

## 2.0.0: 2026-11-15

Feel-first questions, a brainstorm, a delight step, and no more depth modes. Sources
for the design guidance are in [docs/research-notes.md](docs/research-notes.md).

- **Brainstorm (new).** Offered once with the read-back. On yes: at least eight
  directions from different angles, nothing decided, then a short summary that the
  questions start from. `references/brainstorm.md`.
- **Questions.** Feel and intent are asked before mechanics. Taste questions carry no
  recommendation and at least four directions. "Decide for me" became "Not sure, suggest
  one"; "Something else" is always offered. One idea per question.
- **Experience lens.** Six new questions (E19 to E24): the one-minute feeling, the moment
  worth extra care, what it must not be mistaken for, what movement is for, what weak
  phones get, and how often the main action happens. E1 and E4 rewritten.
- **Two new project types.** `website.md` (sites people come to look at) and
  `simulation.md` (things people play with to understand). Three new game questions
  (GA14 to GA16).
- **The generic-look check.** `antipatterns.md` lists the marks of a default AI-built
  page; the spec is checked against them before handover. Look, motion and speed
  defaults added to `defaults.md`.
- **Delight step (new).** Once per interview: 2 to 4 ideas that could only belong to
  this product, each with a reason and a rough cost, accepted, edited or rejected one by
  one. Replaces "one feature suggestion per round". `references/delight.md`.
- **Ordering.** `[required]` and `[optional]` became `[must-ask]`, `[should-ask]` and
  `[nice-to-have]`, used only to decide what is asked first.
- **Removed:** Quick, Standard and Deep modes, the round budget, the blocking gate, and
  the short-format spec. Say "enough" at any point; what was not asked is assumed and
  listed at the top of the summary.
- **`state.json` schema 2:** `depth` and `round_budget` removed; `brainstorm`, `delights`
  and `stopped_early` added; coverage counts `must` and `should`.
- Example specs updated to schema 2. They were produced by 1.0 and are otherwise
  unchanged.

### Changes made during the paper runs

- E4 (lettering) and E22 (movement) are must-ask when people come to look, so "enough"
  after two rounds does not skip them. E19 is asked in round 1.
- P1 and P6 gained `Skip if` lines for websites and simulations.
- GA2 no longer opens with engine names.
- E3 fires whenever colour tells two things apart, not only for money.
- The delight step checks that an idea is true to the subject, and triggers on WS1, GA3
  or SM1 as well as F1.
- Three rows added to the generic-look table: games, simulations, graphs.

Not tested with a real user. See [docs/dry-runs.md](docs/dry-runs.md), runs 5 to 7.

## 1.0.0: 2026-09-21

First public release of **Ultimate Prompt Engine**.

- Interview loop: read-back, classify, research, rounds, review, gate, write, update.
- 5 lenses (product, feature, experience, systems, operations) and 8 project types (web
  app, mobile app, CLI tool, API service, ML system, browser extension, game, generic),
  169 questions in total.
- Research step with documented / widely reported / judgment labels.
- Spec templates, `state.json` schema, and a self-check before handover.
- Update mode for existing specs.
- Works with a question tool (Claude Code, Cowork) or in plain chat.
- Three example specs.

### Changes made during testing, before release

- Plain-language rule after the first read-back question needed rephrasing.
- Lens rotation after design questions were starved by technical follow-ups.
- Experience lens with assets, and "Show me instead" reference uploads for taste questions.
- Research phase, after the best question of the first run came from a live search.
- Stack check, after a clash between offline storage and Expo Go.
- Must-never rule beats pack defaults; decisions sorted by stakes for review.
- Actor check, owner-succession and game-number questions, after gaps found while writing.
- Systems and Operations lenses; account deletion, privacy law, minors, backups.
- Clash shortcut when the newer answer implies the fix.
- Self-check extended to the spec's own wording and to formula edge cases.
- `SKILL.md` cut from 335 to 190 lines.
