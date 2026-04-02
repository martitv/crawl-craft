# PRD: Player Character

**GDD Section**: [Player Character](../design/sections/10-player-character.md)
**Status**: Draft
**Created**: 2026-04-02
**GitHub Issue**: #3 https://github.com/martitv/crawl-craft/issues/3

---

## Problem / Why

The player character is the foundation everything else runs on. Without defined stats, HP, and a leveling model, no other system can be implemented or tuned. This PRD covers the mechanical baseline — not character art or cosmetics.

## Solution Overview

A blank-slate contestant with 5 distributable base stats (Strength, Dexterity, Intelligence, Wisdom, Charisma). 50 base HP, +5 per level. 4 base Composure, scaled by Dexterity. Stats are multipliers on gear flat values. No class selection — identity emerges through play. Player distributes 5 points at run start and 3 points per level-up.

## User Stories

- As a player, I want to distribute starting stat points so that I have a sense of direction without a class screen
- As a player, I want to level up and get stronger so that descending deeper feels rewarding
- As a player, I want my stats to visibly affect my character so that my build has identity beyond numbers

## Vertical Slices

| # | Slice | Description | Acceptance Criteria |
|---|-------|-------------|---------------------|
| 1 | HP + damage model | Player has 50 HP. Taking unblocked damage reduces HP. Reaching 0 HP triggers Knocked Down. | HP displayed, damage reduces it correctly, Knocked Down state triggers at 0 |
| 2 | Base stats + stat screen | 5 stats exist (Str/Dex/Int/Wis/Cha), all start at 1. Stat screen accessible. Stats affect derived values. | All stats stored, Str scales attack damage, Dex scales Composure max/regen |
| 3 | Starting stat distribution | At run start, player distributes 5 free stat points across any of the 5 stats | Stat allocation UI works, points apply immediately, run starts with chosen distribution |
| 4 | XP + leveling | Player earns XP from kills. Reaching XP threshold triggers level-up. Level-up grants 3 stat points + Boon choice (Boon pool stubbed for demo). HP increases by 5. | XP counter works, level-up triggers at threshold, stat points granted, HP increases |
| 5 | Composure scaling with Dexterity | Dexterity above 1 increases Composure max and passive regen rate | Composure max updates when Dex increases, regen rate scales correctly |

## Design Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| 5 base stats, all start at 1 | Str/Dex/Int/Wis/Cha | Clean baseline. Every Boon point investment is meaningful. EV gear-only. Defense/Resistance from items only. |
| Stats are multipliers | Not flat bonuses | Flat values live on gear. Stats scale them. Keeps gear relevant at all depths and avoids stat-stacking triviality. |
| 5 starting points | Distributed freely at run start | Soft loadout decision without class screen. Can put all 5 in one stat — that is a valid choice. |
| 3 stat points per level-up | Per level, freely distributed | Leveling feels tangible beyond just Boon picks. Player continuously refines their stat identity. |
| HP base 50, +5/level | Flat level scaling only, no stat scaling | Predictable HP targets for enemy damage tuning at every floor depth. Tanky vs fragile builds differ in mitigation, not HP pool. |
| No passive HP regen | Luxury stat, not default | HP regen comes from rare gear/Boons. Forces resource management. |
| ~5 level-ups per floor | Approximate target | Enough progression to feel the build evolving on each floor. First level-up before floor boss. |

## Out of Scope

- Boon pool content (Build System scope — stubbed as placeholder for demo)
- Armor and Resistance values (item-sourced, no items in this PRD scope)
- Character visual appearance changes from stats (art scope, post-demo)
- Intelligence/Wisdom → Magical Affinity (no jewelry in demo scope)
- Charisma → EV calculation (Audience System scope)

## Open Questions

- Exact Dexterity → Composure scaling formula (e.g. +1 max per 2 Dex above base, or linear) — implementation tuning
- XP curve per floor: how much XP per kill to hit ~5 level-ups on a typical floor — implementation tuning
- Knocked Down state: for demo, does Knocked Down just mean death (no Follower revive mechanic yet)? Assumption: yes, Knocked Down = run over for demo.

## GDD Reference

> Five distributable stats. All start at 1. The player distributes 5 free points at run start. Stats are multipliers — they scale the flat values provided by weapons, items, and abilities.
>
> Base HP: 50. HP per level: +5. No passive HP regen. Base Composure: 4 points. Scales with Dexterity. ~5 level-ups per floor average. 3 stat points per level-up.
