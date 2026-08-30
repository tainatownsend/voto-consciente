# Reels V2 — Adult Editorial Motion QA

## Product direction

- Adult editorial motion, not e-learning UI.
- Silent-first comprehension.
- Real photographic elements + editorial typography + drawn reasoning paths.
- No emoji-led storytelling, cartoon people, playful bounce, or school-card visual language.
- A frozen frame should read as an editorial composition, not a course slide.
- One idea per composition.

## Narrative architecture

North Star: teach the user to trace whether a political promise can realistically be transformed into public action.

Reusable grammar:

**Hook → concrete case → visual explanation → practical rule/answer → explicit bridge to the next Reel**

No Reel ends on a question whose answer is not delivered or clearly handed to the next Reel.

Series map is documented in `NARRATIVE_ARCHITECTURE_V1.md`. Only Reel 01 is in production scope until the pilot is validated.

## Current pilot — Reel 01: A promessa

Question resolved: can someone simply promise something and make it happen?

Sequence:
1. concrete public problem;
2. apparently simple promise;
3. cargo — who is making the promise?;
4. competência — can that office decide this?;
5. reveal that execution may also depend on resources, other actors, approval and oversight;
6. practical answer: **promessa não é poder**;
7. explicit bridge: next Reel explains the real role of the office.

## Layout hardening applied

- Removed the four-quadrant composition that overlapped on mobile.
- Replaced it with one idea per beat/composition.
- Added a consistent narrative safe area with top reserved for brand/progress and bottom reserved for captions/controls.
- Added fluid typography and compact-height overrides for shorter mobile screens.
- Captions are now rendered in a dedicated bottom band instead of competing with the story canvas.
- Playback controls stay in their own right-side rail and no longer sit on top of caption text.
- Added explicit light/dark UI states so the brand and progress bar maintain contrast over photography.
- Reduced dead space in text-only beats by moving the main idea higher and adding editorial continuity devices (`promise-thread`, giant keyword, logic strip).
- Added persistent visual continuity between beats: problem → promise → cargo → competence → dependencies → rule.
- Final takeaway includes a dedicated bridge zone above the controls.

## Technical safeguards

- 9:16/mobile-first reel shell with a 560 px minimum usable height.
- autoplay with pause/replay.
- pauses automatically when the document becomes hidden.
- `prefers-reduced-motion` supported.
- production root preserved by the Pages workflow.
- isolated preview path: `/preview-reels-v2/`.
- no merge before user validation.

## Assets

The prototype uses two remote Unsplash photographs as neutral illustrative editorial material (hospital/public infrastructure and civic architecture). Before production, replace remote dependencies with locally stored, licensed/attributed final assets and verify political neutrality, accessibility, loading behavior and fallback behavior.

## Pending QA

- confirm newest GitHub Pages deploy and public reachability;
- smoke test at ~320 px, 375 px, 390–430 px widths and shorter mobile heights;
- verify no overlap with iOS in-app browser chrome / safe areas;
- verify caption band and control rail remain separated at all target heights;
- verify remote image loading/fallback behavior;
- verify pause/replay and reduced-motion behavior in Safari/Chrome mobile;
- editorial review for adult visual tone, rhythm and visual continuity;
- institutional/content review before treating the civic example as final;
- user validation of the hybrid grammar before producing Reels 02–08.
