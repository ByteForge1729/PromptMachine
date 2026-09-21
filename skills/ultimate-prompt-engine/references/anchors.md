# Anchors

Jargon the user has not met, translated into something they have already used.

**Rule: never name a pattern without anchoring it.** "Optimistic UI" means nothing to
someone who has not built software. "The action looks done instantly, like when you
like something on Instagram and the heart fills before the server has heard about it"
means something to everyone.

**Rule: the anchor must be a product they plausibly use.** Anchoring to Kubernetes or
Kafka explains nothing to a student building their first app. Anchor to WhatsApp,
Instagram, Spotify, Notion, Google Docs, Swiggy, Uber, Duolingo, iOS, Gmail.

**Rule: one sentence, then stop.** The anchor is there to make the choice decidable,
not to teach the concept. If they want depth they will ask.

When you invent a good anchor, add it here.

---

## Visual and design language

| Term | Anchor |
|---|---|
| Glassmorphism | Frosted translucent panels you can see blurred content through, like iOS Control Centre and visionOS windows |
| Neumorphism | Soft extruded shapes that look pressed into the background, like early Apple Watch fitness dials. Mostly out of fashion, and bad for contrast |
| Brutalism | Raw, loud, unpolished, heavy borders and system fonts, like Bloomberg terminal or Gumroad's redesign |
| Material Design | Google's system: elevation shadows, ripple on tap, floating action button, like Gmail and Google Photos on Android |
| Human Interface Guidelines | Apple's system: large navigation titles, bottom sheets, SF Symbols, like Apple Notes and Fitness |
| Design tokens | Named values for colour and spacing so one change updates everywhere, like Figma styles or CSS variables |
| Dark mode first | Designing for dark and adapting to light, like Linear or the Spotify desktop app |
| Bento grid | Dashboard of unequal tiles, each self-contained, like the Apple product pages or a Notion gallery |
| Skeleton screens | Grey placeholder shapes while content loads instead of a spinner, like Facebook's feed or YouTube |
| Empty state | What the screen shows before any data exists. The most-skipped screen in every project, and the first one a new user sees |

## Interaction and feel

| Term | Anchor |
|---|---|
| Optimistic UI | The action appears done instantly and quietly rolls back if the server rejects it, like liking a post on Instagram |
| Pessimistic UI | Nothing changes until the server confirms, like a bank transfer screen. Slower, but never lies |
| Command palette | Cmd+K opens a searchable list of every action, like VS Code, Linear or Raycast |
| Infinite scroll | Content loads as you reach the bottom with no pages, like Instagram. Kills the footer and makes "go back to where I was" hard |
| Pull to refresh | Drag down to reload, like Twitter and Gmail on phones |
| Bottom sheet | A panel that slides up from the bottom over the content, like the iOS share sheet or Google Maps place details |
| Undo instead of confirm | Do it immediately, offer "Undo" for a few seconds, like Gmail's "Message sent. Undo." Usually better than a confirm dialog |
| Progressive disclosure | Show three options, hide twenty behind "Advanced", like the iPhone camera |
| Haptics | Small vibrations on action, like the iPhone keyboard or Apple Pay confirmation |
| Micro-interaction | Tiny animation acknowledging a tap, like the Twitter heart burst or Duolingo's streak flame |

## Architecture and data

| Term | Anchor |
|---|---|
| Client-server | The app on the phone asks a server for everything, like Instagram. Nothing works without signal |
| Local-first | The app owns the data and syncs when it can, like Apple Notes or Obsidian. Works on a plane |
| Offline-first | Every action works offline and queues, like WhatsApp sending a message in a tunnel and delivering it later |
| Source of truth | The one place that is right when copies disagree. Skipping this decision is why sync bugs are unfixable |
| Eventual consistency | Two people see different numbers for a few seconds, then agree, like an Instagram like count |
| Optimistic locking | Two edits collide and the second person is told "this changed, reload", like Google Sheets warning on a stale tab |
| CRDT | Both edits merge automatically with no conflict prompt, like Google Docs or Figma multiplayer. Powerful, and hard to build |
| Event sourcing | Store what happened, not the current total, like a bank statement instead of a balance. Great for audit, heavier to query |
| Soft delete | The row is hidden, not removed, like the Gmail bin. Decide this before the first delete button exists |
| Denormalisation | Storing the same fact in two places so reads are fast, like Instagram caching the like count on the post |
| Serverless functions | Code that runs only when called and costs nothing idle, like a Vercel or Firebase function |
| Background job | Work that outlives the request, like Spotify generating your Wrapped overnight |
| Webhook | Another service calls you when something happens, like Stripe telling you a payment cleared |
| Rate limiting | Cutting someone off after N requests, like the "too many attempts, try later" on a login screen |
| Idempotency | Doing the same thing twice has the same effect as once, so a double-tapped Pay button charges once |

## Identity and access

| Term | Anchor |
|---|---|
| Magic link | No password, you get an email with a link, like Notion or Substack |
| OAuth / social login | "Continue with Google", like almost every app |
| Passkeys | Face or fingerprint replaces the password entirely, like signing into an Apple account on a new device |
| RBAC | Fixed roles with fixed powers: admin, editor, viewer, like a Google Doc's sharing menu |
| ABAC | Permission computed from attributes, like "only the person who created this expense can delete it" |
| Row-level security | The database itself refuses to return rows you do not own, like Supabase RLS. Safer than checking in app code |
| Multi-tenancy | Many separate groups in one database that must never see each other, like Slack workspaces |
| Guest / anonymous account | Use it before signing up and keep your data when you do, like Duolingo. Big for retention, fiddly to build |

## Growth, money and engagement

| Term | Anchor |
|---|---|
| Freemium | Free forever with a paid tier, like Spotify |
| Paywall | Free until you hit a limit, like Notion's block cap or Figma's file cap |
| Streak | Consecutive-day counter with loss aversion, like Duolingo. Effective, and hostile if done carelessly |
| Leaderboard | Public ranking, like Duolingo leagues or Strava segments. Motivates the top 10%, demotivates everyone else |
| Variable reward | Unpredictable payoff, like Instagram refresh or loot boxes. Powerful and ethically loaded, decide deliberately |
| Social proof | "12 friends already joined", like Splitwise invites |
| Viral loop | Using the product invites someone else by necessity, like a Splitwise group or a Google Doc share |
| Retention hook | The reason to open it on day 7, not day 1. Most projects have none and never notice |
| Analytics event | A named record of something a user did, like "expense_created". Decide the ten you care about before launch, not after |

## Quality and operations

| Term | Anchor |
|---|---|
| Feature flag | Ship it off and turn it on for some people, like Instagram rolling out a feature to 1% |
| Canary release | Give the new version to a few users first, watch the errors, then continue |
| Graceful degradation | Something breaks and the rest still works, like Maps showing the route with no traffic data |
| Observability | Being able to answer "why was it slow for this one user at 3am" after the fact |
| Error budget | An agreed amount of allowed failure, so "never break" stops being the unspoken requirement |
| Accessibility (a11y) | Usable with a screen reader, one hand, or poor eyesight. Legally required in many markets, and the phone-in-sunlight case affects everyone |
| i18n | Built so the language and date format can change without rewriting screens. Cheap now, brutal later |

## Assets and files

| Term | Anchor |
|---|---|
| Asset | Any file the app shows or plays that is not code: icons, pictures, animations, fonts, sounds |
| Vector (SVG) | A picture made of shapes, so it stays sharp at any size, like icons in Google Maps |
| Raster (PNG) | A picture made of pixels, like a phone photo. Blurs when enlarged |
| Lottie | A small animation file, like the loading and success animations in Swiggy or Paytm |
| Rive | Animation that reacts live to what the user does, like the Duolingo characters changing expression |
| Splash screen | The picture shown for a second while the app opens, like the WhatsApp logo on launch |
| Adaptive icon | Android's app icon that the phone crops into a circle, squircle or square, so the edges must be safe to cut |
| Feature graphic | The wide banner at the top of a Play Store listing |
| Style reference sheet | One page showing the character from several angles and moods, so every later drawing matches |
| Design system | The reusable kit of colours, fonts, buttons and spacing, like a LEGO set every screen is built from |
