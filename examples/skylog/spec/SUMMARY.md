# Skylog: spec (Quick mode)

**What:** A members-only website for a college astronomy club: a logbook that works with
no signal, plus a forecast that ranks upcoming campus nights and dark-site weekends
without ever promising a clear sky.
**For:** A member at 8 pm deciding whether to carry the telescope out, and a coordinator
choosing a trip weekend.
**v0 contains:** invite-link membership, 3-tap offline logging, club logbook with notes,
Tonight ranking, Trip-weekend ranking, monsoon season view, CSV export.
**Not building:** star map, astrophotography, public showcase, trip sign-ups or costs,
native app.
**Must never happen:** the app presents a cloudy night as a good one.

## Readiness

```
Product     ########  8/8
Feature     ########  10/10
Experience  ########  12/12
Systems     ########  12/12
Operations  ########  12/12
```
Decisions: 12 yours · 29 assumed (5 found while writing this spec) · 2 deferred · 2 unverified

## Review these first

| # | Decision | Why it matters |
|---|---|---|
| A2 | Custom SMTP for login emails | Supabase's built-in email sends 2 per hour, only to the project team. **Without it, nobody in the club can log in.** |
| A3 | Daily keep-alive request | Free Supabase projects pause after about a week of low activity. **The monsoon would switch the app off.** |
| A4 | Observation IDs made on the phone, uploads stored once | The only way field logs are never lost or doubled |
| A5 | Prompt iPhone users to add to the home screen | Safari can delete a website's saved data after 7 days without a visit |

## Found while writing the spec

| # | Gap |
|---|---|
| A2 | Login emails would not have been delivered at club scale |
| A3 | The monsoon would have paused the database |
| A15 | Your success measure could not be checked, because trips are chosen on WhatsApp. The app now saves its weekend ranking every Monday |
| A27 | The idea had no name. Working title: Skylog |
| A28 | Testing the scoring maths showed a clear full-Moon night would be labelled "0 of 3 forecasts agree it's mostly clear". Agreement now ignores the Moon, which is shown separately |

## Users and flows

**Ananya at 8 pm on campus.** Opens Tonight → sees the next 5 nights ranked, "2 of 3
forecasts agree it's mostly clear" for tonight, Moon and planets times → carries the
telescope out.

**Karan at Rajmachi, 11 pm, no signal.** Taps Log → types "or" → Orion Nebula is first →
taps it → taps 4 → saved on the phone. Six logs later the bus reaches signal and they
upload on their own. Next morning he adds notes.

**A coordinator on Monday.** Opens Trips → Rajmachi on the new-Moon weekend ranks first →
"Share to WhatsApp" → posts it to the club group.

**July.** Tonight is replaced by the season view: "Usually clear from October", last
season's best logs, what opens next.

## Experience

- **Day:** clean observer's notebook: off-white, simple type, generous spacing. (A7,
  placeholder until you send references)
- **Night:** red on black from sunset, manual toggle, nothing bright on screen.
- **Screens:** Tonight, Trips, Log (a button on every screen), Club log, My log, Members
  (coordinators), Sites (coordinators).
- **Words:** "more promising / less promising", "2 of 3 forecasts agree", "fetched 3 h
  ago". Never "best", "go", "will be clear".
- **Accessibility:** ratings shown as numbers as well as stars; type scales with the
  phone's text size.

## Risks

| Risk | Likelihood | Damage | Mitigation | Status |
|---|---|---|---|---|
| Forecasts are wrong and a trip is cloudy | high | Trust drops | Rank only, show agreement, never promise (D9) | mitigated |
| Success measure fails through bad luck | medium | App judged unfairly | Secondary measure (A16) | mitigated |
| Offline logs lost on iPhone | medium | Club memory lost | Home-screen prompt, upload banner (A5) | mitigated |
| Free-tier limits or terms change | medium | App breaks or costs money | Keep-alive, monthly export, non-commercial use only | open |
| Invite link forwarded outside the club | medium | Strangers read logs | Coordinators reset link, remove members | mitigated |
| Nobody logs, because typing is still a chore | medium | Logbook stays empty | 3-tap flow tested in the dark before release | open |

## Files

| File | Answers |
|---|---|
| [00-brief.md](00-brief.md) | The idea and the principles |
| [01-scope.md](01-scope.md) | v0, v1, non-goals, success |
| [03-data-model.md](03-data-model.md) | What is stored, invariants, the scoring maths |
| [04-features/](04-features/) | Six features with acceptance checks |
| [05-architecture.md](05-architecture.md) | Stack, phone versus server, cost |
| [07-decisions.md](07-decisions.md) | Every decision and why |
| [09-open-questions.md](09-open-questions.md) | Deferred and unverified items |
| [10-build-plan.md](10-build-plan.md) | Milestones in order |
| [AGENTS.md](AGENTS.md) | Rules for the coding agent |
