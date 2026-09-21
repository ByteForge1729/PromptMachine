# Expenses

**Tier:** v0 · **Sources:** A4, A7, A12, A14, D15

## Behaviour
1. Fields: amount, description, paid by (default: me), split among (default: everyone),
   equal split only in v0.
2. Split uses the rounding rule in 03-data-model.md: shares always sum to the amount.
3. Save is possible offline. The expense is created on the phone with its own ID and
   uploads on reconnect.
4. Undo is offered for 10 seconds after save or delete.
5. Only the creator of an expense or the group creator can edit or delete it. Deletes are
   soft and appear in history.
6. Every member included in an expense is notified.

## States
- **Not synced:** grey clock icon and "not synced yet" until the server accepts it.
- **Rejected by server** (e.g. group deleted meanwhile): expense turns red, "Couldn't
  save: <reason>", with Retry and Discard.

## Edge cases
- Two members edit the same expense offline: the later edit wins; the earlier editor sees
  "Priya changed this after you" in history. (F6 default)
- ₹100 split among 3 with Priya paying: Priya's share ₹33.34, others ₹33.33.
- An expense in a group whose currency is THB shows ฿, never ₹.

## Acceptance criteria
- [ ] Given airplane mode, when an expense is saved, then it appears with "not synced yet"
      and appears on a second phone within 10 seconds of reconnecting.
- [ ] Given ₹100 split 3 ways paid by Priya, then shares are 3334, 3333, 3333 paise.
- [ ] Given Rahul did not create an expense and is not group creator, then edit and delete
      are hidden.
- [ ] Given a deleted expense, then the history shows who deleted it and when.
