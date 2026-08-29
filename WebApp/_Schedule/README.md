# Vincent Weekly Schedule

A single-file, static webpage for a personal weekly schedule (work / gym / breakfast / weekend reading).
No build step — just open `index.html` in a browser, or publish it with GitHub Pages.

## Structure

```
_Schedule/
├── index.html       <- the whole page (HTML + CSS + JS in one file)
├── _assets/
│   ├── gym_*.png     <- the icons actually used by index.html (500x500, transparent PNG)
│   └── _Sources/      <- original/raw exports, duplicates, .psd working file (not used by the page)
└── README.md
```

Icon filenames follow `gym_<exercise_name>.png` (lowercase, underscores, no spaces or dashes) and
are all resized to exactly 500x500px with transparency preserved.

## Editing content

Everything you'd want to change lives in the `DATA` section near the top of the
`<script>` tag in `index.html`:

- `BREAKFASTS` — rotating breakfast ideas
- `GYM_PLAN` — exercise list, sets/reps, starting/target kg, and icons
- `BOOKS` — weekend reading list
- `TIPS` — the small rotating daily tip
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

## Publishing on GitHub Pages

1. Push this folder's contents to a GitHub repo (or a subfolder of one).
2. In the repo settings, enable **GitHub Pages**, pointing at the branch/folder
   containing `index.html`.
3. The page will be live at `https://<username>.github.io/<repo>/`.
