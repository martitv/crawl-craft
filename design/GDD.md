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
