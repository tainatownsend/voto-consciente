# QA — Animated Explainer V1

## Current validation target

- Branch: `prototype/animated-explainer-v1`
- PR: #6 (draft; do not merge before user validation)
- Preview path: `/preview-animated-v1/`

## Deployment

- Latest verified GitHub Actions run #39 completed successfully on 2026-08-26 for commit `af23821480f137111fea9f5cfb4cd13c17e6b0ca`.
- Both `build` and `deploy` jobs completed successfully; the Pages deploy step itself is green.
- Workflow builds a combined Pages artifact while preserving the current `main` site and adding this prototype at `/preview-animated-v1/`.
- Independent HTTP verification from the automation environment remains blocked by DNS resolution for `tainatownsend.github.io`; GitHub-side deployment is healthy.
- A new run was triggered after the browser-navigation fix at commit `29f5d297133d49980a2371a1ae557d4873d96a5c` and should be rechecked before declaring that revision deployed.

## Technical QA completed

- Added `prefers-reduced-motion` handling.
- Inactive animated scenes are hidden from the accessibility tree (`visibility:hidden` + `aria-hidden`) so screen readers do not read every scene at once.
- Moved live announcements to the concise caption region rather than the entire animated stage.
- Added progress semantics (`role=progressbar`, min/max/current value).
- Added explicit accessible state/labels to autoplay play/pause control.
- Decorative directional arrows are hidden from assistive technology.
- Added visible keyboard focus styling and a disabled state for navigation controls.
- Confirmed the prototype uses no external asset URLs, reducing broken-asset risk.
- Added scene hashes (`#scene-1` … `#scene-6`) and History API handling so browser Back/Forward moves through manually visited scenes instead of immediately leaving the explainer. Direct scene URLs now restore the matching scene. Autoplay replaces the current history entry rather than creating six-second history spam.
- Maintained responsive/mobile CSS and no change to approved UX, visual direction, civic content, or pedagogy.

## Pending before approval

- Confirm the workflow run triggered by commit `29f5d297133d49980a2371a1ae557d4873d96a5c` completes successfully.
- Independent public HTTP reachability check for `/preview-animated-v1/`.
- Manual browser/device smoke test after user validates the prototype direction.
- Continue only technical QA until product validation; do not expand learning journeys or merge PR #6.
