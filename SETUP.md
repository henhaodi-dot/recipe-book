# Setup — recipe book with screenshot capture

There are two parts. Do them in this order.

```
(this folder)
├── index.html, manifest.webmanifest, service-worker.js, icon-*.png   ← the app
└── recipe-capture-worker/                                            ← the capture service
```

## 1 · Put the app online (GitHub Pages)

This is the updated app — it replaces the earlier version, so if you already have a
`recipe-book` repo, just drop these files in over the old ones.

- Upload everything in this folder **except** the `recipe-capture-worker` folder to
  the root of your `recipe-book` repo, and enable Pages (Settings → Pages → Deploy
  from a branch → `main` / root).
- Or, in Claude Code from this folder:

  > "Commit the updated files in this folder (ignore the recipe-capture-worker
  > folder) to my recipe-book repo and push. If the repo doesn't exist yet, create a
  > public repo called recipe-book, push, and enable GitHub Pages on main/root. Then
  > give me the live URL."

Open the URL on your phone and install it (Share → Add to Home Screen on iPhone,
or ⋮ → Install app on Android).

## 2 · Deploy the capture service (Cloudflare Worker)

Full steps are in `recipe-capture-worker/DEPLOY.md`. Short version:

```bash
cd recipe-capture-worker
npm install -g wrangler
wrangler login
wrangler secret put ANTHROPIC_API_KEY      # your key from console.anthropic.com
wrangler secret put APP_TOKEN              # optional password you make up
wrangler deploy                            # prints your Worker URL
```

You'll need an Anthropic **API** key (Console, pay‑as‑you‑go — separate from your
Claude.ai plan). The key is typed into wrangler's prompt only; it never touches the
app or the repo.

## 3 · Connect the app to the service

In the app, tap the ⚙ gear (top of the screen):

- Paste your **Worker URL** (from step 2).
- If you set an `APP_TOKEN`, paste the same value into **App token**.
- Tap **Test connection** — you want "Connected ✓".
- Save.

These live only on the device you enter them on, so do this on each device you want
to import from.

## 4 · Use it

Tap **截图导入 Import**, pick a screenshot from your photos (小红书, Facebook, a blog,
a photo of a cookbook — anything), and it reads the recipe, translates it so you have
both Chinese and English, and opens it in the form. Check it over, pick who likes it,
and save.

Screenshots are the reliable path — importing straight from a link isn't included,
because Facebook and 小红书 block that and often keep the recipe inside the images
anyway. Screenshotting sidesteps all of it.

## Costs, at a glance

- GitHub Pages and Cloudflare Workers: free at this scale.
- Anthropic API: a few cents (or less) per screenshot. Switch `MODEL` in
  `recipe-capture-worker/worker.js` to `claude-haiku-4-5-20251001` to cut it further.
