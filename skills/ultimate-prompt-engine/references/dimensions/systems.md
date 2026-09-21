# Systems lens

Active unless the project is trivially stateless. Covers where data lives, what must be
exact, what the project depends on, and what the chosen tools can and cannot do.

Same entry format as `product.md`. Keep the words plain: users answer these through
scenarios, never through architecture vocabulary. *"Two friends open the app at the same
moment. Must they see the same number?"* beats *"Do you need strong consistency?"*

**The governing rule of this lens:** find what must be *exact* and what may be *slightly
stale*, then put everything exact on the server. Most technical mistakes in small
projects come from treating the two the same.

---

### S1: what must be exact `[required]`
**Ask:** Which numbers or states must never be wrong, even for a second? Money, stock
left, votes, a seat that can only be booked once. Everything on this list is computed in
one place (the server) and never on a phone, and that decision shapes the whole build.
**Options:** propose the list from the brief and the P8 answer; let them add or remove
**Opens:** server-side logic, transactions, invariants in 03-data-model.md

### S2: the source of truth `[required, when data exists on more than one device]`
**Ask:** When a phone and the server disagree, which one is right? The answer decides
whether the app can work offline and what the user sees while it is out of date.
**Options:** server always wins, phone shows a labelled copy (recommended) / phone wins
and syncs up later / depends on the kind of data, decide per item
**Opens:** offline behaviour, conflict handling, "last updated" labels

### S3: who sees what `[required, when more than one person uses it]`
Not a question as written. Build a short visibility table from the answers so far:
each kind of data × each kind of person (owner, group member, stranger, admin). Show it
and ask only *"anything here that should be more private?"* Leaks almost always come
from a cell nobody filled in.
**Opens:** security rules, privacy text, O3

### S4: outside services `[required]`
**Ask:** Which outside services will this depend on (sign-in, payments, maps, AI, email,
messaging)? For each one: what does the user see when it is down, and what happens if it
raises prices or shuts down?
**Research, always:** search every named service for deprecation, shutdown or pricing
changes before recommending it. Tutorials outlive the services they teach. (Firebase
Dynamic Links shut down on 25 August 2025 and is still in many guides.)
**Options:** free text, then propose the failure behaviour for each service
**Opens:** 05-architecture.md integrations table, 08-risks.md

### S5: the stack check `[required, when the user has named tools]`
Not a question. List the tools the user already chose and search each for limits that
collide with answers so far: Expo Go cannot load native modules; some Firebase features
need the paid plan; a static-site host cannot run scheduled jobs. Raise every collision
as a clash in Phase 3. This check caught the largest decision in the first dry run.
**Opens:** 05-architecture.md, A-decisions with evidence links

### S6: clocks and time `[required, when anything is scheduled, expires or counts days]`
**Ask:** Something happens after a waiting period: a reminder, an expiry, a streak. Whose
clock counts? A phone's clock can be changed to skip ahead, and phones stop background
work to save battery.
**Options:** server clock, checked on a schedule (recommended) / the phone's clock / no
timed behaviour
**Opens:** scheduled server jobs, time zones, timer accuracy

### S7: live updates `[optional]`
**Ask:** When Priya adds something, does Rahul need to see it appear on his screen
instantly, or is it fine when he next opens or refreshes? Instant costs more to build and
run, and most apps do not need it everywhere.
**Options:** instant only where it matters (recommended) / instant everywhere / on open or
pull-to-refresh
**Opens:** realtime listeners, cost, battery

### S8: files and media `[optional]`
**Ask:** Will people upload photos or files? Each one needs storage you pay for, a size
limit, and a decision about who can open the link.
**Options:** none in v0 (recommended) / images only, compressed / any file
**Opens:** storage, size limits, link privacy, E-lens asset rules

### S9: getting data in and out `[optional]`
**Ask:** Can people bring their data from what they use today, and take it with them if
they leave? An import path lowers the cost of switching to you; an export is often a
legal right and builds trust.
**Options:** export only, as a simple file (recommended) / import from the main
competitor too / neither in v0
**Opens:** file formats, P2 switching cost

### S10: guessable links `[optional, when anything is shared by link]`
**Ask:** If someone gets a share link, can they change a number in it and see someone
else's data? Links built from short or counting IDs can be guessed.
**Options:** long random IDs and expiring links (recommended) / links never grant access
without sign-in
**Opens:** ID format, link expiry, security rules

### S11: changing the data later `[optional]`
**Ask:** When a later version changes how data is stored, what happens to people still on
the old app? Old phones keep running old code for weeks.
**Options:** support old versions for a while (recommended) / force an update screen /
ignore, tiny user base
**Opens:** migrations, forced update, API versioning

### S12: AI features `[required, when the product calls an AI model]`
**Ask:** When the AI gives a wrong or strange answer, what does the user see and who is
responsible? Also: each call costs money and takes seconds. Who pays, and what shows
while it thinks?
**Options:** AI suggests, the user confirms (recommended) / AI acts on its own / AI only
for low-stakes extras
**Opens:** cost per user, rate limits, loading states, 08-risks.md

---

## Cascade rules

| If the answer is | Add these |
|---|---|
| anything must be exact | server-side computation, invariants with tests, O8 backups |
| offline allowed | S2, labelled stale data, queued writes, conflict rules |
| timers or expiry | S6, one scheduled job, time zones |
| outside services | S4 failure behaviour, deprecation search, cost ceilings in O5 |
| sharing by link | S10, link expiry, what a stranger sees |
| AI features | S12, cost per user, prompt data privacy in O3 |
| user-named tools | S5 stack check against every later answer |
