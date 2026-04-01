# Between Floors

**Status**: In Design
**Core Fantasy**: A breath of safety between acts — and a moment to make choices that define your next performance.
**[← Back to GDD Index](../GDD.md)**

---

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
