# Settle-up

**Tier:** v0 · **Sources:** D1, D3, D4, D5, A3, A15, A29, A30, A33, A35, A39

## Behaviour
1. Pay button (INR groups, receiver has a UPI ID): opens the UPI app chooser with
   receiver ID, name, amount and note "SplitEasy: <group>" filled in.
2. The status the UPI app returns is ignored for money. Only the payer's "I paid" and the
   receiver's decision count.
3. "I paid" creates a settlement in `claimed`. Amount editable downwards (partial).
4. Receiver actions: "Got it" (final now) or "Not paid" (rejected, any time before final).
5. Server timers from `received_at`: day 3 → provisional (game only), day 29 → reminder to
   receiver, day 30 → final. One hourly server job processes all due timers, so timings
   are accurate to within an hour.
6. Non-INR groups and ghosts: no Pay button; "I paid" only.

## States
- Pay button disabled offline: "Needs internet".
- Receiver has no UPI ID: button becomes "Ask Priya for her UPI ID".

## Edge cases
- Rahul taps "I paid" twice by mistake: the second tap is blocked for 60 seconds with
  "You just marked ₹1,000 as paid."
- Priya rejects on day 20: Rahul's monster regrows immediately and both are notified.
- Settlement larger than what Rahul owes Priya: blocked.

## Acceptance criteria
- [ ] Given a settlement claimed on day 0, when the server clock reaches day 3, then the
      payer's tier updates and the displayed balance number does not change.
- [ ] Given a provisional settlement, when the receiver taps "Not paid" on day 20, then
      both the tier and the "awaiting" amount revert within 5 seconds.
- [ ] Given no action, when day 30 passes, then the settlement is final and the balance
      number updates.
- [ ] Given the phone's clock is set 5 days ahead, then no timer fires early.
- [ ] Given a THB group, then no Pay button is shown.
- [ ] Given GPay returns "SUCCESS", then nothing is marked paid without the payer tapping
      "I paid".
