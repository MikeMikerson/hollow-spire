# Hollow Spire — Game Design Document (GDD)

| | |
|---|---|
| **Working title** | Hollow Spire |
| **Document** | Game Design Document |
| **Version** | 0.1 (Draft) |
| **Last updated** | 2026-10-18 |
| **Companion doc** | [Product Requirements Document](./PRD.md) |

> All numbers in this document are **starting tuning values** for prototyping, not final balance.

---

## Table of contents
1. [Vision](#1-vision)
2. [Core loops](#2-core-loops)
3. [Controls & movement](#3-controls--movement)
4. [Combat](#4-combat)
5. [The Spindle](#5-the-spindle)
6. [Threads](#6-threads)
7. [Keepsakes](#7-keepsakes)
8. [Vials](#8-vials)
9. [Climbers](#9-climbers)
10. [Run structure & map](#10-run-structure--map)
11. [Chamber design](#11-chamber-design)
12. [Enemies & intents](#12-enemies--intents)
13. [Bosses](#13-bosses)
14. [Ancients](#14-ancients)
15. [Acts & biomes](#15-acts--biomes)
16. [Economy](#16-economy)
17. [Meta progression: the Tapestry & Heights](#17-meta-progression-the-tapestry--heights)
18. [World & narrative](#18-world--narrative)
19. [Art direction (art bible v0)](#19-art-direction-art-bible-v0)
20. [Animation & game feel](#20-animation--game-feel)
21. [Camera](#21-camera)
22. [UI & HUD](#22-ui--hud)
23. [Audio](#23-audio)
24. [Accessibility & assist](#24-accessibility--assist)
25. [Death, saves & quick restart](#25-death-saves--quick-restart)
26. [Co-op (post-launch)](#26-co-op-post-launch)
27. [Content targets](#27-content-targets)
28. [Open design questions](#28-open-design-questions)

---

## 1. Vision

### 1.1 High concept
*A hand-drawn, high-speed climb up a tower that re-weaves itself every run. Fight like a duellist, plan like a strategist.*

### 1.2 Design pillars
| Pillar | What it means in practice |
|---|---|
| **Fast** | High movement speed, short attack recoveries, cancelable actions, 45–90 s chambers, under 0.5 s room transitions, under 10 s from death to new run. No long corridors, no padding, no unskippable text. |
| **Beautiful** | Painterly hand-drawn art, deep parallax, expressive frame-by-frame animation. Every chamber should be screenshot-worthy. |
| **Readable** | Intent glyphs plus telegraph animation for every attack. A consistent danger language. The play layer always has more contrast than the background. |
| **Builds you can feel** | Every Thread and Keepsake changes *how you play*. The Spindle turns strategy into rhythm. |
| **One more climb** | A full run in about 35–40 minutes. Variety comes from Climbers, biomes, Ancients and drafts. |

### 1.3 What we take from our inspirations

| From *Silksong*-style action-platformers | From *Slay the Spire 2*-style deckbuilders |
|---|---|
| Agile, aggressive movement and needle combat | Branching route map with node types |
| Diagonal pogo, dash, wall-cling | Draft one of three, with skip as a real option |
| Silk meter powering both skills and healing | Deck dilution / consistency tension (the Spindle) |
| Hand-drawn painterly art, parallax, atmosphere | Relics (Keepsakes), potions (Vials), curses (Snags) |
| Tools as limited-use items | Enemy intents shown ahead of time |
| | Ancients offering blessings at the start of each act |
| | Alternate acts, enchantments (Embroidery), quest cards (Wish Threads) |
| | Timeline meta progression (the Tapestry), Ascension (Heights) |

**What we deliberately don't take:** cards, turns or energy; a persistent metroidvania world; any character, creature, name or asset from either game.

---

## 2. Core loops

```
MOMENT (1–5 s)    move → read intent → strike / dodge / pogo → gain silk → spend silk
ROOM   (45–90 s)  enter → clear or traverse → collect reward → choose exit door
ACT    (~11 min)  Ancient blessing → 7 chambers on a route → Boss
RUN    (~35–40 min) Act 1 → Act 2 → Act 3 → Crown Loom (final boss)
META   (many runs)  Tapestry unlocks → new Climbers / Threads → Heights ladder
```

The loop alternates between **fast execution** (inside chambers) and **brief strategy** (rewards, doors, benches). Strategy moments should take seconds, not minutes, and most of them happen while the player is still physically moving through the space.

---

## 3. Controls & movement

### 3.1 Default bindings

| Action | Gamepad | Keyboard |
|---|---|---|
| Move / aim | Left stick / D-pad | WASD / arrows |
| Jump | A / Cross | Space |
| Needle attack | X / Square | J |
| Silk Skill (fire front Thread) | Y / Triangle | K |
| Dash | RB / R1 | L / Shift |
| Bind (heal, hold) | B / Circle | F |
| Fray (skip front Thread) | LB / L1 | Q |
| Use Vial (cycle with D-pad ↕) | LT / L2 | E (1–3 to select) |
| Map overlay | View / Touchpad | Tab |
| Pause | Menu / Options | Esc |

All bindings can be remapped. Pogo is a down attack while airborne. **Pogo direction is configurable**: straight down or diagonal down-forward.

### 3.2 Movement verbs
- **Run:** fast acceleration, near-instant stop. Quick turnaround is a must.
- **Jump:** variable height (release to cut). Coyote time and jump buffer.
- **Dash:** fixed-distance horizontal burst, usable once in the air until you land, hit a wall or pogo something.
- **Wall-cling / wall-jump:** cling slides slowly. A wall-jump kicks the player away from the wall, with a short lockout before they can steer back.
- **Pogo:** a down-strike that bounces the player up off enemies, hazards marked as pogo-able, and silk nodes. Pogo resets the dash and air-jump (if they have one).
- **Ledge grab:** automatic mantle onto ledges within 0.4 tiles of the hands.

### 3.3 Starting tuning values

Units: **1 tile = 64 px at the 1080p reference**. The player is ~2 tiles tall. The simulation runs at a fixed 60 Hz.

| Parameter | Value |
|---|---|
| Run speed | 9.5 tiles/s |
| Ground accel / decel | reach full speed in 0.06 s / stop in 0.04 s |
| Air control | 85% of ground accel |
| Jump height (full / min tap) | 4.25 tiles / 1.25 tiles |
| Time to jump apex | 0.36 s |
| Gravity multiplier when falling | 1.6x |
| Max fall speed | 22 tiles/s |
| Coyote time | 0.10 s |
| Jump buffer | 0.12 s |
| Dash distance / duration | 4.5 tiles / 0.16 s |
| Dash cooldown (grounded) | 0.35 s |
| Wall slide speed | 4 tiles/s |
| Wall-jump horizontal lockout | 0.12 s |
| Pogo bounce height | 3.25 tiles |
| Ledge-grab tolerance | 0.4 tiles |

**Feel rules:**
- The player character never "slides" after releasing the stick on the ground.
- Every movement input produces a visible response within 3 frames.
- Hitting your head on a ceiling cancels upward velocity cleanly (no sticky ceilings). There is a 4 px corner-correction nudge.

---

## 4. Combat

### 4.1 Needle attack
| Property | Value |
|---|---|
| Base damage | 10 |
| Startup / active / recovery | 2 / 4 / 9 frames (60 Hz) |
| Cancel window | Recovery can be cancelled into dash or jump from frame 7 onward |
| Range | 1.6 tiles forward, 1.2 tiles tall arc |
| Directions | Side, up, down (air only, pogo) |
| Attack rate | Up to ~4 attacks/s with buffering |
| On hit | +1 silk, 3-frame hit-stop, enemy knockback 0.5 tiles, player recoil 0.25 tiles (ground only) |

### 4.2 Health
- Health is shown as **pips**. Most hits deal **1 pip**. Heavy attacks and later-act enemies deal **2 pips**, which their intent glyph indicates.
- Climbers start with 4–7 max pips (see §9). A full run might reach 8–10 pips.
- After taking damage the player has **1.1 s of i-frames** (flickering).
- Hazards (spikes, thorns, acid) deal 1 pip and **respawn the player at the last safe ground** in the chamber. This keeps the pace up: no long walk back.
- Health **carries over between chambers**. Healing comes from Bind, Bench Rest, Keepsakes and Vials.

### 4.3 Silk & Bind
- **Silk meter:** 9 segments. Gain +1 per needle hit (some Keepsakes and Threads change this).
- **Silk Skill:** fires the front Thread on the Spindle, costing that Thread's silk (typically 2–4).
- **Bind:** hold to spend **6 silk** and heal **2 pips** over **0.45 s**. Works on the ground or in mid-air (the player hovers briefly). Taking a hit cancels it, and the silk is lost.
- **The central tension:** spending silk on skills makes you more aggressive, while holding it back lets you heal. This choice repeats several times a minute.

### 4.4 Damage & status keywords
| Keyword | Effect |
|---|---|
| **Venom X** | Deals X damage per second, ticking down 1 per second. Stacks. |
| **Bleed** | The next hit taken deals +50% damage, then Bleed is removed. |
| **Rime X** | Slows enemies by 5% per stack (max 50%). Decays over 4 s. |
| **Snare** | Enemy is rooted for 1.5 s. Bosses are immune; they get Rime 3 instead. |
| **Toll X** | If the enemy's HP is X or less, it is executed. (Bonebinder) |
| **Ward X** | Absorbs the next X damage instances. Player only. |
| **Exposed** | Enemy takes +25% damage for 4 s. |

### 4.5 Enemy HP targets (Act 1 baseline)
| Type | HP | Needle hits |
|---|---|---|
| Fodder | 20–30 | 2–3 |
| Standard | 40–60 | 4–6 |
| Heavy | 90–120 | 9–12 |
| Elite | 220–300 | — |
| Boss | 700–900 | — |

Each act scales enemy HP by about 1.5x and adds more 2-pip attacks. The player's damage scales mainly through their build, not flat increases.

---

## 5. The Spindle

The Spindle is Hollow Spire's main design innovation. It brings deckbuilder-style **consistency vs. variety** decisions into real-time combat.

### 5.1 Rules
1. The Spindle is an **ordered loop** of Threads. Each run starts with 4 Threads in a set order, defined per Climber.
2. The HUD shows the **front Thread plus the next 2** (preview length 3).
3. Pressing **Silk Skill** fires the front Thread if you have enough silk. That Thread then moves to the **back** and the queue advances.
4. Without enough silk, the input fails and the Thread's icon flashes. The queue doesn't advance.
5. **Fray** (1 silk): sends the front Thread to the back without firing it. It can be used repeatedly, with a 0.2 s cooldown.
6. A newly drafted Thread is inserted **at the back** of the queue.
7. Outside of combat (benches, the map), the player can **reorder** the Spindle freely. Ordering is part of building.
8. There is no hard length cap, but Keepsakes and Ancients may impose caps or rewards tied to length.

### 5.2 Why it works
- **Thin Spindle (4–6 Threads):** a predictable rotation. You learn the rhythm and can plan combos (e.g., Snare → Heavy strike).
- **Thick Spindle (10+ Threads):** more raw options, but the right tool is less often at the front. Fray becomes a tax on silk.
- **Ordering** works like stacking a deck. It rewards players who plan sequences.
- **Snags** sit in the queue and must be Frayed past (or have their own effects). They work like curses without stopping play.

### 5.3 Prototype variants to test (P0)
| Variant | Description | Risk |
|---|---|---|
| A. Pure queue | As above. | Might feel rigid. |
| B. Queue + Fray (baseline) | As above, with Fray. | Recommended. |
| C. Top-2 choice | Two skill buttons, each firing one of the top two Threads. | More flexible but less tension. More buttons. |

Variant B is the baseline. The playtest metric is whether players can say what their next skill will be without looking at the HUD after 3 runs.

---

## 6. Threads

### 6.1 Thread anatomy
| Field | Notes |
|---|---|
| Name | Evocative, textile- or insect-themed. |
| Climber | Specific Climber or *Shared*. |
| Rarity | Common / Uncommon / Rare. |
| Silk cost | 1–5 (most are 2–3). |
| Type | **Strike** (deals damage), **Weave** (movement / utility), **Ward** (defensive), **Snag** (negative). |
| Effect | One clear sentence. |
| Tempered effect | A clear, felt upgrade: more range, damage or projectiles, or a lower cost. |

### 6.2 Drafting
- After an **Arena**: 3 Threads appear as glowing spools on pedestals. Standing next to one shows its tooltip, and interacting takes it. The others unravel. **Skipping** = leaving the room (a small bead bonus encourages skipping when it's the right call).
- Base rarity odds: **Common 60% / Uncommon 33% / Rare 7%**. Each draft without a Rare raises the Rare chance by +1.5% (pity). The bonus resets when a Rare appears.
- **Elite:** 1 Keepsake plus a draft with Uncommon or better guaranteed.
- **Boss:** a Rare-only draft.

### 6.3 Shared Threads (examples)
| Thread | Cost | Type | Effect | Tempered |
|---|---|---|---|---|
| **Silk Lash** | 2 | Strike | Whip forward 3 tiles for 18 damage. | 26 damage, 4 tiles. |
| **Gossamer Step** | 1 | Weave | Instant short blink in input direction (2.5 tiles). Passes through attacks. | Refunds 1 silk if you pass through an enemy. |
| **Cocoon** | 3 | Ward | Gain Ward 1. | Ward 2. |
| **Spool Burst** | 3 | Strike | Radial burst, 15 damage to all enemies within 2.5 tiles. | 22 damage, knocks back. |
| **Tether Pull** | 2 | Weave | Fire a strand; pulls you to terrain or pulls light enemies to you. | Pulled enemies are Exposed. |
| **Thornlash** | 2 | Strike | Whip that grows a temporary vine platform where it hits (3 s). | Platform lasts 6 s and damages enemies who touch it. |
| **Darning Needle** | 4 | Strike | Piercing thrust across the screen, 40 damage. | Cost 3. |

### 6.4 Snags (curses)
| Snag | Effect while it is the front Thread |
|---|---|
| **Tangle** | Does nothing. Must be Frayed past. |
| **Heavy Knot** | –20% move speed. |
| **Fraying** | Lose 1 silk every 3 s. |
| **Moth-Eaten** | When Frayed past, take 1 pip of damage. (Rare, from risky events.) |

### 6.5 Embroidery (applied to one Thread)
| Embroidery | Effect |
|---|---|
| **Barbed** | Hits apply Bleed. |
| **Echoing** | Fires twice, the second at 50% power. |
| **Anchored** | Using it resets your dash and air-jump. |
| **Gilded** | +1 bead per enemy killed by it. |
| **Thrifty** | –1 silk cost (minimum 1). |

### 6.6 Wish Threads (quests)
Wish Threads start weak and transform when their condition is met during the run.
- **Seedling Strand** (1, Strike, 6 dmg): *Pogo 30 times* → becomes **Canopy Strand** (3 dmg vines rain from above, 4 s).
- **Beggar's Bead** (0, Weave, nothing): *Spend 300 beads* → becomes **Merchant's Thread** (+50% beads from all sources).

---

## 7. Keepsakes

Passive items. Most of a build's identity comes from these.

| Rarity | Source | Design intent |
|---|---|---|
| Common | Elites, shops, caches | Small, broadly useful. |
| Uncommon | Elites, shops, caches | Build-defining hooks. |
| Rare | Elites (lower odds), caches | Strong engines. |
| Boss | Boss rewards (choose 1 of 3) | Big upside with a meaningful drawback. |
| Ancient | Ancient blessings | Run-defining. |

### Examples
| Keepsake | Rarity | Effect |
|---|---|---|
| **Bramble Thimble** | Common | Pogoing an enemy deals +10 damage. |
| **Lacquered Shell** | Common | The first hit you take in each chamber deals 0 damage. |
| **Weaver's Ring** | Uncommon | Every 3rd pogo restores 1 silk. |
| **Shuttle Charm** | Uncommon | Fray costs 0 silk, but has a 1 s cooldown. |
| **Loom Weight** | Uncommon | If your Spindle has 5 or fewer Threads, Threads cost 1 less silk. |
| **Platform Pin** | Uncommon | Landing on a platform you created restores 1 silk. |
| **Moth Lantern** | Rare | Killing an enemy with a Silk Skill heals 1 pip (once per chamber). |
| **Endless Skein** | Rare | Every 10 Threads fired, the next one is free and Echoing. |
| **Gilded Spool** (Boss) | Boss | +3 max silk. Bind costs 9 silk instead of 6. |
| **Crown of Pins** (Boss) | Boss | +40% needle damage. You can no longer Bind; heal only at benches. |
| **Iron Bobbin** (Boss) | Boss | Your Spindle preview grows to 5. Drafts offer 2 Threads instead of 3. |

---

## 8. Vials

One-shot consumables. The belt holds 3 to start. Vials drop from Arenas (25% chance) and are sold at merchants.

| Vial | Effect |
|---|---|
| **Sap Vial** | Heal 2 pips instantly. |
| **Silk Draught** | Fill silk to max. |
| **Ember Flask** | Thrown. Explodes for 40 damage in a 2-tile radius. |
| **Frost Phial** | Thrown. Applies Rime 10 to enemies in an area. |
| **Spinner's Tonic** | For 8 s, Threads cost 0 silk. |
| **Quickcord** | Draft: reroll the current Thread offer (used at the reward pedestal). |

---

## 9. Climbers

Each Climber has a different moveset tweak, starting health, a starting Spindle, a starting Keepsake and a unique mechanic.

### 9.1 Roster overview
| Climber | Archetype | Pips | Unique mechanic | Difficulty | Phase |
|---|---|---|---|---|---|
| **The Wisp** | Speed / venom / thrown pins | 5 | Double dash, Venom stacking | ★★☆ | P1 (first) |
| **The Bulwark** | Heavy / self-damage / sustain | 7 | Blood Price, heavy slam pogo | ★☆☆ | P3 |
| **The Gearling** | Drone orbitals / sequencing | 5 | Drones: Spark / Rime / Hollow | ★★★ | P3 |
| **The Sovereign** | Parry / summoned blade | 5 | Floating blade, Crowns from parries | ★★★ | P4 |
| **The Bonebinder** | Companion / execution | 5 | Knuckle (bone-hand companion), Toll | ★★☆ | P4 |

### 9.2 The Wisp (vertical-slice Climber)
*A moth-winged duellist, fast and fragile, who fights in quick bursts.*
- **Moveset:** double dash in the air; slightly faster run (10 tiles/s); needle range is 0.2 tiles shorter.
- **Unique mechanic: Venom.** Many Wisp Threads apply Venom. A **Venom Burst** Keepsake path lets the player detonate stacks.
- **Starting Spindle:** Pinfan → Silk Lash → Venom Lunge → Pinfan.
- **Starting Keepsake:** **Moth Dust**: dashing through an enemy applies Venom 2.

| Wisp Thread | Cost | Type | Effect |
|---|---|---|---|
| Pinfan | 2 | Strike | Throw 3 pins in a fan, 8 dmg each. |
| Venom Lunge | 2 | Strike | Dash-attack, 12 dmg, Venom 4. |
| Hooked Pin | 2 | Weave | Throw a pin into a wall and swing or zip to it. |
| Smoke Step | 1 | Weave | Dash leaves a cloud. Enemies inside lose track of you for 1.5 s. |
| Needle Rain | 3 | Strike | Leap up and rain 6 pins downward, 6 dmg each. |
| Rot Bloom | 3 | Strike | Detonate all Venom on target: deals stacks × 3 damage. |
| Wingbeat | 2 | Weave | Refresh air dash and jump. Gain 0.5 s i-frames. |
| Thousand Cuts | 4 | Strike | Rare. Blur-dash between up to 5 enemies, 15 dmg each. |

### 9.3 The Bulwark
*An armoured beetle knight who pays in blood for power.*
- **Moveset:** slower run (8 tiles/s); a heavy needle that hits harder (14 base) but recovers slower (12 frames); **Slam Pogo** (downward plunge that damages in a radius on impact).
- **Unique mechanic: Blood Price.** Some Threads cost 1 pip instead of silk. Kills with these Threads give **Ward 1**.
- **Starting Keepsake:** **Scarred Carapace**: killing an Elite heals 2 pips.

### 9.4 The Gearling
*A clockwork mite from the Spire's forgotten workshops.*
- **Unique mechanic: Drones.** Up to 3 drones orbit the player and fire passive effects (Spark: periodic zap; Rime: slows nearby enemies; Hollow: charges up). Many Threads **Launch** the oldest drone, triggering a strong version of its effect. Managing the order of the Spindle *and* the drone queue is the skill ceiling.

### 9.5 The Sovereign
*An exiled royal with a blade that floats at their side.*
- **Unique mechanic: Parry & Crowns.** A **Parry** input with a 6-frame window, at the cost of a short dash cooldown. A successful parry grants a **Crown** (max 5). Crown Threads consume Crowns for finishers. The floating blade auto-attacks the last target the Sovereign struck.

### 9.6 The Bonebinder
*A quiet undertaker bonded to Knuckle, a skeletal hand.*
- **Unique mechanic: Knuckle & Toll.** Knuckle follows the player and can be commanded via Threads: grab and hold an enemy, slam it, catch the player out of a fall (once per chamber), or serve as a pogo point. **Toll** stacks execute enemies at or below the threshold.

---

## 10. Run structure & map

### 10.1 Run flow
1. **Run start:** choose a Climber and a Heights level.
2. **Act 1 opening:** meet the Act 1 **Ancient** and choose 1 of 3 blessings. Then pick an **Act 1 biome door** (Rootwell, up, or Sumpworks, down).
3. **Climb 7 rows** of chambers along the route.
4. **Act boss.** Boss reward: Rare draft, then choose 1 of 3 Boss Keepsakes, then full heal to max (Heights 5+: heal 75%).
5. Repeat for **Act 2** and **Act 3**.
6. **The Crown Loom** (final act: one short ascent chamber, a bench, then the final boss).

### 10.2 Map generation rules (per act)
- Grid: **7 rows × 4 columns**, plus a boss node at the top.
- Generate **4 paths** from row 1 to row 7. Each step moves to an adjacent column (–1, 0, or +1). Paths that land on the same node merge. No paths may cross.
- **Row 1:** always Arena.
- **Row 4:** always Cache (a mid-act treasure).
- **Row 7:** always Bench (before the boss).
- **Elites:** can't appear in rows 1–2. At least 1 and at most 3 per act.
- **Merchant:** at most 2 per act, never in consecutive rows on the same path.
- **No two Benches** in a row on the same path.
- Remaining node weights: Arena 45%, Vignette 25%, Elite 13%, Bench 10%, Merchant 7%.
- **Act 1 only:** at least one path must contain a Merchant (new-player safety, pending decision; see PRD open questions).

### 10.3 Chamber types
| Type | Target time | Description | Reward |
|---|---|---|---|
| **Arena** | 45–75 s | Combat. Doors seal; 2–3 enemy waves. | Thread draft, 12–18 beads, 25% Vial. |
| **Elite** | 60–100 s | One elite enemy (or a punishing gauntlet), sometimes with support enemies. | Keepsake, Uncommon+ draft, 30–40 beads. |
| **Bench** | 10–20 s | A safe room with a woven bench. Choose one: **Rest** (heal 50% max pips, rounded up), **Temper** (upgrade a Thread), or **Unpick** (remove a Thread). | — |
| **Merchant** | 15–40 s | A shopkeeper creature. Sells Threads, Keepsakes and Vials, plus Unpick service. | — |
| **Vignette** | 20–60 s | An event: a short narrative choice, or a traversal challenge with a timer or risk. | Varies. |
| **Cache** | 20–45 s | A treasure room behind a traversal puzzle or secret. | Keepsake (sometimes a choice between two), beads. |
| **Boss** | 120–200 s | Act boss arena. | See §10.1. |

### 10.4 Physical route selection
Each chamber's exits are **doors or shafts that match the outgoing map edges**. Each one shows a glowing **sigil** for the next node type. The player picks a route by going through a door. Most of the time there is no menu.
- The **map overlay** (Tab / View) can be opened at any time, including mid-combat. Opening it **does not pause** the game; it is a quick-look overlay. Pausing shows the full map.
- When an Arena's doors unseal, the door sigils light up.

---

## 11. Chamber design

### 11.1 Principles
1. **Vertical bias.** The run is a climb. Most chambers enter from the bottom or side and exit at the top.
2. **Short and dense.** No traversal longer than ~6 s without a decision (an enemy, a hazard, a branch).
3. **Readable at a glance.** The play space is clear from the first frame on entering. The camera frames the arena whole wherever possible.
4. **One idea per chamber.** Each template is built around one hook (e.g., collapsing platforms, a current, a pogo chain).
5. **Respect the pace.** Arenas seal the doors and spawn enemies immediately. Waves begin within 1 s of entering.

### 11.2 Size guidelines (in tiles; the camera view is ~30 × 17)
| Type | Typical size |
|---|---|
| Arena | 1–1.5 screens (30–45 × 17–25) |
| Elite | 1 screen, fully framed |
| Traversal / Vignette | Up to 1 × 3 screens tall |
| Boss | 1–2 screens, with fixed camera or limited scroll |

### 11.3 Template & variant system
- Each biome has about **40 hand-built chamber templates** at 1.0 (20 for the vertical slice).
- Each template defines **variant layers**: hazard sets, enemy spawn sets (based on act tier and Heights), optional platforms, and horizontal mirroring.
- The run generator picks a template that fits the node type and the entry/exit door configuration, then a variant.
- **Never repeat** the same template twice in one act.

---

## 12. Enemies & intents

### 12.1 Intent glyph system
Every enemy attack is announced by a **glyph** above the enemy, **0.6–0.9 s before it is active** (Act 1). This shrinks to a minimum of 0.4 s in later acts and higher Heights. The glyph is followed by a distinct **telegraph pose** in the animation.

| Glyph | Shape | Colour | Meaning |
|---|---|---|---|
| **Strike** | Fang | Crimson | Melee attack. A double fang means 2-pip damage. |
| **Volley** | Spiral | Ember orange | Projectile(s). |
| **Charge** | Arrowhead | Crimson | Lunging / dashing attack across the arena. |
| **Guard** | Shell | Pale blue | Blocks frontal hits. Attack from behind or above. |
| **Summon** | Egg | Moss green | Will call more enemies. |
| **Empower** | Up chevron | Gold | Buffs itself or allies. |
| **Hex** | Knot | Violet | Applies a debuff or adds a **Snag** to your Spindle. |
| **Unknown** | ? | White | Rare. Some elites hide their intent (a Heights modifier). |

- The shape alone must be readable (the colourblind requirement).
- Each glyph has its own **audio cue** (§23).
- **Bosses** show their next **2–3 intents as a chain** at the top of the screen, so the player can plan whole sequences.

### 12.2 Enemy design rules
- Every enemy has **1–3 attacks** and a clear **weak angle** (e.g., Guard enemies are open from above, which rewards pogo).
- At least half of all enemies should be **pogo-able** in some state.
- Enemies don't deal contact damage while idle, except for "thorned" enemies, which are visually distinct.
- Waves are composed to mix ground and air threats, and melee and ranged.

### 12.3 Act 1 roster (Rootwell) — vertical slice
| Enemy | Role | HP | Attacks / notes |
|---|---|---|---|
| **Burrmite** | Fodder | 20 | Hops toward the player (Strike). Pogo-able. |
| **Lantern Gnat** | Fodder, air | 20 | Hovers and spits a slow seed (Volley). |
| **Thorn Weevil** | Standard | 50 | Guard from the front. Charges when the player is at range. |
| **Vinecaller** | Standard, support | 40 | Summons Burrmites. Flees. Priority target. |
| **Mossback** | Heavy | 110 | Slow. Ground slam with a shockwave (double-fang Strike). The shell is pogo-able. |
| **Sporeling** | Hazard enemy | 30 | Bursts into a lingering spore cloud on death. |
| **Stitchjaw** (Elite) | Elite | 260 | Duellist mantis: Strike → Strike → Charge pattern. Hides its intent on Heights 8+. |
| **The Twinned Husks** (Elite) | Elite | 2 × 140 | Two linked shells. Killing one enrages the other. |

---

## 13. Bosses

### 13.1 Boss design rules
- 2–3 phases. The phase change comes with a brief (≤1.5 s), skippable visual beat. No cutscenes mid-run.
- The **intent chain** is always visible.
- Each boss teaches a skill the next act will test (e.g., pogo chains, air dashing, parry-friendly timing).
- Target fight length: **90–150 s** for an average build.

### 13.2 Act 1 bosses
**The Bramble Matron (Rootwell)** — 800 HP
- *A colossal thorn-bark spider nested in the canopy.*
- Phase 1: Leg Stab (Strike) · Thorn Volley (Volley) · Web Drop (Hex: lays sticky zones).
- Phase 2 (below 50%): the arena floor collapses. The fight moves to vines and a web platform that the player must pogo across. Adds a Summon (Burrmites).
- Lesson: vertical pogo routing and fighting in the air.

**Old Sluicejaw (Sumpworks)** — 850 HP
- *An enormous eel-like grub in a flooded cistern.*
- Pattern: Surface Lunge (Charge) · Gush (Volley, arcs of water) · Undertow (Hex: a current pushes the player toward a hazard).
- Phase 2: the water level rises. Platforms shrink.
- Lesson: managing horizontal space and reading the dash.

### 13.3 Later bosses (outline)
| Act | Biome A boss | Biome B boss |
|---|---|---|
| 2 | **The Brood Regent** (hive queen, summoner) | **The Lamplighter** (market keeper, light/dark arena) |
| 3 | **The Gilded Choir** (three-bodied singing knights) | **The Unspun** (a shapeless silk wraith that copies your Threads) |
| Final | **The Weaver Below the Crown** (the Spire's heart: three phases, reacts to your Spindle) | |

---

## 14. Ancients

At the start of each act, an **Ancient** (a giant dormant creature woven into the Spire's walls) wakes and offers **3 blessings**. The player chooses 1. Each act has a pool of Ancients.

| Ancient | Act | Personality | Example blessings |
|---|---|---|---|
| **Orrowmaw** | 1 | A vast, sleepy grub. Generous but greedy. | +1 max pip · Random Rare Thread · *Start with Tangle (Snag), gain an Elite-tier Keepsake.* |
| **Velith, the Pale Moth** | 1–2 | Cryptic, likes symmetry. | Temper 2 random Threads · Your Spindle can never exceed 6, but all Threads start tempered · +100 beads. |
| **Grandmother Knot** | 2–3 | Stern, tests resolve. | Remove 2 Threads · Choose an Embroidery for any Thread · *Lose 2 max pips; Boss Keepsake choices become 4.* |
| **The Hollow Choir** | 3 | Many voices, unreliable. | Transform your whole Spindle into random Threads of the same rarity · +3 Vial slots · Heal to full and +2 max pips. |

Design rules: one blessing is always "safe," one "synergistic," and one a "gamble" with a drawback.

---

## 15. Acts & biomes

| Act | Biome A | Biome B | Theme |
|---|---|---|---|
| **1** | **The Rootwell**: a vertical overgrown root shaft. Vines, thorns, bioluminescent moss. Climbs **upward**. | **The Sumpworks**: flooded under-galleries. Currents, darkness, swinging lanterns. Descends, then rises. | Learning the climb. |
| **2** | **The Brood Galleries**: a hive with waxy honeycomb, swarms and pulsing walls. | **The Lantern Market**: a vertical bazaar of hanging stalls, light vs. darkness mechanics. | Pressure and crowds. |
| **3** | **The Gilded Reach**: opulent upper halls, golden thread, choirs, falling silk banners. | **The Unspun Wastes**: where the weave has failed: loose threads, voids, gravity anomalies. | Mastery. |
| **Final** | **The Crown Loom**: the top of the Spire, a vast loom over an endless drop. | — | Resolution. |

**Biome choice:** at the end of each act's boss, two exits lead to the next act's two biomes. The sigils on the doors hint at the biome's challenge type.

---

## 16. Economy

### 16.1 Beads (currency)
| Source | Beads |
|---|---|
| Arena | 12–18 |
| Skipping a draft | +8 |
| Elite | 30–40 |
| Boss | 75–90 |
| Cache | 20–60 |
| Enemy drops | 0–2 per kill (Gilded effects increase this) |

### 16.2 Merchant prices
| Item | Price |
|---|---|
| Common Thread | 45–55 |
| Uncommon Thread | 70–85 |
| Rare Thread | 135–160 |
| Common / Uncommon / Rare Keepsake | 130 / 180 / 260 (±10%) |
| Vial | 40–60 |
| Unpick service | 60, +20 for each use this run |

Merchant stock: 5 Threads (at least 1 Shared), 3 Keepsakes, 3 Vials. One random item is discounted 50%.

---

## 17. Meta progression: the Tapestry & Heights

### 17.1 The Tapestry
The Tapestry is a large woven timeline that fills in panel by panel as the player reaches milestones. Each panel unlocks **content** (Climbers, Threads, Keepsakes, Ancients, biome variants) or **lore**, never raw power.

| Example milestone | Unlock |
|---|---|
| Finish your first run (win or lose) | Lore panel: "The First Climber" |
| Defeat an Act 1 boss | 5 new Shared Threads enter the pool |
| Win with The Wisp | The Bulwark |
| Reach Act 3 | Alternate biome: The Sumpworks |
| Use 50 Vials (across runs) | 3 new Vials |
| Defeat the Weaver | Heights unlocked for that Climber |

### 17.2 Heights (difficulty ladder)
Unlocked per Climber by winning. Each level adds a modifier on top of all previous ones.

| Height | Modifier |
|---|---|
| 1 | More Elites on the map. |
| 2 | Standard enemies have +10% HP. |
| 3 | Start with 1 less max pip. |
| 4 | Intent wind-up is 10% shorter. |
| 5 | Boss reward heals 75% instead of 100%. |
| 6 | Start each run with a Tangle Snag. |
| 7 | Elites have +15% HP and an extra attack. |
| 8 | Some elites hide their intent (Unknown glyph). |
| 9 | Merchant prices +15%. |
| 10 | Bosses gain an extra phase-2 attack. |
| 11 | Bench Rest heals 35%. |
| 12 | Hazards deal 2 pips. |
| 13 | Drafts offer 2 Threads instead of 3. |
| 14 | All enemies +15% HP. |
| 15 | Double boss at the end of Act 3. |

---

## 18. World & narrative

### 18.1 Premise
The **Hollow Spire** is a vast tower spun from living silk around an empty core. At its summit, the **Crown Loom** endlessly re-weaves the tower. Every time someone climbs it, the halls, stairs and creatures are re-stitched into new patterns. Countless Climbers have tried to reach the Loom. Their stories are woven into the walls as faded tapestries.

Each Climber climbs for a personal reason, revealed slowly through Tapestry panels, Vignettes and Ancient dialogue:
- **The Wisp** seeks the Loom to unpick their own thread from the Spire's pattern and finally leave.
- **The Bulwark** is the last of an order sworn to guard the Loom, which failed.
- **The Gearling** was built to repair the Loom and still follows its broken orders.
- **The Sovereign** wants to reclaim a throne the Spire wove out of history.
- **The Bonebinder** carries Knuckle, a hand that belonged to someone they lost, to bury it at the top.

### 18.2 Storytelling rules
- **Environmental first.** Tapestries, architecture and enemy behaviour carry the story.
- **Speech is short.** Ancients and merchants speak in 1–3 line bursts that can always be skipped. NPC voices are gibberish vocalisations with subtitles.
- **No mid-run cutscenes** longer than 1.5 s. The story's payoff comes through Tapestry panels between runs.

---

## 19. Art direction (art bible v0)

> **Key focus.** The art is a primary selling point and must hit vertical-slice quality before any other content is scaled up.

### 19.1 Style statement
**Hand-drawn, painterly 2D.** Inked characters with expressive, tapered linework are set against soft, atmospheric painted environments. The world feels **ancient, delicate and hand-made**, like an illuminated manuscript and an embroidered tapestry brought to life. Characters are small against huge vertical spaces, which reinforces the scale of the climb.

**Our own identity: the woven-thread motif.** Hollow Spire must never be mistaken for its inspirations. Everything in the world is stitched, spun or woven:
- Architecture has **seams and stitching** along edges, pillars wrapped in cord, banners and tapestries everywhere.
- Repeating **embroidery patterns** (geometric cross-stitch motifs) are used in UI frames, architecture trims and boss arenas.
- **Golden silk** is the visual thread of the game. It marks interactive objects, rewards and the player's skills.
- Damage and decay are shown as **fraying**: loose threads and unravelling edges.

### 19.2 Character design rules
- **Silhouette first.** Every character and enemy must read in solid black at 64 px tall. Test each design as a silhouette before rendering it.
- **Insect and arthropod inspired**, with clothing and armour made of cloth, wax, chitin and thread. Avoid copying any specific existing character's face design, proportions or costume.
- **Climbers** have a single bright identifying shape: the Wisp's pale wing-cloak edges, the Bulwark's burnished horn, the Gearling's glowing eye-lens, the Sovereign's golden circlet, and the Bonebinder's bone-white Knuckle.
- **Enemies** are darker and lower-saturation than the player. Their **telegraph pose** flashes a rim highlight.
- **Proportions:** player ~2 tiles tall (128 px at 1080p). Fodder 1–1.5 tiles. Heavies 3–4 tiles. Bosses 8–20 tiles.

### 19.3 Linework
- Dark ink outlines (never pure black; tinted to the biome shadow colour).
- **Tapered line weight**: thicker on the outer silhouette and on shadow sides, thinner interior lines.
- Characters and play-layer objects are fully outlined. Backgrounds have **no outlines** (painted edges only). This separation is the core of readability.

### 19.4 Value & contrast hierarchy
| Layer | Value range | Saturation | Detail |
|---|---|---|---|
| Far background | Light (hazy, aerial perspective) | Low | Shapes only |
| Mid / near background | Mid | Low–medium | Painted, soft edges |
| **Play layer** (characters, platforms, hazards) | **Full range, highest contrast** | Medium | Outlined, crisp |
| Foreground silhouettes | Very dark | Low | Blurred slightly, sparse |

**Rule:** at any point on screen, the play layer must have higher local contrast than whatever is behind it. Test with a greyscale overlay in the editor.

### 19.5 Reserved colours
| Use | Colour (indicative) | Rule |
|---|---|---|
| Player accent / silk / rewards | Gold silk `#E8C36A` | Never used for decoration or enemies. |
| Danger (hazards, crimson intents) | Crimson `#C2343F` | Never used for decoration. |
| Heal / silk-gain feedback | Pale white-gold `#FFF3D1` | Only for positive feedback. |

### 19.6 Biome palettes (keys)
| Biome | Key light | Shadow | Accent / mood |
|---|---|---|---|
| Rootwell | Pale green dawn shafts `#B9D9A2` | Deep teal `#1E3B3A` | Bioluminescent moss `#7FE3C1` |
| Sumpworks | Lantern amber `#D99A4E` | Murky indigo `#1A2338` | Water glints `#9FC6D9` |
| Brood Galleries | Honey glow `#E6B04A` | Burnt umber `#3A2116` | Wax cream `#F2E2B6` |
| Lantern Market | Warm paper-lantern `#F0B36B` | Plum `#2C1C33` | Multicolour lantern dots |
| Gilded Reach | Cathedral white-gold `#F4E6C2` | Slate blue `#2B3346` | Gold leaf `#D6A84B` |
| Unspun Wastes | Cold moonlight `#C9D3E6` | Void violet `#15121F` | Loose thread pink `#D98BA6` |
| Crown Loom | Sunrise above clouds `#F7D7A8` | Deep sky `#22304D` | All biome accents return |

### 19.7 Environment construction
- **Parallax layers (minimum):** far BG (0.1x) · mid BG (0.3x) · near BG (0.6x) · **play layer (1.0x)** · foreground (1.2–1.5x).
- **Atmosphere layers:** fog bands, volumetric light shafts (additive sprites), floating motes, falling leaves or threads per biome.
- **Tile + painted hybrid:** the collision geometry is built from tiles, then **dressed with hand-painted overlay sprites** so tile repetition never shows.
- **Asset kits per biome:** about 150–250 painted props/overlays, 30–60 background pieces, and 3–5 painted matte backdrops.

### 19.8 Lighting
- 2D lights with normal maps on large environment pieces (optional) and **rim lighting** on characters from the biome key light.
- Silk effects and the player's Threads use **bloom/glow**, kept subtle.
- Each chamber has one dominant light direction, to keep shading consistent.

### 19.9 VFX
- **Signature effect: silk strands.** Thin, luminous, curving golden lines trail every Silk Skill, Bind and pogo.
- Hit sparks are short (3–5 frames), directional and white-hot at the centre.
- Enemy death: a brief burst of **unravelling threads** and dust, fading in 0.4 s. No corpses linger, to keep the screen clear.
- Keep fullscreen effects to a minimum. Flashes respect the accessibility setting.

### 19.10 Resolution & technical art
- Reference resolution **1920 × 1080**. Art authored at **2x** (3840 × 2160 equivalent) and downsampled.
- Sprite atlases are per biome and per enemy family. Texture memory budget per chamber: ≤ 512 MB VRAM on Steam Deck.
- Must remain readable at **1280 × 800** (Steam Deck). Test every enemy at that size.

### 19.11 UI art
- Hand-drawn, **embroidered frames**: stitched borders, thread-wrapped icons, wax seals for confirmations.
- Icons for Threads are drawn as **spools with an emblem**. Keepsakes are drawn as trinkets on string.
- Fonts: a serif display face for titles, a clean humanist sans for body and tooltips. Both need full CJK coverage.

### 19.12 Art production pipeline
1. Concept thumbnails → silhouette test → colour comp → approval.
2. Characters: rough animation → in-engine timing test → clean-up and colour → final.
3. Environments: blockout (greybox tiles) → paintover concept of the chamber → asset kit → dressing pass → lighting pass.
4. **Art review gate** at the end of each phase. Compare against the vertical-slice "gold standard" chamber.

---

## 20. Animation & game feel

> **Key focus.** The game must feel *fast*: snappy inputs, crisp feedback, no sluggish lockouts.

### 20.1 Animation approach
- **Player and standard enemies:** hand-drawn **frame-by-frame**, played back at an effective **24 fps** (holding frames on 2s at 60 Hz rendering, varied per action for snap).
- **Bosses and very large enemies:** cutout/skeletal rigs with **hand-drawn swap frames** for key poses and impacts.
- **Gameplay is driven by the simulation, not the animation.** Hitboxes and timing are defined in data. Animation frames are synced to them, never the reverse.

### 20.2 Player animation list (The Wisp)
| Animation | Frames | Notes |
|---|---|---|
| Idle | 10 | Subtle cloak breathing loop. |
| Run start / loop / stop | 3 / 8 / 3 | Run start is fast; stop includes a cloak overshoot. |
| Turn | 3 | Must not delay movement; plays on top. |
| Jump rise / apex / fall loop | 3 / 2 / 3 | |
| Land (soft / hard) | 2 / 4 | Hard land after falls over 8 tiles (can be cancelled). |
| Dash | 5 | Strong smear frames. |
| Wall cling / wall jump | 4 loop / 3 | |
| Needle side / up | 6 / 6 | 1 anticipation · 2 active (smear) · 3 recovery. |
| Pogo down-strike | 5 | |
| Silk Skill cast (generic) | 5 | Per-Thread VFX on top. Unique casts for Rares. |
| Bind | 8 | Silk wraps around the body. Gold glow. |
| Hurt | 4 | Strong recoil pose. |
| Death | 14 | Unravels into threads (ties into the restart flow). |
| Bench sit / rise | 6 / 4 | |

Estimated total per Climber: **~120–160 drawn frames** for the base set, plus about 3–6 frames per Rare Thread cast.

### 20.3 Feel parameters
| Event | Hit-stop | Camera shake | Other |
|---|---|---|---|
| Needle hit | 3 frames | none | White flash on the enemy (1 frame), spark |
| Pogo | 3 frames | none | Bounce squash on the player |
| Enemy killed | 5 frames | tiny (0.05 tiles) | Thread-burst VFX |
| Heavy Thread hit | 4 frames | small | |
| Player hurt | 8 frames | small | Desaturation pulse, vignette edge, distinct sound |
| Parry (Sovereign) | 7 frames | small | Gold flash, time-slow 0.15 s at 50% |
| Boss phase change | 10 frames | medium | ≤1.5 s beat |

### 20.4 Responsiveness rules
1. **Input buffer** for attack, jump, dash and Silk Skill: 0.12 s.
2. **Animation never blocks input** for longer than 0.25 s, except for Bind (committed) and Hurt.
3. **Cancels:** needle recovery → dash/jump (from frame 7). Landing → anything. Silk Skill recovery → dash (most Threads).
4. Turning around is instant. Turn animations play on top without delaying the change of direction.
5. **Telegraph minimums for enemies:** Act 1 ≥ 0.35 s wind-up pose, Act 3 ≥ 0.25 s. Intent glyph timing is in §12.1.

---

## 21. Camera
- Smooth follow with **look-ahead** of 2.5 tiles in the movement direction, and 1.5 tiles vertically when falling.
- A **vertical dead zone** of 2 tiles prevents bobbing on small jumps.
- **Room-bounded.** It never shows outside chamber bounds.
- **Arena lock:** when the doors seal, the camera frames the whole arena if it fits, or uses a limited scroll if not.
- **Boss:** zooms out to 90–110%, defined per boss.
- Hold up or down while standing still to look 3 tiles in that direction after 0.4 s.

---

## 22. UI & HUD

### 22.1 HUD layout (in-game)
```
┌───────────────────────────────────────────────────────────┐
│ ◆◆◆◆◇  (health pips)                          ◉ 142 beads │
│ ⟳ silk spool [▮▮▮▮▮▯▯▯▯]                                   │
│ SPINDLE: [Pinfan]  › Lash › Lunge                          │
│ ⚱ vials: ▣ ▣ ▢                                            │
│                                                           │
│                     (play space)                           │
│                                                           │
│                  [boss intent chain, bosses only]          │
└───────────────────────────────────────────────────────────┘
```
- Keepsakes are hidden by default. They show briefly when they trigger, and in full on pause.
- The front Thread is enlarged, with its silk cost shown. It dims when you can't afford it.
- HUD elements are drawn as **embroidered patches** and fade to 60% opacity when not changing.

### 22.2 Key screens
- **Main menu:** a living painting of the Spire base. "Climb" is the default focus. One press from boot to Climber select.
- **Climber select:** Climbers stand around a campfire-like loom. Shows Heights level and Tapestry progress.
- **Pause:** full route map, Spindle (reorderable only at a bench), Keepsakes, glossary, settings.
- **Run summary:** a woven strip showing the route taken, the final Spindle, the killer, and time. **Skip with any button.**

---

## 23. Audio

### 23.1 Music
- **Chamber-orchestral.** Plucked and bowed strings lead, with harp, harpsichord and woodwinds, plus a distinct leitmotif per biome.
- **Adaptive layers per biome:** traversal (sparse), combat (percussive layer added within 0.5 s of the doors sealing), and boss theme (unique per boss, with a phase-2 variation).
- The Crown Loom theme weaves together motifs from every biome.

### 23.2 SFX priorities
1. Player needle hit and miss (crisp, metallic-silk "shink").
2. Player hurt (distinct; must cut through everything).
3. **Intent cues:** each glyph type has a short, unique sound (e.g., Strike = sharp chitter, Volley = rising whistle, Hex = low knot creak).
4. Silk gain, Silk Skill cast, Bind (warm, tonal).
5. Environment and ambience.

### 23.3 Voice
Gibberish vocalisations per character (as in many hand-drawn indies), with subtitles. Climbers have short effort sounds.

---

## 24. Accessibility & assist

| Feature | Details |
|---|---|
| Remapping | Full, per device. |
| Colourblind | Intent glyphs coded by shape. Filters for protanopia, deuteranopia and tritanopia. |
| Screen shake | 0–100% slider. |
| Flashes | Reduce or disable fullscreen flashes. |
| Hit-stop | Full / reduced. |
| Assist: game speed | 70–100%. |
| Assist: extra pips | +1 to +3 max pips. |
| Assist: longer i-frames | +50%. |
| Pogo direction | Down or diagonal. |
| Hold vs. toggle | For Bind and look up/down. |
| Text | UI scale 80–150%, subtitles with background. |

Runs using Assist are tagged on the summary screen and excluded from daily leaderboards. Nothing else is locked.

---

## 25. Death, saves & quick restart

- **Death:** the player unravels (death animation, 0.6 s), then a short summary appears with "Climb Again" focused.
  - **Climb Again** starts a new run with the same Climber and Heights level, controllable in **under 10 s**.
- **Saves:** the run state is saved at every chamber transition. "Save & Quit" resumes at the start of the current chamber.
- **Remnant (Could):** the previous run's death site may appear as a Vignette next run, letting the player recover one Thread from that run by beating an echo of the enemy that killed them.

---

## 26. Co-op (post-launch)

Planned for after 1.0. The architecture should stay co-op-aware.
- 2–4 players, local and online.
- **Silk tether:** players can link. A tethered partner can be swung from or yanked out of pits, and damage is shared across the link.
- Each player has their own Spindle. Shared Threads include co-op effects (e.g., "Bind heals the nearest ally instead").
- Drafts are per player. Keepsakes go to whoever touches them first, with an option to pass.

---

## 27. Content targets

| Content | Vertical slice (P1) | Early Access (P3) | 1.0 (P4) |
|---|---|---|---|
| Climbers | 1 | 3 | 5 |
| Biomes | 1 | 4 (Act 1 A+B, Act 2 A, Act 3 A) + final | 6 + final |
| Chamber templates (per biome) | 20 | 30 | 40 |
| Enemies | 8 | 30 | 55–60 |
| Elites | 2 | 6 | 12 |
| Bosses | 1 | 4 + final | 6 + final |
| Threads | 20 (12 Wisp + 8 shared) | 140 | 75 per Climber + 40 shared |
| Keepsakes | 15 | 70 | 120 |
| Vials | 5 | 15 | 25 |
| Ancients | 1 | 3 | 6 |
| Vignettes | 3 | 25 | 50 |
| Heights | 3 | 10 | 15 |

---

## 28. Open design questions
1. **Spindle preview length:** fixed at 3, or modified per Climber?
2. **Bind cost:** 6 silk for 2 pips, or 9 silk for 3? This needs testing against average silk income per chamber.
3. **Map overlay:** should opening it mid-combat stay unpaused (current proposal) or slow time?
4. **Physical drafting:** do pedestal pickups slow down the experienced player compared to a menu? Option: a "quick draft" menu setting.
5. **True ending:** does reaching the true final boss require something special (e.g., collecting 3 Ancient Keepsakes in one run)?
6. **Hazard respawn:** full 1 pip plus respawn at the last safe ground, or a half-pip system?
7. **Sovereign parry:** a dedicated button, or a dash-into-attack timing?
