# Experience

## Feel

**Placeholder:** playful but clean, like Duolingo: bright, rounded, friendly, with the
numbers always calm and legible. (A20)
`[DEFERRED: replace with a moodboard once reference screenshots arrive; see 09]`

Light and dark themes, following the phone. (A21) Phone's built-in font; Phosphor icons,
rounded weight. (A23)

## Screens

| Screen | Shows | Primary action | Empty state |
|---|---|---|---|
| Home | Group cards: name, your character, your net | Add expense (floating, bottom right) | Villager + "Create a group" (A5) |
| Arena (group) | Every member's character, name, amount; your suggested payments | Add expense | All Villagers, "Add the first expense" |
| Add expense | Amount, description, paid by, split among | Save | - |
| Settle | Suggested payments, Pay / I paid, awaiting items | Pay | "All square" |
| History | Every change, newest first, paginated | - | "Nothing yet" |
| Group settings | Name, currency, big-debt amount (creator only), members, invite | Invite | - |
| Profile | Name, UPI ID | Save | "Add your UPI ID so friends can pay you" |

## Characters

| Tier | Character | States |
|---|---|---|
| Emperor | Seated on a throne of stacked coins | 1 |
| King | Crown, cape, arms folded | 1 |
| Prince | Tiny crown, cheeky grin | 1 |
| Villager | Relaxed, holding a cutting chai | 1 |
| Goblin | Small green thief pocketing a coin | calm, annoyed, furious |
| Monster | Hulking, chewing a crumpled receipt | calm, annoyed, furious |
| Dragon | Sleeps on a pile of IOUs; smoke thickens with anger | calm, annoyed, furious |

Concepts are suggestions from the interview; you may replace any. (D12)

## Asset delivery spec

You are generating these with AI tools (D12). Make a one-page **style reference sheet**
first and generate every character against it, or they will look like different games.
Generate each character in **separate layers** (body, head, eyes, mouth, arms, props) and
keep the source files: v1 live animation needs layers, and flat images would have to be
redrawn. (D13)

| File name | What | Format | Size | Background | Variants | Layers kept | Status |
|---|---|---|---|---|---|---|---|
| `style-sheet.png` | Reference for all characters | PNG | 2048 × 2048 | any | - | - | to make |
| `char-emperor.png` | Emperor | PNG | 1024 × 1024 | transparent | works on light and dark | yes | to make |
| `char-king.png` | King | PNG | 1024 × 1024 | transparent | light and dark | yes | to make |
| `char-prince.png` | Prince | PNG | 1024 × 1024 | transparent | light and dark | yes | to make |
| `char-villager.png` | Villager | PNG | 1024 × 1024 | transparent | light and dark | yes | to make |
| `char-goblin-{calm,annoyed,furious}.png` | Goblin ×3 | PNG | 1024 × 1024 | transparent | light and dark | yes | to make |
| `char-monster-{calm,annoyed,furious}.png` | Monster ×3 | PNG | 1024 × 1024 | transparent | light and dark | yes | to make |
| `char-dragon-{calm,annoyed,furious}.png` | Dragon ×3 | PNG | 1024 × 1024 | transparent | light and dark | yes | to make |
| `app-icon-foreground.png` | Adaptive icon foreground | PNG | 1024 × 1024 | transparent, art inside the central 66% | - | - | to make |
| `app-icon-background.png` | Adaptive icon background | PNG | 1024 × 1024 | solid | - | - | to make |
| `splash-icon.png` | Launch screen mark, centred on a solid colour (Android 12+ style) | PNG | 1024 × 1024 | transparent | light and dark | - | to make |
| `share-card-frame.png` | Frame for WhatsApp reminder cards | PNG | 1080 × 1080 | solid | - | - | to make |

Characters must read clearly at 64 × 64 px, the size they appear in lists. Keep a
consistent ground line so they stand at the same height in the Arena.

## Motion, sound, haptics

- Rest: gentle bob, 2-second loop.
- Anger rises: short shake.
- Reaching Villager from a debt tier: transformation, confetti, one vibration. Once per
  event. (A25)
- No sound in v0. (A25)

## Voice

The monster talks about the debt, never the person. (A26)

- "Your ₹640 for Goa is getting hungry. Feed it?"
- "Rahul says he paid you ₹1,000. Did it land?"
- Hard message: "This one's been lurking for 3 weeks. ₹400 to Priya sends it home."

## Accessibility

- Owe/owed: colour + arrow + words. (A22)
- Characters always have a text label for screen readers ("Rahul, Dragon, owes ₹1,200").
- Respect the phone's font size up to 130% without truncating amounts.
