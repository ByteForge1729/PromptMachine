# Archetype: game

Load when the brief mentions a game, players, levels, a score, physics, or "something
fun to play".

**The governing rule of this archetype:** a game succeeds or fails on thirty seconds of
play that someone wants to repeat. Everything else, including art, levels and features,
is multiplied by that loop. Scope kills more games than bad ideas do, so the first
milestone is always a small playable slice, not a big half-finished world.

Question IDs use the prefix `GA`. For games with a gamified layer inside another app,
use that app's archetype plus the Experience lens instead.

---

### GA1: where it is played `[required]`
**Ask:** Where will people play: a web browser (instant, no install), a phone, a PC through
Steam or itch.io, or a console? Each has its own controls, stores and costs.
**Options:** web browser (recommended for a first game) / phone / PC / console
**Opens:** GA2 engine, GA8 controls, distribution

### GA2: engine `[required]`
**Ask:** Which engine? Godot is free forever with no royalties. Unity is free until the
studio earns about $200,000 a year. Unreal takes 5% of revenue after the first $1 million.
A web framework like Phaser suits small 2D browser games.
**Options:** Godot (recommended for 2D and small 3D) / Unity / Unreal (big 3D) / a web
framework
**Opens:** language, asset pipeline, export targets
**Evidence:** Unity Personal free under $200K revenue since January 2025 after the
Runtime Fee was cancelled in September 2024; Godot MIT licence; Unreal 5% after $1M
lifetime (documented, engine licence terms).

### GA3: the thirty-second loop `[required]`
**Ask:** Describe what the player does over and over in thirty seconds. Jump, aim, match,
build, answer? If this is not fun on grey boxes with no art, no amount of art will fix it.
**Options:** free text; propose a one-line loop from the brief and let them correct it
**Opens:** vertical slice, GA13 scope, prototype milestone

### GA4: why come back tomorrow `[required]`
**Ask:** What brings a player back tomorrow: new levels, an unlocked item, a daily
challenge, friends to beat, a story? Without one, most players leave after the first
session.
**Options:** progression (unlocks, levels) (recommended) / daily challenge / social
(friends, leaderboards) / story
**Opens:** save data (GA6), GA12 leaderboards, notifications

### GA5: alone or together `[required]`
**Ask:** One player, taking turns with friends, or playing live at the same time? Live
multiplayer is a different project: servers, lag, cheating and matchmaking. Turn-based
is far cheaper.
**Options:** single player (recommended for a first game) / turn-based with friends / live
multiplayer
**Opens:** servers, GA12 cheating, S2 source of truth, cost

### GA6: saving `[required]`
**Ask:** Where is progress saved? On the device only means a new phone starts from zero.
Cloud saves need accounts.
**Options:** on the device, saved automatically at every checkpoint (recommended for v0) /
cloud save with an account / none (short arcade games)
**Opens:** O1 accounts, data model

### GA7: learning to play `[optional]`
**Ask:** How does a new player learn the controls: a tutorial level, hints as they go, or
nothing? Most players will not read instructions.
**Options:** teach through the first level itself (recommended) / hints / separate tutorial
**Opens:** level design, first-session flow

### GA8: controls `[required]`
**Ask:** Touch, keyboard and mouse, or a game controller? A game designed for a keyboard
rarely feels good on a touchscreen.
**Options:** one primary input designed for first (recommended) / all equally
**Opens:** UI layout, testing devices

### GA9: performance target `[optional]`
**Ask:** What is the weakest device it must run smoothly on? Budget phones heat up and drop
frames quickly, and a stuttering game gets uninstalled.
**Options:** a named low-end device at 60 frames per second (recommended) / mid-range
only / PC only, not a concern
**Opens:** art budget, effects, testing

### GA10: art and sound `[required]`
**Ask:** How many characters, backgrounds, animations and sounds does v0 need, and who
makes them? Count them now; games routinely need ten times the art people expect.
**Options:** use the Experience lens asset list (E11 to E14) and produce the count
**Opens:** asset delivery spec, licences, timeline

### GA11: money `[optional]`
**Ask:** How does it earn money, if at all? Paid up front, ads, or in-game purchases?
Paid random rewards (loot boxes) are treated as gambling in some countries, and anything
children play carries extra rules.
**Options:** free, no money (recommended for a first game) / paid once / ads / in-game
purchases, no random paid rewards
**Opens:** store rules, O4 minors, payments

### GA12: leaderboards and cheating `[optional, when scores are compared]`
**Ask:** If scores are compared, can someone fake one? A score sent straight from the game
can be edited in seconds. Checking it on a server, or only comparing with friends, keeps
it honest.
**Options:** friends-only leaderboards (recommended) / global, server-checked / global,
trusting the game
**Opens:** server, S1 exactness, O9 abuse

### GA13: the vertical slice `[required]`
**Ask:** What is the smallest version that shows the whole game: one level, finished to the
quality you want, start to end? Build that first and show it to five people before making
more.
**Options:** one complete level (recommended) / three rough levels / the full game
**Opens:** 10-build-plan.md milestone 1, GA10 asset count

---

## Defaults for this archetype

- First milestone is a playable grey-box prototype of the loop, then one polished level.
- The game pauses when it loses focus or a phone call arrives.
- Progress saves automatically at every checkpoint.
- Sound and music each have their own volume control.
- Frame rate target is set before art production starts.

## Cascade rules

| If the answer is | Add these |
|---|---|
| multiplayer | servers, lag handling, GA12, S2, O5 cost |
| leaderboards | GA12, S1 |
| in-game purchases | GA11, store rules, O4 minors, payments |
| cloud saves | O1 accounts, O2 deletion |
| phone | M-pack questions on interruption (M9), storage (M13), distribution (M11) |
