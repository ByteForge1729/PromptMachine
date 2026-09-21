# Defaults

Settled choices, so you do not burn a web search on a question that already has a good
answer. Use these to populate the "(Recommended)" option and to auto-decide when the
user says "decide for me".

**Every entry is dated.** A stale recommendation is still useful because the reasoning
outlives the product names. When an entry is more than a year old, keep the reasoning,
verify the product, and say so rather than asserting it.

**Never present a default as the only option.** The user always gets alternatives and
the reason to pick one.

*Last full review: 2026-09*

---

## Cross-platform mobile

| If | Then | Because |
|---|---|---|
| Solo developer, JavaScript or TypeScript already known | React Native with Expo | Largest hiring pool, best tutorial coverage, Expo removes the native build toolchain entirely. The default unless something below overrides it |
| Heavy custom animation, identical pixels on both platforms | Flutter | Draws its own widgets so the two platforms cannot drift. Dart is a real cost if nobody knows it |
| Android is the real target, iOS is maybe-later | Kotlin, native | Shipping one platform properly beats shipping two badly. Kotlin Multiplatform is the upgrade path if iOS becomes real |
| Existing Android team, iOS added later | Kotlin Multiplatform | Share the logic, keep native UI on both. Matured a lot, and the shared-logic-not-shared-UI split is the right seam |
| It is a form over a database and could be a website | A web app | Say this out loud. Most "apps" do not need to be apps, and an app store review cycle is a real tax on a student project |

*Reviewed 2026-09. Sources below.*

## Backend and database

| If | Then | Because |
|---|---|---|
| Relational data, you want SQL, solo or small team | Supabase (Postgres) | Real Postgres you can leave with, row-level security does authorisation in the database, generous free tier |
| Using Supabase's free tier | Add custom SMTP before launch, and a daily keep-alive request if usage is seasonal | Built-in auth email sends 2 per hour and only to the project's own team; free projects pause after about a week of low activity (Supabase docs, documented, 2026-09) |
| Heavy realtime, document-shaped data, Google ecosystem | Firebase | Realtime sync is genuinely excellent. The cost is a proprietary query model that is painful to migrate off |
| Just needs a local store on the device | SQLite, or Room on Android | No server, no account, no cost, no sync bugs. Enormously underrated for v0 |
| Needs a custom backend for real | Postgres plus one boring server framework | One service. Not microservices. Not until there is a team big enough to need separate deploys |
| Data is genuinely a graph (social, recommendations) | Still Postgres | Recursive queries handle far more than people expect. Reach for a graph database only after Postgres visibly fails |

*Reviewed 2026-09.*

## Authentication

| If | Then | Because |
|---|---|---|
| Already using Supabase | Supabase Auth | One system, one user table, RLS policies reference the session directly. Do not add a second auth provider |
| Already using Firebase | Firebase Auth | Same reasoning |
| Want the best sign-in UX with the least work, paying is fine | Clerk | Drop-in components, organisations and invites built in. Priced per active user, which bites at scale |
| Self-hosted, open source, own the user table | Better Auth or Auth.js | More wiring, no vendor, no per-user cost |
| Enterprise SSO, SAML, compliance | Auth0 or WorkOS | This is what they are for and what you are paying for |
| Never | Rolling your own password storage | There is no version of this that is worth the time |

Sign-in method default: **social login plus magic link, no passwords.** Passwords mean
reset flows, breach exposure and a support burden, for a worse experience. Add passkeys
when the platform makes it cheap.

*Reviewed 2026-09.*

## State and sync

| If | Then | Because |
|---|---|---|
| App works fine online only | Client-server, plain fetching, cache the last response | Simplest thing that works. Do not build sync you do not need |
| Must work with no signal | Local-first: device database is the source of truth, queue writes, sync on reconnect | Roughly a third more work. Worth it only if offline is a real use case, not a nice idea |
| Multiple people edit the same object simultaneously | Last-write-wins plus a visible conflict warning | CRDTs are correct and expensive. Warn first, reach for CRDTs only when users actually collide |
| Money or balances involved | Server is the source of truth, always, no exceptions | A client that can compute a balance is a client that can be wrong about money |

*Reviewed 2026-09.*

## Payments

| If | Then | Because |
|---|---|---|
| Web, most countries | Stripe | Best documentation and developer experience by a distance |
| India-focused | Razorpay or Cashfree, plus UPI | UPI is the payment rail people actually use; a card-only flow will not convert |
| Inside an iOS or Android app, selling digital goods | Store in-app purchase, and budget for the platform cut | Both stores require it for digital goods and will reject you for routing around it |
| Splitting or settling between users | Do not move money in v0 | Handling other people's money turns a side project into a regulated business. Record who owes whom, let them settle in their own payment app, and deep-link into it |

*Reviewed 2026-09. The last row is a scope trap worth flagging unprompted.*

## UPI settle-up (India)

| If | Then | Because |
|---|---|---|
| Users settle debts with each other | Open the UPI app with the payee and amount filled in (a UPI intent link) | Zero cost, no payment licence, uses the app everyone already has |
| Deciding when a debt counts as paid | The receiver confirms, never the payer's return signal | The status a UPI app hands back is missing on some apps, wrong on others, and can be faked. Documented by Android developers; treat it as a hint only |
| Group is not in rupees | Hide the UPI button, settle by hand | UPI moves rupees only |
| Relying on this path in production | Test on real devices with GPay, PhonePe and Paytm before depending on it | Behaviour differs by app, and developers widely report payments to personal UPI IDs being declined. Not confirmed from a primary source, so verify, do not assume |

*Reviewed 2026-09.*

## Assets and animation

| If | Then | Because |
|---|---|---|
| Need icons | A free, consistent set: Material Symbols, Phosphor or Lucide | Minutes instead of days, one visual style, permissive licences |
| Need fonts | The phone's built-in font for v0, one Google Font if the brand needs it | Free, no licence risk, no load delay |
| Simple looping animation | Lottie files (LottieFiles has a free library) | Small JSON files, widely supported. Listed in Expo's own SDK docs |
| Character that reacts live to state | Rive | Built for interactive, state-driven animation. **Needs an Expo development build; it does not run in Expo Go** (stated in Rive's docs) |
| v0 of any character | Still images with a small bounce done in code | Proves the idea for almost no cost before anyone draws animation |
| AI-generated character art | Make a one-page style reference first, generate every pose against it | Otherwise each pose looks like a different creature |
| Free illustrations | unDraw, Storyset | Check the licence of each one before shipping |

*Reviewed 2026-09.*

## Hosting and deploy

| If | Then | Because |
|---|---|---|
| Web frontend, or full-stack JavaScript, **non-commercial** | Vercel or Netlify free tier | Push to deploy, free tier covers a student project comfortably |
| Web project that earns money in any way (payments, ads, affiliate links, paid work) | A paid tier, or a host whose free tier allows commercial use | Vercel's free Hobby plan is non-commercial only and counts ads as commercial (Vercel fair use guidelines, documented, updated 2026-09). Check any host's terms |
| Container, background jobs, a real backend | Railway, Render or Fly | Predictable pricing, no cloud console archaeology |
| Serious scale or an existing cloud contract | AWS, GCP or Azure | Only when something above genuinely fails. Starting here costs weeks |
| Mobile app distribution | TestFlight for iOS, internal testing track for Android | Get it onto real devices before the store review cycle becomes the bottleneck |

*Reviewed 2026-09.*

## Store and legal compliance

Not legal advice. Facts as found on the date below; verify before launch.

| If | Then | Because |
|---|---|---|
| Users can create accounts and the app is on Google Play | In-app account deletion **and** a web page to request deletion | Google Play policy requires both; the web path covers people who uninstalled (Play Console Help, documented) |
| Users can create accounts and the app is on the App Store | In-app account deletion | Apple guideline 5.1.1(v) (documented) |
| Personal data of people in India | Clear consent notice with purpose; erasure within 90 days of request; breach notice to affected users | DPDP Rules notified 14 Nov 2025 with an 18-month phase-in (PIB press release, documented). Check which obligations are live on your date |
| Any user could be under 18 | Verifiable parental consent before processing their data, or an 18+ gate | DPDP rules on children's data (documented) |
| Publishing to any store | Privacy policy URL, support contact, data safety or privacy form | Required for listing |

*Reviewed 2026-09.*

## Things to default without asking

Unless the project specifically makes one wrong, assume these and log them as `ASSUMED`.
Asking about them wastes a question slot.

- Version control is git, hosted on GitHub.
- Secrets live in environment variables, never in the repository.
- Timestamps are stored in UTC and displayed in the viewer's local timezone.
- IDs are UUIDs, not incrementing integers, so records can be created offline.
- Deletes are soft by default; hard delete is an explicit, separate decision.
- Every list view has a defined empty state and a defined error state.
- Analytics is off in development and behind consent in production.
- The first release is one platform, one language, one region.
- Automated tests cover the money-touching and data-destroying paths at minimum.

## Things never to default

Always ask. Getting these wrong silently is unrecoverable.

- Who owns the data, and what happens to it when a user leaves.
- Whether the product moves real money.
- Whether anything is shown publicly that a user might expect to be private.
- Anything involving minors, health, identity documents or location history.
- The single thing that must never happen.
