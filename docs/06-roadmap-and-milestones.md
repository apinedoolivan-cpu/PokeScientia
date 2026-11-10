# Pokescientia — Roadmap and Milestones

**Version 1.3 — approved 2026-11-10** · Owner: @Alex

## Document status

Version 1.3, approved. Turns the approved documents (`01`–`05`) into an ordered plan of small milestones. It adds no features: every milestone points to features, decisions and acceptance criteria already defined.

- Phases 0–2 are planned in detail, Phase 3 in medium detail, Phases 4–6 as outlines. Later phases are detailed when they approach.
- Progress is tracked **in this document** (milestone checkboxes) and in `docs/progress.md` (session log). GitHub Issues are not used for now (D65).
- Changes are recorded in the vision's decision log. Later phases are added as new versions of this document.
- New decisions from this document: **D65–D67** (section 12). Version 1.1 adds the active team and team-centered calculation (D68, D69); version 1.2 adds type tiers and the member coverage view (D71, D72); version 1.3 redefines Phase 4 (D73–D75).

## 1. Planning principles

1. **No deadlines.** Pokescientia is a personal project for practicing how to run a full project professionally. Effort is estimated in **hours of work**, never dates.
2. **Small milestones** (D66). Each one is roughly **4–12 hours**: one to four sessions at the owner's usual pace of about 2–3 hours a day. Each ends in a **working, committed state**.
3. **One milestone at a time.** Finish, check the definition of done, commit, then start the next. Within a phase, milestones can be reordered when their dependencies allow.
4. **Scope stays fixed per milestone.** New ideas go to the decision map (as an open question or a parked idea), not into the current milestone.
5. **Estimates are rough** and only help to size work. Being slower than an estimate is information, not failure.

## 2. Definition of done

A milestone is done when all of these hold:

- [ ] Its acceptance criteria (from `02-functional-modules.md`, or listed here for technical milestones) pass, as automated tests where possible.
- [ ] Lint, unit tests and the production build pass locally and in CI.
- [ ] Every new screen works in **Spanish and English**, in **Día and Noche**, from **360 px** wide, with the **keyboard**, and with **reduced motion** (X-01, X-04–X-07).
- [ ] No accessibility errors from axe on new screens (D20).
- [ ] Documents touched by the milestone are updated (new decisions in the vision and decision map).
- [ ] Committed with Conventional Commits and feature IDs (D53), and an entry added to `docs/progress.md`.
- [ ] Its box in the phase's **Progress** list is ticked.

## 3. How a milestone runs

1. **Start:** open Claude Code in VS Code's terminal at the repository root. It reads `CLAUDE.md`, `docs/progress.md` and the milestone here.
2. **Plan:** Claude restates the milestone's scope and proposes steps; the owner approves or adjusts.
3. **Build:** Claude implements in small steps; the owner reviews each change and runs the app.
4. **Check:** run the definition of done.
5. **Close:** the owner commits (Claude may suggest the message), adds the progress entry and ticks the box.

## 4. Overview

| Phase | Hall(s) | Goal | Milestones | Rough effort | Tag |
| --- | --- | --- | --- | --- | --- |
| 0 | ATRIUM | Foundations: project, CI, design system, shell, data pipeline | 10 | 60–90 h | `v0.1.0` |
| 1 | BIBLIOTHECA | The Pokédex as the *Historia Naturalis* | 10 | 70–110 h | `v0.2.0` |
| 2 | LEGIO | Team building and analysis; the active team | 10 | 65–100 h | `v0.3.0` |
| 3 | ABACUS, ATHENAEUM | Calculator with your own team, then metagame | 8 | 70–110 h | `v0.4.0` |
| 4 | COLOSSEUM | Turn-by-turn battle testing, animated stage, real match | outline | 120–200 h (the largest phase) | `v0.5.0` |
| 5 | — | Accounts and sync (Go backend) | outline | 70–110 h | `v0.6.0` |
| 6 | AENIGMA | Quiz, then AI assistant | outline | open | `v0.7.0`+ |

At around 14 hours a week, Phase 0 takes roughly a month. This is only a sizing aid, not a schedule.

## 5. Phase 0 — Foundations (ATRIUM) · `v0.1.0`

**Goal:** a working, deployable skeleton. Both languages and themes, CI, the design foundations, the academy shell with its entrance, and real Pokémon data produced by the pipeline. No Pokédex pages yet.

**Progress**

- [ ] M0.1 — Workspace and tooling
- [ ] M0.2 — Continuous integration
- [ ] M0.3 — Prerender spike
- [ ] M0.4 — Design tokens and themes
- [ ] M0.5 — First components
- [ ] M0.6 — Academy shell
- [ ] M0.7 — ATRIUM and the presenter
- [ ] M0.8 — Pipeline foundation
- [ ] M0.9 — Pipeline content
- [ ] M0.10 — Close Phase 0

**Order:** M0.1 → M0.2 → M0.3 come first. After that, two tracks can alternate: the **interface track** (M0.4 → M0.7) and the **data track** (M0.8 → M0.9). M0.10 closes the phase.

### M0.1 — Workspace and tooling · ~6–10 h

- Node 26 LTS and `.nvmrc` (D54); `ng new` with the options in architecture §15 (D16, D52, D55).
- `outputMode: "static"`; `@angular/localize` with Spanish source under `/es/` and English under `/en/` (D1, D17, D50).
- ESLint with the layer import rules (architecture §3), Prettier, Vitest; `.vscode/extensions.json`.
- AI guidelines arranged at the root as in architecture §12 (D55).

**Done when:** a production build produces `/es/` and `/en/` with a placeholder page each; lint and tests pass; Claude Code loads `frontend/CLAUDE.md`; the Angular MCP server works from the root.

### M0.2 — Continuous integration · ~3–5 h

- GitHub Actions workflow: install, lint, unit tests, production build on every push to `main` (D21).

**Done when:** a push shows a green run; a deliberately failing test shows a red one.

### M0.3 — Prerender spike · ~5–8 h

- On an **optional experiment branch** (D57): generate a few hundred test pages per language from sample JSON with `getPrerenderParams`.
- Measure build time and output size; confirm how the data service reads data during the build and reuses it on hydration (architecture §7).

**Done when:** results and the chosen data-loading approach are written into architecture §7; the experiment is merged or discarded.

### M0.4 — Design tokens and themes · ~6–10 h

- Tokens for Foro, Día and Noche (design §4, D63); the generated type colors.
- Theme service: follows the device by default, remembers a manual choice, optional time-of-day mode (D62); a `MotionService` for reduced motion.
- Cinzel and Alegreya Sans self-hosted (architecture §8).
- **Design review:** decide **DP-2** (typography), **DP-6** (layout) and **DP-7** (motion) on a sample page.

**Done when:** the theme switches and is remembered; axe shows no contrast errors in either mode on the sample page; DP-2, DP-6 and DP-7 are recorded as decisions or revised.

### M0.5 — First components · ~6–10 h

- `ps-button`, `ps-toggle-group`, `ps-inscription`, `ps-type-badge`, `ps-stat-bar`, `ps-notice` (design §10), built on Angular CDK with component tests.

**Done when:** each component works with the keyboard, in both modes, and has tests.

### M0.6 — Academy shell · ~8–12 h

- Header with wordmark, plain-label menu, language switch and theme switch; dentil band; footer with disclaimer (SHL-F02, SHL-F04, SHL-F05, X-11).
- Root redirect page as a post-build step (D51).
- About and credits (SHL-F06), not-found page (SHL-F07).
- **Design review:** decide **DP-1** (navigation, including the phone menu).

**Done when:** SHL-F04 and SHL-F07 acceptance criteria pass; switching language keeps the page (X-01); DP-1 is recorded.

### M0.7 — ATRIUM and the presenter · ~6–10 h

- Entrance with doors for every hall: open or closed with its phase (SHL-F01, design §3).
- `ps-presenter`: arch, plinth, dismissible introduction (SHL-F08, X-10). First presenter text.
- **Design review:** decide **DP-3** (presenter frame) and **DP-4** (artwork treatment).

**Done when:** SHL-F01 acceptance criterion passes; the introduction stays dismissed after reload; DP-3 and DP-4 are recorded.

### M0.8 — Pipeline foundation · ~8–12 h

- `pipeline/` package (D45); inputs pinned (`@pkmn` versions, PokéAPI commit, D36).
- Download cache, ID mapping with `manual/id-mapping` (D37), CAP exclusion, validation and build report; `meta.json` (DAT-F09).

**Done when:** the report shows no unmatched entities; two runs produce identical output (DAT criteria).

### M0.9 — Pipeline content · ~8–12 h

- Output files for DAT-F01 to DAT-F07: Pokémon index and entries with forms, moves, abilities, items, learnsets, type chart.
- Spanish overrides (D44), the middle-evolutions list (D33) and the type tiers file with its checks (DAT-F13); fallback report.

**Done when:** DAT-F01, DAT-F05, DAT-F09 and DAT-F13 acceptance criteria pass; the measured data size is recorded in architecture §5; generated data is committed (D46).

### M0.10 — Close Phase 0 · ~4–6 h

- Playwright end-to-end tests and axe checks for the shell, in both languages and modes, added to CI.
- Review `docs/progress.md`; update documents; tag `v0.1.0` (D57).

**Done when:** CI runs end-to-end tests green; the tag exists.

## 6. Phase 1 — The Pokédex (BIBLIOTHECA) · `v0.2.0`

**Goal:** the *Historia Naturalis*: every Pokémon, move, ability and item, as a book and as a list, in both languages.

**Progress**

- [ ] M1.1 — Pokédex list
- [ ] M1.2 — Filters and sorting
- [ ] M1.3 — The entry: identity and science
- [ ] M1.4 — Forms and learnsets
- [ ] M1.5 — The book
- [ ] M1.6 — Moves
- [ ] M1.7 — Abilities and items
- [ ] M1.8 — Type chart
- [ ] M1.9 — Global search
- [ ] M1.10 — Close Phase 1

### M1.1 — Pokédex list · ~6–10 h

- Routes and prerender parameters from the generated data (M0.3 approach); data access service.
- List with the competitive view by default and "show all" (ARC-F01, D12).

**Done when:** ARC-F01 acceptance criterion passes; every Pokémon page is generated at build time.

### M1.2 — Filters and sorting · ~5–8 h

- Type, generation and name filters; sorting; state kept in the URL (ARC-F02).

**Done when:** ARC-F02 acceptance criterion passes.

### M1.3 — The entry: identity and science · ~8–12 h

- Entry sections: header with the type tier (ARC-F13), base stats, abilities, type effectiveness (domain logic with unit tests), evolution chain (ARC-F03); previous and next (ARC-F05).

**Done when:** ARC-F03 and ARC-F13 acceptance criteria pass (Gengar's matchups and tier, both languages).

### M1.4 — Forms and learnsets · ~6–10 h

- Form selector with form URLs (ARC-F04); learnable moves with generations, methods and the current-game marker (D32, D39).

**Done when:** ARC-F04 acceptance criterion passes (Alolan Ninetales).

### M1.5 — The book · ~10–14 h

- BIBLIOTHECA shelf with nine books and appendices; codex spread; thumb index; Libros/Lista switch; one page at a time on phones (D61, design §8).
- **Design review:** decide **DP-5** (page turn) with the real animation.

**Done when:** the same entry is reachable as a book page and from the list with the same URL; page turns work with keyboard, swipe and reduced motion; DP-5 is recorded.

### M1.6 — Moves · ~6–8 h

- Moves list with filters including "spread moves" (ARC-F06); move detail page with the Pokémon that learn it (ARC-F07).

**Done when:** ARC-F07 acceptance criterion passes (Lanzallamas).

### M1.7 — Abilities and items · ~6–8 h

- Lists and detail pages (ARC-F08, ARC-F09), linked from the shelf's appendices.

**Done when:** every ability and battle item has a page in both languages.

### M1.8 — Type chart · ~4–6 h

- The 18×18 chart with one or two defending types (ARC-F10).

**Done when:** ARC-F10 acceptance criterion passes.

### M1.9 — Global search · ~6–8 h

- Bilingual, accent-insensitive search across Pokémon, moves, abilities and items (SHL-F03, DAT-F10, X-03).

**Done when:** SHL-F03 acceptance criterion passes in both languages.

### M1.10 — Close Phase 1 · ~4–6 h

- End-to-end tests for the Pokédex flows; performance check of a large list and an entry; data refresh if a new regulation is out (section 10); tag `v0.2.0`.

## 7. Phase 2 — Teams (LEGIO) · `v0.3.0`

**Goal:** build, keep and understand VGC teams in the browser, with one active team that every hall can use.

**Progress**

- [ ] M2.1 — Stat formulas and converter
- [ ] M2.2 — Showdown text
- [ ] M2.3 — Saving and the team library
- [ ] M2.4 — Team editor
- [ ] M2.5 — Rule warnings
- [ ] M2.6 — Type analysis
- [ ] M2.7 — Speed and doubles essentials
- [ ] M2.8 — From the Pokédex to the legion
- [ ] M2.9 — The active team
- [ ] M2.10 — Close Phase 2

### M2.1 — Stat formulas and converter · ~6–8 h

- Domain code for Stat Points and EVs/IVs at level 50, natures, and the converter (STR-F19, D38), tested against `@smogon/calc`.

**Done when:** STR-F19 acceptance criteria pass as unit tests.

### M2.2 — Showdown text · ~6–8 h

- Parser and writer for Showdown team texts (STR-F05, STR-F06), with round-trip tests on real exported teams.

**Done when:** STR-F05 and STR-F06 acceptance criteria pass, including the round trip.

### M2.3 — Saving and the team library · ~8–10 h

- `TeamRepository` on Dexie with schema version 1, autosave, persistent storage (D43, STR-F14); team library with undo on delete (STR-F01); backup export and import (STR-F07).

**Done when:** STR-F01 and STR-F14 acceptance criteria pass.

### M2.4 — Team editor · ~10–14 h

- Six slots with pickers (STR-F02, STR-F03), team format (STR-F17) and stat system (STR-F18); final stats shown.

**Done when:** STR-F17 and STR-F18 acceptance criteria pass.

### M2.5 — Rule warnings · ~5–8 h

- Regulation data (DAT-F08) and non-blocking warnings (STR-F04, D27).

**Done when:** STR-F04 acceptance criterion passes (duplicate Sitrus Berry).

### M2.6 — Type analysis · ~6–8 h

- Defensive and offensive analysis with immunity abilities (STR-F08, STR-F09), team view and member view (D72), updating live (STR-F13).

**Done when:** STR-F08 and STR-F08/F09 acceptance criteria pass (Ground and Levitate; selecting a member).

### M2.7 — Speed and doubles essentials · ~6–8 h

- Speed tiers with Tailwind, +1, −1, Choice Scarf and Trick Room (STR-F10); doubles essentials from the move categories (STR-F11, DAT-F11).

**Done when:** STR-F10 and STR-F11 acceptance criteria pass.

### M2.8 — From the Pokédex to the legion · ~3–5 h

- "Añadir a una legión" on entries (ARC-F11, STR-F12, D28).

**Done when:** STR-F12 acceptance criterion passes.

### M2.9 — The active team · ~6–8 h

- `ActiveTeamService` in `core/`, remembered across visits (X-12, D68, architecture §3); `ps-team-strip` in the shell with switch and import (STR-F20); importing Showdown text makes the new team active (STR-F05); "Añadir a una legión" offers the active team first.

**Done when:** X-12 and STR-F20 acceptance criteria pass.

### M2.10 — Close Phase 2 · ~4–6 h

- End-to-end tests for building, importing, exporting and reloading a team, and for keeping the active team across halls and reloads; tag `v0.3.0`.

## 8. Phase 3 — Calculator and metagame (ABACUS, ATHENAEUM) · `v0.4.0`

Medium detail; specified fully when Phase 2 closes.

The phase starts with the calculator and the owner's own team (R20, D69), which needs no usage data.

- [ ] **M3.1 — ABACUS with your team** (CMP-F03, CMP-F04, STR-F22, D42): the calculator with all 16 rolls and KO chances; the active team's members one click away; "Calcular" from LEGIO.
- [ ] **M3.2 — ABACUS analysis** (CMP-F07 to CMP-F11, CMP-F14): matchup grid, scenarios, roll chart, combined damage, accuracy-adjusted chances, one against the team.
- [ ] **M3.3 — Usage data pipeline** (DAT-F12, D41): confirm Smogon's file format, add it to the pipeline.
- [ ] **M3.4 — ATHENAEUM** (CMP-F01, CMP-F02, ARC-F12): usage overview and common sets in entries.
- [ ] **M3.5 — Threat list** (STR-F21): the most-used threats against the active team, with "Calcular" on each row.
- [ ] **M3.6 — Teams meet the metagame** (CMP-F05, CMP-F12, CMP-F15, STR-F15, STR-F16): benchmarks, one against many, your team in the metagame, fill from common set.
- [ ] **M3.7 — Stretch** (CMP-F06, CMP-F13): trends and the formula explainer.
- [ ] **M3.8 — Close Phase 3** and tag `v0.4.0`.

## 9. Phases 4–6 (outlines)

**Phase 4 — COLOSSEUM (`v0.5.0`).** The largest phase, on purpose (D73). Specify it fully first (LAB features, Q63), then three parts:

1. **Battle engine spike** (Q75): check `@pkmn/sim` for Champions support, forced outcomes, and saving and restoring states.
2. **Testing mode, without animation:** battle setup from the active team (LAB-F07), the turn matrix (LAB-F08), playing turns with the engine (LAB-F09), chosen or real chance (LAB-F10), the turn history (LAB-F11) and branching (LAB-F12). Usable as text alone.
3. **The animated stage:** PixiJS setup, doubles stage, effect library, animated turns and playback controls with a reduced-motion version (LAB-F01, F02, F04–F06); the optional Three.js exploration (Q63).
4. **Real match mode:** the simple rival (LAB-F13, D75).

The smarter rival (LAB-F14) waits for Phase 6.

**Phase 5 — Accounts (`v0.6.0`).** Specify accounts and sync first (ACC features, Q6, Q34). Then the OpenAPI contract, the Go service, sign-in, sync of local teams, account deletion, and hosting for the backend (Q7).

**Phase 6 — AENIGMA and the AI assistant (`v0.7.0`+).** Specify each first (QUZ, AIA features, Q8).

**Public deployment** is not tied to a phase. When the owner wants the site online, a short milestone decides hosting and address (Q7, Q35) and adds a deployment step to CI. A natural moment is after Phase 1, when the Pokédex is usable.

## 10. Recurring work

| Task | When | How |
| --- | --- | --- |
| **Regulation update** | When a new regulation starts (the next one after M-C begins on 2026-12-02) | Data strategy §6: update `@pkmn` packages, edit the regulation file, run the pipeline, review the report, commit as `data:` (R17) |
| **Dependency updates** | About once a month | `ng update` for Angular, `npm outdated` for the rest; one commit per update, CI must stay green |
| **Progress log** | End of every session | One entry in `docs/progress.md` |
| **Document upkeep** | When a decision changes | Vision, decision map and the affected document in the same commit |

Before the pipeline exists (M0.9), a new regulation needs no work.

### Progress log format

```markdown
## 2026-11-14 · M0.1 Workspace and tooling

- Done: Angular 22 project in frontend/, both locales building.
- Next: ESLint import rules.
- Notes: ng new asked about SSR; chose static output as planned.
```

## 11. Risks

| Risk | Effect | Mitigation |
| --- | --- | --- |
| Scope creep from new ideas | Milestones never finish | New ideas go to the decision map or parked ideas (principle 4) |
| Prerendering ~6,600 pages is slow | Long builds | Measured in M0.3 before the Pokédex is built |
| Design choices keep changing | Rework | Decided at fixed review points (M0.4–M0.7, M1.5); tokens make colors cheap to change |
| A source changes format, or a regulation adds a mechanic | Pipeline or team builder breaks | Pinned inputs, pipeline validation; mechanics changes become their own milestone |
| Long breaks between sessions | Lost context | `docs/progress.md` and this checklist are the memory; every session starts from them |

## 12. Decisions

Recorded in [`01-vision-and-requirements.md`](01-vision-and-requirements.md).

| ID | Decision |
| --- | --- |
| D65 | Work is tracked in the documents: milestone checkboxes in `06-roadmap-and-milestones.md` and a session log in `docs/progress.md`. GitHub Issues and Projects are not used for now (revises the tracking part of D21). |
| D66 | Milestones are small (about 4–12 hours each, ending in a committed, working state) and estimated in hours, never dates. |
| D67 | Design proposals DP-1 to DP-7 are decided during Phase 0 and Phase 1 at fixed review points: DP-2, DP-6 and DP-7 in M0.4; DP-1 in M0.6; DP-3 and DP-4 in M0.7; DP-5 in M1.5. |
| D68 | The active team is built in Phase 2 (M2.9). |
| D69 | Phase 3 starts with ABACUS and the active team (M3.1–M3.2), before the usage data; the threat list follows the usage data (M3.5). |
