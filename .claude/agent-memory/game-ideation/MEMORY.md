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
