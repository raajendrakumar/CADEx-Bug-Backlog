# CADEx Bug Backlog Dashboard

An interactive dashboard for True ValueHub's CADEx bug action log — built from
`Action_Log.xlsx` (the "CadEx Reported Bugs" sheet), covering all 119 reported
bugs.

**Live on GitHub Pages:** https://raajendrakumar.github.io/CADEx-Bug-Backlog/
(enable Pages once — see [Enabling GitHub Pages](#enabling-github-pages)
below — after that this link stays live and updates on every push to `main`)

**Live on claude.ai:** https://claude.ai/code/artifact/5ee408d4-9e9a-4e21-8b33-4d7ec4860cb4
(supports "Save for everyone" — the GitHub Pages copy doesn't, since Pages
serves static files with no server-side storage)

## What's in this folder

- **`index.html`** — identical to `CADEx-Bug-Backlog-Dashboard.html`, present
  so GitHub Pages serves the dashboard at the repo's root URL automatically.
- **`CADEx-Bug-Backlog-Dashboard.html`** — the full, ready-to-use dashboard.
  Double-click to open it in any browser, with the 06 Sep 2026 data snapshot
  baked in.
- **`dashboard-template.html`** — the same dashboard as source code, with a
  `__DATA__` placeholder where the bug records get inserted. Useful if you
  want to edit the design/layout yourself and regenerate the final file.
- **`bugs-snapshot.json`** — the 119 bug records extracted from the
  spreadsheet, as plain JSON. This is what gets substituted into
  `__DATA__` in the template.
- **`.nojekyll`** — tells GitHub Pages to serve the files as-is, skipping
  Jekyll processing (not needed for a plain static site like this one).

## Enabling GitHub Pages

One-time setup, from the GitHub web UI (not something a `git push` can turn
on by itself):

1. Go to **Settings → Pages** in this repo.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Set **Branch** to `main` and the folder to `/ (root)`, then **Save**.
4. GitHub builds the site (usually under a minute) and the live URL above
   starts working. Every future push to `main` redeploys it automatically.

## Features

- KPI tiles (items in scope, pending backlog, average age, pending > 12
  months, critical P0 pending, closed) that recalculate live as you filter.
- Click-to-filter charts: status, priority, category, reporter, and ageing
  profile — click any bar to isolate it, click "clear" to undo.
- A "Top 20 open bugs" watchlist, oldest first, with click-to-expand detail.
- An always-visible "Email summary" — an overall status write-up you can copy
  straight into an email, independent of whatever filters are active.
- An in-page "Upload Excel" button: pick a new `Action_Log.xlsx` (or any
  workbook with a "CadEx Reported Bugs"-style sheet) and it re-parses right in
  the browser, no re-upload to Claude needed.
- "Save for everyone" — writes the uploaded data back so the next person who
  opens the *live* link sees it too.

## Using it standalone (outside claude.ai)

Opening `CADEx-Bug-Backlog-Dashboard.html` directly in a browser works for
everything **except** "Save for everyone": that button writes to storage that
only exists on the published claude.ai artifact, so it's disabled when the
file is opened on its own. Filtering, charts, the watchlist, Excel upload
(for that browser session), and the email summary all work fully offline.

## Regenerating the dashboard with new data

If you'd rather not use the in-page "Upload Excel" button, you can rebuild the
file from scratch:

1. Export your updated action log to JSON in the same shape as
   `bugs-snapshot.json` (fields: `sr`, `bug`, `date`, `subject`, `priority`,
   `status`, `category`, `reporter`, `openDays`, `age`, `bucket`, `comment`,
   `model`).
2. In `dashboard-template.html`, replace the `__DATA__` placeholder
   (search for `const EMBEDDED_DATA = __DATA__;`) with that JSON array.
3. Save the result as your new dashboard HTML file.

## Data source

Extracted from the `CadEx Reported Bugs` sheet in `Action_Log.xlsx`, which
tracks bugs True ValueHub's QA team reported to the CAD Exchanger SDK across
sheet metal, CNC/machining, molding, and file-format import feature
detection.
