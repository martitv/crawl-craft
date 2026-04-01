# The AI

**Status**: In Design
**Core Fantasy**: You are being watched by something that has opinions about you — and you can feel it.
**[← Back to GDD Index](../GDD.md)**

---

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
