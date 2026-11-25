# CLAUDE.md — Pokescientia

Permanent instructions for Claude in this repository. Keep this file short; details live in `docs/`.

## Project

Pokescientia is a personal, non-commercial, bilingual (Spanish first, English second) Pokémon knowledge
platform styled as a classical academy of natural science. Competitive play, mainly official doubles (VGC),
is the main lens. It is also a learning project: Angular i18n, GSAP/PixiJS animation, and later a Go backend.

## Current phase

**Phase 0 — Foundations.** Next milestone: **M0.1 Workspace and tooling** (`docs/06-roadmap-and-milestones.md`).
Documents 01–06 are approved and keep growing as ideas are explored. Code, installs and scaffolding are allowed
only within the scope of the current milestone. When a milestone is done, the owner ticks it and this line moves
to the next.

**Pace: open-ended exploration.** There is no deadline. The project is a hobby the owner enjoys thinking about,
and a way to learn the technologies and Claude itself. A session may only explore ideas or the tools, with no
coding at all. Don't push to start M0.1, and don't end sessions with reminders about it; the owner starts it
when they choose. Small throwaway experiments outside the repository are welcome when the owner asks for them.

## Source of truth

- `docs/01-vision-and-requirements.md` — requirements (R), approved decisions (D), assumptions (A), phases.
- `docs/00-decision-map.md` — every open question (Q), grouped by when it must be decided.
- `docs/02-functional-modules.md` — what each module does: feature IDs (`ARC-F03`…), rules, acceptance criteria.
- `docs/03-data-strategy.md` — data sources, licenses, images, regulation updates, calculator and storage choices.
- `docs/04-architecture.md` — repository and code structure, layer rules, pipeline, i18n, rendering, testing,
  CI, coding guidelines, Phase 0 setup.
- `docs/05-design-and-interaction.md` — identity, halls, colors and tokens, typography, presenters, the
  Pokédex book, layout, components, motion. Proposals DP-1 to DP-7 are decided at their roadmap review points.
- `docs/06-roadmap-and-milestones.md` — small milestones per phase, definition of done, recurring work. The
  checkboxes there are the task tracker (D65).
- `docs/progress.md` — session log.
- `frontend/CLAUDE.md` (from Phase 0): Angular's official best practices for code in `frontend/`. This root
  file and `docs/` win on any conflict (D55).
- If code, docs and this file disagree, stop and ask. Never resolve a conflict silently.

## Key decisions (summary — the docs are authoritative)

- Stack: Angular 22, TypeScript, npm, SCSS, standalone components, plain signal-based services for state.
  Prerendered pages. Angular default tooling (Vitest, ESLint, Prettier; Playwright for end-to-end).
- Layout (D9): monorepo. Angular in `frontend/`; Go API in `backend/` and OpenAPI contract in `api/` from Phase 5.
- i18n (D1, D17): `@angular/localize`, one build per language under `/es/` and `/en/`; Spanish is the source
  language. Path words are identical in both languages; resources use stable English IDs
  (`/es/pokedex/charizard`). Localized names are display-only.
- Data (D2, D18, D36–D44): built at build time into split static files, refreshed by hand. Showdown data
  (`@pkmn`) is master for mechanics; PokéAPI raw files for names, descriptions and encyclopedic data; one master
  per field. Public IDs are PokéAPI-style (`ninetales-alola`). Missing Spanish comes from an overrides file, else
  English, marked. Images are linked from PokéAPI's sprite repo, pinned to a commit; never stored, never from
  Showdown's sprite server.
- Current game (D35): Pokémon Champions; the current regulation is set in one regulation file. Teams choose
  Stat Points (default) or EVs/IVs (D38); damage always uses Champions mechanics via `@smogon/calc` (D42).
  Stat formulas are our own code, tested against `@smogon/calc`.
- Pokédex (D6, D10–D12): every Pokémon; a National Pokédex number defines a Pokémon and forms are grouped
  under it. Default view: fully evolved plus relevant middle evolutions. Entry sections are independent and
  extensible. Learnsets cover every game, marking current-game moves; teams choose a Free or Current
  regulation format (D32). Team rules only warn, never block (D27).
- Items (D99–D101): the ARMAMENTARIUM, a room of the BIBLIOTHECA (no menu entry, Mew presents it), shows every
  item from PokéAPI; battle items (those in Showdown's data) get the full page, with availability in the current game
  from the Champions mod. Opens on items available in the current game. LEGIO marks and warns about unavailable items.
- PANTHEON (D108, D109, Phase 1): a room of the BIBLIOTHECA (route `/legendaries`, Mew presents it). Labels from
  Showdown's tags, one per Pokémon: Legendary (Sub-legendary or Restricted), Mythical (never a kind of Legendary),
  Ultra Beast, Paradox; each group's legality read from the regulation data.
- Competitive section (D83): every entry shows Smogon data only, VGC first (current usage, best usage ever in any
  VGC format, common sets; Phase 3), then Smogon Doubles and singles tiers (Phase 1). No hand-made Pokémon ranking.
- Persistence (D3, D4): local-first in the browser; accounts and sync later via the Go backend.
- Architecture (D45–D54): `pipeline/` (own package; manual files in `pipeline/manual/`) writes committed JSON
  to `frontend/public/data/`. Every page prerendered (`outputMode: static`), Spanish source under `/es/`, English
  under `/en/`, XLIFF translations, root redirect page. Zoneless + OnPush: everything on screen is a signal.
  `domain/` never imports Angular; pages use only our `ui/` components on Angular CDK. Follow the layer rules and
  coding guidelines in `docs/04-architecture.md`. Node 26 LTS.
- Animation (D56): 2D stack. GSAP for interface motion and timelines; PixiJS for the COLOSSEUM's stage. Three.js is
  only a Phase 4 exploration option (Q63).
- COLOSSEUM (D73–D75): turn-by-turn battle testing in doubles. Turns are resolved by Showdown's engine (`@pkmn/sim`);
  never write battle rules ourselves.
- AI assistant (D76, D77, Phase 7): its main use is the turn advisor. Code calculates, the AI explains and never
  invents numbers; a predictable tutor, not a perfect opponent. The rival and the advisor share one action scoring.
  Its voice is each hall's presenter, peers that can hand questions to each other (D82; details Q82).
- Presenters (D84): Arcanine (ATRIUM), Mew (BIBLIOTHECA), Falinks (LEGIO), Metagross (ABACUS), Noctowl (ATHENAEUM),
  Incineroar (COLOSSEUM), Delphox (AENIGMA), Braviary (FORUM, D89: the *aquila* of SPQR, a guardian with moderation as
  its role), Rillaboom (CIRCUS, D105: the herald). Presenters need not be Roman; each fits through lore, personality
  and role. Each has a vivid personality of its own matching its hall, and is shown alive, never as a statue (D91,
  design §7). In Phase 7 Braviary is the AI face of reporting and moderation; a moderator confirms penalties (D90). A
  presenter has a responsibility only when it acts, owns a process and would be missed (D94): Falinks inspects and
  fixes teams, Noctowl writes the metagame report, Incineroar coaches the battle, Delphox runs the quiz, Rillaboom
  announces the big events (from Phase 3, by code); Arcanine, Mew and Metagross only answer, each in its own way.
- ATHENAEUM (D106, D107): menu Estrategia / Strategy, route `/strategy`; it teaches as well as showing the metagame.
  Fundamentals pages are written once (mechanics only) with a live part from usage data; roles on usage pages; a
  glossary with `ps-term` tooltips from Phase 1 (M1.10), the rest in Phase 3 (M3.5). No separate learning hall.
- CIRCUS (D102–D105, Phase 3, after the ATHENAEUM): one page to watch official VGC competition, VGC and Masters
  only, Internationals and Worlds; YouTube player (embedded in privacy-enhanced mode, loaded on click; never
  downloaded or re-hosted, nothing over the player), event panel, past replays, both players' open team lists
  beside each replay opening in LEGIO, the season's top players by Championship Points. Hand-curated file in
  `pipeline/manual/`, a source for every fact; an event is covered only if every replay's teams are public. No
  hosting, standings, brackets, player pages or live game data.
- FORUM (D85–D87, Phase 6, after accounts in Phase 5): Reddit-style topics, nested replies and votes; a post can
  attach a team, Pokémon, calculation or battle from another hall. Moderation in layers: limits by design (no
  private messages or image uploads at launch), entrance limits, trust levels, filters that only hold posts for
  review, reports, public rules with logged actions. Every user looks the same: trust levels are internal, never
  shown (D97). Roman civic framing (D96): rules as the LEX FORI in twelve tablets (real-world politics off-topic),
  appeals as *provocatio*, the public ACTA log. Quiz and AI assistant are Phase 7 (D86).
- UI (D19, D20): light and dark themes on design tokens; WCAG 2.2 AA; always honor `prefers-reduced-motion`.
- Identity (D58–D64): a Roman academy. Menu labels are plain words (Inicio, Pokédex, Equipos, Calculadora,
  Estrategia, Torneos, Coliseo, Foro, Quiz); halls carry Latin inscriptions (ATRIUM, BIBLIOTHECA, LEGIO, ABACUS,
  ATHENAEUM, CIRCUS, COLOSSEUM, FORUM, AENIGMA). The Pokédex is the *Historia Naturalis* book with a List view.
  Themes Día/Noche follow the device by default. Travertino palette (D88, formerly Foro) is provisional; never
  hardcode colors, use tokens.
- Security (D98): low-cost measures only, built in as each phase arrives; the project's last priority. Imported
  text (Showdown, PokéPaste, backups) is never rendered as HTML and is validated; `npm audit` in CI; account checklist
  in Q91 (Phase 5).
- Budget (R7): free tools, data, assets and hosting only; open source preferred; free proprietary tools only
  when approved as a decision (GSAP, D56).

## Working rules

1. Never make a major product or architecture decision silently. Propose it, explain trade-offs, wait for approval.
2. Label statements as confirmed, decision, assumption, open question or recommendation when it matters.
3. Challenge scope creep; prefer the simplest design that meets the current phase.
4. Keep docs and this file consistent with approved decisions. When a decision is made or changed, update the
   vision doc, the decision map and the decision log together.
5. Pokémon artwork is never redrawn or imitated; use only credited sources the owner has chosen.
6. No monetization, official logos, or branding presented as our own.

## Git (D21)

- The owner makes every commit, straight to `main`. Claude never commits, pushes, or rewrites history;
  it prepares changes and the owner reviews and commits them.
- How changes are delivered: when Claude cannot write to the owner's copy (a chat session with read-only
  access), it sends **every changed file in full**, ready to replace in place, with its path. Never a patch or diff file.
  Before preparing any file, Claude fetches the latest `main` and builds from it, so no newer commit is overwritten;
  after the owner pushes, it checks the commit against what it sent. The commit message is written in the chat,
  never as a file.
- Commit the lockfile (`package-lock.json`). Never commit secrets or `.env` files.
- Git practices (D57, `docs/04-architecture.md` section 12): one logical change per commit, never force-push
  `main`, keep CI green, tag each phase. Experiment branches are optional.

## Language (D22)

- Code, comments, commit messages and `docs/`: English. Only the README is bilingual.
- Commit messages (D53, D92): **read `docs/04-architecture.md` §12 before writing one**; it is the only full
  set of rules. In short: Conventional Commits, `type(scope): summary`, IDs first (`feat(arc): ARC-F04 add form
  selector`, `docs: D90, D91 …`); a specific summary (never a vague "update/improve"); when several areas or any
  decision change, a bulleted body organized by what changed, not by file: one bullet per decision or change led
  by its ID, then the versions touched. Check where each ID lives (§12 table). Claude prepares messages; the
  owner commits. From M0.1, use the `/commit-message` skill, which loads §12 every time (D93).
- User-facing UI text: Spanish first, with English translations.

## Session routine

- Start: read this file, `docs/progress.md` (if present), the current milestone in
  `docs/06-roadmap-and-milestones.md`, `docs/00-decision-map.md`, and the docs that milestone references.
- Work on one milestone at a time; restate its scope and propose steps before building. New ideas go to the
  decision map, not into the current milestone.
- End: check the definition of done (roadmap section 2) and draft a short entry for `docs/progress.md`:
  what was done, what is next, open issues. The owner ticks the milestone box and commits.
