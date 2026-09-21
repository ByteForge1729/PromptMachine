# Instructions for the build agent

You are building Skylog from the spec in this folder. The spec is the source of truth.

## Never
- Use the words "best", "go" or "will be clear" anywhere in the interface. (D9)
- Show a ranking from a forecast older than 6 hours or with fewer than 2 models. (A25)
- Lose or duplicate an observation. IDs are created on the phone; uploads are
  idempotent. (A4)
- Let anyone who is not a signed-in member read any data. Enforce it in row-level
  security, not only in the interface. (D3)
- Build anything under Non-goals, or v1 items.
- Relitigate a decision in 07-decisions.md. Stop and ask instead.

## Always
- Keep the app fully usable offline for logging.
- Keep night mode dim red; test it in a dark room.
- Write a test for every invariant in 03-data-model.md before the feature that could
  break it.
- Credit the forecast source wherever forecast data appears.
- Build milestones in the order of 10-build-plan.md.

## Principles
1. Never present a night as a sure thing.
2. A log written in the field is never lost or duplicated.
3. Usable in the dark with cold hands.
4. Members only.
5. The club's memory belongs to the club.
