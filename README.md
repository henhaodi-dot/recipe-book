# 我的菜谱 · My Recipe Book

A bilingual recipe book you can install on your phone. Add recipes, filter by
meal type and by who likes what, flag the low‑FODMAP ones, and read each recipe
in Chinese, English, or both. Everything is saved on the device — no account,
no server.

## Files

- `index.html` — the whole app (self‑contained)
- `manifest.webmanifest` — makes it installable
- `service-worker.js` — lets it open and run offline
- `icon-192.png`, `icon-512.png`, `icon-180.png`, `icon-maskable-512.png` — app icons

Keep all files together in one folder.

## Put it online (GitHub Pages)

Same setup you used for Hanzi Garden.

1. Make a new repo (e.g. `recipe-book`) and upload all the files in this folder
   to the root of it.
2. In the repo: **Settings → Pages → Build and deployment → Source: Deploy from
   a branch**, branch `main`, folder `/ (root)`, then **Save**.
3. Wait a minute, then open the URL it gives you
   (`https://<your-username>.github.io/recipe-book/`).

The paths are all relative, so it works whether it sits at the repo root or in a
subfolder.

## Install on your phone

Open that URL in your phone's browser first, then:

**iPhone / iPad (Safari)** — tap the **Share** button → **Add to Home Screen** →
**Add**. It opens full‑screen like a normal app.

**Android (Chrome)** — tap the **⋮** menu → **Install app** (or **Add to Home
screen**) → **Install**.

## Importing recipes from screenshots

Tap **截图导入 Import** and pick a screenshot — it reads the recipe with Claude,
fills in both Chinese and English, and opens it in the form for you to check. This
needs the small Cloudflare Worker in `recipe-capture-worker/` deployed once, and its
URL entered in the app's ⚙ settings. Full walkthrough is in `SETUP.md`.

## Good to know

- Recipes are stored **on each device**. What you add on your phone stays on your
  phone; the laptop keeps its own copy. If you want them to sync across devices
  later (like Hanzi Garden's setup), that can be added.
- To update the app after editing `index.html`, change the version line near the
  top of `service-worker.js` (`recipe-book-v1` → `recipe-book-v2`) so phones pick
  up the new version.
- The three recipes it ships with are just examples — edit or delete them.
