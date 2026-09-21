# Build plan

## M0: Foundations
**Delivers:** hosting, Supabase with row-level security denying everything by default,
custom SMTP, keep-alive job, membership feature.
**Done when:** membership acceptance criteria pass, including 30 sign-ups in an hour.

## M1: Log
**Delivers:** catalog, sky maths, quick log with offline queue, logbook, night mode,
iPhone home-screen prompt.
**Depends on:** M0
**Done when:** quick-log and logbook acceptance criteria pass on one Android and one
iPhone, including the airplane-mode test.

## M2: Tonight
**Delivers:** forecast fetch and cache, scoring, Tonight screen.
**Depends on:** M1 (sky maths)
**Done when:** tonight acceptance criteria pass; the word test finds no banned words.

## M3: Trips
**Delivers:** sites management, weekend ranking, WhatsApp summary, Monday snapshot.
**Depends on:** M2
**Done when:** trips acceptance criteria pass.

## M4: Season view and release
**Delivers:** season view, CSV export, first monthly backup, invite link posted to the
club.
**Depends on:** M1–M3
**Done when:** 10 members have logged at least once.
