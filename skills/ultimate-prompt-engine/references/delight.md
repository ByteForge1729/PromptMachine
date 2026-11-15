# Delight

Load at Phase 3b: once per interview, as soon as the main action and the one-minute
feeling (E19) are answered. The main action is F1, or its counterpart in the pack: WS1
for a website, GA3 for a game, SM1 for a simulation. Earlier and the ideas are generic;
later and the scope has already set.

A delight feature is a small thing nobody asked for that makes the product feel made by
someone who cared. It is not a core feature and it is not decoration.

## Rules

- Propose **2 to 4**, in one message. Never more.
- Each has three parts: **what it is**, in plain words; **why, for this product**, in one
  line that points at something the user said; **rough cost**.
- **Cost** in plain words: *an afternoon*, *a few days*, *a week or more*. Add what else
  it costs when that is real: slower loading, a file someone must make, a simpler version
  for phones, something to keep running.
- **Be honest about the weak one.** If one is the most likely to feel like a gimmick, say
  so.
- The user **accepts, edits or rejects each**. With a question tool: one multi-select
  question listing them, edits in free text. Without: a numbered list and *"reply like:
  1 yes, 2 no, 3 yes but smaller"*.
- No recommendation. "None of them" is a good answer.
- Do it once. Ideas that come later go in `09-open-questions.md`, not into another round.

## The three tests

Every proposal passes all three before the user sees it.

1. **Could it be pasted into a different product unchanged?** Then it is generic: dark
   mode, confetti, a mascot, a streak, an AI chat box, a leaderboard. Drop it.
2. **Does it serve the feeling in E19, and is it true to the subject?** A calm product
   gets no fireworks. A "twin started a hair apart" shows nothing in a system that
   always settles the same way; check the idea against how the thing really behaves.
3. **Does it stay clear of the must-never rule (P8) and the non-goals (P4)?**

## Where to look

Ideas come from the product's own material.

| Look at | Ask |
|---|---|
| The main action | What would make doing it the fiftieth time still pleasant? |
| The thing it is about | Its material, sounds, words and rituals: what can the product borrow? |
| Time | Can people go back, slow down, or compare then and now? |
| The state it is in | Can a moment be kept, named, or sent to someone exactly as it is? |
| The empty and the broken | Can the first screen, the wait or the error be worth seeing? |
| The person | Can it notice something true about how they use it? Never something they would not expect it to know |

## Seeds by project type

Starting points only. Rewrite each until it passes test 1.

| Type | Seeds |
|---|---|
| Website | a way of moving between pages taken from the subject; one object you can handle; a detail that changes with the hour |
| App or tool | undo that shows what it undid; a keyboard path for the main action; a first screen that teaches by example |
| Game | a reaction to something the player did not expect to matter; a replay of the best moment; a quiet secret |
| Simulation | dragging time backwards; a twin started a hair apart; a link that reopens this exact state; guess first, then watch |
| Command-line tool or service | a dry run that shows what would happen; an error that names the fix; a one-line result worth pasting |

## Worked examples

**A double-pendulum simulation.** Feeling: "the moment chaos clicks".

| Proposal | Why, for this product | Rough cost |
|---|---|---|
| Drag time backwards | You want people to see where two swings split apart; rewinding lets them find that instant | a few days; it has to remember the last minute of movement |
| Ghost twin | A second pendulum started a hair apart shows chaos without a word of explanation | an afternoon |
| Send this exact swing | A link that reopens the same starting position, so a teacher can set it up for a class | an afternoon; no accounts needed |
| Guess first | The person draws where it will be in five seconds, then watches | a few days; fiddly on a phone, and the one most likely to feel like a quiz |

**A portfolio for a furniture maker.** Feeling: "quiet, handmade".

| Proposal | Why, for this product | Rough cost |
|---|---|---|
| Along the grain | Moving between pieces wipes along the wood grain of the piece you just saw | a few days; a plain fade on older phones |
| Turn one chair | One piece can be turned by hand, because you said the joints are the point | a week or more; needs a 3D scan, and a photo for phones that cannot show it |
| Workshop hours | The page is a little warmer when the workshop is open | an afternoon |
| Pencil line | The pointer leaves a faint pencil mark | an afternoon; the one most likely to feel like a gimmick |

## Recording

- **Accepted:** `01-scope.md` under the tier the user picks, source `DL<n>`; a file in
  `04-features/` when it has behaviour; its cost in `10-build-plan.md`.
- **Edited:** restate it in one line, run the Phase 3 clash check, then record it as
  accepted.
- **Rejected:** `01-scope.md` under "Offered and declined", so the build agent does not
  add it on its own.
- All of them: `state.json` under `delights`, with their status.
