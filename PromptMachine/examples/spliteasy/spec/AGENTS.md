# Instructions for the build agent

You are building SplitEasy from the spec in this folder. The spec is the source of truth.

## Never
- Show a balance the server did not compute. Phones display balances; they never
  calculate them. (D14, A2)
- Use floating-point numbers for money. Integer minor units only. (A4)
- Trust a UPI app's returned status to change any money state. (D4)
- Use the phone's clock for any timer. (A3)
- Relitigate a decision in 07-decisions.md. If one looks wrong, stop and ask.
- Build anything under Non-goals in 01-scope.md, or any v1/Later item during v0.
- Write insulting or comparative text about a person in any notification or character
  line. (A26)

## Always
- Stop and ask when the spec does not cover a behaviour. Do not invent it.
- Write an automated test for every invariant in 03-data-model.md before the feature that
  could break it.
- Build milestones in the order of 10-build-plan.md.
- Cite the spec file and decision number in commit messages for behaviour changes,
  e.g. `settle-up: day-30 finalisation (D4, A35)`.
- Use development builds, not Expo Go. (A1)

## Principles
1. Never show a wrong balance.
2. The ledger is honest; the game may be early.
3. SplitEasy never touches money.
4. The monster blames the debt, never the person.
5. Simplicity over feature richness.
