# Core Loop

**Status**: In Design
**Core Fantasy**: The thrill of descending deeper into a dungeon that was built to watch you — and playing to the crowd.
**[← Back to GDD Index](../GDD.md)**

---

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
