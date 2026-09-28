# NourishFlow

[![Quality](https://github.com/MykolaDotsenko/nourishflow/actions/workflows/quality.yml/badge.svg)](https://github.com/MykolaDotsenko/nourishflow/actions/workflows/quality.yml)

**A privacy-first meal planner built with HTML, CSS and native JavaScript — no framework, bundler or production dependencies.**

[**Open NourishFlow →**](https://mykoladotsenko.github.io/nourishflow/) · [Architecture](ARCHITECTURE.md)

![NourishFlow meal-planning interface](https://mykoladotsenko.github.io/nourishflow/img/brand/nourishflow-readme-preview.png)

## Product loop

1. choose Whole-Food, Mediterranean, Plant-Based or Balanced;
2. optionally estimate daily maintenance energy;
3. build Morning, Midday, and Evening meal ideas;
4. switch to another set without losing the selected approach;
5. keep a small shopping starter;
6. save one plan locally or copy it elsewhere;
7. reopen or remove that plan later.

Each approach has a four-week authored rotation. The Monday countdown and the content selection use the same deterministic weekly boundary.

No account, name, phone number or remote plan storage is required. The calculator is presented as an approximate adult maintenance estimate, not medical advice.

## Why native JavaScript here

The application is small enough that the browser platform already provides the pieces it needs:

```text
app.js
  ├── domain/
  │    calculator
  │    meal plans
  │    weekly cycle
  ├── features/
  │    plan
  │    persistence
  │    menu
  │    carousel
  └── ui/
       tabs
       dialog
       plan view
```

`app.js` wires the modules explicitly. There is no global event bus or client state framework.

## Data and persistence

- calculator preferences are versioned;
- saved-plan data can migrate from the previous format;
- a future unknown schema is preserved rather than overwritten;
- users can remove the saved plan or clear all NourishFlow-owned local data;
- weekly meal selection is deterministic for the same approach/week.

## Accessibility

The interface uses native semantics first:

- keyboard-operable vertical tabs;
- native `<dialog>`;
- visible focus states;
- labeled calculator inputs and validation;
- meaningful carousel announcements;
- reduced-motion and forced-colors support;
- 44px interaction baseline;
- mobile checks down to 320 CSS px.

## Image delivery

Meal photography is served as responsive AVIF/WebP with JPEG fallback, intrinsic dimensions and lazy loading below the first visible image.

The optimized variants are reproducible through the repository image script and guarded by automated byte-size checks.

## Stack

- semantic HTML
- modern CSS
- native ES modules
- Web Storage
- Node-based validation/tests
- Playwright
- axe-core
- GitHub Actions / GitHub Pages

There are no production runtime packages.

## Quality

```bash
npm install
npm run check
```

CI covers semantic HTML, responsive/touch journeys, axe scans, Chromium/Firefox/WebKit critical flows and visual captures.

Deployment to GitHub Pages occurs only after the verified commit passes Quality.

## Run locally

Requires Node.js 22+.

```bash
npm install
npm run dev
```

Open `http://127.0.0.1:8080`.

## Scope

NourishFlow intentionally stays small:

- one local saved plan rather than an account database;
- shopping starter rather than inventory automation;
- authored four-week rotation rather than generated nutrition plans;
- an energy estimate for context, not per-meal prescription.

## License

ISC — see [LICENSE](LICENSE).
