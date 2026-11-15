# Experience lens

Active whenever a human looks at the product. **Required, not optional,** when the brief
mentions a look, a brand, a mascot or character, a game layer, or a named visual
identity: in those projects the experience is the product, and a spec without it is
a spec for a different app.

Covers five things users rarely separate but builders must: **feel** (what it is like),
**visuals** (colour, type, layout), **assets** (every file someone has to make or find),
**motion and sound**, and **words** (tone and microcopy). Feel comes first: a build agent
handed no point of view fills every gap with the most common choice, and the result
looks like everything else.

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

Ask these before anything about colour, layout or features. Each is a **taste question**:
no recommendation, at least four directions that differ from each other, and always
"show me instead", "something else" and "not sure, suggest one". Write the options fresh
for the project; the ones below only show the shape.

### E19: the one-minute feeling `[must-ask]`
**Ask:** Someone spends one minute with this and then closes it. What do you want them to
feel in that minute? This decides almost everything about how it looks and moves, so it
comes before any of that.
**Options:** calm and in control, like a tidy desk / a small thrill, like opening a
parcel / impressed, like walking into a gallery / at home, like a friend's kitchen /
show me instead / something else / not sure, suggest one
**Opens:** E1, E20, E21, E22, E4, E17. Write the answer into `06-experience.md` as the
point of view, in the user's own words.

### E1: the closest thing that already exists `[should-ask]`
**Ask:** Is there anything that already gives you that feeling? An app, a site, a shop,
a film, a magazine, a room. It does not have to be software. One reference saves a dozen
smaller questions about colour, spacing and speed.
**Options:** show me instead: upload screenshots or links / name it in words / two or
three anchors written for this project, never the same ones twice / nothing comes to mind
**Opens:** colour, type, motion speed, copy tone. Answer E2 to E6 in its light.
**Check:** a reference is a start, not the answer. Ask which part they liked, and what
should be different so this is not a copy of it.

### E20: the moment worth extra care `[should-ask]`
**Ask:** If one moment of this could be far better than it needs to be, which one? Extra
care everywhere costs months. One moment costs days, and it is what people remember.
**Options:** build them from F1 and the brief: the first thing you see / the moment the
main thing is done / going from one part to the next / none, keep it even throughout /
something else / not sure, suggest one
**Opens:** E22, the delight step (`delight.md`), a polish milestone in 10-build-plan.md

### E21: what it must not be mistaken for `[should-ask]`
**Ask:** Picture a version of this that would embarrass you. What does it look like?
Naming it tells the builder what to stay away from, which works better than a word like
"modern".
**Options:** write them for the project: a template everyone has seen / a bank's website
/ a toy for small children / a tech start-up page with a purple glow / something else /
not sure, suggest one
**Opens:** the "Not this" list in `06-experience.md`, the generic-look check in
`antipatterns.md`

### E2: light, dark or both `[should-ask]`
**Ask:** Light mode, dark mode, or both? Both is nearly free if we decide now and costly
to retrofit, because every colour has to be picked twice.
**Options:** both, follow the phone setting (recommended) / dark only / light only
**Opens:** colour tokens, asset variants (icons and art need to work on both)

## Visuals

### E3: colours that carry meaning `[must-ask, when colour tells two things apart: money, scores, two lines on a graph]`
**Ask:** "You owe" and "you are owed" are usually red and green. About 1 in 12 men cannot
tell those apart. Do we rely on colour alone, or add a second signal?
**Options:** colour plus an arrow or +/- sign (recommended) / colour plus words ("you owe")
/ colour only
**Opens:** accessibility, icon set, the balance component design

### E4: lettering `[must-ask, when people come to look: websites, games, simulations, a named look; otherwise should-ask]`
**Ask:** How should the words themselves look? Lettering does more for the look than any
colour. A special typeface is one more file to load, and sometimes to pay for.
**Options:** big and loud, like a film poster / quiet and bookish, like a novel / plain
and exact, like a train timetable / hand-made, like a market sign / show me instead /
something else / not sure, suggest one
**Opens:** font licensing, load time, the numbers design
**In the spec, not the question:** one named face for headings and one for reading, with
sizes in large steps. Never "a clean sans-serif".

### E5: icons `[nice-to-have]`
**Ask:** Where do the small icons come from? Drawing your own takes days; a free icon set
takes minutes and stays consistent.
**Options:** a free icon set like Material Symbols or Phosphor (recommended) / a custom set
matching the brand / mix
**Opens:** asset sourcing, licence file, style consistency

### E6: the main screen layout `[must-ask]`
**Ask:** When the app opens, what fills the screen? The list of groups, your total balance,
or the character? Whatever sits there is what people will think the app is.
**Options:** propose two concrete layouts from the answers to P1 and F1 and let them pick
**Opens:** navigation, home screen spec, 06-experience.md

## Character and game layer

Skip this section entirely when there is no mascot, character or game mechanic.

### E7: what the character is for `[must-ask, when a character exists]`
**Ask:** What is the character's job? To make paying back feel like a win, to nag people
who owe, or just to make the app charming? The same monster that feels fun as a reward
feels hostile as a nag, and people delete apps that make them feel judged in front of
friends.
**Options:** celebrates progress, never shames (recommended) / nags the person who owes /
pure decoration / not sure, suggest one
**Opens:** E8, E9, notification copy, 08-risks.md (social shame risk)

### E8: what drives the character `[must-ask, when a character exists]`
**Ask:** What exactly makes it change? Total money owed, number of days a debt is old, or
how many debts are still open? Each gives a different game. Money-based punishes the
person who covered the big dinner; age-based rewards paying quickly.
**Options:** age of oldest unpaid debt (recommended) / total amount owed / number of open
debts / not sure, suggest one
**Opens:** data the app must track, the states the art must cover, fairness edge cases

### E9: whose character is it `[must-ask, when a character exists]`
**Ask:** Is there one character per group that everyone shares, or one per person? A
shared one creates team spirit. A personal one visible to the group creates public
pressure on whoever owes the most.
**Options:** one per group, shared (recommended) / one per person, private / one per person,
visible to the group
**Opens:** privacy of balances, screen layout, number of art states

### E10: how many looks `[must-ask, when a character exists]`
**Ask:** How many different states does the character need drawn? Every state is a
separate piece of art, and animated states cost several times a still image. Three to
five states is enough for most games.
**Options:** 3 stills (calm, grumpy, defeated) (recommended for v0) / 5 animated states /
it changes smoothly, no fixed states / not sure, suggest one
**Opens:** asset list, animation tool choice, effort estimate

## Assets

Every image, animation, sound and font is a file someone has to make, find or pay for.
Users never list these. Build the list for them.

### E11: who makes the art `[must-ask, when custom art exists]`
**Ask:** Who makes the custom art, like the character? You, an AI image tool, a friend or
freelancer, or a free library? Each has a catch: AI art is fast but hard to keep
consistent across ten poses, and some licences restrict commercial use.
**Options:** AI-generated, then cleaned up by hand / you draw it / a friend or freelancer
/ adapt a free library (unDraw, Storyset) / not sure, suggest one
**Opens:** licences, style consistency, timeline, 08-risks.md

### E12: still or moving art `[must-ask, when a character exists]`
**Ask:** Does the character move? A still image costs nothing to show. A simple
looping animation (like the Duolingo owl bobbing) needs an animation file format. A
character that reacts to taps and changes mood live needs an interactive animation tool.
**Options:** stills with a small bounce done in code (recommended for v0) / looping
animation files (Lottie) / interactive animation (Rive) / not sure, suggest one
**Opens:** tooling, app size, build setup (see defaults.md: Rive needs a development build)
**Always follow up when "live animation later" is the plan:** art made today as flat,
single images cannot be rigged for live animation later; it has to be redrawn. Ask
whether to generate or draw each character in **separate layers** now (body, eyes,
mouth, arms, props) and keep the source files. Costs little today, saves redoing all
the art at v1.

### E13: the store-facing assets `[must-ask, when publishing to a store]`
**Ask:** The store listing needs an app icon, a feature graphic and at least a few phone
screenshots. These are the first thing strangers judge, and they usually get made in a
panic the night before launch. Plan them now?
**Options:** yes, make them part of the build plan (recommended) / later, internal testing
only
**Opens:** 10-build-plan.md, asset list

### E14: the asset list `[must-ask]`
Not a question. Before writing the spec, produce the full asset list from the answers
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

### E22: what movement is for `[must-ask, when people come to look: websites, games, simulations, a named look; otherwise should-ask]`
**Ask:** When things move on screen, what is the movement for? More movement means more
building time, and phones need a simpler version of anything heavy.
**Options:** it leads the eye through a story as you scroll, like an Apple product page /
small replies to your touch, like a button that presses in / one showpiece people
remember, like a 3D object that turns as you scroll / almost none, like a well-printed
book / show me instead / something else / not sure, suggest one
**Opens:** the motion rules in `06-experience.md`, E23 when a showpiece or a scroll story
is chosen, load time (W7, WS7)
**In the spec, not the question:** durations, easing and the swap for people who have
movement switched off come from `defaults.md`.

### E23: what a weak phone gets `[should-ask, when a showpiece, 3D or film is chosen]`
**Ask:** The rich version will be slow on an older phone. What should that person get?
**Options:** a lighter version straight away, with a still picture where the heavy part
would be (recommended) / the same thing, and they wait / words and pictures only
**Opens:** fallback rules, the still picture in the asset list, the performance budget in
05-architecture.md

### E24: the thing done fifty times a day `[should-ask, when people use it daily]`
**Ask:** Which action will someone repeat many times in one sitting? That one should be
instant, with no animation at all. A flourish is charming twice and tiring the fiftieth
time, so flourishes belong on things that happen rarely.
**Options:** name it from F1 and ask them to confirm / nothing repeats, it is used now
and then
**Opens:** what never animates, keyboard shortcuts, E15

### E15: celebration moments `[should-ask]`
**Ask:** When something good happens, like a debt fully cleared, what does the app do?
A small confetti burst and a buzz (like Google Pay's cashback scratch card) makes the
moment feel like a reward. Too many of these and it feels like a slot machine.
**Options:** one big moment for the main win only (recommended) / small touches everywhere /
none
**Opens:** motion spec, haptics, sound

### E16: sound `[nice-to-have]`
**Ask:** Any sounds? Most people keep their phone on silent, so sound can never carry
meaning on its own, but a tiny sound on the big win adds a lot.
**Options:** no sound, vibration only (recommended) / one sound for the big win / sounds
throughout, with a mute switch
**Opens:** asset list, settings screen

## Words

### E17: voice `[must-ask]`
**Ask:** How does the app talk? Read these three versions of the same message and pick.
**Options:** show one real message from this project written three ways, e.g.
"Payment pending" / "Waiting for Rahul to confirm" / "Rahul says he paid. Your move."
**Opens:** all copy, notification text, error messages

### E18: the hard messages `[should-ask]`
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
| a showpiece, 3D or film | E23, a load-time budget, a still picture in the asset list |
| used every day | E24, no animation on the repeated action |
| any movement at all | the swap for movement switched off (`defaults.md`), logged as ASSUMED |
| a feeling but no reference | E1, or propose three small written sketches and let them react |

## Before the spec

Run the generic-look check in `antipatterns.md` over `06-experience.md`. Every choice of
lettering, colour, layout and movement must trace to an answer in this lens. A choice
with no answer behind it is where the default look gets in.
