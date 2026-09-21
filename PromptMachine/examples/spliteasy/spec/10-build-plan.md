# Build plan

Each milestone installs on a real phone and works on its own.

## M0: Foundations
**Delivers:** dev build via EAS, Firebase project on Blaze with a budget alert, Google
sign-in, Crashlytics, Remote Config minimum version, security rules that deny everything
by default, daily backups (A44), consent notice at sign-up (A43).
**Depends on:** nothing
**Done when:** a signed-in user sees an empty home screen on a physical Android phone;
a forced crash appears in Crashlytics.

## M1: Groups, members, ghosts
**Delivers:** groups-and-invites, ghost-members (without claim links yet), profile with
UPI ID.
**Depends on:** M0
**Done when:** groups-and-invites acceptance criteria pass.

## M2: Expenses and balances
**Delivers:** expenses, server balance computation, history, offline expense entry,
stale-balance label.
**Depends on:** M1
**Done when:** expenses and balances acceptance criteria pass, including the zero-sum
property test run over 10,000 random sequences.

## M3: Settle-up
**Delivers:** Pay button, "I paid", "Got it", "Not paid", hourly timer job, suggestions.
**Depends on:** M2
**Done when:** settle-up acceptance criteria pass; UPI tested on GPay, PhonePe and Paytm
and the result recorded in 09.

## M4: Arena
**Delivers:** tiers, anger, the Arena screen, still characters with code motion,
transformation celebration, big-debt setting.
**Depends on:** M2 (tiers), M3 (provisional state), your character files
**Done when:** arena-ranks acceptance criteria pass.

## M5: Reminders and claims
**Delivers:** push notifications, WhatsApp share cards, claim links with the web fallback.
**Depends on:** M1, M4
**Done when:** ghost-members and reminders acceptance criteria pass.

## M6: Release to friends
**Delivers:** internal testing track release under DormWorks, app icon and splash, account
deletion in the app and on a web page (A42), privacy policy and Play data safety form (A43),
abuse limits (A45).
**Depends on:** M0–M5
**Done when:** 3 groups are using it; week-8 success check scheduled.
