# Xanadu Sound — project brief (nodular composition)

> **Provenance notice.** This document was written without access to the MJDL project itself, from a reading of the Algı Bulutu artifact and from conversation with Üstadım. The Project Manager must evaluate it against the project's references and canons before acting on any of it. It may contradict the project's rules.

Version 0.2 · 31 Oct 2026 (v0.1: 30 Oct) · a brief for opening **Xanadu Sound** as its own project, split off from MJDL. Idea and rulings: Bekir Kıraç. Text: Claude (advisor). Turkish is the working language of the conversation; all system files are English.

**v0.2 change log.** §10 Pärt clip sub-project added (31 Oct, morning). §11 added: what the system research changes, and how it is integrated (31 Oct, afternoon). Appendix A embeds the full research report (`XANADU-SOUND-research.md` v0.1) so this file is self-contained. §§1–10 are left as written in v0.1 so that the record of what was believed *before* the research stays legible; where §11 overrides a line in §§4–9, §11 wins.

---

## 1. One sentence

A Perception Cloud is a score: every frame's reading (what the prompt named, what Bekir heard, what the eye could not decide) is rendered as a short piece of sound, and image and sound are shown — and sold — together.

## 2. Why a separate project

- MJDL's object is the **lexicon** (the difference between language proximity and reading proximity). Sound is not needed for that; it is a second *work* built on the same data.
- The sound work has its own questions (mapping, form, timbre, rights, exhibition) that would clutter MJDL's files.
- The two stay coupled by **one contract only**: Xanadu Sound reads the frame reading blocks MJDL produces (§5). It never writes into the cloud.

## 3. What exists today (all working, nothing heard by Claude)

| Item | Where | State |
|---|---|---|
| Listen page FR-001 | `MJDL/sound/xanadu-sound/fr-001/` → `https://bektaron.github.io/MJDL/sound/xanadu-sound/fr-001/` | live, QR printed-ready |
| Listen page FR-002 | `…/fr-002/` | live, QR printed-ready |
| QR codes | `qr-fr-001.png/.svg`, `qr-fr-002.png/.svg` (300 dpi card + vector) | decoded and verified |
| Hosting | GitHub Pages, source *GitHub Actions*, workflow `.github/workflows/pages.yml`, deploys on every push to `main` | QR URLs are stable |
| Engine | Web Audio API, one HTML file per frame, no library, no samples; only external dependency Google Fonts | ≈ 170 lines JS |
| Forms | **soft** (default) · **layers** · **line** — switch on the page | three mappings, see §4 |
| Plan | `MJDL-sonification-plan.md` v0.1 (mapping table, four forms, instrument mode, export) | to be superseded by this brief + a v0.2 plan |
| Sound prototypes (earlier) | artifacts *FR-001 Sound*, *FR-002 Sound*; files `fr001-sound.html`, `fr002-sound.html` (tap-to-hear capsules, node-length slider) | superseded by listen pages; keep as instrument sketch |

Reading data is hand-written inside each page (`F`, `S`, `E`, `K` arrays and `READING`), copied from the mockups. This is the first thing to replace (§5).

## 4. The three forms and what each is for

Shared ground (all forms): root **D3** (146.83 Hz); pitch of a node = hash of its name → scale degree (arbitrary but **stable**: the same node is the same note everywhere); register by gene (SUB low · MED/ENV/COM · LIG/COL · TEX/MOT high; K highest); **ambiguity score → pitch wander** (0 steady, 100 up to ±6 %, faster with score); `&` = two notes together, `|` = two notes together *unresolved*; three-pole `|` adds a third note.

| | **line** (v0.1) | **layers** (v0.2) | **soft** (v0.2b) |
|---|---|---|---|
| Purpose | **reading** — each node audible one by one | **structure** — the frame's depth layers heard as sound layers | **listening** — exhibition, phone, stranger's ear |
| Scale | just major, 7 notes | just major, 7 notes | pentatonic (D E F♯ A B), 5 notes: no sharp interval possible |
| Order | F nodes → tags → `&` → `|`, one after another | simultaneous: BG · pulse · FG · tension | melody walks to the nearest unused pitch (smallest steps) |
| Timbre by partition | F pluck · S breath · E bow · K thin-long | same | nearly uniform sine; only K brighter |
| Background | — | **ground**: the two most certain SUB nodes as pedal, one octave down | D + A pedal, very soft |
| Rhythm | — | TEX nodes 0.5 s, MOT nodes 0.75 s pulse trains; ambiguity makes them stumble | one soft D "heartbeat" every 1.6 s, stumbling with the ground's ambiguity |
| Foreground | — | tags and `&` dyads from 8 s | the melody itself |
| `|` interval | semitone | semitone, over the pedal, last 10 s | **whole tone** (9/8), held; third pole a fourth up |
| Length | ≈ 16–18 s | ≈ 37 s | ≈ 36–39 s |
| Cost | mapping fully legible | 4–5 voices at once: a single node is harder to pick out | four mapping rows weakened (timbre, wander, `|` sharpness, order) |

**Ruling needed (Bekir, by ear):** which form is the exhibition form, or whether all three stay as "three forms, three purposes". Claude's view: keep all three; default *soft* on the public page, *line* in the tool. ☁ PM review — this is a taste decision; the files only need to record it.

## 5. Data contract with MJDL (the only coupling)

Xanadu Sound consumes, per frame, exactly what MJDL's configuration already defines (`MJDL-cloud-configuration.md` §2):

```
frames/<id>.json
  generation.drawn_nodes[]        → F nodes of the passage (id, label, gene, ambiguity, value)
  reading.tags[]                  → S/E/K nodes by name
  reading.pair_readings[]         → {poles, op:"&"|"|", carrier[], carrier_op, depth}
cloud: F.json S.json E.json K.json → ambiguity score, value, contribution, flags
```

Rules:
1. Sound reads; it never writes. Rulings on the cloud happen in MJDL.
2. Contribution **−** nodes are rests (plan §2) — not yet implemented in any form. ☁
3. Value (carrying strength) → loudness — not yet implemented; all values are 0.5 today. ☁
4. Edge intervals (TEX unison · MOT fifth · INT tritone) — not yet implemented; the pages have no relations yet. ☁
5. Ambiguity flag ⟡ → sustain — not yet implemented. ☁
6. A page must be regenerable from the JSON by a script (`build.py` or `build.js`), so that a new frame = new folder, no hand-editing. **First task of the project.**

## 6. Decisions open

1. **Form** (§4) — by ear.
2. **Note assignment**: hash (arbitrary, stable) vs a hand-kept *note lexicon* (node → note, chosen by Bekir). Hash costs nothing and is consistent; a lexicon makes the note *mean* something but must be maintained like the cloud itself. Claude's view: start with hash; open a lexicon only for nodes that recur across many frames. ☁
3. **Length**: a passage beside a printed image should fit one standing listener: 30–40 s. Line at 16 s felt short to Claude but Claude has not heard it.
4. **Rights**: the mapping table is the work; write it down and date it before anything is shown (plan §6.4). This brief's §4 is that record, version 0.1.
5. **Hosting**: GitHub Pages under `bektaron.github.io/MJDL/…` is live; a project domain (e.g. `xanadu.<domain>`) can point at the same files later without changing the HTML. QR codes would have to be reprinted — decide before printing in quantity.
6. **Export**: offline render to WAV (OfflineAudioContext) for the exhibition's room sound and for sale; not built.
7. **Fonts**: the only external dependency; inline the two fonts or accept system fonts for full offline robustness.

## 7. Roadmap (small steps)

| # | Step | Needs | Size |
|---|---|---|---|
| 1 | Ruling on form, by ear, on the phone pages | Bekir | an evening |
| 2 | `build` script: JSON → listen page; regenerate FR-001/002 from JSON instead of hand data | §5 contract fixed in MJDL | one session |
| 3 | Implement the four missing mappings (−, value, edge intervals, ⟡) in the chosen form(s) | step 2 | half a session |
| 4 | WAV export of a passage; batch suite = passages in sequence | step 3 | half a session |
| 5 | Instrument mode inside Partition View (tap = tone, focus = solo, `|` = dyad) | Partition View code | one session |
| 6 | Exhibition pack: print card (QR + title + 1 line), room sound, rights note | steps 1–4 | one session |

## 8. Files of this project (final versions, 30 Oct 2026)

- `XANADU-SOUND-project.md` — this brief
- `MJDL-sonification-plan.md` v0.1 — the original plan (mapping table still authoritative for the unimplemented rows)
- `listen-fr-001.html`, `listen-fr-002.html` — the live pages (identical to the repo copies)
- `fr001-sound.html`, `fr002-sound.html` — earlier tap-to-hear prototypes
- `qr-fr-001.png/.svg`, `qr-fr-002.png/.svg`
- `frame-e14a9911.jpg` (FR-001), `frame-4c1a91ed.jpg` (FR-002)
- Repository: `github.com/bektaron/MJDL` → `sound/xanadu-sound/`

## 9. Risks, plainly

- **Nothing has been heard by the advisor.** Every timbre and gain is a guess verified only as "the audio graph schedules". The first listening may overturn §4.
- **Hash notes are meaningless.** A listener who learns that "wet sand" is F♯ learns nothing about wet sand. That is honest (the mapping claims only stability), but it must be said as such in any wall text.
- **The soft form flatters.** It is the one strangers will like and the one that carries the least data. If it becomes the only public form, the work becomes a soundtrack — exactly what plan §1 said it is not.

---

## 10. Sub-project: Pärt clip (added 31 Oct 2026)

**Ruling (Bekir):** a separate sub-project under Xanadu Sound — a video clip designed for Arvo Pärt's *Für Alina* (1976, piano) and *Spiegel im Spiegel* (1978, violin & piano).

**Direction.** The main project turns reading data into sound. This sub-project runs the other way: existing music → image. That inversion is the reason it is kept apart: it must not be mistaken for the sonification, and §9's "soundtrack" warning does not apply here, because here the music *is* given.

**Open before anything else — rights.** Both works are in copyright (Pärt b. 1935). ☁ Publisher believed to be Universal Edition; recordings (e.g. ECM) carry separate master rights. A public showing or sale needs a synchronisation licence for the composition and, if a commercial recording is used, for the master. A newly commissioned performance removes the master question, not the composition. Until cleared: private study / portfolio only. Not verified; first task of the sub-project is to verify and write the answer here.

**Not yet decided:** what the clip shows (frames from the cloud? the Partition View? new material?), still or moving, one clip per piece or one across both, length (Für Alina ≈ 2–3 min, Spiegel im Spiegel ≈ 8–10 min), whether the Xanadu Sound mapping has any role in it or none. ☁ Claude's view: decide the rights question before designing a frame; a design made for a piece that cannot be shown is the kind of work that gets erased in one stroke.

**Files:** none yet. Proposed folder `MJDL/sound/xanadu-sound/part-clip/`.

**First design (Bekir, 31 Oct 2026, recorded so it is not lost; a concept note, not production — §11.5 P2 still waits for UE).**

A soft, liquid-metal surface, seen from above. It reads like polished or brushed steel: it mirrors, but not fully — perhaps 20–30 % reflectance, not the brightness of a true mirror. On this surface lies a woman's profile. The profile ripples with the surface, half-seen, half-lost. As the music plays, the notes arrive one by one from above and fall onto the surface like drops. Where a drop lands, it alters that part of the woman — the part at the point of impact — a little. So the apparition keeps rippling on the surface and keeps changing with the drops, with the notes. For the whole length of the music it remains the image of a woman who cannot be reached.

Open from this note (not yet ruled): which piece this is for — one of the two or both; whether the drop is the note's attack (hand-placed marker) or derived from amplitude (A§5B argues hand-placed for these quiet pieces); whether the profile is a still image (Photoshop/Midjourney) displaced by a ripple map, or 3D (liquid simulation) — the first is the Photoshop-native path, the second is the 3D path; what reflectance and ripple damping keep "half-seen" from becoming "unreadable".

Realisation notes (advisor, 31 Oct 2026, after Bekir's "ok" to a prototype):
- *Drops per piece.* *Für Alina* is sparse (~40 notes/min): every note can be a drop. *Spiegel im Spiegel* has a continuous piano triplet (~3 notes/s, ~1,600 in 9 min): drops for every note would be rain. There the **violin** notes are the drops; the piano triplets become the surface's own faint ripple. ☁ Ruling needed.
- *"Changes a part of her".* A ripple alone distorts; it does not change. Mechanism: a stack of N variants of the same profile (same seed, small differences); each drop reveals a lower variant inside its radius. When the surface settles, that region is now another variant. Unreachability comes from this: every note makes her slightly someone else.
- *Pipeline:* events.json (onset detection or hand markers; pitch → drop position, velocity → size) → 2D wave heightfield (damping = the "half-seen" dial) → profile texture refracted by the slope, 20–30 % Fresnel reflection, metallic shading → variant-reveal mask per drop → offline render 4K/25 fps → audio laid in Resolve.
- *Tools:* WebGL prototype first (one evening; motion and damping felt on the phone), Blender (Dynamic Paint Waves + Cycles) for the final — real reflections, script places drops from events.json. After Effects is weak here (hundreds of drops, no metallic reflection); A§5B's AE recommendation predates this design.
- *Prototype:* `part-clip/proto/` — WebGL, first 60 s, synthetic Für Alina-like event list, placeholder profile with an image-upload slot for Bekir's own frames. Private study; independent of the UE answer.

---

## 11. What the research changes, and how it is integrated (added 31 Oct 2026)

Source: Appendix A (five research agents, 31 Oct). Everything in this section is **[🌤️]** unless marked: it is a reading of cited evidence, not a listening result. Rulings stay with Bekir.

### 11.1 Where the research helps, in plain terms

1. **It replaces taste with evidence in the four places where the brief was guessing.** v0.1 mapped value → loudness, ambiguity → pitch wander, structure → 4–5 simultaneous voices, and meaning → hashed pitch. The perception literature (A§1) says each of these fails for untrained listeners: loudness is judged badly and bends pitch judgement; small wander is unheard or heard as a mistake; more than ~3 lines fuse into background; pitch direction carries no agreed meaning. These are not opinions about sound; they are the reasons a stranger would not *read* the piece.
2. **It gives a composition rule a non-musician can own.** Tintinnabuli in fixed position (A§2) is a 7-row table: scale degree → one triad note. Every note is then determined. "Unresolved" (`|`) comes from *inside* the rule (the T-voice alternates and never settles), so the system no longer has to step outside its own scale to say "undecided". This is the single most useful finding: the brief's §4 was three *mappings*; after §11 it is one rule set at three *densities*.
3. **It confirms the toolchain and names what to avoid.** The raw Web Audio choice was right; the research adds the render path (pinned headless Chrome → WAV → ffmpeg) and rules out Tone.js (slow maintenance) and Strudel (AGPL, archived). The iOS silent-switch problem (A§3) is a real exhibition failure that would have been discovered at the opening.
4. **It turns the Pärt rights question from a worry into a procedure.** Publisher confirmed (Universal Edition, Vienna), process confirmed (a written briefing, no form, no public fees), master-rights route identified (ECM; alternative: a new recording). The sub-project now has a first deliverable that is a letter, not a design.
5. **It gives the sale a model.** Daata/EAI practice (A§5A): numbered edition, certificate naming private-display rights, file on the artist's own domain, re-download. Museum QR data says uptake can be 5 %; that number decides the headphone station.

### 11.2 What does *not* change

- §2 (why separate) and §5 rules 1 and 6 (read-only; regenerable from JSON) stand unchanged and are strengthened.
- The hash → note rule stays — but demoted to an identity marker ("name tone"). §9's first risk becomes the first sentence of the wall text rather than a risk.
- §6 item 2 (hash vs note lexicon) is answered by the demotion: no lexicon; pitch does not mean, so a lexicon would decorate.

### 11.3 Integration — section by section

| Brief | v0.1 said | After research | Action |
|---|---|---|---|
| §4 shared ground | pitch = hash → degree, carries the node | pitch = name tone, identity only; **harmony = tintinnabuli T-voice** from a fixed table | rewrite §4 in v0.3 after the ear test (11.5 step 1) |
| §4 ambiguity | continuous wander ±6 % | 0, or glide ≥ 1 semitone, or beating pair (beat rate ∝ score) | implement as a switch in `engine.js`; test both |
| §4 `\|` | semitone / whole-tone dyad | T-position alternates, never settles; semitone as optional accent | implement; keep old dyad behind a flag for comparison |
| §4 `&` | two notes together | superior + inferior T-positions together (fusing) | implement |
| §4 timbre by partition | pluck / breath / bow / thin | three *clearly different* timbres **+ fixed stereo** (F centre, S/E left, K right) | implement; raw oscillators may not separate — this is a listening test, not a code task |
| §4 three forms | three mappings | one rule set, three densities: line = 1 voice; layers ≤ 3 voices + bed; soft = 1 voice + pedal | `rules.json` gets a `density` field; *layers* loses two voices |
| §5 rule 3 | value → loudness | **value → duration / repeat count** | reverse |
| §5 rule 2 | − nodes = rests | unchanged; alternative (last-note accent) rejected in favour of the brief's own rule | keep |
| §5 rule 5 | ⟡ → sustain | unchanged; sustain applies to the T-note | keep |
| §6 item 2 | hash vs lexicon | no lexicon | close |
| §6 item 3 | length 30–40 s | unchanged; tintinnabuli works at this length, Eno/Reich do not | keep |
| §6 item 4 | mapping table = the work | **`rules.json` is that table**, versioned and dated in the repo | create file; v0.2 = Appendix A §6 |
| §6 item 5 | hosting / domain | own domain before any QR is printed in quantity; page < 1 MB; short URL under the code | decide domain in step 6 of 11.5 |
| §6 item 6 | WAV export, not built | pinned headless Chrome + `OfflineAudioContext` → 24/48 WAV → ffmpeg `loudnorm` → FLAC (sale) + AAC (phone fallback) | step 4 |
| §7 roadmap | 6 steps | re-sequenced in 11.5 | — |
| §9 risk 2 | hash notes meaningless | becomes wall text + 20 s legend track | write legend |
| §9 risk 3 | soft flatters | the density cap (≤ 3) makes *every* form a curatorial filter; say so on the wall | write wall text |
| §10 Pärt clip | rights unverified | publisher and route verified; fees not public; **no design until UE replies** | write the brief to UE (11.6) |

### 11.4 The new risk the research introduces

**Imitation.** A tintinnabuli engine beside a Pärt clip in the same project will be read by any informed viewer as Pärt-derived. Two honest answers exist: (a) state it — the rule is borrowed as a *grammar*, the data is the composer, and say so on the wall; (b) keep tintinnabuli as the engine but drop the Pärt clip from the public pairing. The research cannot choose; this is Bekir's ruling and it should be taken before step 2 below, because it decides whether the clip sub-project is a companion or a liability. Claude's view: (a), because hiding the source would be the one thing that breaks trust if discovered — and it would be discovered.

### 11.5 Roadmap, re-sequenced (replaces §7)

| # | Step | Needs | Size | Comes from |
|---|---|---|---|---|
| 1 | **Ear test.** A second FR-001 page with the tintinnabuli rule (A§6 table), toggles for old/new `\|`, old/new ambiguity. Bekir listens on the phone; ruling on §11.3 rows 1–6 and §11.4. | nothing | one session + an evening | A§1, A§2 |
| 2 | `rules.json` v0.2 written from the ruling; `engine.js` reads it. No other mapping lives anywhere. | step 1 | half a session | A§6 |
| 3 | `build.js`: `frames/<id>.json` + `rules.json` → `listen/<id>/index.html` + `midi/<id>.mid`. Regenerate FR-001/002 from JSON; delete hand data. | §5 contract fixed in MJDL | one session | brief §5.6, A§3 |
| 4 | `render.js` (pinned Chrome, `OfflineAudioContext`) → WAV; `master.sh` (ffmpeg loudnorm −18 LUFS / −1 dBTP) → FLAC + AAC + `hashes.txt`. Listen page: AudioContext inside tap, `audioSession.type='playback'`, `<audio>` fallback. | step 3 | one session | A§3 |
| 5 | Legend track (20 s, one rule at a time) + wall text (name-tone rule, 3-voice cap, source of the grammar). | step 2 | half a session | A§1 (Schuett) |
| 6 | Domain + edition pack: own domain pointing at the pages; certificate template (edition no., private display, WAV hash); QR cards reprinted once, with short URL; one headphone station. | step 4 | one session | A§5A |
| 7 | Instrument mode inside Partition View (unchanged from v0.1 step 5). | Partition View code | one session | brief §7 |
| P1 | **Pärt brief to UE Vienna** + ECM master quote + price of a new recording. Nothing else in `part-clip/` until the reply. | nothing | an hour to write; weeks to wait | A§4 |
| P2 | Clip design (After Effects, PSD layers, hand markers on phrase structure, AI inserts chained by start/end frames) — **only after P1 answer and §11.4 ruling**. | P1 | several sessions | A§5B |

### 11.6 The UE brief — skeleton (for P1)

To: Universal Edition AG, Promotion, Karlsplatz 6, 1010 Wien (+43 1 33723-100). Works: *Für Alina* (UE 19823), *Spiegel im Spiegel* (UE 30336 or the violin/piano edition). What: a single-channel video work by a visual artist, full pieces, music unaltered, image designed to the score. Uses: (1) gallery exhibition, Turkey and EU, [dates/venues]; (2) limited edition of [5 + 2 AP], private display by collectors; (3) online — [yes/no, platforms]. Recording: [ECM 1591 — separate master request in progress] *or* [new recording to be commissioned]. Request: three separate quotes for (1), (2), (3); any conditions on the edit. Attach: one still, one paragraph on the artist, the Karya/MJDL context in two lines.

### 11.7 Files added by this version

- `XANADU-SOUND-research.md` v0.1 (also embedded as Appendix A)
- to be created in step 2: `sound/xanadu-sound/rules.json`
- to be created in P1: `sound/xanadu-sound/part-clip/brief-to-UE.md`

---

# Appendix A — System research report (embedded verbatim, 31 Oct 2026)

Version 0.1 · 31 Oct 2026 · five parallel research agents (Opus) + synthesis (Fable). Brief: `XANADU-SOUND-project.md` v0.1 §1–10. Requested by Bekir Kıraç. Working language of the report: English (system file).

Marks: **[V]** verified in a cited source · **[I]** inference by an agent or the advisor · **[U]** not verified. The agents did not hear any of the pages. Nothing here is a listening judgement.

---

### 0. Decisions this report recommends (one screen)

| # | Decision | Rests on | Changes in the brief |
|---|---|---|---|
| D1 | **Hash → note stays, but only as a *name tone* (identity). No meaning rides on pitch.** | §1: pitch/loudness interference, polarity unpredictability, 3-voice limit | §4 shared ground: keep; §9 "hash notes are meaningless" becomes the *stated* rule, not a risk |
| D2 | **Composition rule: tintinnabuli, fixed position (close, inferior) on a D triad; D+A pedal stays.** Every node's name tone is an M-note; the T-note comes from a 7-row table. | §2 | replaces "scale degree + wander" as the harmonic engine of all forms |
| D3 | **`\|` (unresolved) = alternating T-position (the T-voice flips above/below and never settles). `&` = both positions sounding.** Semitone dyad kept as an *optional* accent, not the primary signal. | §2 + §1 (dissonant parts stand out) | §4 row "`\|` interval" |
| D4 | **Ambiguity ≠ continuous pitch wander.** Either 0 or a glide of ≥ 1 semitone, or a beating pair whose beat rate = ambiguity. Small wander is heard as a mistake or not at all. | §1 | §4 shared ground |
| D5 | **Value → duration / repeat count, not loudness.** | §1 (loudness judged poorly; interferes with pitch) | §5 rule 3 |
| D6 | **Partition (F · S/E · K) → timbre *and* fixed stereo position.** Gene → register with ≥ 1 octave between bands. | §1 (Brewster) | §4 "timbre by partition" row, all forms |
| D7 | **≤ 3 audible lines at any moment.** Everything else goes to a stated background bed. The cap is a curatorial filter and must be written on the wall. | §1 | §4 *layers* form (4–5 voices) must be cut or restructured |
| D8 | **Toolchain: raw Web Audio + one shared `engine.js` + Node build script + pinned headless Chrome for WAV + ffmpeg loudnorm. Same JSON → `.mid` for DAW versions.** No Tone.js, no Strudel. | §3 | §5 rule 6, §6 item 6, §7 steps 2–4 |
| D9 | **Phone page: single AudioContext started inside the tap; `audioSession.type='playback'`; fallback `<audio>` with the pre-rendered file.** | §3 | listen pages |
| D10 | **Sale unit = image + sound as one numbered edition** (print + 24-bit WAV on own domain + certificate stating private-display rights + QR card). Own domain before printing QR in quantity. | §5A | §6 items 4, 5 |
| D11 | **Pärt clip: no design work until UE answers.** One written brief to UE Vienna asking three prices (exhibition / editions / online); ECM master quote in parallel; price a new recording as the alternative. | §4 | §10 |
| D12 | **Clip tool (when cleared): After Effects backbone, PSD layers, hand-placed markers on the score's phrase structure; AI video (Kling/Midjourney) only as short inserts chained by start/end frames.** | §5B | §10 |

Open after this report: a 5–10 person listening test of D3/D4 ("which one sounded unresolved?"), and Bekir's ear on D2.

---

### 1. Sonification — what untrained ears can follow

**Field state.** Pitch is the most-used channel in the literature and the least evaluated: Dubus & Bresin's review of 179 papers found proper evaluation "only in a marginal proportion"; a 2024 EuroVis survey repeats this (about a third of studies had no evaluation). [V] — [Dubus & Bresin 2013](https://ideas.repec.org/a/plo/pone00/0082491.html), [Enge et al. 2024](https://arxiv.org/pdf/2402.16558)

**Evidence that bears on the brief:**
- *Polarity is not predictable.* Listeners split on whether "more" is higher or lower; tempo:size was near-unanimous (faster = more). [V] — [Walker et al.](https://wirelessrerc.gatech.edu/sites/default/files/publications/walker_et_al_-_a_comparison_of_sonification_mappings.pdf)
- *Pitch and loudness interfere.* A loudness change distorts pitch judgement and vice versa. [V] — [Neuhoff, Kramer & Wayand 2000](https://repository.gatech.edu/entities/publication/b42c37f0-ff76-47b9-833e-24b977198d26). This is the argument against §5 rule 3 (value → loudness).
- *Handbook ch. 15 pitfalls:* too many simultaneous continuous variables on pitch; arbitrary mappings; the unavoidable compromise intuitive/pleasant/precise. Useful devices it shows: snapping to pentatonic, a reference tone whose beating slows to unison, dissonant parts standing out against a harmonic bed. [V] — [Grond & Berger](https://sonification.de/handbook/download/TheSonificationHandbook-chapter15.pdf)
- *Earcon guidelines (Brewster):* clearly different timbres (brass vs organ, not two brasses); register alone is poor, use 2–3 octaves; rhythm/note-count differences "very effective"; loudness judged poorly; stereo position "very useful" for simultaneous sounds. [V] — [Brewster](https://www.dcs.gla.ac.uk/~stephen/earcon_guidelines.shtml)
- *Voice limit:* about 3 similar voices can be followed; the rest fuse into background; alternating tones < 3–4 semitones apart fuse into one line. [V] Bregman — [auditory.org](https://auditory.org/postings/2004/492.html); [Brochard 2000](https://www.mcgill.ca/mpcl/files/mpcl/brochard_2000_jephpp.pdf). Huron's "worsens after 3" is secondhand [U].
- *Pitch wander:* non-musicians' discrimination thresholds are > 6× musicians' [V] — [Micheyl 2006](https://experts.umn.edu/en/publications/influence-of-musical-and-psychoacoustical-training-on-pitch-discr/); laypeople judge out-of-tune singing much like experts [V] — [MPI Aesthetics](https://www.aesthetics.mpg.de/en/newsroom/news/news-article/article/hey-thats-out-of-tune.html). The "dead zone" (small wander unheard or heard as error) is [I].
- *Practice closes the gap:* an arbitrary mapping matched an expert-designed one after < 1 h of practice [V] — [Schuett 2019](https://repository.gatech.edu/entities/publication/2478d429-a60a-43b3-b6ea-5e0eb473bb47). Hence a short legend track.

**Sonified images (precedent):** NASA Chandra sweeps the image left→right, pitch from height/colour snapped to a scale, loudness from brightness, stereo from horizontal position, one instrument per wavelength layer. Outreach, not sold. [V] — [Chandra](https://chandra.cfa.harvard.edu/photo/2021/sonify3/)

**Artists and sales:** Kubisch *Cloud* bought by SFMOMA 2017 [V]; her *Trafowaves* print (a visual by-product of the sound) edition of 30 at €207, sold out [V] — [SFMOMA](https://www.sfmoma.org/artwork/2017.387.A-N), [Kunsthalle Praha](https://shop.kunsthallepraha.org/en/limited-editions/trafowaves/). Ikeda: institutional collections, editions mainly recordings; prices [U]. Winderen: commissions, "Collection the artist" [I]. Sales evidence for pure sound works is thin.

**Recommended (agent):** keep hash → degree as identity only; meaning on timbre + stereo (partition), register (gene), duration/repeats (value), accent position (sign), dissonant dyad (`|`), fusing interval (`&`); ambiguity as beating or ≥ semitone glide; ≤ 3 lines; legend track; saleable print + recording. **Risk:** Web Audio oscillators are hard to make clearly distinct; the 3-voice cap hides nodes; untested.

---

### 2. Rule systems — which guarantees listenability by rule

| System | Rule table for a non-musician? | "Unresolved" from inside the rules? | Fits 16–40 s? | Implementations |
|---|---|---|---|---|
| **Tintinnabuli** (fixed position) | Yes — 7 rows (degree → triad note) | Yes — alternating position; inferior close yields major seconds by itself | Yes | [REAPER Lua gist](https://gist.github.com/rennfly/24727073cbfc6cf32a9ba4c2cd81e86c); formalisation [Algo Pärt, arXiv 2603.26989](https://arxiv.org/html/2603.26989v1); [Kiral](https://www.researchcatalogue.net/view/3795800/3796035); no Strudel/SC/Tidal code found |
| Pentatonic / drone | Yes | **No** — no semitone available; the current `\|` dyad steps outside the scale and breaks the guarantee | Yes | [Parviainen trams](https://teropa.info/loop/) |
| Just intonation | tuning layer only | — | — | **Trap:** on D, E (9/8) + B (5/3) = 40/27, a "grave fifth" ~20 c flat; present in both current scales [V] — [5-limit intervals](https://en.wikipedia.org/wiki/List_of_intervals_in_5-limit_just_intonation). T-voice on the D triad is always clean; only the melody can hit it. |
| Eno generative | Yes (note, loop length, delay) | Loops that never realign | **No** — needs minutes | [teropa/musicforairports.js](https://github.com/teropa/musicforairports.js) |
| Reich phasing | Yes | Yes — two copies drifting | **No** — 1.002 rate ≈ 80 ms drift in 40 s, reads as echo | [teropa/itsgonnarain.js](https://github.com/teropa/itsgonnarain.js) |
| Riley *In C* | rules yes, cells no | — | — | cells are composed melodies (rights [U]) |

**Tintinnabuli facts:** M-voice stepwise diatonic; T-voice only the three triad notes, superior or inferior, close (nearest) or open (next out); four M-modes (up from / down from / down to / up to a centre). *Für Alina* uses one position throughout (close, inferior, B minor) and one hand-broken note [V]. *Summa* uses a history-dependent process, so fixed-position is a simplification [V].

**Mapping proposed by the agent [I, untested]:** name-tone = M-note; `|` = alternating position; `&` = superior + inferior together; ambiguity = distance of M from the centre; sign = M-mode direction; the four partitions take the four M-modes one-to-one.

**Recommended:** tintinnabuli, fixed position, D triad, JI, D+A pedal; one or two M-voices at a time. **Risk:** will sound like Pärt imitation — more so beside the Pärt clip (§4); several M-voices can clash; forbid E and B together or tune by triad; nothing heard.

---

### 3. Toolchain

- **Raw Web Audio** — `OfflineAudioContext` renders faster than real time; WAV writing ≈ 20 lines [V] — [MDN](https://developer.mozilla.org/docs/Web/API/OfflineAudioContext). Output differs slightly across devices (float arithmetic) [V]; so masters come from one pinned renderer. `node-web-audio-api` (IRCAM) exists but OfflineAudioContext support [U] and `getChannelData` "not reliable" [V] — [GitHub](https://github.com/ircam-ismm/node-web-audio-api/). Headless Chrome + Puppeteer is the safer renderer (same engine as phones) [I].
- **Tone.js** — 15.1.22, last release Apr 2025, slow maintenance [V] — [depscope](https://depscope.dev/pkg/npm/tone). `Tone.Offline` exists. Not needed at 170 lines; version drift causes AI-written bugs [I].
- **Strudel** — GitHub archived Jun 2025, moved to Codeberg, **AGPL-3.0** (publishing your source if you build on it) [V] — [GitHub](https://github.com/tidalcycles/strudel), [FAQ](https://live.strudel.cc/learn/faq/); WAV export PR stale [V]. Wrong fit.
- **SuperCollider NRT** — strongest offline reproducibility [V] — [SC guide](https://docs.supercollider.online/Guides/Non-Realtime-Synthesis.html); but two engines (no phone), desktop install, Claude less reliable in sclang [U].
- **Python** — good for the build script and MIDI (music21) [V]; not a phone engine.
- **MIDI → DAW** — only route to sampled piano/strings or human performance; Reaper scriptable, even an MCP server exists [V] — [ReaMCP](https://glama.ai/mcp/servers/tbfl06q0ma); batch render [U]; sample-library licences usually allow selling renders [U].
- **iOS** — AudioContext must resume inside a user gesture (Chrome too) [V] — [Montag](https://www.mattmontag.com/web/unlock-web-audio-in-safari-for-ios-and-macos); unlock may lapse after ~5 s on iOS 18.5 and ~4 contexts max [U, user reports]; **silent switch mutes Web Audio** — `navigator.audioSession.type='playback'` helps but is experimental [V] — [WebKit 251532](https://bugs.webkit.org/show_bug.cgi?id=251532), [MDN](https://developer.mozilla.org/en-US/docs/Web/API/AudioSession/type); fallback: `<audio>` element, or [unmute-ios-audio](https://github.com/feross/unmute-ios-audio).
- **Mastering** — ffmpeg `loudnorm` two-pass, `linear=true` [V] — [guide](https://dev.to/javidjamae/ffmpeg-loudnorm-filter-ebu-r128-loudness-normalization-guide-15d4); no installation LUFS standard found [U]; practical: −18 LUFS integrated, −1 dBTP, same for every frame, room level on the amplifier [I].
- **Sale formats** — Bandcamp: WAV/FLAC/AIFF/ALAC 16/24-bit, not 32 [V] — [Bandcamp help](https://get.bandcamp.help/en/articles/15263308-can-i-upload-higher-resolution-audio). Crypto edition platforms unstable (Sound.xyz subscription, Royal/OneOf closed) [V, source dates inconsistent] — [Chartlex](https://www.chartlex.com/blog/business/music-nft-web3-post-mortem-2026). Master 24-bit/48 kHz WAV; FLAC for sale; certificate with the WAV hash [I].

**Recommended:** one `engine.js` (raw Web Audio) → build script generates per-frame page → same engine in pinned headless Chrome → WAV → ffmpeg → FLAC + AAC fallback; JSON → `.mid` branch. **Risk:** device sample differences (pin Chrome, commit hashes); iOS quirks; Puppeteer/Chrome updates (pin). **Fallback:** pages play pre-rendered `<audio>`; masters from MIDI in Reaper or SC NRT.

---

### 4. Rights — Pärt, *Für Alina* and *Spiegel im Spiegel*

- **Publisher:** Universal Edition, Vienna, for both [V] — [Arvo Pärt Centre, Für Alina](https://www.arvopart.ee/en/arvo-part/work/477/), [UE 19823](https://www.universaledition.com/en/Paert-For-Alina-Variations-for-the-Healing-of-Arinushka/P0018616), UE 30336 for *Spiegel* [V]. UE is not part of Wise Music [V] — [MBW](https://musicbusinessworldwide.com/wise-music-group-acquires-austria-based-classical-music-publisher-doblinger-musikverlag). Pärt alive → fully protected [I].
- **Sync at UE:** no form, no fee schedule; a "specific briefing" to the promotion team [V] — [UE Music for Film and Media](https://www.universaledition.com/en/Hire-Licenses/Music-for-Film-and-Media/). US/Canada contact at Concord (Brooke Primont) [V]; whether Concord covers other territories [U]. UE itself lists *Für Alina* and *Spiegel* in *Gerry* among its licences [V] — [UE film page](https://www.universaledition.com/en/film-commercials-games). Vienna: Karlsplatz 6, +43 1 33723-0; promotion +43 1 33723-100 [V] — [UE locations](https://universaledition.com/locations). Which office handles Turkey [U].
- **Masters:** ECM 1591 *Alina* (rec. 1995, rel. 1999): Malter; Spivakov/Bezrodny; Schwalke/Malter [V] — [Presto](https://www.prestomusic.com/classical/articles/49--recording-of-the-week-arvo-parts-spiegel-im-spiegel). ECM's sync process **not found** [U]; DG/UMG handle distribution only [V]. Other recordings (Kremer/Eurodisc 1980, Arden/Koch) are other master routes [V].
- **Staging:** fees step by use — exhibition, distribution/editions, online [V] — [Film Independent](https://www.filmindependent.org/blog/legal-ease-navigating-the-ins-and-outs-of-music-licensing). **No published UE/Pärt fee** [U]; only anecdotal vendor ranges (€200–2,000 corporate; €5,000–50,000+ broadcast) [U] — [Artyfile](https://artyfile.com/blog/what-does-a-sync-license-cost). The one official exhibition tariff found: STIM SEK 489–5,732 (performance, not sync) [V] — [STIM](https://stim.se/en/om-oss/villkor-och-avtal/prices-and-terms-for-music-licenses/exhibition-installation).
- **New recording:** removes the label; UE sync still required [V]; performer contracts and possibly mechanical (MESAM) [I].
- **Turkey:** MESAM + MSG license jointly since 2022 [V] — [CISAC](https://www.cisac.org/Newsroom/articles/good-news-societies-and-creators-turkey-cmos-achieve-new-collaboration); exhibition tariff [U]; MÜYAP for recordings [U]. Europe: TONO licenses sync for video installations; GEMA does not (go to the rightsholder) [V].
- **Precedents:** *Heaven* (Tykwer 2002) credits ECM recordings "courtesy of Universal Edition" — composition and master cleared separately [V] — [IMDb](https://imdb.com/title/tt0246677/soundtrack). *Spiegel* in *Wit, Gerry, Swept Away, About Time, Foxtrot*, *Gravity* trailer; *Für Alina* in *Mostly Martha, Foxcatcher* [V]. V&A *Memory & Light* (2018) was a sanctioned collaboration [V]; terms [U]. No documented refusal, no documented gallery video-edition licence [U].

**Recommended:** one brief to UE Vienna (both works; what the video is; venues and territories TR + EU; edition size e.g. 5 + 2 AP; online yes/no; full or excerpt) asking three prices; ECM quote in parallel; price a new recording. **Risk:** refusal or editorial approval of the cut [U]; ECM process unknown; editions least likely in a standard licence; no public fees. Not legal advice.

---

### 5. Exhibition, sale, and clip tools

**A. Editions and listening**
- Daata model: 15 editions, price rises per sale, buyer gets downloadable hi-res file + named certificate transferable on resale + re-download + private display only; artist keeps IP [V, 2015 source, current practice U] — [On Screen Today](https://onscreentoday.com/conversation/art-collecting-in-the-air-en/). EAI: certificate signed by artist and gallery, edition number, licensed rights [V] — [EAI](https://eai.org/resourceguide/collection/singlechannel/agreementscontracts.html). Ed Atkins / Vinyl Factory: signed vinyl, 100 + 20 AP, £110 [V]; Rondinone sound edition of 3 + 1 AP with certificate [V].
- QR uptake 4.5 % to 40 % at National Museums Scotland; own domain, clear call to action, code ≈ 1/10 of viewing distance, short URL printed, light page [V] — [NMS](https://blog.nms.ac.uk/?p=30536). Visitors rarely use earbuds → spill; state clip length; dynamic codes [V] — [AAM forum](https://community.aam-us.org/discussion/qr-codes-to-access-audio-clips).
- Directional speakers (Holosonics, Panphonics, Focusonics): vendor sources only; weak bass likely [U]; no published prices.

**B. Clip tools (2026)**
- Midjourney Video 5 s + 4 s steps to 21 s, 480/720p, `--end`, `--loop` [V] — [docs](https://docs.midjourney.com/docs/video). Runway Gen-4.5 2–10 s [V]. Kling 3.0 15 s, extensions ~3 min with drift after ~2 [V]; Veo 3.1 4/6/8 s, extensions to 148 s at 720p; limits disagree across sources [V/U] — [invideo](https://invideo.io/blog/kling-3-vs-veo-3-1/). **No tool holds a 9-minute shot.**
- TouchDesigner non-commercial capped at 1280 px and not for paid work; commercial $600 [V] — [Derivative](https://docs.derivative.ca/TouchDesigner_Products). After Effects "Convert Audio to Keyframes" + PSD import [V] — [AEJuice](https://aejuice.com/blog/how-to-link-keyframes-to-audio-in-adobe-after-effects/). Both Pärt pieces are quiet and near-static: amplitude-reactivity gives jitter, not motion; place events by hand on phrase structure [I].

**Recommended A:** image + sound as one numbered edition; print + 24-bit WAV on own domain + certificate + QR card; listening page < 1 MB on own domain, duration shown, short URL under the code; one wipeable headphone station or one directional speaker for a flagship piece. **Risk:** low uptake; spill; domain must live as long as the edition.
**Recommended B:** After Effects backbone, PSD layers, hand markers to the score, long dissolves and slow drift, AI clips as inserts chained by start/end frames; skip TouchDesigner/Resolume/Notch. **Risk:** rights first; 480–720p inserts need upscaling.

---

### 6. Proposed architecture (one page)

```
MJDL (writes)                     Xanadu Sound (reads only)
─────────────                     ────────────────────────────────────────────
frames/<id>.json ───────────────▶ build/
cloud F/S/E/K.json ─────────────▶   rules.json      ← the mapping table = the work (dated, versioned)
                                    engine.js       ← raw Web Audio, one file, pinned
                                    build.js        ← JSON + rules → listen/<id>/index.html
                                                     JSON + rules → midi/<id>.mid
                                  render/
                                    render.js       ← same engine.js in pinned headless Chrome
                                                     → masters/<id>.wav (24/48)
                                    master.sh       ← ffmpeg loudnorm 2-pass → flac/ + aac/ + hashes.txt
                                  listen/<id>/      ← tap → AudioContext inside gesture; audioSession playback;
                                                     fallback <audio src=aac>; duration shown; short URL
                                  legend/           ← 20 s legend track + wall text (rules, 3-voice cap, name-tone rule)
                                  edition/           ← certificate template (edition no., private display, WAV hash)
                                  part-clip/         ← blocked until UE answer; brief + quotes live here
```

**rules.json (v0.2 draft, to be ruled on by ear):**

| Input | Channel | Rule |
|---|---|---|
| node name | pitch (identity only) | hash → degree of D mode → M-note |
| — | harmony | T-note = fixed table (close, inferior, D triad); D+A pedal |
| partition F / S·E / K | timbre + stereo | three clearly different timbres; centre / left / right |
| gene | register | bands ≥ 1 octave apart; K highest |
| value 0–1 | duration or repeats | not loudness |
| sign + / − | accent | + first note accented; − = rest (brief §5.2) or last-note accent — choose one |
| `&` | interval | superior + inferior together (fusing) |
| `\|` | process | T-position alternates, never settles; optional semitone accent |
| ambiguity 0–100 | beating / glide | 0 = none; else beat rate ∝ score, or glide ≥ 1 semitone; no small wander |
| ⟡ flag | sustain | hold the T-note |
| density | cap | ≤ 3 lines audible; rest = bed |
| constraint | tuning | never E and B together in JI, or tune by triad |

---

### 7. What this report changes in the brief, and what it does not settle

- §4's three forms are no longer three mappings; they become three *densities* of one rule set (line = 1 voice, layers ≤ 3, soft = 1 + bed). *Layers* at 4–5 voices contradicts the evidence.
- §5 rule 3 (value → loudness) reversed.
- §9 risk "hash notes are meaningless" becomes the first sentence of the wall text.
- §10: no design until UE replies. The brief to UE is the next deliverable.
- **Not settled by research:** whether tintinnabuli beside a Pärt clip reads as homage or imitation — that is a curatorial judgement; whether the agents' timbre separation is achievable in raw oscillators — that is a listening test.

