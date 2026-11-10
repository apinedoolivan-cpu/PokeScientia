# Pokescientia — Decision Map

Last updated: 2026-11-10

Every product and technical decision, grouped by when it must be made. This file is the only place open questions are tracked. When a question is decided, its approved text goes into [`01-vision-and-requirements.md`](01-vision-and-requirements.md) (or the relevant doc) as a `D` entry, and its row here changes to **Decided**.

**Kind:** Product = only the owner decides · Technical = Claude proposes, owner approves · Research = facts must be checked first.

## Summary

| Stage | Decided | Open |
| --- | --- | --- |
| A. Discovery and module spec | 27 | 0 |
| B. Architecture (before `ng new`) | 19 | 0 |
| C. Data strategy | 8 | 0 |
| D. Design spec | 7 | 4 |
| E. Later phases | 0 | 8 |
| F. Working process | 5 | 0 |

Parked ideas (section G) are not counted: they are out of scope until the owner reopens them.

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
| Q40 | Phase order of competitive data and the battle stage | Product | Decided → D23 |
| Q41 | Home page | Product | Decided → D24 |
| Q42 | Global search and list filters | Product | Decided → D25 |
| Q43 | Detail pages for moves, abilities and items | Product | Decided → D26 |
| Q44 | Team rule validation | Product | Decided → D27 |
| Q45 | "Add to team" from the Pokédex | Product | Decided → D28 |
| Q46 | Battle stage layout and first version | Product | Decided → D29 |
| Q47 | Bilingual search | Product | Decided → D30 |
| Q48 | Which items the Pokédex shows | Product | Decided → D31 |
| Q49 | Learnset scope and team formats | Product | Decided → D32 |
| Q50 | Competitive middle evolutions list | Product | Decided → D33 |
| Q51 | Team saving | Product | Decided → D34 |
| Q70 | Teams across halls and calculations with one's own team | Product | Decided → D68, D69 |
| Q71 | PokéPaste links | Product | Parked → D70, P2 |
| Q72 | Ranking type combinations | Product | Decided → D71 |
| Q73 | Team coverage: team or member view | Product | Decided → D72 |
| Q5 | Battle stage: real or scripted damage | Product | Decided → D73, LAB-F04 (always real) |
| Q76 | What the COLOSSEUM is for, and how turns are resolved | Product | Decided → D73, D74, D75 |
| Q77 | What the AI assistant is mainly for, and how it relates to the rival | Product | Decided → D76, D77 |

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
| Q52 | Location of the data pipeline | Technical | Decided → D45 |
| Q53 | Generated data committed or generated in CI | Technical | Decided → D46 |
| Q54 | Which pages are prerendered | Technical | Decided → D47 |
| Q55 | Location of domain logic | Technical | Decided → D48 |
| Q56 | Translation file format | Technical | Decided → D50 |
| Q57 | Root address and language redirect | Technical | Decided → D51 |
| Q58 | Change detection | Technical | Decided → D52 |
| Q59 | Commit message convention | Technical | Decided → D53 |
| Q60 | Node version | Technical | Decided → D54 |
| Q61 | GSAP's proprietary license versus R7 ("open-source material only") | Product | Decided → D56 (keep GSAP; R7 reworded) |
| Q62 | Angular's AI configuration files (`--ai-config`) | Technical | Decided → D55 |
| Q2 | UI approach: Material + CDK, custom, or Tailwind | Technical + design | Decided → D49 (CDK plus our own components) |

## C. Data strategy (Phase 0)

| ID | Decision | Kind | Status |
| --- | --- | --- | --- |
| Q1 | Specific data sources, which is master for what, and their licenses | Research | Decided → D36 (sources), D37 (IDs), D44 (Spanish overrides) |
| Q22 | Current official VGC game, its mechanics, and how regulation updates are applied | Research | Decided → D35 (Pokémon Champions), D38 (stat systems), D39 (learnsets) |
| Q23 | Image sources and whether linking to them is reliable and allowed | Research | Decided → D40 |
| Q24 | Data refresh process | Technical | Decided → D18 (by hand) |
| Q25 | Static file layout | Technical | Decided → D18 (split files) |
| Q26 | Browser storage | Technical | Decided → D43 |
| Q32 | Usage statistics source and its license (common sets, D13) | Research | Decided → D41 |
| Q33 | Damage calculator library | Research | Decided → D42 |

## D. Design spec (before the Phase 0 shell)

| ID | Decision | Kind | Status |
| --- | --- | --- | --- |
| Q3 | Presenter cast per section | Product | **Open.** Tentative cast in [`05-design-and-interaction.md`](05-design-and-interaction.md) §7: Mew or Pikachu (BIBLIOTHECA), Falinks (LEGIO), Alakazam or Metagross (ABACUS), Incineroar (COLOSSEUM), Zoroark (AENIGMA); ATRIUM and ATHENAEUM to decide. |
| Q27 | Hall names and navigation structure | Product | Decided → D59, D60 |
| Q28 | Typography and color palette | Design | **Open.** Palette: Foro provisional (D63), final choice after the first real pages. Typography: proposed as DP-2. |
| Q29 | Source of the academy artwork | Design + research | **Open.** Free-licensed only (R18). |
| Q30 | Themes | Product | Decided → D19 (light and dark) |
| Q31 | Accessibility target | Technical | Decided → D20 (WCAG 2.2 AA, reduced motion) |
| Q64 | Visual direction | Product | Decided → D58 (Roman academy) |
| Q65 | Pokédex presentation | Product | Decided → D61 (*Historia Naturalis* book) |
| Q66 | Day and night theme behavior | Product | Decided → D62 |
| Q67 | Battle hall | Product | Decided → D64 (COLOSSEUM) |
| Q68 | Design proposals DP-1 to DP-7 (navigation, typography, presenter frame, artwork treatment, page turn, layout, motion) | Design | **Open.** Reviewed at fixed points in Phase 0 and Phase 1 (D67, [`06-roadmap-and-milestones.md`](06-roadmap-and-milestones.md)). |

## E. Later phases

| ID | Decision | When |
| --- | --- | --- |
| Q63 | Three.js 3D experiments (3D academy entrance, 2.5D COLOSSEUM effects), original content only | Phase 4 |
| Q75 | **Battle engine check** (D74): confirm that `@pkmn/sim` supports Champions and its doubles rules, that outcomes can be forced (rolls, critical hits, accuracy, secondary effects, speed ties), that battle states can be saved and restored for branching, and **how fast it simulates**: turns per second in the browser and the time to copy a battle state, which decide how many playouts the win estimates can afford (AIA-F03, Phase 6). Done as a spike, like M0.3; the fallback for anything unsupported is decided then. | Phase 4 start |
| Q6 | Login method | Phase 5 |
| Q34 | Go web framework and database | Phase 5 |
| Q7 | Hosting for frontend and backend, on free tiers | First deployment |
| Q35 | Address: free subdomain (a paid domain breaks R7) | First deployment |
| Q8 | AI model source. Options noted, not decided: the owner's own API key entered in settings (never stored or paid by the site), a provider's free tier, or a small model running in the browser. Must respect R7 (free resources); the turn advisor's steps 1–3 work without any model (D76). | Phase 6 |
| Q74 | **AI assistant presenter.** The assistant needs a figure that fits the Roman academy. **Current leaning: an ancient-automaton figure such as Magearna**, an artificial mind that suits the classical world (Heron of Alexandria's automata, the Antikythera mechanism) and needs no custom form. **Rotom remains a valid option**, as the academy's resident spirit (Roman Lares) or as an openly modern guest, but its electrical nature clashes with the setting. Another Pokémon may still be chosen. Eliminated in the 2026-11-09 review: Metagross, Porygon, Unown, Sigilyph, Chimecho, Bronzong, Lampent, Xatu (Unown suggested for AENIGMA and Xatu for ATHENAEUM instead). | Phase 6 |

## F. Working process

| ID | Decision | Status |
| --- | --- | --- |
| Q36 | Branching | Decided → D21 (owner commits straight to `main`) |
| Q37 | Continuous integration | Decided → D21 (lint, tests, build from Phase 0) |
| Q38 | Task tracking | Decided → D65 (milestone checkboxes in the roadmap and `docs/progress.md`; no GitHub Issues for now) |
| Q69 | Milestone size and scheduling | Decided → D66 (small milestones, hours not dates) |
| Q39 | Documentation language | Decided → D22 (English; README bilingual) |

## G. Parked ideas

Ideas discussed and deliberately set aside. Nothing is built for them now. A parked idea is reopened only by the owner; when reopened, it becomes a module or open questions above.

| ID | Idea | Parked on | Why parked | If reopened |
| --- | --- | --- | --- | --- |
| P1 | **Fakémon**: fan-made Pokémon shown in the platform, fully separated from official Pokémon (own section and IDs, always labelled fan-made). No competitive section. | 2026-11-04 | Copyright of fan creations made by others, and their artwork would have to be stored, unlike official images (D18). | Scope ceiling: official types and rules, plus at most custom moves and abilities. New types or rules are excluded. Estimated size: one milestone plus content work, mostly adding data. Kept cheap by the architecture guidelines: types read from data, IDs treated as opaque text, entry sections receive their data, image URLs come from data. |
| P2 | **PokéPaste links**: import a team by pasting a `pokepast.es` link (its `/json` and `/raw` views allow reading from any website), and export a team to a new paste through PokéPaste's public form. | 2026-11-08 | Less used than plain Showdown text, which is already imported and exported (STR-F05, STR-F06). | Small: reuses the Showdown importer; the paste's title becomes the team name. Credit PokéPaste on About. |
