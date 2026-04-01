# Crawl Craft — Ubiquitous Language

*Canonical terminology. Use these exact terms in all design docs, PRDs, and code.*
*Last updated: 2026-04-01*

---

## Dungeon Structure

| Term | Definition | Aliases to avoid |
|------|------------|-----------------|
| **Floor** | A single procedurally generated level. The fundamental unit of play. Each floor is a self-contained broadcast episode. | Level, Stage, Zone |
| **Run** | A single playthrough from floor 1 until true death or completion. All Followers and stats reset (or partially reset) at run end. | Session, Game, Attempt |
| **Depth** | How far into the dungeon a player has descended. Expressed as a floor number (e.g. "depth 12"). | Progress, Level number |
| **Between Floors** | The structured, safe transition phase that occurs after clearing a floor. No enemies, no AI events. Contains the Sponsor choice, crafting, and stash management. | Hub, Safe room, Lobby, Transition |
| **Broadcast** | The framing metaphor and in-world reality of the dungeon. Every run is a live broadcast; the dungeon was built as entertainment. Not a UI element — a worldbuilding concept. | Show, Stream, TV show |
| **Floor Exit** | The door or portal that advances the player to the next floor. Always locked until the Key is used. | Exit, Portal, Door, Stairs |
| **Key** | The item required to unlock the Floor Exit. Always present on every floor, but its placement varies (hidden, guarded, gated behind an objective, dropped by a mini-boss). | Exit key, Floor key |

---

## Player & Character

| Term | Definition | Aliases to avoid |
|------|------------|-----------------|
| **Contestant** | The in-world term for a player character. They are not heroes — they are contestants in a broadcast. Use "contestant" in flavour text and AI dialogue; use "player" or "player character" in design docs. | Hero, Player character (in flavour text) |
| **Build** | The combination of stats, equipped items, passive abilities, and active abilities a player has accumulated during a run. | Loadout (loadout = starting item set only), Class, Spec |
| **Loadout** | A pre-configured starting item set unlocked via Clout and selected before a run begins. Distinct from Build (which is the emergent result of a run). | Build (do not use for the starting set) |
| **Stat** | A numeric character attribute. Core stats: Strength, Defense, Dexterity, Intelligence, Wisdom, Entertainment Value. | Attribute |
| **Strength** | Combat stat. Increases physical damage. Visually: character becomes bulkier at high values. | STR |
| **Defense** | Combat stat. Reduces incoming damage. | DEF, Armour (unless referring to an item type) |
| **Dexterity** | Combat stat. Affects speed, dodge, or precision (exact mechanic TBD). Visually: character becomes leaner at high values. | DEX, Agility, Speed |
| **Intelligence** | Stat that contributes to Magical Affinity and accelerates jewelry identification (exact mechanic TBD). Visually: character's head grows larger at high values. | INT |
| **Wisdom** | Stat that contributes to Magical Affinity (exact mechanic TBD). Visually: character's beard grows longer at high values. | WIS |
| **Magical Affinity** | Derived from Intelligence + Wisdom. Gates the effectiveness of equipped Jewelry. Low affinity = item gives EV only; high affinity = full magical effects active. Exact derivation TBD. | Magic stat, Arcane affinity |
| **XP** | Resource earned from all activities: kills, quest completions, events, challenges, exploring, gathering, crafting. Triggers a Level-Up when a threshold is reached. | Experience, Experience points |

---

## Audience System

| Term | Definition | Aliases to avoid |
|------|------------|-----------------|
| **Entertainment Value (EV)** | A core build stat that determines how effectively a player converts spectacular actions into Viewers. Does not affect combat directly. Items and abilities carry EV ratings. | Charisma, Hype stat, Entertainment stat |
| **Current Entertainment** | The real-time entertainment output the player is producing right now. Calculated from EV stat × recent actions. Distinct from EV (which is a static stat). Current Entertainment sets the target Viewcount the Viewer count trends toward. | EV (do not conflate with the stat), Live entertainment |
| **Viewers** | The volatile, real-time audience hype stat. Spikes on spectacular actions; decays during inactivity. Forms the "buff" layer of Total Viewcount. Also serves as spell fuel via Overcasting. | Live viewers, View count (two words) |
| **Viewer Spike** | A sudden sharp increase in Viewers triggered by a high-EV action, Crescendo, or other spectacular moment. | Hype spike, Viewer burst |
| **Target Viewcount** | The Viewer count that the system asymptotically trends toward, set by the player's Current Entertainment. Not a displayed stat — an internal system concept. | Target viewers, Expected viewers |
| **Followers** | Crystallised, permanent Viewers accumulated through Crescendo moments. Forms the "flat base" layer of Total Viewcount. Powers Self-Revive. | Permanent viewers, Fans, Subscribers |
| **Free Viewers** | Viewers that are not currently reserved. Can crystallise into Followers at a Crescendo. Contrast with Reserved Viewers. | Unlocked viewers, Available viewers |
| **Reserved Viewers** | Viewers locked by Overcasting. Still count toward Total Viewcount but cannot crystallise into Followers. Released at Crescendo (Followers first, then live Viewers) or fully reset on floor transition. | Locked viewers, Spent viewers |
| **Total Viewcount** | The combined stat used by all systems: `Total Viewcount = Followers + Viewers`. Everything that scales with audience size reads from this number. | Viewership (retire), View count (retire), Total viewers |
| **Crystallisation** | The process of converting a portion of current Viewers into permanent Followers, triggered by a Crescendo moment. Rate scales with current Follower count. | Conversion, Locking in |
| **Crescendo** | A moment that triggers Crystallisation: completing a quest, killing a boss, finishing a Sponsor Challenge. The "payoff" beat of an arc of entertainment. Also triggers release of Reserved Viewers (Followers first). | Milestone, Completion trigger |
| **Highlight** | A spectacular moment that the game automatically logs. Accessible via the Highlights UI and the Social Room Highlights TV. | Clip, Replay, Best moment |
| **Highlights UI** | A phone-like in-game interface the player pulls up to review their Highlights from the current floor, and see Highlights from other players on the same floor. | Clip viewer, Replay UI |
| **Viewer Lag** | The intentional delay before Viewer count responds to changes in Current Entertainment. Prevents jitter from momentary spikes/lulls and gives Highlights meaningful windows of effect. | Grace period (use "Viewer Lag" specifically) |

---

## The AI

| Term | Definition | Aliases to avoid |
|------|------------|-----------------|
| **The AI** | The dungeon's architect, broadcaster, and primary NPC. Never named. Referred to only as "the AI." Its primary drive is maximising Total Viewcount; its secondary trait is artistic pride in its floor designs. | The Director, The System, The Algorithm, The Entity |
| **AI Mood** | The AI's current disposition toward the player. A function of Plan Adherence and Current Entertainment. States: very happy → neutral → slightly frustrated → mad. Affects quest frequency, AI Offer quality, and flavour text tone. | Director mood, AI disposition |
| **Plan Adherence** | Whether the player is engaging with the floor as the AI designed it — attempting quests, interacting with authored content. One of two inputs to AI Mood. | Following the plan, Quest engagement |
| **AI Message** | A sparse direct communication from the AI to the player mid-run. Maximum 1–2 per floor. Triggered by specific moments (first overkill, ignoring quests, Highlights, Knocked Down). | AI dialogue, Director message, Pop-up |
| **AI Offer** | A rare option injected by the AI into the Level-Up Pool. Visually distinct. Higher risk, higher EV modifier, occasionally the only access path to rare ability tiers. Not the same as an AI Wildcard. | Director offer, Special offer |

---

## Build System

| Term | Definition | Aliases to avoid |
|------|------------|-----------------|
| **Gear Slot** | A dedicated equipment position on the player character. Each slot has a defined design mandate (combat, utility, cosmetic, etc.). | Equipment slot, Item slot |
| **Weapon Slot** | Dedicated gear slot for weapons. Holds either 2x one-handed items (dual-wield or weapon + off-hand) or 1x two-handed item. | Main hand / off hand (use slot config instead) |
| **One-Handed** | A weapon configuration that occupies one of the two weapon sub-slots. Allows dual-wielding or pairing with an off-hand item. | Single-handed |
| **Two-Handed** | A weapon configuration that occupies both weapon sub-slots. Cannot be paired with another weapon or off-hand. | Greatsword (not a generic term) |
| **Tome** | A dedicated gear slot containing the player's active spell loadout. One equipped at a time. Each spell has per-floor Spell Charges. Rare tomes contain Extractable Spells. | Spellbook, Grimoire |
| **Boon** | Umbrella term for any choice-based permanent modifier added to a character during a run. Sources: Level-Up Pool, Sponsor Challenge rewards. Types: stat boosts, Passive Abilities, Active Abilities, AI Offers. | Upgrade, Power, Perk |
| **Active Ability** | A cooldown-based ability sourced from the Level-Up Pool (not a Tome spell). No Viewer cost, no charges. Spammable within cooldown. Contrast with Spells, which are heavier and economic. | Skill, Power (ambiguous) |
| **Passive Ability** | An always-on conditional proc ability. Often references Tags to create cross-component interactions. Sourced from the Level-Up Pool. | Passive, Aura |
| **Curse** | A double-edged player-facing effect: a negative and a meaningful upside, always paired. Applied by enemies, floor traps, AI punishment, or certain rare Boons/Sponsor contracts. Authored drama, not random punishment. | Debuff (debuffs are enemy-facing; curses are player-facing) |
| **Debuff** | A negative status effect applied to an enemy. Enemy-facing only. | Curse (do not use for player-facing effects) |
| **Buff** | A positive status effect applied to the player. | Enhancement (use Buff) |
| **Tag** | A keyword label carried by weapons, abilities, gear, and enemies that enables cross-system synergies. Boons reference Tags to create interactions. The synergy engine's foundation. | Keyword (Tag is preferred) |
| **Consumable** | An inventory item with limited quantity. Used from Quick-Cast Slots (fast) or via Inventory Retrieve (slow). Includes grenades, potions, bombs, one-time effect items. | Potion (too narrow), Item (too broad) |
| **Quick-Cast Slot** | A belt-determined slot for instant consumable use in combat. Number of slots (2–4) determined by Belt tier. | Hotbar slot, Active item slot |
| **Inventory Retrieve** | The slower action of using a Consumable outside the Quick-Cast Slots. Viable but has a real combat cost compared to Quick-Cast. | Slow use, Manual use |
| **Stash** | Infinite item storage accessible only during the Between Floors phase. Items can be stored for use on a later floor. Not accessible mid-floor. | Bank, Storage, Inventory (inventory is active, stash is stored) |
| **Scroll** | A special Consumable subtype. One-time use, no stat or Magical Affinity requirements. No charges. Consumed on use. Sources: floor drops, NPC trades, extracted from rare Tomes. | Spell scroll (too narrow — scrolls include non-spell effects) |
| **Crafted Item** | An item made from enemy-dropped and floor-gathered materials. Available between combat encounters. Full crafting system TBD. | Crafted weapon (use Crafted Item for all crafted results) |

---

## Spells & Magic

| Term | Definition | Aliases to avoid |
|------|------------|-----------------|
| **Spell** | An active combat ability contained in a Tome. Has a per-floor Spell Charge count. Heavier and more economically significant than Active Abilities. Subject to Overcasting. | Skill, Ability (use Spell specifically for Tome-sourced magic) |
| **Spell Tier** | The power classification of a Spell: Minor, Major, or Cataclysmic. Determines base Spell Charges and Overcast cost. | Spell level, Spell rank |
| **Spell Charges** | The per-floor use count for a Spell. Resets fully on floor transition. Minor = many, Major = few, Cataclysmic = 1 or 0 base. When depleted, the Spell can only be used via Overcasting. | Mana, Uses, Cooldown (Spell Charges are distinct from cooldowns) |
| **Overcast** | Using a Spell that has 0 Spell Charges remaining by paying a flat Viewer cost. Triggers Viewer Reservation. Cannot Overcast without enough Free Viewers to cover the full flat cost. | Over-use, Mana burn |
| **Extractable Spell** | A Spell found inside a rare Tome that can be transferred — either into the player's current Tome or into a single-use Scroll. The Tome itself may not be worth equipping; the Spell inside it is the value. | Embedded spell, Hidden spell |

---

## Quests & Challenges

| Term | Definition | Aliases to avoid |
|------|------------|-----------------|
| **Quest** | A narrative/exploration task authored by the AI, written in its voice. Has a destination or target and a narrative wrapper. The only way to fail a Quest is to ignore it entirely — once attempted, it always resolves. Completing a Quest = Crescendo trigger. | Mission, Objective, Task |
| **Challenge** | A condition-based task: "how you play" not "where you go." Event-driven — appears at scheduled floor moments, attached to Quests, or sourced from Sponsors. Completing a Challenge = Crescendo trigger. | Quest (distinct — do not conflate), Achievement, Task |
| **Standalone Challenge** | A Challenge that appears mid-floor as its own event, independent of any Quest. Can be attempted or ignored; ignoring it means missing the bonus reward only. | Independent challenge, Floor challenge |
| **Attached Challenge** | A Challenge modifier layered on top of an existing Quest. Decoupled from Quest success — missing it loses the bonus reward but does not affect Quest completion. | Quest modifier, Optional condition |
| **Narrative Branch** | A special Attached Challenge where the outcome routes the Quest to a different consequence. Both outcomes fully resolve the Quest — neither is a failure. The AI uses these deliberately as storytelling forks, not difficulty modifiers. | Story branch, Quest fork, Optional objective |
| **Sponsor Challenge** | A Challenge with "Sponsor" as its source field. Mechanically identical to other Challenges. Always themed to the sponsored item or playstyle. Completing it = the primary Crescendo for that floor's Sponsor contract. | Sponsor quest, Sponsor objective |
| **Quest Journal** | The unified in-game UI tracking all active Quests and Challenges with their source metadata. Shows Quest status (Active/Complete/Ignored), attached Challenge status (Active/Completed/Missed), and logs Narrative Branch outcomes. Full UI design TBD. | Quest log, Journal, Objective tracker |
| **Source Field** | Metadata on every Quest and Challenge indicating its origin: "AI", "Sponsor", "NPC", "Floor Event", etc. Visible in the Quest Journal. Does not change the mechanic — only the context. | Quest type (the source is not the type) |
| **Quest Ignore** | The only true failure state for a Quest: never attempting it. Once a player begins a Quest, it resolves one way or another. Ignoring a Quest contributes to AI Mood degradation (Plan Adherence drops). | Quest failure (reserve "failure" for never attempting) |

---

## Between Floors

| Term | Definition | Aliases to avoid |
|------|------------|-----------------|
| **Sponsor** | An entity that offers the player a floor contract during the Between Floors phase. | Advertiser, Patron, Quest giver |
| **Sponsor Offer** | One of 3 choices presented to the player on entering a new floor. Each contains a Sponsor Challenge and associated items/bonuses. | Sponsor deal, Contract offer |
| **Sponsor Challenge** | The specific task a Sponsor wants the player to complete on the upcoming floor. Completing it triggers a Crescendo. | Sponsor quest, Floor objective, Contract task |
| **Sponsor Pool** | The collection of possible Sponsor Offers for a given floor. Contains neutral sponsors, build-relevant sponsors, and occasionally an AI Wildcard. | Offer pool |
| **AI Wildcard** | An occasional Sponsor Offer injected into the Sponsor Pool by the AI. Riskier and more unusual than standard offers; written in the AI's voice. Distinct from an AI Offer (which is in the Level-Up Pool). | AI Sponsor, Wildcard sponsor |
| **Level-Up** | A progression event triggered when XP thresholds are reached. Presents the player with a Level-Up Pool of options. | Skill up, Power up, Level |
| **Level-Up Pool** | The set of options presented during a Level-Up. Composed of neutral picks, sponsor-influenced picks, and rare AI Offers. | Option pool, Upgrade pool |
| **Social Room** | The shared post-Mega Boss space accessible to all participants before the next floor opens. Contains the Loot Shrine, Dueling Pit, recruitment, and Highlights TV. | Post-boss room, Lobby, Hangout |
| **Loot Shrine** | A Social Room object where players can sacrifice items for group-wide buffs. A collective coordination moment. | Sacrifice altar, Offering shrine |
| **Dueling Pit** | The opt-in PvP area within the Social Room. Players compete for unique loot stakes. Entirely optional; double-confirmed consent required. | Arena, PvP zone |
| **Highlights TV** | The TV object in the Social Room that plays Highlight reels from the Mega Boss fight just completed. | Replay screen, Highlight reel |

---

## Bosses & Combat

| Term | Definition | Aliases to avoid |
|------|------------|-----------------|
| **Boss** | An optional, named enemy encounter on a floor. Solo/party content. Killing a Boss triggers a Crescendo. | Elite boss, Floor boss |
| **Mega Boss** | A large-scale boss encounter that triggers an Open Queue alert to other players. Shared-world event; distinct in scale and design from standard Bosses. | World boss, Raid boss, Event boss |
| **Mini-boss** | A mid-floor enemy capable of dropping the Key. Smaller in scope than a Boss. | Elite enemy, Champion |
| **Knocked Down** | The temporary downed state entered on first death before true death. Opens a window for Self-Revive (spending Followers) or teammate revive (co-op, 30-second window). | Downed, Dead, Defeated |
| **True Death** | Dying while in the Knocked Down state with no revive. Ends the run and returns the player to floor 1. | Death, Permadeath, Run over |
| **Self-Revive** | Spending Followers to stand up from the Knocked Down state. Trades long-term economic power for immediate survival. | Revive (ambiguous in co-op context), Self-res |
| **Overkill** | Dealing significantly more damage than required to kill an enemy. Generates a Viewer Spike scaled by EV. | Burst kill |
| **Chain Kill** | Killing multiple enemies in rapid succession. Generates a Viewer Spike. | Combo kill, Multi-kill (prefer "Chain Kill" or "Simultaneous Kill") |
| **Simultaneous Kill** | Killing multiple enemies in the same instant. Generates a Viewer Spike. | Multi-kill (prefer the specific term) |

---

## Multiplayer

| Term | Definition | Aliases to avoid |
|------|------------|-----------------|
| **Party** | A group of 1–4 players descending together in co-op. | Team, Group, Squad |
| **Open Queue** | The matchmaking system for Mega Boss encounters. Sends an alert to all players in the dungeon; anyone can join. | Raid queue, Public queue |
| **Mega Boss Alert** | The broadcast notification sent when a Mega Boss encounter is triggered. Visible to all players currently in the dungeon. | Boss alert, Raid alert |

---

## Meta-Progression

| Term | Definition | Aliases to avoid |
|------|------------|-----------------|
| **Clout** | The between-run meta-progression currency. Earned at run end: `Clout = Followers × Floor Depth + Highlight Bonus`. Spent on permanent upgrades. | Meta currency, Fame, Prestige |
| **Highlight Bonus** | The flat Clout bonus calculated from peak Highlight moments during a run. Rewards spectacular play in otherwise short runs. Cap TBD. | Highlight reward |
| **Clout Upgrade** | A permanent unlock purchased with Clout. Categories: Base Follower Count, Starting Loadouts, early-floor conveniences, additional unlocks TBD. | Permanent upgrade, Meta upgrade |
| **Base Follower Count** | The Follower count a player starts each run with, increased via Clout upgrades. Reduces early-run economic disadvantage without affecting mid/late-game balance. | Starting followers |

---

## Relationships

- A **Run** consists of one or more **Floors**
- A **Floor** contains one **Key**, optional **Bosses**, optional **Mini-bosses**, and AI-seeded quests
- A **Mega Boss** is a special type of **Boss** that triggers an **Open Queue** via a **Mega Boss Alert**
- **Between Floors** occurs after every **Floor** and always before the next **Floor** begins
- The **Social Room** is a special phase of **Between Floors** that only occurs after a **Mega Boss** kill
- **Entertainment Value (EV)** determines the ceiling of **Current Entertainment**; **Current Entertainment** drives the **Target Viewcount**; **Viewers** trend asymptotically toward **Target Viewcount**
- **Free Viewers** + **Reserved Viewers** = **Viewers** (total live component); **Viewers** + **Followers** = **Total Viewcount**
- A **Crescendo** triggers **Crystallisation** (converting **Free Viewers** into **Followers**) and releases **Reserved Viewers** (Followers restored first, then regular)
- **Overcasting** converts **Free Viewers** into **Reserved Viewers** at a flat cost; requires enough **Free Viewers** to cover the cost
- **Clout** = **Followers** × **Depth** + **Highlight Bonus**, calculated at **Run** end
- **AI Mood** is a function of **Plan Adherence** + **Current Entertainment**
- **AI Offers** appear in the **Level-Up Pool**; **AI Wildcards** appear in the **Sponsor Pool** — these are distinct things
- A **Tome** contains **Spells**; each **Spell** has **Spell Charges**; depleted **Spells** can be **Overcast**
- **Boons** are the result of **Level-Up** choices or **Sponsor Challenge** rewards; they install **Active Abilities**, **Passive Abilities**, or stat boosts
- **Tags** on gear, weapons, and abilities are the connective tissue that **Boons** reference to create synergies
- **Curses** are player-facing (applied to the **Contestant**); **Debuffs** are enemy-facing — never conflate
- A **Quest** can have zero or more **Attached Challenges**; a **Narrative Branch** is a subtype of **Attached Challenge**
- A **Sponsor Challenge** is a **Challenge** with "Sponsor" as its **Source Field** — same mechanic, different origin
- The **Quest Journal** tracks both **Quests** and **Challenges** under a unified source-metadata system

---

## Flagged Ambiguities

- **"Viewership"**: used once in the GDD. Retire in favour of **Total Viewcount** (combined) or **Viewers** (live component).
- **"Multi-kill"**: ambiguous between Chain Kill and Simultaneous Kill. Use the specific term.
- **"AI Offer" vs "AI Wildcard"**: **AI Offer** = Level-Up Pool injection. **AI Wildcard** = Sponsor Pool injection. Always use the full term.
- **"Loadout" vs "Build"**: Loadout = pre-configured starting set. Build = emergent run result. Not interchangeable.
- **"Contestant" vs "Player character"**: "contestant" in in-world text; "player" in design docs. Never "hero."
- **"Ability"**: overloaded. Be specific: **Active Ability** (cooldown, Level-Up Pool), **Passive Ability** (always-on, Level-Up Pool), or **Spell** (Tome-sourced, has Spell Charges). Never use "ability" alone when one of these specific terms applies.
- **"Spell" vs "Scroll"**: a Spell lives in a Tome and has charges. A Scroll is a one-time Consumable with no requirements. They can contain overlapping effects but are mechanically distinct.

---

## Undefined Terms (need definition added to GDD)

- **Quest ignore threshold** — how does the player know a Quest is about to be failed by non-attempt? Timer, AI Message, visual indicator? TBD.
- **Crafting** — mentioned in Between Floors and item taxonomy but system is TBD. (Separate spar topic)
- **Tag vocabulary** — Tags are confirmed as the synergy engine but no canonical tag list exists yet. Full tag vocabulary TBD during combat design.
- **Magical Affinity** — derivation from Int+Wis, thresholds, and brute-force unlock rate all TBD. Flagged open.
- **Dexterity, Intelligence, Wisdom** — visual effects confirmed; mechanical effects TBD.

---

## Example Usage

> *Designer to developer:* "When the player's Current Entertainment drops sharply below their Total Viewcount, Viewers should start decaying fast. Remember — it's an asymptotic curve with Viewer Lag, not a hard timer."

> *AI Message (correct tone):* "A Simultaneous Kill on four enemies. I designed that room specifically for that moment. You're welcome."

> *Design doc (correct):* "On Knocked Down, the player has a 30-second window before True Death. Spending Followers triggers Self-Revive. In a Party, teammates can revive for free within the same window."

> *Build system (correct):* "The Boon grants a Passive Ability with the `[shadow]` Tag. Combined with the player's existing `[on-kill]` Active Ability, a Tag interaction fires — shadows proc on every kill. That's a two-Tag synergy. The Tome spell they're running has a `[poison]` Tag. If they find the Boon that links `[shadow]` procs to `[poison]` stacks, that's the three-Tag jackpot."

> *Spell economy (correct):* "Player Overcasts the Cataclysmic spell — costs 500,000 Free Viewers, now Reserved. They have 200,000 Followers and 300,000 Free Viewers left. Boss dies. Crescendo fires. Release step: 200,000 Reserved Followers restored first. Then crystallisation converts 100,000 Free Viewers into new Followers. Net: back to 300,000 Followers, 300,000 Reserved still locked until floor transition."
