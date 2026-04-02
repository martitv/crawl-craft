# PRD: Combat System

**GDD Section**: [Combat System](../design/sections/09-combat-system.md)
**Status**: Draft
**Created**: 2026-04-02
**GitHub Issue**: #1 https://github.com/martitv/crawl-craft/issues/1

---

## Problem / Why

Without a combat system, Crawl Craft is a dungeon with nothing to do in it. Combat is also the primary real-time driver of the Audience System — every fight is a performance. The moment-to-moment feel of reading enemies, spending Composure, and building Combo is the core gameplay loop that everything else builds on top of.

## Solution Overview

A timing-based action combat system built around a discrete Composure pool. The player attacks freely but must spend Composure to defend. Three defensive actions — Block, Dodge, Parry — each have distinct costs and payoffs. Combo tracks the quality of performance and feeds Current Entertainment. Getting hit is not just a failure state — it is drama, and the crowd responds to it.

## User Stories

- As a player, I want to read enemy attacks and respond with the right defensive action so that I feel skilled and in control
- As a player, I want my Composure to feel like a meaningful resource so that every defensive decision has weight
- As a player, I want my Combo to feel connected to how well I'm performing so that good play has its own momentum
- As a viewer, I want to see the contestant take a hit and recover so that the broadcast has tension and drama

## Vertical Slices

| # | Slice | Description | Acceptance Criteria |
|---|-------|-------------|---------------------|
| 1 | Player attack | Player can attack enemies. Bare fists deal damage. Enemies have HP and die. | Attacks connect, damage is dealt, enemy HP depletes, enemy death state triggers |
| 2 | Composure + Block | Composure pool exists and is displayed. Block negates incoming damage at Composure cost proportional to hit size. Stagger triggers at 0 Composure. Stagger recovers on timer. | Composure visible as point count, Block works correctly, Stagger state triggers and exits on timer, Stagger → Knocked Down fires on overflow |
| 3 | Dodge | Dodge costs 1 Composure. Grants i-frames and movement burst. | Dodge input works, i-frames active during animation window, movement burst applied, Composure decrements |
| 4 | Parry | Parry costs 1 Composure. Has a timing window. On success: damage negated, Composure refunded, Enemy Stagger applied. On miss: treated as no defensive action. | Timing window functional, success path (refund + enemy stagger) and miss path both work |
| 5 | Combo + Entertainment display | Combo builds on attacks and defensive actions. HP damage pauses Combo growth but does not reset Entertainment value — entertainment is drama, not just performance. Inactivity causes Entertainment to decay (slow start, accelerates). Display shows entertainment value, not raw hit count. | Combo increments on hits and defensive actions, HP damage pauses but doesn't crash entertainment, inactivity decay curve triggers, UI shows entertainment value |
| 6 | Composure regen | Composure regenerates passively at all times. Rate is a tunable parameter. | Composure restores over time, regen rate configurable in code |

## Design Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Composure is discrete points, not a bar | Points (base 4) | Makes cost-per-action legible. Player always knows exactly how many actions they have left. |
| All defensive actions cost Composure | Yes | Unified resource creates meaningful tradeoffs between Block, Dodge, Parry, and Dash |
| Stagger recovery | Time-based only, no input | Avoids button-mashing. Duration is brief but punishing in an active attack chain. |
| Stagger → Knocked Down | Overflow threshold (cost >> remaining Composure) | Distinguishes "dangerously low" from "recklessly empty." Exact threshold is tuning. |
| HP damage and Entertainment | HP damage pauses Combo growth but does NOT reduce Entertainment value | Getting hit is drama. The crowd leans in. Entertainment only decays on inactivity. |
| Combo break display | Entertainment value, not hit counter | Communicates the quality of the performance, not just the quantity of actions |
| Stats are multipliers | Strength multiplies weapon flat damage; Dexterity scales Composure | Flat values live on gear; stats scale them. Keeps gear meaningful at all depths. |

## Out of Scope

- Enemy AI and specific enemy behaviours (see Enemy Design PRD)
- Audience System / Viewer generation (Combo feeds Current Entertainment, but Viewer math is Audience System scope)
- Boon extensions to defensive actions (Build System scope)
- Weapon-specific attack patterns (Build System scope)
- Stealth and Bypass mechanics (stubbed for demo — no stealth spell in scope)

## Open Questions

- Block cost scaling: exact mapping (small=1, medium=2, heavy=3) needs tuning against base Composure pool and enemy hit distribution
- Stagger overflow threshold: exact Composure deficit required to skip to Knocked Down — implementation tuning
- Combo → Entertainment curve: exact rate of Entertainment growth per Combo hit and the inactivity decay shape — implementation tuning
- HP damage entertainment pulse: should taking HP damage generate a small positive Entertainment spike (drama bonus)? Flagged as possible, not locked.

## GDD Change Flagged

The current GDD (Combat System, Combo System section) states that HP damage "breaks Combo" and triggers Entertainment decay. This PRD overrides that: HP damage pauses Combo growth but does not reduce Entertainment. **The GDD should be updated after this PRD is confirmed.**

## GDD Reference

> Combat in Crawl Craft is deliberate and timing-based at its core. The player always has something to do — attack freely, and choose from three defensive options that all feed the Combo. Every defensive action is a performance. Taking unblocked HP damage is a failure state, not a neutral outcome.
>
> Composure is a discrete point pool — not a bar. Base range: 3–5 points. Only defensive actions cost Composure. Attacking is always free.
