# Build plan

## M0: Foundations
**Delivers:** Next.js on Vercel, Supabase with row-level security denying all by default,
custom SMTP, keep-alive, account feature, error tracking.
**Done when:** account acceptance criteria pass.

## M1: Upload and reading
**Delivers:** PDF and camera upload, job queue, extraction with scan regions and figures,
duplicate matching, misread reports, reading cost cap.
**Depends on:** M0, and the policy check in 09.
**Done when:** upload-and-reading criteria pass on 5 real MA 109 papers, including one
phone-photographed paper.

## M2: Syllabus and topic map
**Delivers:** syllabus versions, tagging, frequency formula, topic map, "not asked yet"
branch.
**Depends on:** M1
**Done when:** syllabus and topic-map criteria pass; the frequency property test (sums to
100%, duplicates excluded, marks rule) passes on 10,000 random courses.

## M3: Practice, plan, sharing
**Delivers:** practice screens, private marks, exam plan, share links.
**Depends on:** M2
**Done when:** practice, exam-plan and sharing criteria pass.

## M4: Launch
**Delivers:** announcement in department groups (D22), weekly export.
**Done when:** 3 courses have 3 or more papers.

## v1: AI practice questions
**Starts when:** a sponsor exists (D13).
**First milestone:** the checker test from D12 (50 real questions, planted errors). Nothing
generated is shown to students until it passes.
**Done when (v1):** invariant 3 holds for AI solutions (disagreed ones only behind the red
card, never in plans), and invariant 5 is verified by inspecting server logs and requests
during personal generation: no API key ever appears.
