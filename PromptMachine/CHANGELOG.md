# Changelog

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
