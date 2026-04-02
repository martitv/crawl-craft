# Crawl Craft — Game Design

2D/isometric dungeon crawl RPG inspired by Dungeon Crawler Carl. Players descend dungeon floors, face bosses, and manage viewer counts in a broadcast-style setting. Built in Godot 4.

## Repo structure

- `design/GDD.md` — master Game Design Document (index → links to `design/sections/`)
- `design/ubiquitous-language.md` — canonical game terminology glossary
- `prd/` — Product Requirement Documents (mirrored as GitHub issues)
- `plans/` — phased development plans per feature

## Workflow

```
Braindump / ideas
    ↓ [game-ideation agent] — spar or formalize into GDD
design/GDD.md
    ↓ [/game-ubiquitous-language] — run after significant GDD additions
design/ubiquitous-language.md
    ↓ [/gdd-to-prd <section>]
prd/<feature>.md + GitHub Issue (label: prd)
    ↓ [/prd-to-plan <issue>]  (run in crawl-craft-game repo)
plans/<feature>.md
    ↓ [/prd-to-issues <plan>]  (run in crawl-craft-game repo)
GitHub Issues (label: work-item) → implemented in martitv/crawl-craft-game
```

## Rules

- GDD section status tags: `Idea → In Design → Approved → Implemented`
- Run `/game-ubiquitous-language` after major GDD additions and before writing PRDs
- Each PRD and work issue should be a vertical slice — thin but complete end-to-end
