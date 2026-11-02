# Pokescientia — Decision Map

Last updated: 2026-11-02

Every product and technical decision, grouped by when it must be made. This file is the only place open questions are tracked. When a question is decided, its approved text goes into [`01-vision-and-requirements.md`](01-vision-and-requirements.md) (or the relevant doc) as a `D` entry, and its row here changes to **Decided**.

**Kind:** Product = only the owner decides · Technical = Claude proposes, owner approves · Research = facts must be checked first.

## Summary

| Stage | Decided | Open |
| --- | --- | --- |
| A. Discovery and module spec | 8 | 0 |
| B. Architecture (before `ng new`) | 7 | 1 |
| C. Data strategy | 2 | 4 |
| D. Design spec | 2 | 4 |
| E. Later phases | 0 | 8 |
| F. Working process | 4 | 0 |

## A. Discovery and module spec

| ID | Decision | Kind | Status |
| --- | --- | --- | --- |
| V1 | Approve the vision document | Product | Decided (v1, 2026-11-02) |
| Q10 | Pokédex entry content in the MVP | Product | Decided → D10 |
| Q11 | Alternate forms: grouped or separate | Product | Decided → D11 |
| Q12 | Default "competitive view" filter | Product | Decided → D12 |
| Q13 | Team analyses in the MVP | Product | Decided → D13 |
| Q14 | Presenter behavior | Product | Decided → D14 |
| Q4 | Quiz section scope and phase | Product | Decided → D15 |
| Q9 | Repository layout | Technical | Decided → D9 |

## B. Architecture (before `ng new`)

| ID | Decision | Kind | Status |
| --- | --- | --- | --- |
| Q15 | Angular version | Technical | Decided → D16 (Angular 22) |
| Q16 | Package manager | Technical | Decided → D16 (npm) |
| Q17 | Rendering strategy | Technical | Decided → D16 (prerendering) |
| Q18 | Stylesheet format | Technical | Decided → D16 (SCSS) |
| Q19 | State management | Technical | Decided → D16 (plain signal services) |
| Q20 | URL design | Technical | Decided → D17 |
| Q21 | Testing, lint and format tooling | Technical | Decided → D16 (Angular defaults) |
| Q2 | UI approach: Material + CDK, custom, or Tailwind | Technical + design | **Open.** Recommendation: CDK plus custom components behind our own wrappers and tokens, which keeps the choice reversible. Decide in the design spec, before the Phase 0 shell. |

## C. Data strategy (Phase 0)

| ID | Decision | Kind | Status |
| --- | --- | --- | --- |
| Q1 | Specific data sources, which is master for what, and their licenses | Research | **Open.** A mix of sources is decided (D18); the exact sources are pending research. |
| Q22 | Current official VGC game, its mechanics, and how regulation updates are applied | Research | **Open.** Requirement R17. |
| Q23 | Image sources and whether linking to them is reliable and allowed | Research | **Open.** Linking is decided (D18). |
| Q24 | Data refresh process | Technical | Decided → D18 (by hand) |
| Q25 | Static file layout | Technical | Decided → D18 (split files) |
| Q26 | Browser storage | Technical | **Open.** Recommendation: localStorage for small preferences, IndexedDB (via Dexie) for teams, a service worker for offline data later. Explore in Phase 2. |

## D. Design spec (before the Phase 0 shell)

| ID | Decision | Kind | Status |
| --- | --- | --- | --- |
| Q3 | Presenter cast per section | Product | **Open.** Starting ideas: Alakazam or Metagross (calculator), Incineroar (competitive), Pikachu or Mew (Pokédex), Zoroark (quiz). |
| Q27 | Hall names and navigation structure | Product | **Open.** Spanish first, English too. |
| Q28 | Typography and color palette | Design | **Open.** Free fonts only (R18). |
| Q29 | Source of the academy artwork | Design + research | **Open.** Free-licensed only (R18). |
| Q30 | Themes | Product | Decided → D19 (light and dark) |
| Q31 | Accessibility target | Technical | Decided → D20 (WCAG 2.2 AA, reduced motion) |

## E. Later phases

| ID | Decision | When |
| --- | --- | --- |
| Q5 | Battle stage: real damage numbers or scripted values | Phase 3 |
| Q32 | Usage statistics source and its license (needed for common sets, D13) | Phase 4 |
| Q33 | Damage calculator library | Phase 4 |
| Q6 | Login method | Phase 5 |
| Q34 | Go web framework and database | Phase 5 |
| Q7 | Hosting for frontend and backend, on free tiers | First deployment |
| Q35 | Address: free subdomain (a paid domain breaks R7) | First deployment |
| Q8 | AI model source | Phase 6 |

## F. Working process

| ID | Decision | Status |
| --- | --- | --- |
| Q36 | Branching | Decided → D21 (owner commits straight to `main`) |
| Q37 | Continuous integration | Decided → D21 (lint, tests, build from Phase 0) |
| Q38 | Task tracking | Decided → D21 (`docs/progress.md` and GitHub Issues/Projects) |
| Q39 | Documentation language | Decided → D22 (English; README bilingual) |
