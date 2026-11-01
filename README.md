# My Exercise Plan (PWA)

A static progressive web app: no build step, no server code, no external requests.

```
index.html             the app (everything inline)
manifest.webmanifest   name, icons, colours, standalone display
sw.js                  service worker: offline + automatic updates
icons/                 192, 512, maskable 512, apple-touch 180
.nojekyll              stops GitHub Pages processing the files
```

## Deploy (any static HTTPS host)

Service workers need HTTPS, so any static host works. Upload the folder contents to the site root or a subfolder (all paths are relative).

**GitHub Pages**
1. Create a new repository, e.g. `exercise-plan`.
2. Upload every file in this folder, including `icons/` and `.nojekyll`, to the `main` branch.
3. Go to Settings → Pages → Build and deployment → Source: *Deploy from a branch* → `main` / `(root)` → Save.
4. After a minute it's live at `https://<username>.github.io/exercise-plan/`.

Note: Pages on a free account needs a **public** repo. The page has `noindex` set and contains no names, but anyone with the URL can see the plan text. Dad's ticks, weights and notes never leave his phone.

**Netlify Drop / Cloudflare Pages**: drag this folder onto the upload page.

## Getting it onto Dad's phone

1. Open the link in Chrome on his phone.
2. Tap **Add to my home screen** on the Today page (or ⋮ → *Add to Home screen* → *Install*).
3. Open it once from the home screen while online. After that it works offline.

## Updating

- Edit `index.html` and redeploy. The phone picks up the new version the next time the app opens online (the service worker fetches pages network-first, with a 4-second fallback to the saved copy).
- If you change `sw.js` or the icons, bump `VERSION` in `sw.js`.
- Data lives in `localStorage` under `exercisePlan.v1` on the phone. Redeploying never touches it. Settings → Backup gives a code to move data between devices or browsers.
