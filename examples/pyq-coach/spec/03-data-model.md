# Data model

IDs are UUIDs; times are UTC, shown in IST. Money never appears in v0.

## Entities

### Student
| Field | Type | Rule |
|---|---|---|
| id | uuid | |
| email | text | @iitb.ac.in only (A9) |
| name | text | never shown on public share pages unless the student opts in (A16) |
| confirmed_18_plus | boolean | required to create an account (D18) |
| deleted_at | timestamp or null | on deletion: name, email, marks, plans erased; uploads kept anonymous (D17, A25) |

### Course
`code` ("MA 109"), `title`.

### SyllabusVersion
| Field | Type | Rule |
|---|---|---|
| course_id | course | |
| effective_from_year | integer | a paper is tagged against the version in force in its year (A26) |
| topics | list of Topic | pasted from the course catalogue |
| submitted_by, confirmed_by | student | two different students; unconfirmed versions are not published (D7) |

### Topic
`name`, `syllabus_version_id`, `ai_fundamental` (boolean, labelled "AI-suggested"),
`disagree_count`. (D23)

### Paper
| Field | Type | Rule |
|---|---|---|
| course_id, year, exam_type | | exam_type ∈ {mid-sem, end-sem}; the current semester is refused (D3) |
| uploader_id | student or null | null after the uploader deletes their account (D17) |
| pages | list of images | PDF or phone photos, at most 30 pages, 20 MB (A29) |
| status | enum: processing, ready, failed | |
| duplicate_of | paper or null | set by AI matching; counted once; undo available (D24, A27) |
| prints_marks | boolean | whether the paper shows marks per question (A12) |

### Question
| Field | Type | Rule |
|---|---|---|
| paper_id, number | | "MA 109 · End-sem 2023 · Q4" (A31) |
| text | text with maths notation | extracted; the scan wins when they disagree (A8) |
| scan_region | image crop | always shown beside the text (D21) |
| figure | image crop or null | if cropping fails, the whole scan region is used (D25, A30) |
| marks | integer or null | |
| topics | list of topics | a question on two topics counts half to each (A34) |
| in_current_syllabus | boolean | false → kept, labelled, never counted (D26) |
| misread_reports | integer | at 2 the question is hidden until corrected (D21) |

### Solution
`question_id`, `source` (senior's paper | AI, v1), `text`, `check_status`
(passed | disagreed | pending). Senior solutions are checked exactly like AI ones. (D10, D2)

### Mark (private)
`student_id`, `question_id`, `done`, `hard`. (A15)

### Plan
`student_id`, `course_id`, `sessions` (9 sessions, topic list and questions each),
`based_on_papers`. (D19, A28)

### ShareLink
`owner_id`, `kind` (question set | plan), `items`, `token` (long random, unguessable),
`show_owner_name` (default false). No account needed to open. (D11, A16, A35)

## Invariants

Each needs an automated test.

1. A paper marked as a duplicate never contributes to any topic frequency.
2. Questions not in the current syllabus never contribute to the topic map or plans.
3. No solution is shown as checked unless `check_status = passed`; `disagreed` solutions
   appear only behind the red card and never in plans. (v1; the rule is enforced from v0 for
   senior solutions.)
4. Every question on screen shows its scan region.
5. No personal API key is ever sent to or stored on the server (v1).
6. No paper from the current semester is ever accepted.
7. The interface never says "will be asked", "will come", "predicted", "sure shot" or
   "guaranteed".
8. Every frequency and every plan shows how many papers it is based on.
9. Topic frequencies of a course always add up to 100% (±1% rounding).

## Derived values

### Paper weight (D27, A11)
```
weight(paper) = 0.5 ^ ((current_year - paper.year) / 3)     # half weight every 3 years
```
A paper from the current year weighs 1.0, from 3 years ago 0.5, from 6 years ago 0.25.

### Topic frequency (D9, A12, A34)
```
counted = questions from non-duplicate papers, in the current syllabus, not hidden

size(q) = q.marks   if EVERY counted paper of this course prints marks
          1         otherwise                       # never mix marks and counts

frequency(topic) = Σ over counted q tagged with topic of  weight(q.paper) × size(q) / len(q.topics)
                   ────────────────────────────────────────────────────────────────────────────
                   Σ over all counted q of  weight(q.paper) × size(q)
```
**Found at emit (A12):** a draft rule that counted a question with no printed marks as "1
mark" made a topic covering half of all questions show as 6%, because other papers
printed 15 marks per question. The rule above uses marks only when every paper has them.

### Thin data (D14, A13)
Fewer than 3 counted papers: every frequency and plan carries "based on N papers: a rough
guide".

### Exam plan (D19, A28)
```
priority(topic) = frequency(topic) × (1.5 if the student marked any question in it hard else 1)
sessions: 3 per day × 3 days, about 90 minutes each
fill sessions in priority order; each gets 1–2 topics and 3–6 real past questions
the "Important, not asked yet" topics each get one slot on day 3
```
