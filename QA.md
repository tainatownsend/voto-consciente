# QA — Animated Explainer V1

## Current validation target

- Branch: `prototype/animated-explainer-v1`
- PR: #6 (draft; do not merge before user validation)
- Preview path: `/preview-animated-v1/`

## Deployment

- Latest GitHub Actions run #37 completed successfully on 2026-08-26 for commit `28efbd2f73e7f5f91a4adab1f3c053869b29512e`.
- Workflow builds a combined Pages artifact while preserving the current `main` site and adding this prototype at `/preview-animated-v1/`.
- Independent HTTP verification from the automation environment is currently blocked by DNS resolution for `tainatownsend.github.io`; GitHub-side deployment remains green.

## Technical QA completed

- Added `prefers-reduced-motion` handling.
- Inactive animated scenes are hidden from the accessibility tree (`visibility:hidden` + `aria-hidden`) so screen readers do not read every scene at once.
- Moved live announcements to the concise caption region rather than the entire animated stage.
- Added progress semantics (`role=progressbar`, min/max/current value).
- Added explicit accessible state/labels to autoplay play/pause control.
- Decorative directional arrows are hidden from assistive technology.
- Added visible keyboard focus styling and a disabled state for navigation controls.
- Maintained responsive/mobile CSS and no change to approved UX, visual direction, civic content, or pedagogy.

## Pending before approval

- Independent public HTTP reachability check for `/preview-animated-v1/`.
- Manual browser/device smoke test after user validates the prototype direction.
- Continue only technical QA until product validation; do not expand learning journeys or merge PR #6.
