# Research notes

Collected 2026-11-15 for the question-framework upgrade. Every claim is marked
**[sourced]** (the page was fetched and says so), **[snippet]** (seen only in a search
result, page not read) or **[inferred]** (my synthesis). Nothing here is from memory alone
unless marked inferred.

## Could not verify

- **Codrops** (tympanus.net) returned HTTP 403 to every fetch. The Arnaud Rocca, Joffrey
  Spitzer and Adrián Gubrica case studies were not read; only search snippets exist.
- **three.js WebGPURenderer manual** returned 404 at the URL tried. The claim that WebGPU
  falls back to WebGL 2 automatically (since r171) is a vendor blog snippet only.
- **Anthropic cookbook notebook** (prompting_for_frontend_aesthetics.ipynb): GitHub
  returned page chrome only. Its content is known secondhand through the Anthropic blog.
- **Sound design** and **typography** have no dedicated primary source in this pass.
- "Juice it or lose it": event and year not confirmed. Wikipedia cites only the YouTube
  upload (24 May 2012, Jonasson and Purho); search snippets disagree on the venue.
- No fetched source discusses **shareable states / permalinks** for simulations. That
  delight example comes from the task brief, not from research.

## 1. What generic AI output looks like

- Tells measured on 1,590 Show HN pages by DOM and computed-style checks (no LLM judge):
  Inter everywhere, centred hero, badge above the headline, identical icon-topped feature
  cards, numbered 1-2-3 steps, stat banner rows, emoji icons in nav, purple, gradients,
  glows, permanent dark mode with grey text, all-caps labels, glassmorphism. 22% of pages
  hit 4 or more of 16 patterns; 5 to 10% false positives estimated. **[sourced]**
  https://adriankrebs.ch/blog/design-slop/
- The same list names Space Grotesk, Instrument Serif, Geist and the "serif italic accent
  word" as tells. **[sourced]** (same page). So the fonts people switch to when told
  "not Inter" have become tells themselves. **[inferred]** An avoid-list alone moves the
  default; it does not create a point of view.
- Cause: "distributional convergence"; without direction the model "samples from this
  high-probability center". **[sourced]**
  https://claude.com/blog/improving-frontend-design-through-skills
- Cause: Tailwind's demo default `bg-indigo-500` spread through training data. **[sourced,
  the page's own argument, not measured]**
  https://prg.sh/ramblings/Why-Your-AI-Keeps-Building-the-Same-Purple-Gradient-Website
- Countermeasures that both pages give: decide typography, colour and theme, motion and
  backgrounds up front; commit to one cohesive direction; name a reference aesthetic;
  type contrast in big jumps ("3x+, not 1.5x"; weights 100/200 against 800/900); "one
  well-orchestrated page load" over scattered effects. **[sourced]** (both pages above)
- Things generic output leaves out, beyond looks: validation, error states, accessibility,
  hierarchy. **[sourced]** (prg.sh)
- **[inferred]** For this skill: the spec must carry a stated point of view plus concrete
  type, colour, motion and background decisions that came from the user's answers. The
  build agent fills every gap the spec leaves with the statistical middle.

## 2. Websites (portfolio, studio, brand, landing)

- An award case study starts from a felt idea, then technique. Aircord: make visitors
  "feel that 'experience'", through a transition "from 2D to 3D space and back". **[sourced]**
  https://www.awwwards.com/aircord-case-study.html
- Stack named there: three.js (tree-shaken), GSAP, Lenis, Barba.js. **[sourced]** The same
  combination (GSAP + ScrollTrigger/SplitText, Lenis, three.js or OGL, Barba or Swup)
  recurs in Codrops case-study snippets. **[snippet]**
- Costs they name: per-device three.js modules to cut 1 MB on mobile, WebP, video
  quality per device, a web worker for media, staggered loading, frame-rate monitoring
  during development; no framework meant hand-managing JavaScript. **[sourced]** (Aircord)
- Phones often get a different, simpler experience: a feature dropped, gyroscope for
  mouse, effects made static, a map replaced by an image, WebGL code loaded on demand.
  Performance work "takes a long ass time". **[sourced]**
  https://www.awwwards.com/creativity-and-mobile-performance-one-world-one-face-by-adoratorio.html
- 3D performance levers: cap pixel ratio, fewer draw calls, low-resolution shadows, each
  post-processing pass re-renders the scene, instancing, render only when something
  changes, small textures. The page says its tips are not experimentally verified.
  **[sourced]** https://discoverthreejs.com/tips-and-tricks/
- Draw-call and pixel-ratio numbers (under 50 to 200 calls on mobile, ratio 1 to 1.5)
  vary by blog and are unverified. **[snippet]**
- Page-quality thresholds: LCP within 2.5 s, INP 200 ms or less, CLS 0.1 or less, at the
  75th percentile. **[sourced]** https://web.dev/articles/vitals
- **[inferred]** The questions to ask a website owner: what a visitor should feel and
  remember; whether there is one signature moment; what movement is for; what phones and
  weak devices get; how long the first screen may take when the rich version is heavy.

## 3. Apps and tools

- Motion rules: usually under 300 ms; ease-out for responsive UI; a 180 ms dropdown feels
  faster than a 400 ms one; never animate keyboard-initiated actions; things used hundreds
  of times a day get little or no animation; animate transform and opacity. **[sourced]**
  https://emilkowal.ski/ui/great-animations ,
  https://emilkowal.ski/ui/you-dont-need-animations
- Frequently used menus are shown without animation; motion starts from where the thing
  came from; gestures respond immediately; destructive actions wait for the gesture to
  end. **[sourced]** https://rauno.me/craft/interaction-design
- Finish details: visible focus, hit targets 24 px (44 px on mobile), inputs 16 px on
  mobile, buttons keep their label while loading, spinner delay about 150 to 300 ms and
  minimum show time 300 to 500 ms, optimistic updates with rollback or Undo, all states
  designed (empty, sparse, dense, error), errors that guide the exit, specific button
  labels, keyboard works everywhere, animations cancelable, never `transition: all`,
  animate only for cause and effect or deliberate delight. **[sourced]**
  https://vercel.com/design/guidelines
- **[inferred]** In an app or tool, quality reads as speed and completeness of states, not
  spectacle. The questions should ask how often each action happens (that sets how much
  motion it may have) and where the one deliberate delight goes.

## 4. Reduced motion and accessibility

- `prefers-reduced-motion: reduce` means removing non-essential movement; for some people
  "reducing animations is a medical necessity" (dizziness, nausea, migraine). Supported in
  Chrome 74, Edge 79, Firefox 63, Safari 10.1. **[sourced]**
  https://web.dev/articles/prefers-reduced-motion
- Swap, do not strip: replace a bounce with a fade. **[sourced]**
  https://emilkowal.ski/ui/great-animations
- A blanket rule that zeroes all animation also kills spinners and progress bars.
  **[snippet]**
- Games: no essential information by sound alone (basic); option to turn off background
  movement (intermediate); controls remappable (basic); avoid flickering and repetitive
  patterns (basic). Screen shake is not listed by name. **[sourced]**
  https://gameaccessibilityguidelines.com/full-list/

## 5. Games

- Feel is built in order: input, response, context, then polish, "but only what's
  essential"; polish is "a notorious time sink". **[sourced]**
  https://www.gamedeveloper.com/design/game-feel-the-secret-ingredient
- Techniques: screen shake, easing, squash and stretch, landing dust, particles, a
  split-second pause on impact, trails, layered sound. "Used in excess, juicing techniques
  will both waste your time and annoy your users"; foundations first. **[sourced]**
  https://www.gamedeveloper.com/design/squeezing-more-juice-out-of-your-game-design-
- Coyote time (a jump allowed just after leaving a ledge), responsive controls, and the
  test that a game "should feel engaging to play even after the plot, points, level
  design, music, and graphics are removed". **[sourced]**
  https://en.wikipedia.org/wiki/Game_feel
- Shake durations of 50 to 300 ms with decaying amplitude. **[snippet]**
- **[inferred]** This matches the repo's existing GA3 (fun on grey boxes first). What is
  missing is a question about what the main action feels like, and an off switch for
  shake and flashes.

## 6. Simulations and explorable explanations

- "Most interactive widgets dump the user in a sandbox and say 'figure it out for
  yourself'. Those are not explanations." The author must guide; the reader "is not forced
  to interact in order to learn". Techniques: reactive documents, drag-adjustable numbers,
  multiple representations. **[sourced]** https://worrydream.com/ExplorableExplanations/
- Start with a hook; start small, build big; let the explorer make their own data points;
  gate later content on understanding; do not make everything interactive; gamification
  is not a substitute for understanding. **[sourced]**
  https://blog.ncase.me/explorable-explanations/
- Details on demand, "you draw it" prediction before the reveal, linked highlighting
  between formula and text, play, pause and scrub. Costs: each diagram is custom-built,
  mobile and accessibility are hard, code rots. **[sourced, first half of the page read
  verbatim]** https://distill.pub/2020/communicating-with-interactive-articles/
- Only a fraction of readers interact at all. **[sourced via a summary of the second half
  of the same page; lower confidence]**
- Scrubbable numbers, bigger hit areas than the visible dot, showing all variants side by
  side instead of asking for interaction, deterministic output so a slider does not make
  the picture flicker, every section readable as a static page, standard controls for
  accessibility; touch drags fight scrolling and fingers cover the diagram. **[sourced]**
  https://www.redblobgames.com/making-of/little-things/
- **[inferred]** The questions to ask: what the person should understand afterwards that
  they did not before; guided path, free play, or guided then free; what it shows before
  anyone touches it; which numbers people change and how; whether the maths must be
  exact or only look right; whether a state can be saved or sent to someone.
