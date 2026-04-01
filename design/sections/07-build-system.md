# Build System

**Status**: In Design
**Core Fantasy**: Who you are is something you become through the choices you make on the way down — and occasionally something absurd happens when the pieces click together.
**[← Back to GDD Index](../GDD.md)**

---

### Overview

The Build System is the mechanical identity layer of Crawl Craft. It governs what the player equips, how they fight, what spells they cast, and how those components interact to produce emergent power fantasies. There is no class selection — identity crystallises from the accumulation of gear slots, boons, spells, and tag synergies across a run.

The system is deliberately legible at the surface but deeply interactive underneath. A new player sees: weapon, tome, gear slots, abilities. An experienced player sees: a web of keyword tags creating unexpected interactions they will describe to their friends.

### Mechanics

---

#### Gear Slots

**Weapon**

- Dedicated gear slot with two configurations:
  - **Two one-handed items** — dual-wield or weapon + off-hand (e.g. sword + dagger, sword + torch, axe + shield)
  - **One two-handed item** — greatsword, staff, launcher, etc.
- Each weapon carries keyword tags that interact with boons, abilities, and other equipped items
- Defines the player's primary attack pattern: melee, ranged, and magic variants are all valid
- Sources: looted from enemies, crafted from floor materials, found in rooms
- Run start: bare fists (no weapon equipped — a deliberate pressure to find or craft something fast)

**Tome**

- A dedicated gear slot — one tome equipped at a time
- Contains the player's active spell loadout for the floor
- Each spell in the tome has a per-floor use count (see Spell System below)
- Rare tomes contain extractable spells — the player can extract a spell into their current tome or into a one-time scroll
- Finding a new tome mid-run is a significant build moment: it may contain better spells, but requires replacing the current tome entirely

**Head**

- Hybrid slot — the item category determines function:
  - Defence-focused (helmet): damage mitigation, resistances
  - EV-focused (stylish hat): EV modifier, Viewer-related bonuses
  - Ability-granting (goggles, visors, etc.): vision abilities, enemy marking, tracking — opens gameplay interactions unavailable through other slots

**Gloves**

- Utility and combat interaction slot
- Alters how the player interacts with combat actions: parry windows, grab mechanics, crafting speed, interaction range
- A mechanically rich slot — small changes here can significantly alter playstyle feel

**Belt**

- Determines the number of quick-cast slots: 2–4 depending on belt tier
- Quick-cast slots allow items (consumables, thrown weapons, one-time effects) to be used instantly in combat
- Items outside quick-cast slots are usable but require a slower inventory retrieve — creating genuine tension around belt management under pressure
- A better belt is a quality-of-life upgrade that also has tactical implications

**Boots**

- Movement and traversal slot
- Alters base movement speed, dash behaviour, jump height
- Can carry combat applications: rocket kick, ground-slam landing, gap-closer attacks
- Tags on boots can interact with ability boons (a dash-tag boot interacts with dash-tag boons)

**Jewelry (Rings and Amulets)**

- Magical abilities and passive effects
- Gated by Magical Affinity (derived from Intelligence + Wisdom stats — see Open Questions)
- Effects are not always known on pickup: discovered through use, or identified via scrolls, NPCs, or shrine interactions
- Accelerated identification is available but not guaranteed — some rings remain mysterious until equipped and used

**Chest and Legs**

- Purely cosmetic and EV-boosting — no mechanical gameplay effects
- Affects character appearance and EV stat only
- Low cognitive load loot: equip the better-looking or higher-EV one and move on
- Design intent: zero decision fatigue — these slots are for expression and broadcast appeal, not build crafting

---

#### Item Taxonomy

**Weapons**

- Any item that deals damage and can be actively used is a weapon
- Looted from enemies, crafted from floor-gathered materials, found in rooms
- All carry keyword tags; tag density and composition define how a weapon interacts with the rest of the build

**Consumables**

- Inventory items with limited quantity
- Used from inventory (slow retrieve in combat) or from quick-cast belt slots (instant use)
- Includes: thrown weapons (grenades, bombs, environmental objects), potions, one-time effect items
- Run start: Floor 1 materials (rocks, sticks) are available for crude weapon crafting or use as thrown consumables

**Scrolls**

- Special consumable sub-type
- One-time use only
- No stat or Magical Affinity requirements — any player can use any scroll
- No charge system — consumed on use, gone
- Sources: floor drops, NPC trades, extracted from rare tomes

**Crafted Items**

- Made from enemy-dropped and floor-gathered materials
- Crafting is available between combat encounters; full crafting system TBD (separate design topic)
- Floor 1 example: rocks + stick → crude club or crude knife. The game should be immediately playable even without finding better loot.

---

#### Spell System

Tome spells are the heavy economic tools of the build — each use is a considered investment. They contrast deliberately with non-spell active abilities.

**Spell Tiers and Charge Counts**

| Tier | Base Charges (per floor) | Overcast cost |
|---|---|---|
| Minor | Many (exact value TBD) | Low flat Viewer cost |
| Major | Few (exact value TBD) | Medium flat Viewer cost |
| Cataclysmic | 1 or 0 base | High flat Viewer cost (painful) |

- Charges reset fully on floor transition — no debt, no carry-over
- When charges hit 0: the spell becomes available to Overcast by spending reserved Viewers

**Overcasting**

- Flat Viewer cost per spell tier — the cost is fixed and readable (e.g., "This spell costs X Viewers to Overcast")
- Cannot Overcast without enough free Viewers to cover the full flat cost. No partial payment. No Overcasting with 3 Viewers on a Cataclysmic spell.
- The minimum Viewer floor for Overcasting is effectively the flat cost itself — deeper floors (more Viewers) enable more Overcasting
- Cost values are tuning targets (TBD); design intent is that Cataclysmic overcast costs should feel genuinely painful but not impossible at depth

---

#### Viewer Reservation

When a spell is Overcast, Viewers are reserved as the economic cost.

**Reservation Priority (when locking)**

Non-Follower Viewers are locked first. If the Overcast cost exceeds available live Viewers, Followers are then locked to cover the remainder.

Example:
- Total Viewcount: 1,000 (500 Followers + 500 live Viewers)
- Overcast cost: 666
- Reserved: 500 live Viewers + 166 Followers = 666 reserved

**Release Priority (at Crescendo)**

When a Crescendo fires and triggers Follower crystallisation:

1. Reserved Followers are released first — restored to Follower status, not counted as new crystallisation
2. Remaining crystallisation capacity from the Crescendo is applied to free live Viewers, converting them into new Followers

Example continuing from above:
- Crescendo fires, crystallisation would convert 300 Viewers into Followers
- Release step 1: 166 reserved Followers released (restored, not new)
- Release step 2: remaining 134 crystallisation capacity converts 134 live Viewers into new Followers
- Net outcome: 166 Followers restored + 134 new Followers

**Other Reservation Rules**

- Full reservation reset on floor transition — no reserved Viewers carry between floors
- UI: Viewer bar uses split colour treatment — free Viewers and reserved Viewers visually distinct at a glance

---

#### Non-Spell Active Abilities

- Sourced from the level-up boon pool (not the Tome)
- Cooldown-based. No charges, no Viewer cost, no reservation
- Lighter and faster than tome spells — spammable within their cooldown window
- The contrast with tome spells (heavy, economic, considered) makes both more interesting. Tome spells feel weighty because active abilities feel free.
- Hoarding instinct eliminated: there is no cost to use, so players use them when they are useful

---

#### Boons

- Umbrella term for any choice-based permanent modifier added during a run
- Sources: level-up pool, Sponsor challenge rewards
- Types within the boon pool:
  - Stat boosts (Strength, Dexterity, Intelligence, Wisdom, Defense, EV, etc.)
  - Passive abilities (always-on effects, often tag-referencing)
  - Active abilities (cooldown-based, non-spell)
  - Rare AI Offers (see The AI section — visually distinct, high-risk, high-EV, rare access to ability tiers unavailable otherwise)
- Boon pool is weighted toward the player's current build: the game reads equipped tags, stats, and Sponsor allegiance to surface coherent offers
- Weighting nudges identity formation without locking the player in — you can always take the unexpected option

---

#### Curses

- Applied to the player character, not enemies (debuffs are enemy-facing; curses are player-facing authored drama)
- Always double-edged: a negative effect paired with a meaningful upside
- Sources: enemy interactions, floor traps, AI punishments for ignoring content, certain rare boons or Sponsor contracts
- Removable via shrines and Sponsor rewards — but the upside may be worth keeping
- Curses are one of the AI's primary tools for adding authored narrative drama to a run

---

#### Synergy Engine (Tag System)

- All game components carry keyword tags: weapons, abilities, gear items, enemies
- Boons reference and create interactions between tags
- Simple two-tag interactions are the baseline; obscure three-or-more-tag interactions are the target "jackpot" experience — the moment players describe their run to someone else
- Build identity emerges from tag density clustering around a theme
- Power Fantasy emerges when tags align unexpectedly — a weapon tag interacting with a boots tag through a boon nobody anticipated
- Tag interactions are discoverable through play, item descriptions, and the AI's flavour text — not front-loaded in a tutorial

### Player Experience

- Early floors: the player picks up whatever is available, making pragmatic choices. Identity is fuzzy.
- Mid-run: a tag pattern begins to emerge. Boon choices start to reinforce it or deliberately subvert it.
- Late-run: a build either crystallises into a coherent power fantasy or becomes an interesting hybrid — both outcomes are valid and legible
- The jackpot moment: a third tag interaction activates and transforms a familiar ability into something unexpected. This is the moment players tell their friends about.
- Viewer Reservation creates a push/pull on the Tome: each Overcast is a bet that the Crescendo payoff will cover the Follower debt. Getting this wrong has consequences; getting it right feels like mastery.

### Systemic Interactions

- Tag system connects every gear slot to the boon pool — no slot is inert to the build
- Viewer Reservation links the Spell System directly to the Audience System; Overcasting is not free, it is a trade against your economy
- Belt tier affects consumable access speed, connecting the Belt slot to the pacing of combat encounters
- Curses connect to the AI mood system — the AI uses them as authored pressure, not random punishment
- Boon pool weighting connects to Sponsor allegiance, meaning Between Floors choices shape what options appear in level-up pools
- Magical Affinity gates jewelry power, creating a meaningful stat tradeoff for builds that want ring effects (Intelligence + Wisdom investment vs. combat stats)

### Edge Cases & Risks

- Tag interactions must be discoverable without being opaque. Players should be able to reason about likely synergies even without knowing exact values.
- Cataclysmic spell Overcast costs must be high enough to feel consequential but not so high that Overcasting never happens at reachable floor depths
- Viewer Reservation release priority (Followers restored first) must be clearly communicated in UI — unintuitive reservation logic that players cannot predict will feel like a bug
- Boon pool weighting should nudge, not railroad. If the game surfaces only on-theme boons, off-theme builds become impossible and emergent complexity collapses
- Chest and Legs loot must not feel like a slot-check on every drop. If magical exceptions are too common, the "low cognitive load" intent breaks.

### Open Questions

- **Magical Affinity**: exact mechanic for Intelligence + Wisdom derivation, affinity thresholds, and brute-force identification unlock rate are TBD. Flagged open — far from locked.
- **Weapon tags**: full tag vocabulary for weapons TBD during combat system design
- **Crafting and gathering**: full crafting system TBD — separate design topic
- **Spell cost tuning**: flat Viewer costs for Minor, Major, and Cataclysmic tiers are TBD — implementation tuning
- **Chest and Legs synergy exceptions**: confirm whether to include occasional magical synergy effects or make these slots purely cosmetic/EV
- **Charge counts**: exact base charges per tier for Minor and Major spells TBD
