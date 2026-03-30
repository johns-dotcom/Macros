# Macro Tracker

A mobile-first PWA for tracking daily macros and calories. No backend required — all data lives in localStorage.

## Features
- **Food log** with daily history (swipe between days)
- **Barcode scanner** — type any UPC/EAN barcode to pull nutrition data from Open Food Facts (free, no API key)
- **Food search** — local database + Open Food Facts live search
- **Recipe builder** — combine ingredients, set servings, save as loggable items
- **Meal presets** — save a day's log as a named preset, re-log it in one tap
- **Progress charts** — 7-day calorie and macro trends (Chart.js)
- **Body weight log** — with chart + history
- **Custom goals** — editable kcal/P/C/F targets
- **Dark mode** — automatic via prefers-color-scheme
- **PWA** — installs to home screen, works offline

## Setup

### Run locally
```bash
# Any static server works — e.g.:
npx serve .
# or
python3 -m http.server 3000
```
Then open http://localhost:3000

### Deploy to Vercel (recommended)
1. Push this folder to a GitHub repo
2. Go to vercel.com → New Project → import the repo
3. No build step needed — it's a static site
4. Vercel gives you a live HTTPS URL

### Install as PWA on iPhone
1. Open the Vercel URL in Safari
2. Tap the Share button → "Add to Home Screen"
3. Name it and tap Add

### Install as PWA on Android
1. Open the URL in Chrome
2. Chrome will show a prompt to install, or use menu → "Add to Home Screen"

## Adding icons
Generate icons at https://realfavicongenerator.net and drop `icon-192.png` and `icon-512.png` into this folder.

## Notes
- Barcode lookup requires internet (Open Food Facts API)
- All other data persists in localStorage — no account needed
- If you want multi-device sync, wire up a Supabase backend later
