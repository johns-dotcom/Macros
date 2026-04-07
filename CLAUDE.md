# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

Macro Tracker — a mobile-first PWA for tracking daily calories and macronutrients (protein, carbs, fat). No build step, no backend, no framework. Everything is vanilla HTML/CSS/JS in a single `index.html` file.

## Repository & Deployment

- **GitHub**: github.com/johns-dotcom/Macros
- **Hosting**: Railway (live)

## Running Locally

```bash
npx serve .
# or
python3 -m http.server 3000
```

Open `http://localhost:3000`. No build, install, or compile step.

## Architecture

### Single-file app (`index.html`)

The root `index.html` (~900 lines) contains everything: CSS in a `<style>` block, HTML structure, and all JS in a `<script>` block. There is no bundler or module system.

Key sections of the JS:
- **State management**: A single `state` object persisted to `localStorage` under key `macro_v3`. Contains `logs` (keyed by date string `YYYY-MM-DD`), `goals`, `recipes`, `presets`, `weights`, and `customFoods`.
- **`load()` / `save()`**: Read/write state to localStorage. `save()` is called after every mutation.
- **Page routing**: `showPage(name, btn)` toggles `.active` class on page divs and nav buttons. Pages: `log`, `recipes`, `progress`, `settings`.
- **Food search**: `doSearch()` searches a hardcoded `LOCAL_FOODS` array first, then queries the Open Food Facts API (`world.openfoodfacts.org/cgi/search.pl`) for live results.
- **Recipe builder**: Ingredients stored in `builderIngredients[]`, totals computed by `calcBuilderTotals()`.
- **Charts**: Three Chart.js instances (`kcalChart`, `macroChart`, `weightChart`) rendered in `renderCharts()`.

### PWA files (`files/` and `files 2/`)

Two copies of the PWA scaffolding exist: `files/` and `files 2/`. Each contains:
- `manifest.json` — PWA manifest (app name, icons, theme color `#185FA5`)
- `sw.js` — Service worker caching strategy (cache-first with offline fallback)
- `index.html` — A version of the app (manifest path differs from root)
- `README.md` — Setup and deployment docs

The root `index.html` references manifest at `/Macros/manifest.json`; the copies in `files/` reference `manifest.json` (relative). Keep these in mind when changing PWA config.

### Data flow

All data lives in `localStorage`. There is no API for data persistence. The only external API call is to Open Food Facts for food search/barcode lookup (requires internet).

### Styling

CSS uses custom properties (`:root` variables) for theming. Dark mode is automatic via `@media (prefers-color-scheme: dark)`. The app is constrained to `max-width: 440px` for mobile-first layout.
