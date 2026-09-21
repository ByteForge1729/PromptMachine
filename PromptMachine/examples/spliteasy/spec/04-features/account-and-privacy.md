# Account and privacy

**Tier:** v0 · **Sources:** D16, A11, A13, A42, A43, A45

## Behaviour
1. Sign-up shows a short consent notice: what is stored (name, Google account email, UPI ID
   if added, groups, expenses), why, and how to delete it. Link to the privacy policy.
2. Delete account: in Profile, and on a web page that works without the app. Personal data
   (name, email, UPI ID) is erased; expenses and settlements stay under "Deleted user" so no
   balance changes. Target: immediately; legal maximum 90 days.
3. Limits per member: 20 invites and 60 new expenses per hour; groups up to 50 members.
4. No age check (D16).

## Acceptance criteria
- [ ] Given account deletion from the web page, then the name, email and UPI ID are gone and
      every group's balances are unchanged.
- [ ] Given a member sends a 21st invite within an hour, then it is refused with "Try again
      later".
- [ ] Given sign-up, then the consent notice is shown before the account is created.
