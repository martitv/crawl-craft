# Crawl Craft — Game Design Document

> Living document. Sections grow organically as the game is designed.
> Status tags: `Idea` → `In Design` → `Approved` → `Implemented`

---

## Table of Contents

| # | Section | Status | Summary |
|---|---------|--------|---------|
| 1 | [Game Overview](sections/01-game-overview.md) | ✅ Approved | Premise, core pillars, platform & engine, multiplayer overview |
| 2 | [Core Loop](sections/02-core-loop.md) | 🔧 In Design | Floor structure, death system, Mega Boss events, pacing |
| 3 | [Audience System](sections/03-audience-system.md) | 🔧 In Design | Viewers, Followers, EV, Crescendo, Highlights, Total Viewcount |
| 4 | [The AI](sections/04-the-ai.md) | 🔧 In Design | AI mood, Plan Adherence, AI Messages, AI Offers |
| 5 | [Between Floors](sections/05-between-floors.md) | 🔧 In Design | Sponsor System, Level-Up System, Social Room |
| 6 | [Meta-Progression](sections/06-meta-progression.md) | 🔧 In Design | Clout formula, permanent upgrades, starting loadouts |
| 7 | [Build System](sections/07-build-system.md) | 🔧 In Design | Gear slots, spells, Overcasting, Viewer Reservation, Tag synergy |
| 8 | [Quests & Challenges](sections/08-quests-and-challenges.md) | 🔧 In Design | Quest types, Narrative Branches, Sponsor Challenges, Quest Journal |
| 9 | [Combat System](sections/09-combat-system.md) | 🔧 In Design | Composure, Block/Dodge/Parry, Combo System, enemy tags, Bypass |
| 10 | [Player Character](sections/10-player-character.md) | 💡 Idea | Blank slate identity, stat-driven appearance, crowd reactions |

---

## Design Principles

- **GDD is the source of truth.** PRDs follow the GDD, not the other way around.
- **Vertical slices.** Each PRD and work issue should be thin but complete end-to-end.
- **Status gates.** A section must be `Approved` before a PRD is written against it.
- **Ubiquitous language.** All terms must match `design/ubiquitous-language.md`. Run `/game-ubiquitous-language` after major additions.

---

## Workflow

```
Braindump / ideas
    ↓ [game-ideation agent]
design/GDD.md (this file) + design/sections/<section>.md
    ↓ [/game-ubiquitous-language]
design/ubiquitous-language.md
    ↓ [/gdd-to-prd <section>]
GitHub Issue (PRD) + prd/<feature>.md
    ↓ [/prd-to-plan <issue>]
plans/<feature>.md
    ↓ [/prd-to-issues <plan>]
GitHub Issues (work items) → crawl-craft-game repo
```
