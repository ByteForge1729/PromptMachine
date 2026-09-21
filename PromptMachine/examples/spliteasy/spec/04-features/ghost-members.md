# Ghost members

**Tier:** v0 · **Sources:** D2, D9, D11, A30, A37, A46

## Behaviour
1. Any member can add a ghost by typing a name. Nothing else is stored about a ghost.
2. Ghosts appear in splits, balances and ranks exactly like members. (D9, ghost rank)
3. Any member can send a ghost a **claim link**: single-use, valid 14 days, WhatsApp
   share. Generating a new link invalidates the old one.
4. Claiming: the person signs in with Google, confirms "Are you Amit in 'Goa trip'?", and
   the ghost becomes their membership with full history. The group is notified.
5. Settlements to or from a ghost are always manual (no UPI ID). The group creator taps
   "Got it" or "Not paid" on the ghost's behalf. (A30)
6. If a ghost asks to be removed, the group creator replaces the name with "Removed person";
   amounts and history stay so no balance changes. (A46)

## States
- Ghost row shows the character and a "hasn't joined" tag.
- Claim link expired or already used: web page and app both say "Ask your group for a new
  link."

## Edge cases
- A user who is already a member of the group opens a claim link: blocked, "You're
  already in this group as Rahul."
- Ghost with a non-zero balance is removed: not allowed, same rule as leaving.

## Acceptance criteria
- [ ] Given a ghost Amit owing ₹500, when a claim link is used by a new user, then that
      user sees Amit's full history and owes ₹500.
- [ ] Given a claim link already used once, when it is opened again, then it is refused.
- [ ] Given a claim link created 15 days ago, when it is opened, then it is refused.
- [ ] Given Rahul marks "I paid" to ghost Amit, when Priya (creator) opens the group, then
      she sees "Got it" and "Not paid" for that settlement and Rahul does not.
- [ ] Given ghost Amit owing ₹500 is renamed to "Removed person", then every member's balance
      is unchanged.
