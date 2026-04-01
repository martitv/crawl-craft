# Game Overview

**Status**: Approved
**[← Back to GDD Index](../GDD.md)**

---

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
