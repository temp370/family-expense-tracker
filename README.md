# Family Expense Tracker

A private, local-first personal expense tracker for a family budget. It stores data in the browser (localStorage) and can optionally sync with Google Drive using a Google OAuth Client ID.

## Project structure

- `index.html` – main app
- `manifest.webmanifest` – PWA manifest
- `sw.js` – service worker for offline caching
- `icon.svg` – app icon (SVG for reliable browser support)
- `README-SETUP.md` – setup guide for Google Drive sync and GitHub Pages
- `.gitignore` – hides local secrets and backup files

## Security note

This app is intentionally designed to keep sensitive data local to the browser. Do not place real credentials, secret spreadsheet files, or private Excel exports inside the GitHub repository.

For production/private use:

- keep the GitHub repo private
- store sensitive data only in a backend or private environment
- use environment variables or secret stores for any API keys
- never commit `.env`, `.csv`, `.json` backups, or Excel files

## Local use

Open `index.html` directly in the browser or deploy via GitHub Pages.

## Deploy to GitHub Pages

1. Push this repo to GitHub
2. Go to `Settings -> Pages`
3. Choose source: `Deploy from a branch`
4. Branch: `main` and folder: `/root`
5. Save and wait for deployment

## Optional Google Drive sync

See `README-SETUP.md` for setup steps.
