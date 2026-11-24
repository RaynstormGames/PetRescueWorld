# PetRescueWorld (web game, GitHub Pages) — Changelog

Backfilled 2026-11-24 from project memory, the first-tester briefs, and the push sync record. Newest first. Dates are the Pages push date where a push is recorded; the Settings build stamp is quoted in each entry so a phone can be checked against it. Versions v12, v16, and v17 do not appear in any record on disk and are not documented here.

## v27 — 2026-11-24 · `9223ac9`
- Credits finalized: "Created by Rayn Storm & Mallow Lotyl", "Lead — Rayn Storm" (Guide tab credits card). Stamp: "Credits stage names · Nov 23, 2026 · v27".
- This push carried v25–v27 to Pages in one step. In the shipped configuration (server endpoint unset) the only player-visible change from v24 is the credits; the v25 login gate stays dormant.

## v26 — 2026-11-23 (from build notes)
- Credits name update: the assistant's credit became "Mallow Lotyl" throughout the credits card. Stamp: "Credits name · Nov 23, 2026 · v26".
- Dev build only at the time; reached Pages as part of the v27 push. Its interim credits wording was superseded by v27.

## v25 — 2026-11-23 (from build notes)
- Account login gate: sanctuary-art sign-in screen (dawn art by day, dusk in the evening) with Email | Phone | Twitch tabs, sign-in and create-account modes, a TOTP code step when the server asks for one, and a one-time recovery-code save card after registration (framed as a backup way back in, not a wallet phrase).
- "Forgot your sign-in?" recovery flow included (generic "if that matches an account, a code is on its way" copy; verified 11/11 against a stub of the server v0.4.0 contract — the live-server pass was still owed at build time).
- The gate appears only when a server endpoint is configured; with the endpoint empty the game boots exactly as v24. "Continue on this device only" is always visible, and Settings gains an account card only when an endpoint exists. Stamp: "Accounts login · Nov 23, 2026 · v25".
- Dev build only at the time; reached Pages as part of the v27 push.

## v24 — 2026-11-22 · `74f6646`
- Node reach set to 25 m, widening only to the GPS fix's own accuracy when the fix is rougher than 25 m (replaces 40/75 m).
- Zoom-lock fix: the v22 lock failed on a real phone because the OpenFreeMap GL layer runs one zoom level below Leaflet; the floor is now set on the GL scale (Leaflet − 1) with a Leaflet zoomend snap-back guard. Tap gate exercised with real marker clicks (20 m opens, 30 m refuses at a good fix).
- Guide credits tagline replaced with the mission line: "This game is built for the protection of all the animals of the world through the choices of its players."
- Stamp: "25 m reach + zoom lock fix · Nov 22, 2026 · v24".

## v23 — 2026-11-22 · `f926af4`
- Walking Quests: each whole mile walked heals the active pet set by 10% of max HP (never revives a TKO pet) and pays a flat 10 Coins; progress persists across walks and resets at 00:00 UTC.
- 10 miles in a day drops one random asset of Rare or lower (rarity derived from price bands), once per day.
- Map tab gains a Walking Quest card (today's miles, progress to next mile, quest Coins earned). Practice Map excluded. Harness 27/27.
- Stamp: "Walking quests · Nov 22, 2026 · v23".

## v22 — 2026-11-22 · `a705856`
- GPS zoom lock: Leaflet minimum zoom 16 (street-level play view) on the map, the raster fallback, and the GL layer; zooming in still allowed.
- Node tap gate: taps check distance against the play radius (40 m, or 75 m when GPS accuracy is worse than 40 m) before any trivia/claim code runs. GPS accuracy is now actually captured (it previously was not, so the relaxed radius had nothing to read).
- Note: the zoom lock did not hold on Ryan's phone — root-caused and fixed in v24.
- Stamp: "GPS zoom lock · Nov 22, 2026 · v22".

## v21 — 2026-11-22 · `c70651e`
- Yard gains the pet carousel: swap between active slot pets in the Yard with the same arrows/swipe as Main; the shared current-pet selection drives Main, the Yard header, the map marker, and care/games. Switching is blocked mid-animation.
- PFP fit: the layered pet portrait now scales so pet, hat, and all life stages fit inside the frame box (verified across 49 species × 3 stages × 4 hat states × 2 sizes = 1,176 combinations; the old code overflowed the top by 39 px for an adult at the large size).
- Stamp: "Yard swap + PFP fit · Nov 22, 2026 · v21".

## v20 — 2026-11-22 · `4e431c4`
- Places chain fix: Overpass rotation switched from POST to GET; an HTTP 200 with zero usable places now counts as "no result" and falls through to the next layer; empty cached place sets are never served.
- Map status line names its data source ("Places: live map data" / "Geoapify" / "saved area" / "trail nodes (places service unreachable)").
- Stamp: "Places GET fix · Nov 22, 2026 · v20".

## v19 — 2026-11-22 · `ca08d88`
- Geoapify places fallback goes live (key domain-locked to the Pages site, stored only in the game's secrets block). Fallback chain order: fresh cache → Overpass rotation → Geoapify → scatter.
- Carried all v18 fixes to Pages (v18 was never pushed on its own). Live on Ryan's phone, this build confirmed the walk black-screen fix and the scatter fallback.
- Stamp: "Geoapify live · Nov 22, 2026 · v19".

## v18 — 2026-11-22 (from build notes; shipped inside v19)
- Slot-1 desync fixed: changing Slot 1 in the Kennel now re-derives Main's current pet (and the Yard follows).
- Deterministic scatter fallback ("trail nodes"): when every places service fails, ~14–20 generic trail-style trivia nodes are generated per area (≥40 m apart, no fake business names, no scattered trees/vets), so the map is never empty; real POIs take back over when services recover.
- Main-tab pet swipe rebuilt on Pointer Events, firing mid-gesture into the same code path as the arrows.
- Walk black-screen fix: the GPS map rebuilds when its container has been replaced by a re-render. Places timeouts shortened so failures fall through to scatter faster.

## v15 — 2026-11-22 · `d835d02`
- Maps update: real GPS map uses OpenFreeMap Liberty vector tiles via MapLibre GL, with automatic fallback to the previous OSM raster tiles.
- Places loading rotates three Overpass endpoints (one attempt each, next only on failure), fetches only after moving >350 m or on "Find me", one request in flight, and caches per ~500 m grid cell for 24 h. The failure message shows only after all endpoints fail with no usable cache.
- Geoapify fallback wired but dormant (empty key slot). Practice Map, pet marker, walk tracking, and save shape untouched.
- Stamp: "Maps update · Nov 22, 2026 · v15".

## v14 — 2026-11-22 · `e9d2b32`
- The GPS map's player marker is now the current pet's sprite, swapping when the current pet changes.
- Stamp: "Pet marker · Nov 22, 2026 · v14".

## v13 — 2026-11-22 · `ea7476c`
- First GitHub Pages release (this push also added the repo README). The game went live at raynstormgames.github.io/PetRescueWorld, which fixed the GPS blocker (geolocation requires an HTTPS origin) — field test the same day confirmed location, tiles, and walk tracking on a real street.
- Sprite knockout re-derived conservatively for all 49 pet + 5 poacher sprites: only border-connected background is removed, restoring pet outline lines the earlier knockout had eaten.
- Yard props (bowls, toy, rest spot, dig hole) layer in front of the pet; the dig hole persists 10 seconds before fading.
- The guided care-routine list was removed from the Yard — care order is discovered by doing and tracked on Main; the Yard keeps the button grid, Care % readout, and chain-state badge.
- Stamp: "Yard fixes · Nov 21, 2026 · v13".

## v11 — 2026-11-21 (from build notes; dev artifact only, never on Pages)
- From-scratch rebuild: final tab structure (Main, Kennel, Yard, Map, Rescue, Pass, Field Dex, Adopt, Guide, Settings), Guide tab with credits, "Field Guide" renamed to Field Dex, transparent sprites.
- Care-order chain, Kennel Morale payout, rename cost with Bond reset, growth overlays at Lv 11 and Lv 20, Adoption House, Battle Pass.
- Settings build stamp introduced (the freshness check used by every later build).
