# AFL Masters Position Guides

An interactive web app that helps AFL Masters players (over-35s) learn a new position. The home screen is an Australian Football oval with every position marked; tap a position and its full development guide opens in an overlay.

**Live demo:** https://afl-masters.vercel.app

## What it does

- Renders a full AFL ground (oval, centre square and circle, 50m arcs, goal squares) as an SVG.
- Places 18 clickable position markers where players actually line up, from Full Forward down to Full Back.
- Opening a marker loads that position's guide: role summary, positioning and movement, core skills and drills, common mistakes, over-35s conditioning, and what good looks like.

## How it works

Each guide is a plain Markdown file in [`guides/`](guides/). The page does not hard-code any guide text. When a marker is tapped, it fetches the matching `guides/<id>.md` file, converts it to HTML with a small inline parser, and shows it in the modal. The Markdown files are the single source of truth, so adding or editing a guide is just editing a `.md` file.

To add a new position:

1. Add `guides/<id>.md`.
2. Add one entry to the `MARKERS` array in `index.html` (id, abbreviation, label, x/y percentage on the oval).

## Tech

- Single static `index.html`: vanilla HTML, CSS, and JavaScript. No frameworks, no build step.
- Content authored in Markdown and loaded at runtime via `fetch`.

## Running locally

Because the page fetches Markdown files, it needs to be served over HTTP (opening the file directly will block the fetches). Any static server works:

```bash
python3 -m http.server 4321
# then open http://localhost:4321
```

## Deploying

It is a static site, so it deploys anywhere that serves static files (Vercel, Netlify, GitHub Pages). The live demo above runs on Vercel.
