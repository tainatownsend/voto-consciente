# QA — V3 Conversa Direta

Last technical QA update: 2026-08-25

## Scope

Technical QA only while the prototype is awaiting user validation. No changes to approved UX direction, visual direction, political/civic content, pedagogy, or learning scope.

## Deployment

Meaningful infrastructure issues found and fixed:

- GitHub Pages provides one deployment target per repository. Simply adding `prototype/v3-conversa-direta` to the production Pages workflow meant a push to the prototype branch could replace the public production root with the unvalidated V3.
- The prototype workflow preserves the current `main` site at the public root and publishes V3 under a dedicated preview path.
- The workflow checks out `main` into the deployment root, checks out the prototype separately, copies only the prototype `index.html` into the preview directory, and deploys the combined artifact.
- Corrected the workflow `environment.url`: it uses the Pages deployment output directly.
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

### 2026-08-24 build/deploy dependency fix

The Pages workflow still used a single job for artifact upload and deployment. GitHub's current custom Pages workflow guidance expects deployment to depend on the build/upload job so the Pages artifact is available before `deploy-pages` runs.

Safe infrastructure-only fix applied on `prototype/v3-conversa-direta`:

- split the workflow into `build` and `deploy` jobs;
- `deploy` now declares `needs: build`;
- the Pages artifact is uploaded in the build job before deployment starts;
- no product HTML, UX, civic content, visual direction, or pedagogy was changed.

### 2026-08-24 Pages artifact version fix

The workflow used `actions/upload-pages-artifact@v4` together with `include-hidden-files: true`. That option was added to `upload-pages-artifact` in v5, while v4 excluded dotfiles by design.

Safe infrastructure-only fix applied on `prototype/v3-conversa-direta`:

- upgraded `actions/upload-pages-artifact` from v4 to v5;
- retained `include-hidden-files: true` so `.nojekyll` is actually preserved in the uploaded Pages artifact;
- no product HTML, UX, civic content, visual direction, or pedagogy was changed;
- this commit retriggers the Pages workflow.

### 2026-08-25 github-pages environment protection blocker

The latest workflow run for the prototype branch completed the entire `build` job successfully, including both checkouts, preview assembly, Pages configuration, and artifact upload. The separate `deploy` job then failed before any step started (zero steps, no runner assigned).

This failure pattern is consistent with the `github-pages` environment rejecting `prototype/v3-conversa-direta` via deployment branch protection. GitHub Pages environments are commonly created with the default branch allowed, while environment protection rules can block other refs before a deploy job starts.

Current evidence:

- latest Pages run: build = success;
- deploy = failure before steps;
- artifact creation is therefore no longer the blocker;
- PR #3 remains open and unmerged.

Required repository-setting check:

- Settings → Environments → `github-pages` → Deployment branches and tags;
- allow `prototype/v3-conversa-direta` explicitly, or use **No restriction** if that matches the intended repository policy;
- keep Settings → Pages → Source = **GitHub Actions**.

This setting cannot be changed through the currently available connected GitHub actions, so user/admin input is required before another Pages deploy can succeed.

Expected preview path after the environment rule permits the prototype branch:

`https://tainatownsend.github.io/voto-consciente/preview-v3/`

Current deployment check:

- PR #3 remains open; no merge was performed.
- External DNS resolution for `tainatownsend.github.io` is unavailable from the current execution environment, so HTTP reachability cannot yet be marked passed from here.
- Do not mark Pages as passed until the deployed preview returns 200 and the production root is confirmed intact.

## Browser navigation

Issues found and fixed:

- Previous implementation used `history.replaceState()` for every lesson step, so browser Back/Forward did not reliably traverse the learning journey.
- Direct reloads on `#passo-N` were not restored on initial page load.
- A direct deep link such as `#passo-4` restored correctly, but the in-page **Voltar** button treated that restored state as if it had an earlier Voto Consciente history entry. On a fresh tab it could therefore call `history.back()` and leave the site instead of moving to the previous lesson.

Current behavior:

- entering the journey preserves Home in browser history;
- each Continue action creates a real internal history entry;
- browser Back/Forward restores the correct lesson without creating duplicate history entries;
- direct `#passo-N` URLs restore the matching step;
- direct-link restored states are marked as external/non-internal history, so the in-page **Voltar** button moves to the preceding lesson (or Home) instead of leaving the site;
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

- user/admin: allow `prototype/v3-conversa-direta` to deploy to the `github-pages` environment (or remove that environment branch restriction if appropriate);
- confirm the next prototype-branch Pages deployment completes successfully and `preview-v3/` serves V3;
- confirm the public root still serves the current `main` version after the preview deploy;
- smoke-test Back/Forward and direct-link **Voltar** behavior after deployment in a real mobile browser;
- smoke-test at narrow mobile width (~320 px), common phones (~375–430 px), tablet, and desktop;
- verify the TSE external link from the deployed page.
