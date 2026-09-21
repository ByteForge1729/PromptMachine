# Membership

**Tier:** v0 · **Sources:** D3, D7, A2, A8, A9, A21, A24

## Behaviour
1. A coordinator copies the current join link and shares it in the club WhatsApp group.
2. Opening it: enter name and email → a login link is emailed → tapping it signs in.
   Sessions last 90 days on that phone. (A8)
3. If the join link is opened inside WhatsApp's or Instagram's built-in browser, the page
   first shows "Open in Chrome / Safari" so the login ends up in the real browser. (A24)
4. Coordinators can reset the join link, remove a member, and promote a member to
   coordinator.
5. A member can delete their account: name and email are erased; their logs remain as
   "Former member". (A21)

## States
- Join link reset: old link shows "This link has expired. Ask a coordinator."
- Login link email not arrived after 2 minutes: "Resend" button, limited to 3 per hour.

## Acceptance criteria
- [ ] Given a reset join link, when the old link is opened, then joining is refused.
- [ ] Given a visitor who is not signed in, when they request any observation, site or member through the database API directly, then nothing is returned.
- [ ] Given a removed member, when they open the app, then they are signed out and see
      no data.
- [ ] Given 30 new members join within one hour, then all 30 receive login emails.
      (Tests A2.)
- [ ] Given the join link opened inside WhatsApp's browser, then the "Open in browser"
      prompt appears before the email step.
