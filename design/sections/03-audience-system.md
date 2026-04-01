# Audience System

**Status**: In Design
**Core Fantasy**: You are not just fighting to survive — you are performing for a crowd, and the crowd's energy is a resource you can feel.
**[← Back to GDD Index](../GDD.md)**

---

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
