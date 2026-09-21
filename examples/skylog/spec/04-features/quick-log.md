# Quick log

**Tier:** v0 · **Sources:** D2, D5, D12, A4, A5, A7, A11, A12

## Behaviour
1. One "Log" button on every screen.
2. Typing two letters shows suggestions from the bundled catalog, with objects currently
   above the horizon at the nearest site listed first. Tap one. (D12)
3. Tap a 1–5 rating. Saved. Target: under 10 seconds, 3 taps after typing.
4. Site defaults to the nearest known site by phone location; one tap to change.
5. Not in the catalog: the typed text is saved as `object_text`.
6. Works identically with no signal: the log is saved on the phone and uploaded
   automatically when a connection returns. (D5)
7. Uploads are safe to retry: the server stores each observation ID once. (A4)
8. A banner shows "3 logs waiting to upload" until done.
9. iPhone users who have not added the app to their home screen see a one-time prompt to
   do so, because Safari may delete a site's saved data after 7 days without a visit;
   home-screen web apps are exempt. (A5)

## States
- **Night:** red on black from sunset at the site, manual toggle available. (A7)
- **Upload failed repeatedly:** banner turns amber, "Tap to retry", logs stay on the phone.

## Acceptance criteria
- [ ] Given airplane mode, when 6 observations are logged and the app is closed and
      reopened, then all 6 are still listed as waiting.
- [ ] Given connectivity returns, then all 6 appear on another member's phone within
      30 seconds, and none appear twice even if the upload is interrupted and retried.
- [ ] Given it is 11 pm on campus, when typing "or", then Orion Nebula appears first.
- [ ] Given night mode, then no screen element is brighter than dim red.
