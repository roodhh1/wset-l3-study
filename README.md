# 🍷 WSET Level 3 Study Tool

A self-contained, single-file HTML study companion for the **WSET Level 3 Award in Wines**.

> **Live tool:** [https://roodhh1.github.io/wset-l3-study/](https://roodhh1.github.io/wset-l3-study/)
>
> *Exam date: September 20, 2026 — Napa Valley Wine Academy*

---

## What's inside

12 sections accessible from the top nav:

| Section | What it covers |
|---|---|
| 📊 **Dashboard** | Countdown, 8-week study plan, exam structure |
| 🌱 **LO1** | Viticulture & winemaking foundations |
| 🌍 **LO2** | All wine regions of the world (heaviest weighting) |
| 🥂 **LO3** | Sparkling wine production & key wines |
| 🍷 **LO4** | Fortified wines (Sherry, Port, Muscat) |
| 🍽 **LO5** | Service, storage, faults, pairing, health |
| 🗺 **Visual Maps** | 20 real interactive geographic maps (Leaflet + OSM) |
| 🔗 **Matrix** | Interactive Climate ↔ Grape ↔ Style explorer |
| 👃 **Tasting (SAT)** | Full SAT card + Lexicon + 14-wine practice mode |
| 🃏 **Flashcards** | 350+ cards across 10 decks (spaced repetition) |
| 📝 **Mock Questions** | 200+ MCQs (50 official + 150+ original) + SWAs with model answers |
| ⭐ **Extras** | 7 deadly mistakes, decision trees, food-pairing matrix, cram sheet |

## How to use it

1. **Open the live URL** above (or download `index.html` and double-click).
2. **Click around** — content is data-driven and structured around examiner-rewarded "cause-and-effect" reasoning.
3. **Track progress**: week checkboxes, flashcard mastery, and MCQ answers all save automatically to your browser's `localStorage`.
4. **Switch machines**: use the **⬇ Export** button (top-right) to download your progress as JSON, then **⬆ Import** on the other device.

## Recommended workflow

This tool is a **complement to your WSET classes and videos** — not a replacement. The official WSET online learning content is the authoritative source for the syllabus.

**Weekly rhythm:**
1. Watch your WSET videos / attend class
2. Read the relevant book chapter
3. Come here to drill flashcards, do MCQs, and practice SWAs on that topic
4. Track progress in the dashboard checklist

## Offline / Online

- **95% works fully offline** — all text, flashcards, MCQs, SWAs, tasting practice
- **Maps tab needs internet** to load Leaflet/OSM tiles
- **"Further reading" links** also need internet

## Tech

- Single-file HTML application — no build step, no installation, no accounts
- Vanilla JavaScript + CSS, no framework
- [Leaflet](https://leafletjs.com/) + OpenStreetMap / Esri tiles for the Maps tab
- All progress persisted in `localStorage`

## Content sources

Compiled from:
- WSET Level 3 Specification (Issue 2, May 2022)
- WSET L3 textbook *Understanding Wines: Explaining Style and Quality* (2022 edition)
- Napa Valley Wine Academy preparation materials provided to candidates
- Official WSET practice MCQs and SWAs

Maps use OpenStreetMap and Esri tiles (free, open). Each region links out to authoritative wine cartography (Wine Folly, GuildSomm, official trade-body maps).

## Author

**Rodrigo Hernandez** · [LinkedIn](https://www.linkedin.com/in/rodrigohdez01/) · Instagram [@roodhh](https://instagram.com/roodhh)

Built for personal study. Use it, fork it, share it. Good luck on your exam! 🍷

## License

MIT — do whatever you want with it.
