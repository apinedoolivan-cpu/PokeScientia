# Pokescientia — Technical Architecture

**Version 1.2 — approved 2026-11-06** · Owner: @Alex

## Document status

Version 1.2, approved. Describes **how** Pokescientia is built: structure, layers, rules and tools. It covers Phases 0–2 in detail and only reserves space for later phases. Versions were checked on 2026-11-04 ([Sources](#sources)).

- Decisions (`D#`), requirements (`R#`) and features (`ARC-F03`…) are defined in docs 01–03.
- Decisions A1–A12 from the review are recorded as **D45–D56** (section 16). Three.js is recorded as a Phase 4 exploration option (Q63).

## 1. System overview

Pokescientia is a **static website**: every page is generated at build time, and no server runs while people use it. The only program besides the website is the data pipeline, which runs on the owner's computer.

```
 BUILD TIME (owner's computer)                          RUN TIME (visitor's browser)

 Showdown data (@pkmn) ─┐                               ┌──────────────────────────────┐
 PokéAPI CSV files ─────┼─► pipeline/ ─► frontend/      │ Angular app (static files)   │
 Hand-maintained files ─┘   (Node)       public/data/ ─►│  · prerendered pages /es/ /en/│
                                         (committed)    │  · JSON data, loaded on demand│
                                              │         │  · teams in IndexedDB         │
                                              ▼         └──────────────┬───────────────┘
                              ng build (CI or locally)                 │ images
                              ─► static files ─► free static host      ▼
                                                        raw.githubusercontent.com
                                                        (PokéAPI sprites, D40)

 Phase 5: Go API (backend/) with its OpenAPI contract (api/) for accounts and sync.
```

## 2. Repository structure

The monorepo (D9) holds independent parts that share nothing but documents and, later, the API contract.

```
PokeScientia/
├── CLAUDE.md                     permanent instructions for Claude
├── README.md
├── .github/
│   ├── workflows/ci.yml          CI (section 12)
│   └── commit-instructions.md    commit message rules for Copilot (section 12)
├── .vscode/
│   ├── settings.json             Copilot commit instructions, shared editor settings
│   └── extensions.json           recommended extensions
├── .gitattributes                line endings (D57)
├── .nvmrc                        Node version (D54)
├── docs/                         planning documents
├── pipeline/                     data pipeline (D45), its own package.json
│   ├── manual/                   hand-maintained files (D33, D35, D37, D44, DAT-F11)
│   ├── src/                      pipeline code (TypeScript)
│   └── test/                     validation tests
├── frontend/                     Angular application, its own package.json
│   ├── public/data/              generated data, committed (D46)
│   └── src/                      application code (section 3)
├── backend/                      Phase 5: Go API
└── api/                          Phase 5: OpenAPI contract
```

`backend/` and `api/` don't exist until Phase 5. Each part is installed and tested on its own (`npm install` in `pipeline/` and in `frontend/`).

## 3. Frontend architecture

### Folder structure

Organized by hall, so each part of the site lives together and loads only when visited. Folder and route names use the English menu words; Latin inscriptions are display text only (D59, D60).

```
frontend/src/app/
├── core/          app-wide services: data access, preferences, theme, motion, storage
├── domain/        pure TypeScript: models, formulas, analyses (section 4)
├── ui/            our component library on Angular CDK (D49): ps-button, ps-card,
│                  ps-type-badge, ps-stat-bar, ps-dialog…
├── shell/         layout, header, navigation, global search, presenter area
└── halls/
    ├── atrium/       ATRIUM: home and hall doors (SHL-F01)
    ├── pokedex/      BIBLIOTHECA: shelf, codex, list, moves, abilities, items, types (M2)
    ├── teams/        LEGIO: team library, editor, analysis, converter (M3)
    ├── calculator/   ABACUS: damage calculator (M4, Phase 3)
    ├── metagame/     ATHENAEUM: usage data and trends (M4, Phase 3)
    ├── colosseum/    COLOSSEUM: battle stage (M5, Phase 4)
    ├── quiz/         AENIGMA (M7, later)
    └── about/        About and credits, not-found page
```

### Layers and rules

| Layer | May use | Must not use |
| --- | --- | --- |
| `halls/` pages and components | `ui/`, `core/`, `domain/` | Another hall's internals |
| `shell/` | `ui/`, `core/`, `domain/` | Hall internals |
| `ui/` | Angular, Angular CDK | `core/`, `domain/`, halls (it only displays what it receives) |
| `core/` | Angular, `domain/` | `ui/`, halls |
| `domain/` | Plain TypeScript, `@smogon/calc` | **Angular**, the browser, `core/`, `ui/`, halls |

These rules are enforced by ESLint import restrictions, so a violation fails CI.

- Components are standalone (Angular's default).
- State lives in **signal-based services** (D16). A hall's state lives in its own service; shared state lives in `core/`.
- Every hall is **lazy-loaded**: visiting the Pokédex never downloads the COLOSSEUM.
- Pages read route parameters as English IDs (D17, D37) and ask `core/` data services for data.

### Change detection: zoneless and OnPush (D52)

Angular has to know when to update the screen. Older versions used a library called **Zone.js**, which watched every click, timer and network response and then checked the whole page for changes. That works, but it's broad and wasteful.

New Angular 22 projects are **zoneless** and use **OnPush** by default:

- **Zoneless:** Angular no longer watches everything. It updates when something it tracks changes, mainly **signals**.
- **OnPush:** a component is only re-checked when its inputs change, one of its signals changes, or an event happens inside it.

In practice, the rule for us is simple: **anything that changes on screen is held in a signal** (or comes in through an input). Pokescientia already chose signals for state (D16), so this default fits naturally and makes pages faster.

## 4. Domain logic (D48)

`frontend/src/app/domain/` contains the platform's "science", in plain TypeScript with **no Angular imports**:

| Area | Contents | Features |
| --- | --- | --- |
| Models | Types for Pokémon, forms, moves, abilities, items, teams, spreads | All |
| Type effectiveness | Multipliers, including immunity abilities | ARC-F03, ARC-F10, STR-F08 |
| Stats | Formulas for Stat Points and EVs/IVs at level 50; natures | STR-F02, STR-F10 |
| Converter | `EVs = 8 × SP − 4` and the reverse, with warnings | STR-F19 |
| Team analysis | Defensive, offensive, speed tiers, doubles essentials, rule warnings | STR-F04, STR-F08–F11 |
| Showdown text | Parse and write team texts | STR-F05, STR-F06 |
| Damage (Phase 3) | Wrappers around `@smogon/calc`; combined and accuracy-adjusted probabilities | CMP-F03, CMP-F07–F13 |

Rules:

- Functions are **pure** where possible: same input, same output, no hidden state.
- Everything here has unit tests (section 11).
- Because it has no Angular imports, this folder can later become its own package (for the AI assistant, M8, or the Go backend) without rewrites.

## 5. Data pipeline (D45, D46)

### Technology

TypeScript run directly by Node 26 (Node runs `.ts` files without a separate build step, as long as the code uses only TypeScript features that can simply be erased, such as types; enums and similar are avoided). Dependencies: `@pkmn/dex`, `@pkmn/mods`, a CSV reader. Inputs are pinned (D36): package versions in `package-lock.json`, the PokéAPI data commit in a config file.

### Steps

1. **Download** PokéAPI's CSV files at the pinned commit (into an ignored cache folder).
2. **Read** Showdown data from `@pkmn/dex` and the Champions mod from `@pkmn/mods`.
3. **Filter**: official content only. Showdown also contains fan-made "CAP" Pokémon, moves and items; these are excluded (`isNonstandard: "CAP"`).
4. **Map IDs** between the sources (D37), using `manual/id-mapping` for exceptions. Unmatched entities stop the build.
5. **Merge**, taking each field from its single master source (D36).
6. **Apply manual files**: Spanish overrides (D44), middle evolutions (D33), doubles move categories (DAT-F11), regulation file (D35).
7. **Validate**: every reference resolves, required fields exist, both languages present or reported (DAT acceptance criteria).
8. **Write** JSON to `frontend/public/data/` and a **build report** (fallbacks, warnings, counts).

Running it twice with the same inputs gives identical files.

### Output layout

```
frontend/public/data/
├── meta.json                  data version: build date, sources, game (DAT-F09)
├── pokemon/index.json         list data: ID, number, names, types, stats, flags
├── pokemon/<id>.json          one entry with all its forms (D11)
├── learnsets/<id>.json        per Pokémon: moves by generation and method (D39)
├── moves/index.json  moves/<id>.json
├── abilities/index.json  abilities/<id>.json
├── items/index.json  items/<id>.json
├── types.json                 type chart (DAT-F06)
├── search.json                bilingual search index (DAT-F10)
└── regulation.json            current regulation and rules (DAT-F08)
```

Both languages live in the same files; every name and description has `es` and `en`.

**Estimated size:** learnsets are the largest part (about 3 MB as compact JSON, measured from Showdown's data); everything together should be roughly 5–10 MB, split into small files. Each refresh only commits what changed.

### Running it

From `pipeline/`: `npm run build-data`. Then review the report and the changes in `frontend/public/data/`, and commit (D46).

## 6. Internationalization (D1, D17, D50, D51)

- **Source language:** Spanish. Templates are written in Spanish and marked with `i18n` attributes; texts in code use `$localize`.
- **Translation file:** English, in **XLIFF** (`frontend/src/locale/messages.en.xlf`), extracted with `ng extract-i18n`. Each marked text carries a meaning and description (`i18n="meaning|description@@id"`) to give context when translating.
- **Builds:** one per language. Both languages live in subdirectories: Spanish under `/es/` and English under `/en/` (the `subPath` of each locale in `angular.json`).
- **Language switch:** a link to the same path in the other language (swap `/es/` and `/en/`). The choice is saved in localStorage.
- **Root page (`/`):** static hosting can't choose a language. A tiny static `index.html` at the root sends visitors to their saved language, otherwise their browser's language if it's Spanish or English, otherwise Spanish. It's written into the build output by a small post-build step, because Angular only writes files inside each language folder.
- **Game data:** names come from the data files (D2); the interface picks `es` or `en` based on the active build.

## 7. Rendering and routing (D16, D47)

### Rendering

`outputMode: "static"`: every route is **prerendered** to HTML at build time, for both languages, and no server is produced. The browser then **hydrates** each page (Angular takes over the prerendered HTML instead of redrawing it).

### Routes

Path words are English and identical in both languages (D17). Hall names and Latin inscriptions (D59, D60) only affect what's shown, not URLs.

| Route | Content | Rendering |
| --- | --- | --- |
| `/` (inside each language) | ATRIUM: academy entrance | Prerendered |
| `/pokedex`, `/pokedex/:id` | BIBLIOTHECA: shelf and list; entries as codex pages (forms have their own IDs, D37) | Prerendered, every ID |
| `/moves`, `/moves/:id` | Moves | Prerendered, every ID |
| `/abilities`, `/abilities/:id` | Abilities | Prerendered, every ID |
| `/items`, `/items/:id` | Items | Prerendered, every ID |
| `/types` | Type chart | Prerendered |
| `/teams`, `/teams/:teamId` | LEGIO: team library and editor (Phase 2) | Shell prerendered; content in the browser (teams live in IndexedDB) |
| `/calculator` | ABACUS: calculator (Phase 3) | Prerendered shell |
| `/metagame` | ATHENAEUM: usage data and trends (Phase 3) | Prerendered |
| `/colosseum` | COLOSSEUM: battle stage (Phase 4) | Prerendered shell |
| `/quiz` | AENIGMA (later) | Prerendered shell |
| `/about` | About and credits | Prerendered |
| `/404` | Not-found page | Prerendered; the host serves it for unknown URLs |

Parameterized routes list their IDs at build time with `getPrerenderParams`, read from the generated data.

**Size of the build:** about 3,300 entity pages (≈1,300–1,400 Pokémon and forms, ≈940 moves, ≈310 abilities, ≈540 battle items) × 2 languages ≈ **6,600 HTML pages**, plus a copy of `public/data/` per language. Build output is **not** committed; CI builds it. Angular's documentation warns that large prerenders take time; the Phase 0 spike measures it (section 15).

**Data during prerendering:** pages load their JSON through one data service in `core/`. How that service reads files during the build (from disk) versus in the browser (over HTTP), and how the data is reused when the page hydrates, is validated in the Phase 0 spike before the Pokédex is built.

## 8. Styling (D16, D19, D49)

- **Design tokens** as CSS custom properties in `frontend/src/styles/tokens/`, in two levels:
  - *Primitives:* raw values (a marble white, a bronze, a spacing scale).
  - *Semantic tokens:* what they mean (`--color-surface`, `--color-text`, `--color-accent`, `--space-m`). Components only use semantic tokens.
- **Themes:** light and dark redefine the semantic tokens. The default follows `prefers-color-scheme`; a saved choice sets `data-theme` on `<html>`.
- **SCSS** is used for mixins, breakpoints and file organization, not for colors (those are tokens, so themes work at run time).
- **Components:** pages use only our `ui/` components (D49). Those are built on **Angular CDK** for behavior and accessibility (overlays, dialogs, listboxes, focus management, keyboard navigation) and styled with tokens.
- **Fonts:** free-licensed (R18) and self-hosted through Fontsource packages (OFL), so no external font requests are made. Specific fonts are chosen in the design document (Q28).
- **Type colors** (Fire, Water…) are tokens too, with contrast checked in both themes (D20).

## 9. Animation (D20, R15)

| Tool | Used for | Loaded |
| --- | --- | --- |
| CSS transitions | Small state changes (hover, focus, theme switch) | Always |
| GSAP (free, proprietary license, D56) | Interface motion and choreography: presenter entrances, hall transitions, list choreography, and the COLOSSEUM's timelines (it also animates PixiJS objects) | Where used |
| PixiJS (MIT) | The COLOSSEUM's 2D battle stage (WebGL/WebGPU) | Only in `/colosseum` |

- A `MotionService` in `core/` exposes a signal for `prefers-reduced-motion`. **Every** animation checks it; with reduced motion, motion becomes a fade or is skipped (X-06).
- Animations never hold essential information; the page must work with them off.
- The stack is **2D** (D56): Pokémon images are 2D (D40), and official 3D models can't be used.
- **Exploration option (Q63, Phase 4):** Three.js (MIT, 3D) for experiments with original content only, such as a 3D academy entrance or 2.5D camera effects in the COLOSSEUM. Evaluated when Phase 4 is specified; not part of the core stack.

## 10. Persistence (Phase 2, D3, D43)

- **Dexie** over IndexedDB, wrapped by a `TeamRepository` service in `core/`. Halls never use Dexie directly.
- Database schema has a **version number**; each change adds a migration so saved teams survive updates.
- Every team stores its format (STR-F17) and stat system (STR-F18).
- Persistent storage is requested on first save (D43).
- **Backup format** (STR-F07): a JSON file with a format version, the export date and the teams.
- Preferences (language, theme, dismissed presenters) use localStorage through a `PreferencesService`, with safe defaults if storage is unavailable.

## 11. Testing

| Level | Tool | What | Where |
| --- | --- | --- | --- |
| Unit | Vitest (Angular's default runner) | All of `domain/`: formulas, converter, analyses, parser, probabilities; checked against `@smogon/calc` where relevant | `frontend` |
| Component | Vitest with Angular testing utilities | `ui/` components and key page components | `frontend` |
| End-to-end | Playwright | User flows from the acceptance criteria, in both languages | `frontend/e2e` |
| Accessibility | axe (in Playwright) | Every page type, both themes (X-05) | `frontend/e2e` |
| Data | Vitest | Pipeline validation and snapshots of known Pokémon (DAT criteria) | `pipeline/test` |

**Guidelines:**

- Acceptance criteria in the module spec become tests, named with their feature ID (`ARC-F04: switching to the Alolan form…`).
- `domain/` aims for near-complete coverage; UI tests cover behavior, not appearance.

## 12. Tooling and CI (D21, D53, D54)

### Tools

- **Node 26 LTS** ("Lithium", LTS since 2026-10-28), recorded in `.nvmrc` and in both `package.json` files (`engines`).
- **ESLint** with Angular's rules and the import restrictions from section 3. **Prettier** for formatting.
- **npm scripts** (frontend): `start`, `build`, `test`, `e2e`, `lint`, `extract-i18n`. (pipeline): `build-data`, `test`.

### Commit messages (D53)

**Conventional Commits** with feature IDs: `type(scope): summary`, plus a bulleted body when needed.

| Part | Values |
| --- | --- |
| type | `feat`, `fix`, `docs`, `test`, `refactor`, `style`, `chore`, `data`, `ci` |
| scope | `shell`, `arc`, `str`, `cmp`, `lab`, `domain`, `ui`, `pipeline`, `i18n`, `docs` |
| summary | Imperative, lowercase, specific (never just "update" or "improve"); include the feature ID when implementing one |
| body | Required when several areas, or any decision, requirement or version, change: one bullet per area with IDs and versions |

Examples: `feat(arc): ARC-F04 add form selector` · `data: refresh for Regulation M-D` · `docs: architecture v1`.

**Copilot setup:** `.github/commit-instructions.md` holds these rules, and `.vscode/settings.json` points Copilot's "Generate commit message" to it:

```json
{
  "github.copilot.chat.commitMessageGeneration.instructions": [
    { "file": ".github/commit-instructions.md" }
  ]
}
```

The same rules are in CLAUDE.md, so Claude in the terminal suggests messages in the same style.

### AI guidelines (D55)

The owner writes code with **Claude Code in VS Code's integrated terminal**, started from the repository root, and uses **Copilot** in VS Code for commit messages and chat. Each tool reads its own instruction files:

| File | Written by | Read by | Contents |
| --- | --- | --- | --- |
| `CLAUDE.md` (root) | Us | Claude Code, always | Project rules, decisions, pointers to `docs/`. **Authoritative.** |
| `frontend/CLAUDE.md` | `ng new --ai-config claude-code` | Claude Code, when working on files in `frontend/` | Angular's official best practices (about 60 lines: standalone components, signals, `input()`/`output()`, native control flow, Signal Forms, `inject()`, WCAG AA and axe checks) |
| `.mcp.json` (root) | Generated in `frontend/`, moved to the root | Claude Code | Angular CLI's MCP server (`npx @angular/cli mcp`), which gives Claude Angular-specific tools and documentation |
| `AGENTS.md` (root) | Generated in `frontend/`, moved to the root, plus a short header we add | Copilot chat | Angular's best practices, preceded by: "Project rules are in `CLAUDE.md` and `docs/`; they win on conflict." |
| `.vscode/mcp.json` (root) | Generated in `frontend/.vscode/`, moved to the root | Copilot in VS Code | The same Angular MCP server |
| `.github/commit-instructions.md` | Us | Copilot commit messages | Section above |

Why files move: both tools read their configuration from the folder that is opened or where they start (the repository root), so files generated inside `frontend/` would otherwise be ignored. `frontend/CLAUDE.md` stays where it is, because Claude Code reads nested `CLAUDE.md` files when it works in that folder, which is exactly where Angular's rules apply.

Rules:

- The root `CLAUDE.md` and `docs/` win over any generated guideline. If a generated rule contradicts a decision, the generated file is edited and the change noted in the decision log.
- Phase 0 checks that each tool actually loads its files, and that the MCP server finds the Angular project when started from the root. Paths are adjusted if not.
- When Angular publishes new recommendations, the generated files can be regenerated (`ng generate ai-config`) and compared.

### Git practices (D57)

The owner works alone and commits straight to `main` (D21). These habits keep the history useful and `main` healthy:

1. **Review before committing.** Check the staged changes in VS Code's Source Control panel. A message generated by Copilot is a draft: fix the summary and add anything missing before committing. Claude Code can also suggest a message for the staged changes; the owner still commits.
2. **One logical change per commit.** From Phase 0, commit each feature or step on its own (`feat(arc): ARC-F04 add form selector`), not a day's work at once.
3. **Commit often, push regularly.** GitHub is also the backup; unpushed work exists only on one computer.
4. **Never rewrite pushed history.** No force-push to `main`; a mistake is fixed with a new commit.
5. **Keep `main` working.** If CI fails, fixing it comes before new work.
6. **Tag milestones.** The end of each phase gets a version tag (`v0.1.0` after Phase 0, `v0.2.0` after the Pokédex…), optionally with a GitHub Release listing the changes.
7. **Track work in the documents.** Milestone checkboxes in `06-roadmap-and-milestones.md` and the session log in `docs/progress.md` (D65); a commit names its feature ID or milestone instead of an issue number.
8. **Consistent line endings.** `.gitattributes` stores every text file with LF endings, so Windows editors never make whole files appear changed.
9. **Experiment branches are optional.** A short-lived branch may be used for a risky experiment (for example, the Phase 0 spike) and deleted if it fails. Not required by the workflow.

### CI (GitHub Actions)

On every push to `main`:

1. Install with `npm ci` (frontend; pipeline when its files change).
2. Lint.
3. Unit and component tests; pipeline tests when it changes.
4. Production build (both languages, prerendered).
5. End-to-end and accessibility tests against the built site.

A failure shows on the commit in GitHub. Deployment is added when hosting is chosen (Q7).

## 13. Coding guidelines

1. **Types and type chart come from data.** Never hardcode the 18 types.
2. **IDs are opaque text.** Never assume an ID contains a Pokédex number.
3. **Components receive data as inputs.** Entry sections don't look things up by number themselves.
4. **Image URLs come from data**, never built from a pattern in components (D40).
5. **No hardcoded format rules.** Level, clauses and legality come from `regulation.json` (R17).
6. **Every visible text is translatable** (`i18n` or `$localize`); no concatenated sentences.
7. **Everything that changes on screen is a signal** (D52).
8. **Accessibility is part of "done"** (D20): keyboard, labels, contrast, reduced motion.
9. **Small, focused files**, named with Angular's 2025 style guide (the default for new projects).

Guidelines 1–4 also keep the parked fakémon idea (P1) cheap if it's ever reopened.

## 14. Future: backend (Phase 5)

Reserved only:

- `backend/`: a Go API for accounts and team sync (D4); framework and database are Q34.
- `api/openapi.yaml`: the contract; the frontend generates its TypeScript types from it.
- The frontend keeps working without it (local-first, D3).

## 15. Phase 0 setup

The steps that start Phase 0, after this document and the design document are approved.

1. Install **Node 26 LTS**; add `.nvmrc` with `26`.
2. From the repository root, create the Angular project in `frontend/`:

   ```bash
   npx @angular/cli@22 new pokescientia --directory frontend --style scss --ssr --routing --prefix ps --skip-git --package-manager npm --ai-config claude-code --ai-config vscode
   ```

   | Option | Why |
   | --- | --- |
   | `--directory frontend` | The app lives in `frontend/` (D9) |
   | `--style scss` | D16 |
   | `--ssr` | Adds `@angular/ssr`, needed for prerendering (switched to static output in step 3) |
   | `--routing` | Routes per hall |
   | `--prefix ps` | Component names start with `ps-` (`ps-button`) |
   | `--skip-git` | The repository already exists |
   | `--package-manager npm` | D16 |
   | `--ai-config claude-code --ai-config vscode` | Angular's official AI guidelines for Claude Code and Copilot (D55, section 12) |

   Defaults kept: standalone components, zoneless with OnPush (D52), Vitest, strict TypeScript, 2025 file naming.
3. Set `outputMode: "static"` and the i18n configuration (Spanish source under `/es/`, English under `/en/`) in `angular.json`; add `@angular/localize`.
4. Add ESLint (`ng add angular-eslint`), Prettier, Playwright and axe.
5. Create `pipeline/` with its own `package.json`, and the hand-maintained files in `pipeline/manual/`.
6. Add `.github/commit-instructions.md`, `.vscode/settings.json` and `.github/workflows/ci.yml`.
6b. Arrange the AI guidelines as described in section 12 (move the MCP configurations to the repository root, create the root `AGENTS.md`, and check that both tools load them).
7. **Spike** (a short experiment, kept or discarded): prerender a few hundred test pages in both languages, measuring build time and size, and confirm how the data service reads data during the build and during hydration. Results are written into this document before the Pokédex is built.

[`06-roadmap-and-milestones.md`](06-roadmap-and-milestones.md) turns these steps into Phase 0 milestones M0.1–M0.3.

## 16. Decisions

Approved in review on 2026-11-04.

| Review | Decision | Summary |
| --- | --- | --- |
| A1 | D45 | The data pipeline lives in its own `pipeline/` folder with its own `package.json`; hand-maintained files in `pipeline/manual/` |
| A2 | D46 | Generated data is committed to `frontend/public/data/` after each manual run |
| A3 | D47 | Every page is prerendered, including every Pokémon, move, ability and item |
| A4 | D48 | Domain logic lives in `frontend/src/app/domain/` and never imports Angular |
| A5 | D49 | UI built from our own components on Angular CDK; pages use only our components (closes Q2) |
| A6 | D50 | Translation files in XLIFF, with meaning and description for each text |
| A7 | D51 | A static root page redirects to the saved language, else the browser's, else Spanish |
| A8 | D52 | Zoneless change detection with OnPush (Angular 22 defaults) |
| A9 | D53 | Conventional Commits with feature IDs; Copilot configured through `.github/commit-instructions.md` |
| A10 | D54 | Node 26 LTS, recorded in `.nvmrc` and `engines` |
| A11 | D56 | Keep GSAP (free, proprietary license) with PixiJS as the 2D animation stack; R7 reworded to allow explicitly approved free proprietary tools |
| A12 | D55 | Generate Angular's AI guidelines for Claude Code and Copilot; arrange them at the root as in section 12; root `CLAUDE.md` stays authoritative |
| — | D57 | Git practices for a solo developer (section 12) and `.gitattributes` with LF line endings; experiment branches optional |

## Sources

Checked on 2026-11-04.

- npm registry: `@angular/cli` 22.2.5, `@angular/core` 22.2.4 (Node `^22.22.3 || ^24.15.0 || >=26.0.0`), `@angular/ssr` 22.2.5, `@angular/localize` 22.2.4, `@angular/cdk` 22.2.6, `vitest` 5.1.0, `@playwright/test` 1.64.1, `pixi.js` 8.22.0 (MIT), `gsap` 3.15.1, `dexie` 4.4.7, `@fontsource/*` (OFL-1.1)
- [Angular repository](https://github.com/angular/angular) (commit `78b6c53`): guides `adev/src/content/guide/ssr.md`, `i18n/deploy.md`, `testing/`
- [Angular CLI repository](https://github.com/angular/angular-cli) (commit `12a7d2a`): `ng new` and application schematics (defaults: standalone, zoneless, Vitest, SCSS option, `--ssr`, `--ai-config`)
- [What's new in Angular v22 — Code with Ahsan](https://blog.codewithahsan.dev/whats-new-angular-v22/) and [Angular 22 key features — Angular.love](https://angular.love/angular-22-key-features-and-changes): zoneless and OnPush defaults, Signal Forms stable
- [Node.js 26.13.0 "Lithium" reaches LTS — LinuxCompatible](https://www.linuxcompatible.org/story/nodejs-26130-lithium-reaches-lts-support-through-april-2029/)
- npm registry: `three` 0.187.0 (MIT), `motion` 14.9.1 (MIT), `animejs` 4.5.0 (MIT), compared as alternatives
- [GSAP Standard "No Charge" license — ScanCode LicenseDB](https://scancode-licensedb.aboutcode.org/gsap-standard-no-charge-2025.html)
- Angular's best practices for AI tools: `packages/core/resources/best-practices.md` in the [Angular repository](https://github.com/angular/angular), and the `ai-config` schematic in the [Angular CLI repository](https://github.com/angular/angular-cli)
- [Custom instructions in VS Code — VS Code blog](https://code.visualstudio.com/blogs/2025/03/26/custom-instructions) and [Commit messages with Copilot — Tim Deschryver](https://timdeschryver.dev/blog/gain-control-over-commit-messages-generated-by-github-copilot)
- Pokémon Showdown data (commit `62597d9`): entity counts and learnset size estimate
