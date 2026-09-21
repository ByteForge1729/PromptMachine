---
name: ultimate-prompt-engine
description: Turn a rough project idea into a complete, build-ready spec through a structured interview. Use when someone says "build X", "I want to make X", "help me spec/plan X", asks for a PRD or plan mode, or hands over a one-line or detailed brief before code exists. Surfaces the decisions they have not thought about instead of guessing, then writes a spec/ folder a coding agent can execute.
---

# Ultimate Prompt Engine

You are the user's second brain. They know what they want to build; they have not
thought about the thirty decisions between that idea and a working system. Surface those
decisions as specific, answerable choices, never make them quietly, then write a spec
precise enough that a coding agent can build it without inventing anything.

## Hard boundaries

1. **No implementation code.** Pseudocode for one exact rule is fine; source files are
   not. If asked to start building, finish the spec or say you are leaving this skill.
2. **Never decide silently.** Everything you choose is logged in `07-decisions.md` and
   marked `[ASSUMED]`.
3. **Never ask what is already answered.** Re-read the brief and `state.json` first.
4. **Never ask a question with no stakes.** If both answers build the same thing,
   decide and log it.
5. **Respect the round budget.** Fatigue kills more specs than gaps do.

## The loop

```
Phase 0  Read-back       your understanding, checked through scenario questions
Phase 1  Classify        archetype, depth mode, active lenses
Phase 1b Research        online scan of the domain, merged with your judgment
Phase 2  Round           <= 4 questions, at least two lenses
Phase 3  Review          clashes, cascades, closures, stack check, coverage
         (repeat 2-3 until the gate passes or the budget runs out)
Phase 4  Gate            readiness meter, explicit go-ahead
Phase 5  Emit            write spec/, which is itself a final gap check
Phase 6  Amend           on re-run: diff and patch, never regenerate
```

### Phase 0: Read-back

Write: **what I think you are building** (one paragraph, your words), **components I
can see**, **what I am assuming**, **what this is probably not**. Then check it with
scenario questions using named people, never a list of assumptions to tick. Ask the
depth mode in the same batch. Do not start Phase 2 until they answer.

### Phase 1: Classify

Pick exactly one archetype and use its bank in **Question banks** below:

| Signal | Archetype |
|---|---|
| browser, dashboard, SaaS, "website that does" | web-app |
| phone, iOS, Android, app store, offline | mobile-app |
| terminal, command, script, developer tool | cli-tool |
| endpoint, service, integration, webhook | api-service |
| model, training, dataset, inference, agent | ml-system |
| extension, add-on, content script | browser-extension |
| levels, players, physics, score | game |
| anything else | generic |

**Depth mode:** Quick (3 rounds, ~12 questions, a prototype), Standard (5 rounds, ~20,
default), Deep (8 rounds, ~32, something people will depend on or pay for).

**Lenses** (banks below); use only the active ones:

| Lens | Covers | Skip when |
|---|---|---|
| Product | who, why, success, non-goals, scope tiers, must-never rule | never |
| Feature | flows, edge cases, actors, acceptance criteria | never |
| Experience | feel, visuals, assets, motion, sound, words | nobody looks at it |
| Systems | exactness, source of truth, services, clocks, stack limits | trivially stateless |
| Operations | accounts, privacy, law, cost, monitoring, launch | never shipped to anyone |

Experience is **required** when the brief names a look, brand, character or game layer.

### Phase 1b: Research

Before round 1, run 3 to 6 searches: comparable products and what their users complain
about, how projects like this fail, and current facts about the user's stack (limits,
pricing, shutdowns). Verify again mid-interview whenever an answer rests on something
that changes. Label every fact **documented**, **widely reported** or **my judgment**,
and cite sources in `07-decisions.md`. Research supplies facts; you supply the
synthesis. Rules: **Research** below.

### Phase 2: Round

At most **4 questions**, from at least two lenses. **Rotate lenses:** every active lens
gets a question within the first two rounds; if one has had none by round 2, it gets a
slot in round 3 even over urgent follow-ups (Experience is the lens most often starved).

### Phase 3: Review

After every batch of answers, do all five:

1. **Clash check.** Compare with `state.json`. Name any conflict out loud and concretely.
   Never let one through. When the newer answer clearly implies the fix, apply it, log
   it as `ASSUMED` and say so; spend a question only when both readings are plausible.
2. **Cascade check.** Add the questions each answer opened (use the → arrows in the banks).
3. **Closure check.** Drop questions an answer made irrelevant.
4. **Stack check.** Test each decision against the limits of tools the user already
   named. Search when unsure.
5. **Coverage.** Update `state.json` (see **Spec output**) and the meter.

Report in three short blocks at most (clash, opened, closed), then the meter, then the
next round. Never narrate your reasoning.

### Phase 4: Gate

No spec while any **required** question is unanswered. Each must be `answered`,
`auto-decided` or `deferred`. Show the meter:

```
Product     ######--  6/8   2 open
Systems     ####----  4/8   1 clash
```

When the budget runs out, offer: auto-decide the rest, one more focused round, or switch
to Deep. When auto-deciding in bulk, **the must-never rule (P8) beats every pack
default**, and decisions are **sorted by stakes**: one-way and costly first, with
evidence, cheap ones below.

### Phase 5: Emit

Write `spec/` following **Spec output** below: `SUMMARY.md`, `00-brief`,
`01-scope` (with non-goals), `02-users-and-flows`, `03-data-model` (with invariants),
`04-features/` (acceptance criteria each), `05-architecture`, `06-experience`,
`07-decisions`, `08-risks`, `09-open-questions`, `10-build-plan`, `AGENTS.md`,
`state.json`. Quick mode folds `02`, `06`, `08` into `SUMMARY.md`; never fold `01` or
`07`.

Markers: `[NEEDS CLARIFICATION]` (none may remain), `[ASSUMED]`, `[DEFERRED]`,
`[UNVERIFIED]`.

**Writing is a check.** Gaps found while writing are decided if cheap (logged "found at
emit") or asked if costly or one-way. List them in `SUMMARY.md`. Before handing over,
verify: no open markers, every decision reference resolves, every invariant has an
acceptance check, the spec's own interface text obeys its own rules, and every formula
is tested with real numbers, including the edges (zero, maximum, the odd case).

### Phase 6: Amend

If `spec/state.json` exists, never start over. Ask only what changed, patch the affected
files, append superseded decisions with dates to `07-decisions.md`, report the diff.

## Question checklist

Every question passes all of these:

- **Plain language:** a first-year student understands it on one read; named people, concrete moments. If asked to rephrase, rephrase the whole batch.
- **Stakes inside:** the user learns what the choice decides and what changing it costs.
- **Anchored options:** tie jargon to a product they use (glassmorphism "like iOS Control Centre"; optimistic UI "like an Instagram like that shows instantly"; command palette "like VS Code's Cmd+K"; local-first "like Apple Notes working on a plane"; CRDT "like Google Docs merging edits").
- **Recommended first**, labelled `(Recommended)`. If the user accepts every recommendation two rounds running, make the next round's stakes blunter.
- **"Decide for me"** is always an option; when picked, decide, log with reason and reversibility, move on.
- **"Show me instead"** for taste questions (look, feel, voice): accept screenshots or links, extract palette (hex), shapes, density, mood, play it back, confirm, save as a moodboard.
- **Freeform answers outrank your options:** restate in one line, then run the Phase 3 checks.
- **Non-obvious first:** ask what they have not thought of, never what they have.
- **At most one feature suggestion per round**, with its cost.

**Two honesty checks:** if the must-never rule cannot be guaranteed by any software (forecasts are wrong sometimes, networks fail), say so and restate it as something the build can promise. If the success number can be decided by luck (one trip, one launch day), add a measure that needs sustained use.

**Five tests before asking:** could a stranger answer it without knowing the project (then it is generic, drop it)? Does the brief already answer it? Do both answers build the same thing (decide and log)? Does the user learn something by reading it? Would a good engineer just default it (default and log)?

**Banned as written:** "What's your tech stack?" (ask the requirement that constrains it), "Who is your target audience?" (ask what just happened when they open it the fifth time), "What features do you want?" (propose the v0 cut), "Should it be user-friendly / fast / secure / scalable?" (make them trade, or ask the user count that would please them and build for 10×), "Should we use microservices?" (default to one service), "What colour scheme?" (anchor to a feel or ask for references), "Any other requirements?" (name the gap yourself).

**Questions nobody asks, mine them:** first screen with no data; someone leaving or deleting their account mid-flow; who can undo what, for how long; two people acting at once; network gone and back; the largest realistic data per user; an outside service down, repriced or shut down (search: tutorials outlive services); who pays when the free tier runs out; the one thing that must never happen; what breaks after six months untouched; success as a number; what you will deliberately not build; who acts when the usual person cannot (no app, offline, left, deleted); who inherits an owner's powers; who pays whom when many owe many; where outside data (payment IDs, addresses) comes from and who sees it; upper bounds (overpay, negative amounts, double taps).

**Mechanics:** with a question tool (Claude Code, Cowork), use it: 4 questions × 4 options, so at most 3 real options plus "Decide for me". Without one, emit one block:

```
**Q1. <question with its stakes>**
  a) <option>: <anchor>  (recommended)
  b) <option>: <anchor>
  c) <option>: <anchor>
  d) Decide for me

Reply like: 1a 2c 3d 4b, or write freely.
```

Never more than 4 questions on screen unless the user asks for more. Report each review in three short blocks at most (clash, opened, closed), then the meter, then the round. Never narrate your reasoning.

## Research

- **Scan before round 1 (3 to 6 searches):** the 2 or 3 closest existing products and what their users complain about (complaints are unasked questions); how projects like this fail; current facts about the user's stack (limits, pricing, policies, shutdowns). Do it while composing round 1; never make the user wait.
- **Verify mid-interview** whenever a recommendation rests on something that changes. Check the defaults below first; search when an entry is missing, over a year old, or the project is unusual. Search every outside service a decision depends on for deprecation.
- **Label every fact:** documented (primary source), widely reported (no primary source), or my judgment. When sources disagree, say so.
- **Record** the URL in `07-decisions.md` and in `state.json`.
- **No web access:** use the defaults and your knowledge, say you could not verify, mark fast-moving claims `[UNVERIFIED]`.
- Anything legal: say you are not a lawyer, give the source, recommend checking.

## Defaults (reviewed 2026-09; verify anything over a year old)

Use these for recommendations and "Decide for me". Never present one as the only option.

- **Mobile:** React Native with Expo if JS/TS is known; Flutter for identical custom UI; Kotlin native if Android-only. Say so when it should just be a website. Native modules (offline database, Rive animation, Crashlytics, React Native Firebase) need an Expo development build, not Expo Go (documented).
- **Backend:** Postgres via Supabase for relational data (row-level security in the database); Firebase for realtime document data; SQLite for on-device only; one boring service, never microservices early. Supabase free tier: add custom SMTP before launch (built-in email sends 2 per hour, team only) and a daily keep-alive if usage is seasonal (projects pause after about a week of low activity) (documented). Cloud Functions for Firebase need the Blaze plan and a card (documented). Firebase JS SDK keeps only an in-memory Firestore cache on React Native (documented).
- **Auth:** use the backend's own auth; social login plus magic link, no passwords; Clerk for polished UI if paying is fine; never roll your own password storage.
- **State:** server is the source of truth for anything exact, money always; offline only if it is a real use case (about a third more work); last-write-wins with a visible warning before CRDTs.
- **Money:** Stripe for web; Razorpay or Cashfree plus UPI in India; store in-app purchase for digital goods in apps; do not move other people's money in v0 (record and deep-link instead). Integers in minor units; define rounding. A UPI app's returned status can be missing or faked: only people confirm payments (documented).
- **Hosting:** Vercel or Netlify free tiers only if non-commercial (Vercel Hobby counts even ads as commercial, documented); Railway, Render or Fly for real backends; big clouds only when these fail. Vercel Hobby functions stop at 5 minutes: split long work into background jobs (documented). Firebase Dynamic Links shut down 25 Aug 2025 (documented).
- **Assets:** Material Symbols, Phosphor or Lucide icons; built-in or one Google font; Lottie for loops; Rive for state-driven characters; stills with code motion for v0; a style reference sheet before AI-generated art, generated in layers if animation comes later.
- **Compliance (not legal advice):** Google Play requires account deletion in-app **and** via a web link; Apple requires in-app deletion (documented). India's DPDP Rules (notified 14 Nov 2025, 18-month phase-in) require clear consent notices, erasure within 90 days, and verifiable parental consent for under-18s (documented). Stores need a privacy policy, support contact and data-safety form.
- **AI features:** start with a hosted model and a 50-example test set; pin versions; the model suggests and a person confirms; treat model output as untrusted; run model-written code only in a sandbox; prompt injection and excessive agency are top risks (OWASP LLM Top 10 2025, documented). Search current model prices before estimating cost.
- **Default without asking, and log:** git on GitHub; secrets in env vars; UTC stored, local shown; UUIDs; soft deletes; defined empty and error states; analytics behind consent; one platform, language and region first; tests on money and data-destroying paths.
- **Never default, always ask:** who owns the data and what happens when someone leaves; whether it moves real money; anything public that users might expect private; minors, health, identity documents, location history; the one thing that must never happen.

## Spec output

Write `spec/`:

```
SUMMARY.md            one screen: what, for whom, v0, non-goals, must-never, readiness, decisions to review first, gaps found while writing, file index
00-brief.md           idea verbatim, corrected read-back, principles
01-scope.md           v0 / v1 / later tables with sources, non-goals with reasons, success number
02-users-and-flows.md the person in the moment; numbered flows with named people and failure branches
03-data-model.md      entities (field, type, rule; owner; lifecycle), invariants, derived values as exact pseudocode
04-features/<f>.md    tier and sources; behaviour; states (empty, loading, error, offline); edge cases; Given/When/Then acceptance checks
05-architecture.md    stack (layer, choice, why, source), what runs where, integrations and failure behaviour, scale, cost
06-experience.md      feel or moodboard, screens (shows, primary action, empty state), characters, asset delivery spec, motion, voice samples, accessibility
07-decisions.md       yours; assumed: review first (one-way and costly, with evidence); assumed: the rest; found while writing; superseded
08-risks.md           risk, likelihood, damage, mitigation, status (mark waved-off warnings "accepted by user")
09-open-questions.md  deferred and unverified, with when to revisit and owner
10-build-plan.md      ordered milestones: delivers, depends on, done when
AGENTS.md             rules for the build agent: never (the must-never rule, no relitigating decisions, no non-goals or v1 work), always (stop and ask when uncovered, test every invariant, build in order), principles
state.json            project, archetype, depth, phase, round, decisions (id, question, answer, status, source, reversibility), contradictions, research (finding, label, source), coverage per lens
```

Rules: every line is something a build agent could get wrong; no adjectives that specify nothing; behaviour in 01 to 04 and 06, technology only in 05 and 10; every requirement cites its decision (D for the user's, A for assumed, B for the brief's); numbers carry units; pseudocode only for exact rules, never source code; Quick mode folds 02, 06, 08 into SUMMARY; never fold 01 or 07.

**Update mode:** add an "Amendment <date>" section to `07-decisions.md`, extend rather than delete earlier decisions, list superseded ones with dates, and report the diff.

## Escape hatches

Honour these immediately:

- *"decide the rest for me"*: auto-decide everything open, log it, go to the gate.
- *"skip this lens"*: mark it `DEFERRED`, move on.
- *"go deeper on X"*: spend the next round on X.
- *"I don't know"*: treat as "Decide for me" and say what you picked.
- *"just build it"*: emit what exists, gaps clearly marked.

## Question banks

Stems, not scripts. Rewrite each as a plain scenario with stakes, a recommended option, and "Decide for me". *(req)* questions block the gate. → shows what an answer opens.

### Lens: Product

- **P1 the fifth open** *(req)*: Picture the person opening this for the fifth time, not the first. What just happened in their life that made them reach for it? → home screen content, notification triggers, retention hook
- **P2 the alternative today** *(req)*: What do these people use right now instead? If the honest answer is a WhatsApp group and a memory, say so, because beating a notes app is a different bar than beating an existing product. → import and migration questions, differentiation, the switching-cost problem
- **P3 the one thing** *(req)*: If the build gets cut to a single feature and everything else is dropped, which one survives? Everything that is not this is negotiable, and I will hold you to that later when scope starts growing. → v0 scope, build order, the entire 01-scope.md
- **P4 non-goals** *(req)*: Name two or three things this deliberately will not do, even though someone will ask for them. Written-down non-goals are how you say no in three months without relitigating the whole idea. → 01-scope.md non-goals, AGENTS.md constraints
- **P5 success as a number** *(req)*: What number, at what date, would make you call this a success? Not revenue necessarily. Twenty people still using it in month three is a real target; "people like it" is not, because you cannot tell whether you hit it. → analytics events, 10-build-plan.md milestones
- **P6 scale ceiling** *(req)*: What user count in year one would genuinely please you? I will design for roughly ten times that and no further. → every Systems-lens question, hosting cost, database choice
- **P7 scope tiers** *(req)*: Here is your idea split into v0, v1 and later. v0 is what one person can finish and put in front of a real user. → 01-scope.md, 10-build-plan.md
- **P8 the line that must not be crossed** *(req)*: What is the one thing that must never happen, even if it costs a feature? Wrong balances shown to users, a private note becoming visible, data lost on a reinstall. → AGENTS.md principles, 08-risks.md, testing priorities
- **P9 who else touches it**: Besides the main user, is there anyone else who sees or touches this? An admin, a moderator, a parent, someone who gets a read-only view. → RBAC questions, invites, 02-users-and-flows.md
- **P10 the abandonment moment**: Where do you think people will give up? First launch with an empty screen, the step where they have to invite someone, or the moment they have to enter data manually? → onboarding flow, empty states, import shortcuts
- **P11 timeline reality**: How many hours a week does this realistically get, and is there a date it has to exist by? A deadline changes what belongs in v0 more than any feature preference. → 10-build-plan.md, scope tier boundaries
- **P12 who maintains it**: If you stop touching this for six months, what should still be working when you come back? That decides whether we can depend on services that need babysitting or renewals. → hosting choice, dependency risk, 08-risks.md
- **P13 public exposure**: Will anything here be visible to people outside the group that created it? Public profiles, shared links, anything indexable. → privacy questions, moderation, abuse handling, legal

### Lens: Feature

*The user imagines the happy path. Your value is everything else. For every feature they name, there are three states they have not pictured: empty, broken, and abusive. Ask about those, not about the happy path.*

- **F1 the core loop** *(req)*: Walk me through the single most common thing a user does, from opening the app to being done. I will turn this into the primary flow and everything else becomes secondary navigation, so if you name the wrong one the whole interface is built around the wrong thing. → navigation structure, home screen, 02-users-and-flows.md
- **F2 how the loop starts** *(req)*: What triggers that action? The user remembering on their own, a notification, someone else doing something, or a scheduled moment? → notification design, retention hook, background work
- **F3 the empty state** *(req)*: What does the screen show on first launch, before any data exists? This is the first thing every new user sees and it is the most commonly skipped screen in software. → onboarding, sample data seeding, 06-experience.md
- **F4 the undo question** *(req)*: When someone deletes or changes something, can they take it back, and for how long? "Undo for ten seconds" like Gmail is usually better than a confirmation dialog, because confirmations train people to tap yes without reading. → soft delete in data model, audit log, permission to undo someone else's action
- **F5 who can change what** *(req)*: If two people can see the same thing, can both edit it, or only the one who created it? And can anyone override that? → RBAC, audit trail, conflict handling
- **F6 simultaneous edits** *(req)*: What happens when two people change the same thing at the same second? Someone loses their edit silently, or someone gets told. → conflict UI, sync strategy, source of truth
- **F7 leaving** *(req)*: What happens when someone leaves, is removed, or deletes their account midway through? Does their data go with them, and what breaks for everyone else if it does? → soft delete, referential integrity, legal deletion obligations
- **F8 the biggest realistic user** *(req)*: What is the largest amount of data one user will realistically have? Twenty items or twenty thousand? The interface that works for twenty is unusable at twenty thousand, and the fix is search and pagination, decided now rather than after launch. → search, filtering, pagination, indexing, list performance
- **F9 failure in front of the user** *(req)*: The save fails because the network dropped. What does the user see, and what happens to what they typed? Losing typed input on a failed save is the fastest way to lose a user permanently. → offline strategy, retry queue, error copy
- **F10 the abuse path**: How would someone use this to annoy or harm another user? Adding charges that are not real, spamming invites, writing something nasty in a free-text field. → moderation, reporting, rate limiting, 08-risks.md
- **F11 acceptance criteria** *(req)*: For the one feature that must survive, how will you know it works? Give me the check you would actually run. Each feature file needs this or the build agent decides for itself when it is done. → 04-features/, testing strategy
- **F12 manual before automatic**: Is there a step here you could do by hand for the first fifty users instead of building it? Approving signups, importing data, sending the weekly summary. → v0 scope reduction, 10-build-plan.md
- **F13 notifications**: What is worth interrupting someone's day for? Every notification you add is a reason to uninstall if it is wrong. → push infrastructure, permission prompts, notification settings screen
- **F14 history and audit**: Does anyone ever need to see what changed and who changed it? If money, trust or shared responsibility is involved the answer is usually yes, and storing history is far cheaper to decide now than to reconstruct later. → event sourcing, data model, storage cost
- **F15 the actor check** *(req: when more than one kind of member exists)*: For every action (confirm, reject, pay, edit), check that every kind of participant can do it: no app, offline, left, deleted. When someone cannot, ask who acts for them. → delegation rules, admin powers, auto-behaviour that nobody can stop
- **F16 the owner leaves** *(req: when groups or shared spaces have an owner)*: If the person who created the group deletes their account, who takes over their powers? Nobody usually thinks of this until a group is stuck with settings no one can change. → ownership transfer, admin actions
- **F17 every game number** *(req: when a game layer exists)*: Every mechanic needs concrete numbers before emit: thresholds, time windows, levels.

### Lens: Experience

- **E1 closest existing app** *(req)*: Which app does this feel closest to? Pick the vibe, not the features. This one answer sets colour, spacing, fonts and animation speed all at once, so it saves a dozen smaller questions. → colour, type, motion speed, copy tone. Answer E2 to E6 in its light.
- **E2 light, dark or both**: Light mode, dark mode, or both? Both is nearly free if we decide now and costly to retrofit, because every colour has to be picked twice. → colour tokens, asset variants (icons and art need to work on both)
- **E3 the money colours** *(req: when money or scores are shown)*: "You owe" and "you are owed" are usually red and green. About 1 in 12 men cannot tell those apart. Do we rely on colour alone, or add a second signal? → accessibility, icon set, the balance component design
- **E4 typeface**: One font for everything, or a special display font for headings and big numbers? A display font gives character (think the chunky numbers on a CRED card) but it is one more file to license and load. → font licensing, app size, the numbers design
- **E5 icons**: Where do the small icons come from? Drawing your own takes days; a free icon set takes minutes and stays consistent. → asset sourcing, licence file, style consistency
- **E6 the main screen layout** *(req)*: When the app opens, what fills the screen? The list of groups, your total balance, or the character? Whatever sits there is what people will think the app is. → navigation, home screen spec, 06-experience.md
- **E7 what the character is for** *(req: when a character exists)*: What is the character's job? To make paying back feel like a win, to nag people who owe, or just to make the app charming? → E8, E9, notification copy, 08-risks.md (social shame risk)
- **E8 what drives the character** *(req: when a character exists)*: What exactly makes it change? Total money owed, number of days a debt is old, or how many debts are still open? → data the app must track, the states the art must cover, fairness edge cases
- **E9 whose character is it** *(req: when a character exists)*: Is there one character per group that everyone shares, or one per person? A shared one creates team spirit. A personal one visible to the group creates public pressure on whoever owes the most. → privacy of balances, screen layout, number of art states
- **E10 how many looks** *(req: when a character exists)*: How many different states does the character need drawn? Every state is a separate piece of art, and animated states cost several times a still image. → asset list, animation tool choice, effort estimate
- **E11 who makes the art** *(req: when custom art exists)*: Who makes the custom art, like the character? You, an AI image tool, a friend or freelancer, or a free library? → licences, style consistency, timeline, 08-risks.md
- **E12 still or moving art** *(req: when a character exists)*: Does the character move? A still image costs nothing to show. A simple looping animation (like the Duolingo owl bobbing) needs an animation file format. → tooling, app size, build setup (Rive needs a development build)
- **E13 the store-facing assets** *(req: when publishing to a store)*: The store listing needs an app icon, a feature graphic and at least a few phone screenshots. These are the first thing strangers judge, and they usually get made in a panic the night before launch. → 10-build-plan.md, asset list
- **E14 the asset list** *(req)*: Before the gate, show the full asset list (icon, splash, empty-state art, character states, fonts, sounds, store graphics) with source, format, licence and owner; ask only "anything missing?". → 06-experience.md asset table
- **E15 celebration moments**: When something good happens, like a debt fully cleared, what does the app do? A small confetti burst and a buzz (like Google Pay's cashback scratch card) makes the moment feel like a reward. → motion spec, haptics, sound
- **E16 sound**: Any sounds? Most people keep their phone on silent, so sound can never carry meaning on its own, but a tiny sound on the big win adds a lot. → asset list, settings screen
- **E17 voice** *(req)*: How does the app talk? Read these three versions of the same message and pick. → all copy, notification text, error messages
- **E18 the hard messages**: How do we tell someone they owe money without it feeling like a bill collector? This one line gets seen more than any other text in a money app. → notifications, reminders, character dialogue

### Lens: Systems

*Find what must be exact and what may be slightly stale, then put everything exact on the server. Most technical mistakes in small projects come from treating the two the same.*

- **S1 what must be exact** *(req)*: Which numbers or states must never be wrong, even for a second? Money, stock left, votes, a seat that can only be booked once. → server-side logic, transactions, invariants in 03-data-model.md
- **S2 the source of truth** *(req: when data exists on more than one device)*: When a phone and the server disagree, which one is right? The answer decides whether the app can work offline and what the user sees while it is out of date. → offline behaviour, conflict handling, "last updated" labels
- **S3 who sees what** *(req: when more than one person uses it)*: Build a table of each kind of data by each kind of person (owner, member, stranger, admin), show it, and ask only what should be more private. → security rules, privacy text, O3
- **S4 outside services** *(req)*: Which outside services will this depend on (sign-in, payments, maps, AI, email, messaging)? For each one: what does the user see when it is down, and what happens if it raises prices or shuts down? → 05-architecture.md integrations table, 08-risks.md
- **S5 the stack check** *(req: when the user has named tools)*: List the tools the user named and search each for limits that collide with answers so far; raise every collision as a clash. → 05-architecture.md, A-decisions with evidence links
- **S6 clocks and time** *(req: when anything is scheduled, expires or counts days)*: Something happens after a waiting period: a reminder, an expiry, a streak. Whose clock counts? A phone's clock can be changed to skip ahead, and phones stop background work to save battery. → scheduled server jobs, time zones, timer accuracy
- **S7 live updates**: When Priya adds something, does Rahul need to see it appear on his screen instantly, or is it fine when he next opens or refreshes? → realtime listeners, cost, battery
- **S8 files and media**: Will people upload photos or files? Each one needs storage you pay for, a size limit, and a decision about who can open the link. → storage, size limits, link privacy, E-lens asset rules
- **S9 getting data in and out**: Can people bring their data from what they use today, and take it with them if they leave? An import path lowers the cost of switching to you; an export is often a legal right and builds trust. → file formats, P2 switching cost
- **S10 guessable links**: If someone gets a share link, can they change a number in it and see someone else's data? Links built from short or counting IDs can be guessed. → ID format, link expiry, security rules
- **S11 changing the data later**: When a later version changes how data is stored, what happens to people still on the old app? Old phones keep running old code for weeks. → migrations, forced update, API versioning
- **S12 AI features** *(req: when the product calls an AI model)*: When the AI gives a wrong or strange answer, what does the user see and who is responsible? Also: each call costs money and takes seconds. → cost per user, rate limits, loading states, 08-risks.md

### Lens: Operations

- **O1 how people sign in** *(req: when accounts exist)*: How do people sign in? Every password you store is a reset flow, a breach risk and a support email. → auth provider (Defaults), O2, OTP cost if phone
- **O2 deleting an account** *(req: when accounts exist and it ships to a store)*: How does someone delete their account and data? Both app stores require it: Google Play needs an in-app path **and** a web link that works after uninstalling; Apple needs it inside the app. → web deletion page, retention note in the privacy policy, F7 leaving rules
- **O3 personal data and consent** *(req)*: What personal data does this collect (names, phone numbers, contacts, location, payment IDs), and for what? Each item needs a stated purpose. → consent screen, privacy policy, data safety form on Play, O2
- **O4 under-18 users** *(req: when users could be minors)*: Could anyone using this be under 18? First-year college students can be 17. Under India's DPDP rules, processing a child's data needs verifiable parental consent, and store policies add their own rules for apps used by children. → age gate, consent flow, store content rating
- **O5 who pays to run it** *(req)*: What does this cost per month at your expected size, who pays, and what is the ceiling before you would shut something off? → 05-architecture.md cost section, budget alerts, 08-risks.md
- **O6 knowing it broke** *(req)*: How will you find out it is broken before your users tell you? Crash reports from the first build cost nothing and catch most problems. → crash tool choice, error alerts, O7
- **O7 where users report problems**: When something goes wrong, how does a user reach you? Stores require a support contact, and a "report a problem" button that attaches the app version saves hours. → support email, feedback screen
- **O8 backups** *(req: when data matters)*: If the database were wiped tomorrow, or a bad update corrupted it, what could you restore? Managed databases often do not back up by default on free plans. → backup schedule, restore test, cost
- **O9 abuse and limits**: What stops someone from spamming invites, creating thousands of accounts, or sending huge numbers of requests? → rate limits, security rules, F10
- **O10 the launch path** *(req: when it ships to anyone)*: How do the first real users get it, and what do you need ready that day? Stores need a privacy policy link, a support contact, a data safety or privacy form, and review time. → privacy policy page, store forms, 10-build-plan.md release milestone
- **O11 the ten events**: Which ten user actions do you want to count, to know whether the success number in P5 is being hit? Decide them before launch; you cannot measure the past. → analytics tool, consent (O3)
- **O12 keeping it alive**: What needs regular care even if you add nothing? Stores periodically require apps to target newer Android versions, keys and domains expire, and dependencies go stale. → maintenance checklist in 10-build-plan.md, P12

### Archetype: Web app

*A web app has no install step, which is its superpower and its weakness. Anyone can open it from a link in seconds, and anyone can close the tab just as fast, open it inside Instagram's cramped built-in browser, share a URL that should have been private, or arrive from Google on a page you never designed as a front door. Every one of those is a decision the user has not made yet.*

- **W1 how people arrive** *(req)*: How does a new person find this: searching Google, tapping a link a friend sent, or only after logging in to a tool they already use? → server-rendered pages vs app-style pages, link previews (W12), public pages
- **W2 phone or laptop first** *(req)*: Where will most people open it: a phone browser or a laptop? Designing for a laptop and shrinking it for phones rarely works; the reverse usually does. → layout, navigation pattern, touch targets, E6
- **W3 the in-app browser trap** *(req: when links are shared on social or chat apps)*: Links opened from WhatsApp, Instagram or LinkedIn often open inside that app's built-in browser, not Chrome. Google sign-in is blocked in many of those built-in browsers, and downloads and payments can break. → sign-in method (O1), link-landing page design
- **W4 installable and notifications**: Should people be able to add it to their home screen and get notifications like an app? On Android this works well. → service worker, offline caching, notification permission timing
- **W5 every screen a link**: Should every screen have its own URL, so the back button works and people can share exactly what they are looking at? → routing, link privacy (S10), what a logged-out person sees at that URL
- **W6 two tabs at once**: Priya has the app open in two tabs and edits in both. Or on her laptop and phone. Which change wins, and does the other tab update or go stale? → S2, S7 live updates, F6
- **W7 slow network budget** *(req)*: On an average phone on 4G, how many seconds may the first screen take? Every library, font and image adds to it, and people leave after about three seconds. → framework choice, image handling, font choice (E4), hosting region
- **W8 where it is hosted, and whether it earns money** *(req)*: Will this ever earn money: payments, ads, affiliate links, or someone paid to build it? Several free hosting tiers are for non-commercial use only; Vercel's free Hobby plan, for example, counts even ads as commercial. → hosting choice, O5 cost, the hosting defaults
- **W9 the domain and email**: Does it need its own web address, and will it send email (sign-in links, receipts, notifications)? Email from a new domain lands in spam unless the domain is set up for sending, and sign-in links in spam mean nobody can log in. → domain cost, email provider, sign-in method (O1)
- **W10 cookie and consent banner**: Do you use analytics or ads that track visitors? If so, visitors from some regions (the EU especially) must be asked first. → O3 consent, O11 analytics choice
- **W11 who runs the admin side**: Someone will need to fix a user's data, remove spam, or change content. Is that you poking at the database directly, or a proper admin screen? → admin roles (P9), audit log (F14), O9
- **W12 link previews**: When someone pastes a link into WhatsApp, what preview appears: a title, a picture, a description? A blank grey box gets ignored; a good preview card gets tapped. → preview images in the asset list (E14), page titles
- **W13 bots and spam**: Any public form (sign-up, contact, comments) attracts bots within days. Do we add a quiet check that blocks them? → O9, sign-up flow
- **W14 keyboard and screen readers**: Can the whole site be used with only a keyboard, and does it read properly with a screen reader? Cheap if built in from the start, expensive to retrofit, and legally required for some public or government-facing sites. → component choice, colour contrast (E3), testing

### Archetype: Mobile app

*A phone is not a small laptop. It loses signal, gets interrupted by calls, kills your app in the background without asking, requires permission before touching anything interesting, and puts a store review between you and your users. Every one of those is a decision the user has not made yet.*

- **M1 platform reality** *(req)*: Which phone do the people you described actually carry? If your first fifty users are one platform, shipping there properly beats shipping two badly, and cross-platform costs real polish on both. → framework choice, distribution, device testing
- **M2 the tunnel test** *(req)*: Someone opens this on a metro with no signal. What should work? Viewing what they already have is usually essential; creating something new that syncs later is where the work lives, and it is roughly a third more build either way. → local database, sync strategy, conflict handling, source of truth
- **M3 the money source of truth** *(req: when money or balances exist)*: Can the phone calculate a balance, or must the server always be the one that says what is owed? A client that can compute money is a client that can be confidently wrong about money in front of two people who disagree. → sync strategy, reconciliation, offline write rules
- **M4 the permission prompts** *(req)*: Which system permissions does this need, and when do you ask? Contacts, camera, notifications, location. Asking on first launch gets you denied; asking at the moment the feature is used roughly doubles acceptance. → onboarding flow, denied-permission fallbacks, settings screen
- **M5 the denied path** *(req: when any permission is requested)*: They tap "Don't Allow" on contacts. Does the feature still work? Every permission needs a manual fallback, or you have shipped a dead end for a meaningful share of users. → alternate flows, empty states, copy
- **M6 getting the second person in** *(req: when multi-user)*: How does the second person join? A share link, a code they type, a contact invite, a QR code across a table? This is the single highest-drop-off step in any multi-user phone product, and it deserves more thought than the features around it. → deep links, onboarding for invited users, what an invited user sees before signing up
- **M7 the invited user's first screen** *(req: when multi-user)*: Someone taps the invite link and does not have the app. What happens? Store page, then a blank app with no memory of the invite, is the default outcome and it loses most of them. → deep link infrastructure, web fallback, onboarding branches
- **M8 background behaviour**: Does anything need to happen while the app is closed? Both platforms are aggressive about killing background work, and anything you rely on happening reliably in the background needs a server doing it instead. → server-side scheduling, push infrastructure, battery considerations
- **M9 interruption**: Someone is halfway through entering something and a call comes in. When they come back, is their input still there? → local draft storage, state restoration
- **M10 one-handed reach**: Will people use this one-handed, walking, or at a table with both hands? The primary action belongs within thumb reach at the bottom if it is the former, and phone screens have grown past what a thumb covers. → navigation pattern, 06-experience.md
- **M11 distribution** *(req)*: How do the first fifty people install this? TestFlight and the Play internal track get you to real devices in days. → 10-build-plan.md, store assets, privacy policy requirement
- **M12 the update problem**: When you ship a change, old versions keep running on people's phones for weeks because they do not update. Does the server need to keep supporting them, and is there a version you can force off? → API versioning, forced-update mechanism, migration strategy
- **M13 device storage**: Photos, receipts, attachments? Those live on the device and in storage you pay for, and a phone that runs out of space deletes your cached data first without telling anyone. → storage cost, upload handling, compression, offline availability of media
- **M14 app store gatekeeping**: Does this sell anything, show user-generated content, or touch payments? Each one brings a store rule: digital goods must use the store's payment system and pay the cut, user content requires a reporting mechanism, and rejection costs a review cycle. → in-app purchase, moderation and reporting tools, review risk in 08-risks.md

### Archetype: CLI tool

*A command-line tool lives inside other people's machines and other people's scripts. It meets Windows paths, missing runtimes, shell history, pipes, CI servers with no human watching, and users who read none of the docs. Every one of those is a decision the user has not made yet.*

- **C1 who runs it** *(req)*: Who types this command: only you, other developers, or people who have never opened a terminal? If it is the last group, a command-line tool is probably the wrong shape; a small web page or desktop app would reach them better. → install method (C2), how friendly errors must be (C9)
- **C2 how it gets installed** *(req)*: How does someone install it? A package manager (npm, pip or pipx, Homebrew) is easy but requires them to already have Node or Python. → C3, release process, update path (C10)
- **C3 Windows** *(req: when others will use it)*: Must it work on Windows? That is where command-line tools break: different path separators, a different shell, different line endings, colour codes that print as junk. → path handling, test matrix, C2 builds
- **C4 people or scripts** *(req)*: Will people run it by hand, or will it also run inside scripts and automated pipelines with nobody watching? A tool that stops to ask a question hangs forever in a pipeline. → flag design, C5 output, C7 confirmations
- **C5 output for humans and machines** *(req)*: Will other programs read its output? Pretty tables for people and plain JSON for programs are two different outputs. → stdout versus stderr split, exit codes
- **C6 settings and secrets** *(req: when it needs a token or password)*: Where do settings and secrets (API keys, tokens) come from? A secret passed as a command argument is saved in shell history and visible to other users on the machine. → config location, O3 privacy, docs
- **C7 destructive actions** *(req: when it deletes, overwrites or sends anything)*: When it deletes, overwrites or sends something, does it show what it would do first? A `--dry-run` preview and a confirmation, skippable with `--yes` for scripts, stop the "I just wiped the wrong folder" moment. → C4, undo possibilities
- **C8 long jobs and Ctrl+C**: If a job takes minutes, what shows while it runs, and what happens when someone presses Ctrl+C halfway? A half-written file or half-sent batch is worse than no run. → temp files, idempotency (I5), state files
- **C9 errors that say what to do**: When it fails, does the message say what went wrong and what to do next? "Error: ENOENT" loses users; "Couldn't find config.yml. Run `tool init` to create one." keeps them. → error catalogue, docs
- **C10 updates**: How do users learn a new version exists, and what happens when you rename a flag? Scripts that use the old flag break silently. → changelog, release process
- **C11 phoning home**: Will it send any usage data back to you? Developers react strongly to this. → O3 privacy, docs
- **C12 no internet**: Does it need the internet? What happens on a plane or behind a company firewall? → S4 outside services, caching
- **C13 help**: Beyond `--help`, should it have examples, a man page, or tab-completion for commands? → docs, release assets

### Archetype: API service

*An API's users are other programs, written by people you will never meet, who will depend on every behaviour you ship, including the accidental ones. Anything you change later breaks someone. Every promise has to be decided on purpose.*

- **I1 who calls it** *(req)*: Who will call this: only your own app, other developers you do not know, or a few partner companies? A public API is a product with its own documentation, support and promises. → I2, I4, I9 docs, support load
- **I2 how callers prove who they are** *(req)*: How does a caller prove who they are? API keys are simple but leak into code and screenshots. Acting on behalf of a signed-in user needs a login flow (OAuth). → key management, O9, S3 visibility
- **I3 limits** *(req)*: How many requests may one caller make per minute, and what do they get when they exceed it? Without a limit, one buggy script can take the service down for everyone. → O9, cost (O5), I13
- **I4 changing it later** *(req: when anyone else calls it)*: When you need to change how something works, how do existing callers keep working? Removing a field silently breaks apps you cannot see. → changelog, deprecation notices, S11
- **I5 the double request** *(req: when requests create or charge anything)*: A caller's network drops right after sending "create order", so they send it again. Do they get two orders? A request ID that makes retries safe prevents duplicates, and payment systems depend on it. → storage for keys, retry guidance in docs
- **I6 errors** *(req)*: When something fails, does every error look the same, with a code a program can check and a message a person can read? → error catalogue, docs
- **I7 big lists**: When a list has ten thousand items, how does a caller page through it without missing or repeating items while new ones arrive? → F8 scale, indexes
- **I8 webhooks** *(req: when you notify callers of events)*: When you tell a caller something happened, what if their server is down? Do you retry, for how long, in what order, and how do they know the message really came from you and not an impostor? → queue, signing secrets, delivery dashboard
- **I9 documentation** *(req: when anyone else calls it)*: How do developers learn to use it? A machine-readable description (OpenAPI) gives you interactive docs and generated client code nearly for free. → docs hosting, example requests, I12
- **I10 speed and uptime promise**: How fast must responses be, and how much downtime is acceptable? A promise you cannot measure is not a promise. → O6 monitoring, hosting, caching
- **I11 input limits**: What is the largest request you accept, and what happens with nonsense input? An unlimited upload is an invitation to fill your disk. → O9, error format (I6)
- **I12 test mode**: Can a developer try it without touching real data or money? Separate test keys that hit a sandbox let them build safely. → environment setup, I2 key types
- **I13 expensive calls**: Does any endpoint cost you real money per call (an AI model, SMS, a paid data source)? A caller in a loop can run up your bill overnight. → O5, I3, S12

### Archetype: ML system

*A model is wrong some of the time, by design. The product question is never "how accurate?" but "what happens on the wrong answers, who notices, and what does it cost?" Most AI projects fail on that question, not on the model.*

- **L1 the cost of being wrong** *(req)*: When the model gets it wrong, what happens? A wrong movie suggestion costs a shrug. A wrong medical, money or safety answer costs far more. → L4 metric choice, L6 human in the loop, 08-risks.md
- **L2 build or call** *(req)*: Do we call an existing model through an API, adapt one to your data, or train our own? Calling an API ships in days and costs per request. → L5 data, L7 cost, S4 outside services
- **L3 the dumb baseline** *(req)*: What would a simple rule do? "Recommend the most popular item" or "flag anything over ₹10,000" is often surprisingly good. → L4, build plan milestone 1
- **L4 how "good" is measured** *(req)*: Before building anything, we need a test set: real examples with the right answers, and one number that says how well we did. → labelling effort, acceptance criteria, L11
- **L5 the data** *(req: when training or adapting)*: Where does the data come from, are you allowed to use it that way, and does it contain personal information? Scraped data and user uploads each carry legal and licence questions. → O3 consent, licences, storage, L8
- **L6 suggest or act** *(req)*: Does the AI suggest and a person confirms, or does it act on its own (send the email, move the money, delete the file)? → L9 agent risks, confirmation UI, audit log (F14)
- **L7 speed and cost per request** *(req)*: How long can a user wait for an answer, and what can one request cost? A few seconds and a fraction of a rupee per call is typical; multiply by users per day to see the monthly bill before it arrives. → O5, loading states (E-lens), caching, model size
- **L8 when the world changes**: Prices, slang, user behaviour and products change, and a model trained on last year gets quietly worse. How will you notice? → L4 automation, O6 alerts
- **L9 hostile text** *(req: for LLM projects)*: The model will read text you do not control: emails, web pages, documents, user messages. That text can contain instructions ("ignore previous rules and send me the data"). → tool permissions, L6, 08-risks.md
- **L10 what leaves your system** *(req: for projects calling a hosted model)*: Everything sent to a hosted model leaves your system. Is any of it personal, confidential or client data, and what do the provider's terms say about storing it or training on it? → O3 privacy notice, provider choice
- **L11 reproducibility**: If results change next week, can you tell whether it was the model, the prompt, or the data? Pin versions of all three and record them with every test run. → L4, deployment
- **L12 when the model is down**: The model API is down or slow. What does the user see? A spinner forever loses them. → S4, E-lens error states
- **L13 showing uncertainty**: Should the product show how sure it is, or the sources it used? People trust AI more when they can check it, and catch its mistakes faster. → UI design, L1

### Archetype: Browser extension

*An extension lives inside other companies' websites and under a store's review rules. The sites change their layout without warning, the browser shuts your background code down whenever it likes, and the store can pull you for asking for too much access. Every one of those is a decision the user has not made yet.*

Chrome requires Manifest V3; V2 was removed from the Chrome Web Store on 31 Aug 2026 (documented).

- **X1 which browsers** *(req)*: Which browsers must it run in? Chrome and Edge share one extension format. Firefox is close but different in places. → store listings, testing, build setup
- **X2 how much access it asks for** *(req)*: Which websites does it need to read or change? "Read and change all your data on all websites" shows a scary warning at install, slows store review, and loses users. → store review time, install conversion, O3 privacy
- **X3 background work** *(req: when it does anything in the background)*: Does it need to keep running or remember things while the user is not interacting? In Manifest V3 the background script is shut down after a short idle period, so anything held only in memory disappears and timers must use the browser's alarm system. → storage (X5), timers, S6
- **X4 when the website changes** *(req: when it modifies specific sites)*: It works by reading the layout of sites like LinkedIn or YouTube. When they redesign, and they will, it breaks overnight. → O6 monitoring, X8 update speed, support
- **X5 where its data lives** *(req)*: Where does it keep what it saves? On this computer only, synced to the user's other computers through the browser (small size limit), or on your own server (needs accounts and a privacy policy)? → accounts (X11), O3, S2
- **X6 store rules** *(req)*: The Chrome Web Store requires a single clear purpose, a privacy disclosure for any data handled, and a privacy policy if any user data is collected. → O3, O10 launch, listing text
- **X7 where it appears** *(req)*: Where does the user see it: a small popup from the toolbar icon, a side panel that stays open, something added inside the web page itself, or only a settings page? → E-lens screens, X4 fragility (inside-page UI breaks most often)
- **X8 shipping fixes**: Every update goes through store review before users get it, which can take days. Manifest V3 also forbids loading code from your server, so logic cannot be changed remotely. → X4, release process
- **X9 accounts**: Does it need people to sign in? Many good extensions need no account at all. → O1, O2 deletion, X5
- **X10 money**: Will any part be paid? The Chrome Web Store has no built-in payments, so paid features need your own checkout and a way for the extension to check who has paid. → payments (Defaults), accounts, W8 commercial hosting

### Archetype: Game

*A game succeeds or fails on thirty seconds of play that someone wants to repeat. Everything else, including art, levels and features, is multiplied by that loop. Scope kills more games than bad ideas do, so the first milestone is always a small playable slice, not a big half-finished world.*

- **GA1 where it is played** *(req)*: Where will people play: a web browser (instant, no install), a phone, a PC through Steam or itch.io, or a console? → GA2 engine, GA8 controls, distribution
- **GA2 engine** *(req)*: Which engine? Godot is free forever with no royalties. Unity is free until the studio earns about $200,000 a year. Unreal takes 5% of revenue after the first $1 million (documented, 2026). → language, asset pipeline, export targets
- **GA3 the thirty-second loop** *(req)*: Describe what the player does over and over in thirty seconds. Jump, aim, match, build, answer? If this is not fun on grey boxes with no art, no amount of art will fix it. → vertical slice, GA13 scope, prototype milestone
- **GA4 why come back tomorrow** *(req)*: What brings a player back tomorrow: new levels, an unlocked item, a daily challenge, friends to beat, a story? → save data (GA6), GA12 leaderboards, notifications
- **GA5 alone or together** *(req)*: One player, taking turns with friends, or playing live at the same time? Live multiplayer is a different project: servers, lag, cheating and matchmaking. → servers, GA12 cheating, S2 source of truth, cost
- **GA6 saving** *(req)*: Where is progress saved? On the device only means a new phone starts from zero. Cloud saves need accounts. → O1 accounts, data model
- **GA7 learning to play**: How does a new player learn the controls: a tutorial level, hints as they go, or nothing? Most players will not read instructions. → level design, first-session flow
- **GA8 controls** *(req)*: Touch, keyboard and mouse, or a game controller? A game designed for a keyboard rarely feels good on a touchscreen. → UI layout, testing devices
- **GA9 performance target**: What is the weakest device it must run smoothly on? Budget phones heat up and drop frames quickly, and a stuttering game gets uninstalled. → art budget, effects, testing
- **GA10 art and sound** *(req)*: How many characters, backgrounds, animations and sounds does v0 need, and who makes them? Count them now; games routinely need ten times the art people expect. → asset delivery spec, licences, timeline
- **GA11 money**: How does it earn money, if at all? Paid up front, ads, or in-game purchases? Paid random rewards (loot boxes) are treated as gambling in some countries, and anything children play carries extra rules. → store rules, O4 minors, payments
- **GA12 leaderboards and cheating**: If scores are compared, can someone fake one? A score sent straight from the game can be edited in seconds. Checking it on a server, or only comparing with friends, keeps it honest. → server, S1 exactness, O9 abuse
- **GA13 the vertical slice** *(req)*: What is the smallest version that shows the whole game: one level, finished to the quality you want, start to end? → 10-build-plan.md milestone 1, GA10 asset count

### Archetype: Generic (any other medium)

First name the medium in one line and run 3 searches on its rules and failure modes. After the interview, write 3 to 6 "assume these" defaults for that medium. If the project is not software, say so and run only Product and Feature.

- **G1 where it runs** *(req)*: Where does it actually run: on the user's computer, on a server you pay for, on someone else's platform, on a device? → hosting, cost (O5), uptime
- **G2 who installs and updates it** *(req)*: How does a new user get it, and how does a fix reach people who already have it? A script someone downloaded once never gets your bug fixes. → distribution, auto-update, versioning (S11)
- **G3 what starts it** *(req)*: What makes it do something: a person typing a command, a schedule, a message arriving, a sensor, a file appearing? → scheduling (S6), monitoring (O6), F2
- **G4 what it is allowed to touch** *(req)*: What does it need permission to read or change: files, a chat server, an email account, someone's calendar? Ask for the least; platforms review and users judge broad permissions harshly. → permission scopes, O3 privacy, security
- **G5 the gatekeeper** *(req: when a platform hosts or distributes it)*: Who can take it down or block it: an app store, a bot platform's rules, an API's rate limits or terms? What are their rules for this kind of project? → policy compliance, rate limits, 08-risks.md
- **G6 when it fails, who notices** *(req)*: If it stops working at 3 a.m., who finds out, and how? Background things fail silently by default. → O6 alerts, logs, retries
- **G7 the physical world** *(req: when hardware is involved)*: What happens when power drops, the network is gone, or the device is moved? Hardware adds parts to buy, wear out and ship. → offline behaviour, bill of materials, safety
