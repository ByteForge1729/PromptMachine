# Brief

## Original idea, verbatim

"PYQ Coach. A web app for IIT Bombay students. You upload past-year question papers
(PDFs, often scanned) for a course like MA 109 or EE 225. It pulls out every question,
tags each one by topic using the course syllabus, and shows which topics come up most.
Then it uses Claude or GPT through the API to generate new practice questions in the same
style, with worked solutions. Students mark questions as done or hard. It should work for
any course: seniors upload papers and everyone benefits. Free for students. I'll build it
with Next.js and Supabase, deployed on Vercel. Some papers have handwritten solutions it
must read. I want an exam-week mode that builds a 3-day revision plan from the topic
frequencies, and a leaderboard of who solved the most. Solutions must be correct, because
a wrong solution before an exam is worse than none."

## Read-back, as corrected

A shared, student-built bank of past papers for IIT Bombay courses. Seniors upload papers
from a laptop or photograph them with a phone; an AI model reads every question, including
figures and handwritten solutions, and sorts it under the course's syllabus topics. Every
student sees an honest topic map (how often each topic came up, weighted toward recent
years, never as a prediction), practises real past questions by topic, and gets a 3-day
exam-week plan. AI-generated practice questions arrive in v1, behind a strict checker and a
sponsor. No leaderboard.

## Principles

1. **Never present a solution as checked unless it passed the checks.** (B5, A7)
2. **Never present a guess as a fact.** AI merges, AI "fundamental" labels, and thin data
   are always labelled as such. (A7, D14, D23, D24)
3. **The scan is the source of truth.** Every extracted question shows its original scan.
   (D21, A8)
4. **The topic map describes the past; it never predicts the exam.** (D20, A18)
5. **Nothing from the current semester.** (D3)
