---
description: Scan the GDD and extract a canonical game terminology glossary. Run after significant GDD additions and before writing any PRDs.
---

Extract and formalize domain-specific game terminology from the GDD into `design/ubiquitous-language.md`.

---

## Step 1 — Read source documents

1. Read `design/GDD.md` in full.
2. Read `design/ubiquitous-language.md` if it exists (for prior terms to update rather than duplicate).
3. Read any files in `prd/` to catch terms introduced in PRDs.

---

## Step 2 — Extract terms

Identify all domain-specific terms: game systems, entities, mechanics, UI concepts, meta-game concepts, and any invented vocabulary specific to Crawl Craft.

For each term, note:
- How it's used in the GDD
- Whether it has synonyms or aliases in the text
- Whether it's used inconsistently across sections

**Crawl Craft domain areas to check:**
- Dungeon structure (floors, rooms, zones, runs, etc.)
- Player systems (stats, builds, loadouts, etc.)
- Combat (attacks, abilities, effects, etc.)
- Progression (XP, leveling, unlocks, etc.)
- Broadcast/audience mechanic (viewers, votes, events, etc.)
- Meta-game (between-run persistence, unlocks, etc.)
- Enemies and bosses

---

## Step 3 — Flag problems

Flag:
- **Synonyms**: Two different words that mean the same thing (e.g. "stage" and "floor" used interchangeably)
- **Ambiguities**: One word that means different things in different contexts
- **Undefined terms**: Terms used in the GDD with no definition

For each flag, recommend which term to make canonical and which to retire.

---

## Step 4 — Write the glossary

Write (or overwrite) `design/ubiquitous-language.md` with this structure:

```markdown
# Crawl Craft — Ubiquitous Language

*Canonical terminology. Use these exact terms in all design docs, PRDs, and code.*
*Last updated: [date]*

---

## [Domain Area]

| Term | Definition | Aliases to avoid |
|------|------------|-----------------|
| **[Term]** | [Definition] | [synonyms to retire] |

---

## Relationships

- [Term A] contains one or more [Term B]
- [Term C] is a type of [Term D]
- etc.

---

## Flagged Ambiguities

- **[Term]**: [description of the ambiguity and recommendation]

---

## Example Usage

> [3–5 sentence dialogue showing correct usage between designer and developer]
```

---

## Step 5 — Report

Tell the user:
- How many terms were extracted
- Which synonyms/ambiguities were found and what was recommended
- Any terms that are undefined in the GDD that need a definition added
