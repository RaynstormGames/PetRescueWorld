# PetRescueWorld — GitHub Pages pack (v13, Nov 21, 2026)

Ready to push. This folder holds the current web-edition build so the
game can be served over HTTPS — the step that unblocks the GPS field test.

## Why this matters now

Ryan's Nov 21 playtest proved the downloaded file can never pass the GPS
test: opened from storage, Chrome shows a `content://` address and denies
location instantly without ever asking for permission. Browsers only offer
location on secure HTTPS pages. The same file served from GitHub Pages
gets a real prompt. No code change can fix this from inside the file.

## What's in here

- `index.html` — the v13 build ("Yard fixes · Nov 21, 2026 · v13",
  md5 `16bdb7c0a3dcc513985b0ee7da35dcdb`), copied from the live web app.
  Single file; its only outside dependencies are the Leaflet CDN and
  Google Fonts, both fine over HTTPS.
- Safety check done Nov 21: `DB_MANAGER_URL` in this file is an empty
  placeholder — no Tailscale hostname or private address is embedded, so
  publishing the repo publicly exposes nothing private. (The DB manager
  URL goes in the game's secrets block only when Ryan wires sync up.)

## Push steps (laptop, ~10 minutes)

1. On GitHub, create a **public** repo (Pages is free; public required on
   the free tier). Name it anything, e.g. `petrescueworld`.
2. Upload this folder's `index.html` to the repo's main branch
   (web upload works — no git needed for this step).
3. Repo Settings → Pages → Source: Deploy from a branch → main, /(root)
   → Save. Wait ~1 minute for the green check.
4. Open the Pages URL on the phone in **Chrome** (not in-app) →
   Add to Home Screen.
5. Re-run the GPS test from the laptop checklist
   (`../laptop-setup-checklist.md`, "First live test"):
   Map tab → Enable Location → Allow; debug line should show granted +
   accuracy in metres; map zooms to street level; real businesses appear
   as "?" nodes; walk to one and trivia fires (40 m, or 75 m if coarse).

## After a new build lands

Replace `index.html` in the repo with the new build's file and the Pages
URL serves the new version (hard-refresh on the phone if it shows the
old one — same cache quirk as the in-app viewer).

## Not in scope here

- The Raynstorm Consulting website draft is separate (its own GitHub
  Pages plan, awaiting Ryan's repo setup and approval).
- DB sync still needs the laptop DB manager + Tailscale serve step from
  the laptop checklist; Pages alone only fixes GPS/hosting.
- PetRescueWorld.fun domain purchase is separate and still Ryan's call
  for end of November.
