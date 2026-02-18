# 2026DigitalRain

A lightweight, static “digital rain” / Matrix-style screen built with HTML + CSS animations.

- No build step, no JavaScript
- CSS-driven falling columns, scanlines, vignette, and subtle flicker
- Respects `prefers-reduced-motion`

## Project Structure

- `index.html` — markup for the columns/streams of characters
- `styles.css` — all styling + animation keyframes
- `meta.json` — project metadata (art name + author handle)

## Run Locally

### Option A: Open the file directly

Double-click `index.html` (or drag it into a browser window).

### Option B: Serve via your local web server

If you already have a local web server pointed at this folder, open the site URL it provides.

In this workspace, there is a VS Code task named **Open in Browser** that opens:

- `http://2026digitalrain.localhost/`

(That hostname needs to resolve to your local server setup.)

## Notes / Tweaks

Common places to adjust the look/performance:

- Column density: `.matrix { grid-template-columns: repeat(300, 1fr); }` in `styles.css`
- Text size: `.stream { font-size: 12px; line-height: 12px; }`
- Speed/opacity variance: inline CSS variables on each `.stream` element (`--dur`, `--delay`, `--opa`)

## Metadata

`meta.json` contains:

- `artName` — display name of the piece
- `githubHandle` — author handle
