# Dry runs

What each test run found, and what it changed in the skill.

## 1. SplitEasy: mobile app, Standard, question tool

A gamified bill-splitting app for students.

| Finding | Change to the skill |
|---|---|
| The first read-back question used jargon and had to be rephrased | Plain-language rule; scenario questions with named people |
| The best question (who confirms a UPI payment) came from a live search, not a pack | Research phase |
| Design, visuals and assets were never asked about | Experience lens, lens rotation, "Show me instead" |
| Offline storage clashed with the user's Expo Go setup | Stack check in every review |
| Writing the spec found 14 gaps, including a ghost member who could not reject a fake payment | Actor check, owner succession, game-number questions |
| The Operations lens later found 5 more gaps (account deletion, privacy, minors, backups, abuse) | Tested update mode; see [the diff](../examples/spliteasy/amendment-2026-09-21.diff) |

## 2. Skylog: web app, one-line brief, Quick

An astronomy club's logbook and sky forecast.

| Finding | Change to the skill |
|---|---|
| Research did most of the work for a thin brief (light pollution, monsoon, observers' needs) | Confirmed the research phase |
| Four clashes in three rounds, one resolvable from the newer answer | Clash shortcut |
| "Never call a cloudy night good" cannot be guaranteed | Must-never check: restate impossible rules honestly |
| Success measured by one trip is mostly luck | Success check: add a sustained-use measure |
| The spec's own screen text used a word it banned; an agreement formula mislabelled clear full-Moon nights | Self-check covers the spec's own wording and formula edge cases |
| Supabase's free email and pausing limits would have broken login and the monsoon | Added to `defaults.md` |

## 3. PYQ Coach: ML system, detailed brief, plain chat

A shared past-paper bank with AI practice questions.

| Finding | Change to the skill |
|---|---|
| Never re-asked anything the brief stated | Confirmed |
| Found three traps inside the brief before round 1 (free vs per-call cost, "must be correct" vs AI solutions, live coursework uploads) | Confirmed |
| A frequency formula mixing marks and question counts showed a topic with half of all questions as 6% | Edge-case formula testing earned its place |
| The skill's own earlier claim ("v0 has no model costs") was wrong and corrected mid-interview | Kept as a documented example of correcting itself |

## 4. SplitEasy update

Update mode read the existing `state.json`, asked one question (the one it never decides
alone), decided the rest with sources, and patched 9 files plus 1 new one: 37 lines added,
5 changed, nothing earlier deleted.
