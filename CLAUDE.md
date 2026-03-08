# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Interactive map of Covent Garden (London) for a guided walking tour, hosted on GitHub Pages. Single-page app with no build system — edit `index.html` and push.

## Tech Stack

- Vanilla HTML/CSS/JS (no framework, no package manager)
- Leaflet.js 1.9.4 (CDN) + OpenStreetMap tiles — lightweight open-source map library (~42 KB) providing tile rendering, markers/popups, geometric shapes, and UI controls. `L` is its global namespace
- All data hardcoded in JS — no external APIs or database

## Architecture

`index.html` contains everything: styles, map initialization, location data, and UI logic.

### JS structure (in order of execution)

1. **Map init** — `L.map` centered on Covent Garden, OpenStreetMap tile layer
2. **`colors` object** — maps étape number (1–5) to hex color, reused in markers, popups, and legend
3. **`createIcon(color, label)`** — returns a `L.divIcon` (HTML/CSS circle with label, not an image)
4. **`places` array** — the data source: each entry has `name`, `addr`, `lat`, `lng`, `step`, `num`
5. **Marker loop** — `forEach` on `places`, creates a colored marker + popup per location
6. **Route polyline** — `L.polyline` in dashed gray connecting all points in array order
7. **Legend control** — `L.control` at top-right, builds DOM with a toggle button (mobile only) and location list. `disableClickPropagation` prevents map interaction through the legend

## Deployment

GitHub Pages serves `index.html` at the repo root. No build step — just `git push`.

## Language

All UI text and documentation are in French.
