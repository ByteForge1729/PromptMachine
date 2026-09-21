# Data model

IDs are UUIDs. Times are stored in UTC and shown in IST. A "night" is labelled by the
date it starts (the night of Saturday runs from Saturday sunset to Sunday sunrise). (A26)

## Entities

### Member
| Field | Type | Rule |
|---|---|---|
| id | uuid | |
| name | text | shown on logs |
| email | text | used only for login links; visible to coordinators only |
| role | enum: member, coordinator | coordinators manage sites, invites, members (A9) |
| removed_at | timestamp or null | removed members cannot sign in; their logs stay as "Former member" (A21) |

### Invite
One active join link at a time. A coordinator can reset it, which disables the old one.
(D7, A9)

### Site
| Field | Type | Rule |
|---|---|---|
| id | uuid | |
| name | text | "Campus", "Rajmachi" |
| latitude, longitude | decimal | |
| bortle | integer 1–9 | informational |
| kind | enum: campus, dark_site | campus appears in Tonight; dark sites in Trips (A10) |

At most 10 sites; coordinators only.

### Observation
| Field | Type | Rule |
|---|---|---|
| id | uuid | **created on the phone**, so offline logs have a stable identity (A4) |
| member_id | member | |
| site_id | site | the site nearest the phone's location, changeable |
| object_id | catalog id or null | from the bundled catalog (A11) |
| object_text | text or null | used only when the object is not in the catalog |
| observed_at | timestamp | set on the phone at logging time |
| rating | integer 1–5 | how good the view was |
| notes | text or null | usually added later |
| uploaded_at | timestamp or null | set by the server |
| deleted_at | timestamp or null | soft delete; coordinators can restore (A13) |

Exactly one of `object_id` and `object_text` is set.

### RankingSnapshot
Saved every Monday: the ranked list of the next four weekends per dark site, with the
scores. Needed to check the success measure later. (A15)

## Invariants

1. An observation created on a phone is stored on the server exactly once: never lost,
   never duplicated, however many times the upload is retried.
2. No one who is not a signed-in, non-removed member can read any observation, site or
   member name.
3. The words "best", "go", "will be clear" never appear in the interface.
4. No ranking is shown from a forecast more than 6 hours old, or with fewer than 2
   models available.
5. Every forecast view shows when it was fetched and credits the forecast source.

## Derived values

### Dark hours (A14)
Hours between the end and start of astronomical twilight (Sun more than 18° below the
horizon), computed on the phone for the site and date.

### Night score (A14)
For each forecast model `m` and each dark hour `h`:
```
clear(m, h) = cloud_cover(m, h) < 30%

campus night:  weight(h) = 1                       # the Moon is a target, not a problem
dark-site night: weight(h) = 1 - moon_illumination   if the Moon is above the horizon at h
                             1                        otherwise

score(m)   = Σ weight(h) × clear(m, h)  /  number of dark hours     # used for ranking
clarity(m) = Σ clear(m, h)              /  number of dark hours     # Moon ignored
score      = average of score(m) over available models
agreement  = number of models with clarity(m) ≥ 0.6
```
Nights are listed from highest to lowest `score`. Each shows `agreement` as "2 of 3
forecasts agree it's mostly clear", the Moon separately ("bright Moon until 2 am"), and
the hourly numbers one tap away. Agreement ignores the Moon on purpose: a clear night
under a full Moon is still clear, and saying otherwise would be false.
(Found while testing this formula at emit: using the Moon-weighted score for agreement
labelled a clear full-Moon night "0 of 3 agree it's mostly clear". A28.)

### Weekend score (trips)
Best of the Friday and Saturday night scores for that site. The trips list ranks every
(site, weekend) pair for the next four weekends.
