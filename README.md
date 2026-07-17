# Tide — personal productivity app

A single-file productivity app: to-do list, calendar, notes, and a focus timer — all connected.

- **Today** — dashboard with a weekly strip, schedule, tasks due, and pinned notes
- **Tasks** — priorities, due dates, recurring tasks (daily / weekly / monthly)
- **Calendar** — month view; task due dates and events shown as dots; per-day agenda
- **Notes** — two-pane editor with autosave and pin-to-Today
- **Focus** — ring timer that attaches to a task and logs minutes back to it
- **Drag to schedule** — drag any task (grip handle) onto a day in the week strip or month grid

## Structure

The app itself lives entirely in `index.html` (HTML, CSS, vanilla JS, no build step).
Also included: `manifest.json` and icon PNGs so the app gets a proper icon and name when
added to a phone home screen (Add to Home Screen / PWA install).

## Run locally

Open `index.html` directly in a browser, or serve it:

```
npx serve .
```

## Data & persistence

Data saves automatically to the browser's localStorage (key `tide-data-v1`), so it persists
between sessions per browser/device. When run inside a Claude.ai artifact it also uses the
artifact storage API. There is no backend — for cross-device sync you would need to add one
(e.g. Supabase).

## Deploy

Static site — drag the folder into Netlify, or deploy via Vercel/Cloudflare Pages/GitHub Pages.
No build command; output directory is the project root. Keep `index.html`, `manifest.json`,
and the icon PNGs all at the root level (not nested) so the icon links resolve correctly.
