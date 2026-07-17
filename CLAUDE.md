# Tide — project context for AI agents

Single-file static web app (`index.html`) — a personal productivity app with tasks,
calendar, notes, and a focus timer. No framework, no build step: plain HTML + CSS + vanilla JS
in one file. Keep it that way unless the owner asks otherwise.

## Architecture (all inside index.html)

- **State**: one `state` object — `{tasks, events, notes, sessions, settings}` — serialized
  to a single storage key `tide-data-v1`.
- **Persistence**: layered — `window.storage` (Claude artifact API) if present, then
  `localStorage`, then in-memory. Saves are debounced 350ms via `save()`.
- **Rendering**: imperative re-render functions (`renderToday`, `renderTasks`, `renderCalendar`,
  `renderNotes`, `renderTimer`, `renderWeek`), orchestrated by `renderAll()`. Call the relevant
  render fn after any state mutation.
- **Tasks**: `{id, title, done, due (YYYY-MM-DD|null), priority (high|med|low),
  repeat (none|daily|weekly|monthly), focusMinutes}`. Completing a repeating task spawns the
  next occurrence (`nextDue()`), and the completed instance's repeat is set to none.
- **Drag to schedule**: pointer-event based (`makeDraggable`, `dragMove`, `dragEnd`);
  drop targets are elements with `data-date` and class `.day` or `.wk-day`.
- **Timer**: timestamp-anchored (`timer.endAt`) so background-tab throttling can't cause drift.
  Sessions log to `state.sessions` and credit `focusMinutes` on the linked task.
- **Due date pickers**: transparent `<input type="date">` overlaid on buttons
  (`.chip-wrap` + `.overlay-date`). Do NOT use `showPicker()` — it's blocked in sandboxed iframes.
- **Theme**: CSS variables on `:root` / `[data-theme="dark"]`.
- **Test hook**: `window.__tide` exposes state and actions for automated tests.

## Conventions

- Escape all user content with `esc()` before inserting into innerHTML.
- Dates are local-timezone `YYYY-MM-DD` strings via `isoDate()`; weeks start Monday.
- Design tokens: porcelain/teal palette, Hanken Grotesk + Gabarito + JetBrains Mono.
  Minimal aesthetic — avoid adding heavy decoration.
- Never introduce a build step, framework, or external JS dependency without asking.
