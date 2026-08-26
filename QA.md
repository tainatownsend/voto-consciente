# QA — Animated Explainer V1

## Current validation target

- Branch: `prototype/animated-explainer-v1`
- PR: #6 (draft; do not merge before user validation)
- Preview path: `/preview-animated-v1/`

## Deployment

- Latest verified GitHub Actions run #48 completed successfully on 2026-08-26 for commit `6661c3e9701b9324a14bcccee7d98ce36e4daa4a`.
- Both build and deploy are green on the GitHub side for the current branch head.
- Workflow builds a combined Pages artifact while preserving the current `main` site and adding this prototype at `/preview-animated-v1/`.
- Independent HTTP verification from the automation environment remains blocked by temporary DNS resolution failure for `tainatownsend.github.io`; this is not a GitHub Actions deployment failure.

## Technical QA completed

- Added `prefers-reduced-motion` handling.
- Inactive animated scenes are hidden from the accessibility tree (`visibility:hidden` + `aria-hidden`) so screen readers do not read every scene at once.
- Moved live announcements to the concise caption region rather than the entire animated stage.
- Added progress semantics (`role=progressbar`, min/max/current value).
- Added explicit accessible state/labels to autoplay play/pause control.
- Decorative directional arrows are hidden from assistive technology.
- Added visible keyboard focus styling and a disabled state for navigation controls.
- Confirmed the prototype uses no external asset URLs, reducing broken-asset risk.
- Added scene hashes (`#scene-1` … `#scene-6`) and History API handling so browser Back/Forward moves through manually visited scenes instead of immediately leaving the explainer. Direct scene URLs restore the matching scene. Autoplay replaces the current history entry rather than creating six-second history spam.
- Fixed the in-app `Voltar` interaction with browser history: it now consumes existing in-app history when available and safely steps backward with `replaceState` for direct deep links.
- Maintained responsive/mobile CSS and no change to approved UX, visual direction, civic content, or pedagogy.

## Technical observations for a later safe hardening pass

- On very narrow viewports, the three-button controls row should be smoke-tested for wrapping/overflow rather than assumed from the current flex sizing.
- Autoplay currently continues while the document is in a background tab; pausing it on `visibilitychange` would avoid returning to an unexpectedly advanced scene.
- Fixed-height stage plus `overflow:hidden` should be smoke-tested with browser text zoom / large text settings to ensure scene content cannot be clipped on small screens.
- These are implementation-only items and must not change the approved UX/content direction.

## Pending before approval

- Independent public HTTP reachability check for `/preview-animated-v1/` once DNS resolution is available from the automation environment.
- Manual browser/device smoke test after user validates the prototype direction.
- Continue only technical QA until product validation; do not expand learning journeys or merge PR #6.
