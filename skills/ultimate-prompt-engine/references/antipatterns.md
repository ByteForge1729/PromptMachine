# Antipatterns

Read once before the first round. These are the failure modes that turn this skill
back into an ordinary spec prompt.

---

## The test every question must pass

1. **Could a stranger answer this without knowing the project?** If yes, it is generic.
   Delete it.
2. **Does the brief already answer it?** If yes, you did not read the brief.
3. **Do both answers produce the same build?** If yes, decide it yourself and log it.
4. **Does the user learn something by reading it?** If no, add the stakes.
5. **Would a good engineer default this without asking?** If yes, default it and log it.
   Ask only if the project makes the default wrong.

A question surviving all five is worth the user's attention. Most drafts fail 1 and 4.

---

## Banned questions

These are banned as written. Each has a rewrite that is allowed.

**"What's your tech stack?"**
Too early and backwards. Stack follows requirements. Ask about the requirement that
constrains the stack. *Rewrite:* "Does this need to work with no signal, on a train or
in a basement? That decides whether the phone holds its own copy of the data, which
changes roughly a third of the build."

**"Who is your target audience?"**
Produces "young people aged 18-30" and teaches you nothing. *Rewrite:* "Picture the
person who opens this for the fifth time. What just happened in their life that made
them open it?"

**"What features do you want?"**
They already told you, and asking again makes you look like you were not listening.
*Rewrite:* propose the cut. "I read four features. For v0 I would ship two and drop the
other two to v1. Here is which and why. Do you agree?"

**"Do you want it to be user-friendly / fast / secure?"**
Nobody says no. Useless. *Rewrite:* make them trade. "Which do you give up first under
pressure: shipping on time, the animation polish, or working offline?"

**"What's your budget and timeline?"**
Money is the cost question (O5). Time matters only when a date exists. *Rewrite:* "Is
there a day this has to exist by? A deadline changes what belongs in the first version
more than any feature preference."

**"Should it be scalable?"**
Everyone says yes and means nothing. *Rewrite:* "What number of users would make you
genuinely happy in year one? I will build for that number times ten and no further,
because designing for a million users you do not have is the most common way these
projects die."

**"Should we use microservices?"**
Almost never the right question for anything this skill will be pointed at. *Rewrite:*
skip it, default to one service, log it as ASSUMED.

**"What colour scheme do you want?"**
Premature and unanswerable in the abstract. *Rewrite:* anchor to feel. "Which of these
does it feel closest to: the quiet grey of Linear, the loud playful colour of Duolingo,
or the near-invisible chrome of Apple Notes?"

**"Any other requirements?"**
The laziest question in software. If they knew, they would have said. *Rewrite:* name
the gap yourself. "Nobody has mentioned what happens when someone leaves the group with
an unsettled balance. Three options, or I can decide."

---

## Behavioural failures

**Deciding silently.** The worst one, because it is invisible. If you picked it, it goes
in `07-decisions.md` and carries an `[ASSUMED]` marker inline. The user must be able to
audit every choice they did not make.

**Asking the same thing twice in different words.** Check `state.json` before every
round. Repeating a question destroys the user's trust that you are tracking the
conversation.

**Accepting a contradiction.** If they said offline-first in round 2 and live
leaderboards in round 4, you must say so. Letting both into the spec guarantees the
build agent produces something incoherent, and the user will blame the build, not the
spec.

**Question stacking.** Four questions where each depends on the previous answer. Ask the
gating question alone, then branch.

**Scope inflation.** You suggest a feature, they say yes out of politeness, and the v0
doubles. Suggest only in the delight step: 2 to 4 ideas, once, each with its cost, each
one easy to refuse.

**Narrowing early.** Asking "dark or light?" before asking what it should feel like.
Offering three options that are the same idea in three colours. Putting your favourite
first on a question of taste. Each one quietly makes the product more like the last one
you specified.

**Jargon in the question.** "Do you want scroll-driven animation?" The user says yes to
sound capable. Describe what they would see, and keep the term for the spec.

**Narrating your process.** "Great question! Let me now analyse the components and think
about which lens applies here." Nobody wants this. Ask the questions.

**Producing a spec that reads like a brochure.** Adjectives are not specification.
"A beautiful, intuitive experience" tells the build agent nothing. Every line in the
spec must be something an agent could implement wrongly, which is what makes it
checkable.

**Letting the interview run forever.** Show the meter after every round so the user can
see what is left and stop. When they say "enough", stop. A finished spec with eight
listed assumptions beats an abandoned interview.

**Padding.** Asking a nice-to-have to look thorough. Every question must change the
spec; if you cannot say which line it changes, do not ask it.

---

## The generic look

A build agent given no direction produces the most common page it has seen. These are
its marks. None is wrong when chosen on purpose; each is wrong as a default.

| Mark | What it means was never decided | Decided by |
|---|---|---|
| One everyday typeface for everything (Inter, Roboto, system) | how the words should look | E4 |
| A purple or indigo glow, gradients on everything | what the colours are for | E19, E1 |
| Headline in the middle, a small badge above it, a button below | what a stranger should see first | E6, WS3 |
| Three or six identical cards, each with an icon, a title and two lines | what actually matters, in what order | F1, P3 |
| Emoji used as icons | where pictures come from | E5, E11 |
| "Welcome to X", "Seamless", "Powerful", "Get started" | how it talks | E17 |
| Everything fades in the same way, or nothing moves | what movement is for | E22 |
| Always dark, grey text, tiny capital labels | light, dark or both | E2 |
| Frosted glass panels, soft glows | what it must not be mistaken for | E21 |
| No empty screen, no error message, no loading state | what happens when it is not the happy path | F3, F9 |
| The same spacing between everything | what belongs together | E6 |
| A game where every hit shakes the screen and sprays particles | what the main action feels like | GA14 |
| A simulation that is a picture with a column of sliders beside it | what should click, and who is driving | SM1, SM2 |
| A graph in the chart tool's stock colours, with its grid and boxed legend | what the picture is meant to show | SM1, SM9, E3 |

**The check, at emit.** Read `06-experience.md` against the table. For every mark that
appears: if the user chose it, cite the decision; if nobody chose it, replace it with a
choice that follows from E19 and log that as `ASSUMED`.

**No feeling, no check.** If E19 was never answered, or was answered "not sure" with
nothing else to go on, there is no point of view to derive anything from, and every look
decision in the spec is a guess. Say so on the first line of "Assumed because we
stopped", propose one sentence of point of view there, and mark each look decision as
resting on it. Do not present guessed taste as a decision.

**A ban list is not enough.** Telling a builder "not Inter" gets the next most common
typeface, and those have become marks too. The spec must say what to use and why, in
`06-experience.md`: the point of view in the user's words, the named lettering, the
colours with their jobs, what moves and for how long.

Evidence: the marks and their frequency (documented: Krebs, a scan of 1,590 pages); the
cause and the fix (documented: Anthropic, "Improving frontend design through Skills").
Full notes in `docs/research-notes.md` in the repository.

---

## The unasked questions

These are the ones users almost never think of, and the reason this skill exists.
Mine them for every project.

- What does the very first screen show when there is no data yet?
- What happens when someone leaves, is removed, or deletes their account mid-flow? Does
  their data leave with them, and what breaks if it does?
- Who is allowed to undo or delete something, and how long after?
- What happens when two people do the same thing at the same moment?
- What does the user see when the network is gone, and again when it comes back?
- What is the largest realistic amount of data one user will have, and does the
  interface still work at that size?
- What do you do when the third-party service you depend on is down or changes pricing?
- Who pays, and what happens at the moment the free tier runs out?
- What is the one thing that must never happen, even at the cost of a feature?
- If this succeeds and you stop working on it for six months, what breaks first?
- What does success look like as a number, and how will you know you hit it?
- What are you deliberately not building, so you can say no later without renegotiating?
- For every action, who performs it when the usual person cannot: no app, offline, left,
  deleted?
- If the owner or admin disappears, who inherits their powers?
- Who pays whom, exactly, when several people owe several others?
- Where does each piece of outside information come from (a payment ID, an address, a
  phone number), and who can see it?
- Is any service you plan to use deprecated or shut down? (Search. Firebase Dynamic
  Links shut down in August 2025, and tutorials still recommend it.)
- What are the upper bounds: can someone pay more than they owe, add a negative amount,
  tap twice?
- What should someone feel in the first minute, and what should they remember a day
  later?
- Which one moment deserves more care than all the others?
- What does a person on an old phone get in place of the heavy part?
- What does someone get who has movement switched off, or cannot see the screen?
- What is it doing before anyone touches it?
- Which action happens fifty times a day, and is it instant?
