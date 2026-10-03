# Velora — Base44 Dev Environment

## What this is
A single static HTML file (`velora-2.html`) — a dark luxury fashion brand landing page using Three.js (CDN) and Google Fonts. No build step, no backend, no database.

## Running
```bash
docker compose -f docker-compose.base44.yml up -d
```
Serves on host port 3000 via nginx. The repo is bind-mounted read-only; edits to `velora-2.html` appear on browser refresh (no live reload).

## Key details
- `velora-2.html` is served as the index page (configured in `nginx.conf`).
- A custom `nginx.conf` is required because the repo directory has restrictive permissions (0700); nginx workers must run as `root` to read the bind-mounted files.
- Healthcheck uses `127.0.0.1` (not `localhost`) because the Alpine image resolves localhost to IPv6 first, causing a false-negative.
- No secrets or external credentials needed — all assets are loaded from public CDNs in the browser.
