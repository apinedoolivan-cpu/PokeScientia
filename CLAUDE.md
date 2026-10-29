# CLAUDE.md — Pokescientia

Permanent instructions for Claude in this repository. Keep this file short; details live in `docs/`.

## Project

Pokescientia is a personal, non-commercial, bilingual (Spanish first, English second) Pokémon knowledge
platform styled as a classical academy of natural science. Competitive play, mainly official doubles (VGC),
is the main lens. It is also a learning project: Angular i18n, GSAP/PixiJS animation, and later a Go backend.

## Current phase

**Discovery / planning.** Do not generate application code, install dependencies, or scaffold the Angular
project until the architecture document is approved. Documentation work is allowed.

## Source of truth

- `docs/01-vision-and-requirements.md` — requirements (R), decisions (D), assumptions (A), open questions (Q).
- Other `docs/` files as they are added (modules, architecture, data and AI, design, roadmap, milestones).
- If code, docs and this file disagree, stop and ask. Never resolve a conflict silently.

## Key decisions (summary — the docs are authoritative)

- Frontend: Angular (21+) and TypeScript, standalone components, signals.
- i18n: built-in `@angular/localize`, one build per language (`/es/`, `/en/`). Spanish is the source language.
- Game data (names, descriptions) comes translated from the data source; we translate only UI text.
- Persistence: local-first in the browser; accounts and sync come later via a Go backend.
- Battle simulator: a scripted animation stage (GSAP + PixiJS), not a rules engine.
- Pokédex: all Pokémon included; competitive view by default, toggle for all.
- Budget: free and open-source tools, data and hosting only.
- Repository layout (D9): monorepo. Angular lives in `frontend/`; the Go API in `backend/` and its
  OpenAPI contract in `api/` arrive in Phase 5. Each part is self-contained and they share nothing but the API contract.

## Working rules

1. Never make a major product or architecture decision silently. Propose it, explain trade-offs, wait for approval.
2. Label statements as confirmed, decision, assumption, open question or recommendation when it matters.
3. Challenge scope creep; prefer the simplest design that meets the current phase.
4. Keep docs and this file consistent with approved decisions. When a decision changes, update the docs
   and add an entry to the decision log.
5. Pokémon artwork is never redrawn or imitated; use only credited sources the owner has chosen.
6. No monetization, official logos, or branding presented as our own.

## Git

- The repository owner commits and pushes. Claude does not commit, push, or rewrite history unless
  explicitly asked in the current session.
- Commit the lockfile (`package-lock.json`). Never commit secrets or `.env` files.

## Language

- Code, comments, commit messages and `docs/`: English.
- User-facing UI text: Spanish first, with English translations.

## Session routine

- Start: read this file, the relevant `docs/`, and `docs/progress.md` (if present).
- End: add a short entry to `docs/progress.md` — what was done, what is next, open issues.
