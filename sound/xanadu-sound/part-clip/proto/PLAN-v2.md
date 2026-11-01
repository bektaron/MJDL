# Pärt clip prototype — refinement plan v2

1 Nov 2026 · v2.1 (09:10) · approved structure: three axes (medium / layer / impact), never mixed · prototype: `part-clip/proto/index.html` (WebGL2, one file)

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
| A6 | **Per-layer height map and image** (added 09:01; narrowed 09:08) | Each of the 4 layers is a **layer set**: albedo (the profile variant or any image) + its own height map. Erosion reveals another image *with its own relief*. Material is **not** per layer (see §A7): one medium per piece. | [☀️] |
| A7 | **Three axes, never mixed** (09:06–09:08) | **Medium** (one per piece): liquid / solid / **granular** (sand, dust, grime). Material numbers and material textures live here. **Layer** (up to 4): image + height only. **Impact** (per event): drop / strike / blow. Media do not mix within a piece — no cooling metal, no mud; B6 is dropped. | [☀️] |
| A8 | **Impact types: drop, strike, blow** | Every event carries four medium-independent numbers — **energy, area, duration, direction** — and the medium turns them into its own physics. The three types are presets of those four. `events.json` carries only the four numbers. Per medium: *drop* = ring wave / hairline-to-cluster crack / crater with scatter; *strike* = broad low swell + splash / fissure with spalling / wide pit, grains thrown; *blow* = directional micro-waves while it lasts (the "violin as wind" idea, now medium-independent) / abrasion, skin peels along the brush / grains blown away, the layer below exposed. | [☀️] drop, strike; [🌤️] blow |
| A9 | **Granular medium** | Not a wave equation: height transport — grains pushed outward from the impact, slide when the slope exceeds the angle of repose, pile up. Erosion is the most natural here: where grains leave, the layer below is bare; depth = grain-layer thickness (a real physical meaning for B4). Grain texture slot (albedo + grain size). | [🌤️] grain feel at 512² may stay soft |
| A5 | **Light direction, strength, temperature** | Light panel: azimuth (0–360°), elevation (5–85°), intensity, colour temperature (2000–10000 K → RGB via a standard approximation), plus ambient level and HDRI rotation (if an HDRI is loaded, it rotates with the light). Shadows and the bevel highlights follow it. | [☀️] |

## B. Advisor's proposals

| # | Proposal | Why | Risk |
|---|---|---|---|
| B1 | **Texture slots per surface** (from 1 Nov conversation) | Albedo/height/roughness/normal uploads replace the procedural rust/bronze and the brushing; the liquids get a brushing texture slot and an **HDRI slot** (equirectangular, for real reflections). | [☀️] |
| B2 | **Offline render to PNG sequence** | The point of staying in WebGL: `render.js` (headless Chrome, pinned) steps the sim deterministically from `events.json` and writes frame-0000.png … at the chosen size/fps; ffmpeg assembles ProRes/H.265. Without this, nothing becomes a clip. | [☀️]; speed [🌤️] (4K × 16k frames: hours) |
| B3 | **`events.json` from the recording** | Onset detection on Malter's track (librosa, Python) → {t, pitch, vel}; the prototype's drop rule reads it. Pitch → position, velocity → size. Hand-correctable in a text file. | [☀️] detection; [🌤️] *Alina*'s soft onsets may need threshold tuning |
| B4 | **Layer thicknesses** (from 31 Oct) | `[t0, t1, t2, t3]` per layer instead of equal units; visible depth derived from accumulated erosion. Thin skin, thick core. | [☀️] |
| B5 | **Dispersive waves** (separate pass, Opus) | Real liquid: short ripples travel faster than long swells; the current single-speed equation looks "drawn". Multi-band Verlet (2–3 bands) or spectral. Isolated so it can be reverted. | [🌤️] two passes possible |
| B6 | ~~Cooling metal~~ — **dropped** 09:08 (media never mix, A7). | — |
| B7 | **Two more liquids by numbers**: molten gold, lead | Cheap; gives warm and dull options next to the cool ones. | [☀️] |
| B8 | **Save / load settings** as a `.json` file (not only the readout) | Settings survive a reload; a chosen look is a file in the repo. | [☀️] |

## C. Order and model

| Pass | Contents | Model | Size |
|---|---|---|---|
| **1** | A1, A2, A3, A5, B1, B4, B7, B8 — additive, same file; plus the **impact model** (A8: four numbers, three presets, drop + strike for liquid and solid) | Sonnet | one long session |
| **2** | A4 + A6 (per-layer image + height, bump, crack/wear follow relief) | Sonnet | one session |
| **3** | A9 **granular medium** (drop + strike) | Sonnet | one session, maybe two |
| **4** | A8 **blow** for all three media | Sonnet | one session |
| **5** | B5 (dispersive waves) — isolated | Opus | one session, maybe two |
| **6** | B2 (offline render) + B3 (events from the recording) — first 1080p test render of 60 s | Sonnet + Python by advisor | one session + render time |

Each pass ends with: `node --check`, headless load at phone and iPad sizes, screenshots, push to `main`, one line in this file under "Done".

## D. What this does *not* do

- No audio in the prototype (rights; the recording is ECM's). Timing comes from `events.json` only.
- No Blender. If pass 4's test render fails the eye, Blender is the next plan, and only the look moves there — rules and events stay in JSON.
- The UE brief (§11.6 of the project file) is still the gate for any public showing; nothing here changes that.

## Done

- **1 Nov 2026 — Done — pass 1a** (A5, A1, B4, B7; `proto/index.html`, one file, no new libraries). A5: LIGHT block (azimuth, elevation, intensity, colour temperature via Tanner Helland normalised to 6500 K = white, ambient) read by every shading term (liquid diffuse/specular/Fresnel environment bands, solid diffuse/specular/bevel highlight/occlusion-shadow); defaults are the old hard-coded directions, so the look is unchanged (checked: pixel-identical on liquids with the old bevel off). A1: mask/erosion field 256² → 512² (`FIELD_RES`; falls back to 256 if `MAX_TEXTURE_SIZE` < 4096 or the float target fails; the wave field stays 256² and shares no texture with it, so only the mask pass grows 4×); `edgeWidth`/`edgeHeight` bevel and `edgeSharpness` lip (liquids; the solid gets the lip, not the bevel); `erodeSoftness` → `wearSoftness` (same behaviour). B4: mask holds depth units, `thickness[4]`, `depthScale` (liquid slope field, solid occlusion/shadow heightfield). B7: Molten gold and Lead. JSON gains `light`, `wearSoftness`, `edgeSharpness`, `edgeWidth`, `edgeHeight`, `thickness`, `depthScale`; `erodeSoftness` removed.
- **1 Nov 2026 — Done — pass 1b** (A2, A3; `proto/index.html`, one file, no new libraries). A2: ASPECT block (1:1 default, 16:9, 9:16, 4:5, 21:9, custom W : H from 1:4 to 4:1; `#aspect=16:9`); a change rebuilds every field at the new shape and restarts the piece. Wave, erosion mask, crack, fragment and derived fields are rectangular, long side = the old constant (256 / 512 / 512), short side scaled, so texels stay square; every length (impulse radius and wavelength, border sponge, crack length and width, feather, bevel, noise, shadow reach) is measured in long-side units, and the crack geometry is built in those units and divided by the canvas extent in the vertex shader. At 1:1 the stage is pixel-identical to pass 1a (mercury and rusted iron, 390 and 1024 wide). Preview: fitted to the free area, backing store up to 2048 on the long side (was 1024), DPR up to 2. Image fit (cover / contain / stretch, offset x / y −1…1; default cover, centred) applies to all four layers; uploads are fitted at 1024 on the long side (was 512), procedural placeholders are drawn at the canvas aspect. RENDER block (settings only): size up to 3840×2160 locked to the aspect (even numbers; long side kept when the aspect changes), fps 24 / 25 / 30 / 60, duration (647 s), label; JSON gains `aspect`, `fit`, `render`. A3: PNG and JPEG as before; inline TIFF decoder (II / MM; none and LZW with predictor 2; 8 and 16 bit; RGB, RGBA, grey, WhiteIsZero; strips; orientation); tiles, JPEG / ZIP / PackBits, float, signed, CMYK / palette, planar 2, BigTIFF, a second full-size page, truncated or damaged data are refused with the reason shown under the upload button. A 16-bit TIFF makes the layer stack RGBA16F (8-bit fallback if the device cannot); a 16-bit PNG goes through the browser at 8 bits (tooltip). Tests (kept in the session scratchpad `tiff-test/`, not in the repo): `mktiff.py` makes 83 files with our own LZW encoder, Pillow and tifffile; `tifftest.js` runs the shipped decoder verbatim: 64 decoded exactly, 19 refused with the right reason.
