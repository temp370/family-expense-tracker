# Family Expense Tracker

A private, local-first personal expense tracker for a family budget. It stores data in the browser and can optionally use Supabase for user accounts, Google OAuth, and cloud sync.

## Project structure

- `index.html` – main app
- `manifest.webmanifest` – PWA manifest
- `sw.js` – service worker for offline caching
- `icon.svg` – app icon (SVG for reliable browser support)
- `README-SETUP.md` – GitHub Pages setup
- `SUPABASE-SETUP.md` – Supabase + Google OAuth setup
- `.gitignore` – hides local secrets and backup files

## Important privacy rule

Do not store secrets in the GitHub repository.

Never commit:

- `.env`
- `.json` backups with private data
- `.csv` exports with real records
- Excel/spreadsheet files
- API keys or OAuth secrets

This app supports two modes:

1. Guest/local mode
   - data stays in the browser localStorage
   - good for personal, offline use
2. Cloud-authenticated mode
   - uses Supabase Auth + Google OAuth
   - data is stored in Supabase database and protected by user-specific RLS policies

## Deploy to GitHub Pages

1. Push this repo to GitHub
2. Open `Settings -> Pages`
3. Choose `Deploy from a branch`
4. Branch: `main`, folder: `/root`
5. Save

## Supabase setup

See `SUPABASE-SETUP.md` for the exact steps to enable:

- Google login
- user signup/login
- cloud expense sync
- secure per-user access control

## Local use

Open `index.html` directly in a browser, or deploy via GitHub Pages.
