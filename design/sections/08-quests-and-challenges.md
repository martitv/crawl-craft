# Quests & Challenges

**Status**: In Design
**Core Fantasy**: Every floor has a story the AI wants to tell — and how you engage with it shapes what story you actually get.
**[← Back to GDD Index](../GDD.md)**

---

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
