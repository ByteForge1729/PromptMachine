# Product lens

Always active. Covers who this is for, why it exists, what success means, and above all
what it will not do.

Entry format:

- **Ask** is the question with its stakes already inside it. Do not strip the stakes.
- **Options** are seeds, not final wording. Expand each with an anchor from
  `anchors.md`. The recommendation goes first.
- **Skip if** lets you drop the question without it counting against coverage.
- **Opens** is what this answer cascades into. Feed it to the Phase 3 cascade check.

`[required]` questions block the readiness gate. `[optional]` ones do not.

---

### P1: the fifth open `[required]`
**Ask:** Picture the person opening this for the fifth time, not the first. What just
happened in their life that made them reach for it? The answer decides what the home
screen shows, because that moment is the only thing it needs to serve.
**Options:** free text. Push back on anything that describes a demographic instead of a
moment.
**Opens:** home screen content, notification triggers, retention hook

### P2: the alternative today `[required]`
**Ask:** What do these people use right now instead? If the honest answer is a
WhatsApp group and a memory, say so, because beating a notes app is a different bar
than beating an existing product.
**Options:** nothing / a general tool (notes, spreadsheet, chat) / a direct competitor /
free text
**Opens:** import and migration questions, differentiation, the switching-cost problem

### P3: the one thing `[required]`
**Ask:** If the build gets cut to a single feature and everything else is dropped, which
one survives? Everything that is not this is negotiable, and I will hold you to that
later when scope starts growing.
**Options:** free text, drawn from the brief. Offer your read first and let them correct it.
**Opens:** v0 scope, build order, the entire 01-scope.md

### P4: non-goals `[required]`
**Ask:** Name two or three things this deliberately will not do, even though someone
will ask for them. Written-down non-goals are how you say no in three months without
relitigating the whole idea.
**Options:** propose three plausible ones from the brief and let them accept or swap.
Never leave this empty.
**Opens:** 01-scope.md non-goals, AGENTS.md constraints

### P5: success as a number `[required]`
**Ask:** What number, at what date, would make you call this a success? Not revenue
necessarily. Twenty people still using it in month three is a real target; "people like
it" is not, because you cannot tell whether you hit it.
**Options:** users / retention / frequency of use / a task completed N times / decide for me
**Opens:** analytics events, 10-build-plan.md milestones
**Check:** if the number can be decided by luck (one trip, one launch day), say so and add
a secondary measure that needs sustained use.

### P6: scale ceiling `[required]`
**Ask:** What user count in year one would genuinely please you? I will design for
roughly ten times that and no further. Building for a million users you do not have is
one of the most common ways projects like this die before launch.
**Options:** under 100 / hundreds / thousands / tens of thousands or more
**Opens:** every Systems-lens question, hosting cost, database choice

### P7: scope tiers `[required]`
**Ask:** Here is your idea split into v0, v1 and later. v0 is what one person can finish
and put in front of a real user. Does this cut land right, or have I put something in
the wrong tier?
**Options:** present your proposed three-tier split, do not ask them to produce it
**Skip if:** the brief is already a single small feature
**Opens:** 01-scope.md, 10-build-plan.md

### P8: the line that must not be crossed `[required]`
**Ask:** What is the one thing that must never happen, even if it costs a feature?
Wrong balances shown to users, a private note becoming visible, data lost on a
reinstall. This becomes a hard constraint the build agent is not allowed to trade away.
**Options:** free text. If they shrug, propose the likeliest one for this archetype.
**Check:** if the rule cannot be guaranteed by any software (forecasts are sometimes
wrong, networks fail), say so plainly and restate it as something the build can
promise: *"never present a night as a sure thing"* instead of *"never be wrong about the
weather"*.
**Opens:** AGENTS.md principles, 08-risks.md, testing priorities

### P9: who else touches it `[optional]`
**Ask:** Besides the main user, is there anyone else who sees or touches this? An admin,
a moderator, a parent, someone who gets a read-only view. A second role roughly doubles
the permission work, so it matters whether it exists in v0.
**Options:** just one kind of user (recommended for v0) / two roles / several
**Skip if:** single-player by construction
**Opens:** RBAC questions, invites, 02-users-and-flows.md

### P10: the abandonment moment `[optional]`
**Ask:** Where do you think people will give up? First launch with an empty screen,
the step where they have to invite someone, or the moment they have to enter data
manually? I will spend the design budget there rather than spreading it evenly.
**Options:** empty first launch / invite step / manual data entry / decide for me
**Opens:** onboarding flow, empty states, import shortcuts

### P11: timeline reality `[optional]`
**Ask:** How many hours a week does this realistically get, and is there a date it has
to exist by? A deadline changes what belongs in v0 more than any feature preference.
**Options:** free text
**Skip if:** already captured during depth-mode selection
**Opens:** 10-build-plan.md, scope tier boundaries

### P12: who maintains it `[optional]`
**Ask:** If you stop touching this for six months, what should still be working when you
come back? That decides whether we can depend on services that need babysitting or
renewals.
**Options:** must keep running unattended (recommended) / fine if it needs occasional care /
it is a one-off, it can rot
**Opens:** hosting choice, dependency risk, 08-risks.md

### P13: public exposure `[optional]`
**Ask:** Will anything here be visible to people outside the group that created it?
Public profiles, shared links, anything indexable. The moment something is public, the
privacy and moderation questions stop being optional.
**Options:** fully private (recommended for v0) / shareable by link / public by default
**Opens:** privacy questions, moderation, abuse handling, legal

---

## Cascade rules

Apply during the Phase 3 cascade check.

| If the answer is | Add these |
|---|---|
| more than one user role | invites, permissions, removal, what a removed user can still see |
| thousands of users or more | cost model, rate limiting, moderation, support load |
| a direct competitor exists | why switch, import path, what you deliberately do worse |
| shareable or public | privacy defaults, takedown, abuse, what a stranger sees |
| a hard deadline | ruthless v0 cut, which features become manual instead of built |
| "it must keep running unattended" | dependency renewals, cost creep, breakage alerts |
