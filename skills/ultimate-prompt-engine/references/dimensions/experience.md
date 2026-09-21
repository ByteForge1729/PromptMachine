# Experience lens

Active whenever a human looks at the product. **Required, not optional,** when the brief
mentions a look, a brand, a mascot or character, a game layer, or a named visual
identity: in those projects the experience is the product, and a spec without it is
a spec for a different app.

Covers five things users rarely separate but builders must: **feel** (what it is like),
**visuals** (colour, type, layout), **assets** (every file someone has to make or find),
**motion and sound**, and **words** (tone and microcopy).

Same entry format as `product.md`. Write every question for someone who has never opened
Figma. Show, do not name: "rounded, soft, bouncy, like Duolingo" beats "playful
neo-skeuomorphic".

## Taste questions take references

A menu of four styles makes every project look like one of four apps. For any question
about **taste** (feel, colours, character look, icon style, copy voice), always offer a
**"Show me instead"** option: the user attaches screenshots or photos, or pastes links
(an app, a Pinterest or Dribbble board, a poster, a game, a room, anything).

When they do:

1. **Read every image yourself.** Pull out what is actually there: the colour palette
   (name the 3 to 5 main colours with hex values), shape language (rounded or sharp,
   flat or layered), density (airy or packed), type feel (heavy, thin, playful,
   serious), texture, and the mood in plain words.
2. **Play it back before using it:** "From your screenshots I see: deep purple and neon
   green, very rounded cards, chunky bold numbers, lots of empty space. Is that what you
   liked, or was it something else?" People often pick a reference for one detail, not
   the whole look. Ask which.
3. **Mix sources on purpose.** "Colours from image 1, character style from image 3" is a
   valid answer. Record which reference drove which decision.
4. **Save it.** Store the extracted palette and notes in `06-experience.md` as a
   moodboard section, with each reference listed, so the build agent designs from the
   same inputs.

In a harness with the question tool, "Show me instead" is one of the options, and the
upload happens in the next chat message. Without the tool, ask them to attach images
with their answers.


---

## Feel

### E1: closest existing app `[required]`
**Ask:** Which app does this feel closest to? Pick the vibe, not the features. This one
answer sets colour, spacing, fonts and animation speed all at once, so it saves a dozen
smaller questions.
**Options:** show me instead: upload screenshots or links (recommended when they have any
taste at all) / playful like Duolingo / sharp and premium like CRED / decide for me.
Adapt the anchor options to the project; never offer the same four for every app.
**Opens:** colour, type, motion speed, copy tone. Answer E2 to E6 in its light.

### E2: light, dark or both `[optional]`
**Ask:** Light mode, dark mode, or both? Both is nearly free if we decide now and costly
to retrofit, because every colour has to be picked twice.
**Options:** both, follow the phone setting (recommended) / dark only / light only
**Opens:** colour tokens, asset variants (icons and art need to work on both)

## Visuals

### E3: the money colours `[required, when money or scores are shown]`
**Ask:** "You owe" and "you are owed" are usually red and green. About 1 in 12 men cannot
tell those apart. Do we rely on colour alone, or add a second signal?
**Options:** colour plus an arrow or +/- sign (recommended) / colour plus words ("you owe")
/ colour only
**Opens:** accessibility, icon set, the balance component design

### E4: typeface `[optional]`
**Ask:** One font for everything, or a special display font for headings and big numbers?
A display font gives character (think the chunky numbers on a CRED card) but it is one
more file to license and load.
**Options:** phone's built-in font (recommended for v0) / one free Google Font / a display
font for headings plus a plain body font / decide for me
**Opens:** font licensing, app size, the numbers design

### E5: icons `[optional]`
**Ask:** Where do the small icons come from? Drawing your own takes days; a free icon set
takes minutes and stays consistent.
**Options:** a free icon set like Material Symbols or Phosphor (recommended) / a custom set
matching the brand / mix
**Opens:** asset sourcing, licence file, style consistency

### E6: the main screen layout `[required]`
**Ask:** When the app opens, what fills the screen? The list of groups, your total balance,
or the character? Whatever sits there is what people will think the app is.
**Options:** propose two concrete layouts from the answers to P1 and F1 and let them pick
**Opens:** navigation, home screen spec, 06-experience.md

## Character and game layer

Skip this section entirely when there is no mascot, character or game mechanic.

### E7: what the character is for `[required, when a character exists]`
**Ask:** What is the character's job? To make paying back feel like a win, to nag people
who owe, or just to make the app charming? The same monster that feels fun as a reward
feels hostile as a nag, and people delete apps that make them feel judged in front of
friends.
**Options:** celebrates progress, never shames (recommended) / nags the person who owes /
pure decoration / decide for me
**Opens:** E8, E9, notification copy, 08-risks.md (social shame risk)

### E8: what drives the character `[required, when a character exists]`
**Ask:** What exactly makes it change? Total money owed, number of days a debt is old, or
how many debts are still open? Each gives a different game. Money-based punishes the
person who covered the big dinner; age-based rewards paying quickly.
**Options:** age of oldest unpaid debt (recommended) / total amount owed / number of open
debts / decide for me
**Opens:** data the app must track, the states the art must cover, fairness edge cases

### E9: whose character is it `[required, when a character exists]`
**Ask:** Is there one character per group that everyone shares, or one per person? A
shared one creates team spirit. A personal one visible to the group creates public
pressure on whoever owes the most.
**Options:** one per group, shared (recommended) / one per person, private / one per person,
visible to the group
**Opens:** privacy of balances, screen layout, number of art states

### E10: how many looks `[required, when a character exists]`
**Ask:** How many different states does the character need drawn? Every state is a
separate piece of art, and animated states cost several times a still image. Three to
five states is enough for most games.
**Options:** 3 stills (calm, grumpy, defeated) (recommended for v0) / 5 animated states /
it changes smoothly, no fixed states / decide for me
**Opens:** asset list, animation tool choice, effort estimate

## Assets

Every image, animation, sound and font is a file someone has to make, find or pay for.
Users never list these. Build the list for them.

### E11: who makes the art `[required, when custom art exists]`
**Ask:** Who makes the custom art, like the character? You, an AI image tool, a friend or
freelancer, or a free library? Each has a catch: AI art is fast but hard to keep
consistent across ten poses, and some licences restrict commercial use.
**Options:** AI-generated, then cleaned up by hand / you draw it / a friend or freelancer
/ adapt a free library (unDraw, Storyset) / decide for me
**Opens:** licences, style consistency, timeline, 08-risks.md

### E12: still or moving art `[required, when a character exists]`
**Ask:** Does the character move? A still image costs nothing to show. A simple
looping animation (like the Duolingo owl bobbing) needs an animation file format. A
character that reacts to taps and changes mood live needs an interactive animation tool.
**Options:** stills with a small bounce done in code (recommended for v0) / looping
animation files (Lottie) / interactive animation (Rive) / decide for me
**Opens:** tooling, app size, build setup (see defaults.md: Rive needs a development build)
**Always follow up when "live animation later" is the plan:** art made today as flat,
single images cannot be rigged for live animation later; it has to be redrawn. Ask
whether to generate or draw each character in **separate layers** now (body, eyes,
mouth, arms, props) and keep the source files. Costs little today, saves redoing all
the art at v1.

### E13: the store-facing assets `[required, when publishing to a store]`
**Ask:** The store listing needs an app icon, a feature graphic and at least a few phone
screenshots. These are the first thing strangers judge, and they usually get made in a
panic the night before launch. Plan them now?
**Options:** yes, make them part of the build plan (recommended) / later, internal testing
only
**Opens:** 10-build-plan.md, asset list

### E14: the asset list `[required]`
Not a question. Before the readiness gate, produce the full asset list from the answers
and show it: app icon, splash screen, empty-state art, character states, icons, fonts,
sounds, store graphics. For each: source, format, licence, owner. Ask only "anything
missing?"

When the **user supplies assets themselves** (their own drawings, AI generations,
photos), the list doubles as a delivery spec so their files drop straight in: exact
file name, format (PNG with transparent background, SVG, Lottie JSON), pixel size and
export scale, safe margins, light and dark variants, and layer requirements. A user
who hands over 13 images at the wrong size and on white backgrounds loses a day.
**Opens:** 06-experience.md asset table

## Motion and sound

### E15: celebration moments `[optional]`
**Ask:** When something good happens, like a debt fully cleared, what does the app do?
A small confetti burst and a buzz (like Google Pay's cashback scratch card) makes the
moment feel like a reward. Too many of these and it feels like a slot machine.
**Options:** one big moment for the main win only (recommended) / small touches everywhere /
none
**Opens:** motion spec, haptics, sound

### E16: sound `[optional]`
**Ask:** Any sounds? Most people keep their phone on silent, so sound can never carry
meaning on its own, but a tiny sound on the big win adds a lot.
**Options:** no sound, vibration only (recommended) / one sound for the big win / sounds
throughout, with a mute switch
**Opens:** asset list, settings screen

## Words

### E17: voice `[required]`
**Ask:** How does the app talk? Read these three versions of the same message and pick.
**Options:** show one real message from this project written three ways, e.g.
"Payment pending" / "Waiting for Rahul to confirm" / "Rahul says he paid. Your move."
**Opens:** all copy, notification text, error messages

### E18: the hard messages `[optional]`
**Ask:** How do we tell someone they owe money without it feeling like a bill collector?
This one line gets seen more than any other text in a money app.
**Options:** propose three versions and let them pick
**Opens:** notifications, reminders, character dialogue

---

## Cascade rules

| If the answer is | Add these |
|---|---|
| a character exists | E7 to E12, asset list, social shame risk in 08-risks.md |
| animated or interactive art | animation tool choice, build setup, app size budget |
| AI-generated art | consistency across states, licence check, a style reference sheet |
| balances visible to the group | privacy question, opt-out, shame risk |
| publishing to a store | icon, feature graphic, screenshots, privacy text |
| a playful feel | copy voice, celebration moments, whether errors can be playful too |
| dark mode | every asset in two variants, or assets that work on both |
