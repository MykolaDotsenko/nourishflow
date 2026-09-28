# NourishFlow

**Figure out what to eat tomorrow without turning meal planning into another project.**

[**Open NourishFlow →**](https://mykoladotsenko.github.io/nourishflow/) · [Architecture](ARCHITECTURE.md)

[![Quality](https://github.com/MykolaDotsenko/nourishflow/actions/workflows/quality.yml/badge.svg)](https://github.com/MykolaDotsenko/nourishflow/actions/workflows/quality.yml)

![NourishFlow meal-planning interface](https://mykoladotsenko.github.io/nourishflow/img/brand/nourishflow-readme-preview.png)

A common meal-planning problem is not:

> “Can an app generate hundreds of recipes?”

It is much simpler:

> **“What am I actually going to eat tomorrow, and what do I need to buy?”**

NourishFlow keeps that decision small.

```text
I do not know what to eat
        ↓
choose a meal approach
        ↓
get Morning / Midday / Evening ideas
        ↓
see a small shopping starter
        ↓
try another set if needed
        ↓
save the plan on this device
```

No account is required. No meal plan is sent to a remote database.

## A normal Sunday-evening scenario

Imagine it is Sunday evening.

You want Monday to be a little more organised, but you do not want to:

- build a seven-day spreadsheet;
- log every ingredient and gram;
- create another account;
- browse dozens of recipes;
- ask an AI for a different meal plan every time;
- spend longer planning food than preparing it.

You open NourishFlow and choose **Mediterranean**.

The app gives you one practical day:

- **Morning**
- **Midday**
- **Evening**
- a small **shopping starter**

If the set does not fit your week, choose another one.

If it does, save it locally and come back later.

That is the core product loop.

## Pick an approach, not a diet program

NourishFlow offers four simple starting points:

- **Whole-Food**
- **Mediterranean**
- **Plant-Based**
- **Balanced**

Each approach has four authored weekly plan variants.

The product does not pretend to generate a medically personalised diet. It gives you a small set of practical meal ideas with enough structure to make tomorrow easier.

The weekly rotation is deterministic, so the same approach and week produce the same baseline plan instead of changing unpredictably on every visit.

## One day is often enough

The app focuses on a **single practical day** rather than a complex multi-week calendar.

Each plan contains:

```text
Morning
Midday
Evening
+
shopping starter
```

This keeps the useful part visible:

> “What will I eat, and what should I have in the kitchen?”

If you want a different combination, **Another Set** moves to the next authored variant without changing your selected meal approach.

## The shopping list starts the job instead of finishing it for you

NourishFlow does not try to become inventory software.

The shopping starter is a short list of ingredients connected to the selected day.

For example, a plan may suggest things such as:

- fruit;
- oats;
- vegetables;
- grains;
- beans;
- yogurt or an alternative;
- a preferred protein choice.

It is a starting point you can adapt to what is already in the kitchen.

## Save the useful plan, not a profile

When a plan works, you can save it in the browser.

NourishFlow does not require:

- a name;
- email;
- phone number;
- login;
- cloud meal history.

The saved record stays on the current device.

You can reopen it later, remove it, or clear NourishFlow-owned local data.

That makes the privacy model easy to explain:

```text
your meal plan
      ↓
your browser
      ↓
your device
```

## Energy estimate is optional context

The calculator exists to provide rough daily energy context for adults who want it.

It uses the revised Harris–Benedict equation with an activity factor and validates the supported input ranges before calculating.

The result is shown as an **estimate**, not a prescription.

It is not required to build a meal plan, and NourishFlow does not turn the number into per-meal calorie targets.

That keeps the calculator in its proper role:

> optional context, not the product's main decision.

## Authored plans instead of random generation

Meal ideas are stored as authored product content rather than generated at runtime.

That gives the product a predictable structure:

```text
meal approach
      +
current weekly cycle
      ↓
authored plan variant
      ↓
three meals + shopping starter
```

There are four variants per approach, and the weekly boundary used by the countdown is the same one used by the plan-selection logic.

This makes the experience testable and repeatable.

## The browser already provides most of what this product needs

NourishFlow ships without a frontend framework or production runtime packages.

The application is built with:

- semantic HTML;
- modern CSS;
- native ES modules;
- Web Storage;
- native browser dialog and form controls.

The code is split by responsibility:

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

`app.js` composes the modules explicitly. There is no global event bus or client-state framework.

## Local data is treated as a boundary

Saved browser data is not trusted blindly.

NourishFlow includes:

- versioned calculator preferences;
- saved-plan validation;
- migration from the previous plan format;
- forward-safe handling of unknown future schemas;
- explicit removal of the saved plan;
- a way to clear NourishFlow-owned local data.

If the browser cannot persist the plan, the UI reports that instead of pretending the save succeeded.

## Accessibility is part of the product flow

The app uses browser-native semantics where they fit:

- keyboard-operable vertical tabs;
- native `<dialog>`;
- labeled calculator fields;
- inline validation;
- meaningful carousel announcements;
- visible keyboard focus;
- reduced-motion support;
- forced-colors fallbacks;
- 44px interaction baseline;
- mobile checks down to 320 CSS px.

The important user journey is tested across Chromium, Firefox and WebKit.

## Images are delivered for real devices

Meal photography is served with:

- AVIF;
- WebP;
- JPEG fallback;
- responsive source sizes;
- intrinsic dimensions;
- lazy loading below the first visible image.

The optimized image variants are reproducible through the repository image pipeline and protected by automated byte-size checks.

## Stack

- semantic HTML
- modern CSS
- native JavaScript / ES modules
- Web Storage
- Node-based tests and validation
- Playwright
- axe-core
- GitHub Actions
- GitHub Pages

**Production runtime dependencies: 0**

## Verification

```bash
npm install
npm run check
```

CI covers:

- JavaScript syntax and static integrity;
- meal-plan and calculator domain rules;
- storage migration and recovery;
- semantic HTML;
- 320px–1440px responsive journeys;
- touch behaviour;
- axe accessibility scans;
- Chromium / Firefox / WebKit critical flows;
- image loading and byte budgets;
- visual audit screenshots;
- SEO/product metadata.

GitHub Pages deploys the exact commit that passed the Quality workflow.

## Run locally

Requires Node.js 22+.

```bash
git clone https://github.com/MykolaDotsenko/nourishflow.git
cd nourishflow
npm install
npm run dev
```

Open `http://127.0.0.1:8080`.

## Scope

NourishFlow stays modest:

- one locally saved plan rather than an account database;
- a shopping starter rather than inventory automation;
- authored meal ideas rather than generated nutrition plans;
- one practical day rather than a complex planning calendar;
- an approximate adult energy estimate for context, not medical or dietary prescription.

## License

ISC — see [LICENSE](LICENSE).
