# Catan Score Tracker

A polished, mobile‑friendly score tracker for **Settlers of Catan** with optional support for **Cities & Knights**, **Seafarers**, and **Traders & Barbarians**. No build step required — just open `index.html`.

## Features
- Players (1–4), rename and color‑tag
- Counters: Settlements, Cities, Victory Cards, (Seafarers) Islands, (T&B) Gold & Harbors
- Derived awards: **Longest Road** (≥5 roads, incumbent advantage), **Harbormaster** (≥3 harbors, incumbent advantage)
- Gold rank bonus: unique max +1, unique min −2
- Metropolises (C&K): Science/Trade/Politics (+2 each), **Merchant** (+1), all globally exclusive
- Reset Scores / Reset All / Clear Save
- State saved to `localStorage`
- Works great on phones, tablets, and desktops. Fullscreen toggle supported.

## Quick Start (GitHub)
1. Create a new repo on GitHub (empty).
2. Download this repo bundle as a ZIP from the link below or drag‑and‑drop the files.
3. Commit `index.html`, `README.md`, `DESIGN_NOTES.md`, `LICENSE`, `.nojekyll` (and `.gitignore` if you want).
4. Enable **GitHub Pages**:
   - Settings → Pages → **Branch: main** → **/ (root)** → Save.
   - Your app will be served at the URL GitHub shows.

## Run Locally
Just open `index.html` in a browser.  
For a local HTTP server (recommended for some browsers):
```bash
# Python 3
python -m http.server 8080
# then open http://localhost:8080
```

## Tech
- Single‑file React (UMD) + Babel via CDN
- Tailwind CDN (no build pipeline)
- System fonts only (no external font fetches)

## Notes
- This repo is static and GitHub Pages ready — no Node needed.
- All logic and UI are self‑contained in `index.html`.

## License
MIT — see `LICENSE`.
