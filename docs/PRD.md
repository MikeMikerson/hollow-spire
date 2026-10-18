# Hollow Spire — Product Requirements Document (PRD)

| | |
|---|---|
| **Working title** | Hollow Spire |
| **Document** | Product Requirements Document |
| **Version** | 0.1 (Draft) |
| **Last updated** | 2026-10-18 |
| **Owner** | TBD |
| **Companion doc** | [Game Design Document](./GDD.md) |

---

## 1. Summary

**Hollow Spire** is a fast, hand-drawn 2D action-platformer roguelite. Each run is one climb up a living tower woven from silk. The tower rebuilds itself every time someone climbs it.

Moment to moment, it plays like a modern precision action-platformer: quick, aggressive needle combat, pogo strikes, dashes and a silk-based healing economy. The structure between rooms comes from deckbuilding roguelites: a branching route map, drafting a build one reward at a time, risky elite fights, benches where you must choose between healing and upgrading, and readable enemy intents.

**The hook:** there are no cards. Your build is woven onto a **Spindle**, a visible queue of silk skills that rotates each time you use one. Adding a skill makes the rotation less predictable. Removing one makes it tighter. Choices made between rooms directly change how combat plays.

**Inspirations:** *Hollow Knight: Silksong* (art direction, movement, combat tempo) and *Slay the Spire 2* (run structure, drafting, map, intents, Ancients, alternate acts, meta timeline). Hollow Spire uses original characters, world, art and names, and its own visual identity built on a **textile / woven-thread motif**.

---

## 2. Product pillars

These are ranked. When two pillars conflict, the higher one wins.

1. **Fast.** Movement is quick, combat is aggressive, rooms are short, and restarting is near-instant. The player should almost never be waiting. A full run fits in one sitting (about 35–40 minutes).
2. **Beautiful.** Hand-drawn, painterly 2D art with deep parallax, atmospheric light and expressive frame-by-frame animation. Every screenshot should look like a painting, and gameplay must still be easy to read.
3. **Readable.** The player always knows what is about to hit them (intent glyphs, clear telegraphs, a consistent visual language for danger). When the player dies, it feels fair.
4. **Builds you can feel.** Every reward changes how you move or fight, not just your numbers. The Spindle turns build decisions into combat rhythm.
5. **One more climb.** Short runs, meaningful variety, and a meta layer that unlocks new things without raising raw power.

---

## 3. Problem & opportunity

- Action roguelites (*Dead Cells*, *Hades*, *Rogue Legacy*) are proven. Few combine **precision platforming** with **deckbuilder-style strategy between rooms**. Most action roguelites offer simple pick-1-of-3 stat boons without the consistency and dilution tension that makes deckbuilders deep.
- Metroidvania fans love the feel and art of *Silksong*-like games, but those games take 30+ hours and suit replay poorly. Hollow Spire offers that feel in **replayable, session-sized runs**.
- Deckbuilder fans enjoy route planning and building synergies but may want a more physical, skill-expressive experience.
- Hand-drawn 2D art that stands out sells strongly on Steam and in trailers, and gives a small team a recognisable brand.

---

## 4. Target audience

| Segment | Description | What they want from us |
|---|---|---|
| **Primary: action-platformer fans** | Players of Hollow Knight, Silksong, Celeste, Ori, Dead Cells. Ages 18–35, PC and Switch. | Tight controls, beautiful art, hard but fair bosses, mastery. |
| **Secondary: roguelite strategists** | Players of Slay the Spire, Monster Train, Hades, Balatro. | Build depth, synergies, route decisions, high replay value, Ascension-style difficulty ladders. |
| **Tertiary: streamers / speedrunners** | Content creators. | Short runs, seeded runs, readable spectacle, a daily challenge. |

### Personas
- **"Mara," 27, the Silksong completionist.** Plays on Steam Deck in 30–60 minute sessions. Will drop the game if the controls feel floaty or the art feels cheap. Wants to master bosses.
- **"Dev," 31, the Slay the Spire Ascension grinder.** Has 600 hours across deckbuilders. Wants every reward to involve a real choice, and wants to win through planning as well as reflexes.

---

## 5. Goals & non-goals

### Goals
- G1: Deliver movement and combat feel on par with the best of the genre: responsive, low latency, satisfying hit feedback.
- G2: Ship a hand-drawn art style good enough to be a primary selling point in trailers and capsule art.
- G3: Average full-run length of **35–40 minutes**, and under **10 seconds** from death to the next run.
- G4: Build depth that holds up for 100+ hours for the strategist audience (multiple Climbers, Heights difficulty ladder).
- G5: Launch on PC (Steam) with Steam Deck Verified status, with console ports as a fast follow.

### Non-goals (for 1.0)
- Not a metroidvania. No persistent interconnected world, no backtracking, no permanent ability gates.
- Not a card game. No cards, hands or turns.
- No procedurally generated room geometry. Rooms are hand-authored with procedural variants; the route is procedural.
- No online PvP.
- No free-to-play monetisation, loot boxes or battle pass.
- Online co-op is **not** in 1.0 scope (see §8, post-launch).

---

## 6. Success metrics

| Metric | Target | Measured via |
|---|---|---|
| Steam wishlists before Early Access | 150k+ | Steamworks |
| Demo median playtime (Next Fest) | ≥ 45 min | Opt-in telemetry |
| Demo → wishlist conversion | ≥ 20% | Steamworks |
| Median full-run length (win or loss, reaching Act 2+) | 30–45 min | Telemetry |
| Time from death to controllable new run | ≤ 10 s | Automated test |
| Early-run quit rate (quit in first 3 chambers) | < 15% | Telemetry |
| First-win rate for a Climber within 10 runs | 25–40% | Telemetry |
| Steam review score at 1.0 | ≥ 90% "Very Positive" | Steam |
| Input-to-action latency | ≤ 3 frames at 60 fps | Internal measurement |
| Stable frame rate on Steam Deck | Locked 60 fps | Perf testing |

---

## 7. Release phases & scope

| Phase | Goal | Contents |
|---|---|---|
| **P0 – Feel prototype** | Prove movement, combat and the Spindle are fun in greybox. | 1 Climber's moveset, 6 greybox chambers, 3 enemies, 1 boss, Spindle with 8 Threads, basic map. |
| **P1 – Vertical slice** | Prove the art style and full Act 1 loop at final quality. Use it to estimate content cost. | 1 Climber (The Wisp), Act 1 biome (Rootwell) at final art quality, ~20 chambers, 8 enemies, 2 elites, 1 boss, 1 Ancient, 20 Threads, 15 Keepsakes, 5 Vials, bench / merchant / 3 Vignettes. |
| **P2 – Public demo** | Steam Next Fest. Collect wishlists and feedback. | Vertical slice plus polish, onboarding, telemetry, Heights 1–3. |
| **P3 – Early Access** | Paid launch and community feedback loop. | 3 Climbers, Acts 1–3 (Act 1 with both alternate biomes), final boss, Heights 1–10, Tapestry meta progression (first half). |
| **P4 – 1.0** | Full release. | 5 Climbers, all alternate biomes, Heights 1–15, full Tapestry, daily climb, seeded runs, full localisation, console certification start. |
| **P5 – Post-launch** | Retention. | Local/online co-op (2–4 players), new Climber, mod support (exploratory). |

---

## 8. Functional requirements

Priority: **Must** = required for its phase · **Should** = strongly desired · **Could** = only if time allows.

### 8.1 Movement & combat
| ID | Requirement | Priority | Phase |
|---|---|---|---|
| MC-1 | Responsive run, variable-height jump, coyote time, jump buffering, dash, wall-cling / wall-jump, and downward pogo strike. Starting tuning values are in the GDD. | Must | P0 |
| MC-2 | Needle attack in 4 directions (side, up, down-in-air, down-diagonal pogo) with hit-stop and knockback. | Must | P0 |
| MC-3 | Attack recovery can be cancelled into dash or jump. The player never loses control for more than 0.25 s, except during Bind or after taking damage. | Must | P0 |
| MC-4 | Silk meter fills from needle hits. Silk is spent on Silk Skills (from the Spindle) or on **Bind** (heal). | Must | P0 |
| MC-5 | Health is a small number of discrete pips (4–7 depending on Climber). It carries over between chambers. | Must | P0 |
| MC-6 | Every enemy attack shows an **intent glyph** and a readable wind-up animation before it lands. | Must | P0 |
| MC-7 | Each Climber has a unique mechanic (see GDD §9). | Must | P3 |

### 8.2 Run structure
| ID | Requirement | Priority | Phase |
|---|---|---|---|
| RS-1 | Procedurally generated branching route map per act (7 rows plus a boss), with chamber types: Arena, Elite, Bench, Merchant, Vignette, Cache. | Must | P0 |
| RS-2 | Choosing a route is physical: chamber exits are doors marked with the next node's icon. A map overlay is available at any time. | Must | P1 |
| RS-3 | An Ancient offers a choice of 3 blessings at the start of each act. | Must | P1 |
| RS-4 | Alternate biomes: each act (except the finale) has two biomes, chosen by route. | Should | P3 (Act 1), P4 (all) |
| RS-5 | Mid-run save at every chamber transition. Quitting and resuming returns the player to the start of the current chamber. | Must | P1 |
| RS-6 | Death goes to a run summary with a skippable recap, then a new run in 10 s or less. | Must | P1 |
| RS-7 | Seeded runs and a daily climb with a leaderboard. | Should | P4 |

### 8.3 Build systems
| ID | Requirement | Priority | Phase |
|---|---|---|---|
| BS-1 | **Spindle:** a visible, ordered queue of Threads (silk skills). Using a skill fires the front Thread and rotates the queue. The next 3 Threads are previewed. **Fray** skips the front Thread for a small silk cost. | Must | P0 |
| BS-2 | **Thread drafting:** after an Arena, choose 1 of 3 Threads or skip. Threads are offered as physical pickups in the room. | Must | P0 |
| BS-3 | **Tempering:** upgrade a Thread at a bench. | Must | P1 |
| BS-4 | **Unpicking:** remove a Thread at a bench or merchant. | Must | P1 |
| BS-5 | **Keepsakes:** passive items (Common / Uncommon / Rare / Ancient / Boss) that shape builds. | Must | P1 |
| BS-6 | **Vials:** one-shot consumables in a 3-slot belt. | Must | P1 |
| BS-7 | **Snags:** negative Threads that clog the Spindle (curses). | Should | P1 |
| BS-8 | **Embroidery:** rare modifiers applied to a single Thread. | Should | P3 |
| BS-9 | **Wish Threads:** quest Threads that transform once an in-run condition is met. | Could | P3 |

### 8.4 Meta & difficulty
| ID | Requirement | Priority | Phase |
|---|---|---|---|
| MD-1 | **The Tapestry:** a meta-progression timeline. Completing milestones unlocks Climbers, Threads, Keepsakes and lore panels. It never unlocks raw stat increases. | Must | P3 |
| MD-2 | **Heights:** a stacking difficulty ladder (1–15) per Climber, unlocked by winning. | Must | P3 (1–10), P4 (11–15) |
| MD-3 | Run history and statistics screen. | Should | P3 |
| MD-4 | **Remnant:** the previous run's death site may appear as a Vignette in the next run, with a chance to recover one Thread. | Could | P3 |

### 8.5 Art & animation (key focus)
| ID | Requirement | Priority | Phase |
|---|---|---|---|
| AA-1 | All characters, enemies and environments are **hand-drawn 2D**. No 3D-rendered characters and no pixel art. | Must | P1 |
| AA-2 | The player character and key enemies use **frame-by-frame** animation. Large bosses may use cutout/skeletal rigs with hand-drawn overlay frames for key poses. | Must | P1 |
| AA-3 | Environments use 5+ parallax layers (far, mid and near background; play layer; foreground silhouettes) plus fog, light-shaft and particle layers. | Must | P1 |
| AA-4 | Each biome has a defined palette and lighting key (see the GDD art bible). The player's accent colour and the danger colour are reserved and never used decoratively. | Must | P1 |
| AA-5 | An art bible is written and approved before vertical-slice production begins. | Must | P1 |
| AA-6 | Visual identity is built on a woven-thread motif (stitched seams, embroidery patterns, gold silk accents) so the game reads as its own and not as a clone. | Must | P1 |
| AA-7 | Authored at 2x the 1080p reference resolution. Displays cleanly at 720p (Deck/Switch) up to 4K. | Must | P1 |

### 8.6 UI / UX
| ID | Requirement | Priority | Phase |
|---|---|---|---|
| UX-1 | Minimal in-world HUD: health pips, silk spool, Spindle preview, bead count. | Must | P0 |
| UX-2 | Tooltips for every Thread, Keepsake, Vial and intent glyph. A glossary of keywords is accessible from the pause menu. | Must | P1 |
| UX-3 | First-run onboarding is taught through room design, not text walls. | Must | P2 |
| UX-4 | Full controller support, with keyboard + mouse and full rebinding. | Must | P1 |

### 8.7 Audio
| ID | Requirement | Priority | Phase |
|---|---|---|---|
| AU-1 | Adaptive music per biome (exploration layer and combat layer, plus a boss theme). | Must | P1 |
| AU-2 | Every intent type has a distinct audio cue. | Must | P1 |
| AU-3 | Instrumentation is chamber-orchestral, led by plucked and bowed strings. | Should | P1 |

### 8.8 Accessibility
| ID | Requirement | Priority | Phase |
|---|---|---|---|
| AC-1 | Intent glyphs are coded by shape first; colour is secondary. Colourblind filters are available. | Must | P1 |
| AC-2 | Toggles for screen shake, flashing and hit-stop intensity. | Must | P2 |
| AC-3 | Assist options: game speed (70–100%), extra health pips, longer i-frames. Runs using Assist are tagged but not penalised. | Should | P3 |
| AC-4 | Subtitles for all spoken or vocalised lines. Scalable UI text. | Must | P3 |

---

## 9. Non-functional requirements

| Area | Requirement |
|---|---|
| **Performance** | Locked 60 fps on Steam Deck and a GTX 1060-class PC. Supports 120/144 Hz. Gameplay runs on a fixed 60 Hz simulation tick, decoupled from rendering. |
| **Input latency** | At most 3 frames from button press to first visible response, at 60 fps. |
| **Load times** | Chamber transitions under 0.5 s (rooms are streamed or preloaded). Cold boot to main menu under 8 s. |
| **Saves** | Atomic writes, with a mid-run snapshot at each chamber transition. Cloud saves via Steam. |
| **Engine** | Recommended: **Godot 4.x** (strong 2D tooling, open source, no runtime fees; used by comparable 2D roguelites). Alternative: Unity 6. Final decision at the end of P0. |
| **Localisation** | All strings externalised from day one. 1.0 languages: EN, FR, DE, ES, PT-BR, JA, ZH-Hans, KO, RU. |
| **Telemetry** | Opt-in only. Collects run length, death location and cause, reward picks and skip rates, and route choices. |
| **Platforms** | PC (Windows, Linux/Deck, macOS) at launch. Switch 2, PS5 and Xbox Series after 1.0. |

---

## 10. Business model

- **Premium**, one-time purchase. Target price **$19.99–$24.99 USD** at 1.0, discounted in Early Access.
- No microtransactions. Possible future paid expansion (new Climber + act).

---

## 11. Team & dependencies (assumed)

A small indie team, scaled by phase:

| Role | P0 | P1–P2 | P3–P4 |
|---|---|---|---|
| Game director / designer | 1 | 1 | 1 |
| Gameplay programmer | 1 | 2 | 2–3 |
| 2D animator (frame-by-frame) | 0–1 | 2 | 3 |
| Environment / concept artist | 0–1 | 1–2 | 2 |
| Composer / sound designer | contract | contract | 1 |
| Level designer | – | 1 | 2 |
| QA / producer | – | part-time | 1–2 |

---

## 12. Risks & mitigations

| Risk | Impact | Likelihood | Mitigation |
|---|---|---|---|
| **Hand-drawn animation cost** exceeds budget. | High | High | Price everything during the vertical slice. Cap animation states per enemy. Share rigs and base animation sets across enemy families. Use skeletal animation with drawn overlays for bosses. |
| **The Spindle feels confusing in real-time combat.** | High | Medium | Prototype in P0 with 3 variants (pure queue, queue + Fray, queue + free pick of the top 2). Playtest with 10+ external players. Fallback: fixed skill slots plus draft. |
| **Too many hand-made rooms to build** for a roguelite. | High | Medium | Build each room template with variant layers (hazards, enemy sets, mirroring). Target ~40 templates per biome, each with 4+ variants. |
| **Runs get longer** as content is added. | Medium | Medium | Hard target: 7 rows per act. Chamber time budget of 45–90 s. Telemetry alerts if the median run exceeds 45 min. |
| **Looks or feels too derivative** of its inspirations. | High | Medium | Original characters and world, a textile visual identity, original names. Brand review at each art milestone. |
| **Difficulty splits the audience** (platformer veterans vs. strategists). | Medium | Medium | Heights ladder, Assist options, and Climbers covering a range of skill levels. |
| **Scope creep from co-op.** | High | Medium | Co-op is explicitly post-launch. Keep the architecture co-op-aware (deterministic input, entity ownership) but don't build co-op features before 1.0. |

---

## 13. Milestones (relative)

| Milestone | Target | Exit criteria |
|---|---|---|
| P0 Feel prototype | Month 0–3 | Blind playtesters rate controls as at least "tight." A Spindle variant has been chosen. Engine is locked. |
| P1 Vertical slice | Month 3–8 | Act 1 is playable start to boss at final art quality. Cost-per-asset figures are known. Art bible is locked. |
| P2 Demo | Month 8–10 | Next Fest build passes the perf and latency targets. Telemetry is live. |
| P3 Early Access | Month 10–20 | 3 Climbers and 3 acts. Crash-free sessions ≥ 99.5%. |
| P4 1.0 | Month 20–30 | All content in, localisation complete, review score target tracking. |

---

## 14. Open questions

1. Is the Spindle's preview length (3) right, or should it vary by Climber or Keepsakes?
2. Should damage between chambers persist fully (as in Slay the Spire) or partially regenerate? The current proposal is full persistence plus Bench Rest.
3. Does Act 1 need a guaranteed Merchant for new players?
4. Does the final act need a "true ending" requirement (e.g., a specific Keepsake set) in the way deckbuilder roguelites often do?
5. Co-op design: shared Spindle or individual Spindles? (Post-launch.)
6. Final name: is "Hollow Spire" clear for trademark and too close to existing titles? Legal check needed before the store page goes up.

---

## 15. Glossary

| Term | Meaning |
|---|---|
| **Climber** | A playable character. |
| **Chamber** | A single room / map node. |
| **Thread** | A silk skill. The roguelite equivalent of a card. |
| **Spindle** | The rotating queue of Threads. The equivalent of a deck. |
| **Fray** | Skip the front Thread on the Spindle by spending silk. |
| **Tempering** | Upgrading a Thread. |
| **Unpicking** | Removing a Thread. |
| **Snag** | A negative Thread (curse). |
| **Embroidery** | A modifier applied to one Thread. |
| **Keepsake** | A passive relic-like item. |
| **Vial** | A one-shot consumable. |
| **Bind** | Spend silk to heal. |
| **Beads** | Currency. |
| **Ancient** | A giant creature woven into the Spire that offers blessings at the start of each act. |
| **Heights** | Difficulty ladder. |
| **The Tapestry** | Meta-progression timeline. |
