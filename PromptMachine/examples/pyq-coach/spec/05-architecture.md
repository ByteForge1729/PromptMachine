# Architecture

## Stack

| Layer | Choice | Why | Source |
|---|---|---|---|
| App | Next.js, responsive: phone for capture and browsing, laptop for reading | Your stack; D28 sync | B1, D28 |
| Hosting | Vercel Hobby | Free and non-commercial. **If a sponsor's logo appears, check the terms first: Vercel counts advertising as commercial use** | B1, D13 |
| Database, auth, files | Supabase: Postgres with row-level security, storage for scans, email login links | Your stack | B1, A9 |
| Login email | A transactional email service as custom SMTP | Supabase's built-in email sends 2 per hour, team addresses only (documented) | A3 |
| Keep-alive | Daily scheduled request | Free projects pause after about a week of low activity; usage is seasonal around exams (documented) | A4 |
| Background jobs | A queue table in Postgres; a database webhook calls one function per page or question | Vercel Hobby functions stop at 5 minutes (documented); per-page jobs stay far below | A2 |
| AI model (v0) | Claude Haiku 4.5 for reading pages, tagging, duplicate matching | Cheapest current model that reads images; $1 / $5 per million input / output tokens (documented) | A23 |
| AI model (v1) | A stronger Claude model through the Batch API (50% off) for generation and checking | Quality matters more than speed; generated once per course | D1, A23 |
| Code check (v1) | Runs in an isolated sandbox service, never inside the app's own functions | AI-written code is untrusted (OWASP LLM 2025) | A1 |
| Maths display | A browser maths renderer | Questions are maths-heavy | A8 |

## Boundaries

**Browser:** capture, display, marks, plan view, v1 personal generation with the student's
own key (the key never leaves the device). **Server:** everything else: storage, reading
jobs, tagging, frequencies, plans, share links. **Sandbox (v1):** code checks only.

## Integrations

| Service | Used for | When it fails |
|---|---|---|
| AI provider | Reading and tagging | Jobs retry 3 times, then "Couldn't read this page"; uploads never lost |
| Email service | Login links | "Resend" after 2 minutes |
| Supabase | Everything | Error page; nothing offline in v0 (A24) |

## Scale and cost

Designed for about 5,000 students (A20). Reading cost, my estimate: about ₹50 to ₹70 per
course for 10 papers; you cover up to ₹1,000 a semester with a budget alert, then reading
pauses and queues (A6). v1 generation: about ₹500 per course per semester at batch prices,
paid by the sponsor, with its own cap.
