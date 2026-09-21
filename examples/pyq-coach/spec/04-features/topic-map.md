# Topic map

**Tier:** v0 · **Sources:** D9, D14, D20, D27, A11, A12, A13, A18

## Behaviour
1. First screen of every course: all current-syllabus topics, shaded by frequency
   (03-data-model.md), with "based on N papers".
2. Fixed line on the map: "How often a topic came up before. Any syllabus topic can be
   asked."
3. Separate branch "Important, not asked yet" for AI-suggested fundamental topics with zero
   appearances.
4. No topic is ever hidden or greyed out.
5. Wording never implies prediction (invariant 7).

## States
- No papers: "No papers yet. Upload the first one." with the upload button.
- 1–2 papers: map shown, "based on N papers: a rough guide".

## Acceptance criteria
- [ ] Given papers where only some print marks, then frequencies count questions, not marks.
- [ ] Given frequencies for any course, then they add up to 100% ±1%.
- [ ] Given a topic with zero appearances, then it is still shown, never greyed.
- [ ] Given any state, then none of the banned phrases appear.
