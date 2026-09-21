# Architecture

## Stack

| Layer | Choice | Why | Source |
|---|---|---|---|
| App | Expo (React Native, TypeScript) with **development builds** via EAS | Keeps the current toolchain; dev builds allow native modules | A1 |
| Auth | Firebase Auth, Google sign-in only | Every student has a Google account; no passwords | A11 |
| Database | Cloud Firestore via React Native Firebase | Native SDK keeps an on-disk cache so balances survive an offline restart. The JS SDK only keeps an in-memory cache on React Native (Firebase issue #7947) | D15, A1 |
| Server logic | Cloud Functions for Firebase | Balances, settlement transitions, timers, notifications must run on the server | A2, A3 |
| Scheduler | One Cloud Scheduler job, hourly | Runs every due timer; the first three jobs per account are free | A35 |
| Push | Firebase Cloud Messaging | Same project, no extra vendor | A15 |
| Crashes | Crashlytics (native SDK) | Not available in the JS SDK | A1 |
| Min version | Remote Config `min_supported_version` | Force old builds to update | A18 |
| Links | Android App Links + a web fallback page on Firebase Hosting | Firebase Dynamic Links shut down on 25 Aug 2025 | A38 |
| Pay | UPI intent link: `upi://pay?pa=<id>&pn=<name>&am=<amount>&cu=INR&tn=<note>` | Opens the user's own UPI app; no payment licence | D1 |
| Share cards | Render a view to PNG on the phone, share via the system share sheet | Works offline, no server image rendering | D11 |
| Characters | Bundled PNGs, motion in app code | v0 still images | D13 |
| Backups | Firestore daily scheduled backup, 14-week retention | Recover money records | A44 |
| Deletion page | A page on Firebase Hosting where a user can request account deletion without the app | Play requirement | A42 |

## Boundaries

**Phone:** display, input, offline cache, queued writes for new expenses and "I paid",
share cards, UPI hand-off.

**Server only:** balance and tier computation, settlement status changes, all timers,
claim-token validation, threshold changes, history writes, notifications. Anything that
touches the must-never rule lives here.

**Security rules:** members may create expenses and settlement claims in their own
groups. Clients may never write balances, settlement status, history, or another group's
data. Receiver decisions go through a callable function that checks the caller is the
receiver (or the group creator for a ghost).

## Integrations

| Service | Used for | When it fails |
|---|---|---|
| UPI app (GPay, PhonePe, Paytm) | Moving money | User taps "I paid" manually; nothing depends on the UPI response |
| WhatsApp | Invites, claim links, ghost reminders | System share sheet offers other apps |
| Google sign-in | Accounts | Cannot sign in; app shows retry |

## Scale posture

Designed for a few thousand users (hundreds expected, × 10). First thing to break beyond
that: recomputing a whole group's balances on every change. Fine up to hundreds of members
per group; groups here have 2 to 20.

## Cost

Requires the **Blaze (pay-as-you-go) plan**, because Cloud Functions do (A36). Blaze needs
a payment card on the Firebase project; set a budget alert at ₹100/month.

Firestore free quota: 50,000 reads, 20,000 writes and 20,000 deletes per day, 1 GiB
stored. A 5-person group adding 10 expenses a day costs roughly 60 writes and a few
hundred reads, so about 100 active groups stay within the free quota.
[ASSUMED: estimate, my judgment]
