# Player Character

**Status**: Idea
**Core Fantasy**: You did not choose who to be — you became someone through what you did.
**[← Back to GDD Index](../GDD.md)**

---

### Overview

The player character begins as a blank slate contestant dropped into the dungeon. There is no class selection, no backstory screen, no archetype picker. Identity is constructed entirely through play: the items you equip, the Sponsors you align with, the level-up choices you make, and how deep you get.

### Mechanics

- No class selection at run start
- Single canonical character design for initial release — visual variety comes from equipped items, not character selection
- Build identity forms through level-up choices and Sponsor contracts over the course of a run
- Equipped items are visible on the character model
- Stats dynamically affect character appearance, making builds visually readable at a glance:
  - Strength → character becomes physically larger and bulkier
  - Dexterity → character becomes leaner and more agile-looking
  - Intelligence → head grows larger
  - Wisdom → beard grows longer
- Character visually and behaviourally reacts to Viewer count: taunts and crowd-plays at high Viewer counts, defensive and head-down at low counts
- No scripted voice lines — all personality is emergent from build and choices

### Player Experience

- Players who align with a particular Sponsor across multiple floors will feel their character adopt that Sponsor's playstyle flavour
- The character's crowd reactions provide real-time feedback on Viewer count without the player needing to check a UI element

### Systemic Interactions

- Character crowd reactions connect visual feedback to the Audience System
- Sponsor allegiance as identity connects the Sponsor System to the character's perceived personality

### Edge Cases & Risks

- Blank slate starts may feel directionless in early floors — the Sponsor System's floor-entry choice must do the work of giving the player an immediate sense of intent

### Open Questions

- Do Sponsor allegiances have visual effects on the character (costume changes, aura effects)?
- Is there any form of persistent character identity across runs (a name, a record, a broadcast history)?
