# Archetype: website

Load when people come mainly to **look**: a portfolio, a landing page, a studio, brand or
event site, an online magazine piece. When they come to **do** something with an account
or their own data, load `web-app.md` instead.

Read alongside the Experience lens, which is always active here and goes first.

**The governing rule of this archetype:** nobody needs this page. A stranger gives it a
few seconds, and in those seconds it either has a point of view or it looks like every
other page. The two usual ways to fail are opposite: a page built from the same parts as
everyone else's, and a page so heavy with effects that it never finishes loading on a
phone. Every question here is about choosing on purpose between them.

Question IDs use the prefix `WS`.

---

### WS1: the one thing a visitor does `[must-ask]`
**Ask:** A stranger lands here and looks around for a minute. What is the one thing you
want them to do before they leave? Everything on the page either leads there or is in
the way.
**Options:** write to you / look closely at one piece of work / buy or book / remember the
name and come back / something else / not sure, suggest one
**Opens:** what the first screen leads to, WS3, the contact path (W13 when there is a form)

### WS2: how people get here `[must-ask]`
**Ask:** How does someone end up on this page: a link in your profile, a search, a code
printed on a card, a friend sending it? A person who searched knows nothing about you; a
person who tapped your profile already does, and the first screen should not repeat it.
**Options:** from a link I share (recommended for a portfolio) / from a search / from
print or an event / a mix
**Opens:** whether a search engine must be able to read it (W1), link preview (W12),
first-screen content

### WS3: the first five seconds `[must-ask]`
**Ask:** What does someone see before they scroll or touch anything? This is the only
part everybody sees.
**Options:** one piece of your best work, filling the screen / a single sentence in large
letters / something moving that sets the mood / you, in a photo or film / show me
instead / something else / not sure, suggest one
**Opens:** E4 lettering, E22 movement, load time (WS7), asset list

### WS4: what is real today `[must-ask]`
**Ask:** What material exists right now: photos, films, writing, a logo? Count it. A
page designed around pictures that do not exist yet ends up looking like a template,
because that is what fills the gaps.
**Options:** all of it is ready / some, the rest is coming by a date / almost none yet
**Opens:** E11 who makes the art, E14 asset list, who writes the words (E17), build order
**Check:** when the answer is "almost none", say so plainly: the design waits for the
material, or is built around words alone.

### WS5: how the story unfolds `[should-ask]`
**Ask:** How should someone move through it?
**Options:** one long page that tells a story as you scroll / separate rooms, one page
each / a wall you can wander in any order / a single screen, nothing to scroll / show me
instead / something else / not sure, suggest one
**Opens:** navigation, E22, WS6, every page a link (W5)

### WS6: going from one page to the next `[nice-to-have, when there is more than one page]`
**Ask:** When someone taps a piece of work, how does the next page arrive? A plain cut
is free. Anything richer means the whole site is built as one continuous thing, which
costs a few days and makes every later change slower.
**Options:** a plain cut / a soft dissolve / the picture you tapped grows into the next
page / something else / not sure, suggest one
**Opens:** build approach in 05-architecture.md, E22

### WS7: the slow phone `[should-ask]`
**Ask:** On an ordinary phone with an ordinary signal, how long may the first screen
take to appear? People leave after about three seconds, and every film, special
typeface and effect adds to it.
**Options:** under 2 seconds, and anything heavy arrives after (recommended) / under 4
seconds / it may take longer, with something worth watching while it loads
**Opens:** image and film sizes, E4, E23, the performance budget in 05-architecture.md
**Evidence:** main content within 2.5 seconds is Google's "good" line (documented,
web.dev Core Web Vitals).

### WS8: who changes it later `[should-ask]`
**Ask:** When there is new work to add in three months, who adds it? If it is you and
you do not write code, the site needs a simple editing screen, and that is its own piece
of building.
**Options:** me, through a simple editor / me, by editing files / whoever built it / it
will not change
**Opens:** content tool choice, hosting, P12

### WS9: other languages `[nice-to-have]`
**Ask:** Does it need more than one language? Decided now it is cheap; added later,
every page is rebuilt.
**Options:** one language (recommended) / two or more, from the start
**Opens:** content volume, layout (long words break tight designs)

### WS10: keyboard and screen readers `[should-ask]`
**Ask:** Should someone who cannot see the screen, or cannot use a mouse, still get
everything? A site made of pictures and movement shuts those people out unless every
picture has words behind it. Cheap from the start, costly later.
**Options:** yes, everything has a words-only path (recommended) / the main content only
/ not in the first version
**Opens:** picture descriptions in the asset list, W14, E3

### WS11: counting visitors `[nice-to-have]`
**Ask:** Do you want to know how many people came and what they looked at? Counting
that follows people around needs a consent banner in some countries; simple counting
does not.
**Options:** simple counting, no banner (recommended) / none / full tracking with a banner
**Opens:** W10, O3

---

## Defaults for this archetype

Assume these, log as `ASSUMED`, do not spend questions on them:

- Words are real text, never pictures of text.
- It is fully usable with movement switched off (see `defaults.md`, Look, motion and
  speed).
- Anything heavy has a still picture that shows first and stays if the heavy part fails.
- Phone layout is designed, not shrunk from the laptop one.
- One title, one description and one preview picture per page.
- A designed "page not found".
- No sound unless the visitor starts it.

## Cascade rules

| If the answer is | Add these |
|---|---|
| a search must find it | W1, readable pages before any code runs, W12 |
| a showpiece, 3D or film on the first screen | E23, WS7, a still picture in the asset list |
| one long scrolling story | E22, what phones get, movement switched off |
| a contact or booking form | W13 bots, where messages go, W9 email |
| it sells something | W8 hosting terms, payments (`defaults.md`), O3 |
| the owner edits it | WS8 editing screen, picture size limits |
| material is not ready | E11, a date for it, build order in 10-build-plan.md |
