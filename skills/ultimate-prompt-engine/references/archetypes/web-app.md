# Archetype: web app

Load when the brief mentions a website, a browser, a dashboard, SaaS, a portal, or
"a site where people can...".

Read alongside the active dimension files. The dimensions ask what the product does;
this asks what the browser forces on it.

**The governing rule of this archetype:** a web app has no install step, which is its
superpower and its weakness. Anyone can open it from a link in seconds, and anyone can
close the tab just as fast, open it inside Instagram's cramped built-in browser, share a
URL that should have been private, or arrive from Google on a page you never designed
as a front door. Every one of those is a decision the user has not made yet.

---

### W1: how people arrive `[required]`
**Ask:** How does a new person find this: searching Google, tapping a link a friend sent,
or only after logging in to a tool they already use? If Google must find it (like a
Zomato restaurant page), pages have to be readable before any code runs, which shapes
the whole build. If it lives behind a login (like a Notion workspace), that does not
matter at all.
**Options:** mostly behind a login (recommended for tools) / shared links / Google search
/ decide for me
**Opens:** server-rendered pages vs app-style pages, link previews (W12), public pages

### W2: phone or laptop first `[required]`
**Ask:** Where will most people open it: a phone browser or a laptop? Designing for a
laptop and shrinking it for phones rarely works; the reverse usually does. Most Indian
users will arrive on a phone.
**Options:** phone first, works on laptop (recommended) / laptop first, usable on phone /
laptop only (say so on phones)
**Opens:** layout, navigation pattern, touch targets, E6

### W3: the in-app browser trap `[required, when links are shared on social or chat apps]`
**Ask:** Links opened from WhatsApp, Instagram or LinkedIn often open inside that app's
built-in browser, not Chrome. Google sign-in is blocked in many of those built-in
browsers, and downloads and payments can break. Do we detect this and show an "Open in
Chrome" prompt?
**Options:** detect and prompt (recommended) / offer email sign-in as a fallback / accept it
**Opens:** sign-in method (O1), link-landing page design
**Evidence:** Google OAuth policy blocks sign-in from embedded web views (documented,
Google Identity docs).

### W4: installable and notifications `[optional]`
**Ask:** Should people be able to add it to their home screen and get notifications like an
app? On Android this works well. On iPhone, web notifications only work after the
person adds the site to their home screen by hand, which most never do.
**Options:** no, a normal website (recommended for v0) / installable (PWA) on Android,
email for iPhone users / build a real app instead (switch to `mobile-app.md`)
**Opens:** service worker, offline caching, notification permission timing
**Evidence:** iOS web push requires a home-screen web app, iOS 16.4+ (documented, WebKit).

### W5: every screen a link `[optional]`
**Ask:** Should every screen have its own URL, so the back button works and people can
share exactly what they are looking at? Worth it for almost everything; the exception is
a checkout or a wizard where jumping into the middle makes no sense.
**Options:** yes, every screen is a link (recommended) / only main pages / single screen app
**Opens:** routing, link privacy (S10), what a logged-out person sees at that URL

### W6: two tabs at once `[optional, when users edit data]`
**Ask:** Priya has the app open in two tabs and edits in both. Or on her laptop and phone.
Which change wins, and does the other tab update or go stale?
**Options:** other tabs refresh when data changes (recommended) / last save wins silently
(never for important data) / warn "this changed in another tab"
**Opens:** S2, S7 live updates, F6

### W7: slow network budget `[required]`
**Ask:** On an average phone on 4G, how many seconds may the first screen take? Every
library, font and image adds to it, and people leave after about three seconds. A number
now stops the build agent adding heavy things casually.
**Options:** under 2 seconds (recommended) / under 4 seconds / not a concern (internal tool)
**Opens:** framework choice, image handling, font choice (E4), hosting region

### W8: where it is hosted, and whether it earns money `[required]`
**Ask:** Will this ever earn money: payments, ads, affiliate links, or someone paid to build
it? Several free hosting tiers are for non-commercial use only; Vercel's free Hobby plan,
for example, counts even ads as commercial.
**Options:** strictly non-commercial (free tiers fine) / earns money now or later (plan a
paid tier or a host that allows it) / decide for me
**Opens:** hosting choice, O5 cost, defaults.md hosting table
**Evidence:** Vercel fair use guidelines, "Hobby teams are restricted to non-commercial
personal use only" (documented, 2026).

### W9: the domain and email `[optional]`
**Ask:** Does it need its own web address, and will it send email (sign-in links, receipts,
notifications)? Email from a new domain lands in spam unless the domain is set up for
sending, and sign-in links in spam mean nobody can log in.
**Options:** own domain plus an email-sending service set up properly (recommended if it
sends email) / free subdomain, no email / decide for me
**Opens:** domain cost, email provider, sign-in method (O1)

### W10: cookie and consent banner `[optional]`
**Ask:** Do you use analytics or ads that track visitors? If so, visitors from some regions
(the EU especially) must be asked first. If you only use cookies needed to stay logged in,
you usually do not need a banner at all.
**Options:** no tracking, no banner (recommended for v0) / privacy-friendly analytics
without cookies / full analytics with consent banner
**Opens:** O3 consent, O11 analytics choice

### W11: who runs the admin side `[optional]`
**Ask:** Someone will need to fix a user's data, remove spam, or change content. Is that you
poking at the database directly, or a proper admin screen? Admin screens are a whole
second app; skipping one is fine at first if you accept the risk of hand-editing live data.
**Options:** database console for v0, admin screen later (recommended) / simple admin
screen in v0 / content managed by a separate tool
**Opens:** admin roles (P9), audit log (F14), O9

### W12: link previews `[optional, when links get shared]`
**Ask:** When someone pastes a link into WhatsApp, what preview appears: a title, a
picture, a description? A blank grey box gets ignored; a good preview card gets tapped.
**Options:** one branded preview for every page (recommended) / a custom preview per page
(like a product image) / none
**Opens:** preview images in the asset list (E14), page titles

### W13: bots and spam `[optional, when anything accepts input from strangers]`
**Ask:** Any public form (sign-up, contact, comments) attracts bots within days. Do we add a
quiet check that blocks them?
**Options:** invisible bot check plus rate limits (recommended) / email verification only /
nothing in v0
**Opens:** O9, sign-up flow

### W14: keyboard and screen readers `[optional]`
**Ask:** Can the whole site be used with only a keyboard, and does it read properly with a
screen reader? Cheap if built in from the start, expensive to retrofit, and legally
required for some public or government-facing sites.
**Options:** meet the common standard (WCAG AA) from the start (recommended) / basic
care only / ignore in v0
**Opens:** component choice, colour contrast (E3), testing

---

## Defaults for this archetype

Assume these, log as `ASSUMED`, do not spend questions on them:

- Works on the latest two versions of Chrome, Safari, Firefox and Edge, plus Chrome on
  Android.
- Phone-first responsive layout.
- HTTPS everywhere.
- A designed 404 page and a designed error page.
- One page title and description per page.
- No tracking cookies unless W10 says otherwise.
- Sessions last 30 days on a personal device; a "log out everywhere" option exists.

## Cascade rules

| If the answer is | Add these |
|---|---|
| Google must find it | server-rendered public pages, W12 previews, page titles, sitemap |
| links shared on social or chat apps | W3 in-app browser handling, W12 previews |
| installable or notifications | W4 service worker, iPhone limits, permission timing |
| earns money in any way | W8 commercial hosting, O5 cost, payments (defaults.md) |
| sends email | W9 domain setup, sign-in link deliverability |
| public input | W13 bot checks, O9 limits, moderation (F10) |
| tracking or ads | W10 consent, O3 privacy |
| edits in multiple tabs or devices | W6, S7 live updates |
