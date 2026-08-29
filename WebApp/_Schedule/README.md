# Vincent Weekly Schedule

A single-file, static webpage for a personal weekly schedule (work / gym / breakfast / weekend reading).
No build step — just open `index.html` in a browser, or publish it with GitHub Pages.

## Structure

```
_Schedule/
├── index.html       <- the whole page (HTML + CSS + JS in one file)
├── _assets/
│   └── gym_*.png     <- the icons actually used by index.html (500x500, transparent PNG)
├── _Backups/          <- timestamped snapshots of index.html, saved before bigger edits
└── README.md
```

(`_Sources/` — the original/raw icon exports, duplicates, and the .psd working file — now lives one
level up, next to `_Schedule/`, since it's not part of the published page.)

Icon filenames follow `gym_<exercise_name>.png` (lowercase, underscores, no spaces or dashes) and
are all resized to exactly 500x500px with transparency preserved.

## Reverting to a previous version

`_Backups/` holds dated copies of `index.html` (e.g. `index_2026-08-29_2112.html`). To roll back,
just copy one of those over `index.html`.

## Editing content

Everything you'd want to change lives in the `DATA` section near the top of the
`<script>` tag in `index.html`:

- `BREAKFASTS` — rotating breakfast ideas
- `GYM_PLAN` — exercise list, sets/reps, starting/target kg, and icons
- `BOOKS` — weekend reading list
- `tips.json` (separate file, not in the script) — the daily tip pool, grouped by category (food, focus, gym, reading)
- `WEEK` — the Mon–Sun schedule blocks

## Using a real photo instead of an emoji icon for an exercise

1. Drop the image into `_assets/`, named `gym_<exercise_name>.png` (lowercase, underscores only),
   resized to 500x500px with a transparent background.
2. In `GYM_PLAN.exercises`, add `img` and `imgFlat: true`:
   ```js
   { icon: "🏋️", img: "_assets/gym_kettlebell_front_squat.png", imgFlat: true, name: "Kettlebell Front Squat", ... }
   ```
   The image replaces the emoji automatically. Leave `img` out to keep the emoji.
   Raw/working source files (other formats, duplicates, .psd) go in `_assets/_Sources/` and aren't referenced by the page.

Currently `_assets/TreadMill.jpg` is wired up for the Treadmill entry.

## A note on tips.json

The daily tip is loaded from `tips.json` via `fetch()`, which browsers only allow over http/https —
not when you double-click `index.html` and open it as a local `file://` page. So:
- On GitHub Pages (or any real web server), it works normally.
- Opened directly as a local file, it silently falls back to a single built-in tip instead of erroring.
- To test it locally with the real tip rotation, run a tiny local server from this folder, e.g.
  `python -m http.server` (Python) or `npx serve` (Node), then open `http://localhost:8000/`.

## Publishing on GitHub Pages

1. Push this folder's contents to a GitHub repo (or a subfolder of one).
2. In the repo settings, enable **GitHub Pages**, pointing at the branch/folder
   containing `index.html`.
3. The page will be live at `https://<username>.github.io/<repo>/`.
