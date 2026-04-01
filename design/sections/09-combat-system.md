# Combat System

**Status**: In Design
**Core Fantasy**: Every fight is a performance. You read the enemy, you respond with precision, and when the build clicks the crowd goes insane.
**[← Back to GDD Index](../GDD.md)**

---

### Overview

Combat in Crawl Craft is deliberate and timing-based at its core, with momentum and fluidity as earned rewards from build progression. The player always has something to do — attack freely, and choose from three defensive options that all feed the Combo. Every defensive action is a performance. Taking unblocked HP damage is a failure state, not a neutral outcome.

The broadcast lens is built into the combat loop: the Combo System directly drives Current Entertainment, which drives Viewer generation. A player who reads enemies and responds with precision is not just surviving — they are performing for a crowd.

### Combat Feel

- **Floor 1**: raw and dangerous. Every hit matters. The player is learning the dungeon, reading enemies, and making deliberate defensive choices with limited Composure.
- **Mid-run**: Composure builds expand the defensive toolkit. Boons, gear tags, and stat thresholds start creating systemic interactions. Combat begins to feel authored.
- **Late-run**: fluid, fast, momentum-fuelled. Dead Cells-style power fantasy is earned, not given. The transition from careful to explosive is part of the progression arc.

The primary reference feel is Hades/Dark Souls: commitment in attacks, readable enemy behaviour, meaningful timing windows. The Dead Cells momentum register is the destination, reached through play.

### Composure (Defensive Resource)

Composure is a discrete point pool — not a bar. Base range: 3–5 points (tuning TBD).

- Only defensive actions cost Composure. Attacking is always free.
- Bigger hits cost more Composure points to block (scaling cost, not flat). Small hits cost 1 point; large hits may cost 2 or 3.
- Composure regenerates passively between actions.
- Build items, Boons, and stat thresholds can increase Composure max, accelerate regen rate, or reduce defensive costs.
- Dexterity is the primary stat affecting Composure max and regen rate.

**At 0 Composure — Stagger:**

When the player attempts to Block with 0 Composure remaining, the block still fully negates the incoming damage — but the player enters **Stagger**. Stagger is a brief vulnerability window where the player cannot act. It is not the same as Knocked Down (the pre-death state). It is a dangerous intermediate state.

A Stagger landing in the middle of an enemy attack chain almost always results in the following hit dealing HP damage, which breaks Combo and represents a genuine punish. Using Block as a zero-Composure emergency option is always available — but it is a calculated risk, not a safe fallback.

Stagger is the mechanical cost of reckless defence. The design intent: blocking is never locked out, but spending it carelessly has consequences that can cascade.

### Three Defensive Actions

All three defensive actions cost Composure. All three count as Combo hits — the player is still performing while defending.

---

**1. Block**

- Costs Composure proportional to the incoming hit size (scaling, not flat).
- Fully negates all damage from the incoming hit.
- Counts as a Combo hit.
- At 0 Composure: damage is still fully blocked, but the player enters Stagger.
- Base effect only. Extensible through items, Boons, weapon effects, stat thresholds (e.g., a Boon that causes Block to reflect a small amount of damage; a weapon tag that restores 1 Composure on a clean Block).

---

**2. Dodge**

- Costs flat Composure (1 point, base).
- Grants brief invincibility frames (i-frames) and a movement burst.
- Counts as a Combo hit.
- Base effect only. Extensible through items, Boons, Boots slot effects.

---

**3. Parry**

- Costs flat Composure (1 point, base).
- Requires a precise timing window relative to the incoming hit.
- On success: fully negates damage, applies a small stagger to the attacking enemy, and refunds the Composure spent.
- Counts as a Combo hit.
- Base effect only. Extensible through items, Boons, timing-window wideners, escalating enemy staggers.

---

All three actions are intentionally minimal at base. The design space lives in how items, Boons, potions, weapon tags, and stat thresholds extend each action — not in complexity at the base level.

### Stagger

Stagger is the vulnerability state entered when Blocking at 0 Composure. It is distinct from Knocked Down.

- During Stagger the player cannot perform any action — no attacks, no defensive actions.
- Duration is brief but long enough to matter in a continuing enemy attack chain.
- A hit landing during Stagger deals HP damage directly, since no defensive action is possible.
- HP damage during Stagger breaks Combo (see Combo System).
- Whether Stagger can transition into Knocked Down if sufficient damage lands during the window is an open question.

### Combo System (Performance)

The Combo System is the bridge between combat and the Audience System. A Combo is not just a score — it is the mechanism by which fighting well generates Viewers.

**What builds Combo:**

- Every attack that connects with an enemy counts as a Combo hit.
- Every defensive action — Block, Dodge, Parry — counts as a Combo hit. The player is performing while defending.
- Combo is continuous as long as every incoming hit is handled by a defensive action.

**What breaks Combo:**

- HP damage being dealt to the player. This means: being hit with no defensive action taken, or being hit while in Stagger.
- Block does not break Combo — damage never reaches HP.
- A 0-Composure Block (Stagger) does not break Combo on its own — but the vulnerability window that follows frequently leads to a Combo break on the next hit.

**Why Combo matters:**

- Each Combo hit incrementally raises Current Entertainment.
- Current Entertainment drives Viewer generation — the higher it climbs, the more Viewers trend toward the current target.
- A high-Combo fight creates a Viewer spike. A Combo break resets the Current Entertainment contribution from the Combo (Viewers already gained persist, subject to Viewer Lag).
- Higher Viewers = better loot weighting, more AI attention, stronger Overcast options.

The emotional arc of a great fight: build the Combo, feel Current Entertainment climbing, land the kill — Viewers flood in. Break the Combo from a sloppy hit — feel the crowd drop. This tension is the broadcast loop in microcosm.

### Enemy Design Philosophy

Every enemy has unique behaviour and at least one mechanical trait to play around. Enemies are not stat-padded obstacles — they are authored characters in the broadcast.

**Enemy Tags:**

- **Behaviour Tags** — always visually legible. A flanker moves like a flanker before it flanks. A charger telegraphs its charge. The player can read these before contact.
- **Vulnerability/Resistance Tags** — a hidden layer. Not displayed by default. Revealed through identification gear (e.g., Goggles item slot), identification scrolls, or NPC services. A player who has not identified an enemy does not know their build's tags interact with it.
- **Masked Behaviour Tags** — hidden behaviours that are only revealed the first time that behaviour is triggered (e.g., an enemy that counterattacks on Block reveals that tag the first time it does so).

**Enemy groupings on a floor are authored by the AI** — they are designed encounters, not random spawns from a pool. The AI composes enemy groupings with broadcast intent: pacing, spectacle, and challenge.

### Floor Structure

Floors are thematic compositions, not repeating room grids. A single floor can contain a variety of spatial types within a unified thematic setting.

- Open outdoor spaces
- Corridors
- Interconnected room clusters
- Arena spaces (boss rooms, challenge rooms)

These are not separate biome tiles — they are elements within a single authored floor environment. The spatial structure follows the narrative.

Example: a floor set in an abandoned castle may move through a garden courtyard (open) → outer wall corridor → castle interior (connected rooms) → throne room (arena). The floor structure is the AI's episode staging.

### Encounter Design

Fighting enemies is the default and is rewarded:

- XP and stat progression
- Loot drops
- Viewer Spikes from spectacular combat (overkills, chains, simultaneous kills)
- Plan Adherence contribution (combat is performing)

Bypassing enemies is a valid build option — not the optimised playstyle:

- Stealth builds can slip past enemies below a detection threshold
- CC consumables (sleep bomb, sleep scroll, etc.) can neutralise a group for bypassing
- Bypassed enemies yield: no XP, no drops, no Viewer Spikes, lower Plan Adherence contribution
- If a Quest or Challenge requires kills, bypassing those enemies has narrative consequences: the Quest may be routed to a Narrative Branch outcome, or the Challenge is simply missed

The design intent: combat is not mandatory, but avoiding it has real economic and narrative costs. A stealth build that skips combat is making a trade — not finding a free path.

### Player Experience

- First contact with a new enemy type should feel like reading a problem: "what does this thing do, and how do I play around it?"
- A clean defensive read — Parrying a heavy attack, Dodging through a charge, Blocking a burst — should feel satisfying in isolation, before any build layer is applied.
- The Combo System should make the player feel the crowd reacting in real time. A long unbroken Combo that ends in a spectacular kill is the core broadcast moment of every fight.
- Stagger should feel like a mistake being punished — not a death sentence by itself, but a signal that something went wrong that needs to be recovered from immediately.
- Late-run combat should feel like the player has solved the dungeon's enemy language and is now fluent in it.

### Systemic Interactions

- **Audience System**: Combo directly drives Current Entertainment → Viewer generation. Combat is the primary real-time driver of Viewership within a floor.
- **Build System**: Composure max and regen are modified by Dexterity and by gear/Boons. Weapon tags, Boon synergies, and Belt consumables all extend the three base defensive actions. Enemy Vulnerability Tags interact with gear and spell tags.
- **AI Mood**: spectacular combat (high Combo, Viewer Spikes) drives Current Entertainment up, which satisfies the AI's entertainment axis. Combat engagement also satisfies Plan Adherence.
- **Quests & Challenges**: some Challenges are combat-condition-based (e.g., "complete the floor without breaking Combo"). Kill requirements in Quests connect enemy encounters to narrative resolution.
- **Sponsors**: Sponsor Challenges may require specific combat behaviours (e.g., "kill 5 enemies using a specific tag interaction"). Combat is the primary surface for Sponsor engagement.

### Edge Cases & Risks

- Composure as a discrete point pool (not a bar) must communicate state clearly to the player. A player who does not know their Composure count will be surprised by Stagger. UI design for Composure is critical.
- Stagger must feel punishing but not opaque. Players need to understand they entered it and why. A clear visual/audio state indicator is required.
- The Combo-as-performance system needs to feel rewarding before the Audience System is visible. If the Combo meter only matters because of Viewer math, players who do not understand the Audience System will feel like the Combo is cosmetic. The moment-to-moment feel of maintaining Combo must have its own satisfying feedback.
- Enemy Masked Behaviour Tags require a satisfying reveal mechanic. A surprise counter the player had no way to know about must not feel unfair — the reveal must reframe it as information the player now has for all future encounters with that enemy type.
- Bypass viability: stealth and CC bypass must not become the dominant optimised path at high floors. The economic cost (no XP, no drops, no Viewers) must be substantial enough that a bypass build is a genuine trade-off and not strictly superior.

### Open Questions

- Composure point count: working range 3–5. Needs tuning against encounter design and enemy hit size distribution.
- Does Stagger have a player-triggered recovery action (e.g., a "get up" input that speeds recovery) or is it purely time-based?
- Can Stagger chain into Knocked Down if sufficient damage lands during the Stagger window?
- Stealth system: detection levels confirmed to exist, but the full detection model (visual cones, proximity, sound, alert states) is TBD — separate design topic.
- Combo multiplier curve: how fast does Current Entertainment climb per Combo hit, and does the rate accelerate with Combo count (e.g., multiplier increases every N hits)?
- Does Combo count reset to zero on a break, or does it have decay (partial retention possible with certain Boons)?
- Block cost scaling: what is the cost mapping? (e.g., small hit = 1 point, medium = 2, heavy = 3) — needs tuning against base Composure pool size.
