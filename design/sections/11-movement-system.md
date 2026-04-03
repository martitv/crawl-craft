# Movement System

**Status**: Implemented (Demo)
**Core Fantasy**: Every move is a decision — where you are, how you got there, and what you gave up to do it.
**[← Back to GDD Index](../GDD.md)**

---

### Overview

Movement in Crawl Craft is isometric top-down. The full movement vocabulary is: **walk** and **dash**. No jumping. Floors are authored environments, not platforming spaces.

**Move Direction vs Facing Direction**: the player has two independent direction vectors. **Move Direction** (WASD) controls walking and Dash direction. **Facing Direction** (mouse cursor) controls attack arc and Block arc. These are decoupled — the player can retreat while aiming forward.

The Dash is the single movement verb beyond walking. Its behaviour is entirely defined by the player's equipped Boots — the Boots slot owns the Dash identity. Boons add properties on top of the Boots type but never replace it.

All Dashes cost Composure. Always. Even traversal outside of combat. This means movement choices carry real economic weight — spending Composure to cross a room leaves less for the fight that follows.

---

### Composure Economy

Dash is not gated by charges or cooldowns. The only limit is Composure. This keeps the economy consistent and unified: all defensive and movement decisions draw from the same pool.

- Composure-only balancing is the starting model. If balancing specific Boots types proves intractable without a separate charge limit, charges may be added — but as a last resort, not by default.
- Dexterity increases Composure max and regen rate, making high-Dexterity builds naturally more mobile.
- High-Composure builds (10+ points, achievable through Dexterity + gear) can Dash more freely while maintaining defensive options. This is a valid build axis, not an edge case.

---

### Dash Types

Boots define the Dash. There are two categories: **Defensive** and **Offensive**. These are not cosmetic distinctions — equipping Offensive Boots fundamentally changes the defensive model.

---

#### Defensive Dashes

Grant i-frames during the dash. The player can use these to avoid incoming hits.

| Boot Type | Composure Cost | Identity |
|-----------|---------------|---------|
| **Burst** | 1 | Short range, reliable i-frames. Implemented as a velocity impulse + tween to zero (0.15s), not an instant teleport — feels smooth and directional. The baseline — readable, forgiving, no edge cases. |
| **Roll** | 1 | Longer i-frame window than Burst, but directional commitment — fixed arc, no mid-dash correction. Rewards reads, punishes panic. |
| **Phase** | 2 | Long-range teleport to a targeted point. I-frames are extremely brief (blink-duration only). The payoff is precision placement, not i-frame safety. |

---

#### Offensive Dashes

Replace the i-frame escape entirely. The Dash becomes an attack or CC. No i-frames. No defensive application.

This is a **conscious build trade**: a player who equips Offensive Boots has chosen to give up their dodge in exchange for offensive output. Their only defensive options are Block and Parry. That is the intended design — not a trap, a choice.

| Boot Type | Composure Cost | Identity |
|-----------|---------------|---------|
| **Stomp** | 2 | Single-target slam. Deals damage and applies Knockdown or heavy Stagger to the target. High CC payoff — costs more because Knockdown is powerful. Best against single targets. |
| **Lunge** | 1 | Long-range gap closer. Deals a small hit. No CC. Budget offensive — i-frame removal is the full cost. Pure aggression tempo. |
| **Kick / Offensive variant** | 1 | Offensive dash that passes through or strikes enemies in a line or area. Exact form TBD — the archetype is "offensive movement that hits multiple targets." Distinct from Lunge (single target gap close) and Stomp (hard CC). |

Offensive Dash cost logic: Stomp costs 2 because Knockdown is a strong CC and must be expensive. Lunge and Kick cost 1 because i-frame removal is their primary cost — they do not get additional CC payoff to offset the risk.

---

### Boons and the Dash

Boons extend Dash behaviour — they never replace or change the base Boots type. A player always knows what their Dash fundamentally is from their Boots slot.

Boon extension examples by type:

- **Roll + "Aftershock"**: the first attack after a Roll deals a bonus shockwave at the landing point. Rewards deliberate roll-into-melee timing.
- **Phase + "Ghost Charge"**: phasing through an enemy leaves a spectral echo on them for 3 seconds; hits in that window splash AOE damage. Turns an escape tool into an offensive setup.
- **Burst + "Momentum Tax"**: the first hit after a Burst deals bonus damage scaling with distance traveled. Creates a deliberate retreat-and-charge rhythm.

The pattern: Boons change *how* the Boots are used, not *what* they are.

---

### Environmental Traversal

Walk + Dash is the complete movement vocabulary. There are no additional traversal verbs (no climbing, no swimming, no vaulting).

Environmental interactables — shelves to push, carts to knock over, fire pits to kick enemies into — are **combat and narrative props**, not movement mechanics. They interact with attack actions and the Combo system, not with the movement system. Full environmental interaction design is a separate topic.

---

### Player Experience

- Early floors: Burst Boots are the natural starting point. Composure feels scarce; every Dash is deliberate.
- Mid-run: Phase or Roll Boots appear as drops. The player feels the identity shift — Phase opens positional play, Roll demands reads.
- Late-run: A Stomp or Lunge build with 8+ Composure is a different game. The player has no escape valve but can stagger and Knockdown enemies faster than they can be threatened. High risk, high aggression, high crowd entertainment.
- Boon accumulation layered on Boots creates a final movement language unique to each run.

---

### Systemic Interactions

- **Composure (Combat System)**: Dash draws from the same Composure pool as Block, Dodge, and Parry. Dashing into a fight with low Composure directly weakens defensive options.
- **Build System / Dexterity**: Dexterity governs Composure max and regen, making it the primary stat for mobile builds regardless of Boots type.
- **Build System / Boons**: Boon pool reads equipped Boots type via Tags and surfaces relevant Dash extension Boons.
- **Enemy Design**: Offensive Dash players face harder encounters against Masked Behaviour enemies that counterattack on approach — they cannot i-frame through the counter and must Block or Parry instead.
- **Boots Slot**: Movement identity lives entirely in the Boots slot. Gloves affect combat interactions; Boots affect movement and traversal.

---

### Edge Cases & Risks

- **Composure drain on traversal**: large floors with many traversal Dashes before combat begins will tax Composure. Floor design must account for this — authored rooms should not force wasteful traversal Dashes.
- **Offensive Boot players at 0 Composure**: no escape option exists. Encounter design should not create unavoidable hit scenarios that exclusively punish Offensive Boot builds. Stagger + Knockdown chaining is particularly dangerous for this archetype.
- **Phase Dash visual legibility**: teleporting past enemies in isometric view requires clear visual language. The blink effect must read instantly as "went there, not here."
- **Composure-only balancing assumption**: if a specific Boots type proves too strong at high Composure values (e.g., unlimited Phase Dashes in a high-Dex build), charges may be added as a targeted fix for that archetype without changing the rest of the system.

---

### Open Questions

- Kick/Offensive variant: exact form TBD (fly-kick, drive-through, horizontal sweep). Design mandate is clear; specifics are implementation work.
- Composure cost for Roll: listed at 1, same as Burst. May need to be 2 if the longer i-frame window proves too strong at high Composure values.
- Phase Dash detection interaction: can Phase Dash bypass High Perception enemies mid-travel? Working assumption: no — High Perception enemies react to destination position, not travel arc. Needs confirmation during enemy design.
- Boon pool depth: full Dash-extension Boon vocabulary is TBD during Boon system design.
