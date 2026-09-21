# Decisions

Reversibility: **cheap** (an afternoon), **costly** (days or a data migration),
**one-way** (effectively permanent once data exists).

## From your brief (not asked again)

| # | Decision |
|---|---|
| B1 | Next.js, Supabase, Vercel |
| B2 | A hosted AI model (Claude or GPT) through the API |
| B3 | Any course; seniors upload |
| B4 | Must read scanned papers and handwritten solutions |
| B5 | A wrong solution is worse than none (restated as A7) |

## Yours

| # | Decision | Round |
|---|---|---|
| D1 | Shared bank free for everyone; students may add their own API key for personal generation | 0 |
| D2 | Unconfirmed solutions sit behind a red "checks disagreed" card and never enter plans | 0, 1 |
| D3 | Only mid-sem and end-sem papers from past semesters | 0 |
| D4 | Standard interview depth | 0 |
| D5 | Own-key questions are private, shareable by their owner | 1 |
| D6 | No leaderboard | 1 |
| D7 | Syllabus pasted from the catalogue by the first uploader, confirmed by a second student | 1 |
| D8 | Look: calm study tool, like Notion or Anki | 2 |
| D9 | First screen: topic map shaded by frequency | 2 |
| D10 | Seniors' handwritten solutions checked exactly like AI ones | 2 |
| D11 | Share links open to anyone, no account | 2 |
| D12 | Checker must catch 9 of 10 planted wrong solutions before launch; re-test on changes | 3 |
| D13 | A sponsor pays for shared generation | 3 |
| D14 | Topic map shown even with 1 paper, labelled | 3 |
| D15 | Success: 5+ courses with 5+ papers, 200+ students practising 10+ questions | 3 |
| D16 | v0 = bank, map, real-question practice, exam plan; AI generation in v1 | 4 |
| D17 | A deleted account's uploads stay, anonymous | 4 |
| D18 | 18+ confirmation; under-18s use share links only | 4 |
| D19 | Plan from frequency plus the student's "hard" marks, 3 sessions a day | 4 |
| D20 | A separate "Important, not asked yet" branch for fundamental never-asked topics | 5 |
| D21 | Scan snippet beside every question; 2 misread reports hide it | 5 |
| D22 | Launch empty; seniors fill the bank | 5 |
| D23 | The AI suggests which topics are fundamental | gate |
| D24 | The AI matches questions to merge duplicate papers | extra |
| D25 | Figures cropped from the scan | extra |
| D26 | Old-syllabus questions kept, labelled, never counted | extra |
| D27 | Recent papers count more | extra |
| D28 | One synced account: capture on phone, read on laptop | extra |

## Assumed: review first

| # | Decision | Why | Reversibility | Evidence |
|---|---|---|---|---|
| A36 | **v0 hides every senior solution behind a "Not checked yet" card** | D10 needs the v1 checker; showing them plainly would break A7 | cheap, but touches your must-never rule | found at emit |
| A7 | **Must-never restated:** never present a solution as checked unless it passed; never present a guess as a fact | No checker makes B5 literally true | one-way as a principle | my judgment |
| A2 | Background jobs, one per page or question | Vercel Hobby functions stop at 5 minutes | costly to change later | [Vercel docs](https://vercel.com/docs/functions/configuring-functions/duration) (documented) |
| A1 | v1 code checks run in an isolated sandbox | AI-written code is untrusted | costly | [OWASP LLM Top 10 2025](https://owasp.org/www-project-top-10-for-large-language-model-applications/assets/PDF/OWASP-Top-10-for-LLMs-v2025.pdf) (documented) |
| A5 | Personal API keys never leave the student's device | A leaked key costs the student money | one-way once built | my judgment |
| A3 | Custom SMTP for login emails | Built-in: 2 per hour, team only | cheap, but blocking | [Supabase docs](https://supabase.com/docs/guides/auth/auth-smtp) (documented) |
| A4 | Daily keep-alive | Free projects pause; exam-season traffic is bursty | cheap | [Supabase docs](https://supabase.com/docs/guides/platform/free-project-pausing) (documented) |
| A6 | You pay reading costs up to ₹1,000 a semester, capped; then reading queues | No sponsor yet; reading still costs something | cheap | my estimate from [Claude pricing](https://platform.claude.com/docs/en/about-claude/pricing) |
| A12 | Frequencies use marks only if every paper prints marks, else question counts | Mixing them made a topic with half of all questions show as 6% | costly once shown to students | found at emit, tested |

## Assumed: the rest

| # | Decision | Why | Reversibility |
|---|---|---|---|
| A8 | The scan is the source of truth; extracted text is a convenience | Extraction errors are the main v0 risk | cheap |
| A9 | @iitb.ac.in email login links | Institute-only accounts, no passwords | cheap |
| A11 | Paper weight halves every 3 years | D27 needs a number | cheap |
| A13 | Under 3 papers: "rough guide" label | D14 needs a threshold | cheap |
| A15 | Done / hard marks are private | No leaderboard; nothing to compare | cheap |
| A16 | Share pages: unguessable tokens, not indexed, clean WhatsApp preview, owner hidden by default | Public links done safely | cheap |
| A17 | Non-goals: current-semester material, predictions, doubt chat, other colleges | Stay small and honest | cheap |
| A18 | Banned phrases: "will be asked", "will come", "predicted", "sure shot", "guaranteed" | Map describes the past only | cheap |
| A19 | Phone capture with blur warning and retake | D28 | cheap |
| A20 | Designed for about 5,000 students | One institute | costly |
| A21 | Weekly database export as backup | Free-tier backups unverified | cheap |
| A22 | Error tracking plus alert on failed reading jobs | Silent failures otherwise | cheap |
| A23 | Claude Haiku 4.5 for reading and tagging; a stronger model via batch for v1 | Cheapest capable model now; brief allowed Claude or GPT | cheap |
| A24 | No offline mode in v0 | Web app, studied on wifi | cheap |
| A25 | Account deletion in app and on a web page | Privacy law erasure | cheap |
| A28 | 9 sessions of about 90 minutes; day 3 covers "not asked yet" topics | D19 needs numbers | cheap |
| A29 | Upload limits: 30 pages, 20 MB, 20 papers per student per day | Abuse and cost | cheap |
| A30 | Figure crop fails → show the whole question region | Never lose the figure | cheap |
| A31 | Every question labelled with course, exam, year, number | Students trust sources | cheap |

## Assumed: found while writing the spec

| # | Decision | Why | Reversibility |
|---|---|---|---|
| A26 | Syllabus versions with the year they take effect | D26 needs to know which syllabus a paper belongs to | costly |
| A27 | Merge when most questions match; "merged by AI" with undo for anyone signed in | D24 must be reversible | cheap |
| A34 | A question on two topics counts half to each | Otherwise frequencies exceed 100% | cheap |
| A35 | v0 share links cover question sets and plans; own-key questions join in v1 | D11 was about v1 content | cheap |

(A12 and A36 were also found at emit; they are listed above with the high-stakes items.)

## Superseded

| # | Was | Replaced by | Round |
|---|---|---|---|
| Brief | Leaderboard | D6 | 1 |
| Brief | Upload PDFs only | D28 adds phone capture | extra |
| R3 | Topic map hidden until 3 papers (recommended) | D14 | 3 |
