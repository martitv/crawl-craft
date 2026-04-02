# PRD: Movement System

**GDD Section**: [Movement System](../design/sections/11-movement-system.md)
**Status**: Draft
**Created**: 2026-04-02
**GitHub Issue**: #2 https://github.com/martitv/crawl-craft/issues/2

---

## Problem / Why

Without movement, the player is static. The movement system defines how the player navigates floors, positions in combat, and expresses build identity through Boots. Critically, Dash draws from the same Composure pool as defensive actions — so movement and defence are always in tension.

## Solution Overview

Isometric top-down movement with two verbs: walk and Dash. The Boots slot defines the Dash type. All Dashes cost Composure. Defensive Dashes grant i-frames; Offensive Dashes replace i-frames with an attack or CC effect. Boons extend Dash behaviour on top of the Boots type.

## User Stories

- As a player, I want to move freely around the floor so that I can explore and position in combat
- As a player, I want my Dash to feel distinct based on my Boots so that movement is a meaningful build choice
- As a player, I want Dashing to cost Composure so that I feel the tension between mobility and defensive options
- As a player choosing Offensive Boots, I want my Dash to deal damage or CC so that I consciously trade my dodge escape for offensive power

## Vertical Slices

| # | Slice | Description | Acceptance Criteria |
|---|-------|-------------|---------------------|
| 1 | Basic movement | Player walks in all directions in isometric top-down view | Smooth 8-directional movement, correct isometric perspective |
| 2 | Burst Dash | Default Dash. Costs 1 Composure. Short range, i-frames during animation, movement burst. | Dash input works, i-frames active during dash window, Composure decrements, feels snappy |
| 3 | Composure drain on traversal | All Dashes cost Composure even outside combat. Composure regen always active. | Dashing in an empty room decrements Composure, regen restores it over time |
| 4 | Phase Dash (Boots swap) | Equipping Phase Boots changes Dash to long-range teleport. 2 Composure. Very brief i-frames. | Dash behaviour changes with Boots slot, teleport places player at targeted position, Composure cost is 2 |
| 5 | Stomp Boots (Offensive Dash) | Equipping Stomp Boots replaces Dash with a targeted slam. 2 Composure. Deals damage and applies Knockdown/Stagger. No i-frames. | Dash is now an attack, deals damage, applies CC, no i-frames granted |

## Design Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Walk + Dash only | No jump, no climb | Isometric top-down — verticality creates spatial legibility problems. Simplest vocabulary for demo. |
| All Dash costs Composure | Always, even traversal | Unified resource. Movement decisions have real cost. Dexterity builds feel the benefit of high Composure. |
| Boots own the Dash type | Boots = identity, Boons = extensions | Player always knows what their Dash fundamentally is. Boons add without replacing. |
| Offensive Dash has no i-frames | Pure player choice | Player who equips Offensive Boots consciously trades dodge escape for offensive power. Not a trap — a build decision. |
| Composure-only balancing | No separate charge/cooldown | Simplest model. Add charges only if specific Boots prove unbalanceable without. |

## Out of Scope

- Roll Dash, Lunge Boots (demo uses Burst + Phase + Stomp as the representative set)
- Boon extensions to Dash (Build System scope)
- Environmental traversal interactions (combat/narrative props, separate topic)

## Open Questions

- Roll Dash Composure cost: listed at 1, same as Burst — may need to be 2 if longer i-frames prove too strong at high Composure builds. Post-demo tuning.
- Phase Dash and High Perception enemies: does Phase Dash bypass detection mid-travel? Working assumption: no — detection reacts to destination position, not travel arc. Confirm during enemy AI implementation.

## GDD Reference

> Movement in Crawl Craft is isometric top-down. The full movement vocabulary is: walk and dash. No jumping. All Dashes cost Composure. Always. Even traversal outside of combat.
>
> Boots define the Dash. Defensive Dashes grant i-frames. Offensive Dashes replace the i-frame escape entirely — the Dash becomes an attack or CC. This is a conscious build trade.
