# Player Character

**Status**: Implemented (Demo)
**Core Fantasy**: You did not choose who to be — you became someone through what you did.
**[← Back to GDD Index](../GDD.md)**

---

### Overview

The player character begins as a blank slate contestant dropped into the dungeon. There is no class selection, no backstory screen, no archetype picker. Identity is constructed entirely through play: the items you equip, the Sponsors you align with, the level-up choices you make, and how deep you get.

---

### Base Stats

Five distributable stats. All start at **1**. The player distributes **5 free points** at run start — a soft loadout decision, not a class selection.

| Stat | Role | Visual Effect |
|------|------|---------------|
| **Strength** | Damage multiplier on weapons, abilities, and attacks | Character becomes physically larger and bulkier |
| **Dexterity** | Composure max and regen rate | Character becomes leaner and more agile-looking |
| **Intelligence** | Contributes to Magical Affinity (with Wisdom); accelerates jewelry identification | Head grows larger |
| **Wisdom** | Contributes to Magical Affinity (with Intelligence) | Beard grows longer |
| **Charisma** | Foundation of Entertainment Value (EV) | More expressive animations, showmanship (exact visual TBD) |

Stats are **multipliers** — they scale the flat values provided by weapons, items, and abilities. A weapon's base damage is flat; Strength multiplies it. A spell's base EV output is flat; Charisma multiplies it.

**Armor** and **Resistance** are not stats. They are derived from items, Boons, and buffs only.

---

### Entertainment Value (EV)

EV is a derived accumulation, not a direct stat:

```
EV = f(Charisma) + gear EV ratings + Boon EV modifiers + active buffs
```

EV is then multiplied by the player's actions to generate Viewers:

```
Viewer generation = EV × action multiplier
```

Action multipliers vary: overkill, chain kill, simultaneous kill, Parry, high-Combo continuation, and spectacular moments each carry their own multiplier. A weapon with a high EV multiplier is marginal on a low-Charisma build and powerful on a high-Charisma build.

---

### HP

- **Base HP**: 50
- **HP per level**: +5
- HP scales only with character level, not with any stat. This keeps damage tuning predictable across all build types — a tanky player and a fragile player differ in mitigation and Composure, not in HP pool.
- **No passive HP regen.** HP regeneration is a luxury — sourced from specific gear, Boons, or consumables. It is deliberately rare and never a default.

---

### Composure

- **Base Composure**: 4 points
- **Scales with Dexterity**: +1 max Composure per Dex above 1. Regen rate also scales with Dex.
- Passive regen: 1 point per 2.0s (base). Always active.
- **Composure floor**: Composure is clamped to 0 minimum — it can never go negative.

**Visual feedback**:
- **Player Stagger**: shake effect (±2px oscillation) — matches enemy stagger visual.
- **Knocked Down**: sprite flips (rotation = PI) to indicate death state.

---

### Armor & Resistance

Not stats — always item/Boon/buff-sourced.

- **Armor**: reduces incoming physical damage. Diminishing returns model: `mitigation = Armor / (Armor + 100)`. Maximum effective cap: **50% physical damage reduction**. Never reachable trivially.
- **Resistance**: reduces incoming magical damage. Same formula and cap: **50% magical damage reduction**.
- Combined against magic: Armor applies at half effectiveness on magical damage (25% max from Armor alone), Resistance applies fully (50% max). Together: **75% maximum magical mitigation** — an extreme build outcome, not expected from normal play.

---

### Leveling

- **XP sources**: kills, quest completions, challenges, exploration, gathering, crafting. Bypass builds are not locked out.
- **Level-ups per floor**: approximately 5 on average for early floors. Each level-up presents a Boon pool choice and grants **3 free stat points** to distribute across any of the 5 base stats.
- **First level-up timing**: roughly 60% through the floor — before the floor boss, so the boss encounter is shaped by at least one Boon choice.
- Exact XP thresholds are implementation tuning targets.

---

### Starting Equipment

- Bare fists at run start. No weapon equipped.
- Floor 1 always has weapons accessible without combat — rocks, sticks, crude craftable weapons in the opening area. The bare-fists pressure is brief and intentional; the player should feel the need to arm themselves immediately.

---

### Visual Identity

- Single canonical character design for initial release. Visual variety comes from equipped items and stat-driven appearance changes, not character selection.
- Equipped items are visible on the character model.
- Character behaviourally reacts to Viewer count: taunts and crowd-plays at high Viewer counts, defensive and head-down at low counts. Real-time Audience System feedback without requiring a UI check.
- No scripted voice lines — all personality is emergent from build and choices.
- Charisma visual effect TBD (working direction: more expressive idle animations, showmanship gestures at high values).

---

### Player Experience

- The 5 starting stat points are the only pre-run decision. They frame an opening direction without locking the player into a class.
- A player who puts all 5 into Charisma arrives on floor 1 with no combat investment — the dungeon immediately communicates that this is a high-risk broadcast build.
- Players who align with a particular Sponsor across multiple floors will feel their character adopt that Sponsor's playstyle flavour.
- The character's crowd reactions provide real-time feedback on Viewer count.

---

### Systemic Interactions

- **Audience System**: Charisma → EV → Viewer generation. The stat directly drives the broadcast economy.
- **Combat System**: Dexterity → Composure. Strength → damage output.
- **Build System**: Magical Affinity (Intelligence + Wisdom) gates jewelry effects. Armor and Resistance come exclusively from the gear and Boon systems.
- **Movement System**: Dexterity affects Composure, which gates both defensive actions and Dash frequency.

---

### Edge Cases & Risks

- The 5 starting stat points must not feel like a hidden class selection. If one distribution is clearly optimal, the blank-slate intent collapses. Enemy design and floor 1 tuning must ensure multiple opening distributions are all viable.
- HP not scaling with any stat means the damage model is entirely in enemy tuning. This is a feature (predictable targets) but requires disciplined encounter design at every floor depth.
- Bare-fists start requires a very close first weapon opportunity. If the first weapon is gated behind a combat encounter, new players may take HP damage before they feel equipped to fight.

---

### Open Questions

- Charisma visual effect: exact animation/appearance change at high Charisma values TBD.
- Do Sponsor allegiances have visual effects on the character (costume changes, aura effects)?
- Is there any form of persistent character identity across runs (a name, a record, a broadcast history)?
- Exact Dexterity → Composure scaling formula (e.g. +1 max Composure per 2 Dex above base, +X regen per point) — implementation tuning.
