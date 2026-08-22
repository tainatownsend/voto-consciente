# QA — V3 Conversa Direta

Last technical QA update: 2026-08-22

## Scope

Technical QA only while the prototype is awaiting user validation. No changes to approved UX direction, visual direction, political/civic content, pedagogy, or learning scope.

## Deployment

- GitHub Pages workflow exists and deploys repository root.
- The prototype branch `prototype/v3-conversa-direta` was not included in the Pages push trigger, so pushes to the current prototype could not deploy a preview.
- Fixed on the prototype branch by adding `prototype/v3-conversa-direta` to the workflow branch trigger.
- Public reachability still needs confirmation after the workflow completes.
- No PR merge performed.

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

- confirm the latest prototype-branch Pages deployment completed successfully and the public URL serves V3;
- smoke-test Back/Forward after deployment in a real mobile browser;
- smoke-test at narrow mobile width (~320 px), common phones (~375–430 px), tablet, and desktop;
- verify the TSE external link from the deployed page.
