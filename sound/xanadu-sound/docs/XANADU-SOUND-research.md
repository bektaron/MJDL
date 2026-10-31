# Xanadu Sound — system research report

Version 0.1 · 31 Oct 2026 · five parallel research agents (Opus) + synthesis (Fable). Brief: `XANADU-SOUND-project.md` v0.1 §1–10. Requested by Bekir Kıraç. Working language of the report: English (system file).

Marks: **[V]** verified in a cited source · **[I]** inference by an agent or the advisor · **[U]** not verified. The agents did not hear any of the pages. Nothing here is a listening judgement.

---

## 0. Decisions this report recommends (one screen)

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

## 1. Sonification — what untrained ears can follow

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

## 2. Rule systems — which guarantees listenability by rule

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

## 3. Toolchain

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

## 4. Rights — Pärt, *Für Alina* and *Spiegel im Spiegel*

- **Publisher:** Universal Edition, Vienna, for both [V] — [Arvo Pärt Centre, Für Alina](https://www.arvopart.ee/en/arvo-part/work/477/), [UE 19823](https://www.universaledition.com/en/Paert-For-Alina-Variations-for-the-Healing-of-Arinushka/P0018616), UE 30336 for *Spiegel* [V]. UE is not part of Wise Music [V] — [MBW](https://musicbusinessworldwide.com/wise-music-group-acquires-austria-based-classical-music-publisher-doblinger-musikverlag). Pärt alive → fully protected [I].
- **Sync at UE:** no form, no fee schedule; a "specific briefing" to the promotion team [V] — [UE Music for Film and Media](https://www.universaledition.com/en/Hire-Licenses/Music-for-Film-and-Media/). US/Canada contact at Concord (Brooke Primont) [V]; whether Concord covers other territories [U]. UE itself lists *Für Alina* and *Spiegel* in *Gerry* among its licences [V] — [UE film page](https://www.universaledition.com/en/film-commercials-games). Vienna: Karlsplatz 6, +43 1 33723-0; promotion +43 1 33723-100 [V] — [UE locations](https://universaledition.com/locations). Which office handles Turkey [U].
- **Masters:** ECM 1591 *Alina* (rec. 1995, rel. 1999): Malter; Spivakov/Bezrodny; Schwalke/Malter [V] — [Presto](https://www.prestomusic.com/classical/articles/49--recording-of-the-week-arvo-parts-spiegel-im-spiegel). ECM's sync process **not found** [U]; DG/UMG handle distribution only [V]. Other recordings (Kremer/Eurodisc 1980, Arden/Koch) are other master routes [V].
- **Staging:** fees step by use — exhibition, distribution/editions, online [V] — [Film Independent](https://www.filmindependent.org/blog/legal-ease-navigating-the-ins-and-outs-of-music-licensing). **No published UE/Pärt fee** [U]; only anecdotal vendor ranges (€200–2,000 corporate; €5,000–50,000+ broadcast) [U] — [Artyfile](https://artyfile.com/blog/what-does-a-sync-license-cost). The one official exhibition tariff found: STIM SEK 489–5,732 (performance, not sync) [V] — [STIM](https://stim.se/en/om-oss/villkor-och-avtal/prices-and-terms-for-music-licenses/exhibition-installation).
- **New recording:** removes the label; UE sync still required [V]; performer contracts and possibly mechanical (MESAM) [I].
- **Turkey:** MESAM + MSG license jointly since 2022 [V] — [CISAC](https://www.cisac.org/Newsroom/articles/good-news-societies-and-creators-turkey-cmos-achieve-new-collaboration); exhibition tariff [U]; MÜYAP for recordings [U]. Europe: TONO licenses sync for video installations; GEMA does not (go to the rightsholder) [V].
- **Precedents:** *Heaven* (Tykwer 2002) credits ECM recordings "courtesy of Universal Edition" — composition and master cleared separately [V] — [IMDb](https://imdb.com/title/tt0246677/soundtrack). *Spiegel* in *Wit, Gerry, Swept Away, About Time, Foxtrot*, *Gravity* trailer; *Für Alina* in *Mostly Martha, Foxcatcher* [V]. V&A *Memory & Light* (2018) was a sanctioned collaboration [V]; terms [U]. No documented refusal, no documented gallery video-edition licence [U].

**Recommended:** one brief to UE Vienna (both works; what the video is; venues and territories TR + EU; edition size e.g. 5 + 2 AP; online yes/no; full or excerpt) asking three prices; ECM quote in parallel; price a new recording. **Risk:** refusal or editorial approval of the cut [U]; ECM process unknown; editions least likely in a standard licence; no public fees. Not legal advice.

---

## 5. Exhibition, sale, and clip tools

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

## 6. Proposed architecture (one page)

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

## 7. What this report changes in the brief, and what it does not settle

- §4's three forms are no longer three mappings; they become three *densities* of one rule set (line = 1 voice, layers ≤ 3, soft = 1 + bed). *Layers* at 4–5 voices contradicts the evidence.
- §5 rule 3 (value → loudness) reversed.
- §9 risk "hash notes are meaningless" becomes the first sentence of the wall text.
- §10: no design until UE replies. The brief to UE is the next deliverable.
- **Not settled by research:** whether tintinnabuli beside a Pärt clip reads as homage or imitation — that is a curatorial judgement; whether the agents' timbre separation is achievable in raw oscillators — that is a listening test.
