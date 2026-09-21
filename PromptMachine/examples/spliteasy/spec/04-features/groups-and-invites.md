# Groups and invites

**Tier:** v0 · **Sources:** D2, D3, D10, A13, A31, A34, A37, A38

## Behaviour
1. Any signed-in user can create a group: name and currency (default INR).
2. The creator is the only person who can change the group's "big debt" amount (default
   ₹500). Every change posts to the group: "Priya changed the big-debt amount to ₹2,000".
3. Currency can change only while the group has no expenses.
4. Invite links are App Links. Installed app: opens the group. Not installed: a web page
   on the project's hosting with a Play Store button and a 6-character join code.
5. A member may leave only when their balance is exactly ₹0 and they have no open
   settlements. Otherwise: "Settle up first. You owe ₹340."

## States
- **Empty (no groups):** Villager character, "Create a group" button, "Have a code?" link.
  No sample data. (A5)
- **New group, no expenses:** member list with every character as Villager, one button
  "Add the first expense".
- **Offline:** creating a group is disabled: "Needs internet".

## Edge cases
- Two people tap the same invite at once: both join; the link is multi-use (unlike claim
  links).
- The creator deletes their account: the longest-standing member becomes creator.
  [ASSUMED: A13 extension, found at emit, cheap]

## Acceptance criteria
- [ ] Given a group with one expense, when the creator opens settings, then currency is
      shown but not editable.
- [ ] Given Rahul (not creator), when he opens group settings, then the big-debt amount is
      read-only.
- [ ] Given the creator changes big-debt to ₹2,000, when any member opens the group, then
      a history entry shows the old and new amounts and every rank reflects the new value
      within 5 seconds.
- [ ] Given Rahul owes ₹340, when he taps "Leave group", then he sees "Settle up first.
      You owe ₹340." and remains a member.
- [ ] Given a phone without SplitEasy, when the invite link is opened, then a web page
      shows an install button and the join code.
