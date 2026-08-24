# QA — V3 Conversa Direta

Last technical QA update: 2026-08-24

## Scope

Technical QA only while the prototype is awaiting user validation. No changes to approved UX direction, visual direction, political/civic content, pedagogy, or learning scope.

## Deployment

Meaningful infrastructure issues found and fixed:

- GitHub Pages provides one deployment target per repository. Simply adding `prototype/v3-conversa-direta` to the production Pages workflow meant a push to the prototype branch could replace the public production root with the unvalidated V3.
- The prototype workflow preserves the current `main` site at the public root and publishes V3 under a dedicated preview path.
- The workflow checks out `main` into the deployment root, checks out the prototype separately, copies only the prototype `index.html` into the preview directory, and deploys the combined artifact.
- Corrected the workflow `environment.url`: it uses the Pages deployment output directly.
- Updated `actions/upload-pages-artifact` from v3 to v4 and added `.nojekyll` to the deployed artifact for static-file robustness.
- Repository Settings → Pages → Build and deployment → Source has been set to **GitHub Actions** by the user.
- No PR merge was performed.

### 2026-08-24 route alignment fix

A deployment-path mismatch was found during the latest check:

- the prototype workflow expected `preview/v3/`;
- the current `main` tree already contains the established V3 preview directory `preview-v3/`;
- maintaining two different preview URLs made 404 diagnosis ambiguous and could leave the user testing the wrong route.

Safe infrastructure-only fix applied on `prototype/v3-conversa-direta`:

- standardized the prototype Pages deployment path to `public/preview-v3/index.html`;
- no product HTML, UX, civic content, visual direction, or pedagogy was changed;
- the workflow update itself retriggers Pages.

Expected preview path after this run:

`https://tainatownsend.github.io/voto-consciente/preview-v3/`

Current deployment check:

- PR #3 remains open; no merge was performed.
- External DNS resolution for `tainatownsend.github.io` is unavailable from the current execution environment, so HTTP reachability cannot yet be marked passed from here.
- Do not mark Pages as passed until the deployed preview returns 200 and the production root is confirmed intact.

## Browser navigation

Issue found and fixed:

- Previous implementation used `history.replaceState()` for every lesson step, so browser Back/Forward did not reliably traverse the learning journey.
- Direct reloads on `#passo-N` were not restored on initial page load.

Current behavior:

- entering the journey preserves Home in browser history;
- each Continue action creates a real history entry;
- browser Back/Forward restores the correct lesson without creating duplicate history entries;
- direct `#passo-N` URLs restore the matching step;
- `#concluido` restores the completion screen.

## Accessibility implementation

Safe implementation improvements completed:

- added `aria-live="polite"` to the main dynamic region;
- added accessible labeling/value text to the progress element;
- decorative mode icons remain hidden from assistive technology;
- unavailable Ouvir/Assistir modes expose `aria-disabled="true"`;
- interactive buttons explicitly use `type="button"`;
- focus is moved to the lesson heading when a new lesson is rendered;
- focus-visible styling also covers links.

## Responsive robustness

Current safeguards retained:

- `box-sizing: border-box` globally;
- `min-width: 0` globally to prevent flex/grid overflow;
- `max-width: 100%` and `overflow-x: hidden` on the page;
- mobile-first single-column layout;
- fluid container width using `calc(100% - 28px)`;
- responsive type sizing and a mobile breakpoint at 520px;
- SVG illustrations scale within their containers.

No horizontal-scroll-producing fixed content width was found in this QA pass.

## Assets and links

- V3 uses inline SVG illustrations, eliminating external image asset dependencies for the learning journey.
- TSE footer link remains a normal HTTPS link.
- No broken local asset reference was found in the V3 document.

## Pending technical checks

- confirm the prototype-branch Pages deployment completes successfully and `preview-v3/` serves V3;
- confirm the public root still serves the current `main` version after the preview deploy;
- smoke-test Back/Forward after deployment in a real mobile browser;
- smoke-test at narrow mobile width (~320 px), common phones (~375–430 px), tablet, and desktop;
- verify the TSE external link from the deployed page.
