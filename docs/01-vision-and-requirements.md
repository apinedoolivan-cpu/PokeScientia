# Pokescientia — Vision & Requirements

Oct 29, 2026 · @Alex

## Document status

Draft 1 for review. Nothing here is final until you approve it; approved items move to the Decision log.

Every statement carries one of five labels:

| Label | Meaning |
| --- | --- |
| **Confirmed (R)** | A requirement you stated directly |
| **Decision (D)** | A choice we discussed and you approved |
| **Assumption (A)** | Something I inferred; correct it if wrong |
| **Open (Q)** | Not decided yet; noted with when it must be decided |
| **Recommendation** | My advice, not yet approved |

This document is the source of truth for scope. The module spec, architecture, and CLAUDE.md must stay consistent with it.

## Vision

Pokescientia is a personal, bilingual (Spanish first) Pokémon knowledge platform, styled as a classical academy of natural science, where competitive play is the main lens.

It joins three things that usually live on separate sites: a reference Pokédex, competitive analysis and team building centered on official doubles (VGC), and a space to explore web animation. Each section is a hall of the academy, introduced by a resident Pokémon.

It is also a learning project. Exploring Angular i18n, animation with GSAP and PixiJS, and later a Go backend are goals in their own right, not side effects.

## Goals and non-goals

The project succeeds if it is useful to you, fun to build, and teaches you something at each phase.

**Goals**

1. A Pokédex covering all generations, readable in Spanish and English, with a competitive emphasis.
2. VGC-oriented tools that answer real questions: what does my team fear, what outspeeds what, how does this matchup look.
3. A distinctive, polished interface with a recognizable identity and purposeful animation.
4. An animation lab where you can freely experiment with GSAP and PixiJS.
5. Hands-on learning: Angular `@angular/localize`, local-first data, and later a Go API.
6. An architecture you can grow one feature at a time without rewrites.

**Non-goals** (explicitly out of scope unless we revisit)

- Any monetization, ads, or official affiliation.
- A rules-accurate battle engine of our own.
- Online player-vs-player battles or matchmaking.
- Paid infrastructure or paid APIs of any kind.
- Competing with Smogon, Showdown or Bulbapedia on completeness; we link to them instead.

## Target user and use cases

The primary user is you: a Spanish-speaking player who follows official VGC and enjoys Pokémon knowledge in general. A secondary, future user is a friend or community member visiting a public deployment.

| # | As a user, I want to… | Module |
| --- | --- | --- |
| U1 | Look up any Pokémon and see stats, types, abilities, moves and evolutions in Spanish | Pokédex |
| U2 | Switch between a competitive view and the full list of all Pokémon | Pokédex |
| U3 | Search and filter moves, abilities and items | Pokédex |
| U4 | Build a team of six with moves, item, ability, nature and spreads | Team builder |
| U5 | See my team's shared weaknesses, type coverage and speed tiers | Team analysis |
| U6 | Import and export teams in Showdown text format | Team builder |
| U7 | Save teams in my browser and find them later | Persistence |
| U8 | Calculate damage between two Pokémon | Calculator (later) |
| U9 | Watch an animated two-Pokémon scene with ball, entrance, attack and effects | Animation lab |
| U10 | Test my knowledge with a quiz or puzzle | Quiz (candidate) |
| U11 | Sign in and have my teams on any device | Accounts (later) |
| U12 | Ask an assistant to critique my team with evidence | AI assistant (much later) |

## Differentiating features

Pokescientia's edge is identity and integration, not data volume.

- **Spanish first.** Most competitive tools are English-only; here Spanish is the default experience.
- **The academy identity.** A naturalist's archive: marble and columns framing specimen plates, field notes and instruments.
- **Resident presenters.** Each hall is introduced by a Pokémon whose nature fits it.
- **Lookup to analysis in one flow.** From a Pokédex entry straight into a team, and from a team straight into its weaknesses.
- **Doubles first.** Analysis tuned for VGC (speed control, spread moves, partners), not adapted from singles.
- **Animation as a feature.** Motion is designed, not decorative, and the lab shows off what the web can do.

## Confirmed requirements

These come directly from your answers in the discovery conversation.

| ID | Requirement |
| --- | --- |
| R1 | Recreational, personal project. No money in any form, nothing official. |
| R2 | Built by you with Claude as architect, advisor and implementer. |
| R3 | Frontend in Angular (21+) and TypeScript. |
| R4 | Pokémon knowledge is the core; competitive play, mainly official doubles (VGC), is the main lens. Singles is secondary. |
| R5 | The battle simulator is a low-stakes space to explore animation, not a serious feature. |
| R6 | The AI agent is low priority. |
| R7 | Free resources and open-source material only. |
| R8 | Built for you first, but deployable online later. |
| R9 | Bilingual: Spanish primary, English secondary. |
| R10 | Pokédex covers all generations, with a competitive emphasis. |
| R11 | Sessions and user accounts are wanted eventually. |
| R12 | A backend is a learning goal, possibly in Go, but optional and secondary to the app. |
| R13 | Visual identity mixes a laboratory and an ancient Greek aesthetic; no retro look. |
| R14 | Each section is presented by a different Pokémon. |
| R15 | Interest in GSAP for UI motion and PixiJS for 2D rendering. |

## Approved decisions

These were proposed during discovery and you approved them.

| ID | Decision | Why |
| --- | --- | --- |
| D1 | Interface translation uses Angular's built-in `@angular/localize`, one build per language (`/es/`, `/en/`). | You've used it before and want a deeper understanding; build cost is acceptable. |
| D2 | Game data (names, descriptions) comes translated from the data source, not translated by us. | Official Spanish names exist; translating them ourselves is error-prone. |
| D3 | Persistence is local-first: teams and preferences live in the browser, with export and import. | Usable from day one with no server. |
| D4 | Accounts and sync come later through a Go backend. | Learning goal; the backend never blocks the frontend. |
| D5 | Visual direction is an even blend: a naturalist's archive inside a classical academy. | Both aesthetics appealed to you; refine as we design. |
| D6 | The Pokédex includes every Pokémon, with a competitive view as the default and a toggle for all. | Middle evolutions can be competitive (Eviolite); inclusion costs little. |
| D7 | The battle simulator is a scripted animation stage, not a rules engine. | It exists to explore animation (R5). |
| D8 | Planning documents live as editable docs; CLAUDE.md is a Markdown file in the repository. | Docs are easy to review and comment on; CLAUDE.md must sit with the code. |

## Assumptions

Correct any of these that are wrong; each one shapes later documents.

| ID | Assumption | If wrong… |
| --- | --- | --- |
| A1 | Desktop-first, but every screen must work on a phone. | Mobile-first would change layout and the battle stage's canvas size. |
| A2 | We start on Angular 22, the current major, which satisfies "21+". | Staying on 21 is possible but means an upgrade soon. |
| A3 | Competitive data targets the current official VGC regulation; older formats are not analyzed. | Supporting past formats multiplies usage data and legality rules. |
| A4 | Pokémon data is pre-processed at build time into static files, not queried live. | Live querying adds a dependency and slower pages. |
| A5 | Pokémon sprites and artwork come from open community sources and are credited. | Without them, presenters and the Pokédex lose their visuals. |
| A6 | The whole app stays free to host, ideally on static hosting until the Go backend arrives. | Paid hosting conflicts with R7. |
| A7 | Work happens in short, independent sessions, so each session starts from CLAUDE.md and these docs. | Longer sessions change nothing, but docs still matter. |

## Open decisions

None of these block the vision; each is listed with the latest point at which it must be decided.

| ID | Question | Decide by | Notes |
| --- | --- | --- | --- |
| Q1 | Which data sources (PokéAPI, Showdown data via `@pkmn`, usage statistics) and their licenses? | Architecture doc | Needs research; see Constraints. |
| Q2 | UI component approach: Angular Material + CDK, a custom design system, or a utility CSS framework? | Design spec | The academy identity favors custom components over a stock look. |
| Q3 | Presenter cast per section. | Design spec | Your early ideas: Alakazam or Metagross (calculator), Incineroar (competitive), Pikachu or Mew (Pokédex), Zoroark (quiz). |
| Q4 | Is the quiz or puzzle section in scope, and in which phase? | MVP definition | New idea, not in the original brief. |
| Q5 | Does the battle stage show real damage numbers from a calculator, or purely scripted values? | Animation lab phase | Scripted is enough for D7. |
| Q6 | Login approach for the Go backend (passwords, magic links, or a third-party sign-in). | Accounts phase | Deferred by D4. |
| Q7 | Where to host, and which free tier. | Before first deployment | Free tiers change; research at the time. |
| Q8 | AI assistant model source: free hosted tier or a small local model. | AI phase | Deferred by R6. |
| Q9 | Repository layout: one repo for frontend and backend, or separate repos. | Architecture doc |  |

## Constraints

The two hard limits are zero budget and respect for Pokémon intellectual property.

**Budget.** Every tool, library, data source and host must be free or open source (R7). Any feature that would need paid capacity is redesigned or postponed.

**Intellectual property.** Pokémon names, artwork, sprites, music and logos belong to Nintendo, Game Freak and The Pokémon Company. As a non-commercial fan project, Pokescientia follows these rules:

- No monetization, ever (R1).
- No official logos or branding used as our own identity; the Pokescientia brand is original.
- Data and asset sources are credited on an About page.
- A visible disclaimer states that the site is an unofficial fan project.
- Pokémon artwork is never redrawn or imitated; it comes only from the sources we choose. Original work (UI, effects, academy art) is ours.

**Licenses to verify** (part of Q1): the code license of the Showdown-derived libraries, PokéAPI's terms, the terms of any sprite repository, and the license of every font, icon set and texture.

**Effort.** One developer working in sessions. Each phase must deliver something usable on its own.

## Tentative scope and phases

Recommendation, not yet approved: ship the Pokédex and team builder first, then the animation lab. The roadmap document will refine this with milestones and acceptance criteria.

1. **Phase 0: Foundations.** Angular project, Spanish and English builds, the academy design tokens, layout shell, data pipeline producing static files, and a first presenter.
2. **Phase 1: MVP, the Archive.** Pokédex (Pokémon, moves, abilities, items) with competitive and full views, search and filters.
3. **Phase 2: The Strategy Hall.** Team builder with Showdown import and export, local saving, and VGC analysis: shared weaknesses, coverage, speed tiers.
4. **Phase 3: The Animation Lab.** Scripted battle stage in PixiJS and GSAP: ball throw, entrance, attack, effects, HP bar.
5. **Phase 4: Deeper analysis.** Damage calculator, usage trends, common partners and matchups.
6. **Phase 5: Accounts.** Go backend with sign-in and team sync, layered on the local-first data.
7. **Phase 6: Extras.** Quiz or puzzle section (if Q4 is approved), then the AI assistant (Q8).

Why this order: the Archive's data is the foundation everything else reads. The team builder gives the most value per hour. The lab is the most fun, but it depends on Pokémon data and assets being in place.

## Glossary

| Term | Meaning |
| --- | --- |
| VGC | Video Game Championships: the official competitive format, played in doubles. |
| Regulation | The ruleset in force for VGC at a given time, including which Pokémon are legal. |
| Showdown format | The plain-text team format used by Pokémon Showdown, widely used for sharing teams. |
| Speed tier | A Pokémon's final Speed stat compared with common threats; decides who moves first. |
| Local-first | Data lives on the user's device first; a server, if any, only syncs it. |
| `@angular/localize` | Angular's built-in translation system; produces one compiled app per language. |
| GSAP | JavaScript animation library, here for interface motion. |
| PixiJS | 2D rendering engine using WebGL, here for the battle stage. |
| Presenter | The resident Pokémon that introduces a section of the site. |
| Hall | A main section of the academy (for example, the Archive or the Strategy Hall). |

## Decision log

Newest first. Each entry links back to a decision above.

| Date | Decision | Source |
| --- | --- | --- |
| 2026-10-29 | D1–D8 recorded for review in Draft 1 | Discovery rounds 2 and 3 |
| 2026-10-29 | Requirements R1–R15 confirmed | Discovery rounds 1 to 3 |
