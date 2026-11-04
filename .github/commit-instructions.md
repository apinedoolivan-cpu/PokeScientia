# Commit message rules — Pokescientia

Write commit messages in English, following Conventional Commits (decision D53 in `docs/01-vision-and-requirements.md`).

## Format

```
type(scope): description

optional body
```

- **type** (required): one of
  - `feat`: new feature
  - `fix`: bug fix
  - `docs`: documentation only (`docs/`, `README.md`, `CLAUDE.md`)
  - `test`: tests only
  - `refactor`: code change that neither fixes a bug nor adds a feature
  - `style`: formatting, no code meaning change
  - `chore`: tooling, configuration, dependencies
  - `data`: regenerated data in `frontend/public/data/` or hand-maintained files in `pipeline/manual/`
  - `ci`: GitHub Actions workflows
- **scope** (optional): the area changed. One of `shell`, `arc`, `str`, `cmp`, `lab`, `domain`, `ui`, `pipeline`, `i18n`, `docs`. Omit it when the change spans several areas.
- **description** (required): imperative mood, lowercase, no final period, at most 72 characters for the whole first line.
- **Feature IDs:** when the change implements or fixes a feature from `docs/02-functional-modules.md`, put its ID at the start of the description (for example `ARC-F04`).

## Body

Optional. Use it when the change needs explaining: what changed and why, in short bullet points. Mention decision IDs (for example `D38`) when a change applies or modifies a decision.

## Examples

- `feat(arc): ARC-F04 add form selector`
- `fix(str): STR-F19 correct rounding in EV to SP conversion`
- `data: refresh for regulation M-D`
- `docs: architecture v1 and decision map update`
- `chore: add commit message instructions for Copilot`
