# Tide — personal productivity app

A single-file productivity app: to-do list, calendar, notes, and a focus timer — all connected.

- **Today** — dashboard with a weekly strip, schedule, tasks due, and pinned notes
- **Tasks** — priorities, due dates, recurring tasks (daily / weekly / monthly)
- **Calendar** — month view; task due dates and events shown as dots; per-day agenda
- **Notes** — two-pane editor with autosave and pin-to-Today
- **Focus** — ring timer that attaches to a task and logs minutes back to it
- **Drag to schedule** — drag any task (grip handle) onto a day in the week strip or month grid

## Structure

The entire app lives in `index.html` — HTML, CSS, and vanilla JS, no build step and no dependencies.

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

It's a static site — drag the folder into Netlify, or deploy via Vercel/Cloudflare Pages.
No build command; output directory is the project root.
