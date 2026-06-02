# Deal Analyzer — installable iPad app

This is the full installable (offline-capable) version of the dashboard. It’s a small
bundle of files that must all live **together in the same folder** when hosted.

## Files (keep them in one folder)

- `index.html` — the dashboard
- `sw.js` — service worker (handles offline caching)
- `manifest.webmanifest` — app name, icon, and “standalone” launch settings
- `icon-180.png`, `icon-192.png`, `icon-512.png`, `icon-512-maskable.png` — app icons

## Why it has to be hosted

iPad can only turn a **web link** into a home-screen app, and offline caching only
works over **HTTPS**. A loose file in the Files app can’t do either. GitHub Pages is
free and serves over HTTPS, so it’s a perfect home for this.

## Step 1 — Put it on GitHub Pages

1. Create a new repository (e.g. `deal-analyzer`).
1. Upload all the files above into the **root** of the repo (not inside a subfolder).
1. Go to **Settings → Pages**.
1. Under “Build and deployment,” set **Source: Deploy from a branch**, branch **main**,
   folder **/ (root)**, then **Save**.
1. Wait ~1 minute. Pages will show your URL, e.g.
   `https://YOURNAME.github.io/deal-analyzer/`

(Prefer no setup? Drag the whole folder onto <https://app.netlify.com/drop> for an instant
HTTPS link instead.)

## Step 2 — Install it on the iPad

1. Open that HTTPS URL in **Safari** (not Chrome) — **while you have a connection**, so
   it can cache itself.
1. Let the page fully load. Then tap the **Pipeline** tab once so the U.S. map data
   gets cached too.
1. Tap the **Share** button → **Add to Home Screen** → name it → **Add**.
1. Tap the new icon. It launches fullscreen, no browser bar, and appears in the app
   switcher like a native app.

## After that

- It opens **with no internet** — the whole dashboard, including the map (as long as you
  loaded the Pipeline tab once while online in step 2).
- Home-screen web apps aren’t wiped by Safari’s normal storage cleanup, so it stays put.

## Updating it later

When you change any file, open `sw.js` and bump the version on the first line —
`const CACHE = 'deal-analyzer-v1';` → `'deal-analyzer-v2'` — and re-upload. Next time the
iPad opens with a connection, it pulls the new version automatically.
