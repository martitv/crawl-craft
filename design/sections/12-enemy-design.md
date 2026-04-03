# Enemy Design

**Status**: Implemented (Demo)
**Core Fantasy**: Every enemy is a problem to read — and when you read it correctly in front of a crowd, they feel it.
**[← Back to GDD Index](../GDD.md)**

---

### Overview

Enemies in Crawl Craft are authored characters in the broadcast, not obstacle generators. Every enemy has a distinct Behaviour Tag, a visually legible tell, and a specific combat mechanic it forces the player to engage with. Enemy groupings on a floor are composed by the AI with broadcast intent — pacing, spectacle, and challenge.

Regular enemies teach and pressure through combat mechanics. Audience/Viewer interactions are reserved for bosses and mini-bosses, where the dramatic stakes are high enough to carry them.

### Combat Fundamentals

All melee enemies share these base behaviours:

- **Wind-up Telegraph**: 0.5s yellow flash before a melee attack lands. Gives the player time to Block/Parry.
- **Activation Range**: enemies idle until the player is within 200px.
- **Angle Slot Positioning**: enemies claim unique angles (8 slots) around the player. Prevents clumping. Pack Tactics enemies prefer back-angle slots (flanking).
- **Enemy Stagger**: 1.0s timer with shake visual, auto-recovers. Triggered by Parry or specific abilities.
- **Health Bars**: visible above enemies. Green→red gradient based on HP ratio.
- **Death Animation**: shrink + fade tween (0.3s) before removal.
- **Name + Tag Labels**: display name visible, Behaviour Tags shown. Masked Tags appear on first reveal.

---

### Enemy Tag System

See [Combat System](09-combat-system.md) for the full tag model. Summary:

- **Behaviour Tags** — always visually legible before contact. A flanker moves like a flanker.
- **Vulnerability/Resistance Tags** — hidden by default. Revealed through identification gear, scrolls, or NPCs.
- **Masked Behaviour Tags** — hidden until the first time the behaviour triggers. Designed to teach, not to punish repeatedly.

---

### Base Enemy Archetypes (Demo Set)

Five archetypes for the initial demo floor. Each teaches one core mechanic through pressure, not instruction.

---

#### 1. Swarm Runner
**Behaviour Tag**: `[Pack Tactics]`
**Appears as**: group of 3–5 small, individually weak enemies
**Visual tell**: small, crouched, fast. Always moving toward the player in loose formation.

**What it teaches**: multi-enemy pressure and Combo fundamentals. Each individual hit costs only 1 Composure to Block — but three Swarm Runners hitting in quick succession drains nearly the full base pool. The player learns that Composure is a shared resource across all incoming hits, not a per-enemy budget.

**The mechanic to discover**: staying mobile through the pack and landing hits on multiple targets maintains Combo and generates Viewer spikes (Chain Kill, Simultaneous Kill). Freezing and Block-spamming drains Composure and Staggers.

**Encounter position**: first. Bare fists, loose threat, high energy. Teaches "hitting things builds Combo" before any other system is in play.

**Degenerate strategy**: pick them off one at a time from a distance. Valid — ranged builds have a natural advantage here. Melee builds that learn to move through the pack are rewarded with more spectacular results.

---

#### 2. Slugger
**Behaviour Tag**: `[Heavy Hitter]`
**Appears as**: single large enemy with an oversized weapon (club, sledgehammer)
**Visual tell**: slow wind-up animation, wide stance before attack. The telegraph is long and unmistakable.

**What it teaches**: Block is a resource, not a wall. The Slugger's hit costs 2–3 Composure to Block. A player who Blocks every hit will drain and Stagger before it dies. The lesson: Block selectively, not reflexively.

**The mechanic to discover**: the long wind-up creates an attack window before the hit lands. A player who reads the telegraph, attacks twice, then Blocks the hit is playing optimally. Dodge is also valid — 1 flat Composure versus 2–3 for a Block — and landing behind the Slugger creates a punish window.

**Masked Behaviour Tag**: `[Feint]` — every 3rd attack is a Feint (fast jab, 1 Composure cost). The pattern repeats: hit–hit–feint. Parry becomes appealing on the feint jabs: 1 Composure cost, refunded on success, Composure banked for the next heavy hit. First trigger reveals the tag.

**Encounter position**: second. First solo threat. Forces the player to think about hit cost before any multi-enemy complexity.

---

#### 3. Darter (Ranged)
**Behaviour Tag**: `[Skirmisher]`
**Appears as**: small, fast enemy that circles at range. The first ranged archetype the player encounters.
**Visual tell**: crouched movement, maintains ~120px preferred distance. Retreats after attacking. No wind-up telegraph — fires projectiles without the 0.5s flash that melee enemies use.

**What it teaches**: Dodge timing over Block when projectiles have no telegraph. The Darter fires projectiles at 0.75s cooldown (half normal enemy attack speed). Projectiles are blockable (costs Composure) and parryable (refunds Composure, no enemy stagger). The player needs to read the positional cue (Darter stops retreating and faces the player) and Dodge before the shot, not during it.

**The mechanic to discover**: the positional tell and the ranged pressure pattern. Players who try to Block every projectile drain Composure quickly. Players who close distance force the Darter to retreat, creating windows to attack. Players who learn to Parry projectiles can sustain Composure at range.

**Masked Behaviour Tag**: `[Third Strike Grab]` — every third consecutive attack is a grab that cannot be Blocked or Dodged, only Parried. First trigger reveals the tag. Teaches pattern-counting alongside projectile-reading.

**Encounter position**: third. Introduces Dodge as the correct answer and ranged pressure after the Slugger established Block as expensive.

---

#### 4. Brute
**Behaviour Tag**: `[Relentless]`
**Appears as**: heavy enemy that moves at a measured, steady walk. Never stops. Never flinches.
**Visual tell**: metronomic rhythm — swings at a consistent pace with no variation in timing between hits.

**What it teaches**: Parry as the efficient answer to sustained pressure. The Brute swings medium hits (2 Composure each to Block). At base Composure of 4, the player gets two clean Blocks before danger. The Brute does not pause. Blocking it is viable but expensive. Parrying is the puzzle solution: 1 Composure cost, refunded on success, Brute staggers.

**The mechanic to discover**: the metronomic rhythm is Parry bait. A player who finds the timing rides Composure refunds indefinitely while the Brute stumbles. The moment of discovery — "this exhausting fight is actually a rhythm game" — is the core player experience beat.

**Masked Behaviour Tag**: `[Lunge]` — every 4–5 hits the Brute lunges, closing distance and hitting for 3 Composure cost. Punishes pure kiting. Parrying the regular swings conserves Composure for the lunge Block; Parrying the lunge staggers the Brute hard. First trigger reveals the tag.

**Second Masked Behaviour Tag**: `[Enrages]` — below 50% HP, attack speed increases slightly. The reliable rhythm shifts. First trigger reveals the tag. Lesson: finish it fast rather than dance with it indefinitely.

**Encounter position**: fourth. By this point the player has seen Block (Slugger), Dodge (Darter), and now encounters the enemy where Parry is the efficient answer.

---

#### 5. Sentinel
**Behaviour Tag**: `[High Perception]`
**Masked Behaviour Tag**: `[Counter on Block]`
**Appears as**: heavily armoured enemy. Arms in a guard position. Moves to intercept rather than charge.
**Visual tell**: measured, deliberate movement. No rush — the Sentinel is patient.

**What it teaches**: synthesis. The Sentinel requires combining all three defensive options. It also teaches that some enemies resist stealth entirely (High Perception tag is visible — this enemy cannot be bypassed with Stealth spells).

**The mechanic to discover**: `[Counter on Block]` — if the player Blocks a Sentinel hit, it immediately counters with a fast strike. First trigger reveals the tag. The player now has three decisions each swing: Block and eat the counter (risky), Dodge through (avoids the counter trigger), or Parry (staggers the Sentinel, prevents the counter entirely). Parry is the clean answer — but requires the skill to land it.

**The Combo teach**: the Sentinel moves deliberately with clear attack windows between swings. The Combo-conscious player recognises attack opportunities — but every Block risks a counter that breaks Combo. The Sentinel is the first enemy that makes Combo-preservation a tactical question, not just a consequence of good play.

**Counter damage tuning**: the `[Counter on Block]` hit should deal 5–8 HP damage. Enough to register as a meaningful punish and communicate "that was wrong." Not enough to feel like a death sentence.

**Encounter position**: fifth and final before the mini-boss. Synthesises everything.

---

### Floor 1 Mini-Boss: The Showboater

**Type**: Mini-boss (can drop the Key)
**Behaviour Tags**: `[Pattern Breaker]`
**Masked Behaviour Tag**: `[Crowd Reader]`

The Showboater is an ex-contestant — a dungeon-runner who descended too far and went native. They know the broadcast meta. They play to the crowd. This is the first encounter in Crawl Craft that explicitly acknowledges the audience as a live variable in the fight.

---

**Phase Structure**

The Showboater cycles through three recognisable attack patterns drawn from the base archetypes:

| Phase | Pattern | Teaches |
|-------|---------|---------|
| 1 | Slow, telegraphed heavy hits | Block management (Slugger pattern) |
| 2 | Fast darts with quick retreat | Dodge timing (Darter pattern) |
| 3 | Relentless pressure, no pause | Parry efficiency (Brute pattern) |

Phases do not gate on HP thresholds — the Showboater reads the fight and switches. A player who handles one pattern well will find the Showboater escalating to the next.

---

**Crowd Reader (Masked Behaviour Tag)**

`[Crowd Reader]` reveals the first time the Showboater escalates in direct response to the player maintaining a high Combo.

When the player's Combo is high, the Showboater accelerates to Phase 3 early — it is trying to break the performance. The player's own entertainment output is being used against them.

This creates a genuine strategic decision:
- **Build the Combo and race the escalation** — high risk, high Viewer reward if the Showboater dies before Phase 3 locks in
- **Manage the Combo conservatively** — safer fight, lower Viewer generation, but the Showboater stays in manageable phases longer

Both approaches are valid. Neither is the "correct" answer. The player chooses how they want to perform this fight.

---

**Broadcast Identity**

The Showboater is a foil — another performer competing for the same crowd. The AI has explicitly authored this as a rivalry moment. The flavour text (written in the AI's voice) should make this clear before the fight begins.

When the player wins, they have beaten another broadcaster. Not just cleared an obstacle.

---

### Encounter Sequencing (Floor 1)

The five archetypes should appear in this order to build mechanical knowledge progressively:

```
Swarm Runners → Slugger → Darter → Brute → Sentinel → Showboater (mini-boss)
```

**Why this order matters:**
- Swarm first: teaches Combo before any individual mechanic is introduced
- Slugger before Darter: establishes Block as a resource before Dodge is introduced as the alternative
- Darter before Brute: establishes Dodge before Parry is introduced as the superior answer to sustained pressure
- Brute before Sentinel: Parry must be discovered before the Sentinel punishes not using it
- Sentinel last: only encounters the synthesis enemy after each individual tool is understood

Putting the Brute before the Darter would risk players trying to Parry the Darter and failing badly — sequence protects the learning arc.

---

### Design Principles for Enemy Authoring

- **Visual legibility is non-negotiable.** Behaviour Tags must be readable before contact. A flanker moves like a flanker. A charger telegraphs its charge. If the tell requires gear or scrolls to read, it is a Vulnerability/Resistance Tag or a Masked Behaviour Tag — not a Behaviour Tag.
- **Masked Tags teach, not punish.** The first trigger of a Masked Behaviour Tag should be survivable and informative. After the reveal, the player has earned the knowledge.
- **Viewer/Audience mechanics belong on bosses.** Regular enemies teach combat through combat. The broadcast layer is reserved for encounters where the dramatic stakes match the complexity.
- **Enemy groupings are authored, not random.** The AI composes groups with pacing and spectacle in mind. A Sentinel placed adjacent to a Swarm pack is a deliberate design decision, not a random spawn.

---

### Systemic Interactions

- **Combat System**: all enemy Behaviour Tags interact directly with Block, Dodge, Parry, and Composure. Enemy design IS combat system tuning.
- **Audience System**: spectacular kill methods against any enemy generate Viewer spikes (Overkill, Chain Kill, Simultaneous Kill). Regular enemies create Combo opportunities; the broadcast layer rewards capitalising on them.
- **Build System**: Vulnerability/Resistance Tags on enemies create hidden interactions with player gear and spell Tags — the discovery layer of the build system.
- **Quests & Challenges**: some Challenges are enemy-condition-based ("kill 5 enemies without breaking Combo"). Enemy design must produce encounters where these conditions are achievable and interesting.

---

### Open Questions

- Exact HP values for each archetype — needs tuning against player HP (50 base) and stat model.
- Showboater HP — mini-boss needs to survive the full three-phase arc without being a slog. TBD.
- How many Swarm Runners appear in the opening pack? 3 is readable; 5 is chaotic. TBD through playtesting.
- Do Slugger feint jabs deal 0 damage (pure Composure drain) or minor damage? Intent is Composure pressure, not HP threat.
- Brute lunge frequency: every 4–5 hits is the working value. Needs tuning against Parry timing.
- Additional enemy archetypes for floors 2+: ranged enemies, magic-casting enemies, enemies that interact with the environment. TBD — out of scope for demo.
