# Crawl Craft — Game Design Repo

2D/isometric dungeon crawl RPG inspired by Dungeon Crawler Carl. Players descend dungeon floors, face bosses, and manage viewer counts in a broadcast-style setting. Built in Godot 4.

## This repo

Design only. No game code lives here.

- `design/GDD.md` — master Game Design Document (living doc, grows organically)
- `design/ubiquitous-language.md` — canonical game terminology glossary
- `prd/` — Product Requirement Documents (markdown + mirrored as GitHub issues)
- `plans/` — phased development plans per feature
- `.claude/agents/` — subagents
- `.claude/commands/` — slash commands (skills)

## Workflow

```
Braindump / ideas
    ↓ [game-ideation agent] — spar or formalize into GDD
design/GDD.md
    ↓ [/game-ubiquitous-language] — run after significant GDD additions
design/ubiquitous-language.md
    ↓ [/gdd-to-prd <section>] — per feature/system
GitHub Issue (PRD) + prd/<feature>.md
    ↓ [/prd-to-plan <issue>]
plans/<feature>.md
    ↓ [/prd-to-issues <plan-file>]
GitHub Issues (work items) → implemented in crawl-craft-game repo
```

## Rules

- GDD is the source of truth. PRDs follow the GDD, not the other way around.
- Run `/game-ubiquitous-language` after major GDD additions and before writing PRDs.
- GDD section status tags: `Idea → In Design → Approved → Implemented`
- Vertical slices — each PRD and work issue should be thin but complete end-to-end.
- The game code repo is `crawl-craft-game` (Godot 4, set up separately).

## GitHub setup

Set `GITHUB_TOKEN` env var for issue-creation skills. Repo is auto-detected from `git remote`.
