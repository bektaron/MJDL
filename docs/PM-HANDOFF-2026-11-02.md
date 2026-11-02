# Handover to the Project Manager — MJDL · Xanadu Sound · Pärt clip

**Period covered:** four working sessions, 29 Oct – 3 Nov 2026 ("Mermaid akış şeması", "Mermaid akış şeması dosyaları", "Arvo Pärt klip tasarımı", "MJDL HANDOFF.md …").
**Written by:** the advisor (Claude), 2 Nov 2026, 07:30 CET, for Bekir Kıraç, on his request. **Updated 3 Nov 2026, ~02:30 (Istanbul)** after pass 3b-i (wind) was reviewed and pushed; changes are marked "(3 Nov)".
**Language:** English, per the Oct 2026 ruling that all MJDL system files are written in English.

**Provenance.** The advisor had no access to the MJDL project's own canons and references in any of these sessions; everything about the Perception Cloud below is what Bekir stated or approved in conversation, and the PM must check it against the project files. Marks: [☀️] measured or counted, [🌤️] strong inference, [☁️] gap filled by the advisor, [📜] ruling by Bekir recorded in a project file, [🔍] looked up.

---

## 0. The one-paragraph state

Three streams. (1) **MJDL / Perception Cloud**: the interactive reference tool *XAN Partition View* reached v28 and a reusable layout engine (*phobia-engine.js* 0.2, *Phobia Lab* v8) was built and accepted "subject to develop"; a phase-model physics trial was parked by ruling. This stream lives in a zip package (`MJDL-package-2026-10-30.zip`), **not in the git repo**. (2) **Xanadu Sound**: the sonification of the cloud was spun off as its own project; two listening pages (FR-001, FR-002) and a tintinnabuli ear-test page are live on GitHub Pages; the ear test is unanswered since 31 Oct. (3) **Pärt clip** (a sub-project of Xanadu Sound): a single-file WebGL2 prototype of a picture that is a surface — liquid, solid or sand — struck by the notes of *Für Alina*; eight reviewed passes are pushed to `bektaron/MJDL` (`sound/xanadu-sound/part-clip/proto/`), the last one (3b-i, **wind on sand**) at 02:10 on 3 Nov. The granular ("the image is the sand") medium is in and correct in its accounting; a gust now carries the picture's grains downwind (the sand's natural impact), the sliding piles stop when they really stop, and the top image keeps its full thickness. Still unjudged by Bekir on a real screen: the strike's flat rim and how much a default gust speckles the whole picture. No audio and no public showing until Universal Edition answers a licence letter that has not been sent.

---

## 1. What was done, by session

### 1.1 — 29 Oct, "Mermaid akış şeması" (MJDL)
- Opened with the **visual ↔ conceptual-emotional correlation study** idea: the advisor describes images physically (and measures palette, contrast, edge density etc. in code), Bekir reads them conceptually; both blind to the prompt; fixed axes, 1–7 scores, self-consistency re-scoring. Judged worth doing as a *tool* (Bekir's personal visual grammar), not as science; main risk is banal findings. [🌤️] Status: designed, not started.
- **XAN Partition View** (single HTML file, offline, SVG) carried from v18 to v22: help drawer (`?`), per-partition colour pickers (viewer preference, not data), full **EN/TR interface** with the ruling that **codes never translate** (XAN, F S E K, gene codes, TEX·MOT·INT, ⟡, `& |`, property tags). [📜]
- Documents created/maintained: `MJDL-cloud-configuration.md` (0.10 → 0.14), `MJDL-PM-brief.md` (change log from 30 Oct 10:30), the procedure/definitions/transition notes, a README; packaged as `MJDL-package-2026-10-30.zip`.
- **Sonification** first sketched as a joke, then ruled a work in its own right: "nodüler beste" — the cloud as a score, sound sold with the images. A plan file was written (no code). [📜]

### 1.2 — 30–31 Oct, "Mermaid akış şeması dosyaları" (MJDL)
- Relations display was too cluttered → mockup of alternatives → **"type clouds"** approved (relations grouped by type into tagged clouds with lettered sub-clouds) → built as Partition View v26; later v28. [📜]
- Bekir's layout rules — labels on strings, unrelated things **"phobic"** of each other, zoom, size tiers on focus, drag anything — became a standalone, DOM-free **`phobia-engine.js`** (0.1 → 0.2) with a public API and a single-page **Phobia Lab** (v8): elastoplastic clouds, the "drop" drag model (grab point = membrane tip, capsules lag in a bulb), nested sub-clouds (F's SUB/TEX/MOT), sliders. Numerically verified after three drag types (no capsule overlap, no cloud intersection, no foreign label). [☀️ for the checks]
- Rulings: the phobic rule is first priority and applies to the whole cloud; the engine is **infrastructure to reuse in other projects** and to be saved as it matures; the Lab will live in the cloud's **settings section**; capsules are weightless under all conditions; motion mechanics is the base the other layers are rewritten on. [📜]
- **Phase model** (solid → liquid → gas by one slider φ): plan page with sketches approved, then trial 1 (`phobia-phase-lab.html`, hand-tuned springs) built and judged "doesn't inspire confidence". Advisor's view: the limitation is the hand-tuned-force approach, not JavaScript; **XPBD** is the technique to use if resumed; Python would not help and would cost iPad access. **Ruling: stop here — Phobia Lab v8 + engine 0.2 is the accepted point**; trial parked. [📜]
- Package closed at phobia table 0.7, brief 09:00 CET 31 Oct. **Partition View v28 is not yet rewired onto the engine** (v29 was started, not packaged because untested).

### 1.3 — 31 Oct – 1 Nov, "Arvo Pärt klip tasarımı" (Xanadu Sound, Pärt clip)
- Xanadu Sound brief read back (v0.1 → v0.2): why a separate project, what exists (FR-001/FR-002 pages, QR-ready), three forms (*line / layers / soft*), data contract, open decisions, six-step roadmap. Ear-test page `fr-001-tintinnabuli` built; a research report added.
- **New sub-project: a clip for Arvo Pärt.** Rulings: first clip *Für Alina*, **piano only** (Alexander Malter, ECM *Alina*, 10:48); wind layer reserved for *Spiegel im Spiegel*; third piece *Cantus in memoriam Benjamin Britten* for the sweep impact. The visual flow is Bekir's own, the music accompanies it — **the concept paragraph is not to be written until Bekir dictates it.** [📜]
- Prototype built from a first WebGL sketch (liquid-metal surface, woman's profile, notes as drops) through reviewed passes **1a / 1b / 1c**: light panel, erosion field, layer stack of four images with thicknesses, solid surfaces with crack clusters, any aspect ratio, PNG/JPEG/TIFF (8/16-bit, inline decoder), texture slots, settings JSON save/load, impact model v1 (**drop, strike, sweep, blow, flow**; the last three inert for now), Random 45 s mode. Plan v2.1 fixes three independent axes — **medium / layer / impact** — never mixed within a piece. [📜]
- Working method set, at Bekir's "no haste, nothing sloppy": **Sonnet writes a scoped pass → Opus reviews independently (never saw it written) → advisor looks at frames and sends Bekir 1–4 → push to `main` as Bekir** with the Claude co-author trailer; no half-built file is ever committed. `HANDOFF.md` written for session-to-session continuity.

### 1.4 — 1–2 Nov, "MJDL HANDOFF.md …" (Pärt clip, this session)
- **Pass 2:** liquid strike rebuilt (wide, low, zero-volume swell — it had read as a narrower drop), per-layer **height maps** (A6), **relief coupling** (A4: wear follows relief, cracks lean into valleys). Advisor overrode the writer on one constant (swell amplitude 0.02 → 0.30) after rendering both. [☀️] Pixel-identical elsewhere.
- **Ruling (1 Nov, 17:08): "the surfaces are made of sand; the pixels are grains; water or wind wear it and reveal what is beneath; sweep draws the pixels in."** Reference: the Mural of Souls in *Foundation*. Follow-ups: layer count stays 4 for now; pixels may be grouped into random-size clusters so plates break off (clods); the granular part must be a **settings file**, changeable per situation; Bekir said "proceed with your proposals". [📜]
- **Pass 3a:** third family `granular` (Sand, Dust): deposit field, crater + volume-conserving rim + thrown grains, angle-of-repose relaxation, a **top-grain colour rule (no averaging anywhere → no mud)**, granular display, `granular:{map, live}` settings block, a generic **Apply (patch)** button. Review: ship with flags; two defects found.
- **Pass 3a-look:** the two defects fixed (rim colour now carries the removed grains by volume; 32-bit deposit field), conservation under bottom-out and relief wear, dithered nearest-layer bed (crossfade "mud" 5 % → 0.002 % of pixels), 24 small irregular thrown grains instead of 12 ink-drop discs, Sand/Dust own default depth, Apply names unknown keys. Review: ship with flags (below). Pushed 02:00, commit `277edcb`.
- Docs: PLAN-v2 "Done" log (full measurements per pass), HANDOFF pass log and flags, IMPACTS.md, project file §10 (the sand ruling in Bekir's words), PLAN-v2 A9 (3b design: wind, clods, nested cell scales, set-events).
- **(3 Nov) Pass 3b-i — wind on sand, and the three leftovers from 3a-look.** Bekir, from a plane, chose to go on with 3b over the advisor's advice to render first ("bence sen 3b'ye giriş"); the advisor split 3b into 3b-i (wind + leftovers) and 3b-ii (clods + set-events) to keep passes reviewable. Timeline (Istanbul): first writer 12:50–15:11; the advisor rejected its wind on the frames (D-wide stripes, the crater rim stamped downwind as a "ringed tube", 82 % of the moved sand leaving the canvas — a conveyor, not wind) and wrote a fix brief; second writer 17:26–18:58 (stopped by a permission prompt tapped on the phone; its detached test queue ran on to 21:28); Opus review 21:29 → interrupted by a container restart at 01:08 → resumed → verdict 01:55 "ship with flags", one two-line fix (black texels 75 → 0); docs, commit `88b9bea`, push 02:10. **Delivered:** blow on granular as a band gust with **stochastic hops** (a grain hops ~3 times a second at wind 1, hop length drawn from four exponential classes, exact volume conservation ≤ 2e-7 in wrap mode; open edges lose what leaves, by design); three sliders `windLift` / `windCarry` / `windBed` under `granular.live`; **repose gate on motion** (a GPU "moved" flag read back every 0.25 s; piles stop at the slope bound, 1.119 where 3a-look had frozen them at 1.20); **strike rim colour by the removed volume's depth quantile** (82.4 % vs 82.3 % removed; was 39 vs 53); **layer boundary at the layer's full thickness** (3a-look showed the top image to half its thickness). Liquid and solid pixel-identical on 10 scenes. Bekir also asked for a sixth impact type, **scratch** (kazıma), recorded in IMPACTS.md, unscheduled.

---

## 2. Rulings in force (Bekir's decisions — the canon for these streams)

| Stream | Ruling | When |
|---|---|---|
| MJDL | System files in English; conversation in Turkish | Oct 2026 |
| MJDL | Codes and abbreviations never translate | 30 Oct |
| MJDL | Type clouds for relations; phobic rule first priority, whole cloud | 30 Oct |
| MJDL | phobia-engine = reusable infrastructure; Lab lives in settings; capsules weightless; motion mechanics is the base | 30–31 Oct |
| MJDL | **Stop at Phobia Lab v8 + engine 0.2**; phase trial parked | 31 Oct 08:52 |
| MJDL | Public pages in `bektaron/MJDL` (GitHub Pages), never on claude.ai addresses | 30 Oct |
| Xanadu | Sonification = a work ("nodüler beste"), sold with the images; separate project | 30 Oct |
| Pärt | First clip *Für Alina*, piano only, Malter/ECM recording; wind layer for *Spiegel*; *Cantus* = sweep | 31 Oct – 1 Nov |
| Pärt | *Für Alina* medium = **liquid** | 1 Nov |
| Pärt | Three axes (medium / layer / impact) never mixed in a piece; sweep **accumulates** (does not vanish); erosion bottoms out at white; Blender not now; nothing public before UE answers | 31 Oct – 1 Nov |
| Pärt | **The image is the sand** (granular ruling, 17:08); 4 layers for now; clods of random size; granular = a settings file; concept paragraph only when Bekir dictates it | 1 Nov |
| Pärt | UE letter with two options: commercial sale / exhibition only | 1 Nov |
| Process | No haste; Sonnet writes → Opus reviews → advisor checks frames → push as Bekir; never commit a half-built file | 31 Oct |

---

## 3. Problems and open flags

### 3.1 Blocking or risky
1. **The MJDL package is not under version control.** Partition View v28, phobia-engine 0.2, Phobia Lab v8, the phase trial and the five docs exist only in `MJDL-package-2026-10-30.zip` (delivered to Bekir) and in claude.ai artifacts. One lost zip = the stream is gone. [☀️] Recommendation: commit the package to `bektaron/MJDL` (private folder or a second repo) before any further work on it.
2. **Rights.** The Pärt clip uses an ECM master (Malter) and Universal Edition's score. The UE letter (§11.6 of the project file) is **not sent**; it needs venues/dates, edition size, online y/n, an artist sentence + still — all from Bekir — and the Cantus UE catalogue number must be verified. ECM master quote not requested. Nothing public until then. [📜]
3. **Nothing has been seen on a real screen since pass 2.** All pass 3a / 3a-look / 3b-i verification ran in software GL (SwiftShader) at 10–60 s per frame; frame rate on iPad, 16-bit fallbacks and real-GPU behaviour are untested. Bekir's iPad test scenario is written (six steps, two images) and pending. (3 Nov) 3b-i adds two real-GPU unknowns: the repose gate's asynchronous read-back (Chrome prints a buffer warning once per 0.25 s check in real-time play; cause not found) and the mixed-format render targets (32-bit deposit + 8-bit "moved" flag) on iOS — a failure there refuses the sand family cleanly, it does not crash. [☀️]
4. **The ear test is unanswered since 31 Oct** (`fr-001-tintinnabuli`: which `|`, which ambiguity, is K too shrill). Xanadu Sound's roadmap step 1 waits on it. [📜]

### 3.2 Pärt prototype — correctness flags (from the reviews; numbers in PLAN-v2 "Done")
- ~~Repose (sand sliding) is gated by an 8 s tail after the last event and **freezes piles still moving**~~ **(3 Nov) fixed in 3b-i**: gated on motion; every stop is a fixed point (drop 15°: 1.119 = the bound; stress drop: 1.149 = the bound, after 54 s of sliding — no cap on that time, flag).
- ~~Strike rim colour share misses the removed-volume share by 13.7 points~~ **(3 Nov) fixed in 3b-i**: depth-quantile map, 82.4 % vs 82.3 % removed.
- On devices without 32-bit float render targets: deposit volume creeps (+3.5 % at 6 s on stacked drops), rim conservation under bottom-out/wear is off, and (3 Nov) the wind's bed lift is off. Deposit program is 20 uniform vectors under WebGL2's 224 minimum (move `uGd` to a data texture if a device fails).
- (3 Nov) Wind, from the 3b-i review: a second "ghost" rim 36–48 texels downwind of a crater (the longest hop class landing in a ring; 0.047 vs the rim's 0.18); hop lengths clamped at 48 texels at Energy 2 (mean hop 30 instead of 41); the hop hashes repeat every 17 s; the asynchronous repose read-back warning above. Not run: iOS / any real GPU; the 16-bit deposit fallback with wind; family switch with blow events.
- Liquid strike leaves a flat standing offset in the wave field (~0.015 per strike): invisible, harmless in 32-bit, degrades 16-bit after ~100 strikes.
- 8-bit height maps make grain in relief-wear erosion (use 16-bit TIFF or read one mip coarser); `RELIEF_K` 0.10 is a mild lean; mask relief computed for idle texels (cost only).
- Display canvas cap 2048 → 4× pixels at DPR 2 on iPad; three 2048² 16-bit texture slots + HDRI ≈ 170 MB on iPad — keep 1024 on mobile.

### 3.3 Pärt prototype — look flags (advisor's judgement, as a stranger would see it)
- **The strike on sand still reads as a flat dark disc with one lit crescent**, not as thrown sand; its rim relief is a third of the drop's. Lever: shading exaggeration or a taller strike rim. Bekir's taste call.
- Drops now read as craters at defaults and clearly at low light (20°); thrown grains read as grains. Dust vs Sand difference is subtle (repose 24° vs 34°, finer grain) — may not justify two surfaces.
- ~~The nearest-layer rule shows the top layer only to half its thickness~~ **(3 Nov) fixed in 3b-i**: boundary at the full thickness; the lower layer's grains show through the last fifth of a layer only (cut 0.30 → 0 %, 0.36 → 50 %, 0.40 → 100 % on a 0.4 layer).
- (3 Nov) **Wind, as a stranger sees the frames:** a gust over a crater now reads as blown sand — the picture's dark grains scatter onto the light ground downwind, light grains land in the silhouette, the rim's deep-layer grains stream into a plume, grains from upwind fall into the crater. Three weak spots: (1) a **default gust (area 0.6) covers the whole canvas and speckles the whole picture** — 12.3 % of pixels change by more than 16 levels although the bed loses only 0.006 of depth, i.e. a one-grain film recolours a pixel completely; levers are a smaller default area, a weaker bed (`windBed`), or a thin-film display rule — **Bekir's taste call on the iPad before anything is tuned**; (2) a narrow gust's edge is a ruler line (3b-ii: noise on the band edge); (3) faint streaks along the wind in the plume (lateral scatter is ±1 texel only).
- Risk named at design time: a 512² field may never give "sand" feel; particles (pass 3c) are the fallback for flying patches.

### 3.4 Process and documentation
- The advisor's briefs twice specified the wrong thing (thrown-disc size 15–30 px; the rim-colour depth map); both fixed in 3a-look. Reviews caught what the writer declared and what it did not — the Sonnet→Opus→advisor chain is working; keep it.
- "Load" of a settings file has never reset keys absent from the file (HEAD behaviour since 1c, found only in the 3a review) — decide whether it should.
- Session scratch (scripts, screenshots, probes for every pass) is **not in the repo**; only the numbers survive, in PLAN-v2. Acceptable so far; say so if a reproducible test suite is wanted.
- (3 Nov) The advisor's 3b-i brief specified a wind transport that was wrong in kind (a continuous lift rate with a fixed carry — a conveyor), caught only on the rendered frames, after a 2 h 20 min writing pass; the model was replaced (stochastic hops) in a second pass. Third time a brief of the advisor's needed a rewrite after the fact; the frame check before review is what catches these — keep it, and consider a short "look probe" (one 1024 frame of the new feature) before the full test battery.
- (3 Nov) Two operational hazards met and documented in HANDOFF.md: a writer's long wait loop raised a permission prompt on Bekir's phone and a tap ended the agent for good (its detached tests finished on their own); the cloud container restarted mid-review (the review resumed from its transcript with nothing lost but its running processes). Neither affected the code.

---

## 4. What is next (in order; owner in brackets)

1. **[Bekir] iPad test of 3a-look and 3b-i** — the six-step scenario (Sand drop; three drops at one spot; strike via `#surface=sand&impact=strike`; low light + Energy 2 + Depth 1; Dust drop; Random 45 s seed 3) with no image, then with two strongly different images; answers in one word each; (3 Nov) plus `#surface=sand&impact=blow` and Random 45 s on Sand: does a gust read as wind over sand or as the picture dissolving into speckle; is the whole-canvas speckle too much; frame rate while a pile slides and during a gust. Frame rate from the HUD. This decides whether the sand route continues or particles come forward, and how the wind is tuned.
2. **[Advisor → Sonnet/Opus] Pass 3b-ii** (brief not yet written; design in PLAN-v2 A9; (3 Nov) 3b-i — wind, repose gate, rim quantile, boundary — is done): **clods** — a skewed-size cell map, cohesion rising with size, `clodFraction`, borders invisible until they break, three nested scales in one RGB id texture; `events.json` **set-events** with ramp (mid-piece character change); band-edge noise for the wind; a thin-film display rule or default-area change if Bekir finds the speckle too much; strike rim relief. Then **3c** particles for flying patches. Scratch (a furrow with two ridges) is recorded, unscheduled.
3. **Pass 4** sweep for all three media (absorb + pile at the edge); **pass 5** blow + flow for all three; **B5** dispersive waves (Opus, isolated); **B2** offline render (`render.js`, headless Chrome → PNG sequence → ffmpeg) + **B3** `events.json` from the Malter recording (onsets; pitch → position, velocity → energy). First 60 s at 1080p = the Blender decision point.
4. **[Bekir] Decisions still open on the prototype:** default layer thicknesses (advisor: [0.4, 1.5, 2.5, 3]); thin lip vs old bevel on the liquid edge; strike basin amplitude (0.30) and `reliefCrack` strength with his own height maps; whether Dust stays.
5. **[Bekir] Rights:** the UE brief inputs (venues/dates, edition, online, artist sentence + still) and the concept paragraph in his words; [Advisor] draft the letter in two options, verify the Cantus catalogue number, find UE's licensing contact route; request the ECM master quote in parallel.
6. **[Bekir] Ear test** answers; **[Advisor]** then the Xanadu `build` script (pages from frame JSON), the four unimplemented mappings (`−` = rest, value = loudness, edge intervals, ⟡ = sustain), WAV export, hosting/domain before QR printing.
7. **[PM] MJDL stream:** put the package under version control; rewire Partition View onto phobia-engine (v29); the Lab into the settings section; decide whether the phase model is resumed (if so, XPBD); start the correlation study only with a fixed theme and 60–100 images varied one axis at a time.

---

## 5. Where things are

| What | Where | State |
|---|---|---|
| Pärt clip prototype | `bektaron/MJDL` → `sound/xanadu-sound/part-clip/proto/index.html` (one file, ~4 200 lines, no libraries) | live at `bektaron.github.io/MJDL/sound/xanadu-sound/part-clip/proto/`; HEAD `88b9bea` (3 Nov, pass 3b-i) |
| Its plan, log, rulings | same folder: `PLAN-v2.md` (A-rows = design, "Done" = measured log per pass), `HANDOFF.md` (session-to-session: method, pass log, known flags, open questions), `IMPACTS.md` (impact model v1 + scratch, pieces mapped, pass order) | current to 3 Nov 02:10 |
| Xanadu Sound project file, research | `sound/xanadu-sound/docs/XANADU-SOUND-project.md` (§10 = Pärt clip, §11.6 = UE brief), `…-research.md` | current |
| Listening pages, ear test | `sound/xanadu-sound/fr-001/`, `fr-002/`, `fr-001-tintinnabuli/`, `index.html` | live on Pages; reading data hand-written into the pages (first thing to replace) |
| MJDL package | `MJDL-package-2026-10-30.zip` (with Bekir) — `tool/xan-partition-view.html` v28, `tool/phobia-engine.js` 0.2, `tool/phobia-lab.html` v8, `tool/phobia-phase-lab.html` (parked), `phase-model-plan.html`, `docs/MJDL-cloud-configuration.md` 0.14+, `MJDL-PM-brief.md` (change log to 31 Oct 09:00), `MJDL-phobia-table.md` 0.7, procedure/definitions/transition notes, README | **not in git** |
| Nodular composition plan | in the package docs (written 30 Oct, no code) | plan only |

### 5.0 What the PM must request from Bekir (not in the repo)

| Request | How to recognise the right copy |
|---|---|
| **`MJDL-package-2026-10-30.zip`** — the only MJDL package; it was re-packed under the **same name** many times on 30–31 Oct. Ask for the **last** copy: the one delivered 31 Oct 2026 ~09:00 CET with the caption "Kapanış paketi" (closing package). | Its `README.md` lists `xan-partition-view.html` **v28**, `phobia-engine.js` **0.2**, `phobia-lab.html` **v8** "(the accepted point)", `phobia-phase-lab.html` "(parked, not applied)", `MJDL-phobia-table.md` **0.7**; `docs/MJDL-PM-brief.md` ends "Last updated: 31 Oct 2026, 09:00 CET". An older copy shows lower numbers — ask again. |
| If the zip is lost: the files were also sent singly in the 29–30 Oct session — `xan-partition-view.html`, `MJDL-cloud-configuration.md`, `MJDL-PM-brief.md`, `MJDL-phobia-table.md` — and the tools are published as claude.ai artifacts named **"Phobia Lab"** and the Partition View (owner: Bekir). | Single files are older than the zip (v19–v22 era for the Partition View); only the zip holds v28 and the engine. |
| **Nothing to request for Xanadu Sound or the Pärt clip** — everything is in `bektaron/MJDL`. | `git log` HEAD `88b9bea` or later. |

### 5.1 File-by-file, latest version known to the advisor

Versions marked [☀️] were read from the repo today; [🌤️] are taken from the session transcripts (the package itself is not reachable from here — the PM verifies against the zip's `README.md` and `docs/MJDL-PM-brief.md`, whose change log is authoritative).

**Repo `bektaron/MJDL`, HEAD `88b9bea` (3 Nov 2026, 02:10 Istanbul)** [☀️]

| File | Latest | Notes |
|---|---|---|
| `sound/xanadu-sound/part-clip/proto/index.html` | pass 3b-i, commit `88b9bea` (3 Nov) | settings JSON `version 1` (+ `granular.live.windLift/windCarry/windBed`); one file, no libraries |
| `sound/xanadu-sound/part-clip/proto/PLAN-v2.md` | v2.1 + "Done" log through pass 3b-i | A9 holds the 3b design (clods, set-events still to do) |
| `sound/xanadu-sound/part-clip/proto/HANDOFF.md` | current to 3 Nov 02:10 | method, pass log, flags, open questions |
| `sound/xanadu-sound/part-clip/proto/IMPACTS.md` | v1 (1 Nov) + Für Alina = liquid, pass order 3a/3b; + scratch row and granular blow marked done (2–3 Nov) | |
| `sound/xanadu-sound/docs/XANADU-SOUND-project.md` | §10 extended to the sand ruling (1 Nov) | §11.6 = UE brief |
| `sound/xanadu-sound/docs/XANADU-SOUND-research.md` | 31 Oct | |
| `sound/xanadu-sound/fr-001/index.html`, `fr-002/index.html`, `fr-001-tintinnabuli/index.html`, `sound/xanadu-sound/index.html` | 30–31 Oct | live on Pages |
| `docs/PM-HANDOFF-2026-11-02.md` | this file, updated 3 Nov | |

**Package `MJDL-package-2026-10-30.zip`, closed 31 Oct 2026 09:00 CET** [🌤️]

| File | Latest | Notes |
|---|---|---|
| `tool/xan-partition-view.html` | **v28** | v29 (rewired onto the engine) started, not packaged |
| `tool/phobia-engine.js` | **0.2** | DOM-free, public API in the header; reusable |
| `tool/phobia-lab.html` | **v8** | engine inlined; the accepted point |
| `tool/phobia-phase-lab.html` | trial 1 | parked by ruling, not applied |
| `phase-model-plan.html` | plan page with sketches | approved before the trial |
| `tool/xan-relations-mockup.html` | 30 Oct | the alternatives that led to type clouds |
| `docs/MJDL-PM-brief.md` | last updated 31 Oct 09:00 | change log from 30 Oct 10:30 — read first |
| `docs/MJDL-cloud-configuration.md` | 0.14 at the end of 29 Oct; bumped further on 30 Oct for v23–v28 (exact number: see the brief) | |
| `docs/MJDL-phobia-table.md` | **0.7** | rank table, contradictions, §13–14 phase model + XPBD |
| `docs/MJDL-canon-transition.md` | 0.3 | |
| procedure note | 1.12 (as of 30 Oct 10:30) | exact file name: see README |
| definitions note | 0.12 (as of 30 Oct 10:30) | exact file name: see README |
| `docs/MJDL-sonification-plan.md` | 0.1 | "nodular composition" plan, no code |
| `docs/XANADU-SOUND-project.md` | 0.1 (early copy) | **superseded** by the repo's version |
| `README.md` | lists every file with its version | |

**To resume the Pärt work in a new session:** connect `bektaron/MJDL`, read `sound/xanadu-sound/part-clip/proto/HANDOFF.md`, continue. To resume MJDL: unzip the package, read `docs/MJDL-PM-brief.md` first.
