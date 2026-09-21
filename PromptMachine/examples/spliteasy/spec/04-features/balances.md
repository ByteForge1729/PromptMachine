# Balances

**Tier:** v0 · **Sources:** D5, D14, D15, A2, A4, A28

## Behaviour
1. Balances are computed only by the server after every expense or settlement change, in
   one transaction per group. Phones display them and never compute them.
2. Each member sees: their net ("You owe ₹640" / "You are owed ₹1,200"), money awaiting
   confirmation, and suggested payments ("Pay Priya ₹640").
3. Owe/owed is shown with colour, an arrow and words, never colour alone. (A22)
4. Offline, the last server balance is shown with "as of <time>".

## States
- **Settled:** "All square" with the Villager.
- **Awaiting:** "₹1,000 · you say paid, awaiting Priya".
- **Stale:** "as of 2 h ago" whenever the phone has not heard from the server in over
  1 minute.

## Acceptance criteria
- [ ] Given any sequence of expenses, edits, deletes and settlements, then the group's
      balances sum to exactly 0 paise. (Invariant 1; property-based test.)
- [ ] Given two phones on the same group, when both are online and idle for 5 seconds,
      then they show identical numbers.
- [ ] Given a client tries to write a balance document directly, then the server rejects
      it.
- [ ] Given airplane mode and an app restart, then the last balances still show, labelled
      with their time.
