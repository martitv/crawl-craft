# Crawl Craft — Game Design Document

> Living document. Sections grow organically as the game is designed.
> Status tags: `Idea` → `In Design` → `Approved` → `Implemented`

---

## Game Overview

**Status**: Approved

### Premise

Crawl Craft is a 2D/isometric dungeon crawl RPG inspired by the Dungeon Crawler Carl book series. Players descend procedurally generated dungeon floors, fighting enemies, completing challenges, and managing a live audience — because everything in this dungeon is a broadcast.

The player is not a hero exploring a dungeon. They are a contestant performing in one. The dungeon was designed and is actively watched by "the AI" — a ratings-obsessed, artistically prideful entity that built every floor as a piece of entertainment and takes the quality of your run personally.

### Platform & Engine

Godot 4. Design-first, indie scope.

### Core Pillars

1. **The Dungeon is a Show** — every system bends toward the broadcast metaphor. Kills are performances. Loot is sponsorship. Progression is viewership.
2. **Audience as Economy** — Viewers and Followers are the game's primary economic layer, sitting alongside combat stats as first-class resources.
3. **The AI as Auteur** — the dungeon's designer is a character with opinions. Player behaviour shapes its mood, which shapes the dungeon.
4. **Multiplayer as Event** — 1–4 player co-op for standard floors; open-queue Mega Bosses that pull in strangers and feel like live events.
5. **Build Identity through Play** — no class selection at start. Who you are emerges from the choices you make descending.

### Multiplayer

- Standard floors: 1–4 player co-op party
- Mega Bosses: open queue alert system that attracts or requires larger groups; these are shared world events, not private instances
- Post-Boss Social Rooms: shared spaces after Mega Boss kills where strangers can meet, trade, duel, and recruit

---

## Core Loop

**Status**: In Design
**Core Fantasy**: The thrill of descending deeper into a dungeon that was built to watch you — and playing to the crowd.

### Overview

Each floor is a self-contained act in the broadcast. The player explores, fights, and performs. At the end, a safe transition phase provides breathing room before the next act begins. Death is permanent (with a single chance at reprieve), which gives every floor genuine stakes.

### Mechanics

**On a Floor**

- Explore a procedurally generated floor
- Fight enemies; spectacular kill methods (overkills, chains, simultaneous) generate Viewer spikes
- Complete optional quests and challenges seeded by the AI for that floor
- Find and unlock the Key to open the floor exit
  - The Key is always present on the floor, but its placement varies: hidden, guarded by enemies, locked behind an objective, or dropped by a mini-boss
  - Creative Key placement is one of the AI's expressions of floor authorship
- Optional boss encounters exist on floors; smaller bosses are solo/party content

**Death**

- First time downed: enter a Knocked Down state — a brief window where Followers can be spent to self-revive
- In co-op: teammates have a 30-second window to reach and revive a downed player at no Follower cost
- True death (Knocked Down with no revive): run ends, return to floor 1

**Mega Bosses**

- Certain boss encounters trigger an alert broadcast to all players currently in the dungeon
- An open queue fills with players who respond to the alert
- Mega Boss fights are large-scale events, distinct from solo/party bosses in scale and design

### Player Experience

- Each floor should feel like a short episode with a beginning (entry, Sponsor choice), middle (exploration, combat, quests), and end (Key find, boss, exit)
- Players who engage with quests and combat spectacularly are rewarded with Viewer spikes that make the next moments feel electric
- Players who play safely and efficiently get through floors but feel the economic pressure of low Viewership accumulating

### Systemic Interactions

- Viewer count at floor exit influences loot quality on the next floor
- The AI's mood (shaped by floor engagement) adjusts quest frequency and difficulty in subsequent floors
- Follower count gates the self-revive mechanic, creating genuine risk/reward tension around spending Followers

### Edge Cases & Risks

- Key placement must never feel unfair — even hidden Keys need discoverable tells or a fallback timer/reveal mechanic
- The 30-second co-op revive window needs playtesting; too short feels punishing, too long removes stakes

### Open Questions

- How many optional bosses per floor on average, and how does that change at depth?
- Does the Key always appear at floor start, or is it generated mid-exploration?

---

## Audience System

**Status**: In Design
**Core Fantasy**: You are not just fighting to survive — you are performing for a crowd, and the crowd's energy is a resource you can feel.

### Overview

The Audience System is Crawl Craft's central economic identity — the feature that distinguishes it from every other roguelite. Two stats, Viewers and Followers, form a layered economy that sits alongside traditional combat stats and governs loot quality, Director attention, quest intensity, and survivability.

The core formula: **Total Viewcount = Followers + current Viewers**. This mirrors the structure of a weapon's base damage plus active damage buffs — one is the reliable floor, the other is the volatile spike.

### Mechanics

**Entertainment Value (EV)**

- A core build stat, on equal footing with Strength or Defense
- Sources: items carry EV ratings; abilities have EV modifiers; kill methods generate bonus Viewers scaled by the player's EV stat
- High-EV play tends to be slower, flashier, and riskier — crowd-pleasing but tactically demanding
- Low-EV play is efficient, surgical, and quiet — effective in combat but economically lean
- EV is a purely economic stat. It does not affect raw damage output or survivability. It converts spectacular play into Viewers.

**Current Entertainment**

- Distinct from EV: EV is a static build stat; Current Entertainment is the real-time entertainment output the player is actually producing right now
- Calculated as: EV stat × recent actions (kill methods, overkills, chains, quest progress, etc.)
- Current Entertainment sets the "target viewership" the Viewer count asymptotically trends toward
- High EV raises the ceiling of achievable Current Entertainment; moment-to-moment actions determine where within that ceiling the player operates

**Viewers**

- The live, volatile measure of current audience hype
- Spikes on spectacular actions: high-EV kills, overkills, simultaneous kills, chain kills, quest completions, Crescendo moments
- Viewer count follows an asymptotic curve toward the "target viewership" implied by Current Entertainment:
  - Current Entertainment HIGH, Viewers LOW: rapid growth (large gap closing fast)
  - Viewers approaching the expected level for that entertainment output: growth rate falls off
  - Steady entertainment = steady viewership
  - Current Entertainment LOW, Viewers HIGH: rapid drop
- **Lag/grace period**: Viewer count does not respond instantly to entertainment shifts. A brief lag prevents jitter from momentary spikes or lulls, makes Highlight moments meaningful (a big moment has a window of effect), and prevents the system from feeling reactive to every single action.
- Everything that calculates from Total Viewcount benefits from a Viewer spike in the moment it triggers
- A large Viewer spike immediately before a boss fight (e.g., a spectacular kill in the final room) can dramatically affect the boss loot roll

**Followers**

- Crystallised Viewers — the permanent base layer of the economy
- Accumulated exclusively through Crescendo moments: completing a quest, killing a boss, finishing a challenge. At the trigger moment, a portion of current Viewers crystallises permanently into Followers
- Crystallisation rate scales with current Follower count: more Followers = higher % crystallised per Crescendo. The more famous you already are, the better you convert a viral moment into permanent fans.
- Certain events and modifiers (items, Sponsor bonuses, AI buffs) can increase the crystallisation % for specific Crescendo triggers
- Permanent within a run. Mostly permanent across runs — but repeated skipping of quests and challenges causes Follower decay, preventing passive accumulation without engagement
- Followers power the self-revive mechanic: spending Followers on a revive trades long-term economic power for immediate survival

**Total Viewcount**

- The number everything reads from: loot quality tables, AI mood thresholds, quest frequency, challenge intensity
- Total Viewcount = Followers (flat base) + Viewers (current modifier)
- High Followers = stable, reliable floor. High Viewers = volatile spikes that can briefly inflate outcomes dramatically.

**Highlights**

- The game automatically logs spectacular moments as Highlights
- Players can pull up a phone-like Highlights UI mid-run to review their best moments from the current floor and see Highlights from other players running the same floor
- In the post-boss Social Room, a TV object can be interacted with to watch Highlight reels from the fight just completed

### Player Experience

- Players who invest in EV-rated gear feel their combat style shift — flashier, more deliberate, more theatrical
- Watching Viewers tick up in real time after a spectacular kill creates an immediate dopamine feedback loop distinct from standard damage numbers
- The Follower crystallisation at Crescendo moments makes quest completion feel economically weighty, not just optional
- Spending Followers to revive is a genuine dilemma: survival now versus weakened economy for the rest of the run

### Systemic Interactions

- EV stat interacts with item and ability selection: two items with identical combat value may differ significantly in EV, making every gear choice a dual-axis decision
- Viewer decay creates pacing pressure on floors — players cannot sit idle
- Follower permanence connects the Audience System directly to Meta-Progression (Clout calculation) and the revive mechanic
- The AI's mood is gated by Total Viewcount thresholds, making the Audience System the primary driver of the AI's behaviour

### Edge Cases & Risks

- EV must never feel mandatory — a low-EV surgical build should be a valid, interesting choice with clear tradeoffs, not a "wrong" build
- Viewer decay rate needs careful tuning: too fast = constant anxiety; too slow = EV becomes irrelevant
- Follower decay for skipping content needs a grace threshold — skipping one quest should not punish; habitual skipping should

### Open Questions

- Are there items or abilities that let players "hold" Viewer count before a boss (e.g., slow the decay)?
- How is the Highlights UI surfaced to players — automatic popup, or manually accessed?
- What specific tuning parameters govern the lag/grace period on Viewer changes — duration, and does it differ for growth vs. drop?

---

## The AI

**Status**: In Design
**Core Fantasy**: You are being watched by something that has opinions about you — and you can feel it.

### Overview

The AI is the dungeon's architect, broadcaster, and most important NPC. It is never named. It is referred to only as "the AI." Its primary directive is to maximise Total Viewcount across all dungeon broadcasts. Its secondary characteristic is artistic pride — it designed every floor as intentional entertainment, and it responds to how players treat its work.

The AI is not an antagonist. It is more like a demanding showrunner: it wants you to succeed spectacularly, but it will not hide its disdain if you play boringly.

### Mechanics

**Mood States**

The AI's mood is a function of two inputs:
- **Plan adherence**: whether the player is engaging with the floor as the AI designed it — quests attempted, authored content engaged with
- **Entertainment output**: whether the player is producing high Current Entertainment

The two inputs combine into four quadrant states:

| | High Entertainment | Low Entertainment |
|---|---|---|
| **Follows plan** | AI very happy — frequent quests, best AI Offers, warm/excited flavour text | AI slightly frustrated — trying, but boring. Adjusts tone; may reduce AI Offer quality. |
| **Ignores plan** | AI acceptable/neutral — ratings are good, just not artistically satisfying | AI mad — ruining the floor AND boring the audience. Fewer quests, dismissive/terse tone. |

- The AI never softlocks the player or inflicts catastrophic punishment. It adjusts the experience; it does not destroy the run.
- Specific mood thresholds are design intent at this stage; exact values will be tuned during implementation.

**Direct Messages**

- The AI sends sparse direct messages to the player mid-run
- Maximum 1–2 messages per floor
- Triggers: first overkill kill of a run, ignoring a quest past a threshold, hitting a Highlight moment, player death (Knocked Down state)
- Tone: dry, slightly condescending about bad play; genuinely excited about spectacular moments. Never sycophantic.
- All quest flavour text is written in the AI's voice — it is the author of every challenge description, every quest hook, every reward label

**AI Offers**

- Rare injections into the level-up option pool
- Visually distinct from standard level-up options: different border, different colour treatment, description text that carries the AI's unsettling, artistically presumptuous tone
- Properties: higher risk profile, higher EV modifier, occasionally gated access to rare ability tiers unavailable through any other path
- Not always present — their appearance is an event, not a guarantee
- The player can decline an AI Offer; doing so while the AI is already in a Mad state deepens the mood penalty

### Player Experience

- Players who read flavour text will feel the AI's presence accumulating across a run — a consistent voice commenting on their performance
- The moment a player receives their first AI Offer, the AI shifts from background presence to active relationship
- Declining an AI Offer is a meaningful social choice, not just a mechanical one

### Systemic Interactions

- AI mood is gated by Total Viewcount thresholds and engagement behaviours, connecting the AI directly to the Audience System
- AI Offers inject into the level-up pool, connecting the AI to the Between Floors progression system
- Quest frequency (mood-driven) affects Crescendo moment frequency, which affects Follower accumulation rate — the AI's mood has downstream effects on the entire economic stack
- The AI's voice in flavour text is the primary worldbuilding delivery mechanism; it replaces traditional item lore and narrator text

### Edge Cases & Risks

- The AI's tone must walk a careful line: entertaining and characterful without being grating. Players will read this text constantly. It cannot wear out.
- AI Offers that are too obviously correct will always be taken, collapsing the decision. Offers that are too risky will always be declined, making them invisible.
- The "never catastrophically punishes" rule must be strictly maintained in implementation — any system that can softlock or brick a run based on AI mood will be perceived as unfair

### Open Questions

- How many AI Offers can appear in a single run at most? Is there a cap?
- Does the AI have a memory of previous runs (meta-progression awareness), or does it reset each run?
- Is the AI's identity revealed through lore, or does it remain permanently ambiguous?

---

## Between Floors

**Status**: In Design
**Core Fantasy**: A breath of safety between acts — and a moment to make choices that define your next performance.

### Overview

Between Floors is the structured transition phase that separates every floor. It is safe, predictable, and free of AI events or enemies. It serves three functions: stash management and crafting downtime, the Sponsor offer decision for the upcoming floor, and (after Mega Boss kills) the Social Room shared experience.

### Mechanics

**Sponsor System (Floor Entry)**

Immediately upon entering a new floor, the player is presented with 3 Sponsor offers and must choose one. Each offer packages:
- A playstyle framing or challenge for the upcoming floor (e.g., "Kill 10 enemies without taking damage," "Complete the floor in under 4 minutes")
- Associated items or bonuses tied to that floor if the challenge is completed

The Sponsor pool contains:
- Neutral sponsors: broadly applicable challenges with standard rewards
- Build-relevant sponsors: offers that align with the player's current gear and ability loadout — the game reads the build and surfaces synergistic challenges
- AI wildcard (occasional): a risky, high-EV offer injected by the AI — higher potential reward, more demanding or unusual challenge framing, in the AI's voice

Completing a Sponsor challenge on the floor triggers a Crescendo moment (see Audience System), crystallising Viewers into Followers.

**Level-Up System**

On levelling up (triggered by XP thresholds), the player chooses 1 option from a presented pool. The pool contains:
- Stat boosts (Strength, Defense, EV, etc.)
- Passive abilities
- Active abilities
- Rare AI Offers (see The AI section) — visually distinct, not always present

**Post-Boss Social Room**

After a Mega Boss kill, a shared social space becomes available to all participants before the next floor opens:
- **Loot Shrine**: sacrifice carried items for group-wide buffs — a collective decision requiring social coordination
- **Dueling Pit**: optional PvP for unique loot stakes; entirely opt-in
- **Recruitment**: players can invite strangers met in the Social Room into their party for subsequent floors
- **Highlights TV**: a TV object in the room that plays Highlight reels from the Mega Boss fight just completed
- No mechanical time limit on the Social Room; the next floor portal opens when the party is ready

### Player Experience

- The Sponsor choice on floor entry immediately frames the upcoming floor with intent — the player knows what they are trying to do before the door opens
- Level-up moments are quick decisions that accumulate into a distinct build identity across the run
- The Social Room after a Mega Boss is the game's highest-density social moment — a decompression space that rewards lingering

### Systemic Interactions

- Sponsor challenges that complete mid-floor trigger Crescendo moments, linking the Sponsor System directly to Follower accumulation
- AI wildcard Sponsor offers connect the Sponsor System to the AI mood system — taking one pleases the AI; ignoring them repeatedly contributes to Mad state
- Level-up pool composition is shaped by Sponsor allegiances and AI mood, meaning Between Floors decisions in one cycle affect the next cycle's options
- The Social Room Loot Shrine creates a collective EV decision — sacrificing loot for group buffs is a broadcast-friendly spectacle moment

### Edge Cases & Risks

- Build-relevant Sponsor offers require reliable build-reading logic — surfacing irrelevant "synergistic" offers will feel broken and erode trust in the system
- The Loot Shrine must clearly communicate the trade being made before sacrifice — irreversible decisions need legible UI
- Social Room duel consent must be explicit and double-confirmed; accidental PvP in a cooperative context is a trust-breaker

### Open Questions

- How many level-up options are presented per roll? (3 is standard for the genre; does a higher EV stat unlock more options?)
- Is the Sponsor challenge visible during the floor, or must the player remember it?
- Can a player enter a floor without choosing a Sponsor, and if so, what is the penalty or default state?
- What is the design of the Between Floors space itself — a literal corridor, a safe room, a lobby abstraction?

---

## Meta-Progression

**Status**: In Design
**Core Fantasy**: Every run, no matter how short, leaves a mark — and deep runs feel like legacies.

### Overview

Meta-progression in Crawl Craft is built around a single resource: Clout. Clout is earned at the end of every run and spent between runs on permanent upgrades. Its calculation is deliberately structured to reward depth and engagement over farming, ensuring that the optimal path to Clout is playing well and descending far, not dying quickly and repeatedly.

### Mechanics

**Clout**

Earned at run end (death or completion):

```
Clout = Followers × Floor Depth Reached + Highlight Bonus
```

- **Followers** at time of run end is the primary multiplier — rewarding Follower accumulation across the run
- **Floor Depth** is the secondary multiplier — rewarding descent over shallow farming
- **Highlight Bonus**: a flat bonus calculated from the peak Highlight moments logged during the run; rewards spectacular individual moments even in otherwise short runs
- Shallow runs with low Followers = minimal Clout. Deep runs with high Follower counts = substantially more. There is no meaningful incentive to farm early-floor deaths.

**Clout Spending (Permanent Upgrades)**

Clout is spent between runs on permanent unlocks across several categories:
- Base Follower count at run start (reduces the cold-start economic disadvantage of new runs)
- Starting item sets (pre-equipped loadout options that frame the opening build direction)
- Floor 1–3 convenience upgrades (quality-of-life improvements to the early game that do not affect balance at depth)
- Additional unlocks (to be designed — content gates, cosmetics, challenge modes)

### Player Experience

- Players who play spectacularly and die on floor 8 may earn more Clout than players who play boringly and reach floor 12 — the Highlight Bonus rewards quality
- Watching the Clout calculation screen at run end should feel like a box office report: here is what your broadcast earned
- Base Follower upgrades make subsequent runs feel meaningfully warmer from the first floor — not easier, but less economically naked

### Systemic Interactions

- Followers (Audience System) feed directly into the Clout formula, making the Audience System the engine of meta-progression, not just floor-level economy
- Floor depth multiplier creates tension between safe play (survive longer, reach deeper) and spectacular play (maximise Followers, take risks) — both contribute, neither dominates
- Starting item sets (Clout unlock) connect to the Sponsor System — a starting set can pre-establish a build direction that Sponsor offers then reinforce

### Edge Cases & Risks

- The Highlight Bonus must be capped — if a single spectacular early moment can match the Clout of a full deep run, the depth multiplier becomes irrelevant. Placeholder cap set at [TBD]; will be tuned during implementation.
- Base Follower upgrades must not trivialise the Follower economy at depth — they reduce early-game friction, not mid/late-game challenge

### Open Questions

- Is there a Clout cap per run, or is it theoretically unbounded for elite play?
- Are there Clout sinks beyond the initial unlock tree (seasonal content, cosmetics, prestige resets)?
- Does run completion (reaching a final floor) grant a completion bonus multiplier, or is depth continuous?
- What is the shape of the Clout unlock tree — linear, branching, or a grid?

---

## Build System

**Status**: In Design
**Core Fantasy**: Who you are is something you become through the choices you make on the way down — and occasionally something absurd happens when the pieces click together.

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

---

## Quests & Challenges

**Status**: In Design
**Core Fantasy**: Every floor has a story the AI wants to tell — and how you engage with it shapes what story you actually get.

### Overview

Quests and Challenges are the AI's primary tools for authoring the floor experience. Quests are narrative and exploratory — go somewhere, interact with something, engage with the floor's authored content. Challenges are condition-based — they test how you play, not just where you go. Both are authored by the AI (or sourced from Sponsors and NPCs), and both completion trigger Crescendo moments.

The critical design distinction: **the only way to fail a Quest is to not attempt it**. There is no mid-attempt fail state. Once a player engages with a Quest, it will resolve — the only question is how.

### Mechanics

---

#### Quests

- Authored by the AI, written entirely in its voice
- Narrative and exploration tasks: go somewhere, interact with something, experience the floor's authored content
- Structure: a destination or target + a narrative wrapper (context, stakes, flavour text)
- **Fail state**: the only way to fail a Quest is to ignore it entirely — never attempting it. Once attempted, the Quest resolves. There is no mid-attempt failure.
- Source field: tracked in the Quest Journal with metadata (e.g., "AI", "NPC", "Floor Event")
- Completing a Quest = Crescendo trigger → Viewer crystallisation into Followers

---

#### Challenges

Condition-based. "How you play" not "where you go." Event-driven — can appear at scheduled floor moments, as optional modifiers attached to Quests, or as Sponsor-sourced conditions.

Three types:

**1. Standalone Challenge**
- Appears mid-floor as its own event, independent of any Quest
- A skill test, condition window, or behavioural target the player can choose to attempt or ignore
- Completing it = Crescendo trigger; ignoring it = no penalty to Quest state, but missed bonus reward

**2. Attached Challenge**
- A modifier condition layered on top of an existing Quest
- Decoupled from Quest success by default — missing the Challenge bonus loses the bonus reward but does not affect Quest completion or resolution
- Example: "Kill all enemies on this floor without using a Tome spell." Quest succeeds regardless; the Challenge bonus is contingent on the condition.

**3. Narrative Branch**
- A special category of Attached Challenge where the outcome routes the Quest to a different consequence — not a pass/fail gate, but a fork
- Both outcomes fully resolve the Quest. There is no failure path. The outcomes are simply different.
- Example: "Stop the ritual before the summoning completes." Stop it → the demon never spawns; the floor ends with a specific loot outcome. Fail to stop it → the demon spawns; the player must fight or flee, and the floor ends differently. Both are complete resolutions of the Quest.
- Narrative Branches are the AI's deliberate storytelling tool. They are used sparingly and intentionally — not as routine difficulty modifiers. Every Narrative Branch the AI places is a designed fork, not a trap.
- Both Narrative Branch outcomes can trigger their own Crescendo (the resolution moment, not the challenge condition itself)

Source field applies to all Challenge types: "AI", "Sponsor", "NPC", "Floor Event", etc.

---

#### Sponsor Challenges

- Challenges with "Sponsor" as the source field
- Mechanically identical to other Challenges — the source field is what distinguishes them
- Always themed to the sponsored item or playstyle
- Example: Sponsor provides a shrink-ray → Sponsor Challenge: "Collect 10 brains from shrunken enemies."
- Completing the Sponsor Challenge = the primary Crescendo for that Sponsor contract on that floor

---

#### Quest Journal

A unified UI tracking all active Quests and Challenges with source metadata visible.

- Per Quest entry: Quest status (Active / Complete / Ignored) + any attached Challenge status (Active / Completed / Missed)
- Narrative Branch outcomes are logged — the player can see which branch they took and what consequence resulted
- Source metadata visible at a glance for every entry
- Full UI design is a separate topic (layout, surfacing method, in-game placement TBD)

---

### Player Experience

- Entering a floor with a Quest already seeded by the AI creates immediate directional intent — the floor has a story before the player takes a single step
- Encountering a Narrative Branch mid-Quest reframes the Quest as interactive rather than scripted — the player's actions have authorial weight
- Completing a Quest (any outcome) should feel like a chapter ending: a Crescendo fires, the AI has an opinion, the floor's story beat resolves
- Failing to attempt a Quest entirely should feel like leaving the theatre early — the AI noticed, and it will say so

### Systemic Interactions

- Quest completion and Challenge completion = Crescendo triggers → Viewer crystallisation into Followers (Audience System)
- **AI Mood**: attempting Quests (regardless of outcome, including Narrative Branch outcomes) satisfies Plan Adherence. Ignoring Quests entirely is what drives the AI toward Mad state.
- **Viewer spikes**: Challenges especially generate Viewer spikes on completion — the crowd responds to a visible skill test being resolved
- **Narrative Branches** create unique floor states that can alter enemy spawns, room availability, and loot — the floor is materially different depending on which branch was taken
- Sponsor Challenges connect to the Between Floors Sponsor System: the Sponsor offer chosen on floor entry determines what Sponsor Challenge (if any) appears during the floor
- Quest Journal connects to the Highlights system — significant Quest resolutions and Narrative Branch outcomes are loggable as Highlights

### Edge Cases & Risks

- Narrative Branches must not feel like hidden fail states. If players perceive "fail to stop the ritual" as losing, the design intent collapses. Both outcomes must be presented as valid narrative paths, not a pass and a punishment.
- Quest density must be calibrated so the floor never feels like a checklist. If there are too many Quests per floor, engagement feels mandatory rather than authored.
- The "ignore = fail" rule for Quests needs a clear signal to players. If the ignore threshold is invisible, players will accidentally fail Quests without understanding why.
- Sponsor Challenges must feel thematically coherent with the sponsored item — a disconnected challenge breaks the fiction and feels like an arbitrary condition.

### Open Questions

- How many Quests does a typical floor have? How does that number scale with floor depth?
- How many Challenges (Standalone + Attached) per floor on average?
- Can Quests chain across floors — multi-floor narrative arcs with persistent state?
- How does the Quest Journal surface in-game — a pause menu, an always-visible tracker, a phone-like UI consistent with the Highlights system?
- Can Challenges have partial completion states, or are they binary (pass/fail)?
- How is the "ignore threshold" for Quest failure communicated to the player — a timer, a visual indicator, an AI message?

---

## Player Character

**Status**: Idea
**Core Fantasy**: You did not choose who to be — you became someone through what you did.

### Overview

The player character begins as a blank slate contestant dropped into the dungeon. There is no class selection, no backstory screen, no archetype picker. Identity is constructed entirely through play: the items you equip, the Sponsors you align with, the level-up choices you make, and how deep you get.

### Mechanics

- No class selection at run start
- Single canonical character design for initial release — visual variety comes from equipped items, not character selection
- Build identity forms through level-up choices and Sponsor contracts over the course of a run
- Equipped items are visible on the character model
- Stats dynamically affect character appearance, making builds visually readable at a glance:
  - Strength → character becomes physically larger and bulkier
  - Dexterity → character becomes leaner and more agile-looking
  - Intelligence → head grows larger
  - Wisdom → beard grows longer
- Character visually and behaviourally reacts to Viewer count: taunts and crowd-plays at high Viewer counts, defensive and head-down at low counts
- No scripted voice lines — all personality is emergent from build and choices

### Player Experience

- Players who align with a particular Sponsor across multiple floors will feel their character adopt that Sponsor's playstyle flavour
- The character's crowd reactions provide real-time feedback on Viewer count without the player needing to check a UI element

### Systemic Interactions

- Character crowd reactions connect visual feedback to the Audience System
- Sponsor allegiance as identity connects the Sponsor System to the character's perceived personality

### Edge Cases & Risks

- Blank slate starts may feel directionless in early floors — the Sponsor System's floor-entry choice must do the work of giving the player an immediate sense of intent

### Open Questions

- Do Sponsor allegiances have visual effects on the character (costume changes, aura effects)?
- Is there any form of persistent character identity across runs (a name, a record, a broadcast history)?
