# Kids Arcade

Public site of kid-friendly browser games for Gabe's kids (around 5–6 years old).
Live at https://gabeenso.github.io/kids-arcade/ via GitHub Pages (deploys from `main`, root folder, about 1 minute after a push).

**This repo is public.** No real names, photos, school, location or anything personal about the kids. Games must be gentle and silly: no gore, no scary content, no ads, no links out, no data collection.

## How the arcade works
- `index.html` is the game picker. It reads `games.json` and shows a big card per game. Don't hard-code games into it.
- `manifest.webmanifest` + `icons/` make the site installable (Share → Add to Home Screen) so it opens full screen on the iPad.
- Each game lives in its own folder: `games/<game-id>/`.

## Adding a new game (checklist)
1. Create `games/<game-id>/index.html` as a complete, self-contained HTML document (`<!doctype html>`, head, body). Inline CSS/JS. External scripts only from cdnjs.cloudflare.com with a pinned version.
2. In its `<head>` include:
   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no, viewport-fit=cover">
   <link rel="manifest" href="../../manifest.webmanifest">
   <meta name="theme-color" content="#4fc3ff">
   <meta name="mobile-web-app-capable" content="yes">
   <meta name="apple-mobile-web-app-capable" content="yes">
   <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
   <link rel="apple-touch-icon" href="../../icons/apple-touch-icon.png">
   ```
3. Give the game's start screen a big Home button linking to `../../` (see the round yellow house button in `games/zombie-pop-truck/`).
4. Add a 4:3 cover image at `games/<game-id>/cover.svg` (bright, readable at small size, no text a 5-year-old needs to read).
5. Add an entry to `games.json`:
   ```json
   { "id": "<game-id>", "title": "…", "tagline": "…", "path": "games/<game-id>/", "cover": "games/<game-id>/cover.svg", "color": "#hex" }
   ```
   If the game replaces a `"comingSoon": true` placeholder, replace that entry.
6. Design for iPad touch first: big targets (60px+), no hover-only controls, no pinch/scroll gestures, works in landscape and portrait, sound starts only after the first tap.
7. Save progress with `localStorage` under a key unique to the game (e.g. `unicorn.v1`), wrapped in try/catch.
8. Commit to `main` and push. Check the live URL after about a minute.

## Games
- `zombie-pop-truck` — 3D (three.js r128) truck rail shooter, 20 levels in two worlds, cartoon zombies that pop into confetti, Star Squad friends who join the truck and shoot alongside you, plus timed power-ups. Bosses have styles: stomp, sway, hop, fly, grow.
- `unicorn-sparkle-pop` — gentler fork of the same engine for a 4-year-old: unicorn on a rainbow road, pastel sleepy zombies that pop into rainbow confetti, 10 levels, three original pop-star friends (Nova, Bella, Jojo) who fly alongside and shoot. The friends are original characters; never make them look like characters from films or TV.
- `reptile-rangers` — 2D canvas shooter for a 6-year-old: a ranger in a jeep, boat or submarine splashes goo monsters across 5 worlds (Outback, Jungle, River, Ocean, Dragon Island), 15 levels, pops bubbles to rescue 15 real reptiles. Each reptile has 3 spoken facts, a picture quiz after each level and a Reptile Book. Bosses on every third level. Facts must stay accurate; check any new one before adding it.
- `pool-pals` — tap-only pool-safety adventure for a 4-year-old with original brick-built characters (Pip the pup, Ollie the otter lifeguard, Bo the bunny). Nine map stops: grown-up watching, gate shut, sun smart, walk don't run, feet first, starfish float, ask a grown-up for toys, shout for help, pool party recap. Everything is spoken aloud (Web Speech). Never make the characters look like Bluey or use LEGO branding.

Each game exposes `window.__zpt` debug hooks used by headless tests; leave them in.
