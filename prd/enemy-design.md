# PRD: Enemy Design (Demo Set)

**GDD Section**: [Enemy Design](../design/sections/12-enemy-design.md)
**Status**: Draft
**Created**: 2026-04-02
**GitHub Issue**: #4 https://github.com/martitv/crawl-craft/issues/4

---

## Problem / Why

Without enemies, there is no combat to test, no Combo to build, and no floor to clear. The demo requires a minimum set of enemy archetypes that together teach the core combat system through play — not tooltips. Each enemy must be distinctly readable and force the player to engage with a specific mechanic.

## Solution Overview

Five enemy archetypes plus one mini-boss, sequenced to teach Block, Dodge, Parry, multi-enemy pressure, and synthesis in that order. The Showboater mini-boss introduces the first Audience System interaction: the `[Crowd Reader]` masked tag that escalates when the player's Combo is high.

## User Stories

- As a player, I want enemies to telegraph their behaviour visually so that I can learn to read them without a tutorial
- As a player, I want each enemy type to feel distinct so that I am always solving a different problem
- As a player, I want the mini-boss to feel like a culmination of everything I learned on the floor
- As a viewer, I want the Showboater to acknowledge the crowd so that the broadcast metaphor feels real

## Vertical Slices

| # | Slice | Description | Acceptance Criteria |
|---|-------|-------------|---------------------|
| 1 | Swarm Runner | Small, fast enemy. Appears in groups of 3–5. Individual hit costs 1 Composure to Block. `[Pack Tactics]` tag. | Enemy spawns in groups, moves toward player, attacks, dies. Group pressure drains Composure faster than single enemies. |
| 2 | Slugger | Large enemy, slow wind-up, heavy hit (2–3 Composure to Block). `[Heavy Hitter]` tag. Masked: `[Feint]` — jab-jab-SLAM pattern reveals on first trigger. | Wind-up animation readable, Block cost scales with hit size, Feint pattern triggers and masked tag reveals on first occurrence |
| 3 | Darter | Small, fast, no wind-up. Darts in on positional cue. `[Skirmisher]` tag. Masked: `[Third Strike Grab]` — every 3rd dart is a grab, Parry-only. | Positional tell readable, fast attack, grab triggers on 3rd dart, masked tag reveals, grab is Parry-only |
| 4 | Brute | Steady walk, metronomic attack rhythm, medium hits. `[Relentless]` tag. Masked: `[Lunge]` every 4–5 hits. Second masked: `[Enrages]` below 50% HP. | Never stops moving, consistent rhythm, Lunge triggers at interval, speed increases at 50% HP, both masked tags reveal on first trigger |
| 5 | Sentinel | Armoured, deliberate. `[High Perception]` tag (visible). Masked: `[Counter on Block]` — counters with 5–8 damage if player Blocks. | Counter fires on Block, masked tag reveals on first trigger, High Perception tag visible pre-combat, stealth spells ineffective |
| 6 | Showboater (mini-boss) | Ex-contestant. Three combat phases cycling Slugger/Darter/Brute patterns. Masked: `[Crowd Reader]` — escalates to Phase 3 when player Combo is high. Drops Key on death. | Phase switching functional, Crowd Reader triggers when Combo threshold crossed, masked tag reveals on first escalation, Key drops on death |

## Design Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Encounter sequencing | Swarm → Slugger → Darter → Brute → Sentinel → Showboater | Each enemy teaches one mechanic. Sequence protects the learning arc — e.g. Brute before Darter would cause players to try Parrying the Darter and fail badly. |
| Masked Tags reveal once | First trigger only | Teaches through surprise, not repeated punishment. After first reveal, player has the information for all future encounters. |
| Sentinel Counter damage | 5–8 HP | Meaningful punish that communicates "wrong choice." Not a death sentence. |
| Viewer mechanics on bosses only | Yes | Regular enemies teach combat. Audience interactions belong at dramatic stakes — mini-boss and above. |
| Showboater Crowd Reader threshold | Combo-based (TBD exact value) | Forces player to decide: build Combo and race the escalation, or manage Combo for a safer fight. Both valid. |

## Out of Scope

- Enemy loot drops (item system not in demo scope beyond Key)
- Ranged enemies, magic-casting enemies, environmental-interaction enemies (floors 2+ scope)
- Vulnerability/Resistance Tags (identification system not in demo scope)
- Enemy HP exact values (implementation tuning)
- Crowd-sympathy enemy mechanics (reserved for full game, not demo)

## Open Questions

- Exact enemy HP values: need tuning against player HP (50 base) and damage output with bare fists / crude weapon
- Showboater HP: must survive full three-phase arc without becoming a slog — tuning target
- Swarm Runner group size: 3 is readable, 5 is chaotic — start at 3, increase if floor feels too easy
- Slugger feint jabs: 0 damage (pure Composure drain) or minor damage? Intent is Composure pressure — leaning toward 0 damage for clarity
- Brute lunge frequency: every 4–5 hits is the working value — needs tuning against Parry timing window

## GDD Reference

> Enemies in Crawl Craft are authored characters in the broadcast, not obstacle generators. Every enemy has a distinct Behaviour Tag, a visually legible tell, and a specific combat mechanic it forces the player to engage with.
>
> Viewer/Audience mechanics are reserved for bosses and mini-bosses. Regular enemies teach and pressure through combat mechanics alone.
