# Commit message rules — Pokescientia

Write commit messages in English, following Conventional Commits (decision D53 in `docs/01-vision-and-requirements.md`). A good message lets someone reading the history understand **what changed and why** without opening the files.

## Format

```
type(scope): summary

- area: specific change (IDs, versions)
- area: specific change
```

## First line

- **type** (required): one of
  - `feat`: new feature
  - `fix`: bug fix
  - `docs`: documentation only (`docs/`, `README.md`, `CLAUDE.md`)
  - `test`: tests only
  - `refactor`: code change that neither fixes a bug nor adds a feature
  - `style`: formatting, no change in meaning
  - `chore`: tooling, configuration, dependencies
  - `data`: regenerated data in `frontend/public/data/` or hand-maintained files in `pipeline/manual/`
  - `ci`: GitHub Actions workflows
- **scope** (optional): the area changed. One of `shell`, `arc`, `str`, `cmp`, `lab`, `domain`, `ui`, `pipeline`, `i18n`, `docs`. Omit it when the change spans several areas.
- **summary** (required): the **most important change, stated specifically**. Imperative mood, lowercase, no final period, at most 72 characters for the whole first line.
  - Name the outcome: "approve architecture v1", "add form selector", "convert EVs to stat points".
  - Never use vague wording on its own: "update files", "improve docs", "for clarity", "minor changes", "various fixes".
  - Don't list file names in the summary; describe the change.
- **Feature IDs:** when the change implements or fixes a feature from `docs/02-functional-modules.md`, start the summary with its ID (for example `ARC-F04`).
- When the commit mixes types (for example docs plus configuration), use the type of the most important change and list the rest in the body.

## Body

**Required** when the commit touches more than one area, adds or changes a decision, requirement or document version, or when the summary can't say everything important. Optional only for small, single-purpose changes.

- One bullet per area or file group, starting with its name (`architecture:`, `vision:`, `decision map:`, `pipeline:`…).
- Be specific: include decision, requirement and question IDs (`D56`, `R7`, `Q63`), feature IDs and document versions (`v1.6`).
- Say what changed, not that something changed: "R7 reworded to allow approved free proprietary tools", not "updated R7".
- Wrap lines at about 72 characters.

## Examples

Small change, no body needed:

- `feat(arc): ARC-F04 add form selector`
- `fix(str): STR-F19 correct rounding in EV to SP conversion`
- `data: refresh for regulation M-D`

Several areas, with body:

```
docs: approve architecture v1 and add Copilot commit rules

- architecture: v1 approved; AI guidelines (D55); 2D animation stack
  with GSAP and PixiJS (D56); Three.js as Phase 4 exploration (Q63)
- vision: v1.6; R7 reworded to allow approved free proprietary tools
- decision map: Q61 and Q62 closed, Q63 added
- CLAUDE.md, README: aligned with R7 and the new decisions
- chore: add .github/commit-instructions.md and .vscode/settings.json
```
