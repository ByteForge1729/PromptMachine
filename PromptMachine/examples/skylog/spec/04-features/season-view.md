# Season view

**Tier:** v0 · **Sources:** D10, A17

## Behaviour
1. Appears on Tonight when every campus night in the next 5 scores below 0.2 for 7 days
   running (in practice, the monsoon).
2. Shows: the club's historically clear months (built-in: "November to February are usually the clearest months"),
   the club's highest-rated logs from last season, and what will be visible when the
   season opens.
3. Disappears automatically when a night scores 0.2 or more.

## Acceptance criteria
- [ ] Given 7 consecutive days of all-low scores, then Season view replaces the list and
      the hourly numbers stay one tap away.
