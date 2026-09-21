# Reminders and notifications

**Tier:** v0 · **Sources:** D7, D11, A14, A15, A16, A26

## Behaviour
1. One notification category, written in the monster's voice about the debt, never about
   the person:
   - an expense involving you was added, edited or deleted;
   - someone says they paid you;
   - a payment to you confirms tomorrow;
   - weekly reminder while you owe money (only if in debt for 7+ days).
2. Permission is requested after the user creates or joins their first group.
3. Ghost reminders are WhatsApp cards (F-6): character image, amount, group, claim link.

## Voice samples
- "Your ₹640 for Goa is getting hungry. Feed it?"
- "Rahul says he paid you ₹1,000. Did it land?"
- "This ₹200 confirms tomorrow unless you say it didn't arrive."

## Acceptance criteria
- [ ] Given notifications denied, then the app works fully and shows a dismissible banner.
- [ ] Given Rahul has owed money for 6 days, then no weekly reminder is sent; on day 7 one is.
- [ ] Given a WhatsApp card is generated, then it contains the character image, amount,
      group name and a working claim link.
- [ ] No notification text contains insults or compares members to each other.
