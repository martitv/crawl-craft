---
description: Turn a GDD section into a PRD. Creates a local markdown file and a GitHub issue. Usage: /gdd-to-prd <section name or description>
argument-hint: <GDD section name>
---

Convert a GDD section into a Product Requirements Document, saved locally and as a GitHub issue.

---

## Parse `$ARGUMENTS`

`$ARGUMENTS` is the name or description of a GDD section to convert (e.g. "Combat System", "Broadcast Viewer Mechanic").

If no argument is given, list all sections found in `design/GDD.md` with their current Status and ask the user to pick one. Stop until they respond.

---

## Step 1 — Read context

1. Read `design/GDD.md` — locate the target section.
2. Read `design/ubiquitous-language.md` — use canonical terms throughout. If it doesn't exist, note this and suggest running `/game-ubiquitous-language` first.
3. Read any existing files in `prd/` to understand the established PRD style.

If the target section has Status `Idea`, warn the user:
> "This section is still at Idea status. PRDs work best on In Design or Approved sections. Want to continue anyway, or should we spar on it first with the game-ideation agent?"

Stop and wait for their answer.

---

## Step 2 — Gap analysis

Read the GDD section carefully. Identify what's defined and what's missing for a complete PRD:

- Unclear mechanics or edge cases
- Missing acceptance criteria (how do we know this is done?)
- Unresolved Open Questions that block implementation
- Systemic interactions that need definition

---

## Step 3 — Requirements interview

For each significant gap, ask the user one question at a time. Provide a recommended answer based on the GDD context and game design principles.

Format:
> **Q**: [question]
> **Recommended**: [suggested answer with brief rationale]

Wait for their answer before asking the next question. Continue until all blockers are resolved or the user says to proceed with assumptions.

---

## Step 4 — Identify vertical slices

Think about how this feature can be broken into thin, complete end-to-end slices — each deliverable independently, each demoable on its own.

A vertical slice cuts through all layers (game logic, UI, data) rather than implementing one layer at a time. Prefer many thin slices over fewer large ones.

Draft 3–6 slices and show them to the user. Ask:
> "Does this breakdown make sense? Anything to split, merge, or reorder?"

Adjust based on feedback.

---

## Step 5 — Write the PRD

Write the PRD to `prd/<feature-slug>.md`:

```markdown
# PRD: [Feature Name]

**GDD Section**: [section name and link]
**Status**: Draft
**Created**: [date]

---

## Problem / Why

[What player experience problem does this solve? What does the game feel like without this?]

## Solution Overview

[High-level description of the feature. 2–4 sentences.]

## User Stories

- As a player, I want to [action] so that [outcome]
- As a viewer, I want to [action] so that [outcome]
- *(add more as relevant)*

## Vertical Slices

| # | Slice | Description | Acceptance Criteria |
|---|-------|-------------|-------------------|
| 1 | [name] | [description] | [how we know it's done] |
| 2 | ... | ... | ... |

## Design Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| [decision] | [choice] | [why] |

## Out of Scope

- [things explicitly not included in this PRD]

## Open Questions

- [anything still unresolved]

## GDD Reference

[Relevant excerpt or summary from the GDD section]
```

---

## Step 6 — Show and confirm

Show the user the PRD. Ask:
> "Ready to create the GitHub issue, or do you want to edit anything first?"

Wait for confirmation.

---

## Step 7 — Create GitHub issue

Use `gh` to create the issue (handles auth automatically):
```bash
gh issue create \
  --title "PRD: [Feature Name]" \
  --body-file prd/<feature-slug>.md \
  --label "prd"
```

If `gh` is not on PATH, try the full path:
```bash
"/c/Program Files/GitHub CLI/gh" issue create ...
```

If gh is not authenticated, print:
```
Run: gh auth login
Then re-run this command.
```

On success, print the issue URL and update the PRD file with the issue number:
```markdown
**GitHub Issue**: #[number] [url]
```
