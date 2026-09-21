# Archetype: browser extension

Load when the brief mentions a Chrome extension, a browser add-on, "something that runs
on every page", or modifying how websites look or behave.

**The governing rule of this archetype:** an extension lives inside other companies'
websites and under a store's review rules. The sites change their layout without
warning, the browser shuts your background code down whenever it likes, and the store
can pull you for asking for too much access. Every one of those is a decision the user
has not made yet.

Question IDs use the prefix `X`.

**Platform fact:** Chrome extensions must use Manifest V3. Manifest V2 was disabled for
all users on 24 July 2025 and removed from the Chrome Web Store on 31 August 2026
(Chrome for Developers, documented). Ignore any tutorial written for V2.

---

### X1: which browsers `[required]`
**Ask:** Which browsers must it run in? Chrome and Edge share one extension format. Firefox
is close but different in places. Safari requires a Mac, Xcode and the App Store.
**Options:** Chrome and Edge (recommended for v0) / plus Firefox / plus Safari
**Opens:** store listings, testing, build setup

### X2: how much access it asks for `[required]`
**Ask:** Which websites does it need to read or change? "Read and change all your data on
all websites" shows a scary warning at install, slows store review, and loses users.
Asking only when the user clicks the extension on a page shows no warning at all.
**Options:** only when clicked on the current page (recommended) / a named list of sites /
all sites
**Opens:** store review time, install conversion, O3 privacy

### X3: background work `[required, when it does anything in the background]`
**Ask:** Does it need to keep running or remember things while the user is not
interacting? In Manifest V3 the background script is shut down after a short idle
period, so anything held only in memory disappears and timers must use the browser's
alarm system.
**Options:** stateless, everything saved to storage (recommended) / periodic work via
alarms / needs a long-running process (reconsider the design)
**Opens:** storage (X5), timers, S6

### X4: when the website changes `[required, when it modifies specific sites]`
**Ask:** It works by reading the layout of sites like LinkedIn or YouTube. When they
redesign, and they will, it breaks overnight. How will you find out, and how fast can you
ship a fix given that store review takes time?
**Options:** automated daily check against the target pages, plus a friendly "this site
changed" message (recommended) / user reports / accept breakage
**Opens:** O6 monitoring, X8 update speed, support

### X5: where its data lives `[required]`
**Ask:** Where does it keep what it saves? On this computer only, synced to the user's
other computers through the browser (small size limit), or on your own server (needs
accounts and a privacy policy)?
**Options:** local only (recommended for v0) / browser sync for small settings / your
server
**Opens:** accounts (X11), O3, S2

### X6: store rules `[required]`
**Ask:** The Chrome Web Store requires a single clear purpose, a privacy disclosure for
any data handled, and a privacy policy if any user data is collected. Extensions that do
two unrelated things, or hide what they collect, get rejected or pulled.
**Options:** one purpose, minimal data, disclosed (recommended) / free text to discuss
**Opens:** O3, O10 launch, listing text

### X7: where it appears `[required]`
**Ask:** Where does the user see it: a small popup from the toolbar icon, a side panel that
stays open, something added inside the web page itself, or only a settings page?
**Options:** popup (recommended for quick actions) / side panel (for longer work) / inside
the page / settings only
**Opens:** E-lens screens, X4 fragility (inside-page UI breaks most often)

### X8: shipping fixes `[optional]`
**Ask:** Every update goes through store review before users get it, which can take days.
Manifest V3 also forbids loading code from your server, so logic cannot be changed
remotely. Is that acceptable for how often this will need fixes?
**Options:** yes, plan releases (recommended) / keep fast-changing rules as data on your
server (allowed; code is not) / reconsider
**Opens:** X4, release process

### X9: accounts `[optional]`
**Ask:** Does it need people to sign in? Many good extensions need no account at all.
**Options:** no account (recommended) / sign in with the browser's Google account / its own
accounts
**Opens:** O1, O2 deletion, X5

### X10: money `[optional]`
**Ask:** Will any part be paid? The Chrome Web Store has no built-in payments, so paid
features need your own checkout and a way for the extension to check who has paid.
**Options:** free (recommended for v0) / paid features via your own site / donations
**Opens:** payments (defaults.md), accounts, W8 commercial hosting

---

## Defaults for this archetype

- Manifest V3.
- Minimum permissions; `activeTab` over broad host access.
- No remotely hosted code.
- All state saved to storage, never only in memory.
- A visible "this page isn't supported" state.

## Cascade rules

| If the answer is | Add these |
|---|---|
| broad site access | X2 review delay, X6 disclosures, O3 |
| modifies specific sites | X4 monitoring, X8 fix speed |
| background work | X3 alarms and storage |
| stores data on a server | X9 accounts, O2 deletion, O3 privacy policy |
| paid features | X10, W8 |
