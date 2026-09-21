# Research

Load in Phase 1b, and whenever an answer depends on a fact that can change.

The reference packs are a floor, not a ceiling. They make questions *correct*. Research
makes them *specific to this project*. Your own judgment turns both into
recommendations.

---

## The scan, once before round 1 (3 to 6 searches)

- **Comparable products.** Find the two or three closest existing products and what
  their users complain about in reviews, forums and store listings. Complaints are
  unasked questions in disguise. (First dry run: "everyone has to install Splitwise" was
  the top complaint, which proved the ghost-member feature; "reminding friends is
  awkward" gave the debt monster its real job.)
- **Domain pitfalls.** How projects like this fail: platform rules, payment or legal
  constraints, known technical traps.
- **Platform facts.** Anything the user's stated stack depends on that could have
  changed: store policies, SDK support, pricing, API limits, **shutdowns**.

Do the scan while composing round 1. Never make the user wait through research before
their first question.

## Verify mid-interview

Whenever a question or recommendation depends on something that changes (a price, a
policy, whether a library works on a platform, what a law requires):

1. Check `defaults.md` first.
2. Search when the entry is missing, older than a year, or the project is unusual.
3. For every outside service a decision depends on, search for deprecation or shutdown.

## Labels

Every fact you pass to the user carries one:

- **documented**: a primary source says so (official docs, policy page, press release);
- **widely reported**: many people say so, no primary source found;
- **my judgment**: your synthesis, stated as such.

Never pass off a forum post as fact. When sources disagree, say so ("3 or 4 a day,
sources disagree").

## Recording

- Cite the URL in `07-decisions.md` for any decision that rests on research, and in
  `state.json` under `research`.
- When research overturns or adds to a default, update `defaults.md` with the date so the
  next project starts smarter.

## No web access

Use `defaults.md` and your own knowledge, say that you could not verify, and mark every
fast-moving claim `[UNVERIFIED: claim]` in the spec.
