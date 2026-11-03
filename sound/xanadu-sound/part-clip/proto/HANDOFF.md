# HANDOFF — Xanadu Sound / Pärt clip prototype

For the next chat. Written 1 Nov 2026 by the advisor at the end of a two-day session (31 Oct–1 Nov). Read this first; then PLAN-v2.md, IMPACTS.md, and `docs/XANADU-SOUND-project.md` §10–11. Project-level handover (done / to do, one screen each): `../HANDOVER-2026-11-03.md`.

## How to start the next chat

1. Attach the repo `bektaron/MJDL` (push access). Everything lives under `sound/xanadu-sound/`.
2. Say: "Read sound/xanadu-sound/part-clip/proto/HANDOFF.md and continue."
3. Working language Turkish; system files English. Address: Üstadım.

## What exists (all pushed to `main`; pass 3b-i pushed 3 Nov 2026, early — see the pass log)

| Path | What | State |
|---|---|---|
| `docs/XANADU-SOUND-project.md` v0.2 | project brief; §10 Pärt clip (design, rulings, realisation notes); §11 research integration; Appendix A = research report | authoritative |
| `docs/XANADU-SOUND-research.md` v0.1 | five-agent research (sonification, rule systems, toolchain, rights, exhibition) | reference |
| `fr-001-tintinnabuli/index.html` | ear test for the sound work: tintinnabuli rule, old/new `|` and ambiguity toggles, three densities | **not yet listened to by Bekir** |
| `part-clip/proto/index.html` | the WebGL2 prototype (one file, no libraries) | live at `bektaron.github.io/MJDL/sound/xanadu-sound/part-clip/proto/` |
| `part-clip/proto/PLAN-v2.md` v2.1 | refinement plan: three axes, passes, "Done" log | authoritative |
| `part-clip/proto/IMPACTS.md` v1 | impact model: drop / strike / sweep / blow / flow × liquid / solid / granular | authoritative |

## Rulings by Bekir (do not reopen without him)

- First clip: **Für Alina, piano only** — Alexander Malter, ECM *Alina* (1999), track 2, 10:47. **Medium: liquid** (ruling 1 Nov, afternoon).
- Second: *Spiegel im Spiegel* (open; violin = blow/flow idea on file). Third: **Cantus in memoriam Benjamin Britten** for the **sweep** impact.
- Three axes, **never mixed in one piece**: medium (liquid / solid / granular) · layer (image + its own height map, up to 4, then white) · impact (five types, four numbers: energy, area, duration, direction).
- Sweep **absorbs** and **piles at its edge**; blow **pushes solids** (piece size = medium, scaled by energy — advisor's proposal, accepted "don't know"); flow flows.
- Drops do not start by themselves; he taps. Random 45 s mode exists for sequences.
- Erosion bottoms out at **white**; no wrap.
- Stay in WebGL; Blender only if the 1080p test render fails the eye.
- Nothing public until Universal Edition answers (§11.6 brief not yet sent). ECM master licence or a new recording also needed.

## Working method (he asked for this explicitly: "no haste, nothing sloppy")

- Each pass: **Sonnet writes** (small, scoped brief; pixel-identical at defaults; node --check; headless Chrome at 390×844 and 1024×768 with `#surface=…&auto=1&seek=7`; screenshots) → **Opus reviews independently** (diff vs commit, measured regressions, determinism, iOS risks, wiring of every slider; fixes clear bugs, flags the rest) → advisor looks at screenshots → **push**. Commits as Bekir with the Claude co-author trailer.
- Never commit a file an agent is still editing. Never send a message to a running agent (two were lost that way — the harness reported "stopped by the user"; cause unclear, probably an interrupted tool call). If an agent dies mid-edit: back up the half state to the scratchpad, `git checkout --` the file, re-run in smaller slices. (3b-i) Two more ways an agent stops: a long foreground wait loop (`until … sleep`) raises a permission prompt on Bekir's phone and a tap kills the agent for good — tell writers to use short polls or background runs; and the container can restart mid-review (1 Nov–3 Nov: once) — scratch dirs and the working copy survive, background processes do not; a finished-or-stopped agent can be resumed with SendMessage and keeps its context.
- He is often on the phone: send 1–4 rendered frames (headless Chromium, software GL is slow: 5 frames ≈ 10 min) rather than asking him to open the page. `#seek=N` fast-forwards the sim; `#auto=1` turns on synthetic events; `#surface=`, `#aspect=`, `#impact=`, `#drop=`, `#random=1&seed=N` exist.
- Useful hooks on `window.XANADU`: `fieldRes`, `light`, `readMask()`, `readWave()`, `step`, `fire`, `loadLayerHeight`, `clearLayerHeight`, `layerHeights`, `cracks`.

## Pass log

- Pass 1a (done, reviewed): light panel (azimuth/elevation/intensity/Kelvin/ambient), erosion field 512², thinner layer edge (edgeWidth 0.04 raised-cosine bevel, wearSoftness/edgeSharpness), thickness[4] + depthScale, Molten gold, Lead.
- Pass 1b (done, reviewed, fuzzed): any aspect ratio (rectangular isotropic fields), fit cover/contain/stretch + offset, RENDER settings block, PNG/JPEG/TIFF (inline decoder: LE/BE, 8/16-bit, none/LZW+predictor; 150 Mpx cap), 16-bit → RGBA16F.
- Pass 1c (done, reviewed — no bugs; one flag, fixed in pass 2: liquid strike read narrower than a drop): texture slots (solid: albedo/height→bump/roughness; liquid: brushing/HDRI), save/load settings JSON, impact model first half (drop + strike; sweep/blow/flow inert), Random 45 s uses the impact type.
- Pass 2 (done, reviewed — one house-style fix; three flags below): liquid strike rebuilt (zero-volume swell, lam/sigma 3.40, swell amp 0.30 + splash 0.4 of a drop's: wider AND lower — lip ring 1.75× a drop's at 2.5 s, peak 0.27× at 0.6 s); A6 per-layer height map (second TEXTURE_2D_ARRAY, R8/R16F, Height/Clear per layer, `layerBump` 0–2; solid bump crossfades with the stack, liquid = diffuse shading only); A4 relief coupling (`reliefWear` 0–1 in both mask shaders, `reliefCrack` 0–1 steers the crack planner, `RELIEF_K` 0.10). Details in PLAN-v2 "Done — pass 2".
- Pass 3a (done, reviewed — no edits; shipped as CORE with flags, look not yet right): third family `granular` (Sand, Dust): deposit field (RGBA16F pair, x height, yzw top-grain colour), crater + volume-conserving rim + thrown discs for drop/strike, repose relaxation (2 gather iterations/substep, quantised flows), top-grain colour rule (mud index 0), granular display (grain noise, matte, occlusion + cast shadow), GRANULAR sliders, `granular:{map,live}` settings block, generic Apply (patch) button. Liquid/solid pixel-identical. Six defects and the look flags are listed below and in PLAN-v2 "Done — pass 3a"; fix them in **3a-look** before 3b builds on the deposit field.
- Pass 3a-look (done, reviewed — no edits; two flags open): rim and disc colour by removed volume (decided once per event; drop gap 9.4 points, strike 13.7 — the feathered wall), `dep` RGBA32F with 16F fallback (stacked-drop creep gone in 32F), rim fed by the mask's actual increment (bottom-out / relief wear conserve), nearest-layer dithered bed colour (mud 0.002 % of pixels), 24 small irregular discs, Sand/Dust own Depth scale 0.8/0.6, `GRAN_SHADE_K` 1, repose gated by `REPOSE_TAIL` 8 s (freezes moving slides — flag), Apply names unknown keys. Details in PLAN-v2 "Done — pass 3a-look".
- Pass 3b-i (done, reviewed — one two-line edit; flags open): **wind on granular** (`#impact=blow`; band gust, stochastic hops: hop probability × `WIND_GRAB` 0.02, K = 4 exponential hop lengths × lateral ±1, exact-conservation gather, bed lift `windBed` 0.05; sliders `windLift` / `windCarry` / `windBed`), **repose gate on motion** (R8 "moved" output → 32×32 max reduction → PBO + fence every 0.25 s, stop after 0.5 s quiet; every stop is a fixed point), **strike rim colour by depth quantile** (82.4 % vs 82.3 % removed; was 39 vs 53), **grain boundary at full thickness** (one-sided dither 0.2), review fix for black texels (colour re-decided on a bare texel; 75 → 0). The first wind (whole film lifted every substep, fixed 20-texel carry) was rejected on the frames — stripes and a stamped "tube" — and rewritten before review. Details in PLAN-v2 "Done — pass 3b-i".

## Next passes (PLAN-v2 §C + IMPACTS.md)

2. ~~A4 + A6~~ done.
3. ~~Granular core~~ done (3a); ~~3a-look~~ done; ~~3b-i wind + gate + quantile + boundary~~ done. Left for **3b-ii**: **clods** (PLAN-v2 A9: three nested scales in one RGB id texture cut once per seed, cohesion rising with size, `clodFraction`, borders invisible until a break) + **`events.json` set-events** (`{t, type:"set", granular.live:{…}, ramp}`) so a piece can change wind/repose/grain over time; also from the 3b-i flags: band edge noise (a narrow blow's edge is a ruler line), a thin-deposit display rule or a lower `WIND_BED` against whole-canvas speckle, HUD "drops" count naming blows, strike rim relief (`GRAN_SHADE_K` or a taller strike rim), `fnote` wording. Then **3c**: particles for flying patches. The old 3a-look list, for the record: rim/grain colour carried by volume (colour of the layer being cut at each substep, top-grain rule per increment); repose exact above deposit 1 (store height scaled, or RGBA32F where it renders); crater floor through the grain rule, not the `layerMix` crossfade; thrown grains small and irregular (4–12 px, 30–40, particles later in 3c); relief visible at defaults (depth or shade); edge / bottom-out / 5th-strike volume accounted; `depDirty` reset; readout `map.seed` = frozen seed; Apply names unknown keys.
4. Sweep for all three media (absorb + pile).
5. Blow + flow for all three media.
6. B5 dispersive waves — **Opus**, isolated, revertible.
7. B2 offline render (`render.js`, pinned headless Chrome → PNG sequence → ffmpeg) + B3 `events.json` from the Malter recording (librosa onsets; pitch → position, velocity → energy). First 60 s at 1080p = the Blender decision point.

## Known flags (from reviews, not fixed)

- Display canvas cap is 2048 (was 1024): up to 4× pixels at DPR 2 on iPad → possible slowdown; one-line revert.
- 16-bit TIFF upload uses a 64 MB staging buffer; four 16-bit layers on an iPhone may hurt.
- Solid shader does 11 more texture reads per pixel since pass 1a.
- Kelvin → RGB has a small step at 6600 K (the approximation's own).
- Render lock is on at load but 1920×1080 does not match the 1:1 preview.
- `readMask()` returns zeros on devices without 32-bit float render targets.
- Layer edge in liquids: the old wide "greasy" bevel is gone by design; mean diff vs old 6.95 — Bekir has not yet said whether the new thin lip is right.
- Settings key is still `dropSize` while the slider reads "Energy" (cosmetic; rename when the save format next changes).
- Three 2048² 16-bit texture slots + 16-bit HDRI ≈ 170 MB on an iPad — keep textures at 1024 on mobile.
- Drops clustering → cracks become a lattice; to be solved by position rule in `events.json`, not in the prototype.
- (pass 2) Relief wear with an **8-bit** height map makes grain in the eroded depth on liquids (depth Laplacian p99 0.021 vs 0.002 with the same map as 16-bit TIFF). Fix: read the mask relief one mip coarser (`uLHLod + 1`) and/or store R16F whenever the device can. Defaults unaffected.
- (pass 2) `RELIEF_K` 0.10 is a mild lean (valley share of crack length +0.10 at reliefCrack 1 on a 50 %-contrast sine); real maps are gentler → try 0.2–0.25 with Bekir's maps.
- (pass 2) Both mask shaders compute the relief for every texel while reliefWear > 0; gate on `adv > 0` / `inc > 0` (same output, less work).
- (pass 2, pre-existing since 1c) A strike leaves a flat standing offset in the wave field (~0.015 per strike at swell amp 0.30; the old strike left 0.017). Invisible (display reads only the slope) and harmless in RGBA32F; on the RGBA16F fallback precision degrades after ~100 strikes. Fix later: subtract the field mean, or make the injection velocity-neutral.
- (pass 2) Solid display: +8 texture reads per fragment while a layer height map is in use (known +11 → +19); liquid display +8 under the same condition; masks +2/+3 while reliefWear > 0.
- (pass 3b-i) **Whole-canvas speckle**: one default E1 blow (area 0.6 → half-width 0.66 covers the canvas) moves 12.3 % of pixels by > 16 levels — dark grains on the light ground 0.3–0.4 widths downwind 0 → 11 %, light grains inside the silhouette 12.5 → 33.5 % — while the bed loses only 0.0056 mean. Levers: `WIND_BED` (0.05), a thin-deposit display rule (a 1-grain film should not fully recolour a pixel), or a smaller default `area` for blow. Bekir's taste call on iPad first.
- (pass 3b-i) **Ghost rim**: a second deposit peak of 0.047 (the rim's own gain 0.18) 36–48 texels downwind of a crater = the longest of the 4 hop classes landing in a ring. Lever: more classes / continuous lengths (cost ∝ taps), or a log-spaced set.
- (pass 3b-i) A narrow blow's edge is a ruler line (coverage 31 % → 0 over ~20 texels across the band). Fix in 3b-ii: noise on the band's half-width along the wind (hash of the along-wind coordinate × time).
- (pass 3b-i) Plume streaks along the wind: lag-1 autocorrelation of the lee gain 0.39 along vs 0.32 across (lateral jitter ±1 texel only). Lever: lateral ±2 (taps 12 → 20 per blow).
- (pass 3b-i) Hop lengths: at Energy 2 the longest class is clamped at `WIND_DMAX` 48 texels (mean hop 30 instead of 41); hop hashes use `uSalt` = substep mod 1024, so draws repeat every 17 s (invisible in tests; raise the modulus if a long still gust ever shows a pattern). `wrapP` uses `%` on negative ints — undefined in GLSL ES 3.00, test path (`GRAN.windWrap`) only.
- (pass 3b-i) Repose gate: the async PBO read makes Chrome warn "READ-usage buffer was written, then fenced, but written again before being read back" once per 0.25 s check in real-time play (not in batch; cause not found — moving `getBufferSubData` before `deleteSync` did not help); on SwiftShader 6 of 12 reads blocked — unknown on a real GPU (watch the HUD frame rate on iPad while a pile slides). `GRAN.reposeCap` default 0: the stress drop runs 54 s of repose passes. Mixed-format MRT (RGBA32F deposit + R8 moved; RGBA32F + RGBA16F mask on 16-bit-mask devices) untested on iOS — a failure refuses the granular family cleanly, as the 32F probe does.
- (pass 3b-i) HUD "drops" count includes blows (cosmetic). Not run: iOS / any real GPU; forced 16F deposit with wind; family switch with blow events.
- (pass 3a-look — FIXED in 3b-i: gate on motion, every stop a fixed point) `REPOSE_TAIL` 8 s stopped the repose while piles were still sliding: drop 15° at Depth 0.8 frozen at slope ratio 1.20 (now stops at 1.119 = the bound), stress drop at 1.82 (now 1.149 = the bound).
- (pass 3a-look — FIXED in 3b-i: depth quantile, 82.4 vs 82.3) Strike rim colour: 39 % red for 53 % removed (red 0.2 over blue); the bowl-depth map ignored the shallow feathered wall.
- (pass 3a-look) Strike rim reads as a flat dark disc with one lit crescent (relief swing 0.8× grain on the outer half; drop rim 2.9×). Lever: `GRAN_SHADE_K`, or a taller strike rim (W = R, half depth now).
- (pass 3a-look — half-thickness FIXED in 3b-i: boundary at full thickness, one-sided dither 0.2) Forced RGBA16F deposit (devices without `EXT_color_buffer_float`): stacked drops still creep +3.5 % at 6 s; a 16-bit mask sets `uRatioOn` 0 (and now wind's bed lift off), so bottom-out / wear no longer conserve there. Deposit program is 20 uniform vectors under the WebGL2 minimum of 224 (204 now; `uGd` 144 → data texture if a device fails). `fnote` refusal text still says "half-float".
- (pass 3a, defect — FIXED in 3a-look in RGBA32F) Repose creates volume once a texel's deposit exceeds 1 depth unit (half-float spacing 2^-10 above 1, 2^-9 above 2; flows are 2^-11): +1.6 % at 2 s, +4.5 % at 6 s and growing on three stacked Energy-2 drops; exact below 1. Fix in 3a-look.
- (pass 3a, defect — FIXED in 3a-look, strike gap 13.7 points remains) Rim and thrown-grain colour = the crater-bottom colour at the end of the build (repainted every substep), not the removed grains' colour by volume: red over blue, strike 0.25 deep → removed 88 % red, rim 86 % blue, all discs blue. Against the ruling. Fix in 3a-look.
- (pass 3a — bottom-out, 5th strike, `wearMul` FIXED in 3a-look; off-canvas loss is by design, noted in the readout) Off-canvas crater/rim volume is lost silently (centre at x 0.05: drop −30 %, strike −25 %); the stack bottoming out at white makes the rim exceed the crater (+13 % with 0.2 thicknesses); a 5th simultaneous strike drops its discs silently (−1 %); `wearMul` scales the crater but not the rim (code read).
- (pass 3a, look — rings, discs, crossfade, shade K addressed in 3a-look; strike rim still flat) Drops read as thin rings, not craters (rim 1–2 px at default Depth scale 0.3); thrown discs 15–30 px read as ink drops; crater floors between two layers show the `layerMix` crossfade (~4 % of pixels nearest the 50/50 mix on red/blue) — grains should not blend; `GRAN_SHADE_K` 2 shows 45° at a 34° limit; Energy scales the drop radius by √(E/0.5) while the note says depth only.
- (pass 3a — addressed in 3a-look: `reposeUntil`, frozen seed in the readout, unknown keys named) `depDirty` never resets: 2 repose passes (13-texel gather, 512²) every substep after the first event — no device timing yet. Readout `map.seed` shows the seed field, not the frozen `granMapSeed`. Apply accepts a patch without `version` and never names unknown top-level keys; `seed` beats `granular.map.seed` silently; a patch naming the current surface restarts and resets the granular sliders. `derived` is already RGBA16F, so the granular refusal only triggers if the deposit pair alone fails.
- (pass 3a) Load has never reset keys absent from the file (HEAD behaviour, found by the pass 3a review) — the brief's "missing keys → defaults" was never true; decide whether Load should.

## Open questions for Bekir

- Ear test (`fr-001-tintinnabuli`): which `|`, which ambiguity, is K too shrill? — unanswered since 31 Oct.
- Thin lip vs old bevel on the liquid edge — judge on iPad.
- Default layer thicknesses — advisor suggested [0.4, 1.5, 2.5, 3].
- Pass 3b-i on iPad (`#surface=sand&impact=blow`, or Random 45 s on Sand): does a default blow read as wind over sand, or as the picture dissolving into speckle? Is the whole-canvas speckle (12 % of pixels) too much — smaller default area, or weaker bed? Does the lee smear behind a crater read as a drift? Frame rate while a pile slides (the repose gate's readback) and during a gust. Is the top image's full thickness now right (the lower layer appears only in the last fifth)?
- Pass 3a-look on iPad: Sand drop at defaults — crater or ring? Strike — does the dark rim read as sand thrown out, or as a disc? Are the small discs grains? Frame rate while repose runs (first 8 s after an event).
- Pass 3a on iPad: do drops read as craters or rings? Do the thrown discs read as grains or ink? Is relief visible at defaults? Does Dust differ from Sand? Frame rate with the repose passes running (HUD).
- Pass 2 taste calls: is the strike's basin (swell amp 0.30) right on screen? Is `reliefCrack` strong enough with real maps? — judge with his own height maps.
- Send the UE brief (§11.6 of the project file), now for two works (Alina, Cantus); ECM master quote in parallel.
