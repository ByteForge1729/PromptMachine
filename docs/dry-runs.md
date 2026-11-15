# Dry runs

What each test run found, and what it changed in the skill.

Runs 1 to 4 were made with version 1.0, which had fixed interview lengths. Runs 5 to 7
are paper runs of version 2.0.

## 1. SplitEasy: mobile app, five rounds, question tool

A gamified bill-splitting app for students.

| Finding | Change to the skill |
|---|---|
| The first read-back question used jargon and had to be rephrased | Plain-language rule; scenario questions with named people |
| The best question (who confirms a UPI payment) came from a live search, not a pack | Research phase |
| Design, visuals and assets were never asked about | Experience lens, lens rotation, "Show me instead" |
| Offline storage clashed with the user's Expo Go setup | Stack check in every review |
| Writing the spec found 14 gaps, including a ghost member who could not reject a fake payment | Actor check, owner succession, game-number questions |
| The Operations lens later found 5 more gaps (account deletion, privacy, minors, backups, abuse) | Tested update mode; see [the diff](../examples/spliteasy/amendment-2026-09-21.diff) |

## 2. Skylog: web app, one-line brief, three rounds

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

---

# Version 2.0: paper runs

**What these are.** Runs 5 to 7 trace the 2.0 files by hand from brief to spec outline.
The author of the changes played both sides: no real user answered, no spec folder was
written, and nothing was built from the result. They show which questions fire, in what
order, and where a generic result can still get through. They do not show that the
questions are good; only a real run can.

## 5. Portfolio site

Brief: *"a portfolio site for my illustration work"*. Pack: `website.md`. Lenses:
product, feature, experience, operations.

| Step | What happens |
|---|---|
| Read-back | Two scenario checks (who lands here; what they should do), plus the brainstorm offer |
| Brainstorm (yes) | Ten directions from ten angles: a sketchbook you page through; one endless wall; a shop that happens to show work; a single drawing you travel into; a drawing a day; three pieces and a contact line, nothing else; a printed zine with a web copy; the wrong one, no pictures until you ask. Synthesis: pulled toward the sketchbook and "three pieces"; pushed away from anything shop-like |
| Round 1 | E19 the one-minute feeling, WS1 the one thing a visitor does, WS2 how people get here, WS4 what is real today |
| Round 2 | WS3 the first five seconds, E4 lettering, E22 what movement is for, P8 must-never |
| Delight | After WS1 and E19: page turns that follow the paper's edge (a few days); one drawing shown from pencil to ink by dragging (a few days, needs the pencil scans); the page a shade warmer in the evening (an afternoon, marked as the likely gimmick) |
| "enough" | After round 2. Assumed and listed: E21, E20, E23, WS5, WS7, WS8, WS10, P3, P4, P5, F3, F9, O3, O5 |
| Spec | `06-experience.md` carries the point of view in her words, a named heading and reading face, three colours with jobs, a motion table, a still picture behind the page-turn effect |

| Finding | Change to the skill |
|---|---|
| P1 "the fifth open" makes no sense for a page people visit once | `Skip if` added to P1; WS1 and WS2 ask it in the medium's terms |
| P6 asks for a user count on a site with no users | `Skip if` added to P6 |
| With "enough" after two rounds, lettering and movement were should-ask and would never have been asked | E4 and E22 are must-ask when people come to look |
| E19 could land in round 2 behind product questions | E19 is asked in round 1 whenever Experience is active |
| The delight step was tied to F1, which a website does not really have | Trigger is F1 or its counterpart: WS1, GA3, SM1 |

**Where a generic result can still get through**

- **"Not sure, suggest one" on every taste question.** The point of view is then the
  model's, drawn from the middle of what it has seen. The spec says so on the first line
  of the assumptions, which is honest, not a cure.
- **Naming the typeface.** She said "quiet and bookish"; the model still has to name a
  face, and will reach for the most common bookish one. The skill cannot see typefaces.
  Only a reference from the user ("show me instead") really fixes this.
- **The same motion numbers for everyone.** `defaults.md` gives every project movement
  under 300 ms with the same settle. Safe, and a house style of its own.
- **Material that does not exist yet** (WS4 "almost none"). The spec says the design
  waits; a build agent may still fill the gaps with stand-in pictures.
- **Product and operations must-asks written for apps.** The five tests should default
  most of them for a website, but a literal reading asks them and uses up the user's
  patience before E20 and E21.

## 6. 2D game

Brief: *"a 2D browser game where you are a cat knocking things off shelves"*. Pack:
`game.md`. Lenses: product, feature, experience.

| Step | What happens |
|---|---|
| Brainstorm | Declined. Not offered again |
| Round 1 | GA3 the thirty-second loop, E19 the one-minute feeling, GA1 where it is played, P8 must-never |
| Round 2 | GA14 what the main action feels like (answer: "soft and satisfying, then one loud crash"), GA8 controls, GA4 why come back, E4 lettering |
| Delight | After GA3 and E19: the owner's voice from another room, louder with each thing broken (a few days, needs recorded lines); the last ten seconds replayed as a loop to send (a few days); the cat falls asleep if you stop playing (an afternoon) |
| Rounds 3 to 5 | The remaining must-asks: GA2 the game-making tool, GA5 alone or together, GA6 saving, GA10 art and sound count, GA13 the first finished level, E22 what movement is for, and the product and feature ones that apply |
| Round 6 | Should-asks begin: GA15 comfort switches, GA7 learning to play. The user says "enough". Assumed and listed: GA9, E20, E21, E2 |
| Spec | Effects table: each effect with its trigger, length and off switch; one loud crash reserved for the last object on a shelf |

| Finding | Change to the skill |
|---|---|
| GA2 opened with "Which engine?" and three engine names, which a non-technical person cannot answer | GA2 now asks whether they already use a tool and offers to pick one; the licence facts moved to the spec |
| Nothing asked what the main action should feel like; the model would have listed every standard effect | GA14, asked after GA3 |
| Shake and flashes had no off switch, and one cue was sound only | GA15, and two new defaults |
| The generic-look table only described web pages | Rows added for games, simulations and graphs |

**Where a generic result can still get through**

- **The art.** If E11 is "AI-generated", the skill asks for a style sheet but cannot
  judge the pictures. This is the largest gap for a game.
- **The effects list is written by the model.** GA14 sets the feel, but the model still
  chooses which effects deliver it and may list the usual set. The check catches "every
  hit shakes the screen"; it will not catch a merely ordinary list.
- **Whether the loop is fun.** GA3 says to prove it on grey boxes first. A spec cannot
  test that.
- **Sound.** One nice-to-have question (E16) and the count in GA10. No source on sound
  design was read for this version.

## 7. Maths simulation

Brief: *"something to explore the predator-prey model for my class"*. Pack:
`simulation.md`. Lenses: product, feature, experience, systems.

| Step | What happens |
|---|---|
| Brainstorm (yes) | Nine directions: a meadow you watch from above; a single sentence with numbers you drag; a game where you are the fox; two graphs and nothing else; a week-long classroom experiment that advances a day at a time; a version with the numbers hidden, where students guess the rule; the wrong one, sound only. Synthesis: pulled toward the meadow with one graph; pushed away from the game |
| Round 1 | SM1 what clicks (answer: "the two populations chase each other in a loop, and neither wins"), E19, SM2 who is driving, SM6 right or looks right |
| Round 2 | SM3 before anyone touches it, SM4 what people can change, P8 must-never, E3 colours that carry meaning |
| Delight | After SM1 and E19: drag time backwards along the graph (a few days); "remove the foxes" as one button, to see what the loop depends on (an afternoon); a link that reopens this exact meadow for the class (an afternoon). The stock seed "a twin started a hair apart" was dropped: this model returns to the same loop, so a twin would show nothing |
| Round 3 | E4 lettering, E22 movement, SM7 time, SM9 seeing it more than one way |
| "enough" | Assumed and listed: SM5, SM8, SM10, SM11, E21, E23, P4, P5 |
| Spec | The calculation rule written out, with a check that the populations return to their start after one loop; the opening state chosen and written as numbers |

| Finding | Change to the skill |
|---|---|
| A delight seed that is false for the subject passed the three tests | Test 2 now asks whether the idea is true to how the thing behaves |
| E3 (red and green) only fired for money and scores; two lines on a graph have the same problem | E3 fires whenever colour tells two things apart |
| The default shape, a picture with sliders beside it, had no mark in the check | Row added to the generic-look table, and one for stock chart styling |

**Where a generic result can still get through**

- **The stock graph.** The check names it, but replacing it needs a decision about what
  the graph is for, and that rests on SM1 and SM9. If SM9 is assumed, so is the graph.
- **Correct maths.** SM6 "must be right" leads to a known-answer check in the spec. A
  simple step-by-step method makes this model drift outward slowly, and a check run for
  a short time will pass it. The spec asks for one full loop; a longer run would be safer.
- **Writing.** SM2 "led first, then free" needs words. If nobody writes them, the build
  falls back to labels, and the result is the box of sliders again.
- **Phones.** SM11 was assumed here. Dragging inside a picture on a phone is the hardest
  part of this kind of project and the spec treats it in two lines.

## What the paper runs did not test

- Whether real people can answer the feel questions, or find them vague.
- Whether a brainstorm of eight to twelve directions feels generous or tiring.
- Whether a build agent follows `06-experience.md` closely enough for any of this to
  show in the result.
- The older question packs (mobile, command-line, service, extension, ML) were retagged
  and had "decide for me" renamed, but were not re-read line by line for technical words
  in the question text. GA2 was found this way by accident; there may be others.
