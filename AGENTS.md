# AGENTS.md

Guidance for coding agents working in this repository.

## Agent Quick Start

- Primary target: edit `index.html` and keep current structure/behavior intact.
- No build step exists; use `python3 -m http.server 8000` for local verification.
- No test runner exists; perform manual browser checks after UI/JS changes.
- Keep IDs/classes stable unless every reference is updated.
- Keep styling and scripting patterns consistent with existing inline CSS/JS.
- Do not add frameworks, bundlers, or package tooling unless explicitly requested.
- Check `.cursor/rules/`, `.cursorrules`, and `.github/copilot-instructions.md` when present.
- Prefer the smallest safe change and avoid broad refactors.

## Repository Snapshot

- Project type: static website (single-page HTML with inline CSS and JS).
- Primary file: `index.html`.
- Assets folder: `Images/`.
- CI workflow present: `.github/workflows/opencode.yml`.
- No package manager files detected (`package.json`, `pnpm-lock.yaml`, `pyproject.toml`, etc.).
- No formal test suite detected.
- No formatter/linter configuration files detected.
- No Cursor rules detected (`.cursor/rules/` or `.cursorrules`).
- No Copilot instructions detected (`.github/copilot-instructions.md`).

## Source of Truth

- Treat this document and existing code patterns in `index.html` as the style baseline.
- If the repository later adds config files (ESLint, Prettier, tests), prefer those over this file.
- Do not invent build systems that are not already part of the repo unless explicitly asked.

## Build, Lint, and Test Commands

Current state: there is no configured build/lint/test toolchain.

### Build

- Build command: none required for current static site.
- Deployment-style verification: open `index.html` in a browser and verify layout/behavior.
- Local static server (recommended for realistic checks):
  - `python3 -m http.server 8000`
  - Then open `http://localhost:8000/`.

### Lint

- Lint command: none configured in-repo.
- If linting is requested, propose adding tooling first.
- Optional ad-hoc check if tools are available:
  - `npx htmlhint index.html`
  - `npx stylelint "**/*.html"`

### Test

- Test command: none configured in-repo.
- There are currently no unit/integration/e2e test files.
- Manual test pass is expected after UI/JS changes.

### Running a Single Test (Important)

- Not currently possible in this repository because no test runner is configured.
- If tests are added later, prefer these patterns:
  - Vitest single test file: `npx vitest run path/to/file.test.ts`
  - Vitest by test name: `npx vitest run -t "test name"`
  - Jest single test file: `npx jest path/to/file.test.js`
  - Playwright single spec: `npx playwright test tests/example.spec.ts`
  - Playwright single test title: `npx playwright test -g "test title"`

## Code Style Guidelines

These guidelines are inferred from existing code and should be kept consistent unless asked to refactor.

### HTML

- Use semantic containers where practical (`nav`, `section`, `footer`).
- Keep `id` attributes stable; in-page nav and JS hooks rely on them.
- Use lowercase kebab-case for class names (e.g., `reveal-on-scroll`, `contact-card`).
- Keep heading hierarchy meaningful and sequential.
- Keep attributes quoted with double quotes.
- Use meaningful `alt` text for all non-decorative images.
- If image is purely decorative, keep `alt=""` and avoid redundant wording.

### CSS

- Keep design tokens in `:root` variables where possible.
- Reuse existing variables before adding new color values.
- Group styles by section with clear comment headers.
- Keep specificity moderate; prefer class selectors over deep selector chains.
- Preserve existing breakpoints unless change requires new ones.
- Avoid `!important` unless unavoidable and justified.
- Keep transitions purposeful and subtle.

### JavaScript

- Use `DOMContentLoaded` wrapper for DOM-dependent logic.
- Keep DOM queries cached in local constants when reused.
- Guard optional elements before binding events.
- Preserve existing behavior for mobile nav toggle and smooth scroll.
- Do not introduce heavy dependencies for simple DOM behavior.

## Imports and Dependencies

- Current external dependencies are CDN links in `index.html`:
  - Google Fonts
  - Font Awesome
- No module import system exists in-repo.
- If adding dependencies, prefer minimal, browser-safe additions.
- If adding npm-based tooling, document commands in this file.

## Formatting Conventions

- Use spaces for indentation (current file uses 4-space indentation in CSS/JS blocks).
- Keep line length reasonable for readability (target under ~120 chars when practical).
- Keep one blank line between major sections.
- Preserve readable alignment in multiline CSS/JS blocks.

## Types and Data Modeling

- There is no TypeScript or typed schema layer at present.
- If adding script complexity, prefer JSDoc annotations before introducing TS toolchain.
- Keep data structures simple and local to the feature scope.

## Naming Conventions

- CSS classes: kebab-case.
- JS variables/functions: camelCase.
- Constants that never reassign: `const` with descriptive camelCase names.
- Section IDs: kebab-case aligned with nav targets.
- File names for new static assets: lowercase kebab-case.

## Error Handling and Resilience

- Fail gracefully when optional DOM elements are missing.
- Wrap risky DOM interactions in existence checks.
- Prefer no-op fallback behavior over hard failure in UI scripts.
- Use browser console logging sparingly and only when helpful.

## Accessibility and UX Guardrails

- Keep interactive elements keyboard-usable.
- Maintain sufficient color contrast for text over backgrounds.
- Preserve `aria-label` usage where present.
- Do not remove focusability from actionable controls.
- Ensure mobile nav remains operable and understandable.

## Performance and Asset Practices

- Optimize new images before adding them to `Images/`.
- Prefer modern formats when possible without breaking compatibility.
- Avoid oversized background assets where lighter alternatives exist.
- Keep JS lightweight and avoid unnecessary reflows.

## Git and Change Hygiene

- Keep edits scoped to requested tasks.
- Do not reformat unrelated sections of `index.html` without request.
- Avoid renaming classes/IDs unless all references are updated.

## Cursor and Copilot Rule Status

- `.cursor/rules/`: not found.
- `.cursorrules`: not found.
- `.github/copilot-instructions.md`: not found.
- If these files are added later, merge their instructions into future agent behavior.

## When Unsure

- Prefer smallest safe change.
- Preserve current structure and behavior.
- Document assumptions in PR/commit notes.
- Ask for explicit direction before introducing new tooling.
