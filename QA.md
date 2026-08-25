# QA — V3 Conversa Direta

Last technical QA update: 2026-08-25

## Scope

Technical QA only while the prototype is awaiting user validation. No changes to approved UX direction, visual direction, political/civic content, pedagogy, or learning scope.

## Prototype lineage / validation target

### 2026-08-25 stale-preview clarification

A validation-target mismatch was confirmed after the user reported that the published `/preview-v3/` link showed an older version.

- PR #3 (`prototype/v3-conversa-direta`) is still the original V3 conversation prototype and remains open/unmerged.
- `main` has since advanced with newer prototype work, including `preview-motion-v2/` (`Prototype motion v2 with visual reasoning and path drawing` plus its SVG initialization fix).
- Therefore `/preview-v3/` is technically the correct deployment of PR #3, but it is **not the newest prototype experience** in the repository.
- This QA branch must not silently redefine or overwrite `/preview-v3/` with newer product work, because that would change the prototype/UX under review rather than perform infrastructure-only QA.
- Until prototype lineage is intentionally consolidated, treat `/preview-v3/` as the legacy PR #3 validation target and `preview-motion-v2/` as the newer motion prototype living on `main`.

No UX, visual, civic/political content, pedagogy, or learning scope was changed in this clarification.

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

The prototype workflow completed the entire `build` job successfully, including both checkouts, preview assembly, Pages configuration, and artifact upload. The separate `deploy` job then failed before any step started (zero steps, no runner assigned).

This failure pattern was consistent with the `github-pages` environment rejecting `prototype/v3-conversa-direta` via deployment branch protection.

Evidence before the fix:

- Pages build = success;
- deploy = failure before steps;
- artifact creation was therefore no longer the blocker;
- PR #3 remained open and unmerged.

### 2026-08-25 isolated preview environment fix

The preview workflow was changed to use a dedicated `github-pages-preview` deployment environment rather than weakening the protected production `github-pages` environment.

Safe infrastructure-only fix applied on `prototype/v3-conversa-direta`:

- changed only the deploy job environment from `github-pages` to `github-pages-preview`;
- retained the same combined artifact that checks out the current `main` into the public root and adds V3 only at `/preview-v3/`;
- no product HTML, UX, civic content, visual direction, or pedagogy was changed.

### 2026-08-25 successful Pages deployment

The first complete run after the isolated preview-environment fix succeeded.

Run #30 (`32796236415`) results:

- `build` = success;
- `deploy` = success;
- `actions/deploy-pages@v4` found the uploaded `github-pages` artifact;
- GitHub created the Pages deployment for commit `6e920bff1774c0653e0205fcca36f033c1d1f0ab`;
- the deploy action reported `Reported success!`;
- GitHub evaluated the environment URL as `https://tainatownsend.github.io/voto-consciente/`.

Expected PR #3 preview path:

`https://tainatownsend.github.io/voto-consciente/preview-v3/`

Current deployment check:

- GitHub-side Pages deployment status is **success**.
- PR #3 remains open; no merge was performed.
- External DNS resolution for `tainatownsend.github.io` remains unavailable from the current execution environment, so an independent HTTP 200 check cannot yet be completed here.
- The Pages deployment blocker itself is resolved; remaining deployment QA is independent public reachability and confirmation that the production root still serves the current `main` version.
- Because the repository now contains newer motion prototype work on `main`, successful reachability of `/preview-v3/` should not be interpreted as validation of the newest prototype experience.

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

- independently confirm `/preview-v3/` returns HTTP 200 when external DNS resolution is available;
- independently confirm `/preview-motion-v2/` reachability when external DNS resolution is available, because it is the newer prototype path in the repository;
- confirm the public root still serves the current `main` version after preview deploys;
- smoke-test Back/Forward and direct-link **Voltar** behavior after deployment in a real mobile browser;
- smoke-test at narrow mobile width (~320 px), common phones (~375–430 px), tablet, and desktop;
- verify the TSE external link from the deployed page.
