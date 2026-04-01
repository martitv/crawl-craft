# Game Ideation — Persistent Memory

## Vision & Tone
- Dungeon Crawler Carl as spiritual inspiration: the dungeon is designed entertainment, not a neutral space
- Tone is dry, slightly satirical, broadcast-savvy. Not comedic, but aware of its own absurdity.
- The AI character is the voice of the game's world. All quest text, item descriptions, flavour text flows through it.

## Approved Features
- **Game Overview**: full premise approved. Core pillars locked: dungeon as broadcast, audience as economy, AI as auteur, multiplayer as event, build identity through play.

## Features In Design (key decisions locked)
- **Core Loop**: floor = act structure. Key always present, placement varies. True death with Follower-spend revive. Co-op 30s revive window. Mega Boss open-queue events. Full-run floor count deferred until story is established.
- **Audience System**: EV is an economic stat only — does NOT affect combat damage or survivability. Viewers = volatile. Followers = crystallised at Crescendo moments. Total Viewcount = Followers + Viewers. Follower decay on repeated quest-skipping. Highlights UI (phone) mid-run + TV in Social Room.
  - **EV vs Current Entertainment**: EV is a static build stat. Current Entertainment = EV × recent actions (real-time). Current Entertainment sets the "target viewership" that Viewers asymptotically trend toward.
  - **Viewer curve**: asymptotic toward target (not linear). Large gap = fast movement. Near target = slow movement. Brief lag/grace period prevents jitter and makes Highlights meaningful.
  - **Follower crystallisation**: % of Viewers crystallised at Crescendo scales with current Follower count (more famous = better conversion). Items/Sponsor bonuses/AI buffs can boost % for specific triggers.
- **The AI**: never named. Mood is never catastrophically punishes. Max 1-2 DMs per floor. AI Offers are rare level-up pool injections — visually distinct, high risk/EV, gated rare ability tiers.
  - **AI mood model (locked)**: two inputs — plan adherence + Current Entertainment. Four quadrant states: high entertainment + follows plan = very happy; high entertainment + ignores plan = neutral/acceptable; low entertainment + follows plan = slightly frustrated; low entertainment + ignores plan = mad. Specific thresholds TBD in implementation.
- **Between Floors**: Sponsor System on floor entry (3 offers: neutral / build-relevant / AI wildcard). Level-up pool has AI Offers. Post-Mega Boss Social Room with: Loot Shrine, Dueling Pit, Recruitment, Highlights TV.
- **Meta-Progression**: Clout = Followers × Floor Depth + Highlight Bonus. No early-death farming incentive by design. Spend on: base Followers at run start, starting item sets, F1-3 convenience upgrades. Highlight Bonus cap: placeholder [TBD], tuned in implementation.
- **Player Character**: blank slate, no class selection. Single canonical design for initial release (visual variety from items). Equipped items visible on model. Stats alter appearance: Strength = bulkier, Dexterity = leaner, Intelligence = larger head, Wisdom = longer beard. Visual crowd reactions to Viewer count. No voice lines.

## Design Preferences Expressed
- Emergent complexity preferred over scripted systems
- Broadcast lens is a first-class design filter (how does this look to a viewer?)
- Feasibility respected but not a creativity blocker at GDD stage

## Key Tensions Navigated
- EV stat: decided it is purely economic, not a combat stat. Prevents mandatory feeling.
- Follower decay: only on repeated skipping, not occasional. Grace threshold needed.
- AI mood: adjusts experience, never destroys run. Hard constraint.
- Clout formula: depth multiplier + Follower multiplier prevents shallow-farming. Highlight Bonus rewards quality even in short runs but must be capped.
- Viewer curve: asymptotic chosen over linear — prevents jitter, makes grace period and Highlights meaningful.
- Follower crystallisation scaling: scales with existing Follower count (famous = better conversion), not flat %.
- Player character: single design confirmed for initial release. Stat-driven appearance changes over cosmetic variety.

- **Build System**: full section written. Status: In Design. Key decisions:
  - Gear slots: Weapon (tagged item, not locked slot), Tome (spell loadout), Head (hybrid), Gloves (utility/combat), Belt (2–4 quick-cast slots by tier), Boots (movement/combat), Jewelry (Magical Affinity gated, effects discovered through use), Chest/Legs (cosmetic/EV, low cognitive load)
  - Item taxonomy: Weapons (tagged), Consumables (inventory or quick-cast), Scrolls (no requirements, one-use), Crafted items (materials system TBD)
  - Spell tiers: Minor (many charges), Major (few), Cataclysmic (1 or 0). Charges reset on floor transition.
  - Overcast costs are FLAT per tier. Cannot Overcast without enough free Viewers to cover full cost. No fractional payment.
  - Viewer reservation: lock non-Followers first, then Followers if needed. Release: restore reserved Followers first, then apply remaining crystallisation to new Followers.
  - Non-spell active abilities: cooldown-based, no Viewer cost. Contrast with tome spells (heavy/economic) is intentional.
  - Boons: umbrella for all run-permanent modifiers. Pool weighted toward current build tags/Sponsor — nudges identity, doesn't lock in.
  - Curses: always double-edged (negative + upside). Player-facing, not enemy-facing. AI's authored drama tool.
  - Synergy engine: keyword tags on all components. 3+ tag interactions = jackpot experience target.
  - Magical Affinity: flagged OPEN. Int + Wis derived, thresholds and brute-force unlock TBD.
  - Bare fists = run start weapon. No class selection confirmed.

- **Quests & Challenges**: full section written. Status: In Design. Key decisions locked:
  - Only way to fail a Quest = ignoring it entirely. No mid-attempt fail state.
  - Three Challenge types: Standalone (independent event), Attached (modifier on a Quest, decoupled from Quest success), Narrative Branch (special Attached — routes Quest to different consequence, both outcomes valid, both resolve the Quest).
  - Narrative Branches are AI's deliberate storytelling tool — used sparingly, not as routine difficulty. Example: stop ritual = demon never spawns; fail = demon spawns, fight or flee. Either way, Quest resolves.
  - Sponsor Challenges = Challenges with Sponsor as source field. Completing = primary Crescendo for that Sponsor contract.
  - Both Quest and Challenge completion = Crescendo triggers.
  - AI Mood Plan Adherence: attempting Quests satisfies it. Ignoring entirely is what angers the AI.
  - Quest Journal tracks all active Quests + Challenges with source metadata and Narrative Branch outcome logs. Full UI design TBD.
  - Narrative Branches can alter enemy spawns, room availability, and loot — floor state is materially different by branch taken.

- **Combat System**: full section written. Status: In Design. Key decisions locked:
  - Combat feel arc: Floor 1 = deliberate/Hades-like. Late-run = fluid/Dead Cells momentum earned through progression.
  - Composure: discrete point pool (base 3–5 TBD). Only defensive actions cost it. Attacks always free. Dexterity affects max and regen.
  - Bigger hits cost MORE Composure points to Block (scaling, not flat).
  - Stagger: state entered when Blocking at 0 Composure. Damage still blocked. Player cannot act for a brief window. NOT the same as Knocked Down. A hit landing during Stagger deals HP damage.
  - Three defensive actions: Block (variable Composure cost, full damage negation), Dodge (flat cost, i-frames + movement burst), Parry (flat cost, timing window, negates damage + enemy stagger + Composure refund on success). All three count as Combo hits.
  - Combo: builds on attacks and ALL defensive actions. Breaks only when HP damage is dealt (no defence, or hit during Stagger). Drives Current Entertainment → Viewer generation.
  - Enemy Tags: Behaviour (visible), Vulnerability/Resistance (hidden, revealed by gear/scrolls/NPCs), Masked Behaviour (revealed on first trigger).
  - Floor structure: thematic compositions with varied spatial types (open, corridor, rooms, arenas) — not random tile grids.
  - Bypassing: valid stealth/CC build option. Costs: no XP, no drops, no Viewer Spikes, lower Plan Adherence. Not the optimised path.

## Rejected Ideas
- (none yet)

## Open Questions Flagged in GDD (high priority)
- Viewer lag/grace period tuning parameters
- Whether items/abilities can slow Viewer decay pre-boss
- Highlights UI surface method (auto popup vs manual)
- Full run floor count (deferred — awaiting story establishment)
- AI mood exact transition thresholds (deferred to implementation)
- Whether AI has meta-progression memory across runs
- Sponsor allegiance visual effects on character
- Persistent character identity across runs
- Magical Affinity: Int+Wis derivation, thresholds, brute-force unlock rate (Build System)
- Weapon slot: dedicated slot vs inventory/belt managed (Build System)
- Spell cost flat values per tier (Build System — implementation tuning)
- Chest/Legs: confirm cosmetic-only vs occasional synergy exceptions (Build System)
- Crafting system: full system TBD (separate spar)
- Quests: floor count per floor, cross-floor chaining, ignore threshold UI signal
- Challenges: partial completion states vs binary, count per floor
- Quest Journal: UI surfacing method (pause menu, always-visible tracker, phone UI)
- Combat — Composure point count: working range 3–5, needs tuning
- Combat — Stagger recovery: player-triggered vs time-based TBD
- Combat — Stagger → Knocked Down chaining: unresolved
- Combat — Stealth detection model: full system TBD (separate design topic)
- Combat — Combo multiplier curve: rate and acceleration TBD
- Combat — Block cost scaling map: small/medium/heavy cost values TBD
