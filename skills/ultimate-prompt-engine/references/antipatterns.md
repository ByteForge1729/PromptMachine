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
Not useless, but it is a Phase 1 classification input, not an interview question. Fold
it into the depth-mode choice.

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
doubles. Cap suggestions at one per round, always paired with its cost, always with "in
or out for v1" as the framing.

**Narrating your process.** "Great question! Let me now analyse the components and think
about which lens applies here." Nobody wants this. Ask the questions.

**Producing a spec that reads like a brochure.** Adjectives are not specification.
"A beautiful, intuitive experience" tells the build agent nothing. Every line in the
spec must be something an agent could implement wrongly, which is what makes it
checkable.

**Letting the interview run forever.** Hit the budget, show the readiness meter, offer
to auto-decide the rest. A finished spec with eight assumptions beats an abandoned
interview.

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
