# SplitEasy: spec

**What:** An Android app where friend groups split shared expenses, pay each other back
through GPay, and see everyone's balance as a rank in a game: people owed money wear
crowns, people who owe money turn into monsters.
**For:** A student just back from an outing where one friend paid, logging it before
everyone forgets.
**v0 contains:** groups, ghost members, expenses with equal split, server-computed
balances, GPay settle-up with confirm/reject, seven-level ranks with the debt monster
(still images), WhatsApp reminder cards, offline viewing.
**Not building:** holding money in-app, personal budgeting, receipt scanning, a web app,
Pro, ads.
**Must never happen:** two people seeing different balances for the same group, or any
balance that is wrong.

## Readiness

```
Product     ########  8/8
Feature     ########  10/10
Mobile      ########  8/8
Experience  ########  12/12
```
Decisions: 16 yours · 46 assumed (14 found while writing this spec, 5 added by amendment) · 3 deferred · 1 unverified

## Amended 2026-09-21

The Operations lens found five gaps: account deletion (Play requires it in-app and on the
web), privacy notice, backups, abuse limits, and removal requests from ghosts. Added as
A42–A46 with a new feature file. You chose no age check (D16), recorded as an accepted risk.

## Review these first

| # | Decision | Why it matters |
|---|---|---|
| A36 | **Firebase Blaze plan, which needs a payment card on the project** | Server-side balances (A2) need Cloud Functions, and Cloud Functions require Blaze. Usage stays inside the free quotas at your scale, but a card must be on file. **If you cannot add one, tell me: it changes 05-architecture.md** |
| A1 | Move from Expo Go to development builds now | Offline storage on disk, crash reports and v1 live animation all need it |
| A2 | Balances computed only on the server | Direct consequence of the must-never rule |
| A3 | Timers run on the server clock | A phone clock can be changed to skip ahead |
| A4 | Round to the paisa; every group sums to exactly ₹0 | Otherwise balances drift and the must-never rule breaks |
| A34 | Group currency locked once the first expense exists | Changing it later would silently change every balance |

## Found while writing the spec

The interview missed these. Each is decided and logged in 07-decisions.md; flip any.

| # | Gap |
|---|---|
| A28 | Nobody decided who pays whom. Settle-up now suggests the fewest payments |
| A29 | Nobody decided where UPI IDs come from. Each user adds theirs in their profile |
| A30 | A ghost cannot tap "Got it" or "Not paid", so the 30-day auto-confirm had nobody to stop it. The group creator acts for ghosts |
| A31 | No default money amounts for the seven ranks. Default "big debt" is ₹500 |
| A32 | No numbers for monster anger. Calm under 7 days, annoyed 7 to 20, furious 21+ |
| A33 | Partial payments were never discussed. Allowed |
| A34 | Could a group change currency? Locked after the first expense |
| A35 | Timers need a scheduler. One hourly job runs all of them |
| A36 | Server functions need the Blaze plan |
| A37 | Claim links had no expiry. Single-use, 14 days |
| A38 | Firebase Dynamic Links, the usual invite-link tool, shut down on 25 August 2025. v0 uses App Links plus a typed claim code |
| A39 | Can you tap "I paid" offline? Yes; the timers start when the server receives it |
| A40 | Nobody decided what happens if the group creator deletes their account. The longest-standing member takes over |
| A41 | Nothing stopped a payment larger than what was owed, or a double tap. Both blocked |

## Files

| File | Answers |
|---|---|
| [00-brief.md](00-brief.md) | The idea and the principles |
| [01-scope.md](01-scope.md) | What is in v0, v1, later, and never |
| [02-users-and-flows.md](02-users-and-flows.md) | Who uses it and every step they take |
| [03-data-model.md](03-data-model.md) | What is stored, the money maths, the rules that must always hold |
| [04-features/](04-features/) | One file per feature with acceptance checks (account-and-privacy added 2026-09-21) |
| [05-architecture.md](05-architecture.md) | Stack, phone versus server, cost |
| [06-experience.md](06-experience.md) | Look, screens, characters, asset delivery spec, voice |
| [07-decisions.md](07-decisions.md) | Every decision and why |
| [08-risks.md](08-risks.md) | What will bite you |
| [09-open-questions.md](09-open-questions.md) | Deferred and unverified items |
| [10-build-plan.md](10-build-plan.md) | Milestones in build order |
| [AGENTS.md](AGENTS.md) | Rules for the coding agent |
