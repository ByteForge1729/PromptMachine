# Archetype: mobile app

Load when the brief mentions a phone, iOS, Android, an app store, offline use, or
anything a person carries around.

Read this alongside the active dimension files. The dimensions ask what the product
does; this asks what the phone forces on it.

**The governing rule of this archetype:** a phone is not a small laptop. It loses
signal, gets interrupted by calls, kills your app in the background without asking,
requires permission before touching anything interesting, and puts a store review
between you and your users. Every one of those is a decision the user has not made yet.

---

### M1: platform reality `[required]`
**Ask:** Which phone do the people you described actually carry? If your first fifty
users are one platform, shipping there properly beats shipping two badly, and
cross-platform costs real polish on both.
**Options:** Android only / iOS only / both from day one / decide for me
**Opens:** framework choice, distribution, device testing
**Note:** in India, student and campus products skew heavily Android. Say this rather
than assuming iOS parity matters.

### M2: the tunnel test `[required]`
**Ask:** Someone opens this on a metro with no signal. What should work? Viewing what
they already have is usually essential; creating something new that syncs later is where
the work lives, and it is roughly a third more build either way.
**Options:** read what is cached (recommended for v0) / read and create, queued for sync /
nothing works offline / decide for me
**Opens:** local database, sync strategy, conflict handling, source of truth
**Cascade:** anything beyond "read cached" makes every Systems-lens sync question required

### M3: the money source of truth `[required, when money or balances exist]`
**Ask:** Can the phone calculate a balance, or must the server always be the one that
says what is owed? A client that can compute money is a client that can be confidently
wrong about money in front of two people who disagree.
**Options:** server is always right (recommended) / phone calculates and server verifies /
phone is authoritative
**Skip if:** nothing numeric or financial
**Opens:** sync strategy, reconciliation, offline write rules

### M4: the permission prompts `[required]`
**Ask:** Which system permissions does this need, and when do you ask? Contacts, camera,
notifications, location. Asking on first launch gets you denied; asking at the moment the
feature is used roughly doubles acceptance. A denied permission is permanent for most
users, so the timing is a real design decision.
**Options:** ask in context at first use (recommended) / ask during onboarding with
explanation / avoid the permission entirely with a manual alternative
**Opens:** onboarding flow, denied-permission fallbacks, settings screen

### M5: the denied path `[required, when any permission is requested]`
**Ask:** They tap "Don't Allow" on contacts. Does the feature still work? Every permission
needs a manual fallback, or you have shipped a dead end for a meaningful share of users.
**Options:** manual entry fallback (recommended) / feature disabled with an explanation /
block the user until granted (never choose this)
**Opens:** alternate flows, empty states, copy

### M6: getting the second person in `[required, when multi-user]`
**Ask:** How does the second person join? A share link, a code they type, a contact
invite, a QR code across a table? This is the single highest-drop-off step in any
multi-user phone product, and it deserves more thought than the features around it.
**Options:** share link to WhatsApp (recommended in India) / join code / QR code in person /
contact-based invite
**Skip if:** single-user
**Opens:** deep links, onboarding for invited users, what an invited user sees before
signing up

### M7: the invited user's first screen `[required, when multi-user]`
**Ask:** Someone taps the invite link and does not have the app. What happens? Store
page, then a blank app with no memory of the invite, is the default outcome and it loses
most of them. Deferred deep linking preserves the context through the install.
**Options:** deferred deep link into the right group (recommended) / store page then manual
join code / web preview they can see without installing
**Skip if:** single-user
**Opens:** deep link infrastructure, web fallback, onboarding branches

### M8: background behaviour `[optional]`
**Ask:** Does anything need to happen while the app is closed? Both platforms are
aggressive about killing background work, and anything you rely on happening reliably
in the background needs a server doing it instead.
**Options:** nothing (recommended) / periodic sync / server-driven push that wakes the app
**Opens:** server-side scheduling, push infrastructure, battery considerations

### M9: interruption `[optional]`
**Ask:** Someone is halfway through entering something and a call comes in. When they come
back, is their input still there? Phones kill apps without warning, and losing a
half-filled form is a phone-specific failure that web products rarely face.
**Options:** draft saved locally and restored (recommended) / form cleared / block until
finished
**Opens:** local draft storage, state restoration

### M10: one-handed reach `[optional]`
**Ask:** Will people use this one-handed, walking, or at a table with both hands? The
primary action belongs within thumb reach at the bottom if it is the former, and phone
screens have grown past what a thumb covers.
**Options:** one-handed, bottom-anchored actions (recommended) / two-handed, layout is free
**Opens:** navigation pattern, 06-experience.md

### M11: distribution `[required]`
**Ask:** How do the first fifty people install this? TestFlight and the Play internal
track get you to real devices in days. A full store listing adds review time, screenshots,
a privacy declaration and a support contact, which is real work nobody budgets for.
**Options:** internal testing tracks only (recommended for v0) / full public store listing /
sideloaded APK for a small group
**Opens:** 10-build-plan.md, store assets, privacy policy requirement

### M12: the update problem `[optional]`
**Ask:** When you ship a change, old versions keep running on people's phones for weeks
because they do not update. Does the server need to keep supporting them, and is there a
version you can force off?
**Options:** support old versions for a period (recommended) / force update on breaking
changes / ignore, small user base
**Opens:** API versioning, forced-update mechanism, migration strategy

### M13: device storage `[optional]`
**Ask:** Photos, receipts, attachments? Those live on the device and in storage you pay
for, and a phone that runs out of space deletes your cached data first without telling
anyone.
**Options:** no attachments in v0 (recommended) / images, compressed, server-stored /
arbitrary files
**Opens:** storage cost, upload handling, compression, offline availability of media

### M14: app store gatekeeping `[optional]`
**Ask:** Does this sell anything, show user-generated content, or touch payments? Each one
brings a store rule: digital goods must use the store's payment system and pay the cut,
user content requires a reporting mechanism, and rejection costs a review cycle.
**Options:** none of these (recommended for v0) / sells something / user-generated content /
handles payments
**Opens:** in-app purchase, moderation and reporting tools, review risk in 08-risks.md

---

## Defaults for this archetype

Assume these, log as `ASSUMED`, do not spend questions on them:

- Portrait orientation only in v0.
- Minimum OS version covering roughly the last four years of devices.
- No tablet-specific layout until someone asks.
- Dark mode supported, because the platform gives it to you nearly free if the design
  uses tokens from the start.
- Crash reporting from the first build, because a crash you did not see did not get fixed.
- Analytics behind consent, off in development.

## Cascade rules

| If the answer is | Add these |
|---|---|
| offline creation is needed | local database, sync queue, conflict resolution, source of truth |
| any permission is requested | prompt timing, denied fallback, settings deep link |
| multi-user | invite flow, deferred deep links, what a non-installed invitee sees |
| attachments or photos | storage cost, compression, offline media, upload retry |
| public store listing | privacy policy, screenshots, support contact, review timeline |
| money or balances | server authority, reconciliation, audit trail, rounding rules |
| notifications | permission timing, settings screen, what happens when muted |
