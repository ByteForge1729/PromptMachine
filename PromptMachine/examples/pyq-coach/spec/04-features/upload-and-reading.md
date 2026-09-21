# Upload and reading

**Tier:** v0 · **Sources:** B4, D3, D10, D21, D24, D25, D28, A2, A8, A19, A27, A29, A30, A31

## Behaviour
1. Upload by PDF (laptop or phone) or phone camera, up to 30 pages / 20 MB.
2. Blurry photos are flagged before upload: "Retake this page".
3. Uploader picks course, year, exam type. Current semester is refused.
4. Processing runs in the background as one short job per page, then one per question,
   so no job approaches the hosting time limit. Status shows "Reading page 4 of 12".
5. The AI model extracts each question's text with maths notation, marks, figure crop, scan
   region, and any handwritten solution.
6. Duplicate check: if most questions match an existing paper of the same course, the new
   paper is merged into it ("merged by AI", undo available to anyone signed in).
7. Every question is shown with its scan snippet and a "Report a misread" button; 2 reports
   hide it until corrected.

## States
- Processing failed on a page: that page is marked "Couldn't read", the rest publish.
- Reading budget cap reached: uploads are accepted and queued, "Reading will resume next
  month", nothing is lost. (A6)

## Acceptance criteria
- [ ] Given a 12-page scanned PDF, then all questions appear within 10 minutes and no single
      processing job runs longer than 2 minutes.
- [ ] Given a paper labelled with the current semester, then upload is refused.
- [ ] Given the same paper uploaded twice, then it counts once and shows "merged by AI" with
      undo; after undo, it counts as a separate paper.
- [ ] Given an EE 225 question with a circuit, then the figure appears with the question.
- [ ] Given 2 misread reports, then the question is hidden from practice and plans.
