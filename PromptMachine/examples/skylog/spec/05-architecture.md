# Architecture

## Stack

| Layer | Choice | Why | Source |
|---|---|---|---|
| App | Installable website (PWA) with a service worker, phone-first | Offline logging; no app store | D5, A5 |
| Hosting | A free static host (Netlify, Cloudflare Pages or Vercel Hobby) | The club earns no money, so non-commercial free tiers apply (Vercel Hobby is non-commercial only) | A22 |
| Database and auth | Supabase free tier: Postgres with row-level security, email login links | Members-only rules enforced by the database itself | A1 |
| Login email | A free transactional email service connected as custom SMTP | Supabase's built-in email sends only 2 per hour and only to the project's own team (documented) | A2 |
| Keep-alive | A scheduled job that makes a small database request every day | Free Supabase projects pause after about a week without activity, which the monsoon would cause (documented) | A3 |
| Forecast | Open-Meteo, three models, fetched by the phone | Free for non-commercial use up to 10,000 calls a day, no key, credit required (documented) | A6 |
| Sky maths | A browser astronomy library (for example astronomy-engine) | Twilight, Moon, planets and alt/az on the phone, offline | A11, A14 |
| Catalog | Bundled file: Moon, planets, Messier 110, ~300 named stars, ~100 showpiece NGC/IC | Suggestions work offline | A11 |
| Offline store | IndexedDB on the phone, upload queue | D5 | A4 |

## Boundaries

**Phone:** catalog, sky maths, forecast fetch and cache, scoring, logging, upload queue.
**Database:** membership, observations, sites, snapshots; row-level security denies all
reads to non-members. **Scheduled jobs:** daily keep-alive, Monday ranking snapshot.

## Integrations

| Service | Used for | When it fails |
|---|---|---|
| Open-Meteo | Forecast | Last cached forecast with its age; ranking hidden after 6 h |
| Email service | Login links | "Resend" after 2 minutes; coordinator can re-invite |
| Supabase | Data | Logging keeps working offline; reading the club log needs a connection |

## Scale and cost

Designed for about 100 members. Everything runs on free tiers while the club earns no
money. If the club ever charges for anything through the app, the hosting and forecast
terms change (non-commercial only).
