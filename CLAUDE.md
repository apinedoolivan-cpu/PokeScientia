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

- `docs/01-vision-and-requirements.md` — requirements (R), approved decisions (D), assumptions (A), phases.
- `docs/00-decision-map.md` — every open question (Q), grouped by when it must be decided.
- Other `docs/` files as they are added (modules, architecture, data and AI, design, roadmap, milestones).
- If code, docs and this file disagree, stop and ask. Never resolve a conflict silently.

## Key decisions (summary — the docs are authoritative)

- Stack: Angular 22, TypeScript, npm, SCSS, standalone components, plain signal-based services for state.
  Prerendered pages. Angular default tooling (Vitest, ESLint, Prettier; Playwright for end-to-end).
- Layout (D9): monorepo. Angular in `frontend/`; Go API in `backend/` and OpenAPI contract in `api/` from Phase 5.
- i18n (D1, D17): `@angular/localize`, one build per language under `/es/` and `/en/`; Spanish is the source
  language. Path words are identical in both languages; resources use stable English IDs
  (`/es/pokedex/charizard`). Localized names are display-only.
- Data (D2, D18): mixed open sources processed at build time into split static files, refreshed by hand.
  Game data comes already translated from the source. Images are linked, never stored in the repo.
- Pokédex (D6, D10–D12): every Pokémon; a National Pokédex number defines a Pokémon and forms are grouped
  under it. Default view: fully evolved plus relevant middle evolutions. Entry sections are independent and
  extensible.
- Persistence (D3, D4): local-first in the browser; accounts and sync later via the Go backend.
- Battle stage (D7): scripted animation (GSAP + PixiJS), not a rules engine.
- UI (D19, D20): light and dark themes on design tokens; WCAG 2.2 AA; always honor `prefers-reduced-motion`.
- Budget: free and open-source tools, data, assets and hosting only.

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
- Commit the lockfile (`package-lock.json`). Never commit secrets or `.env` files.

## Language (D22)

- Code, comments, commit messages and `docs/`: English. Only the README is bilingual.
- User-facing UI text: Spanish first, with English translations.

## Session routine

- Start: read this file, `docs/00-decision-map.md`, the relevant `docs/`, and `docs/progress.md` (if present).
- End: draft a short entry for `docs/progress.md`: what was done, what is next, open issues.
