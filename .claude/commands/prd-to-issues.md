---
description: Break a development plan into GitHub Issues. Each issue is a vertical slice classified as HITL or AFK. Usage: /prd-to-issues <plan file path>
argument-hint: plans/<feature>.md
---

Convert a development plan into individual GitHub Issues and push them directly.

---

## Parse `$ARGUMENTS`

A file path to a plan (e.g. `plans/combat-system.md`).

If no argument is given, list files in `plans/`. Ask the user to pick one. Stop until they respond.

---

## Step 1 — Read context

1. Read the plan file in full.
2. Read the linked PRD (from plan header).
3. Read `design/ubiquitous-language.md` — use canonical terms.
4. Read `design/GDD.md` (index) and the relevant section file(s) from `design/sections/` — understand the broader design context for each slice.

---

## Step 2 — Draft issues

For each phase in the plan, create one GitHub issue. Each issue must:

- Be independently executable (a developer can pick it up and complete it without waiting on anything except its listed dependencies)
- Deliver a complete vertical slice (not a layer)
- Be demoable or verifiable on its own

### Issue classification

Classify each issue as:

- **HITL** (Human-In-The-Loop): Requires design decisions, architectural choices, or player-feel judgment calls during implementation. Human must be available.
- **AFK** (Away From Keyboard): Can be implemented, tested, and merged without mid-task decisions. Fully spec'd.

Prefer AFK where possible. If an issue could be AFK with a bit more spec work, add the extra spec to the issue body rather than marking it HITL.

---

## Step 3 — Show draft and confirm

Present the full list before creating anything:

```
Issue 1: [title] [AFK/HITL]
  → [one-line description]
  → Depends on: [none / Issue N]

Issue 2: [title] [AFK/HITL]
  → [one-line description]
  → Depends on: [Issue 1]

...
```

Ask:
> "Does this breakdown look right? Anything to split, merge, change classification, or reorder before I create them?"

Adjust based on feedback. Do NOT create issues until the user confirms.

---

## Step 4 — Create issues in dependency order

Write each issue body to a temp file, then create with `gh`:

```bash
gh issue create \
  --title "[Phase Name]" \
  --body-file /tmp/issue-body.md \
  --label "plan-issue,afk"
```

If `gh` is not on PATH, use full path: `"/c/Program Files/GitHub CLI/gh"`

**Issue body template (write to temp file):**

```markdown
## [Phase Name]

**Plan**: [link to plan file]
**PRD**: #[issue number]
**Classification**: AFK | HITL
**Depends on**: #[issue number] | None

---

## Description

[What gets built. Describe behaviors and contracts — not method names or implementation details. This issue should still be useful after a major refactor.]

## Acceptance Criteria

- [ ] [observable, testable outcome]
- [ ] [observable, testable outcome]

## User Stories Covered

- [from PRD]

## Design Notes

[Any design decisions or constraints relevant to this slice. Include Godot-specific context where helpful.]

## Out of Scope

- [things explicitly NOT in this issue]
```

Labels to apply:
- `plan-issue` — on all issues
- `hitl` or `afk` based on classification

If gh is not authenticated: `gh auth login` then retry.

---

## Step 5 — Report

After all issues are created, print:

```
Created N issues:
  #[n] [title] — [url]
  #[n] [title] — [url]
  ...

AFK: X  HITL: Y
```

Suggest next step:
> "Issues are live. Open `crawl-craft-game` in Claude Code and start on issue #[first AFK issue]."
