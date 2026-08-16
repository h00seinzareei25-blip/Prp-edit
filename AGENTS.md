# AGENTS.md

## Cursor Cloud specific instructions

### What this repo is
- A single, self-contained offline web app: `Prp100 .html` (note the space in the filename). It is a Persian/Farsi (RTL) PRP clinic management dashboard (patients, appointments, treatment stages, SMS reminders).
- Everything (HTML + CSS + vanilla JS) is embedded in that one file. There is **no build system, no package manager, no backend, and no database**. Persistence is browser-local (IndexedDB + localStorage); backups are JSON export/import.

### How to run it
- Serve the folder with any static server and open the file, e.g. from `/workspace`:
  - `python3 -m http.server 8000` then open `http://localhost:8000/Prp100%20.html` (the space must be URL-encoded as `%20`).
- Serving over HTTP (rather than `file://`) is preferred so IndexedDB and fetch behave consistently. The app is otherwise fully offline.

### Lint / test / build
- None exist. There are no linters, no automated tests, and no build step. "Testing" means opening the app in a browser and exercising a flow (e.g. registering a patient via the blue `ثبت بیمار` button).

### Non-obvious gotchas
- The mobile-number input renders Persian numerals and can appear to truncate while typing; the saved value is still correct. If automating input, setting the field value directly (e.g. `document.getElementById('addPhone').value = '09123456789'`) is a reliable workaround.
- SMS gateway integrations (Kavenegar, SMS.ir, IPPanel, IranPayamak, Ghasedak) are optional, require user-supplied API keys entered in the app settings, and send real messages — not needed for functional testing.
