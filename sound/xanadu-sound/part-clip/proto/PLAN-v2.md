# Pärt clip prototype — refinement plan v2

1 Nov 2026 · for approval by Bekir before any work starts · prototype: `part-clip/proto/index.html` (WebGL2, one file)

Decision context: we stay in WebGL for now; Blender only if the 1080p test render reads as a "screen effect" (§10 of the project brief, advisor's view 1 Nov). This plan refines the prototype toward a renderable clip for *Für Alina* (Malter/ECM, 10:47, piano only).

Marks: [☀️] certain · [🌤️] likely, may need a second pass · [☁️] uncertain.

---

## A. Bekir's additions (1 Nov)

| # | Request | What will be built | Risk |
|---|---|---|---|
| A1 | **Eroded layer edge looks too thick** — light? resolution? | Both, plus one more. (i) The erosion field is 256² while the image is 512²+: the layer boundary is upsampled, so its edge is 2–4 px wide at best. → erosion/mask field to **512²** (1024² optional on desktop). (ii) The "bevel" at the boundary is a fixed slope → make its width and height sliders (`edgeWidth`, `edgeHeight`), default much thinner. (iii) The crossfade between layers is wide by design (`erodeSoftness`) → separate the *worn-skin* softness (wide, for the surface wear) from the *edge* sharpness (narrow, for the lip where the layer ends): two sliders instead of one. | [☀️] |
| A2 | **Any aspect ratio, resolution, size; video limits set accordingly** | Canvas becomes W×H (presets 16:9, 9:16, 1:1, 4:5, 21:9, custom). Simulation fields become rectangular at the same aspect. Profile images are fitted by a chosen rule (cover / contain / stretch, with offset). **Render settings** panel: output width/height (up to 3840×2160 — [🌤️] GPU-dependent), fps (24/25/30/60), duration (free; 10:47 preset), bit depth. These settings go into the JSON readout and into the offline render job (B2). | [☀️] canvas; [🌤️] 4K on iPad: display stays ≤ 2K, 4K is for offline render only |
| A3 | **TIFF and PNG, not only JPEG** | PNG: native [☀️]. TIFF: browsers do not decode TIFF; add a small inline decoder (uncompressed / LZW / 8- and 16-bit, no external library) — [🌤️] covers Photoshop's default TIFF exports; exotic TIFFs (ZIP, 32-bit float, layered) will be refused with a message. 16-bit PNG/TIFF are read at 16-bit and uploaded as half-float textures. | [🌤️] |
| A4 | **Metal surface works with a height map, bump-like** | Each surface gets a **texture set**: albedo (colour), height (grey → bump), optional roughness and normal. Height is turned into a normal in-shader (`bumpStrength` slider, 0–2) and *added* to the simulation normal (wave or crack). Height also modulates the crack path for solids (cracks prefer valleys) [🌤️] and wear (ridges erode first) [🌤️]. | [☀️] bump; [🌤️] crack/wear coupling |
| A6 | **Per-layer height map and surface** (added 09:01) | The stack is no longer "4 images + one surface": each of the 4 layers is a **layer set** — albedo (the profile variant or any image), its own height map, and optionally its own surface material (liquid/solid type and numbers, or "inherit from above"). So: top layer rusted iron with its own relief, second layer bare steel with another, third a different profile on gallium… Erosion reveals not only another image but another *material*. The shader samples albedo/height/material from the layer under the current erosion value (and the one above, for the crossfade). The wave sim stays one field; only the *shading* and the *crack/wear behaviour* change per layer. ☁ Open: whether a drop on a liquid top layer that has worn down to a solid lower layer should crack there — I would say yes, and that makes B6 (cooling metal) a special case of this. | [☀️] per-layer albedo + height; [🌤️] per-layer material switching mid-piece |
| A5 | **Light direction, strength, temperature** | Light panel: azimuth (0–360°), elevation (5–85°), intensity, colour temperature (2000–10000 K → RGB via a standard approximation), plus ambient level and HDRI rotation (if an HDRI is loaded, it rotates with the light). Shadows and the bevel highlights follow it. | [☀️] |

## B. Advisor's proposals

| # | Proposal | Why | Risk |
|---|---|---|---|
| B1 | **Texture slots per surface** (from 1 Nov conversation) | Albedo/height/roughness/normal uploads replace the procedural rust/bronze and the brushing; the liquids get a brushing texture slot and an **HDRI slot** (equirectangular, for real reflections). | [☀️] |
| B2 | **Offline render to PNG sequence** | The point of staying in WebGL: `render.js` (headless Chrome, pinned) steps the sim deterministically from `events.json` and writes frame-0000.png … at the chosen size/fps; ffmpeg assembles ProRes/H.265. Without this, nothing becomes a clip. | [☀️]; speed [🌤️] (4K × 16k frames: hours) |
| B3 | **`events.json` from the recording** | Onset detection on Malter's track (librosa, Python) → {t, pitch, vel}; the prototype's drop rule reads it. Pitch → position, velocity → size. Hand-correctable in a text file. | [☀️] detection; [🌤️] *Alina*'s soft onsets may need threshold tuning |
| B4 | **Layer thicknesses** (from 31 Oct) | `[t0, t1, t2, t3]` per layer instead of equal units; visible depth derived from accumulated erosion. Thin skin, thick core. | [☀️] |
| B5 | **Dispersive waves** (separate pass, Opus) | Real liquid: short ripples travel faster than long swells; the current single-speed equation looks "drawn". Multi-band Verlet (2–3 bands) or spectral. Isolated so it can be reverted. | [🌤️] two passes possible |
| B6 | **Cooling metal** (new liquid type) | Viscosity and tension rise with time; past a threshold the surface hands over to the solid family and freezes the wave map — liquid becomes crust becomes crack in one piece. Joins the two families. | [🌤️] transition tuning |
| B7 | **Two more liquids by numbers**: molten gold, lead | Cheap; gives warm and dull options next to the cool ones. | [☀️] |
| B8 | **Save / load settings** as a `.json` file (not only the readout) | Settings survive a reload; a chosen look is a file in the repo. | [☀️] |

## C. Order and model

| Pass | Contents | Model | Size |
|---|---|---|---|
| **1** | A1, A2, A3, A5, B1, B4, B7, B8 — all additive, same file | Sonnet | one long session |
| **2** | A4 + A6 (per-layer sets: albedo, height, material; bump; crack/wear coupling), B6 (cooling metal, as a case of A6) | Sonnet | one session, maybe two |
| **3** | B5 (dispersive waves) — isolated | Opus | one session, maybe two |
| **4** | B2 (offline render) + B3 (events from the recording) — `render.js`, `events.py`, first 1080p test render of 60 s | Sonnet (render) + Python by advisor | one session + render time |

Each pass ends with: `node --check`, headless load at phone and iPad sizes, screenshots, push to `main`, one line in this file under "Done".

## D. What this does *not* do

- No audio in the prototype (rights; the recording is ECM's). Timing comes from `events.json` only.
- No Blender. If pass 4's test render fails the eye, Blender is the next plan, and only the look moves there — rules and events stay in JSON.
- The UE brief (§11.6 of the project file) is still the gate for any public showing; nothing here changes that.

## Done

_(empty)_
