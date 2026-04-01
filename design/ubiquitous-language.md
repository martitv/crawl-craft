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
| **Intelligence** | Non-combat stat (exact mechanic TBD). Visually: character's head grows larger at high values. | INT |
| **Wisdom** | Non-combat stat (exact mechanic TBD). Visually: character's beard grows longer at high values. | WIS |
| **XP** | Resource gained through actions that triggers Level-ups when thresholds are reached. Exact mechanic TBD. | Experience, Experience points |

---

## Audience System

| Term | Definition | Aliases to avoid |
|------|------------|-----------------|
| **Entertainment Value (EV)** | A core build stat that determines how effectively a player converts spectacular actions into Viewers. Does not affect combat directly. Items and abilities carry EV ratings. | Charisma, Hype stat, Entertainment stat |
| **Current Entertainment** | The real-time entertainment output the player is producing right now. Calculated from EV stat × recent actions. Distinct from EV (which is a static stat). Current Entertainment sets the target Viewcount the Viewer count trends toward. | EV (do not conflate with the stat), Live entertainment |
| **Viewers** | The volatile, real-time audience hype stat. Spikes on spectacular actions; decays during inactivity. Forms the "buff" layer of Total Viewcount. | Live viewers, View count (two words) |
| **Viewer Spike** | A sudden sharp increase in Viewers triggered by a high-EV action, Crescendo, or other spectacular moment. | Hype spike, Viewer burst |
| **Target Viewcount** | The Viewer count that the system asymptotically trends toward, set by the player's Current Entertainment. Not a displayed stat — an internal system concept. | Target viewers, Expected viewers |
| **Followers** | Crystallised, permanent Viewers accumulated through Crescendo moments. Forms the "flat base" layer of Total Viewcount. Powers self-revive. | Permanent viewers, Fans, Subscribers |
| **Total Viewcount** | The combined stat used by all systems: `Total Viewcount = Followers + Viewers`. Everything that scales with audience size reads from this number. | Viewership (retire), View count (retire), Total viewers |
| **Crystallisation** | The process of converting a portion of current Viewers into permanent Followers, triggered by a Crescendo moment. Rate scales with current Follower count. | Conversion, Locking in |
| **Crescendo** | A moment that triggers Crystallisation: completing a quest, killing a boss, finishing a Sponsor challenge. The "payoff" beat of an arc of entertainment. | Milestone, Completion trigger |
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
| **AI Offer** | A rare option injected by the AI into the Level-Up pool. Visually distinct. Higher risk, higher EV modifier, occasionally the only access path to rare ability tiers. Not the same as an AI Wildcard. | Director offer, Special offer |

---

## Between Floors

| Term | Definition | Aliases to avoid |
|------|------------|-----------------|
| **Sponsor** | An entity that offers the player a floor contract during the Between Floors phase. | Advertiser, Patron, Quest giver |
| **Sponsor Offer** | One of 3 choices presented to the player on entering a new floor. Each contains a Sponsor Challenge and associated items/bonuses. | Sponsor deal, Contract offer |
| **Sponsor Challenge** | The specific task a Sponsor wants the player to complete on the upcoming floor. Completing it triggers a Crescendo. | Sponsor quest, Floor objective, Contract task |
| **Sponsor Pool** | The collection of possible Sponsor Offers for a given floor. Contains neutral sponsors, build-relevant sponsors, and occasionally an AI Wildcard. | Offer pool |
| **AI Wildcard** | An occasional Sponsor Offer injected into the Sponsor Pool by the AI. Riskier and more unusual than standard offers; written in the AI's voice. Distinct from an AI Offer (which is in the Level-Up pool). | AI Sponsor, Wildcard sponsor |
| **Level-Up** | A progression event triggered when XP thresholds are reached. Presents the player with a pool of options to choose from (stats, passives, abilities, rare AI Offers). | Skill up, Power up, Level |
| **Level-Up Pool** | The set of options presented during a Level-Up. Composed of neutral picks, sponsor-influenced picks, and rare AI Offers. | Option pool, Upgrade pool |
| **Social Room** | The shared post-Mega Boss space accessible to all participants before the next floor opens. Contains the Loot Shrine, Dueling Pit, recruitment, and Highlights TV. | Post-boss room, Lobby, Hangout |
| **Loot Shrine** | A Social Room object where players can sacrifice items for group-wide buffs. A collective coordination moment. | Sacrifice altar, Offering shrine |
| **Dueling Pit** | The opt-in PvP area within the Social Room. Players compete for unique loot stakes. Entirely optional; double-confirmed consent required. | Arena, PvP zone |
| **Highlights TV** | The TV object in the Social Room that plays Highlight reels from the Mega Boss fight just completed. | Replay screen, Highlight reel |

---

## Bosses & Combat

| Term | Definition | Aliases to avoid |
|------|------------|-----------------|
| **Boss** | An optional, named enemy encounter on a floor. Solo/party content. Killing a boss triggers a Crescendo. | Elite boss, Floor boss |
| **Mega Boss** | A large-scale boss encounter that triggers an open-queue alert to other players. Shared-world event; distinct in scale and design from standard Bosses. | World boss, Raid boss, Event boss |
| **Mini-boss** | A mid-floor enemy capable of dropping the Key. Smaller in scope than a Boss. | Elite enemy, Champion |
| **Knocked Down** | The temporary downed state entered on first death before true death. Opens a window for self-revive (spending Followers) or teammate revive (co-op, 30-second window). | Downed, Dead, Defeated |
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
- A **Mega Boss** is a special type of Boss that triggers an **Open Queue** via a **Mega Boss Alert**
- **Between Floors** occurs after every **Floor** and always before the next **Floor** begins
- The **Social Room** is a special phase of **Between Floors** that only occurs after a **Mega Boss** kill
- **Entertainment Value (EV)** determines the ceiling of **Current Entertainment**; **Current Entertainment** drives the **Target Viewcount**; **Viewers** trend asymptotically toward **Target Viewcount**
- **Viewers** + **Followers** = **Total Viewcount**
- A **Crescendo** triggers **Crystallisation**, converting **Viewers** into **Followers**
- **Clout** = **Followers** × **Depth** + **Highlight Bonus**, calculated at **Run** end
- **AI Mood** is a function of **Plan Adherence** + **Current Entertainment**
- **AI Offers** appear in the **Level-Up Pool**; **AI Wildcards** appear in the **Sponsor Pool** — these are distinct things

---

## Flagged Ambiguities

- **"Viewership"**: used once in the GDD ("low Viewership accumulating"). Retire in favour of **Total Viewcount** for the combined stat or **Viewers** for the live component. Do not use "viewership" as a term.
- **"Multi-kill"**: used colloquially but ambiguous between Chain Kill and Simultaneous Kill. Use the specific term.
- **"AI Offer" vs "AI Wildcard"**: these sound similar but are different systems. **AI Offer** = rare injection into the Level-Up pool. **AI Wildcard** = rare injection into the Sponsor Pool. Always use the full term; never shorten to "AI option" or "AI pick."
- **"Loadout" vs "Build"**: Loadout = a pre-configured starting set (a Clout unlock). Build = the emergent result of a full run. Do not use these interchangeably.
- **"Contestant" vs "Player character"**: use "contestant" in in-world text (flavour, AI Messages, quest descriptions). Use "player" or "player character" in design docs. Never use "hero."

---

## Undefined Terms (need definition added to GDD)

- **XP** — mentioned as the Level-Up trigger resource but never defined. How is it earned? From kills, quest completions, floor clears?
- **Dexterity, Intelligence, Wisdom** — listed as stats with visual effects but mechanical effects are TBD. Need stub definitions once decided.
- **Contestant** — used once as the in-world player term. Should be formally adopted or retired.
- **Quests** — referenced throughout but never formally defined as a system. Are they procedural? AI-authored? What is their structure?
- **Crafting** — mentioned as part of Between Floors but never described.

---

## Example Usage

> *Designer to developer:* "When the player's Current Entertainment drops sharply below their Total Viewcount, Viewers should start decaying fast. Remember — it's an asymptotic curve with Viewer Lag, not a hard timer."

> *AI Message (correct tone):* "A Simultaneous Kill on four enemies. I designed that room specifically for that moment. You're welcome."

> *Design doc (correct):* "On Knocked Down, the player has a 30-second window before True Death. Spending Followers triggers Self-Revive. In a Party, teammates can revive for free within the same window."
