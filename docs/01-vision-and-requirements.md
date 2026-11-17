# Pokescientia — Vision & Requirements

**Version 1.23 — approved 2026-11-17** · Owner: @Alex

## Document status

Version 1.23, approved. Changes are made by editing this file and adding an entry to the Decision log.

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
2. VGC-oriented tools that answer real questions: what does my team fear, what outspeeds what, how does this matchup look, and what do the calcs say **for my own team** against the metagame.
3. A distinctive, polished interface with a recognizable identity and purposeful animation.
4. A battle stage, the COLOSSEUM, to test teams turn by turn in doubles, with full control over each turn, and to experiment with GSAP and PixiJS.
5. Hands-on learning: Angular `@angular/localize`, local-first data, and later a Go API.
6. An architecture that grows one feature at a time without rewrites.
7. A place where players meet: the FORUM, where anyone can open a topic and discuss it, built around the academy's own tools (R21).

**Non-goals** (explicitly out of scope unless revisited)

- Any monetization, ads, or official affiliation.
- A rules-accurate battle engine of our own.
- Online player-vs-player battles or matchmaking.
- Paid infrastructure, paid APIs, or a paid domain.
- Competing with Smogon, Showdown or Bulbapedia on completeness; we link to them instead.

## Target user and use cases

The primary user is the owner: a Spanish-speaking player who follows official VGC and enjoys Pokémon knowledge in general. A secondary, future user is a friend or community member visiting a public deployment; from Phase 6 they can also take part in the FORUM (R21).

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
| U14 | Keep one team active while I move between halls, and import it by pasting Showdown text | Team builder | 2 |
| U15 | Run calcs with my own team: its members against any Pokémon, and the most-used threats against my team | Calculator and metagame | 3 |
| U10 | Test my team turn by turn against a rival team: see what every move does, choose what chance does, rewind and branch, and watch each turn animated | Battle stage (COLOSSEUM) | 4 |
| U16 | Play a match with my team against a rival that decides by itself | Battle stage (COLOSSEUM) | 4 |
| U17 | During a battle, get short advice on every action each of my Pokémon can take: why to use it or not, and an estimated chance to win | AI assistant | 7 |
| U11 | Sign in and have my teams on any device | Accounts | 5 |
| U18 | Open a topic and discuss it with other players, attaching a team, a Pokémon, a calculation or a battle | Forum (FORUM) | 6 |
| U19 | Vote on posts and replies, and report anything that breaks the rules | Forum (FORUM) | 6 |
| U12 | Test my knowledge with a quiz or puzzle | Quiz | 7 |
| U13 | Ask an assistant to critique my team with evidence | AI assistant | 7 |

## Differentiating features

Pokescientia's edge is identity and integration, not data volume.

- **Spanish first.** Most competitive tools are English-only; here Spanish is the default experience.
- **The academy identity.** A Roman academy: marble and travertine halls with Latin inscriptions, and a Pokédex read as a book, the *Historia Naturalis*.
- **Resident presenters.** Each hall is introduced by a Pokémon whose nature fits it, each with a personality to match (D84). In the last phase, the same presenters answer your questions as the voice of the AI assistant (D82).
- **Lookup to analysis in one flow.** From a Pokédex entry straight into a team, and from a team straight into its weaknesses.
- **Your team everywhere.** The active team follows you through the academy: analysed in LEGIO, calculated in ABACUS, measured against the metagame in ATHENAEUM.
- **Doubles first.** Analysis tuned for VGC (speed control, spread moves, partners), not adapted from singles.
- **Discussion built on the tools.** In the FORUM, a post can carry a team, a calculation or a battle from the other halls, shown already analysed, so every discussion starts from the same evidence (D85).
- **Animation as a feature.** Motion is designed, not decorative, and the COLOSSEUM shows off what the web can do.

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
| R7 | Free resources only. Open-source material is preferred; free proprietary tools are allowed only when explicitly approved and recorded as a decision (currently GSAP, D56). |
| R8 | Built for the owner first, but deployable online later. |
| R9 | Bilingual: Spanish primary, English secondary. |
| R10 | Pokédex covers all generations, with a competitive emphasis. |
| R11 | Sessions and user accounts are wanted eventually. |
| R12 | A backend is a learning goal, possibly in Go, but optional and secondary to the app. |
| R13 | Visual identity mixes a laboratory and an ancient Greek aesthetic; no retro look. (Refined by D58: a Roman academy of natural science.) |
| R14 | Each section is presented by a different Pokémon. |
| R15 | Interest in GSAP for UI motion and PixiJS for 2D rendering. |
| R16 | The Pokédex entry must be extensible: new sections can be added later without redesigning the page. |
| R17 | Competitive data follows the current official VGC regulation and must be easy to update when the regulation changes. |
| R18 | All assets we add (fonts, icons, textures, our own artwork) must be free-licensed. Official Pokémon images are not free-licensed: they are used as fan content, credited, from the chosen sources (D40). |
| R19 | The battle stage shows the official doubles format: two Pokémon per side. |
| R20 | Doing damage calculations with the owner's own team is a core motivation of the project. A team built in the platform is available in every hall, and the calculator and metagame tools work directly from it. |
| R21 | A social hall, the FORUM: users open topics and others discuss them, like Reddit. It needs user accounts, so it comes after them. |

## Approved decisions

| ID | Decision | Why |
| --- | --- | --- |
| D1 | Interface translation uses Angular's built-in `@angular/localize`, one build per language (`/es/`, `/en/`). Spanish is the source language. | The owner has used it before and wants a deeper understanding; build cost is acceptable. |
| D2 | Game data (names, descriptions) comes translated from the data source, not translated by us. | Official Spanish names exist; translating them ourselves is error-prone. |
| D3 | Persistence is local-first: teams and preferences live in the browser, with export and import. | Usable from day one with no server. |
| D4 | Accounts and sync come later through a Go backend. | Learning goal; the backend never blocks the frontend. |
| D5 | Visual direction is an even blend: a naturalist's archive inside a classical academy. **Superseded by D58.** | Both aesthetics appealed; refined in the design spec. |
| D6 | The Pokédex includes every Pokémon, with a competitive view as the default and a toggle for all. | Middle evolutions can be competitive (Eviolite); inclusion costs little. |
| D7 | The battle simulator is a scripted animation stage, not a rules engine. (Revised by D73 and D74.) | It exists to explore animation (R5). |
| D8 | The repository is the master copy of all documentation: planning documents in `docs/` and CLAUDE.md at the root, all Markdown. Drafts may be reviewed elsewhere, but only the committed version is in force. | Both the web chat and the terminal sessions read the repository, so it is the only shared memory. |
| D9 | Monorepo: frontend and backend share this repository. Angular lives in `frontend/`; the Go API (`backend/`) and its OpenAPI contract (`api/`) are added in Phase 5. Each part is self-contained and they communicate only through the API contract. | Single developer; one CLAUDE.md and one `docs/`; the API contract changes with both sides in one commit. |
| D10 | MVP Pokédex entry: base stats, types, abilities, weaknesses and resistances, evolution chain, and learnable moves, laid out as independent sections (R16). | The core of a useful entry; more sections arrive later. |
| D11 | A National Pokédex number defines a Pokémon. Entries sharing a number (regional forms, Megas, other variants) are forms of one Pokémon, shown in one entry with a form selector. | A simple, unambiguous rule for the data model. |
| D12 | The competitive view shows all fully evolved Pokémon plus competitively relevant middle evolutions. "Show all" reveals the rest. | Keeps the full Pokédex in focus without depending on legality data in Phase 1. |
| D13 | MVP team analysis: shared weaknesses and resistances, offensive coverage, speed tiers, and doubles essentials (speed control, Fake Out, Intimidate, redirection, spread moves). Common sets come with usage data in Phase 3. | The first useful version arrives sooner; usage data needs its own research. |
| D14 | Presenters start simple (portrait and introduction) and grow later. | Low cost; a natural first GSAP use. |
| D15 | The quiz section stays as a Phase 6 candidate. (Moved to Phase 7 by D86.) | Not core to the MVP. |
| D16 | Technical baseline: Angular 22, npm, prerendered pages, SCSS, plain signal-based services for state (NgRx only if a real need appears), and Angular's default tooling (Vitest, ESLint, Prettier; Playwright for end-to-end tests). | Simple, standard, fits static hosting. |
| D17 | URLs: the language is the build prefix (`/es/`, `/en/`); path words are identical in both languages; resources are identified by stable English IDs (e.g. `/es/pokedex/charizard`). Localized names are for display only. | Switching language only swaps the prefix; links stay stable. |
| D18 | Data: a mix of open sources, processed at build time into split static files (loaded on demand), refreshed by hand with a script. Images are linked from their source, not stored in the repository. | Free, fast, small repository; specific sources pending research. |
| D19 | Light and dark themes, built on design tokens from day one. | Owner preference; tokens make both cheap. |
| D20 | Accessibility target: WCAG 2.2 AA, and full respect for the reduced-motion setting. | Cheap if designed in early, expensive to retrofit; motion is central to the site. |
| D21 | Process: the owner makes every commit, straight to `main`; Claude never commits or pushes. CI runs lint, tests and build from Phase 0. Work is tracked in the documents (revised by D65). | Solo developer; CI still checks every push. |
| D22 | Documentation, code, comments and commit messages are in English. Only the README is bilingual. | One version of the truth; no drift between translations. |
| D23 | Phase order: competitive data and calculator in Phase 3, battle stage (now the COLOSSEUM) in Phase 4. | Competitive tools matter more and build on Phases 1–2; the battle stage can then show real damage from the calculator. |
| D24 | The home page is the academy entrance, presenting the site's features as halls. | Fits the identity and introduces every presenter. |
| D25 | Search exists twice: a global search across all data, and filters within each list. | Quick lookup and deep browsing serve different needs. |
| D26 | Moves, abilities and items have their own detail pages, not only lists. | Cheap with prerendering; good for linking and search. |
| D27 | Team rules (species, items, legality, learnsets, spreads) produce warnings and never block editing or saving. | Lets the user experiment and import any team. |
| D28 | Every Pokémon entry offers "add to team" once the teams hall (LEGIO) exists. | Core to the lookup-to-analysis flow. |
| D29 | The battle stage (now the COLOSSEUM) uses a doubles layout (R19) and starts with a fixed demo scene before adding choices. | Matches official play; a demo is the simplest start for a learning space. Owner had no preference on the demo. (Demo scene replaced by D73.) |
| D30 | Search matches names in Spanish and English, ignoring accents and capitals; both names lead to the same page. | Competitive resources use English names; small cost (an index of about 3,000 entries). |
| D31 | The Pokédex shows items with a competitive purpose; all items keep their category so other groups can be shown later. | No value in items that do nothing in battle, without closing the door. |
| D32 | Learnsets include every move a Pokémon has learned in any game, marking those available in the current game. Each team chooses a format: Free (no legality warnings) or Current regulation (with warnings). | All Pokémon are equal and sets don't depend on game availability, unless the user asks for that check. |
| D33 | Competitive middle evolutions are a short list maintained by hand. | Simple and precise; changes rarely. |
| D34 | Teams autosave in the browser; there is no Save button. | Nothing is lost by accident. |
| D35 | The current official game is Pokémon Champions (Regulation Set M-C until 2026-12-02). The current regulation is set in a single regulation file. | Researched in the data strategy; one place to change when regulations change (R17). |
| D36 | Data sources: Showdown data (`@pkmn` packages) is master for mechanics; PokéAPI raw data files are master for names, descriptions and encyclopedic data. Each field has exactly one master. | Showdown has the mechanics but no Spanish; PokéAPI has Spanish but weaker mechanics. |
| D37 | Public IDs use PokéAPI's hyphenated style (`ninetales-alola`); Showdown IDs are stored internally; a mapping file covers exceptions. | Readable URLs that match image file names. |
| D38 | Each team chooses its stat system: Stat Points (Champions; default) or EVs and IVs (earlier games). A converter shows spreads in both systems. Damage always uses Champions mechanics. | Supports official play and older builds; the conversion is exact in most cases. |
| D39 | Learnsets keep detail per generation and method. A move is "available in the current game" when it is in the Champions learnset. | Enough for D32, with smaller data. |
| D40 | Images are linked from PokéAPI's sprite repository through `raw.githubusercontent.com`, pinned to a commit, with original placeholders when an image fails. Showdown's sprite server and jsDelivr are not used. | The address PokéAPI gives to applications; no hosting needed (D18). |
| D41 | Usage statistics come from Smogon's monthly aggregated statistics for Showdown's Champions VGC format. Smogon's written sets and analyses are not used. | Aggregated statistics are public domain; written content is copyrighted. |
| D42 | `@smogon/calc` is the damage engine. Pokescientia builds its own calculator on top: all rolls, KO chances, matchup grid, scenarios, roll charts, combined damage, accuracy-adjusted chances, one against many, and a formula explainer. Stat formulas are our own code. | Proven, maintained mechanics; our effort goes into analysis and presentation. |
| D43 | Browser storage: localStorage for preferences; IndexedDB through Dexie for teams, with persistent storage requested. | Right tool for each kind of data; backups remain the safety net. |
| D44 | A hand-maintained file supplies official Spanish names missing from the sources; anything still missing falls back to English, marked and reported by the build. | The newest content often lacks Spanish in PokéAPI. |
| D45 | The data pipeline lives in its own `pipeline/` folder with its own `package.json`; hand-maintained files live in `pipeline/manual/`. | The website and the build tool keep separate dependencies. |
| D46 | Generated data is committed to `frontend/public/data/` after each manual pipeline run. | CI never depends on external sources; Git shows what each refresh changed. |
| D47 | Every page is prerendered, including every Pokémon, move, ability and item, in both languages. | Instant, shareable, indexable pages on static hosting. |
| D48 | Domain logic (formulas, analyses, parsers, calculator wrappers) lives in `frontend/src/app/domain/` and never imports Angular. | Testable and movable into a package later, without premature setup. |
| D49 | The UI is built from our own components on Angular CDK; pages use only our components. Closes Q2. | The academy identity needs custom visuals; CDK gives accessible behavior; the choice stays reversible. |
| D50 | Translation files use XLIFF, with a meaning and description for each text. | Context helps when translating short or ambiguous texts. |
| D51 | A static root page sends visitors to their saved language, otherwise their browser's language, otherwise Spanish. | Static hosting has no server to choose a language. |
| D52 | Change detection is zoneless with OnPush (Angular 22 defaults); anything that changes on screen is a signal. | Fits D16 and makes pages faster. |
| D53 | Commit messages follow Conventional Commits with feature IDs; Copilot's commit message generation is configured with `.github/commit-instructions.md`. | Readable history linked to the spec, using the owner's existing workflow. |
| D54 | Node 26 LTS, recorded in `.nvmrc` and in `engines`. | Current LTS, supported by Angular 22; same version locally and in CI. |
| D55 | Angular's official AI guidelines are generated for Claude Code and Copilot (`--ai-config claude-code --ai-config vscode`) and arranged at the repository root; the root `CLAUDE.md` and `docs/` stay authoritative. | Claude Code (in VS Code's terminal) writes the code; Angular's guidelines keep it idiomatic. |
| D56 | The animation stack is 2D: GSAP (free, proprietary license) for interface motion and choreography, PixiJS for the COLOSSEUM's stage. Three.js is a Phase 4 exploration option for original 3D content only (Q63). | GSAP has the richest timelines and plugins; our Pokémon images are 2D. |
| D57 | Git practices for a solo developer: review generated messages before committing, one logical change per commit, push regularly, no force-push to `main`, keep CI green, tag each phase (`v0.x.0`), LF line endings via `.gitattributes`. Experiment branches are optional. | Professional habits that cost little and keep the history useful, without adding a branching workflow. |
| D58 | Visual identity: a Roman academy of natural science. Greek learning appears as content, not as a second style. Supersedes D5. | The name is Latin; the codex is Roman; Rome covers both knowledge and competition; Spanish comes from Latin. |
| D59 | Hall naming: the menu uses plain names in the active language; each hall carries a Latin inscription over its door and as its heading. "Coliseo" is also its own menu label. | Recognizable navigation, atmosphere in the scenery. |
| D60 | Hall map: ATRIUM (home), BIBLIOTHECA (Pokédex), LEGIO (teams), ABACUS (calculator), ATHENAEUM (metagame), COLOSSEUM (battle stage), AENIGMA (quiz). | Strategy and information halls outnumber spectacle; Latin names work in both languages. |
| D61 | The Pokédex is the *Historia Naturalis*: nine books (one per region) plus appendices, read as a codex with a thumb index and page turns; a List view is always available; scrolls are ornament only. | Honors Pliny and Aristotle; the codex is the Roman, consultable book. |
| D62 | Themes are Día (light) and Noche (dark). The default follows the device; a manual choice is remembered; an optional mode follows the time of day. Refines D19. | Day and night as two moods of the same academy. |
| D63 | Foro (travertine, porphyry, bronze) is the provisional palette; Pompeya, Mosaico and Púrpura imperial remain alternatives until real pages exist. (Renamed Travertino by D88.) | Palettes are design tokens, cheap to change. |
| D64 | The battle stage is the COLOSSEUM (module M5, formerly "Animation Lab"). | The arena is the natural Roman setting for battles; analysis lives in LEGIO and ABACUS. (Rationale revised by D73: the COLOSSEUM now analyses turns too.) |
| D65 | Work is tracked in the documents: milestone checkboxes in `06-roadmap-and-milestones.md` and a session log in `docs/progress.md`. GitHub Issues and Projects are not used for now. Revises the tracking part of D21. | One person, one branch; Git workflow learning is out of scope. Can be revisited if the project demands it. |
| D66 | Milestones are small (about 4–12 hours each, ending in a committed, working state) and estimated in hours, never dates. | No deadline; about 14 variable hours a week; small steps keep progress visible. |
| D67 | Design proposals DP-1 to DP-7 are decided at fixed review points in Phase 0 and Phase 1: DP-2, DP-6, DP-7 in M0.4; DP-1 in M0.6; DP-3, DP-4 in M0.7; DP-5 in M1.5. | Each proposal is judged on a real page instead of in the abstract. |
| D68 | **Active team** (X-12, STR-F20): one saved team stays selected across halls and visits, shown in a compact strip; importing Showdown text creates a team and makes it active. Built in Phase 2. | Teams must be usable outside LEGIO without reloading them in each hall (R20). |
| D69 | **Team-centered calculation** (R20): the calculator loads the active team's members in one click (CMP-F04); new features STR-F21 (threat list), STR-F22 (calculate from the team), CMP-F14 (one against the team) and CMP-F15 (your team in the metagame). Phase 3 starts with ABACUS, before the usage data. | Calcs with one's own team are why the project exists; starting Phase 3 with them delivers that first. |
| D70 | Import from and export to PokéPaste links is parked (P2). Showdown text import and export stay. | Showdown text is the format everyone uses; PokéPaste is a nice extra. |
| D71 | **Type tiers** (DAT-F13, ARC-F13): every type combination has a tier from the owner's own hand-made list (S, A, B, C, D, F), kept as a hand-maintained data file and shown in every Pokédex entry. It is labelled as the site's own assessment, mixing competitive and general play; no external credit is needed. | No formula can rank type combinations fairly; a considered list is closer to how players judge them. |
| D72 | **Team and member coverage** (STR-F08, STR-F09): coverage shows the whole team by default; selecting a member shows that member alone. | The team view answers "what does my team fear"; the member view explains where it comes from. |
| D73 | **The COLOSSEUM tests teams turn by turn** in doubles, in two modes: a testing mode (both sides controlled, a damage matrix before each turn, chosen or real chance, turn history with branching) and a real match mode (your side only, the rival plays itself). It starts from the active team. Revises D7, D29 and the rationale of D64; Phase 4 becomes the largest phase on purpose. | Showdown already simulates battles; studying what happens in a turn, and why, is what's missing. |
| D74 | **Turns are resolved by Showdown's open-source battle engine** (`@pkmn/sim`, MIT), running in the browser. Pokescientia builds the analysis, history, branching and animation around it and does not write its own battle rules. Checked at the start of Phase 4: Champions support, forcing outcomes, saving and restoring battle states (Q75). | Correct rules for free, kept up to date by others; effort goes into what is unique. |
| D75 | **The rival starts simple:** predictable, documented rules based on the calculator. A smarter rival comes later (LAB-F14), possibly with the AI assistant. | A simple rival is enough to practise against and easy to understand; a clever one is a project of its own. |
| D76 | **The AI assistant's primary use is the turn advisor** (AIA-F03), built in four steps: facts, ranking, win estimates (all computed by code), then explanations by a language model. Code calculates, the AI explains and never invents numbers. It is a **predictable tutor, not a perfect opponent**: imperfection is accepted, it runs on modest resources, and its assumptions are shown. | A perfect player would need a powerful model and vast resources, and isn't the aim; a tutor that explains its reasoning is. |
| D77 | **One action scoring** (LAB-F15), built in Phase 4 for the simple rival and reused by the turn advisor in Phase 7 (D86). Simulations must not assume the rival always plays the top-scored action. | Built and tested once; improvements help both; avoids advice that only looks good because the rival is perfectly predictable. |
| D78 | **Accessibility, low-cost measures only**, on top of D20: no information by color alone (X-05); a color-blindness simulation check on new screens; no flashing above three per second (X-13); sound optional and never essential (X-14); a screen reader check (Orca) of the main flows at each phase close; a test by a color-blind user when possible. Costlier options (extra palettes, high-contrast theme, spoken battle announcements, an audio-playable battle, AAA compliance) are not planned (P3). | Cheap when built in from the start; covers color blindness, deafness and the basics of blindness without expensive work. |
| D79 | **Fan-content stance.** Official Pokémon images are used without permission: The Pokémon Company states it doesn't review requests and asks projects not to use its IP, and fan sites rely on its tolerance. Safeguards: non-commercial, the disclaimer (X-11), no official logos, images linked rather than hosted, immediate compliance with any request from the rights holders, and every official image replaceable by an original fallback with one setting (X-15). Game data itself (stats, matchups, formulas) is factual information. | Keeps the standard fan-site approach while making the worst case (a takedown request) cheap to handle. |
| D80 | **Music** (SHL-F09): only free-licensed tracks (for example CC0 or CC BY, credited on About) in a style that fits the academy or Pokémon. No Pokémon or other copyrighted songs, not even kept in the repository. Off by default (X-14). | Pokémon music is actively enforced; free-licensed music carries no risk and can suit the Roman theme. |
| D81 | **Smogon tiers** (DAT-F14, ARC-F14): every Pokédex entry shows Smogon's official tiers as facts, read from Showdown's data (`@pkmn`), with nothing kept by hand: the **Champions singles tier** (current game) and the **National Dex singles tier** (covers nearly every Pokémon). For **VGC**, where Smogon publishes no tiers, the same line shows Smogon's Champions VGC **usage rank** from Phase 3 (D41, ARC-F12). Each form shows its own values; a missing value shows "—". Labels are plain text, credited to Smogon, and never mixed with the S–F type tier (D71). The site keeps no ranking of its own for Pokémon. (Revised by D83.) | Official, well-established and updated with each data refresh at no cost; covers the whole Pokédex, unlike a hand-made list of the Champions roster, which was considered and dropped (too much to maintain, too many Pokémon left unranked). |
| D82 | **Presenters are the AI assistant's voice** (Q74). The assistant has no figure of its own: in each hall, that hall's presenter answers, as its *genius loci* (the guardian spirit Romans gave every place). All presenters are peers, ATRIUM included; any of them can hand a question to the presenter whose hall fits it better. Only the principle is decided; how it works is open (Q82, Phase 7). It never overrides D76: code calculates, the voice only explains. | Solves what no single figure could: nothing in a Roman setting fits an AI, and Magearna (steampunk) and Rotom (appliances) each fitted only partly. Reuses the presenter frame and voice already planned, places each assistant feature with its hall's presenter (turn advisor in the COLOSSEUM, team critique in LEGIO), and hand-offs make the academy feel inhabited. The assistant is the last thing built, so the details stay open to change. |
| D83 | **Competitive section** (ARC-F14, DAT-F14, DAT-F15; revises D81): every Pokédex entry has a competitive section of its own, VGC first, built only from Smogon's data with nothing kept by hand. **VGC** (Phase 3): the usage rank and percentage in the current Champions regulation (D41), the **best usage rank ever reached in any VGC format** in Smogon's statistics archive, with the format and month ("No VGC record" when there is none), and the common sets (CMP-F02). **Doubles** (Phase 1): Smogon's Doubles tier (DUber, DOU, DUU) from the most recent generation in which the Pokémon was legal, naming that generation. **Singles** (Phase 1): the Champions singles tier and the National Dex tier. Missing values show "—"; each form shows its own values; labels are plain text, credited to Smogon, and never mixed with the type tier (D71). | VGC is the lens, yet no source ranks every Pokémon for VGC; showing the best VGC and doubles fact that exists for each Pokémon, with singles as context, covers the whole Pokédex honestly at no maintenance cost. |
| D84 | **Presenter cast** (Q3, X-10): ATRIUM **Arcanine** (Kanto form), BIBLIOTHECA **Mew**, LEGIO **Falinks**, ABACUS **Metagross**, ATHENAEUM **Noctowl**, COLOSSEUM **Incineroar**, AENIGMA **Delphox**. Each is chosen for lore or symbolism that matches its hall's function, and each has **a clear personality that matches that function**, used in its introductions and, in Phase 7, its assistant voice (D82). Reasons, personalities and rejected candidates are in the design spec §7. Any presenter may still be swapped before its hall is built. | Completes the cast with one rule for all: the Pokémon's own lore or a clear symbol must tell what the hall does (Metagross calculates, Falinks is a formation of six, Delphox is named after the oracle of Delphi). A clear personality per presenter gives the introductions and the Phase 7 voices a consistent character. |
| D85 | **The FORUM** (R21, module M9 `FOR`): a social hall, menu Foro / Forum, inscription FORUM, route `/forum`, in a new Community wing. Reddit-style: a post with a title and text opens a topic; others reply and vote. A post may **attach one item from another hall** (a team, a Pokémon, a calculation or a battle), shown as a card already analysed. Votes rank posts and replies; sorting by Hot, New and Top; a few categories at launch; replies nested up to 3–4 levels. Anyone can read; posting needs an account. | Social interaction is the one thing the academy lacks. A generic forum would lose to Reddit, Smogon and Discord; discussion anchored to the academy's own tools is something they can't offer. The Roman forum was the public square where citizens met and argued, so the name says what the hall does in both languages. |
| D86 | **Phase order:** the FORUM is **Phase 6**, right after accounts (Phase 5); the quiz and the AI assistant move to **Phase 7**. Accounts stay their own phase. A public deployment must happen before Phase 6. Revises the phase of D15. | The backend is fresh after Phase 5 and every hall a post can link to already exists. Accounts are tested first on a simple use (team sync, deletion) before strangers post. Merging both would make a phase of about 150–250 hours, against D66, and the forum needs its own specification. The forum does not need the assistant. |
| D87 | **Moderation in layers** (M9 rules): (1) **limits by design** at launch: no private messages, no image uploads, structured attachments; (2) **entrance limits:** verified email, a CAPTCHA, rate limits, new accounts can't post links; (3) **trust levels** earned through participation and votes, unlocking abilities up to helping to moderate; (4) **automatic filters** hold suspicious posts in a review queue and never delete by themselves; (5) a **report** button on every post, and a post reported by several trusted users is hidden until reviewed; (6) **public rules**, a penalty ladder (warning, temporary mute, suspension, ban), a log of every action with its reason, and appeals. Volunteer moderators come later, chosen from trusted users. EU legal duties and a minimum age are part of the Phase 6 specification (Q86). | One person can't moderate a community by hand, so the layers that work without a moderator carry the weight. Most spam comes from new accounts; trust levels (Discourse, Stack Overflow) turn good members into helpers; filters make mistakes, so a person decides. Private messages are the biggest risk with a young audience because nobody else sees them. |
| D88 | The provisional palette **Foro is renamed Travertino**, with the same values. Revises the name in D63. | "Foro" now names a hall (D85); two things with one name would confuse the docs and the code. |
| D89 | **FORUM presenter: Braviary** (Unova form; closes Q85). It stands as the Roman ***aquila***, the eagle that carried **SPQR**, "the Senate and People of Rome": the emblem of the people who met in the forum, not of war. Its role leans to **moderation more than messaging**: a proud, brave guardian that protects the community and, as a bird of prey, swoops on abusive posts; as a bird, and as Jupiter's eagle that carried his will, it still links to messages. Its American look (a bald eagle in red, white and blue) is handled by the framing: the eagle as a state's emblem comes from Rome's *aquila*. (Image revised by D91: no statue treatment.) Reasons, personality, forum lore for its introductions and rejected candidates are in the design spec §7. | No Pokémon stands for public discussion itself, so the cast follows a clearly Roman symbol given a fitting role, as Arcanine does for ATRIUM. Its lore fits that role: it is "often seen as a motif for various kinds of emblems" and, as the "soldiers of the sky", fights tirelessly to protect its friends. Tornadus (Therian Forme), the only close rival, is not clearly an eagle and comes with a Fūjin form. |
| D90 | **Braviary is the AI face of reporting and moderation** (Phase 7, AIA-F04; option A of the review). In the FORUM, the assistant speaks as Braviary and becomes the main way to report a post and to moderate: users report by talking to it; it reads the post against the public rules, says what it will do and why, may hide the post at once while it is reviewed, and proposes the penalty. **A moderator confirms every penalty, and appeals always go to a person** (D87 unchanged). Letting it act alone on clear cases is open (Q88). | Braviary's brave guardian personality (D89) makes it the natural voice of moderation, and one familiar character is easier to report to than a form. Keeping a person on every penalty respects D87 and the EU expectation that users can contest moderation; a language model will sometimes misjudge, and here a mistake hits a real user. |
| D91 | **Presenters are shown alive, each with a vivid personality of its own.** Official artwork in original color (DP-4's default); no bronze or statue treatment for Braviary, which revises the image part of D89. Every presenter's personality must be distinct and vivid enough that, in Phase 7, talking to the assistant feels like talking to that presenter (D82). | The presenters will speak for the assistant, so they should look and feel like living characters, not monuments. A statue suggests the opposite. |

## Assumptions

Approved with version 1. Revisit any that stops holding.

| ID | Assumption | Status |
| --- | --- | --- |
| A1 | Desktop-first, but every screen must work on a phone. | Approved |
| A2 | Angular 22, the current major. | Confirmed by D16 |
| A3 | Competitive analysis targets the current official VGC regulation only; older formats are not analyzed. | Approved; see R17 |
| A4 | Pokémon data is pre-processed at build time into static files, not queried live. | Confirmed by D18 |
| A5 | Pokémon sprites and artwork come from open community sources, linked and credited. | Confirmed by D40 |
| A6 | The whole app stays free to host, on static hosting until the Go backend arrives. | Approved |
| A7 | Work happens in short sessions that start from CLAUDE.md and these docs. | Approved |

## Open decisions

All open questions are tracked in [`00-decision-map.md`](00-decision-map.md), grouped by when they must be decided.

## Constraints

The two hard limits are zero budget and respect for Pokémon intellectual property.

**Budget.** Every tool, library, data source, asset and host must be free; open source is preferred, and any free proprietary tool needs explicit approval (R7, R18). Any feature that would need paid capacity is redesigned or postponed.

**Intellectual property.** Pokémon names, artwork, sprites, music and logos belong to Nintendo, Game Freak and The Pokémon Company. As a non-commercial fan project, Pokescientia follows these rules:

- No monetization, ever (R1).
- No official logos or branding used as our own identity; the Pokescientia brand is original.
- Data and asset sources are credited on an About page.
- A visible disclaimer states that the site is an unofficial fan project.
- Pokémon artwork is never redrawn or imitated; it comes only from the sources we choose. Original work (UI, effects, academy art) is ours.

**Users and their content.** From Phase 6 the FORUM hosts what users write. Personal data and user posts follow EU law: data protection (GDPR) and the duties of a hosting service (Digital Services Act). These, and a minimum age to sign up, are designed into the Phase 6 specification, not added later (D87, Q86).

**Licenses:** data, image and library licenses were verified in [`03-data-strategy.md`](03-data-strategy.md). Every font, icon set and texture we add must still be checked when chosen (R18).

**Effort.** One developer working in sessions. Each phase must deliver something usable on its own.

## Scope and phases

Approved with version 1. Milestones for each phase are in [`06-roadmap-and-milestones.md`](06-roadmap-and-milestones.md).

1. **Phase 0: Foundations.** Angular project in `frontend/`, Spanish and English builds, design tokens with light and dark themes, layout shell, data pipeline producing static files, CI, and a first presenter.
2. **Phase 1: MVP, the BIBLIOTHECA (Pokédex).** Pokédex (Pokémon, moves, abilities, items) with the competitive and full views, forms, search and filters.
3. **Phase 2: LEGIO (teams).** Team builder with Showdown import and export, local saving, the active team that follows you between halls, and team analysis (D13, D68).
4. **Phase 3: ABACUS and ATHENAEUM (calculator and metagame).** Damage calculator working from the active team first, then usage data and common sets, the threat list, speed benchmarks, trends.
5. **Phase 4: The COLOSSEUM (battle stage).** Turn-by-turn testing of a team in doubles, resolved by Showdown's battle engine: damage matrix, chosen or real chance, history with branching; then the animated PixiJS and GSAP stage; then a real match mode against a simple rival (D73–D75). The largest phase.
6. **Phase 5: Accounts.** Go backend with sign-in and team sync, layered on the local-first data.
7. **Phase 6: The FORUM.** Reddit-style discussion: posts that open a topic, replies, votes, and optional attachments from the other halls, with moderation in layers (D85–D87). Needs the accounts of Phase 5 and a public deployment.
8. **Phase 7: Extras.** Quiz or puzzle section, then the AI assistant, whose primary use is the turn advisor in the COLOSSEUM (D76).

Why this order: the Pokédex's data is the foundation everything else reads. The team builder gives the most value per hour. Competitive data builds directly on both and matters more than the battle stage (D23). The COLOSSEUM comes last among the core phases, so it can use the data, assets and calculator already in place. The FORUM follows accounts directly, reusing the new backend while every hall it links to already exists (D86).

## Glossary

| Term | Meaning |
| --- | --- |
| VGC | Video Game Championships: the official competitive format, played in doubles. |
| Regulation | The ruleset in force for VGC at a given time, including which Pokémon are legal. |
| National Pokédex number | The number that identifies a species across all games; defines a Pokémon in Pokescientia (D11). |
| Form | A variant sharing a National Pokédex number (regional form, Mega, appliance form…). |
| Showdown format | The plain-text team format used by Pokémon Showdown, widely used for sharing teams. |
| Common sets | The moves, items, abilities and spreads most used for a Pokémon, from usage statistics. |
| Smogon tier | Smogon's official tier for a Pokémon in a singles format (Uber, OU, UU, RU…) or in Smogon Doubles (DUber, DOU, DUU), set by usage thresholds and council bans. VGC has no tiers; usage ranks are shown instead (D83). |
| Speed tier | A Pokémon's final Speed stat compared with common threats; decides who moves first. |
| Local-first | Data lives on the user's device first; a server, if any, only syncs it. |
| `@angular/localize` | Angular's built-in translation system; produces one compiled app per language. |
| Prerendering | Generating each page's HTML at build time, so pages load fast and can be served as static files. |
| Design tokens | Named values for colors, spacing and type (e.g. `--color-surface`) used instead of raw values; enable themes. |
| WCAG | Web Content Accessibility Guidelines, the W3C accessibility standard; AA is the common target level. |
| Reduced motion | An operating-system setting asking sites to minimize animation. |
| GSAP | JavaScript animation library, here for interface motion. |
| PixiJS | 2D rendering engine using WebGL, here for the battle stage. |
| Presenter | The resident Pokémon that introduces a section of the site and, in Phase 7, speaks for the AI assistant there (D82). |
| Hall | A main section of the academy, shown in the menu by its function and in the hall by its Latin inscription (for example, Pokédex · BIBLIOTHECA). |
| Inscription | A hall's Latin name, carved over its door and shown as its heading (D59, D60). |
| Attachment | A team, Pokémon, calculation or battle from another hall, added to a FORUM post and shown as a card (D85). |
| Trust level | A stage a FORUM user reaches through good participation; each one unlocks abilities, such as posting links or helping to moderate (D87). |
| *Historia Naturalis* | The Pokédex presented as one work in nine books (*libri*), one per region, plus appendices (D61). |

## Decision log

Newest first.

| Date | Decision | Source |
| --- | --- | --- |
| 2026-11-17 | Version 1.23: D90 Braviary as the AI face of reporting and moderation in Phase 7, with a person confirming penalties (AIA-F04); D91 presenters shown alive with vivid personalities, no statue treatment for Braviary (revises D89); opens Q88; modules v1.15, design v1.12, roadmap v1.12 | Braviary review |
| 2026-11-17 | Version 1.22: D89 Braviary as the FORUM's presenter, the *aquila* of SPQR with a moderator's personality; closes Q85; modules v1.14, design v1.11, roadmap v1.11 | FORUM presenter review |
| 2026-11-16 | Version 1.21: R21 and D85–D88: the FORUM hall (Reddit-style discussion with attachments from the other halls); a new Phase 6 right after accounts, with the quiz and the AI assistant moved to Phase 7; moderation in layers; the Foro palette renamed Travertino. U18, U19 added; opens Q84–Q87; modules v1.13 (M9), data strategy v1.4, architecture v1.7, design v1.10, roadmap v1.10 | Forum discussion |
| 2026-11-16 | Version 1.20: D84 presenter cast (Arcanine, Mew, Falinks, Metagross, Noctowl, Incineroar, Delphox), each with a personality that matches its hall; closes Q3; modules v1.12, design v1.9 | Presenter cast review |
| 2026-11-15 | Version 1.19: D83 competitive section in every entry, VGC first (current usage, best VGC usage ever, common sets), then Smogon Doubles and singles tiers; revises D81; DAT-F15 added; modules v1.11, data strategy v1.3, design v1.8, roadmap v1.9 | VGC focus review of D81 |
| 2026-11-14 | Version 1.18: D82 each hall's presenter is the AI assistant's voice, peers that can hand questions to each other; closes Q74, opens Q82 (Phase 6 details), adds a casting criterion to Q3; modules v1.10, design v1.7, roadmap v1.8 | Assistant presenter discussion |
| 2026-11-13 | Version 1.17: D81 Smogon's official tiers in every entry (Champions singles, National Dex, and the VGC usage rank from Phase 3); DAT-F14, ARC-F14; modules v1.9, data strategy v1.2, roadmap v1.7. Replaces a hand-made Pokémon tier list proposed on 2026-11-12 and never applied | Pokémon ranking discussion |
| 2026-11-11 | Version 1.16: D79 fan-content stance and image fallback switch (X-15); D80 free-licensed music only (SHL-F09); modules v1.8, data strategy v1.1, architecture v1.6, design v1.6, roadmap v1.6 | Copyright review |
| 2026-11-11 | Version 1.15: D78 low-cost accessibility measures; X-13, X-14 added, X-05 extended; modules v1.7, roadmap v1.5, design v1.5 | Accessibility review |
| 2026-11-10 | Version 1.14: D76 turn advisor as the AI's primary use, a tutor not a perfect opponent; D77 shared action scoring; U17 added; modules v1.6, roadmap v1.4, architecture v1.5 | AI assistant review |
| 2026-11-10 | Version 1.13: D73–D75 approved (COLOSSEUM as turn-by-turn testing with two modes, Showdown's engine as referee, simple rival first); U10 revised, U16 added; modules v1.5, roadmap v1.3, architecture v1.4, design v1.4 | COLOSSEUM review |
| 2026-11-09 | Design v1.3: AI assistant presenter recorded as open question Q74 (leaning Magearna, Rotom valid); Xatu and Unown suggested for ATHENAEUM and AENIGMA. No new decisions | Assistant presenter discussion |
| 2026-11-09 | Version 1.12: D71 type tiers, D72 team and member coverage; modules v1.4, roadmap v1.2 | Hall ideas review |
| 2026-11-08 | Version 1.11: R20 added; D68–D70 approved (active team, team-centered calculation, PokéPaste parked); modules v1.3, roadmap v1.1 | Team and calculator review |
| 2026-11-08 | Version 1.10: design spec (`05`) and roadmap (`06`) approved as v1; DP-1 to DP-7 stay open (D67). Planning closed; Phase 0 starts with M0.1 | Final planning review |
| 2026-11-07 | Version 1.9: D65–D67 approved (tracking in the documents, small milestones, design review points); roadmap drafted | Roadmap discussion |
| 2026-11-06 | Version 1.8: D58–D64 approved (Roman identity, halls, book, themes, palette, battle stage); design spec drafted | Design exploration |
| 2026-11-05 | Version 1.7: D57 approved (Git practices); commit message rules strengthened (D53) | Git practices discussion |
| 2026-11-04 | Version 1.6: D56 approved; R7 reworded; architecture approved as v1 | Architecture review |
| 2026-11-04 | Version 1.5: D55 approved (AI guidelines) | Architecture review |
| 2026-11-04 | Version 1.4: D45–D54 approved from the architecture review | Architecture review |
| 2026-11-04 | Version 1.3: D35–D44 approved from the data strategy; R18 reworded | Data strategy review |
| 2026-11-03 | Version 1.2: D30–D34 approved; functional module spec approved as v1 | Module spec review |
| 2026-11-03 | Version 1.1: D23 (phase swap) and D24–D29 approved; R19 added; module spec drafted | Module spec discussion |
| 2026-11-02 | Version 1 approved; assumptions A1–A7 and phase order approved | Discovery round 4 |
| 2026-11-02 | D10–D22 approved; R16–R18 added; open questions moved to `00-decision-map.md` | Discovery round 4 |
| 2026-10-29 | D9 approved: monorepo; closes Q9 | Repository layout discussion |
| 2026-10-29 | D8 revised: the repository is the master copy of documentation | Web and terminal workflow discussion |
| 2026-10-29 | D1–D8 recorded for review in Draft 1 | Discovery rounds 2 and 3 |
| 2026-10-29 | Requirements R1–R15 confirmed | Discovery rounds 1 to 3 |
