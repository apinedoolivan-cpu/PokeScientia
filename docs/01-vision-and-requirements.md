# Pokescientia — Vision & Requirements

**Version 1.1 — approved 2026-11-03** · Owner: @Alex

## Document status

Version 1.1, approved. Changes are made by editing this file and adding an entry to the Decision log.

Every statement carries one of five labels:

| Label | Meaning |
| --- | --- |
| **Confirmed (R)** | A requirement the owner stated directly |
| **Decision (D)** | A choice discussed and approved by the owner |
| **Assumption (A)** | An inference approved with this version; revisit if it stops holding |
| **Open (Q)** | Not decided yet; tracked in [`00-decision-map.md`](00-decision-map.md) |
| **Recommendation** | Advice, not yet approved |

This document is the source of truth for scope. The module spec, architecture, and CLAUDE.md must stay consistent with it. Open questions live only in the decision map, so they are never tracked in two places.

## Vision

Pokescientia is a personal, bilingual (Spanish first) Pokémon knowledge platform, styled as a classical academy of natural science, where competitive play is the main lens.

It joins three things that usually live on separate sites: a reference Pokédex, competitive analysis and team building centered on official doubles (VGC), and a space to explore web animation. Each section is a hall of the academy, introduced by a resident Pokémon.

It is also a learning project. Exploring Angular i18n, animation with GSAP and PixiJS, and later a Go backend are goals in their own right, not side effects.

## Goals and non-goals

The project succeeds if it is useful to the owner, fun to build, and teaches something at each phase.

**Goals**

1. A Pokédex covering all generations, readable in Spanish and English, with a competitive emphasis.
2. VGC-oriented tools that answer real questions: what does my team fear, what outspeeds what, how does this matchup look.
3. A distinctive, polished interface with a recognizable identity and purposeful animation.
4. An animation lab to freely experiment with GSAP and PixiJS.
5. Hands-on learning: Angular `@angular/localize`, local-first data, and later a Go API.
6. An architecture that grows one feature at a time without rewrites.

**Non-goals** (explicitly out of scope unless revisited)

- Any monetization, ads, or official affiliation.
- A rules-accurate battle engine of our own.
- Online player-vs-player battles or matchmaking.
- Paid infrastructure, paid APIs, or a paid domain.
- Competing with Smogon, Showdown or Bulbapedia on completeness; we link to them instead.

## Target user and use cases

The primary user is the owner: a Spanish-speaking player who follows official VGC and enjoys Pokémon knowledge in general. A secondary, future user is a friend or community member visiting a public deployment.

| # | As a user, I want to… | Module | Phase |
| --- | --- | --- | --- |
| U1 | Look up any Pokémon and see stats, types, abilities, weaknesses, evolutions and moves in Spanish | Pokédex | 1 |
| U2 | Switch between the competitive view and the full list of all Pokémon | Pokédex | 1 |
| U3 | Search and filter moves, abilities and items | Pokédex | 1 |
| U4 | Build a team of six with moves, item, ability, nature and spreads | Team builder | 2 |
| U5 | See my team's shared weaknesses, type coverage, speed tiers and doubles essentials | Team analysis | 2 |
| U6 | Import and export teams in Showdown text format | Team builder | 2 |
| U7 | Save teams in my browser and find them later | Persistence | 2 |
| U8 | See the most common sets for a Pokémon in the current format | Usage data | 3 |
| U9 | Calculate damage between Pokémon, including doubles conditions | Calculator | 3 |
| U10 | Watch an animated doubles scene with balls, entrances, attacks and effects | Animation lab | 4 |
| U11 | Sign in and have my teams on any device | Accounts | 5 |
| U12 | Test my knowledge with a quiz or puzzle | Quiz | 6 |
| U13 | Ask an assistant to critique my team with evidence | AI assistant | 6 |

## Differentiating features

Pokescientia's edge is identity and integration, not data volume.

- **Spanish first.** Most competitive tools are English-only; here Spanish is the default experience.
- **The academy identity.** A naturalist's archive: marble and columns framing specimen plates, field notes and instruments.
- **Resident presenters.** Each hall is introduced by a Pokémon whose nature fits it.
- **Lookup to analysis in one flow.** From a Pokédex entry straight into a team, and from a team straight into its weaknesses.
- **Doubles first.** Analysis tuned for VGC (speed control, spread moves, partners), not adapted from singles.
- **Animation as a feature.** Motion is designed, not decorative, and the lab shows off what the web can do.

## Confirmed requirements

These come directly from the owner's answers in discovery.

| ID | Requirement |
| --- | --- |
| R1 | Recreational, personal project. No money in any form, nothing official. |
| R2 | Built by the owner with Claude as architect, advisor and implementer. |
| R3 | Frontend in Angular (21+) and TypeScript. |
| R4 | Pokémon knowledge is the core; competitive play, mainly official doubles (VGC), is the main lens. Singles is secondary. |
| R5 | The battle simulator is a low-stakes space to explore animation, not a serious feature. |
| R6 | The AI agent is low priority. |
| R7 | Free resources and open-source material only. |
| R8 | Built for the owner first, but deployable online later. |
| R9 | Bilingual: Spanish primary, English secondary. |
| R10 | Pokédex covers all generations, with a competitive emphasis. |
| R11 | Sessions and user accounts are wanted eventually. |
| R12 | A backend is a learning goal, possibly in Go, but optional and secondary to the app. |
| R13 | Visual identity mixes a laboratory and an ancient Greek aesthetic; no retro look. |
| R14 | Each section is presented by a different Pokémon. |
| R15 | Interest in GSAP for UI motion and PixiJS for 2D rendering. |
| R16 | The Pokédex entry must be extensible: new sections can be added later without redesigning the page. |
| R17 | Competitive data follows the current official VGC regulation and must be easy to update when the regulation changes. |
| R18 | All assets (fonts, textures, icons, artwork) must be free-licensed. |
| R19 | The battle stage shows the official doubles format: two Pokémon per side. |

## Approved decisions

| ID | Decision | Why |
| --- | --- | --- |
| D1 | Interface translation uses Angular's built-in `@angular/localize`, one build per language (`/es/`, `/en/`). Spanish is the source language. | The owner has used it before and wants a deeper understanding; build cost is acceptable. |
| D2 | Game data (names, descriptions) comes translated from the data source, not translated by us. | Official Spanish names exist; translating them ourselves is error-prone. |
| D3 | Persistence is local-first: teams and preferences live in the browser, with export and import. | Usable from day one with no server. |
| D4 | Accounts and sync come later through a Go backend. | Learning goal; the backend never blocks the frontend. |
| D5 | Visual direction is an even blend: a naturalist's archive inside a classical academy. | Both aesthetics appealed; refined in the design spec. |
| D6 | The Pokédex includes every Pokémon, with a competitive view as the default and a toggle for all. | Middle evolutions can be competitive (Eviolite); inclusion costs little. |
| D7 | The battle simulator is a scripted animation stage, not a rules engine. | It exists to explore animation (R5). |
| D8 | The repository is the master copy of all documentation: planning documents in `docs/` and CLAUDE.md at the root, all Markdown. Drafts may be reviewed elsewhere, but only the committed version is in force. | Both the web chat and the terminal sessions read the repository, so it is the only shared memory. |
| D9 | Monorepo: frontend and backend share this repository. Angular lives in `frontend/`; the Go API (`backend/`) and its OpenAPI contract (`api/`) are added in Phase 5. Each part is self-contained and they communicate only through the API contract. | Single developer; one CLAUDE.md and one `docs/`; the API contract changes with both sides in one commit. |
| D10 | MVP Pokédex entry: base stats, types, abilities, weaknesses and resistances, evolution chain, and learnable moves, laid out as independent sections (R16). | The core of a useful entry; more sections arrive later. |
| D11 | A National Pokédex number defines a Pokémon. Entries sharing a number (regional forms, Megas, other variants) are forms of one Pokémon, shown in one entry with a form selector. | A simple, unambiguous rule for the data model. |
| D12 | The competitive view shows all fully evolved Pokémon plus competitively relevant middle evolutions. "Show all" reveals the rest. | Keeps the full Pokédex in focus without depending on legality data in Phase 1. |
| D13 | MVP team analysis: shared weaknesses and resistances, offensive coverage, speed tiers, and doubles essentials (speed control, Fake Out, Intimidate, redirection, spread moves). Common sets come with usage data in Phase 3. | The first useful version arrives sooner; usage data needs its own research. |
| D14 | Presenters start simple (portrait and introduction) and grow later. | Low cost; a natural first GSAP use. |
| D15 | The quiz section stays as a Phase 6 candidate. | Not core to the MVP. |
| D16 | Technical baseline: Angular 22, npm, prerendered pages, SCSS, plain signal-based services for state (NgRx only if a real need appears), and Angular's default tooling (Vitest, ESLint, Prettier; Playwright for end-to-end tests). | Simple, standard, fits static hosting. |
| D17 | URLs: the language is the build prefix (`/es/`, `/en/`); path words are identical in both languages; resources are identified by stable English IDs (e.g. `/es/pokedex/charizard`). Localized names are for display only. | Switching language only swaps the prefix; links stay stable. |
| D18 | Data: a mix of open sources, processed at build time into split static files (loaded on demand), refreshed by hand with a script. Images are linked from their source, not stored in the repository. | Free, fast, small repository; specific sources pending research. |
| D19 | Light and dark themes, built on design tokens from day one. | Owner preference; tokens make both cheap. |
| D20 | Accessibility target: WCAG 2.2 AA, and full respect for the reduced-motion setting. | Cheap if designed in early, expensive to retrofit; motion is central to the site. |
| D21 | Process: the owner makes every commit, straight to `main`; Claude never commits or pushes. CI runs lint, tests and build from Phase 0. Work is tracked in `docs/progress.md` and GitHub Issues/Projects. | Solo developer; CI still checks every push. |
| D22 | Documentation, code, comments and commit messages are in English. Only the README is bilingual. | One version of the truth; no drift between translations. |
| D23 | Phase order: competitive data and calculator in Phase 3, Animation Lab in Phase 4. | Competitive tools matter more and build on Phases 1–2; the lab can then show real damage from the calculator. |
| D24 | The home page is the academy entrance, presenting the site's features as halls. | Fits the identity and introduces every presenter. |
| D25 | Search exists twice: a global search across all data, and filters within each list. | Quick lookup and deep browsing serve different needs. |
| D26 | Moves, abilities and items have their own detail pages, not only lists. | Cheap with prerendering; good for linking and search. |
| D27 | Team rules (species, items, legality, learnsets, spreads) produce warnings and never block editing or saving. | Lets the user experiment and import any team. |
| D28 | Every Pokémon entry offers "add to team" once the Strategy Hall exists. | Core to the lookup-to-analysis flow. |
| D29 | The Animation Lab uses a doubles layout (R19) and starts with a fixed demo scene before adding choices. | Matches official play; a demo is the simplest start for a learning lab. Owner had no preference on the demo. |

## Assumptions

Approved with version 1. Revisit any that stops holding.

| ID | Assumption | Status |
| --- | --- | --- |
| A1 | Desktop-first, but every screen must work on a phone. | Approved |
| A2 | Angular 22, the current major. | Confirmed by D16 |
| A3 | Competitive analysis targets the current official VGC regulation only; older formats are not analyzed. | Approved; see R17 |
| A4 | Pokémon data is pre-processed at build time into static files, not queried live. | Confirmed by D18 |
| A5 | Pokémon sprites and artwork come from open community sources, linked and credited. | Approved; sources pending research |
| A6 | The whole app stays free to host, on static hosting until the Go backend arrives. | Approved |
| A7 | Work happens in short sessions that start from CLAUDE.md and these docs. | Approved |

## Open decisions

All open questions are tracked in [`00-decision-map.md`](00-decision-map.md), grouped by when they must be decided.

## Constraints

The two hard limits are zero budget and respect for Pokémon intellectual property.

**Budget.** Every tool, library, data source, asset and host must be free or open source (R7, R18). Any feature that would need paid capacity is redesigned or postponed.

**Intellectual property.** Pokémon names, artwork, sprites, music and logos belong to Nintendo, Game Freak and The Pokémon Company. As a non-commercial fan project, Pokescientia follows these rules:

- No monetization, ever (R1).
- No official logos or branding used as our own identity; the Pokescientia brand is original.
- Data and asset sources are credited on an About page.
- A visible disclaimer states that the site is an unofficial fan project.
- Pokémon artwork is never redrawn or imitated; it comes only from the sources we choose. Original work (UI, effects, academy art) is ours.

**Licenses to verify:** the code license of the Showdown-derived libraries, PokéAPI's terms, the terms of any sprite source (including whether linking is allowed), usage statistics sources, and the license of every font, icon set and texture.

**Effort.** One developer working in sessions. Each phase must deliver something usable on its own.

## Scope and phases

Approved with version 1. The roadmap document adds milestones and acceptance criteria.

1. **Phase 0: Foundations.** Angular project in `frontend/`, Spanish and English builds, design tokens with light and dark themes, layout shell, data pipeline producing static files, CI, and a first presenter.
2. **Phase 1: MVP, the Archive.** Pokédex (Pokémon, moves, abilities, items) with the competitive and full views, forms, search and filters.
3. **Phase 2: The Strategy Hall.** Team builder with Showdown import and export, local saving, and team analysis (D13).
4. **Phase 3: Competitive data.** Usage data and common sets, damage calculator, speed benchmarks, trends.
5. **Phase 4: The Animation Lab.** Scripted doubles battle stage in PixiJS and GSAP: ball throws, entrances, attacks, effects, HP bars, with real damage from the calculator.
6. **Phase 5: Accounts.** Go backend with sign-in and team sync, layered on the local-first data.
7. **Phase 6: Extras.** Quiz or puzzle section, then the AI assistant.

Why this order: the Archive's data is the foundation everything else reads. The team builder gives the most value per hour. Competitive data builds directly on both and matters more than the lab (D23). The lab comes last among the core phases, so it can use the data, assets and calculator already in place.

## Glossary

| Term | Meaning |
| --- | --- |
| VGC | Video Game Championships: the official competitive format, played in doubles. |
| Regulation | The ruleset in force for VGC at a given time, including which Pokémon are legal. |
| National Pokédex number | The number that identifies a species across all games; defines a Pokémon in Pokescientia (D11). |
| Form | A variant sharing a National Pokédex number (regional form, Mega, appliance form…). |
| Showdown format | The plain-text team format used by Pokémon Showdown, widely used for sharing teams. |
| Common sets | The moves, items, abilities and spreads most used for a Pokémon, from usage statistics. |
| Speed tier | A Pokémon's final Speed stat compared with common threats; decides who moves first. |
| Local-first | Data lives on the user's device first; a server, if any, only syncs it. |
| `@angular/localize` | Angular's built-in translation system; produces one compiled app per language. |
| Prerendering | Generating each page's HTML at build time, so pages load fast and can be served as static files. |
| Design tokens | Named values for colors, spacing and type (e.g. `--color-surface`) used instead of raw values; enable themes. |
| WCAG | Web Content Accessibility Guidelines, the W3C accessibility standard; AA is the common target level. |
| Reduced motion | An operating-system setting asking sites to minimize animation. |
| GSAP | JavaScript animation library, here for interface motion. |
| PixiJS | 2D rendering engine using WebGL, here for the battle stage. |
| Presenter | The resident Pokémon that introduces a section of the site. |
| Hall | A main section of the academy (for example, the Archive or the Strategy Hall). |

## Decision log

Newest first.

| Date | Decision | Source |
| --- | --- | --- |
| 2026-11-03 | Version 1.1: D23 (phase swap) and D24–D29 approved; R19 added; module spec drafted | Module spec discussion |
| 2026-11-02 | Version 1 approved; assumptions A1–A7 and phase order approved | Discovery round 4 |
| 2026-11-02 | D10–D22 approved; R16–R18 added; open questions moved to `00-decision-map.md` | Discovery round 4 |
| 2026-10-29 | D9 approved: monorepo; closes Q9 | Repository layout discussion |
| 2026-10-29 | D8 revised: the repository is the master copy of documentation | Web and terminal workflow discussion |
| 2026-10-29 | D1–D8 recorded for review in Draft 1 | Discovery rounds 2 and 3 |
| 2026-10-29 | Requirements R1–R15 confirmed | Discovery rounds 1 to 3 |
