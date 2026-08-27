# Reels V2 — Adult Editorial Motion QA

## Product direction

- Adult editorial motion, not e-learning UI.
- Silent-first comprehension.
- Real photographic elements + editorial typography + drawn reasoning paths.
- No emoji-led storytelling, cartoon people, playful bounce, or school-card visual language.
- A frozen frame should read as an editorial composition, not a course slide.

## Current pilot

Topic: evaluate whether a political promise fits the responsibilities of a public office.

Sequence:
1. concrete public problem;
2. apparently simple promise;
3. trace the decision path: office → competence → resources/execution → approval/oversight;
4. show that public decisions can involve different functions/branches/levels;
5. return to the promise with the critical question;
6. close with the rule: understand the job before choosing the person.

## Technical safeguards

- 9:16 mobile-first reel shell.
- autoplay with pause/replay.
- pauses automatically when the document becomes hidden.
- `prefers-reduced-motion` supported.
- production root preserved by the Pages workflow.
- isolated preview path: `/preview-reels-v2/`.
- no merge before user validation.

## Assets

The prototype uses two remote Unsplash photographs as neutral illustrative editorial material (hospital/public infrastructure and civic architecture). Before production, replace remote dependencies with locally stored, licensed/attributed final assets and verify political neutrality, accessibility, and loading behavior.

## Pending QA

- confirm GitHub Pages deploy success and public reachability;
- smoke test at ~320, 375–430 px widths and desktop framing;
- verify image loading/fallback behavior;
- verify pause/replay and reduced-motion behavior in Safari/Chrome mobile;
- editorial review for adult visual tone;
- institutional/content review before treating the civic example as final.
