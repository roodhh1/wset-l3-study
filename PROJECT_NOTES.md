# Project Notes — WSET L3 Study Tool

> Internal design notes and handoff documentation for the WSET L3 study tool.
> Useful if you (or a future AI session) want to extend, debug, or rebuild from scratch.

**Live URL:** https://roodhh1.github.io/wset-l3-study/
**Repo:** https://github.com/roodhh1/wset-l3-study
**Built:** April 2026 (with help from Cursor + Claude)
**Exam date:** September 20, 2026, Napa Valley Wine Academy

---

## Goal

A self-contained, single-file HTML study companion for the WSET Level 3 Award in Wines exam. Designed as a *complement* to the official WSET classes/videos/textbook, not a replacement. Optimized for the cause-and-effect "why" reasoning that examiners reward in the SWA section.

## Design principles

1. **Single file** — `index.html` is the entire app. No build step, no dependencies (except Leaflet via CDN). Anyone can fork it, copy it to a USB stick, or open it offline.
2. **Cause-and-effect framing** — content is structured around climate → why → resulting style, mirroring how WSET examiners want answers structured.
3. **Progress is private** — `localStorage` only, never sent anywhere. Export/Import lets users move progress between machines manually.
4. **Mobile-friendly** — works on phone, tablet, laptop.
5. **Offline-first** (95% of features) — only the Maps tab needs internet for tile loading.

## Architecture

The file has 13 inline `<script>` blocks, one per major section, all wrapped in IIFEs. Section pattern:

```javascript
(function() {
  // local data and helpers
  document.getElementById('sec-X').innerHTML = `...`;
})();
```

Sections (in nav order):
- `sec-dashboard` — countdown, 8-week study plan, "how to use" callout
- `sec-lo1` through `sec-lo5` — Learning Outcomes
- `sec-maps` — Leaflet maps (only section needing internet)
- `sec-matrix` — Climate ↔ Grape ↔ Style interactive table
- `sec-tasting` — SAT card + Lexicon + practice mode
- `sec-flash` — flashcards with mastery tracking
- `sec-mock` — MCQs + SWAs
- `sec-extras` — cram sheets, mnemonics, decision trees

Plus a "core" script at the top handling: tabs, theme toggle, localStorage, countdown, export/import.

## Key technical decisions

### Maps: Leaflet + Esri World Topo Map
- **Tried first**: hand-coded SVG schematics — too cramped, hard to read, didn't scale
- **Tried second**: Esri World Terrain — had missing tiles at certain zoom levels ("Map data not yet available")
- **Final**: Esri World Topo Map (full global coverage at every zoom 1-18). Mosel close-up uses Esri World Imagery (satellite) to show the river meanders + slope orientations.
- Tile layer URLs are at the top of the maps `<script>` block.

### Markers: shape encodes status, color encodes climate
- **Circle (●)** = notable sub-region · color = climate
- **Triangle (▲)** = top-tier / premium site · color = climate · gold halo
- 4 climate colors only: cool (#4a90b8), moderate (#6ba85f), warm (#d49032), hot (#c0432e)
- Earlier had a separate "premium" color (burgundy) but it overrode the climate signal — bad UX.

### LocalStorage key
- `wset-l3-progress` — single JSON blob with weeks, flashcards, mcq answers, etc.
- Export/Import buttons in header serialize/deserialize this.

### Map performance
- Maps render only when the Maps tab is active (deferred via `setTimeout` after `innerHTML`).
- Tab-switch event re-calls `invalidateSize()` on Leaflet maps so tiles redraw correctly when the container resizes from `display:none`.
- `scrollWheelZoom` starts disabled — user must click to enable. Prevents accidental zoom while scrolling the page.

## Content sources

All content compiled from these files (originally in `~/Downloads/`, NOT in the repo):
- `1 How to Prepare for the Theory Examination.pdf` (WSET official)
- `2 How to Prepare for the Tasting Examination.pdf` (WSET official)
- `1-L3 Online Practice Theory Questions.pdf` — source of the **50 official MCQs and 3 official SWAs**
- `wset_l3wines_specification_en_highres_may2022_issue2.pdf` — the syllabus
- `WSET_L3_SWA-Guide.pdf` — SWA marking guide
- WSET L3 textbook *Understanding Wines: Explaining Style and Quality* (2022 edition, ISBN 9781913756543) — referenced but not uploaded

Original 50 MCQs marked as `official` in the data; the 150+ extras are AI-generated in the WSET style.

## How to extend

### Add a new wine region to LO2 + Maps + Matrix in one shot
The `REGIONS` array in `sec-lo2` is the canonical source. Add an entry there with the same shape as existing ones (country, climate, grapes, AOCs, styles, why explanation, laws, hazards). The Matrix tab reads from this array automatically. The Maps tab is separate (Leaflet) and needs a new map block added manually.

### Add flashcards
The flashcards module in `sec-flash` programmatically generates cards from the `REGIONS` data + dedicated arrays for each deck (Laws, Winemaking, Faults, etc.). Add to the relevant array.

### Add MCQs
In `sec-mock`, the `MCQS` array is the single source. Each entry has: `q`, `options`, `correct`, `explain`, `lo`, `source` (`'official'` or `'original'`). Filter UI in the rendered HTML.

### Add a new map
In `sec-maps`, copy any existing region block and update: `id`, `title`, `subtitle`, `center` (lat/lng), `zoom`, `keyTakeaway`, then add `addPin` calls inside the wrapped `r.init`. Use `topo` layer for most regions; `sat` for satellite views.

### Update the live site
```bash
cd ~/Documents/WSET-L3
# edit files
git add -A && git commit -m "describe change" && git push
```
GitHub Pages auto-deploys in ~1 minute.

## Conversation/decision history

Key decisions made during the build:

1. **Personal vs work setup** — kept this entirely in `~/Documents/WSET-L3/` (no work repos, no Knowledge Engine integration). Local git identity is `Rodrigo Hernandez <rohernandezh1@gmail.com>`; global git stays work email.

2. **Maps approach went through 3 iterations:**
   - V1: hand-coded SVG schematics → too cramped
   - V2: redesigned SVGs with bigger labels → still couldn't compete with real cartography
   - V3 (final): Leaflet + real basemaps + custom shape/color markers

3. **Footer email removed** post-publication because the tool is shared publicly. Name, LinkedIn, Instagram retained.

4. **Repo published as public** at github.com/roodhh1/wset-l3-study with GitHub Pages on `main` branch root. URL: https://roodhh1.github.io/wset-l3-study/

## Pending / nice-to-haves

If you want to keep iterating, candidates:
- Add a "Daily Challenge" mode that picks 5 random MCQs + 1 random SWA per day
- Add audio pronunciation for tricky region names (Châteauneuf-du-Pape, Sankt Helenstal, etc.)
- Add a settings tab to choose tile layers per map
- Add dark-mode tweaks for maps (currently the satellite view looks fine in dark mode but topo doesn't shift)
- Add Spanish translations for sub-headers (since you're bilingual)
- Add a "compare two regions" view in the matrix
- Add a "WSET L4 prep" sibling tool 😈

## Resurrection guide (if everything explodes)

If the live site breaks or you need to start over from scratch:

```bash
# Re-clone from your personal GitHub
git clone https://github.com/roodhh1/wset-l3-study.git
cd wset-l3-study

# Open index.html directly to test locally
open index.html

# Or serve it from a local web server (better, avoids CORS issues with Leaflet in some browsers)
python3 -m http.server 8000
# then open http://localhost:8000
```

Good luck on 9/20! 🍷
