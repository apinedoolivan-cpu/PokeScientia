# Pokescientia — Data Strategy

**Version 1.9 — approved 2026-11-25** · Owner: @Alex

## Document status

Version 1.9, approved. Defines where every piece of data comes from, under which license, how it is kept current, and the risks. Research done on 2026-11-04; source versions checked that day are listed in [Sources](#sources).

- Decisions (`D#`) and requirements (`R#`) live in [`01-vision-and-requirements.md`](01-vision-and-requirements.md); feature IDs (`DAT-F05`…) in [`02-functional-modules.md`](02-functional-modules.md).
- Proposals DS-1 to DS-9 were reviewed and approved on 2026-11-04 (some revised). Section 14 maps each one to its decision (`D35`–`D44`).
- How the pipeline is built (scripts, folders, schedules) belongs to the architecture doc. This document covers **what** comes from **where**.
- Version 1.5 adds PokéPaste (D95) as an external service for importing and exporting teams. It is not a data source: it carries the user's own teams, only when the user asks.
- Version 1.7 adds official tournaments for the CIRCUS (D104), in section 15: hand-curated results and team lists, and videos embedded from Pokémon's YouTube channel.
- Version 1.4 moves the AI assistant to Phase 7 (D86). What users write in the FORUM (Phase 6) is not game data: its storage and legal handling are specified with Phase 6 (Q86).

## Summary

| Need | Source | License | Decision |
| --- | --- | --- | --- |
| Game mechanics: Pokémon, forms, stats, abilities, moves, battle items, learnsets, formats | Pokémon Showdown data, through the `@pkmn/dex` and `@pkmn/mods` packages | MIT | D36 |
| Spanish and English names, descriptions, evolution conditions, Pokédex numbers, the full item list with categories | PokéAPI raw data (CSV files in its GitHub repository) | BSD-style | D36 |
| Current game and regulation | Pokémon Champions, Regulation Set M-C, from Showdown's Champions data | MIT | D35, D38, D39 |
| Images | PokéAPI sprites repository, linked through `raw.githubusercontent.com` | Images © The Pokémon Company; repository CC0 | D40 |
| Usage statistics (Phase 3) | Smogon's monthly statistics for Showdown's Champions VGC ladder | Aggregated stats: public domain | D41 |
| Damage calculator (Phase 3) | `@smogon/calc` as the engine; our own calculator experience on top | MIT | D42 |
| Browser storage (Phase 2) | localStorage for preferences, IndexedDB through Dexie for teams | Dexie: Apache-2.0 | D43 |
| Official VGC tournaments (Phase 3): events, team lists, top players, videos | Hand-curated from official results (Play! Pokémon, RK9), cross-checked with community sources; videos embedded from Pokémon's official YouTube channel | Facts, credited; videos under YouTube's terms, never copied | D104 |

## 1. The current competitive context (Q22)

Official VGC moved from Scarlet and Violet to **Pokémon Champions** in 2026. Champions launched on April 8, 2026 (Switch; mobile on June 17), and Play! Pokémon uses it for official events from May 2026 ([Wikipedia](https://en.wikipedia.org/wiki/Pok%C3%A9mon_Champions)).

| Regulation | Dates (2026) | Notes |
| --- | --- | --- |
| M-A | April 8 – June 17 | First Champions set |
| M-B | June 17 – September 9 | |
| **M-C** | **September 9 – December 2** | Current. Adds Pokémon and six Mega Evolutions, including new "Z" Megas ([The Pokémon Company press release](https://asia-press.portal-pokemon.com/press-release/pokemon-champions_20260830/), [Victory Road](https://victoryroad.pro/champions-regulations/)) |
| Next | From December 2 | Not announced on 2026-11-04 |

**Format rules** (Showdown's in-game "Flat Rules" for Champions): doubles, bring 6 and pick 4, level 50, species clause, item clause, no Mythical or Restricted Legendary Pokémon, open team sheets.

**Mechanics that change the team builder (STR-F02):**

| Mechanic | Champions | Earlier games |
| --- | --- | --- |
| Stat investment | **Stat Points**: 66 per Pokémon, at most 32 per stat; each point adds 1 to the stat at level 50 | EVs (510 total, 252 per stat) |
| IVs | Fixed at 31; not shown | 0–31 per stat |
| Natures | Kept (called Stat Alignments; 21 options) | 25 natures |
| Battle gimmick | **Mega Evolution**, one per battle, with Mega Stones | Terastallization (Scarlet and Violet) |

Sources: [Champsdex guide](https://champsdex.com/posts/pokemon-champions-ev-iv-stats-guide-2026/); confirmed in Showdown's code, whose Champions validator requires all IVs at 31 and rejects more than 32 Stat Points in a stat. Terastallization is not active in M-C and may arrive in a later set.

**DS-3 (revised in review), approved as D38: both stat systems, chosen per team.**

- Each team chooses its stat system: **Stat Points** (Champions: 66 total, at most 32 per stat, IVs fixed at 31) or **EVs and IVs** (earlier games: 510 total, at most 252 per stat, IVs 0–31). New teams use Stat Points. The choice is independent of the team format (D32).
- All teams use natures and level 50.
- A **converter** shows any spread in both systems. At level 50 with IVs at 31, the first Stat Point equals 4 EVs and each further point equals 8 EVs, so `EVs = 8 × SP − 4` (for SP ≥ 1). This follows Showdown's Champions stat formula.
  - Stat Points to EVs is always exact.
  - EVs to Stat Points is exact for most spreads. It warns when an IV is not 31, and when the converted total goes over 66, asking which stat to trim.
- Damage is always calculated with the current game's mechanics (Champions). EV-based stats are calculated with the classic formula, which at level 50 gives the same stats as the equivalent Stat Points.

## 2. Sources evaluated (Q1)

| Source | What it provides | Strengths | Weaknesses |
| --- | --- | --- | --- |
| **Pokémon Showdown data** (`@pkmn/dex`, `@pkmn/mods`, v0.10.13, updated 2026-11-03) | Species, forms, base stats, types, abilities, moves (target, priority, flags), battle items, learnsets of every generation, formats and legality, a Champions mod | Exactly the mechanics competitive tools use; IDs match Showdown team texts and `@smogon/calc`; Champions support (current and previous regulation); MIT | English only; few encyclopedic details |
| **PokéAPI** (raw CSV in GitHub repo, updated 2026-11-02) | Names and descriptions in many languages, evolution chains and conditions, Pokédex numbers, generations, item categories and flags, learnsets per game (including a Champions version group) | Spanish names for all 1,025 species and 919 moves; downloadable files, no API calls needed; BSD-style license | Newest entries lack Spanish; item "holdable" flags incomplete (Mega Stones not flagged); mechanics less detailed |

Neither source is enough alone: Showdown has the mechanics but no Spanish; PokéAPI has Spanish but weaker mechanics. This confirms the "mix of sources" in D18.

**DS-1, approved as D36: one master per kind of data.** Each field comes from exactly one source, so the two never disagree silently.

| Data (feature) | Master | Other source used for |
| --- | --- | --- |
| Pokémon and forms: types, base stats, abilities, weight (DAT-F01) | Showdown | — |
| Pokémon: Pokédex number, generation, height, evolution chain and conditions (DAT-F01) | PokéAPI | — |
| Names and descriptions, Spanish and English (DAT-F01–F04) | PokéAPI | Showdown English names as fallback |
| Moves: type, category, power, accuracy, PP, priority, target, flags (DAT-F02) | Showdown | — |
| Abilities (DAT-F03) | Showdown | — |
| Items: which items appear and their category (DAT-F04) | PokéAPI (every item, D100) | Showdown marks the battle items and gives their battle data (D100, D101) |
| Items: availability in the current game, Mega form, species-specific holder (DAT-F04) | Showdown Champions mod | — |
| Learnsets (DAT-F05) | Showdown | — |
| Type chart (DAT-F06) | Showdown | — |
| Legality and format rules (DAT-F08) | Showdown Champions mod | Hand-maintained regulation file for name and dates |
| Smogon tiers: Champions singles, National Dex, Doubles (DAT-F14) | Showdown (`tier` in the Champions mod, `natDexTier`, `doublesTier` of each generation) | — |
| VGC usage history (DAT-F15, Phase 3) | Smogon's statistics archive | — |
| Search index (DAT-F10) | Built from the above | — |

**Items (D100, D101).** Checked on 2026-11-21 in `@pkmn/dex` and `@pkmn/mods` (0.10.13 and 0.11.0 give the same counts):

| | Count |
| --- | --- |
| Items in PokéAPI's data (2026-11-04) | 2,223 (2,218 with a Spanish name) |
| Items in Showdown's data (battle items) | 587 |
| Available in Champions (no `isNonstandard` flag in the Champions mod) | 166 |
| Marked `Past` (earlier games only) | 408 |
| Other flags (`Future`, `Legends`, `CAP`, `Unobtainable`) | 13 |

- A **battle item** is an item present in Showdown's data. PokéAPI's "holdable" flag is not used to decide it, because it is incomplete (Mega Stones are not flagged).
- Showdown's data includes Poké Balls (marked `Past` in Champions); they still count as battle items and get the full page.
- Spanish descriptions are less complete than names, so more item pages fall back to English, marked (X-02, D44). The build report lists every fallback.
- Showdown's Champions data says whether an item is available **now**, not since which regulation, and its count (166) is higher than the 117 items third-party sites listed for M-A. The difference may be the items added in M-B and M-C, or Mega Stones in the game but not in the current regulation. Both are checked in Q93.

PokéAPI is used through its **raw data files**, never through the live API, so its fair-use limits don't apply and builds don't depend on its servers.

## 3. Identifiers and mapping

The two sources name things differently. For example, Showdown uses `ninetalesalola` and PokéAPI uses `ninetales-alola`.

**DS-2, approved as D37: public IDs follow PokéAPI's hyphenated style** (`ninetales-alola`, `fake-out`, `sitrus-berry`). They are readable in URLs (D17) and match the image file names. Each entity also stores its Showdown ID internally, for team import and export and for the calculator.

The pipeline matches the two sources automatically by comparing names without hyphens or spaces, plus a small **hand-maintained mapping file** for the exceptions. Any entity that can't be matched stops the build with a clear message, so nothing is lost silently.

IDs are treated as opaque text everywhere (architecture guideline, see parked idea P1).

## 4. Languages (D2, X-02)

Spanish coverage in PokéAPI on 2026-11-04:

| Entity | Total | With Spanish name |
| --- | --- | --- |
| Species | 1,025 | 1,025 |
| Moves | 919 | 919 |
| Abilities | 314 | 311 |
| Items | 2,223 | 2,218 |

Descriptions are less complete (for example, 826 moves have a Spanish description). The gaps are mostly the newest content: for example, the Champions ability Aura Guard and the form Mega Absol Z exist only in English.

**DS-9, approved as D44: Spanish overrides file.** A small hand-maintained file supplies official Spanish names missing from PokéAPI. Anything still missing falls back to English, marked as such (X-02). The build reports every fallback, so the list of gaps is always visible.

## 5. Learnsets and team formats (D32)

D32 needs two things: every move a Pokémon has ever learned, and whether each move is available in the current game.

- **Every game:** Showdown's learnsets list each move with codes per generation and method (for example `9M` = generation 9 by TM, `8L` = generation 8 by level). The pipeline keeps the generations and methods.
- **Current game:** Showdown's Champions mod has its own learnsets (about 260 species) and legality data (about 350 species and forms usable in Champions). A move is "available in the current game" when it appears in the Champions learnset.

**DS-4, approved as D39:** learnset detail is kept **per generation**, not per individual game. That is enough for "learned in any game" and "available now", and it keeps the data smaller. PokéAPI also offers per-game learnsets if more detail is ever wanted.

## 6. Keeping up with regulations (R17)

The current set, M-C, ends on December 2, 2026, so the first update will come soon. Updating is a data task, not a code change:

1. Update `@pkmn/dex` and `@pkmn/mods` to a version that includes the new regulation. So far Showdown has added each Champions regulation: M-B and M-C are both in its data.
2. Edit the regulation file: name, dates, Showdown format ID.
3. Run the pipeline by hand (D18) and check its report.
4. In Phase 3, usage statistics for the new format appear after its first full month.

Package versions and the PokéAPI commit are pinned, so the same inputs always give the same output (DAT acceptance criteria).

## 7. Images (Q23)

| Image set (PokéAPI sprites repository) | Looks like | Used for |
| --- | --- | --- |
| Official artwork (about 1,540, including forms) | Large, high-quality illustrations | Pokédex entry header, presenters, academy entrance |
| Default sprites | Small 96×96 in-game sprites | Lists, search results, team slots: light and fast |
| Animated battle sprites, **front and back** (about 1,470 each) | Animated images | Battle stage, COLOSSEUM (Phase 4): front for the opponent, back for your side |
| HOME renders | 3D-style renders, with shiny and female variants | Optional alternative to artwork |
| Per-game sprites | Sprites from each generation's games | Possible future entry section (R16) |
| Item sprites and type icons | Small icons | Item lists, type badges |
| Dream World | Vector art, older generations only | Not used |

**DS-5, approved as D40: link images from PokéAPI's repository through `raw.githubusercontent.com`, pinned to a commit.** This is the address PokéAPI itself gives to applications. Pinning prevents a repository change from breaking images. If an image fails to load, an original placeholder is shown.

Not used:

- **Showdown's sprite server:** the `@pkmn/img` documentation strongly asks projects to host their own copies instead, to avoid raising Showdown's bandwidth costs.
- **jsDelivr CDN:** its terms forbid using it as a general media host and forbid content that violates others' proprietary rights.

**Licensing note.** The sprites repository is CC0, but it states that "all image contents within are Copyright The Pokémon Company". The images are **not** free-licensed. Pokescientia uses them the way fan sites do: non-commercially, credited, with the disclaimer, and complying promptly with any takedown request. Being non-commercial lowers the risk a lot, but it relies on the rights holder's tolerance, not on a license. R18 was reworded accordingly: it covers the assets we add, not official Pokémon images.

**Update 2026-11-11 (D79).** The Pokémon Company's support page says it is "not in a position to review requests to use the Pokémon intellectual property" and asks projects not to use it. There is no permission to rely on, only tolerance. As a safeguard, every official image goes through one image service with an original fallback, and one setting replaces them all (X-15).

**Risk:** GitHub's raw file service is not a CDN and may throttle heavy traffic. For a personal site this is acceptable. If the site is deployed publicly and grows, revisit (for example, mirroring to the free host chosen in Q7).

## 8. Usage statistics (Q32, Phase 3)

Smogon publishes monthly statistics for Showdown's ladder formats. They include usage %, moves, items, abilities, spreads and teammates, which covers common sets (CMP-F02). The current format's ID on Showdown is `gen9championsvgc2026regmc`.

**DS-6, approved as D41:** use Smogon's monthly statistics for the current Champions VGC format, downloaded by the pipeline. Use only the **aggregated numbers**. The `@pkmn/smogon` project describes them as "freely available in the public domain", while Smogon's written sets and analyses are "copyrighted by Smogon and its contributors", so those are not used.

Limits to state in the interface (CMP rules):

- The data comes from Showdown's ladder, not from the in-game ranked mode or official tournaments. Sites like MunchStats read in-game data but publish no license, so they are not used.
- Statistics appear monthly, about a month behind.
- This session's network could not reach Smogon's servers, so the exact file format will be confirmed when Phase 3 starts.

**VGC usage history (D83, DAT-F15).** The same archive keeps past months for earlier VGC formats. The pipeline reads one rating cut-off for every VGC format, keeps each Pokémon's best rank with its format and month, maps old names to our IDs (D37), and writes one small file; the site never loads the archive. *Assumption:* the archive covers VGC formats from several generations; its real extent, the cut-off and the download size are confirmed in M3.3.

## 9. Damage calculator (Q33, Phase 3)

**DS-7 (revised in review), approved as D42: `@smogon/calc` is the damage engine; Pokescientia builds its own calculator on top.**

`@smogon/calc` (v0.12.0, MIT, updated 2026-09-18) is a modernized, library version of Honko's original damage calculator, the same lineage as the [NCP VGC Damage Calculator](https://nerd-of-now.github.io/NCP-VGC-Damage-Calculator/) (MIT) used as the reference for this module. The library has no interface; everything on screen is ours. It implements Champions mechanics (its own Champions calculation and Stat Point formula) and classic EV stats.

What the engine provides (checked in its code):

- All 16 damage rolls, per hit for multi-hit moves; % range.
- KO chances (OHKO, 2HKO…) with exact probability, including hazards, end-of-turn damage and healing items; recoil and drain.
- Doubles field: Helping Hand, Friend Guard, Tailwind, screens, Protect, Gravity, Magic Room, Wonder Room, Ruin abilities, auras, Battery, Power Spot, Steely Spirit, Flower Gift, Stealth Rock, Spikes; weather (including extreme) and terrain.
- Pokémon state: boosts −6 to +6, status, current HP, ability on or off, item, Tera type, allies fainted, weight. Move options: critical hit, hits, times used, overrides.

What Pokescientia builds on top (CMP features in the module spec):

- Matchup grid: both Pokémon, all four moves each way.
- Scenario comparison: the same attack under different conditions, side by side.
- Roll distribution chart.
- Combined damage: two attackers on one target in the same turn, with an exact combined KO chance (our own probability math).
- Accuracy-adjusted KO chances (our own math).
- One attack against the most-used Pokémon in the regulation (with usage data).
- A step-by-step explainer of how damage is calculated, using the engine's description of applied modifiers and our own stat code.

Not in the engine: a few niche field effects some calculators offer (Sea of Fire, Swamp, G-Max fields, custom multipliers). A custom modifier can be added on our side if needed.

Stat formulas (both systems and the converter, DS-3) are written by us, because the team editor needs them anyway; they are tested against the engine's results.

## 10. Browser storage (Q26, Phase 2)

| Data | Storage | Why |
| --- | --- | --- |
| Language, theme, dismissed presenters | localStorage | Tiny values, read on startup |
| Teams (STR-F01, STR-F14) | IndexedDB, through **Dexie** (Apache-2.0) | Structured, large, asynchronous; Dexie makes it simple |
| Pokédex data for offline use | Service worker cache | Later, optional |

**DS-8, approved as D43:** adopt this split, and ask the browser for persistent storage so teams aren't cleared under storage pressure. Backup export (STR-F07) remains the safety net. This closes Q26.

## 11. AI integration (Phase 7)

The AI assistant (M8) is deferred (R6); its model source is Q8. The only requirement for now, already in the module spec: analyses and calculations must work without the interface, so the assistant can call them later. The assistant must cite the same data sources listed here.

## 12. Licenses and credits

The About page (SHL-F06) credits:

| Source | License | Credit |
| --- | --- | --- |
| Pokémon Showdown data (via `@pkmn`) | MIT | Pokémon Showdown and its contributors; pkmn |
| PokéAPI data | BSD-style | PokéAPI and its contributors |
| PokéAPI sprites | Repository CC0; images © The Pokémon Company | PokéAPI sprites; The Pokémon Company |
| Smogon usage statistics | Aggregated statistics, public domain | Smogon University / Pokémon Showdown |
| Smogon tiers (in Showdown's data) | MIT, as part of the Showdown data | Smogon University (tiering) |
| `@smogon/calc` | MIT | Smogon |
| Dexie | Apache-2.0 | Dexie.js |
| PokéPaste (service used to import and export team links, D95) | Source code BSD-style; pastes are their authors' | PokéPaste, by Felix Friedlander |
| Official results, team lists and Championship Points (D104) | Facts; no license published | Play! Pokémon (The Pokémon Company International); RK9 |
| Tournament videos, through YouTube's embedded player (D104) | YouTube API Services Terms; videos are their owner's | The Pokémon Company, on YouTube |

Plus the unofficial fan-project disclaimer (README, Constraints).

## 13. Risks

| Risk | Impact | Mitigation |
| --- | --- | --- |
| A source changes its data format | Pipeline fails | Pinned versions; validation in the pipeline (DAT tests) |
| Spanish missing for new content | English shown in places | Overrides file (DS-9); build report lists gaps |
| Name mismatches between sources | Missing or wrong entries | Mapping file; unmatched entities stop the build |
| A new regulation brings a new mechanic (e.g. Terastallization) | Team builder needs new fields | Planned as a code change when announced; formats otherwise data-driven |
| GitHub throttles image links | Images fail under heavy use | Placeholders; revisit hosting if the site grows |
| Usage data only covers Showdown's ladder | Common sets differ from in-game trends | Source and period always shown |
| Takedown request from a rights holder | Content removed | Non-commercial, credited, disclaimer; comply promptly |
| PokéPaste is down, changes its addresses or closes (its code was last changed in 2021) | Link import and export stop working | Pasting Showdown text always works (STR-F05, STR-F06); errors say so; tests use recorded responses (D95) |
| Sources disagree on a result right after an event | A wrong winner or team in the CIRCUS | Wait for the official results; cross-check two sources before adding an event (D104) |
| A tournament video is removed or can't be embedded | Empty player | A link to watch it on YouTube; the panel and the teams still show (CIR rules) |
| A player asks to be removed from the CIRCUS | Personal data shown against their wish | Remove them promptly (D104) |

## 14. Approved proposals

All approved on 2026-11-04 and recorded in the vision document.

| ID | Proposal | Decision | Closes |
| --- | --- | --- | --- |
| — | Current official game is Pokémon Champions; the current regulation is set in one regulation file | D35 | Q22 |
| DS-1 | Showdown data (`@pkmn`) is master for mechanics; PokéAPI raw files are master for languages and encyclopedic data; one master per field | D36 | Q1 |
| DS-2 | Public IDs follow PokéAPI's hyphenated style; Showdown IDs stored internally; mapping file for exceptions | D37 | — |
| DS-3 | Both stat systems, chosen per team (Stat Points by default); converter between them; damage always with Champions mechanics | D38 | Q22 |
| DS-4 | Learnsets kept per generation and method; "current game" means the Champions learnset | D39 | Q22 |
| DS-5 | Images linked from PokéAPI's sprite repository via `raw.githubusercontent.com`, pinned to a commit, with placeholders; R18 reworded | D40 | Q23 |
| DS-6 | Smogon monthly aggregated statistics for the Champions VGC format; no Smogon written content | D41 | Q32 |
| DS-7 | `@smogon/calc` as the damage engine, with our own calculator experience on top | D42 | Q33 |
| DS-8 | localStorage for preferences, IndexedDB via Dexie for teams, persistent storage requested | D43 | Q26 |
| DS-9 | Hand-maintained Spanish overrides file; English fallback marked and reported | D44 | — |
| — | Every item from PokéAPI, battle items marked and completed from Showdown; availability in the current game from the Champions mod (approved 2026-11-21) | D100, D101 | — |
| — | Official tournaments hand-curated from official results, team lists from RK9, videos only embedded from Pokémon's YouTube channel; covered only where every replay's teams are public (approved 2026-11-24) | D104 | Q94 |

## 15. Official tournaments (Phase 3, D104)

The CIRCUS (M10) shows the big official VGC events. No source offers them as open data: official results and team lists are published as web pages, and community sites publish no license. So the data is **hand-curated**, a few events a season, in one file in `pipeline/manual/` that the pipeline validates (DAT-F16).

| Data | Comes from | How it is used |
| --- | --- | --- |
| Event facts: name, dates, place, regulation, winner | Pokémon's official event pages, cross-checked with Victory Road or Liquipedia | Typed by hand, with a link to the source |
| Team lists | RK9, the official registration and pairings system, which publishes the open team lists during the event | Copied by hand for the two players of each replay, with a link |
| Top players | The official Championship Points standings, Masters division | The top of the standings, by hand after each big event, with its date and a link |
| Videos | Pokémon's official YouTube channel (`@Pokemon`), which broadcasts VGC at every big event | Only the video ID is stored; the video plays in YouTube's embedded player |

**Open team lists set the coverage.** TPCi events have used open team lists since the 2023 season, and the 2026 handbook keeps them for Pokémon Champions. A list shows each Pokémon's species, ability, item and moves (plus Tera Type in Scarlet and Violet), never its stats. Because an event is covered only when every replay can show both teams (D104), the archive starts at the 2023 season at most; earlier events come in only if their teams can be found complete (Q95).

**Embedding.** YouTube's embedded player is governed by the YouTube API Services Terms. It is used in privacy-enhanced mode (`youtube-nocookie.com`), where views don't personalize the viewer's YouTube experience, and it loads only when the user presses play. YouTube requires the page to send its address (an HTTP Referer), or embedded videos refuse to play, and its minimum functionality rules forbid covering the player. The videos stay on Pokémon's channel: nothing is downloaded, re-uploaded or restreamed.

**Live broadcasts.** The data holds each event's broadcast times; "live" means now falls within them. The live video's ID is added by hand when Pokémon publishes the stream; until then the player shows the latest replay and a link to the channel. Whether a channel-level live address can be embedded instead is checked in M3.8.

**Facts, not content.** Results, rankings and team lists are facts. Only those are copied, always credited; never articles, reports, images or commentary from the sources.

**People.** Only adults of the Masters division appear, with what the official results publish: name, country, results and teams. No photos and no personal details. A player who asks to be removed is removed.

## 16. Our own texts (Phases 1 and 3, D107)

The glossary (DAT-F17), the fundamentals texts (DAT-F18) and the PANTHEON's group texts (DAT-F19) are not data from a source: the owner writes them, in Spanish and English, as hand-maintained files in `pipeline/manual/`. They belong to the project, so no license or credit is needed beyond the site's own.

- **No translation from sources** (D2 is about game data): both languages are written, and the pipeline rejects a term or text missing either.
- **What they may say:** mechanics only. Anything that changes with the regulation (who is popular, what is legal) is read from the usage and regulation data at build time, never written into the text, so a new regulation needs no rewriting.
- **Review:** when a new game changes a mechanic, the affected texts are revised as part of that game's data milestone (section 6).
- **Format:** chosen when M1.10 is built (for example one file for the glossary, and one Markdown file per concept and language for the fundamentals); the pipeline validates them and writes JSON like the rest of the data.

## 17. Pokémon categories (Phase 1, D108, D109)

Each Pokémon's category comes from **Showdown's tags** (MIT, like the rest of its data): Restricted Legendary, Sub-Legendary, Mythical, Ultra Beast and Paradox. The games' own legendary and mythical flags (in PokéAPI) are not used for the label, because the PANTHEON shows the competitive distinction; where the two disagree, the hand-written notes explain it. Whether each group is allowed comes from the regulation data (DAT-F08), so the PANTHEON follows each new regulation with no rewriting. Whether the Champions data carries the tags for every Pokémon, or they must be read from the national data, is checked in M1.12.

## Sources

Opened on 2026-11-04.

- [Pokémon Champions — Wikipedia](https://en.wikipedia.org/wiki/Pok%C3%A9mon_Champions)
- [Regulation Set M-C press release — The Pokémon Company](https://asia-press.portal-pokemon.com/press-release/pokemon-champions_20260830/)
- [Pokémon Champions regulations — Victory Road](https://victoryroad.pro/champions-regulations/)
- [Pokémon Champions regulations — Pokémon Zone](https://www.pokemon-zone.com/champions/regulations/)
- [EVs, IVs and stats in Pokémon Champions — Champsdex](https://champsdex.com/posts/pokemon-champions-ev-iv-stats-guide-2026/)
- [Pokémon Showdown source code](https://github.com/smogon/pokemon-showdown) (commit `62597d9`, 2026-11-02): `config/formats.ts`, `data/mods/champions/`, `sim/team-validator.ts`
- [Add Champions Doubles format — Showdown pull request #12401](https://github.com/smogon/pokemon-showdown/pull/12401)
- [PokéAPI repository](https://github.com/PokeAPI/pokeapi) (commit `e5b79b2`, 2026-11-02): license and `data/v2/csv`
- [PokéAPI sprites repository](https://github.com/PokeAPI/sprites) (commit `1b3b7c0`, 2026-11-03): license and README
- npm packages: `@pkmn/dex`, `@pkmn/data`, `@pkmn/mods` (0.10.13; item counts rechecked with 0.10.13 and 0.11.0 on 2026-11-21), `@pkmn/img` (0.3.5, README on hosting sprites), `@smogon/calc` (0.12.0), `dexie` (4.4.7)
- [Pokémon Champions format snapshot — MetaVGC](https://metavgc.com/guides/pokemon-champions-format-legal-pokemon-items-moves) (opened 2026-11-21): 117 allowed items in M-A
- [pkmn/smogon — Smogon data APIs](https://github.com/pkmn/smogon)
- [jsDelivr terms of use](https://raw.githubusercontent.com/jsdelivr/jsdelivr/master/Terms%20of%20Use.md)
- [About MunchStats](https://munchstats.com/about)
- Opened on 2026-11-24, for official tournaments (D104): [2023 season — Victory Road](https://victoryroad.pro/2023-season) (open team lists in TPCi events), [VGC handbook update for Pokémon Champions — Bulbanews](https://www.bulbagarden.net/threads/pokemon-champions-axes-local-communication-options-new-information-released-in-vgc-handbook.310263/), [Pokémon Champions regulations — Victory Road](https://victoryroad.pro/champions-regulations/), [2026 LAIC broadcast — The Pokémon Company press release](https://press.pokemon.com/en/Tune-In-to-the-2026-Latin-America-International-Championships-Live-Nov), [Embed videos and playlists — YouTube Help](https://support.google.com/youtube/answer/171780), [YouTube API Services Required Minimum Functionality](https://developers.google.com/youtube/terms/required-minimum-functionality)
- [NCP VGC Damage Calculator](https://nerd-of-now.github.io/NCP-VGC-Damage-Calculator/) and [its repository](https://github.com/nerd-of-now/NCP-VGC-Damage-Calculator) (MIT; commit `a2e408c`, 2026-10-24)
