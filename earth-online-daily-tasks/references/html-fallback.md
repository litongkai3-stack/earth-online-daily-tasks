# HTML fallback

Use this path only when the current agent cannot access a native image-generation tool. The output is a publishable, standalone HTML card—not a degraded preview and not a reason to skip the daily record.

## Procedure

1. Inspect the supplied reference image. Carry over its broad visual cues where the CSS variables permit: border color, sky/ground balance, text density, and safe zones. Use a fixed 3:4 canvas (the bundled template uses 1242 × 1656) inside a scale-to-fit stage so browser size never changes the intended layout. Never reuse the reference's earlier task copy.
2. Copy `assets/fallback-card.html` to `.earth-online-daily-tasks/output/YYYY-MM-DD.html` (or `-v2.html` for a same-date visual revision).
3. Replace **only** the JSON values in the `earth-online-card-data` script block: `date`, three `coreTasks`, `eggLines`, and `footer`. Preserve valid JSON escaping.
4. Optionally tune the CSS custom properties at the top of the copied file to better match the reference's palette. Keep contrast high and preserve the layout hierarchy.
5. Open or render the copied HTML when a browser/viewer is available. Check it against the quality checklist, then create/update the Markdown record using the `.html` card path.

## Constraints

- The fallback must work offline as a single file; do not load web fonts, scripts, images, or CSS from a CDN.
- Do not embed the reference image as a background: it may contain old date/task text and is only a visual guide.
- Keep `date` as eight digits. Preserve exactly three core tasks, one egg task (one or two lines), and the required footer prefix.
- Do not attempt a PNG export unless a local renderer is genuinely available. Returning the standalone HTML is the correct fallback output.
