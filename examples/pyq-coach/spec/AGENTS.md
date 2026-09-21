# Instructions for the build agent

You are building PYQ Coach from the spec in this folder. The spec is the source of truth.

## Never
- Present a solution as checked unless its check passed. In v0 no solution is checked, so
  every solution sits behind the "Not checked yet" card. (A7, A36)
- Present a guess as a fact: AI merges, AI "fundamental" labels, and thin-data numbers are
  always labelled. (A7)
- Show a question without its scan region. (D21)
- Count duplicates or out-of-syllabus questions toward frequencies. (D24, D26)
- Mix marks and question counts in one frequency calculation. (A12)
- Accept current-semester papers. (D3)
- Use the phrases "will be asked", "will come", "predicted", "sure shot", "guaranteed". (A18)
- Build v1 features (AI generation, personal keys) during v0.
- Relitigate a decision in 07-decisions.md. Stop and ask instead.

## Always
- Run every AI reading step as a short background job, never inside a page request. (A2)
- Treat all AI output as untrusted input.
- Test every invariant in 03-data-model.md before building the feature that could break it.
- Build milestones in the order of 10-build-plan.md.

## Principles
1. Never present a solution as checked unless it passed the checks.
2. Never present a guess as a fact.
3. The scan is the source of truth.
4. The topic map describes the past; it never predicts the exam.
5. Nothing from the current semester.
