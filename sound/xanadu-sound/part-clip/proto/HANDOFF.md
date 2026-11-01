# HANDOFF — Xanadu Sound / Pärt clip prototype

For the next chat. Written 1 Nov 2026 by the advisor at the end of a two-day session (31 Oct–1 Nov). Read this first; then PLAN-v2.md, IMPACTS.md, and `docs/XANADU-SOUND-project.md` §10–11.

## How to start the next chat

1. Attach the repo `bektaron/MJDL` (push access). Everything lives under `sound/xanadu-sound/`.
2. Say: "Read sound/xanadu-sound/part-clip/proto/HANDOFF.md and continue."
3. Working language Turkish; system files English. Address: Üstadım.

## What exists (all pushed to `main`, last commit of this session is listed at the bottom)

| Path | What | State |
|---|---|---|
| `docs/XANADU-SOUND-project.md` v0.2 | project brief; §10 Pärt clip (design, rulings, realisation notes); §11 research integration; Appendix A = research report | authoritative |
| `docs/XANADU-SOUND-research.md` v0.1 | five-agent research (sonification, rule systems, toolchain, rights, exhibition) | reference |
| `fr-001-tintinnabuli/index.html` | ear test for the sound work: tintinnabuli rule, old/new `|` and ambiguity toggles, three densities | **not yet listened to by Bekir** |
| `part-clip/proto/index.html` | the WebGL2 prototype (one file, no libraries) | live at `bektaron.github.io/MJDL/sound/xanadu-sound/part-clip/proto/` |
| `part-clip/proto/PLAN-v2.md` v2.1 | refinement plan: three axes, passes, "Done" log | authoritative |
| `part-clip/proto/IMPACTS.md` v1 | impact model: drop / strike / sweep / blow / flow × liquid / solid / granular | authoritative |

## Rulings by Bekir (do not reopen without him)

- First clip: **Für Alina, piano only** — Alexander Malter, ECM *Alina* (1999), track 2, 10:47.
- Second: *Spiegel im Spiegel* (open; violin = blow/flow idea on file). Third: **Cantus in memoriam Benjamin Britten** for the **sweep** impact.
- Three axes, **never mixed in one piece**: medium (liquid / solid / granular) · layer (image + its own height map, up to 4, then white) · impact (five types, four numbers: energy, area, duration, direction).
- Sweep **absorbs** and **piles at its edge**; blow **pushes solids** (piece size = medium, scaled by energy — advisor's proposal, accepted "don't know"); flow flows.
- Drops do not start by themselves; he taps. Random 45 s mode exists for sequences.
- Erosion bottoms out at **white**; no wrap.
- Stay in WebGL; Blender only if the 1080p test render fails the eye.
- Nothing public until Universal Edition answers (§11.6 brief not yet sent). ECM master licence or a new recording also needed.

## Working method (he asked for this explicitly: "no haste, nothing sloppy")

- Each pass: **Sonnet writes** (small, scoped brief; pixel-identical at defaults; node --check; headless Chrome at 390×844 and 1024×768 with `#surface=…&auto=1&seek=7`; screenshots) → **Opus reviews independently** (diff vs commit, measured regressions, determinism, iOS risks, wiring of every slider; fixes clear bugs, flags the rest) → advisor looks at screenshots → **push**. Commits as Bekir with the Claude co-author trailer.
- Never commit a file an agent is still editing. Never send a message to a running agent (two were lost that way — the harness reported "stopped by the user"; cause unclear, probably an interrupted tool call). If an agent dies mid-edit: back up the half state to the scratchpad, `git checkout --` the file, re-run in smaller slices.
- He is often on the phone: send 1–4 rendered frames (headless Chromium, software GL is slow: 5 frames ≈ 10 min) rather than asking him to open the page. `#seek=N` fast-forwards the sim; `#auto=1` turns on synthetic events; `#surface=`, `#aspect=`, `#impact=`, `#drop=`, `#random=1&seed=N` exist.
- Useful hooks on `window.XANADU`: `fieldRes`, `light`, `readMask()`, `step`, `fire`.

## Pass log

- Pass 1a (done, reviewed): light panel (azimuth/elevation/intensity/Kelvin/ambient), erosion field 512², thinner layer edge (edgeWidth 0.04 raised-cosine bevel, wearSoftness/edgeSharpness), thickness[4] + depthScale, Molten gold, Lead.
- Pass 1b (done, reviewed, fuzzed): any aspect ratio (rectangular isotropic fields), fit cover/contain/stretch + offset, RENDER settings block, PNG/JPEG/TIFF (inline decoder: LE/BE, 8/16-bit, none/LZW+predictor; 150 Mpx cap), 16-bit → RGBA16F.
- Pass 1c (done, reviewed — no bugs; one flag: **liquid strike reads narrower than a drop**, outer ring r95 268 px vs 355 px at 2.5 s — fix first in pass 2: strike should spread over `area`, lower amplitude, wider ring): texture slots (solid: albedo/height→bump/roughness; liquid: brushing/HDRI), save/load settings JSON, impact model first half (drop + strike; sweep/blow/flow inert), Random 45 s uses the impact type.

## Next passes (PLAN-v2 §C + IMPACTS.md)

2. A4 + A6: per-layer height map (bump; cracks prefer valleys, ridges wear first).
3. Granular medium (sand/dust): height transport, angle of repose; drop + strike.
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

## Open questions for Bekir

- Ear test (`fr-001-tintinnabuli`): which `|`, which ambiguity, is K too shrill? — unanswered since 31 Oct.
- Thin lip vs old bevel on the liquid edge — judge on iPad.
- Which medium for *Für Alina*: liquid (advisor's view) or solid?
- Default layer thicknesses — advisor suggested [0.4, 1.5, 2.5, 3].
- Send the UE brief (§11.6 of the project file), now for two works (Alina, Cantus); ECM master quote in parallel.
