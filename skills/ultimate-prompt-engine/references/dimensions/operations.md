# Operations lens

Active whenever real people other than the builder will use the project. Covers
accounts, privacy and law, money for running it, knowing when it breaks, and keeping it
alive. These are the questions that block a launch the week before it happens.

Same entry format as `product.md`. This lens touches law. Say plainly that you are not a
lawyer, give the facts you found with their source, and recommend checking anything that
could carry legal risk. Never skip a question here because it sounds boring.

---

### O1: how people sign in `[required, when accounts exist]`
**Ask:** How do people sign in? Every password you store is a reset flow, a breach risk
and a support email.
**Options:** Google sign-in (recommended for students) / phone number with OTP / email
magic link / no accounts at all
**Opens:** auth provider (defaults.md), O2, OTP cost if phone
**Note:** phone OTP costs money per SMS; say so.

### O2: deleting an account `[required, when accounts exist and it ships to a store]`
**Ask:** How does someone delete their account and data? Both app stores require it:
Google Play needs an in-app path **and** a web link that works after uninstalling; Apple
needs it inside the app. Also: what stays behind, like their name on shared records?
**Options:** delete personal data, keep shared records under "Deleted user"
(recommended for shared apps) / delete everything they touched / anonymise only
**Opens:** web deletion page, retention note in the privacy policy, F7 leaving rules
**Evidence:** Google Play Console Help, "account deletion requirements" (documented);
Apple guideline 5.1.1(v) (documented).

### O3: personal data and consent `[required]`
**Ask:** What personal data does this collect (names, phone numbers, contacts,
location, payment IDs), and for what? Each item needs a stated purpose. India's DPDP Rules
were notified on 14 November 2025 with an 18-month phase-in; they require clear consent
notices and erasure on request within 90 days. Other countries have their own (GDPR in
the EU).
**Options:** list what the answers so far imply, and propose dropping anything without
a clear purpose
**Opens:** consent screen, privacy policy, data safety form on Play, O2
**Always:** data about people who never signed up (contacts, ghost members, tagged
friends) gets its own line: minimal, deletable on request.

### O4: under-18 users `[required, when users could be minors]`
**Ask:** Could anyone using this be under 18? First-year college students can be 17. Under
India's DPDP rules, processing a child's data needs verifiable parental consent, and store
policies add their own rules for apps used by children.
**Options:** 18+ only, stated at sign-up (recommended when plausible) / allow minors with
parental consent / not relevant
**Opens:** age gate, consent flow, store content rating

### O5: who pays to run it `[required]`
**Ask:** What does this cost per month at your expected size, who pays, and what is the
ceiling before you would shut something off? Several free tiers require a payment card
on file even when usage stays free.
**Options:** propose the monthly estimate and the first free-tier limit hit; recommend a
budget alert
**Opens:** 05-architecture.md cost section, budget alerts, 08-risks.md

### O6: knowing it broke `[required]`
**Ask:** How will you find out it is broken before your users tell you? Crash reports
from the first build cost nothing and catch most problems.
**Options:** crash reporting plus an alert on server errors (recommended) / crash
reporting only / users tell me
**Opens:** crash tool choice, error alerts, O7

### O7: where users report problems `[optional]`
**Ask:** When something goes wrong, how does a user reach you? Stores require a support
contact, and a "report a problem" button that attaches the app version saves hours.
**Options:** in-app "report a problem" to email (recommended) / a WhatsApp group / store
reviews only
**Opens:** support email, feedback screen

### O8: backups `[required, when data matters]`
**Ask:** If the database were wiped tomorrow, or a bad update corrupted it, what could you
restore? Managed databases often do not back up by default on free plans.
**Options:** scheduled automatic backups (recommended) / manual export weekly / accept
the risk
**Opens:** backup schedule, restore test, cost

### O9: abuse and limits `[optional]`
**Ask:** What stops someone from spamming invites, creating thousands of accounts, or
sending huge numbers of requests? A small cap on the obvious actions prevents most of it.
**Options:** simple limits on invites, sign-ups and writes (recommended) / none in v0
**Opens:** rate limits, security rules, F10

### O10: the launch path `[required, when it ships to anyone]`
**Ask:** How do the first real users get it, and what do you need ready that day? Stores
need a privacy policy link, a support contact, a data safety or privacy form, and review
time.
**Options:** closed testing with friends first (recommended) / straight to public /
web link only
**Opens:** privacy policy page, store forms, 10-build-plan.md release milestone

### O11: the ten events `[optional]`
**Ask:** Which ten user actions do you want to count, to know whether the success number
in P5 is being hit? Decide them before launch; you cannot measure the past.
**Options:** propose the ten from P5 and the core loop
**Opens:** analytics tool, consent (O3)

### O12: keeping it alive `[optional]`
**Ask:** What needs regular care even if you add nothing? Stores periodically require
apps to target newer Android versions, keys and domains expire, and dependencies go
stale. Who does it, and how often?
**Options:** a calendar reminder every 3 months (recommended) / whenever something breaks
**Opens:** maintenance checklist in 10-build-plan.md, P12

---

## Cascade rules

| If the answer is | Add these |
|---|---|
| accounts exist | O1, O2 in-app plus web deletion, O3 |
| data about non-users | O3 minimal-data line, deletion on request |
| users may be minors | O4, parental consent, store rating |
| paid services or a paid plan | O5 budget alert, card requirement, 08-risks.md |
| money-related data | O8 backups, O6 alerts, audit history (F14) |
| public store release | O2, O7 support contact, O10 privacy policy and forms, O12 |
