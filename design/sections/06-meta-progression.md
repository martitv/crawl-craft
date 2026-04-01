# Meta-Progression

**Status**: In Design
**Core Fantasy**: Every run, no matter how short, leaves a mark — and deep runs feel like legacies.
**[← Back to GDD Index](../GDD.md)**

---

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
