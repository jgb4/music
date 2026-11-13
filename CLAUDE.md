# music

Small music web tools, published with GitHub Pages at https://jgb4.github.io/music/
(repo: github.com/jgb4/music, branch `main`, served from the repo root).
A sibling of the `tools` repo (jgb4.github.io/tools/): each GitHub repo is its own top-level path,
so anything that should live under `/music/` belongs in this repo, not in `tools`.

## Layout

```
index.html              ← landing page: one card per tool
<tool-name>/index.html  ← each tool in its own folder → jgb4.github.io/music/<tool-name>/
```

Current tools: `spotify-stats/`.

## Adding a tool

1. Create `<tool-name>/index.html` (lowercase, hyphenated; it becomes the URL, so don't rename it later).
2. Add a card for it to the root `index.html`, copying the existing `<a class="tool">` card.
3. Update the "Current tools" list above.

## Rules

- **Static only.** Everything runs in the browser; libraries come from a CDN with exact pinned versions.
- **Relative paths only** (`../`), never `/…`: the site lives under `/music/`.
- **No username in the code.** Relative paths and `location` keep everything working if the account is renamed.
- Same look as the `tools` site: same CSS color tokens, light and dark mode, works at phone width.

## Deploying

Commit and push to `main`; the site updates in about 30 seconds. Verify the live URL afterwards.
Commit as `jgb4` with the GitHub noreply email (set in the repo's git config); never use a personal email.

## Spotify Stats (spotify-stats/)

Spotify's Authorization Code + PKCE flow, entirely in the browser (no secret, no server).
`DEFAULT_CLIENT_ID` near the top of the script is the public Client ID of the owner's Spotify app.
Its Redirect URIs must match exactly: `https://<pages-host>/music/spotify-stats/` and, for local testing,
`http://127.0.0.1:8765/spotify-stats/` (Spotify rejects `localhost`; `.claude/launch.json` serves on 127.0.0.1:8765).
Development Mode (2026 rules): the app owner needs Premium, at most 5 allowlisted users,
no batch `GET /artists`, and artist genres/popularity may be missing; the page degrades gracefully.
