# Simple Notes App (Astro Frontend)

A minimal, modern notes UI built with Astro following the **Ocean Professional** theme:
- Primary: `#2563EB` (blue)
- Secondary: `#F59E0B` (amber)
- Background: `#f9fafb`
- Surface: `#ffffff`
- Text: `#111827`

## Features

- Left sidebar navigation + sticky top toolbar
- Responsive grid of note cards
- Create / edit / delete notes (frontend-only)
- Notes persist in `localStorage` (no backend required)
- Accessible modal dialog:
  - Escape to close
  - Focus is trapped within the dialog
  - Clicking outside closes the dialog
- Empty states and search filtering

## Run locally (port 3000)

From `notes_frontend/`:

```sh
npm install
npm run dev -- --port 3000 --host 0.0.0.0
```

Then open:

- http://localhost:3000

> This project’s `astro.config.mjs` is already configured to use port `3000`.

## Storage

Notes are stored in your browser under a versioned key:

- `notes_app.notes.v1`

Clearing site data or localStorage will remove notes.

## Switching to a backend later (using PUBLIC_API_BASE)

This UI is intentionally **local-first** and does **not** call any backend yet.

When you add an API later:
1. Set `PUBLIC_API_BASE` in your environment (must be `PUBLIC_*` so it can be read in the browser).
2. Replace the localStorage calls in:
   - `src/lib/notesStore.ts`
   - `src/components/NotesApp.astro` (script section)

Suggested future approach:
- `GET /notes` to load
- `POST /notes` to create
- `PUT /notes/:id` to update
- `DELETE /notes/:id` to delete

Keep the same UI and swap the persistence layer behind the scenes.

## Environment variables

This frontend reads only the following (safe) public variables if present:
- `PUBLIC_API_BASE`
- `PUBLIC_BACKEND_URL`
- `PUBLIC_FRONTEND_URL`
- `PUBLIC_WS_URL`
- `PUBLIC_NODE_ENV`
- `PUBLIC_PORT`

No backend is required to run the app.
