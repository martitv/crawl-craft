---
description: Turn a PRD into a phased vertical-slice development plan. Usage: /prd-to-plan <issue number or prd file path>
argument-hint: <GitHub issue number or prd/feature.md>
---

Convert a PRD into a phased implementation plan saved to `plans/`.

---

## Parse `$ARGUMENTS`

Either:
- A GitHub issue number (e.g. `12`) — fetch the issue body
- A file path (e.g. `prd/combat-system.md`) — read the file

If a GitHub issue number is given, fetch it:
```bash
gh issue view <number> --json title,body
```
If `gh` not on PATH: `"/c/Program Files/GitHub CLI/gh" issue view <number> --json title,body`

If no argument is given, list files in `prd/` and open GitHub issues labeled "prd". Ask the user to pick one. Stop until they respond.

---

## Step 1 — Read context

1. Read the PRD in full.
2. Read `design/GDD.md` — this is the index. Find the relevant section and read it from `design/sections/`.
3. Read `design/ubiquitous-language.md` — use canonical terms.
4. List existing files in `plans/` — check for related plans that share dependencies.

---

## Step 2 — Identify durable decisions

From the PRD, extract decisions that are unlikely to change and should anchor the plan:

- Core data structures (what entities/resources does this feature introduce?)
- Key game states (what states does the player/system move through?)
- Integration points (what existing systems does this touch?)
- Godot-specific constraints (scene structure, signals, autoloads)

These become the architectural backbone of the plan. List them explicitly — they survive refactors.

---

## Step 3 — Draft vertical slices

Break the PRD into phases. Each phase:

- Delivers a narrow but **complete** path through every layer (game logic, UI, data persistence if any)
- Is independently **demoable** upon completion
- Builds directly on the previous phase
- Avoids specifying implementation details that may change (method names, exact node paths, etc.)

Aim for 4–8 phases. First phase is always the tracer bullet: the thinnest possible working slice.

Draft the phases and show them to the user:
> "Here's the proposed breakdown. Does the order make sense? Anything to split, merge, or reorder?"

Adjust based on feedback.

---

## Step 4 — Write the plan

Derive the file name from the PRD: `plans/<feature-slug>.md`

```markdown
# Plan: [Feature Name]

**PRD**: [link to prd file or GitHub issue]
**GDD Section**: [section name]
**Created**: [date]

---

## Architectural Decisions

These are durable — they should survive implementation changes.

| Decision | Choice | Rationale |
|----------|--------|-----------|
| [decision] | [choice] | [why] |

---

## Phases

### Phase 1 — [Name] *(Tracer Bullet)*

**Goal**: [What is demoable when this phase is complete?]

**User Stories Covered**:
- [from PRD]

**Description**:
[What gets built. Focus on behaviors and contracts, not implementation details.]

**Acceptance Criteria**:
- [ ] [observable outcome]
- [ ] [observable outcome]

**Dependencies**: None

---

### Phase 2 — [Name]

**Goal**: [What is demoable when this phase is complete?]

**User Stories Covered**:
- [from PRD]

**Description**:
[What gets built.]

**Acceptance Criteria**:
- [ ] [observable outcome]

**Dependencies**: Phase 1

---

*(repeat for each phase)*

---

## Out of Scope

- [things not covered in this plan — deferred to future PRDs]

## Open Questions

- [anything that needs resolving before or during implementation]
```

---

## Step 5 — Confirm and save

Show the plan to the user. Ask:
> "Ready to save this plan? After this we can run `/prd-to-issues` to break it into GitHub work items."

Save to `plans/<feature-slug>.md` on confirmation.
