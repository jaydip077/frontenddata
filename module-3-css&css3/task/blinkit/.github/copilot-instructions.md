<!--
Repository: module-3-css-css3 / blinkit (frontend-only static project)
Purpose: Short, actionable instructions to help AI coding agents be productive in this codebase.
-->

# Copilot instructions — Blinkit (small static frontend)

Keep this short and specific. This repo is a small static frontend with HTML, CSS, Less and SCSS source files under `assets/`. There is no package.json, build script, or server provided. Treat edits as local static changes unless the user adds a build tool.

Key facts
- Single HTML entry: `Blinkit.html` (top-level). It links `assets/CSS/style.css` and `main.js` (the JS file is referenced but not present in the repo root).
- Styling sources: compiled CSS lives in `assets/CSS/`. Authoring sources exist in `assets/less/` and `assets/scss/`.
- Font assets and images are under `assets/fonts/` and `assets/images/`.

What an agent should assume and do first
- Assume this is a static project meant to be edited and previewed in-browser. Use the filesystem and browser preview rather than running a build unless the user adds a toolchain.
- If you need a tooling step (sass/less compilation, bundling), ask the user whether they want us to add a simple npm workflow (package.json + scripts) or perform one-off compilation locally and commit the compiled CSS.

Project-specific patterns and conventions
- CSS is authored both as compiled CSS (`assets/CSS/style.css`) and as sources in `assets/less/` and `assets/scss/`. Changes to source files (LESS/SCSS) will not affect `Blinkit.html` until compiled and the compiled CSS replaced/updated in `assets/CSS/`.
- Many `.less` and `_*.scss` files mirror FontAwesome parts. Keep FontAwesome source changes isolated — there are already compiled `font-awesome.css` and `font-awesome.min.css` in `assets/CSS/`.
- The HTML references `main.js` at the repo root. If implementing JS, prefer creating `main.js` at the repo root (next to `Blinkit.html`) rather than changing the HTML path, unless the user asks otherwise.

Editing and commit guidance for agents
- When editing visual styles, prefer editing the source in `assets/scss/` or `assets/less/` and then update the compiled files in `assets/CSS/` as part of the same change. If you cannot run the compiler, clearly mark the compiled artifact as manually edited in the commit message.
- Keep CSS selectors scoped to the element with id="navbar" or to new classes to avoid global style regressions. Example selector used in this project: [id="navbar"] strong, [id="navbar"] input, [id="navbar"] p, [id="navbar"] button { width: 20%; }.

What to look for when making changes
- Broken references: `Blinkit.html` references `main.js` which may be missing — ensure any new JS is placed at the referenced path or update the HTML and explain the change in the PR description.
- Consistency between source and compiled CSS: If you update `assets/less/` or `assets/scss/`, update the corresponding `assets/CSS/` files or note why you didn't (e.g., adding a new build step).

Common tasks an agent will be asked to do (how to proceed)
- Add a visual change to the site: edit `assets/CSS/style.css` (fast) or edit `assets/scss/_core.scss` or `assets/less/core.less` and compile (preferred). Ask whether to add npm scripts for tooling.
- Add JS behavior: create `main.js` next to `Blinkit.html` and keep logic minimal and unobtrusive. Avoid changing the page structure unless requested.
- Introduce a build tool: propose adding a minimal `package.json` with devDependencies for `sass` or `less` and scripts `build:css` and `watch:css`. Do not add automatically without user confirmation.

Examples from this repo
- HTML entry: `Blinkit.html` — single-page, links `assets/CSS/style.css` and `main.js`.
- Compiled style: assets/CSS/style.css shows global resets and a navbar layout on the element with id="navbar" (display:flex).
- Source snippet: `assets/less/core.less` contains FontAwesome mixins and variables.

Do not invent behavior not visible in the repository
- The repo contains no CI, tests, or server. Do not add CI or server code without explicit instruction.

If you need more context
- Ask the user for intended workflow (live dev server? npm build?). If they want a build step, propose the smallest change (package.json + two scripts) and request permission to modify the repo.

End of instructions.
