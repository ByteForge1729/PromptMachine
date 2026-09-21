# Archetype: API service

Load when the brief mentions an API, endpoints, a backend others connect to, an
integration, webhooks, or "a service that other apps call".

**The governing rule of this archetype:** an API's users are other programs, written by
people you will never meet, who will depend on every behaviour you ship, including the
accidental ones. Anything you change later breaks someone. Every promise has to be
decided on purpose.

Question IDs use the prefix `I` (interface).

---

### I1: who calls it `[required]`
**Ask:** Who will call this: only your own app, other developers you do not know, or a few
partner companies? A public API is a product with its own documentation, support and
promises. A private one can change whenever your app changes.
**Options:** only our own app (recommended for v0) / a few named partners / public developers
**Opens:** I2, I4, I9 docs, support load

### I2: how callers prove who they are `[required]`
**Ask:** How does a caller prove who they are? API keys are simple but leak into code and
screenshots. Acting on behalf of a signed-in user needs a login flow (OAuth).
**Options:** your app's normal sign-in token (own app only) / API keys that can be revoked
and rotated (recommended for partners) / OAuth for acting on behalf of users
**Opens:** key management, O9, S3 visibility

### I3: limits `[required]`
**Ask:** How many requests may one caller make per minute, and what do they get when they
exceed it? Without a limit, one buggy script can take the service down for everyone.
**Options:** per-key limits with a clear "slow down" response (recommended) / a global limit
only / none in v0
**Opens:** O9, cost (O5), I13

### I4: changing it later `[required, when anyone else calls it]`
**Ask:** When you need to change how something works, how do existing callers keep
working? Removing a field silently breaks apps you cannot see.
**Options:** add fields freely, never remove; breaking changes get a new version with a
dated retirement of the old one (recommended) / version from day one / no promise
**Opens:** changelog, deprecation notices, S11

### I5: the double request `[required, when requests create or charge anything]`
**Ask:** A caller's network drops right after sending "create order", so they send it
again. Do they get two orders? A request ID that makes retries safe prevents duplicates,
and payment systems depend on it.
**Options:** callers may send an idempotency key on create requests (recommended) /
duplicates detected by content / accept duplicates
**Opens:** storage for keys, retry guidance in docs

### I6: errors `[required]`
**Ask:** When something fails, does every error look the same, with a code a program can
check and a message a person can read? Inconsistent errors force every caller to
special-case each endpoint.
**Options:** one error format everywhere with codes (recommended) / plain status codes only
**Opens:** error catalogue, docs

### I7: big lists `[optional]`
**Ask:** When a list has ten thousand items, how does a caller page through it without
missing or repeating items while new ones arrive?
**Options:** cursor-based pages (recommended) / page numbers / return everything (never
past a few hundred)
**Opens:** F8 scale, indexes

### I8: webhooks `[required, when you notify callers of events]`
**Ask:** When you tell a caller something happened, what if their server is down? Do you
retry, for how long, in what order, and how do they know the message really came from
you and not an impostor?
**Options:** retries with backoff for a day, signed messages, an event log they can
re-fetch (recommended) / retry a few times / fire and forget
**Opens:** queue, signing secrets, delivery dashboard

### I9: documentation `[required, when anyone else calls it]`
**Ask:** How do developers learn to use it? A machine-readable description (OpenAPI) gives
you interactive docs and generated client code nearly for free.
**Options:** OpenAPI spec plus examples for every endpoint (recommended) / a written guide
/ read the code
**Opens:** docs hosting, example requests, I12

### I10: speed and uptime promise `[optional]`
**Ask:** How fast must responses be, and how much downtime is acceptable? A promise you
cannot measure is not a promise.
**Options:** internal target only, measured (recommended for v0) / published promise (SLA)
/ none
**Opens:** O6 monitoring, hosting, caching

### I11: input limits `[optional]`
**Ask:** What is the largest request you accept, and what happens with nonsense input? An
unlimited upload is an invitation to fill your disk.
**Options:** size limits and strict validation on every field (recommended) / validate
only critical fields
**Opens:** O9, error format (I6)

### I12: test mode `[optional, when others build on it]`
**Ask:** Can a developer try it without touching real data or money? Separate test keys
that hit a sandbox let them build safely.
**Options:** test and live keys, fully separate data (recommended) / one shared
environment
**Opens:** environment setup, I2 key types

### I13: expensive calls `[optional]`
**Ask:** Does any endpoint cost you real money per call (an AI model, SMS, a paid data
source)? A caller in a loop can run up your bill overnight.
**Options:** per-key limits and a spending cap on costly endpoints (recommended) / pass
the cost to callers through plans / no special handling
**Opens:** O5, I3, S12

---

## Defaults for this archetype

- JSON over HTTPS only.
- Timestamps in UTC, ISO 8601.
- Every response carries a request ID for debugging.
- Rate-limited responses say when to retry.
- Secrets never appear in URLs or logs.
- Health-check endpoint for monitoring.

## Cascade rules

| If the answer is | Add these |
|---|---|
| anyone else calls it | I2 keys, I4 versioning, I9 docs, I12 test mode |
| creates or charges | I5 idempotency, audit log (F14) |
| sends events | I8 webhooks, signing, retries |
| costly downstream calls | I13, I3, O5 budget alerts |
| public | O9 abuse, O7 support, O10 launch |
