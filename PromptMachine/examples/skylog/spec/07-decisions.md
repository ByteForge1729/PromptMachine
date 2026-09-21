# Decisions

Reversibility: **cheap** (an afternoon), **costly** (days or a data migration),
**one-way** (effectively permanent once data exists).

## Yours

| # | Decision | Round |
|---|---|---|
| D1 | Both jobs from day one: campus nights and trip weekends | 0 |
| D2 | Logging is a few taps, notes added later | 0 |
| D3 | Members only | 0 |
| D4 | Quick interview depth | 0 |
| D5 | Logs saved on the phone with no signal, uploaded later | 1 |
| D6 | Show the raw forecast | 1 |
| D7 | Join through an invite link from a coordinator | 1 |
| D8 | The app only ranks; trips are organised on WhatsApp | 2 |
| D9 | **Must never: present a cloudy night as a good one.** No "best", only a ranking with model agreement | 2, 3 |
| D10 | Season view in the cloudy months | 3 |
| D11 | Success: a trip chosen with the app turned out clear | 3 |
| D12 | Type 2 letters and pick a suggestion, visible objects first | 3 |

## Assumed: review first

| # | Decision | Why | Reversibility | Evidence |
|---|---|---|---|---|
| A2 | **Custom SMTP for login emails** | Supabase's built-in email sends 2 per hour, only to the project team. Without this, members cannot log in | cheap, but blocking | [Supabase SMTP docs](https://supabase.com/docs/guides/auth/auth-smtp) (documented) · found at emit |
| A3 | **Daily keep-alive request** | Free projects pause after about a week of low activity; July would pause the club's app | cheap | [Supabase pausing docs](https://supabase.com/docs/guides/platform/free-project-pausing) (documented) · found at emit |
| A4 | Observation IDs created on the phone; uploads stored once per ID | The only way to guarantee no lost or duplicated field logs | one-way once data exists | my judgment |
| A1 | Supabase free tier (Postgres, row-level security, email login) | Members-only enforced in the database; free | costly to move | my judgment |
| A5 | Prompt iPhone users to add the app to their home screen | Safari may delete a site's data after 7 days without a visit; home-screen apps are exempt | cheap | [WebKit tracking prevention](https://webkit.org/tracking-prevention/) (documented) |
| A6 | Open-Meteo, three models, credited on screen | Free for non-commercial use, no key | costly | [Open-Meteo](https://open-meteo.com/) (documented) |

## Assumed: the rest

| # | Decision | Why | Reversibility |
|---|---|---|---|
| A0 | Build order: membership, log, tonight, trips, season view | Logging needs members; forecasts need nothing else | cheap |
| A7 | Daytime look: clean observer's notebook; red on black from sunset | You delegated the look; readable logs; research says red mode is essential | cheap |
| A8 | Join: name + email, then a login link; 90-day sessions | No passwords; field use needs long sessions | cheap |
| A9 | Roles: member, coordinator; coordinators reset links, remove members, manage sites | Invite links get forwarded | cheap |
| A10 | Up to 10 sites, coordinators only; campus plus dark sites | Trips need named sites | cheap |
| A11 | Bundled catalog: Moon, planets, Messier, ~300 named stars, ~100 showpiece NGC/IC | Offline suggestions | cheap |
| A12 | Log fields: object, site, time, 1–5 rating, optional notes. No photos in v0 | Speed at the eyepiece | cheap |
| A13 | Members edit/delete their own logs; coordinators edit any and restore | Club memory is precious | cheap |
| A14 | Scoring: clear = under 30% cloud in dark hours; Moon discounts dark-site hours only | On campus the Moon is a target, at dark sites it is the enemy | cheap |
| A16 | Secondary success: 15 members log 5+ nights | One trip is mostly weather luck | cheap |
| A17 | Season view contents: usual clear months, last season's best logs, what opens next | Keeps the app alive in the monsoon | cheap |
| A18 | Non-goals: star map, astrophotography, public showcase, native app | Stay small | cheap |
| A19 | Coordinators can export all logs as CSV | Observers want export; club memory | cheap |
| A20 | Monthly CSV export by a coordinator as a backup | Free-tier backup availability not verified | cheap |
| A21 | Account deletion erases name and email; logs remain as "Former member" | Privacy law lets people erase personal data; the club keeps its record | costly |
| A22 | Free static hosting | Non-commercial project | cheap |
| A23 | Latest two versions of the major browsers; phone first | Archetype default | cheap |
| A24 | "Open in Chrome / Safari" prompt inside WhatsApp's browser | Logins inside in-app browsers stay trapped there | cheap |
| A25 | Forecasts older than 6 h or with fewer than 2 models: numbers shown, ranking hidden | D9 beats convenience | cheap |
| A26 | Times in IST; a night is named by the date it starts | Avoids "which night is Saturday?" | cheap |

## Assumed: found while writing the spec

| # | Decision | Why | Reversibility |
|---|---|---|---|
| A15 | Save the weekend ranking every Monday | Otherwise D11 cannot be checked, because trips are chosen on WhatsApp | cheap |
| A27 | Working title "Skylog" | The brief had no name | cheap |
| A28 | Agreement counts clear hours ignoring the Moon; the Moon is shown separately | Testing the formula showed a clear full-Moon night labelled "0 of 3 agree it's mostly clear" | cheap |

(A2 and A3 were also found at emit; they are listed above with the high-stakes items.)

## Superseded

| # | Was | Replaced by | Round |
|---|---|---|---|
| R2 "mark the best" | Highlight the best window and weekend | D9 (rank only) | 3 |
| R3 "type the name" | Full typing | D12 (2 letters + suggestions) | 3 |
