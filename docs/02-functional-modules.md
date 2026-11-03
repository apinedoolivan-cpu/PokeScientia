# Pokescientia — Functional Module Specification

**Draft 1 for review** · 2026-11-03 · Owner: @Alex

## Document status

Draft 1. Describes **what** each module does, from the user's point of view. It does not describe how it is built (architecture doc), where data comes from (data strategy), or how it looks (design spec).

- Decisions referenced as `D#` and requirements as `R#` live in [`01-vision-and-requirements.md`](01-vision-and-requirements.md).
- Open questions live in [`00-decision-map.md`](00-decision-map.md).
- Statements marked **Assumption** are proposals made while drafting. Confirm or correct them in review.
- Detail follows the phase: Phases 0–2 in full, Phase 3 in medium detail, Phases 4–6 as outlines. Later modules are detailed when their phase approaches.

### Feature IDs

Every feature has a stable ID: `<MODULE>-F<number>` (for example `ARC-F03`). Milestones, GitHub Issues and commit messages refer to these IDs. IDs are never reused; a removed feature keeps its ID with the status "Removed".

### Acceptance criteria format

Key features have criteria in **Given / When / Then** form. A feature is done when all its criteria pass, ideally as automated tests.

## Module map

| ID | Module | Code | Phase | Depends on |
| --- | --- | --- | --- | --- |
| M0 | Academy shell | `SHL` | 0 | M1 |
| M1 | Data pipeline | `DAT` | 0 | — |
| M2 | Archive (Pokédex) | `ARC` | 1 | M0, M1 |
| M3 | Strategy Hall | `STR` | 2 | M0, M1, M2 |
| M4 | Competitive data and calculator | `CMP` | 3 | M1, M2, M3 |
| M5 | Animation Lab | `LAB` | 4 | M1, M4 |
| M6 | Accounts | `ACC` | 5 | M3 |
| M7 | Quiz | `QUZ` | 6 | M1, M2 |
| M8 | AI assistant | `AIA` | 6 | M2, M3, M4 |

```
M1 Data pipeline ──► M2 Archive ──► M3 Strategy Hall ──► M4 Competitive data & calculator
        │                 │                │                       │
        │                 │                └──► M6 Accounts        └──► M5 Animation Lab
        │                 └──► M7 Quiz
        └──► M0 Academy shell (hosts every hall)          M8 AI assistant ◄── M2, M3, M4
```

---

## Cross-cutting capabilities

These rules apply to every module and are not repeated in module sections.

| ID | Capability | Rule |
| --- | --- | --- |
| X-01 | Languages | The whole interface exists in Spanish (default) and English (D1). Switching language keeps the current page by swapping the `/es/` or `/en/` prefix (D17). |
| X-02 | Game data language | Names and descriptions appear in the active language (D2). If a Spanish text is missing, the English text is shown and marked. |
| X-03 | Bilingual search | Any search box matches names in **both** languages, so "Lanzallamas" and "Flamethrower" find the same move. **Assumption.** |
| X-04 | Themes | Light and dark themes (D19). The default follows the operating system; a manual choice is remembered. |
| X-05 | Accessibility | WCAG 2.2 AA (D20): full keyboard use, visible focus, labels for screen readers, 4.5:1 text contrast, type information never shown by color alone. |
| X-06 | Reduced motion | With `prefers-reduced-motion` on, large motion becomes fades or is skipped; nothing essential depends on animation (D20). |
| X-07 | Responsive | Desktop-first, fully usable from 360 px width (A1). |
| X-08 | States | Every data view has loading, empty and error states, each with a clear message and, for errors, a way to retry. |
| X-09 | Shareable URLs | Every Pokémon, form, move, ability, item and hall has its own URL with stable English IDs (D17). |
| X-10 | Presenters | Each hall has a presenter: portrait plus a short introduction (D14). The introduction can be dismissed. |
| X-11 | Legal | Every page links to About; the unofficial fan-project disclaimer is always reachable (Constraints). |

**Acceptance criteria (cross-cutting)**

- *Given* I am on `/es/pokedex/charizard`, *when* I switch to English, *then* I land on `/en/pokedex/charizard` with all interface text in English.
- *Given* reduced motion is enabled in my OS, *when* I open any hall, *then* no element moves more than a fade or a short opacity change.
- *Given* I use only the keyboard, *when* I navigate any page, *then* I can reach and operate every control, and focus is always visible.

**Testing approach:** automated accessibility checks (axe) in end-to-end tests on every page type; an end-to-end test of the language switch; visual review of both themes.

---

## M0 — Academy shell (`SHL`) · Phase 0

**Purpose.** The frame of the site: the academy entrance, navigation between halls, global search, and site-wide settings.

### Features

| ID | Feature | Phase |
| --- | --- | --- |
| SHL-F01 | **Academy entrance (home).** The site's features presented as halls of the academy, each with its presenter, name and a one-line description. Search is visible from the entrance. | 0 |
| SHL-F02 | **Hall navigation.** Always available; shows which hall I am in. | 0 |
| SHL-F03 | **Global search.** One search box in the header, searching Pokémon (with forms), moves, abilities and items; results grouped by kind; opens the detail page. | 1 |
| SHL-F04 | **Language switch** (X-01). The last choice is remembered and used when visiting the site root. | 0 |
| SHL-F05 | **Theme switch** (X-04). | 0 |
| SHL-F06 | **About and credits.** Purpose, unofficial disclaimer, every data and asset source with its license, and the data version (DAT-F09). | 0 |
| SHL-F07 | **Not-found page**, in the academy style, with a way back. | 0 |
| SHL-F08 | **Presenter area** in each hall (X-10). | 0 |

### Rules

- Halls that don't exist yet are not navigable. Whether they appear as "closed doors" or are hidden is decided in the design spec.
- Global search shows at most a handful of results per kind, with a link to the full filtered list.
- The global search needs the Archive's data, so it arrives with Phase 1. In Phase 0 the search box is not shown.

### Data

Reads the search index (DAT-F10) and the list of halls. Stores language and theme preferences in the browser.

### Connections

Hosts every hall. Global search links into M2.

### Acceptance criteria

- **SHL-F01** *Given* I open the site root, *when* the page loads, *then* I see the available halls, each with presenter, name and description, and I can enter each one.
- **SHL-F03** *Given* the Archive exists, *when* I type "char" in the global search, *then* I see Charmander, Charmeleon, Charizard and any moves, abilities or items matching, grouped by kind, and I can open any result with the keyboard.
- **SHL-F04** *Given* I chose English last time, *when* I visit the site root, *then* I am sent to `/en/`.
- **SHL-F07** *Given* I open a URL that doesn't exist, *then* I see the not-found page in my language, with a link to the entrance.

**Testing approach:** end-to-end tests for navigation, search and settings; unit tests for the search ranking.

### Out of scope

User accounts in the header (M6), notifications, and a site-wide settings page beyond language and theme.

---

## M1 — Data pipeline (`DAT`) · Phase 0

**Purpose.** Produce all the game data the site needs, in Spanish and English, as static files built ahead of time (D18). This section defines **what** data must exist. Sources are chosen in the data strategy; the processing design is in the architecture doc.

### Features

| ID | Data | Phase |
| --- | --- | --- |
| DAT-F01 | **Pokémon and forms**, all generations: National Pokédex number, English ID, names (es/en), forms grouped under their number (D11), types, base stats, abilities (including hidden), height and weight, evolution chain with conditions, image URL, flags "fully evolved" and "competitive view". | 0 |
| DAT-F02 | **Moves**: ID, names and descriptions (es/en), type, category, power, accuracy, PP, priority, **target** (single, both foes, all others…; essential for doubles), and flags such as contact or sound. | 0 |
| DAT-F03 | **Abilities**: ID, names and descriptions (es/en). | 0 |
| DAT-F04 | **Items**: ID, names and descriptions (es/en), category. Only items that can be held in battle. **Assumption.** | 0 |
| DAT-F05 | **Learnsets**: the moves each Pokémon or form can learn. **Assumption:** the learnset of the current VGC game; for Pokémon not in that game, the latest game they appeared in, and the page says which game. | 0 |
| DAT-F06 | **Type chart** of the current generation. | 0 |
| DAT-F07 | **Competitive middle evolutions**: a short, hand-maintained list (e.g. Porygon2, Dusclops) included in the competitive view (D12). **Assumption.** | 0 |
| DAT-F08 | **Regulation data**: which Pokémon and forms are legal in the current VGC regulation, plus the format rules (level, team size, clauses). Kept in one file that is easy to update (R17). | 2 |
| DAT-F09 | **Data version**: the date the data was built and the game it reflects, shown in About. | 0 |
| DAT-F10 | **Search index**: names in both languages for every Pokémon, form, move, ability and item. | 1 |
| DAT-F11 | **Doubles move categories**: hand-maintained lists of moves for speed control, redirection, Fake Out, Protect-like moves, etc., used by STR-F11. | 2 |
| DAT-F12 | **Usage statistics** for the current regulation (see M4). | 3 |

### Rules

- Every entity has a stable English ID, used in URLs and references (D17).
- Data is split into small files loaded on demand (D18). A Pokémon page never loads the whole Pokédex.
- Images are referenced by URL, never stored in the repository (D18).
- Refreshing the data is a single, documented command run by hand (D18). Running it twice with the same sources gives the same files.
- Hand-maintained lists (DAT-F07, DAT-F08, DAT-F11) live in the repository as small, readable files.

### Acceptance criteria

- **DAT-F01** *Given* the pipeline has run, *then* every Pokémon from #1 to the latest has an entry with Spanish and English names, and Ninetales has two forms (standard and Alolan) under number 38.
- **DAT-F05** *Given* the pipeline has run, *then* every form has a learnset and a label of the game it comes from.
- **DAT-F09** *Given* the pipeline has run, *then* the data version file contains the build date and the source game.
- **General** *Given* the pipeline runs twice with the same sources, *then* the output files are identical.

**Testing approach:** validation tests on the generated files (schema checks, no missing IDs or names, references between files resolve); snapshot tests on a few known Pokémon.

### Out of scope

Live querying of external APIs from the browser (A4); data for spin-off games; anime or card-game data.

---

## M2 — Archive (`ARC`) · Phase 1

**Purpose.** The Pokédex: look up any Pokémon, move, ability or item, in Spanish or English, with a competitive emphasis.

### Features

| ID | Feature | Phase |
| --- | --- | --- |
| ARC-F01 | **Pokémon list.** Each item shows image, number, name and types. The competitive view is the default (D12); "Show all" reveals every Pokémon. | 1 |
| ARC-F02 | **List filters and sorting.** Filter by type (one or two), generation and name; sort by number, name, each base stat and stat total. The view, filters and sort are kept in the URL. | 1 |
| ARC-F03 | **Pokémon entry.** Independent sections (R16): header, base stats, abilities, type effectiveness, evolution chain, learnable moves (D10). | 1 |
| ARC-F04 | **Form selector.** Switches all sections to the selected form; each form has its own URL (e.g. `/pokedex/ninetales-alola`). | 1 |
| ARC-F05 | **Previous and next** entry by National Pokédex number. | 1 |
| ARC-F06 | **Moves list** with filters (type, category, name, and a "spread moves" filter) and sorting. | 1 |
| ARC-F07 | **Move detail page.** All move data and description, and the Pokémon that can learn it. | 1 |
| ARC-F08 | **Abilities list and detail page.** Description and the Pokémon that have it (regular or hidden). | 1 |
| ARC-F09 | **Items list and detail page.** Description and category. | 1 |
| ARC-F10 | **Type chart page.** Full 18×18 chart; pick one or two defending types to see what hits them. | 1 |
| ARC-F11 | **"Add to team" button** on a Pokémon entry (D28). | 2 |
| ARC-F12 | **Competitive section** in the entry: usage rank and common sets (D13). | 3 |

### Entry sections (ARC-F03)

| Section | Contents |
| --- | --- |
| Header | Image, number, name (active language, with the other language shown smaller), types, form selector |
| Base stats | Six stats with bars, and the total |
| Abilities | Each ability with a short description and a link to its page; hidden ability marked |
| Type effectiveness | Weaknesses (×4, ×2), resistances (×½, ×¼) and immunities. A note appears when an ability can change them (e.g. Levitate). |
| Evolution chain | Every stage with its condition (level, item, trade…), each linking to its entry |
| Learnable moves | Table of moves with type, category, power, accuracy and how it is learned; filterable and sortable; labelled with the game the learnset comes from (DAT-F05) |

### Rules

- A Pokémon is defined by its National Pokédex number; forms are shown within one entry (D11).
- The competitive view contains fully evolved Pokémon plus the hand-maintained middle evolutions (D12, DAT-F07).
- Display names follow the active language; links always use English IDs (D17).
- New sections can be added to the entry without changing existing ones (R16).

### Data

Reads DAT-F01 to DAT-F07 and DAT-F10. Writes nothing.

### Connections

Global search (M0) links here. ARC-F11 sends a Pokémon to the Strategy Hall (M3). M4 adds the competitive section (ARC-F12).

### Acceptance criteria

- **ARC-F01** *Given* I open the Pokédex, *then* I see the competitive view; Charizard and Porygon2 appear and Charmander doesn't. *When* I choose "Show all", *then* Charmander appears.
- **ARC-F02** *Given* I filter by Fire and sort by Speed, *when* I copy the URL and open it in a new tab, *then* I see the same filtered, sorted list.
- **ARC-F04** *Given* the Ninetales entry is open, *when* I select the Alolan form, *then* types, stats, abilities and moves change to Alolan Ninetales and the URL becomes `/pokedex/ninetales-alola`.
- **ARC-F03** *Given* the Gengar entry, *then* the type effectiveness shows Ground as ×2 and Normal and Fighting as immune.
- **ARC-F07** *Given* the Flamethrower page in Spanish, *then* it is titled "Lanzallamas" and lists Charizard among the Pokémon that learn it.
- **ARC-F10** *Given* I pick Water and Ground as defending types, *then* Grass shows ×4 and Electric shows ×0.

**Testing approach:** unit tests for type effectiveness and filtering logic; end-to-end tests for list, entry, form switch and detail pages in both languages; prerender check that every entity page is generated.

### Out of scope (for now)

Pokédex flavor text, locations and encounter data, sprites from every game, cries, and side-by-side comparison of Pokémon. Any of them can be added later as a new entry section (R16).

---

## M3 — Strategy Hall (`STR`) · Phase 2

**Purpose.** Build VGC teams, keep them in the browser, and understand their strengths and weaknesses.

### Features

| ID | Feature | Phase |
| --- | --- | --- |
| STR-F01 | **Team library.** List of saved teams (name, the six Pokémon, last edited). Create, rename, duplicate and delete (delete can be undone). | 2 |
| STR-F02 | **Team editor.** Up to six slots. Each slot: Pokémon and form, ability, held item, four moves, nature, stat spread, and the battle mechanic fields of the current game. Final stats at level 50 are calculated and shown. **Provisional:** spread and mechanic fields depend on the Q22 research. | 2 |
| STR-F03 | **Smart pickers.** Searchable choices for Pokémon, abilities, items and moves. Move choices come from the Pokémon's learnset. | 2 |
| STR-F04 | **Rule warnings** (D27). Warnings for duplicate species, duplicate items, Pokémon not legal in the regulation, moves not learnable, impossible abilities and invalid spreads. Warnings never block editing or saving. | 2 |
| STR-F05 | **Import from Showdown text.** Lines that can't be read are reported; the rest is imported. | 2 |
| STR-F06 | **Export to Showdown text**, with one-click copy. | 2 |
| STR-F07 | **Backup:** export all teams to a file and import them back. | 2 |
| STR-F08 | **Defensive analysis.** For each of the 18 attacking types: how many members are weak, resistant or immune; shared weaknesses are highlighted. Abilities that grant immunity (e.g. Levitate, Flash Fire) are counted. | 2 |
| STR-F09 | **Offensive coverage.** Which types the team's damaging moves hit super-effectively, and which types nothing hits super-effectively. | 2 |
| STR-F10 | **Speed tiers.** Each member's final Speed, ordered, with views for +1, −1, Tailwind and Choice Scarf, and a Trick Room view (reversed order). | 2 |
| STR-F11 | **Doubles essentials.** For each category (speed control, Fake Out, Intimidate, redirection, spread moves, Protect, priority) whether the team has it and which members provide it (DAT-F11). | 2 |
| STR-F12 | **Add from Archive.** Receives a Pokémon from ARC-F11 into a new or existing team (D28). | 2 |
| STR-F13 | **Live analysis.** All analyses update immediately as the team changes. | 2 |
| STR-F14 | **Autosave.** Changes are saved in the browser automatically; no "Save" button. **Assumption.** | 2 |
| STR-F15 | **Benchmarks.** Speed tiers compared against popular threats in the regulation. | 3 |
| STR-F16 | **Fill from common set.** Fill a slot with a common set from usage data. | 3 |

### Rules

- A team has at most six Pokémon; analysis works with any number from one to six.
- Format rules (level 50, species clause, item clause, legality) come from the regulation data (DAT-F08), not from code, so a new regulation needs only a data update (R17).
- Analysis covers all six members. In VGC you bring six and choose four per game; choosing four is not modeled.
- Teams live only in this browser until accounts exist (D3). The backup (STR-F07) is how they move between devices.
- The analysis functions are independent of the screens, so the calculator (M4) and the AI assistant (M8) can reuse them.

### Data

Reads Pokémon, moves, abilities, items, learnsets, type chart, regulation data and doubles move categories. Reads and writes teams in browser storage (storage technology: Q26).

### Connections

Receives Pokémon from M2. Feeds teams to M4 (calculator) and later M6 (sync) and M8 (assistant).

### Acceptance criteria

- **STR-F01** *Given* I delete a team, *when* I choose "Undo" in the message that appears, *then* the team is back unchanged.
- **STR-F04** *Given* two members hold Sitrus Berry, *then* a duplicate-item warning appears on both, and I can still keep editing and the team is still saved.
- **STR-F05** *Given* valid Showdown text for six Pokémon, *when* I import it, *then* the team has the same Pokémon, items, abilities, moves, natures and spreads. *Given* one line has an unknown move, *then* that line is reported and the rest is imported.
- **STR-F05/F06** *Given* a team, *when* I export it and import the text again, *then* the result is identical to the original.
- **STR-F08** *Given* a team with three Pokémon weak to Ground and none resistant or immune, *then* Ground is highlighted as a shared weakness. *When* I add a Levitate Pokémon, *then* it counts as immune to Ground.
- **STR-F10** *Given* a member with 100 final Speed, *when* I open the Tailwind view, *then* it shows 200.
- **STR-F11** *Given* a team with Tailwind on one member and no Fake Out, *then* speed control shows as covered by that member and Fake Out shows as missing.
- **STR-F14** *Given* I edit a team and reload the page, *then* my changes are still there.
- **STR-F12** *Given* the Garchomp entry, *when* I choose "Add to team" and pick a team with a free slot, *then* Garchomp appears in that team.

**Testing approach:** unit tests for stat calculation, every analysis and the Showdown parser (including round-trip tests with real exported teams); end-to-end tests for building, importing, exporting and reloading a team.

### Out of scope

Team sharing by link (needs M6), team-preview simulation (choosing four of six), opponent prediction, and damage calculations (M4).

---

## M4 — Competitive data and calculator (`CMP`) · Phase 3

**Purpose.** Bring real competitive data into the platform: what people actually use, and how much damage attacks do. Medium detail; specified fully before Phase 3 starts.

### Features

| ID | Feature | Phase |
| --- | --- | --- |
| CMP-F01 | **Usage overview.** Most used Pokémon in the current regulation, with usage rank and percentage. | 3 |
| CMP-F02 | **Common sets.** For each Pokémon: most used moves, items, abilities, spreads and teammates. Shown in the entry (ARC-F12) and usable to fill a team slot (STR-F16). | 3 |
| CMP-F03 | **Damage calculator.** Attacker against one or two defenders, with doubles conditions: spread-move reduction, weather, terrain, screens, Helping Hand, stat changes and the current game's battle mechanic. Result as a damage range in % and the chance to knock out. | 3 |
| CMP-F04 | **Calculator from a team.** Load attackers or defenders straight from a saved team. | 3 |
| CMP-F05 | **Speed benchmarks** feeding STR-F15. | 3 |
| CMP-F06 | **Usage trends** over time, if the data source allows it. | 3 (stretch) |

### Rules

- Usage data always shows its source, the period it covers and the format.
- Damage calculation uses an established open-source calculator library (Q33); we don't write our own formulas.

### Open questions

Q32 (usage data source and license), Q33 (calculator library). Both are researched in the data strategy document.

### Acceptance criteria (outline)

- **CMP-F03** *Given* a well-known matchup with published results, *then* our result matches the reference calculator within its rounding.
- **CMP-F02** *Given* usage data is loaded, *then* each common-set panel names its source and period.

**Testing approach:** comparison tests against the reference calculator for a set of known matchups; validation tests on the usage data files.

---

## M5 — Animation Lab (`LAB`) · Phase 4

**Purpose.** A place to explore web animation: a scripted doubles battle stage built with PixiJS and GSAP (D7). Outline; specified fully before Phase 4.

### Features

| ID | Feature | Phase |
| --- | --- | --- |
| LAB-F01 | **Doubles stage.** Two Pokémon per side on a battle field (D29). | 4 |
| LAB-F02 | **Battle sequence:** ball throw, entrance of all four Pokémon, a move, hit effect, HP bar change, optional faint. | 4 |
| LAB-F03 | **First version: a fixed demo scene.** Later, choosing the Pokémon and moves (D29). | 4 |
| LAB-F04 | **Real damage values** from the calculator (M4), closing Q5. | 4 |
| LAB-F05 | **Playback controls:** play, pause, replay, speed. A calm version for reduced motion (X-06). | 4 |
| LAB-F06 | **Effect library** by move type and category (generic effects per type, not one per move). | 4 |

### Rules

- Pokémon images come only from the chosen sources; all effects, fields and UI are original work.
- The lab is not a rules engine: it plays scripted scenes.

---

## M6 — Accounts (`ACC`) · Phase 5

**Purpose.** Sign in and keep teams in sync across devices, through the Go backend (D4). Outline.

- **ACC-F01** Sign in and sign out (method: Q6).
- **ACC-F02** First sign-in uploads existing local teams; the app keeps working offline and syncs later (D3).
- **ACC-F03** Conflicts between devices are shown to the user, never silently overwritten.
- **ACC-F04** Delete my account and all my data.
- **ACC-F05** Share a team by link.

---

## M7 — Quiz (`QUZ`) · Phase 6 candidate

**Purpose.** Test Pokémon knowledge in a playful way (D15). Outline; presenter idea: Zoroark.

- **QUZ-F01** Question types built from existing data: silhouettes, type matchups, "which is faster", ability or move identification.
- **QUZ-F02** Scores kept in the browser.

---

## M8 — AI assistant (`AIA`) · Phase 6 candidate

**Purpose.** An assistant that critiques teams and answers questions with evidence. Outline; model source: Q8.

- **AIA-F01** Team critique that cites the same analyses the Strategy Hall shows (STR-F08 to STR-F11) and, when available, usage data and damage calculations.
- **AIA-F02** Every claim points to the data it comes from.

**Requirement for earlier phases:** analyses and calculations must be callable without the user interface (see M3 rules), so the assistant can use them later without rewrites.

---

## Assumptions introduced in this draft

Confirm or correct each in review.

| Where | Assumption |
| --- | --- |
| X-03 | Search matches names in both languages. |
| DAT-F04 | The Archive lists only items that can be held in battle. |
| DAT-F05 | Learnsets come from the current VGC game, or the latest game the Pokémon appeared in, labelled. |
| DAT-F07 | Competitive middle evolutions are a short hand-maintained list. |
| STR-F14 | Teams autosave; there is no "Save" button. |
| LAB-F03 | The lab starts with a fixed demo scene, then adds choices (owner had no preference). |
