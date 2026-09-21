# Feature lens

Always active. Covers what the thing actually does, step by step, including the paths
nobody pictures when they imagine their own product.

Same entry format as `product.md`. `Opens` feeds the Phase 3 cascade check.

**The governing rule of this lens:** the user imagines the happy path. Your value is
everything else. For every feature they name, there are three states they have not
pictured: empty, broken, and abusive. Ask about those, not about the happy path.

---

### F1: the core loop `[required]`
**Ask:** Walk me through the single most common thing a user does, from opening the app
to being done. I will turn this into the primary flow and everything else becomes
secondary navigation, so if you name the wrong one the whole interface is built around
the wrong thing.
**Options:** free text, or propose your read from the brief and let them correct it
**Opens:** navigation structure, home screen, 02-users-and-flows.md

### F2: how the loop starts `[required]`
**Ask:** What triggers that action? The user remembering on their own, a notification,
someone else doing something, or a scheduled moment? Self-triggered products need a
reason to be remembered, and most fail there rather than on features.
**Options:** user remembers / push notification / another person's action / scheduled
**Opens:** notification design, retention hook, background work

### F3: the empty state `[required]`
**Ask:** What does the screen show on first launch, before any data exists? This is the
first thing every new user sees and it is the most commonly skipped screen in software.
Blank and confusing is the default outcome if we do not decide now.
**Options:** guided setup / sample or demo data they can delete (recommended) / a single
large call to action / decide for me
**Opens:** onboarding, sample data seeding, 06-experience.md

### F4: the undo question `[required]`
**Ask:** When someone deletes or changes something, can they take it back, and for how
long? "Undo for ten seconds" like Gmail is usually better than a confirmation dialog,
because confirmations train people to tap yes without reading.
**Options:** undo window (recommended) / confirm dialog / soft delete with a recycle bin /
permanent, no recovery
**Opens:** soft delete in data model, audit log, permission to undo someone else's action

### F5: who can change what `[required]`
**Ask:** If two people can see the same thing, can both edit it, or only the one who
created it? And can anyone override that? This is the permission question that gets
discovered during the build if it is not decided now, and retrofitting it is expensive.
**Options:** creator only (recommended for v0) / anyone in the group / creator plus an
admin / decide for me
**Skip if:** strictly single-user
**Opens:** RBAC, audit trail, conflict handling

### F6: simultaneous edits `[required]`
**Ask:** What happens when two people change the same thing at the same second? Someone
loses their edit silently, or someone gets told. Silence is the default if we do not
choose, and silent data loss is the bug users never forgive.
**Options:** last write wins with a visible warning (recommended) / lock while editing /
merge automatically / cannot happen here
**Skip if:** single-user, or nothing is shared
**Opens:** conflict UI, sync strategy, source of truth

### F7: leaving `[required]`
**Ask:** What happens when someone leaves, is removed, or deletes their account midway
through? Does their data go with them, and what breaks for everyone else if it does?
Almost nobody thinks about this, and it is where multi-user products quietly corrupt
their own data.
**Options:** data stays, name becomes "deleted user" (recommended) / data leaves with
them / blocked from leaving until resolved / decide for me
**Skip if:** single-user
**Opens:** soft delete, referential integrity, legal deletion obligations

### F8: the biggest realistic user `[required]`
**Ask:** What is the largest amount of data one user will realistically have? Twenty
items or twenty thousand? The interface that works for twenty is unusable at twenty
thousand, and the fix is search and pagination, decided now rather than after launch.
**Options:** tens / hundreds / thousands / more
**Opens:** search, filtering, pagination, indexing, list performance

### F9: failure in front of the user `[required]`
**Ask:** The save fails because the network dropped. What does the user see, and what
happens to what they typed? Losing typed input on a failed save is the fastest way to
lose a user permanently.
**Options:** keep it locally and retry silently (recommended) / show an error and keep the
form filled / show an error and clear it (never choose this)
**Opens:** offline strategy, retry queue, error copy

### F10: the abuse path `[optional]`
**Ask:** How would someone use this to annoy or harm another user? Adding charges that
are not real, spamming invites, writing something nasty in a free-text field. You do not
have to solve it in v0, but it should be written down rather than discovered.
**Options:** free text, propose the likeliest two yourself
**Skip if:** strictly single-user with no shared content
**Opens:** moderation, reporting, rate limiting, 08-risks.md

### F11: acceptance criteria `[required]`
**Ask:** For the one feature that must survive, how will you know it works? Give me the
check you would actually run. Each feature file needs this or the build agent decides
for itself when it is done.
**Options:** propose two or three concrete checks and let them confirm
**Opens:** 04-features/, testing strategy

### F12: manual before automatic `[optional]`
**Ask:** Is there a step here you could do by hand for the first fifty users instead of
building it? Approving signups, importing data, sending the weekly summary. Doing it
manually for a month tells you whether it is worth automating at all.
**Options:** free text, propose the candidate you can see
**Opens:** v0 scope reduction, 10-build-plan.md

### F13: notifications `[optional]`
**Ask:** What is worth interrupting someone's day for? Every notification you add is a
reason to uninstall if it is wrong. I would rather ship one that earns its place than
five that get muted together.
**Options:** one, tied to the core loop (recommended) / a daily or weekly digest / several
event-based / none in v0
**Skip if:** no notification surface
**Opens:** push infrastructure, permission prompts, notification settings screen

### F14: history and audit `[optional]`
**Ask:** Does anyone ever need to see what changed and who changed it? If money, trust or
shared responsibility is involved the answer is usually yes, and storing history is far
cheaper to decide now than to reconstruct later.
**Options:** full change log (recommended when shared and consequential) / last-modified
only / nothing
**Opens:** event sourcing, data model, storage cost

### F15: the actor check `[required, when more than one kind of member exists]`
Not a question to ask as written. For every action in the spec (confirm, reject, pay,
edit, approve), check that every kind of participant can actually perform it: a member
without the app, one who is offline, one who left, one whose account was deleted. When
someone cannot, ask who acts for them. *"Amit has no app, so he can't tap 'Not paid'.
Who can, on his behalf?"* This check found the biggest gap in the first dry run.
**Opens:** delegation rules, admin powers, auto-behaviour that nobody can stop

### F16: the owner leaves `[required, when groups or shared spaces have an owner]`
**Ask:** If the person who created the group deletes their account, who takes over their
powers? Nobody usually thinks of this until a group is stuck with settings no one can
change.
**Options:** longest-standing member (recommended) / the group votes / nobody, settings
freeze
**Opens:** ownership transfer, admin actions

### F17: every game number `[required, when a game layer exists]`
Every mechanic needs concrete numbers before emit: thresholds, time windows, levels.
Propose defaults with a one-line rationale and let the user adjust them all in one
question, instead of discovering them while writing the spec.

---

## Cascade rules

| If the answer is | Add these |
|---|---|
| shared editing is allowed | conflict handling, audit log, permission to undo others |
| data leaves with a departing user | referential integrity, what breaks, legal deletion |
| thousands of items per user | search, pagination, indexing, list virtualisation |
| notifications exist | permission prompt timing, settings screen, quiet hours |
| free-text fields visible to others | moderation, reporting, length limits, injection safety |
| undo exists | soft delete throughout, retention window, who may undo whose action |
| network failure keeps data locally | local storage, retry queue, sync conflict handling |
