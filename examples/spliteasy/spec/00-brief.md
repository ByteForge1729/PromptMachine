# Brief

## Original idea

SplitEasy: a gamified Android bill-splitting app for college students. Group expense
splitting, ghost members, offline/Firebase sync, multi-currency support, a ₹99 Pro
unlock, and a "debt monster" game layer with the visual identity "The Ledger and The
Arena". Built with Claude Code, Expo and EAS Build; published under the DormWorks Play
developer account. Priority: simplicity over feature richness.

## Read-back, as corrected

A friends group records shared expenses and pays each other back. SplitEasy never holds
money: paying opens GPay with the amount filled in. Ghost members are friends without
the app who can claim their profile when they install it. Each group has one currency.
Every member carries a visible rank from today's balance, from Emperor down to Dragon.
The monster reminds people about debts and celebrates when they are paid. Pro and ads
wait for v1.

## Principles

1. **Never show a wrong balance.** No feature, shortcut or animation may make any person
   see a balance that differs from the server's ledger. (D14)
2. **The ledger is honest, the game may be early.** Ranks may react to a payment before
   it is confirmed; the balance number never does. (D5)
3. **SplitEasy never touches money.** It records and links out to UPI. (D1)
4. **The monster blames the debt, never the person.** (A26)
5. **Simplicity over feature richness.** When in doubt, cut.
