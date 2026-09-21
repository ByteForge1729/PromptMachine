# PYQ Coach: spec (Standard mode)

**What:** A student-built bank of IIT Bombay past papers. Seniors upload or photograph
papers; an AI model reads every question and sorts it by syllabus topic; students see an
honest topic map, practise real past questions, and get a 3-day exam plan. AI-generated
practice questions come in v1.
**For:** A student three weeks before an end-sem deciding where to spend their time.
**v0 contains:** accounts synced across phone and laptop, PDF and camera upload, reading
with scan snippets and figures, duplicate merging, syllabus versions, topic map with an
"Important, not asked yet" branch, practice by topic, exam-week plan, share links.
**Not building:** current-semester material, exam predictions, a leaderboard, a doubt chat,
other colleges.
**Must never happen:** a solution shown as checked when it isn't, or a guess shown as a fact.

## Readiness

```
Product     ########  8/8
Feature     ########  10/10
Experience  ########  12/12
Systems     ########  12/12
Operations  ########  12/12
ML          ########  13/13   (v1 items decided now, built later)
```
Decisions: 5 from your brief · 28 yours · 32 assumed (6 found while writing this spec) ·
2 deferred · 2 unverified

## Review these first

| # | Decision | Why it matters |
|---|---|---|
| A36 | **Every senior solution is hidden behind "Not checked yet" in v0** | You chose to check senior solutions like AI ones, but the checker only exists in v1. Showing them plainly would break your must-never rule |
| A7 | Must-never restated as "never present a solution as checked unless it passed; never present a guess as a fact" | Your original wording cannot be guaranteed by any checker |
| A12 | Frequencies use marks only when every paper prints them | Found by testing the formula: mixing them misreports topics badly |
| A2 | Reading runs as small background jobs | Vercel's free plan stops any job at 5 minutes |
| A6 | You cover reading costs up to ₹1,000 a semester | No sponsor yet, and reading scans still costs money |
| 09 | **Check your department's AI policy before M1** | Sending institute exam papers to an outside AI company may not be allowed |

## Found while writing the spec

| # | Gap |
|---|---|
| A36 | Senior solutions had no safe display until the v1 checker exists |
| A12 | The frequency formula misreported topics when some papers print marks and others don't. Tested: a topic with half of all questions showed as 6% |
| A26 | "Old syllabus" needed syllabus versions with the year they take effect |
| A27 | AI duplicate merges needed an undo |
| A34 | A question on two topics would have counted twice, pushing frequencies over 100% |
| A35 | Share links in v0 needed content, since the questions you asked about are v1 |

## Files

| File | Answers |
|---|---|
| [00-brief.md](00-brief.md) | The idea and the principles |
| [01-scope.md](01-scope.md) | v0, v1, non-goals, success |
| [02-users-and-flows.md](02-users-and-flows.md) | Six flows, with failure branches |
| [03-data-model.md](03-data-model.md) | Entities, 9 invariants, the frequency and plan maths |
| [04-features/](04-features/) | Seven features with acceptance checks |
| [05-architecture.md](05-architecture.md) | Stack, jobs, sandbox, cost |
| [06-experience.md](06-experience.md) | Look, screens, words, assets |
| [07-decisions.md](07-decisions.md) | Every decision and why |
| [08-risks.md](08-risks.md) | Including the two risks you accepted |
| [09-open-questions.md](09-open-questions.md) | Policy check, backups, sponsor |
| [10-build-plan.md](10-build-plan.md) | M0 to M4, then v1 |
| [AGENTS.md](AGENTS.md) | Rules for the coding agent |
