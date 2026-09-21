# Macro & Finance Tracker

A single-page personal tracker for daily calories/macros and personal finances
(money lent with reducing-balance interest, plus mutual funds and stocks).

Installable on phones and desktops, works fully offline, and **all data stays on the
device** — there is no server and no account.

## Contents

```
index.html                     the whole app (markup, styles, logic)
manifest.webmanifest           app name, colours, icons
sw.js                          service worker (offline caching)
icons/icon-192.png             home screen / taskbar icon
icons/icon-512.png             high-res icon
icons/icon-maskable-512.png    Android adaptive icon
```

Nothing else belongs in this repo. Your tracked data never lives here.

## Deploy to GitHub Pages

1. Create a new **public** repo under https://github.com/Git-repo999 — for example `tracker`.
   (GitHub Pages needs a public repo on a free plan.)

2. From this folder, push the contents:

   ```bash
   git init
   git add .
   git commit -m "Macro & Finance Tracker PWA"
   git branch -M main
   git remote add origin https://github.com/Git-repo999/tracker.git
   git push -u origin main
   ```

3. In the repo: **Settings → Pages → Source = Deploy from a branch**,
   branch `main`, folder `/ (root)`. Save.

4. Wait about a minute, then open:

   ```
   https://Git-repo999.github.io/tracker/
   ```

All paths in the app are relative, so the repo name can be anything —
no code changes needed if you pick a different name.

## Install as an app

| Platform | How |
| --- | --- |
| Android | Open in Chrome → menu → **Install app** |
| iPhone / iPad | Open in **Safari** → Share → **Add to Home Screen** |
| Windows | Chrome or Edge → install icon in the address bar |
| macOS | Chrome/Edge install icon, or Safari 17+ → File → **Add to Dock** |

After the first load it runs offline.

## Moving your existing data in

Browser storage is tied to the site address, so the hosted app starts empty.

1. Open your old local `calorie_tracker.html`.
2. **Settings → Export / Backup** and save the JSON file.
3. Open the hosted app and **install it first** (see table above).
4. Launch it from the home screen / taskbar, then **Settings → Import / Restore**
   and pick that JSON.

On iOS, install before importing. A home-screen web app may not inherit data entered
in the Safari tab, so importing first can look like the data disappeared.

## Important: data is per device

There is **no sync**. Each device keeps its own independent copy — a payment logged on
your phone will not appear on your laptop. To move data between devices, use
Export on one and Import on the other.

Keep exporting periodically. Clearing browser data wipes the app's data, and iOS can
evict web storage when space is tight. The app's built-in 7-day backup reminder is
there for exactly this reason. Treat the JSON exports as your real backup.

## Shipping an update

Edit `index.html`, then bump the cache version in `sw.js`:

```js
const CACHE_NAME = 'tracker-v2';   // was tracker-v1
```

Commit and push. Installed copies pick up the new version next time they open online.
Without the version bump, devices may keep serving the old cached page.
