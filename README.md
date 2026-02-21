# Digital Rain

A lightweight, static “digital rain” / Matrix-style screen built with **HTML + CSS animations**.

Live preview: https://digitalrain.fcjamison.com/

## What This Is

This project renders a Matrix-style effect without JavaScript:

- The “rain” is **pre-authored HTML**: each column contains a `.stream` with characters separated by `<br>`.
- The motion is **pure CSS**: each stream animates vertically using `@keyframes fall`.
- Atmosphere is handled by **CSS overlays** (scanlines, vignette, subtle flicker).

## Features

- No build step
- No JavaScript
- CSS-driven falling columns + scanlines + vignette + subtle flicker
- Respects `prefers-reduced-motion` (disables the falling animation and flicker)

## Project Layout

- `index.html` — markup for the columns/streams of characters
- `styles.css` — styling + animation keyframes + motion preferences
- `meta.json` — metadata for the piece (name + author handle)

## Local Development

Because it’s static, you can either open the file directly or serve it from a local web server.

### Option A: Open directly

Open `index.html` in a browser (double-click or drag into the window).

### Option B: Serve locally (recommended)

Serving avoids any browser quirks around local file URLs and more closely matches production hosting.

Pick one:

- Python: `python -m http.server 8000`
- Node: `npx serve .`
- PHP: `php -S localhost:8000`

Then open `http://localhost:8000/`.

### VS Code task in this workspace

This workspace includes a task named **Open in Browser** that opens:

- `http://digitalrain.localhost/`

That hostname must be mapped to a local server in your environment (it’s not created by this repo).

## How It Works (Developer Notes)

### Streams and per-stream tuning

Each stream is a `.stream` element with inline CSS variables that randomize the motion/opacity:

- `--dur` — animation duration (e.g. `4.72s`)
- `--delay` — negative delay to “seed” the stream at a random point in the animation
- `--opa` — per-stream opacity multiplier

These variables are read by `.stream` in `styles.css`:

- `animation: fall var(--dur, 8s) linear infinite;`
- `animation-delay: var(--delay, -3s);`
- `opacity: var(--opa, .9);`

### Column density

The overall density is controlled by the grid on `.matrix`:

- `grid-template-columns: repeat(300, 1fr);`

Reducing that number makes fewer columns (faster/less dense). Increasing it makes the rain denser.

### Typography and glow

Primary knobs in `styles.css`:

- `.stream { font-size: 12px; line-height: 12px; }`
- `.stream { color: rgba(0, 255, 102, .42); }`
- `.stream { text-shadow: 0 0 6px rgba(0, 255, 100, .45); }`
- `.head { color: rgba(235, 255, 245, .95); }` (the leading “bright” character)

### Accessibility / reduced motion

In `styles.css`, the `@media (prefers-reduced-motion: reduce)` block disables:

- the falling stream animation
- the vignette flicker animation

If you add new animations, include them in the same media query so motion-reduction stays consistent.

## Deployment

This is a static site. Deploy by uploading `index.html` + `styles.css` (and optionally `meta.json`) to any static host:

- GitHub Pages
- Netlify / Vercel
- S3 / Cloudflare Pages
- Any standard web server (Apache/Nginx)

No build output is produced; what you see in the repo is what you deploy.

## Metadata

`meta.json` contains:

- `artName` — display name of the piece
- `githubHandle` — author handle
