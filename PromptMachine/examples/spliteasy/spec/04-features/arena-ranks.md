# Arena ranks and the debt monster

**Tier:** v0 (still images) · v1 (live animation) · **Sources:** D7 to D10, D12, D13, A25, A31, A32

## Behaviour
1. Every member, ghosts included, has a tier computed from `game_net` (formula in
   03-data-model.md): Emperor, King, Prince, Villager, Goblin, Monster, Dragon.
2. Goblin, Monster and Dragon also have an anger state (calm, annoyed, furious) from how
   long the member has been in debt.
3. Tiers and anger are visible to the whole group.
4. v0 motion: characters bob gently at rest, shake when anger rises, and play one
   transformation with confetti and a vibration when a member reaches Villager from a
   debt tier. No sound.
5. The group screen ("the Arena") shows every member's character, name and amount.

## States
- Whole group settled: every character is a Villager, with "All square" banner.

## Edge cases
- Rahul's settlement turns provisional and moves him from Monster to Goblin; Priya then
  rejects it: he goes back to Monster with no celebration replayed.
- The creator raises big-debt: tiers recompute; no celebration fires for tiers changed
  by a threshold edit.

## Acceptance criteria
- [ ] Given B = ₹500 and Rahul owes ₹1,200, then Rahul is Dragon.
- [ ] Given Rahul owes ₹400 and has been in debt 10 days, then he is Goblin, annoyed.
- [ ] Given Rahul pays everything and it becomes provisional, then his character plays the
      transformation once and becomes Villager.
- [ ] Given a ghost owes ₹600 with B = ₹500, then the ghost is shown as Monster with a
      "hasn't joined" tag.
