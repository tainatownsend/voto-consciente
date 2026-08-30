# Reels V2 — Adult Editorial Motion QA

## Product direction

- Adult editorial motion, not e-learning UI.
- Silent-first comprehension.
- **Visual-first target: ~70–80% visual / 20–30% text.**
- Real photographic elements + editorial typography + drawn reasoning paths.
- Images are explanatory material, not decorative backgrounds.
- No explanatory beat should require a paragraph to work.
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

Visual sequence:
1. real public problem shown photographically;
2. promise shown as an editorial clipping;
3. civic/institutional image + only the prompt `Quem promete?`;
4. visual comparison `cargo → decisão`, with imagery carrying the relationship;
5. photographic institutional scene + animated path for resources / other actors / control;
6. practical answer: **promessa não é poder**;
7. compact visual recap `promessa → cargo → competência → execução`;
8. explicit bridge to Reel 02.

## Layout + visual hardening applied

- Removed the four-quadrant composition that overlapped on mobile.
- Replaced it with one idea per beat/composition.
- Added a consistent narrative safe area with top reserved for brand/progress and bottom reserved for captions/controls.
- Captions render in a dedicated bottom band; playback controls stay in a separate right-side rail.
- Added explicit light/dark UI states for contrast over photography.
- Replaced paragraph-heavy Cargo/Competência beats with photographic crops and short labels.
- Added a visual `cargo → decisão` relationship instead of explaining it in prose.
- Reduced caption copy and total Reel duration to ~35 seconds.
- Added compact-height overrides for short mobile screens.
- Final takeaway closes the reasoning and bridges explicitly to Reel 02.

## Technical safeguards

- 9:16/mobile-first reel shell with a 560 px minimum usable height.
- autoplay with pause/replay.
- pauses automatically when the document becomes hidden.
- `prefers-reduced-motion` supported.
- production root preserved by the Pages workflow.
- isolated preview path: `/preview-reels-v2/`.
- no merge before user validation.

## Assets

The prototype currently uses remote Unsplash photographs as neutral illustrative editorial material. Before production, replace remote dependencies with locally stored, licensed/attributed final assets and verify political neutrality, accessibility, loading behavior and fallback behavior.

## Pending QA

- confirm newest GitHub Pages deploy and public reachability;
- smoke test at ~320 px, 375 px, 390–430 px widths and shorter mobile heights;
- verify no overlap with iOS in-app browser chrome / safe areas;
- verify caption band and control rail remain separated at all target heights;
- verify remote image loading/fallback behavior;
- verify pause/replay and reduced-motion behavior in Safari/Chrome mobile;
- editorial review for adult visual tone, rhythm and visual continuity;
- institutional/content review before treating the civic example as final;
- user validation of the visual-first grammar before producing Reels 02–08.
