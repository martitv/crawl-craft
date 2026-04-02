# PRD: Demo Integration

**GDD Sections**: All (see references below)
**Status**: Draft
**Created**: 2026-04-02
**GitHub Issue**: #5 https://github.com/martitv/crawl-craft/issues/5
**Depends on**: #1 Combat System, #2 Movement System, #3 Player Character, #4 Enemy Design

---

## Problem / Why

Individual system PRDs define what each feature does in isolation. This PRD defines what "done" looks like when all systems are wired together into a single playable demo floor. Without an integration target, individual systems can be complete but the demo remains unplayable.

## Solution Overview

One hand-crafted floor. The player spawns with bare fists, finds a crude weapon early, fights through 5 enemy archetypes in the designed sequence, defeats the Showboater mini-boss to get the Key, and exits the floor. All core systems — movement, combat, Composure, Combo, stats, XP, leveling — are wired and functional. The Audience System is present as a Combo-driven entertainment display only (no full Viewer economy).

## Demo Definition of Done

The demo is complete when a player can:

1. Start a run, distribute 5 starting stat points, spawn on the floor
2. Move freely in isometric top-down view, Dash with Burst Boots
3. Find and equip a crude weapon within the first 30 seconds without combat
4. Encounter and defeat all 5 enemy archetypes in the designed sequence
5. See Masked Behaviour Tags reveal on first trigger for Slugger, Darter, Brute, and Sentinel
6. Encounter the Showboater mini-boss, see `[Crowd Reader]` reveal, and defeat it
7. Pick up the Key, unlock the Floor Exit, and exit the floor
8. See the level-up UI trigger ~5 times during the floor, allocate 3 stat points each time
9. See the Combo/Entertainment display respond to attacks, defensive actions, and breaks
10. Die (HP reaches 0), see Knocked Down state, and return to floor start

## User Stories

- As a player, I want to play a complete floor from start to exit so that I can experience the core game loop
- As a developer, I want all systems communicating correctly so that tuning and iteration can begin

## Vertical Slices

| # | Slice | Description | Acceptance Criteria |
|---|-------|-------------|---------------------|
| 1 | Floor scene | Hand-crafted floor with rooms/corridors in isometric view. Player spawns. Floor Exit exists and is locked. | Scene loads, player spawns, Floor Exit present but locked |
| 2 | Weapon pickup | Crude weapon (crude club or crude knife) available in opening area without combat. Player can equip it. | Weapon item in scene, equip interaction works, bare fists → weapon swap |
| 3 | Enemy spawns in sequence | All 5 archetypes placed on floor in designed sequence. Each group/encounter triggers on player approach. | All enemies present, encounter triggers work, enemies behave per their archetype |
| 4 | Key + Floor Exit | Showboater drops Key on death. Key can be picked up. Floor Exit unlocks when Key is used. | Key drops, pickup works, Floor Exit unlocks, transition triggers |
| 5 | Systems wired | Movement, combat, Composure, Combo, stats, XP, leveling all communicating. Stat changes affect derived values in real time. | Dex increase raises Composure max, Str increase raises damage, XP bar fills, level-up triggers at threshold |
| 6 | UI baseline | HP bar, Composure display (point count), Entertainment display, XP bar, stat screen accessible | All displays present and accurate, no placeholder values |

## Out of Scope

- Procedural floor generation (hand-crafted floor only)
- Full Audience System (Viewers, Followers, Crescendo — not in demo)
- Sponsor System, Between Floors phase, Meta-Progression
- Boon pool content (level-up grants stat points only; Boon choice is stubbed)
- Ranged or magic enemies
- Multiple Boots types beyond Burst (demo uses Burst Boots only)
- Loot drops beyond Key and starting weapon
- Co-op / multiplayer

## Open Questions

- Floor layout: how many rooms? Working target: 6–8 rooms/areas — enough to space the 5 enemy sequences without feeling cramped.
- Starting weapon placement: room adjacent to spawn, no combat required to reach it.
- Level-up Boon stub: show "Boon choice coming soon" placeholder or just auto-grant a fixed Boon? Leaning toward placeholder UI so the flow is established.

## Child PRDs (must be complete before integration)

| # | PRD | Status |
|---|-----|--------|
| [#1](https://github.com/martitv/crawl-craft/issues/1) | Combat System | Draft |
| [#2](https://github.com/martitv/crawl-craft/issues/2) | Movement System | Draft |
| [#3](https://github.com/martitv/crawl-craft/issues/3) | Player Character | Draft |
| [#4](https://github.com/martitv/crawl-craft/issues/4) | Enemy Design (Demo Set) | Draft |
