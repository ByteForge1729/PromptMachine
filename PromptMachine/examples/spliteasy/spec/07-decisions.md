# Decisions

Reversibility: **cheap** (an afternoon), **costly** (days, or a data migration),
**one-way** (effectively permanent once users have data).

## Yours

| # | Decision | Round |
|---|---|---|
| D1 | Paying back opens GPay with the amount filled in; SplitEasy never holds money | 0 |
| D2 | Ghost members can claim their profile later through a personal claim link | 0, 1 |
| D3 | One currency per group; Pay button hidden in non-INR groups | 0, 1 |
| D4 | Payer taps "I paid"; receiver can press "Not paid" until day 30; otherwise final | 1, 3, 4 |
| D5 | Rank reacts on day 3; the balance number stays "awaiting" until final | 4, gate |
| D6 | v0 = core + debt monster; Pro and ads in v1 | 1 |
| D7 | The monster reminds about debts and celebrates payments | 2 |
| D8 | Everyone has a visible rank from today's balances, seven levels | 2, 3, 4 |
| D9 | Size by amount owed, anger by age; ghosts ranked like everyone | 3 |
| D10 | Thresholds in rupees, set per group by the creator only, changes announced | 4, 5 |
| D11 | Ghosts reminded by a WhatsApp card with their character and claim link | 4 |
| D12 | You generate character art with AI from agreed concepts and supply the files | 5 |
| D13 | v0 still images with code-driven motion; live animation in v1 | 5 |
| D14 | **Must never happen: a wrong balance** | 5 |
| D15 | Offline: last known balance with its time; offline expenses marked "not synced" | gate |
| D16 | No age check; under-18 use accepted as a known risk | amend 2026-09-21 |

## Assumed: review first

| # | Decision | Why | Reversibility | Evidence |
|---|---|---|---|---|
| A36 | Firebase Blaze plan with a ₹100 budget alert | Cloud Functions require Blaze; A2 requires Cloud Functions. Needs a card on file | costly | [Firebase docs](https://firebase.google.com/docs/functions) (documented) |
| A1 | Development builds instead of Expo Go, from v0 | JS SDK has no disk cache on React Native; native SDK needs a dev build; also unlocks Crashlytics and Rive | cheap now, costly later | [firebase-js-sdk #7947](https://github.com/firebase/firebase-js-sdk/issues/7947), [Expo: Using Firebase](https://docs.expo.dev/guides/using-firebase/) (documented) |
| A2 | Balances computed only on the server | D14 | one-way | my judgment |
| A3 | All timers use the server clock | A phone clock can be changed | costly | my judgment |
| A4 | Integer paise; remainder to payer; groups sum to exactly 0 | D14 | one-way once data exists | my judgment |
| A34 | Currency locked once a group has an expense | Changing it would silently change every balance | one-way | found at emit |
| A5 | No sample data in empty groups | Fake expenses in a money app break D14; overrides the pack default | cheap | my judgment |

## Assumed: the rest

| # | Decision | Why | Reversibility |
|---|---|---|---|
| A6 | Home screen = your groups plus one big "Add expense" | Logging happens right after spending or never | cheap |
| A7 | Equal split by default, done in under 10 seconds | Covers most student expenses | cheap |
| A8 | Non-goals: no money held, no budgeting, no receipt scanning, no web app | Keeps v0 finishable | cheap |
| A9 | Success = 3 groups, ~15 people, still adding expenses in week 8 | Retention proves it | cheap |
| A10 | Designed for a few thousand users | Hundreds expected | costly |
| A11 | Google sign-in only | Every student has Gmail | cheap |
| A12 | Only an expense's creator or the group creator can edit or delete; 10 s undo; full history | Trust in shared money | costly |
| A13 | Leaving needs a zero balance; deleted accounts become "Deleted user" | Leaving must not change anyone's balance | costly |
| A14 | Everyone in an expense is notified | Stops fake expenses slipping in | cheap |
| A15 | One notification category in the monster's voice | Extra notifications get the app muted | cheap |
| A16 | Only notification permission, asked after the first group | Asked on launch, it gets denied | cheap |
| A17 | Play internal testing track under DormWorks for v0 | Real devices in days | cheap |
| A18 | Force-update screen from a server setting | Old versions must not show balances differently | costly |
| A19 | History paginated; search in v1 | A semester is hundreds of expenses | cheap |
| A20 | Placeholder look: playful but clean like Duolingo | Awaiting your screenshots | cheap |
| A21 | Light and dark, following the phone | Nearly free if decided now | costly later |
| A22 | Owe/owed = colour + arrow + words | ~1 in 12 men can't separate red and green | cheap |
| A23 | Built-in font, Phosphor icons | Free and consistent | cheap |
| A24 | Home cards show your character and net; group opens the Arena | The game is visible immediately | cheap |
| A25 | One celebration: debt cleared → transformation, confetti, vibration; no sound | One moment that earns its place | cheap |
| A26 | Monster speaks about the debt, never insults the person | Fun without real hurt | cheap |
| A27 | Store graphics deferred to v1 | Internal track only | cheap |

## Assumed: found while writing the spec

| # | Decision | Why | Reversibility |
|---|---|---|---|
| A28 | Settle-up suggests the fewest payments (largest debtor pays largest creditor) | Nobody decided who pays whom | cheap |
| A29 | Users add their own UPI ID in their profile; visible only through the Pay button | Nobody decided where UPI IDs come from | cheap |
| A30 | Group creator confirms or rejects on a ghost's behalf | A ghost cannot act, so auto-confirm had no brake | cheap |
| A31 | Default big-debt ₹500; Goblin < B, Monster ≥ B, Dragon ≥ 2B, mirrored for Prince, King, Emperor; Villager within ₹1 | Ranks need numbers | cheap |
| A32 | Anger: calm < 7 days, annoyed 7–20, furious 21+, counted from when the member went into debt | Anger needs numbers | cheap |
| A33 | Partial payments allowed | Real people pay in parts | cheap |
| A35 | One hourly server job runs every timer; timers accurate to within an hour | Uses one of three free scheduler jobs | cheap |
| A37 | Claim links: single-use, 14 days, reissuing invalidates the old one | Limits forwarded links | cheap |
| A38 | Invites via App Links + web fallback with a join code; install-referrer handoff in v1 | Firebase Dynamic Links shut down 25 Aug 2025 ([FAQ](https://firebase.google.com/support/dynamic-links-faq), documented) | cheap |
| A39 | "I paid" works offline; timers start when the server receives it | Payer may be offline after paying | cheap |
| A40 | If the group creator deletes their account, the longest-standing member becomes creator | Groups need an owner for thresholds and ghosts | cheap |
| A41 | A settlement cannot exceed what the payer owes that receiver; repeat taps within 60 s blocked | Prevents overpayment and double claims | cheap |

## Amendment 2026-09-21: Operations lens

Added after the skill gained its Operations lens, which found five gaps in this spec.
Nothing earlier was superseded; A13 is extended by A42.

| # | Decision | Why | Reversibility | Evidence |
|---|---|---|---|---|
| A42 | Account deletion inside the app **and** on a web page; personal data erased, shared records stay as "Deleted user" (extends A13) | Google Play requires both paths for apps with accounts | costly if skipped: listing rejected | [Play Console Help](https://support.google.com/googleplay/android-developer/answer/13327111?hl=en) (documented) |
| A43 | Privacy policy, consent notice at sign-up, Play data safety form | DPDP Rules 2025: clear consent notices, erasure within 90 days | cheap | [PIB, DPDP Rules](https://www.pib.gov.in/PressReleasePage.aspx?PRID=2190014&reg=3&lang=2) (documented) |
| A44 | Daily Firestore scheduled backup, kept 14 weeks | Money records must be recoverable; needs Blaze, which A36 already requires | cheap | [Firestore backups](https://firebase.google.com/docs/firestore/backups) (documented) |
| A45 | Abuse limits: 20 invites and 60 expenses per member per hour, 50 members per group | Stops spam invites and runaway scripts | cheap | my judgment |
| A46 | A ghost can ask to be removed: name replaced with "Removed person", amounts kept | Erasure for non-users without changing anyone's balance (D14) | cheap | my judgment |

## Superseded

| # | Was | Replaced by | Round |
|---|---|---|---|
| R1.confirm | Receiver must tap "Got it"; nothing auto-confirms | D4 | 3 |
| R2.noreply | Auto-confirm after 3 days, no way to reject | D4 | 3 |
| R0.pro | Pro = features + no ads, in v0 | D6 (moved to v1) | 1 |
