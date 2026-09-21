# Logbook

**Tier:** v0 · **Sources:** D2, D3, A13, A19

## Behaviour
1. Club log: every member's observations, newest night first, grouped by night and site.
2. My log: only mine. Here I add notes to earlier observations.
3. Filter by object, member, site, or month.
4. A member can edit or delete their own observations; coordinators can edit any and
   restore deleted ones. Deletes are soft.
5. Coordinators can download all observations as CSV. (A19)

## States
- Empty club log: "No observations yet. The first one is yours." plus the Log button.

## Acceptance criteria
- [ ] Given a member adds a note the morning after, then the observation shows the note
      and keeps its original observed time.
- [ ] Given a coordinator exports CSV, then every non-deleted observation appears once
      with member name, object, site, time (IST), rating and notes.
- [ ] Given a deleted observation, then only coordinators see it, marked deleted.
