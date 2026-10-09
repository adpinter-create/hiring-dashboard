# Hiring command center

Live job-market dashboard for andreipinter.com, published to GitHub Pages and refreshed by a scheduled GitHub Action (same setup as PulseNews).

- **Daily:** live postings for the tracked roles from the Adzuna jobs API (`scripts/refresh_hiring.py live`).
- **Mondays and manual runs:** unemployment, job openings, hires rate and openings per unemployed worker from BLS, plus a "What changed" entry when BLS publishes (`scripts/refresh_hiring.py weekly`).

The page reads `data.json` on load and falls back to its built-in snapshot if that's missing. If a source is down, the last good numbers stay up.

## Setup

1. Settings → Pages → Source: **GitHub Actions**.
2. Settings → Secrets and variables → Actions:
   - `ADZUNA_APP_ID`, `ADZUNA_APP_KEY` (free at https://developer.adzuna.com), required for live postings
   - `BLS_API_KEY` (optional)
3. Settings → Pages → Custom domain: `hiring.andreipinter.com`. DNS (Squarespace): CNAME, host `hiring`, data `adpinter-create.github.io`.
4. Actions → Refresh hiring dashboard → Run workflow.
5. When the domain verifies, tick **Enforce HTTPS**.

## Changing the tracked roles

Edit `roles.json` (title, search terms, location). Keep titles matching `LIVE_ROLES` in `index.html`, which holds each card's tag and fallback numbers.
