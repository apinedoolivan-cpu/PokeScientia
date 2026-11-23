# Pokescientia — Decision Map

Last updated: 2026-11-23

Every product and technical decision, grouped by when it must be made. This file is the only place open questions are tracked. When a question is decided, its approved text goes into [`01-vision-and-requirements.md`](01-vision-and-requirements.md) (or the relevant doc) as a `D` entry, and its row here changes to **Decided**.

**Kind:** Product = only the owner decides · Technical = Claude proposes, owner approves · Research = facts must be checked first.

## Summary

| Stage | Decided | Open |
| --- | --- | --- |
| A. Discovery and module spec | 32 | 0 |
| B. Architecture (before `ng new`) | 19 | 0 |
| C. Data strategy | 8 | 0 |
| D. Design spec | 8 | 3 |
| E. Later phases | 2 | 19 |
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
| Q48 | Which items the Pokédex shows | Product | Decided → D31, revised by D100 (every item, battle items in full) |
| Q49 | Learnset scope and team formats | Product | Decided → D32 |
| Q50 | Competitive middle evolutions list | Product | Decided → D33 |
| Q51 | Team saving | Product | Decided → D34 |
| Q70 | Teams across halls and calculations with one's own team | Product | Decided → D68, D69 |
| Q71 | PokéPaste links | Product | Decided → D95 (parked as P2 by D70, reopened 2026-11-19) |
| Q72 | Ranking type combinations | Product | Decided → D71 |
| Q73 | Team coverage: team or member view | Product | Decided → D72 |
| Q5 | Battle stage: real or scripted damage | Product | Decided → D73, LAB-F04 (always real) |
| Q76 | What the COLOSSEUM is for, and how turns are resolved | Product | Decided → D73, D74, D75 |
| Q77 | What the AI assistant is mainly for, and how it relates to the rival | Product | Decided → D76, D77 |
| Q78 | Accessibility for color blindness, deafness and blindness | Product | Decided → D78 (low-cost measures only; costlier ones parked as P3) |
| Q79 | Using official Pokémon images without permission | Product | Decided → D79 (fan-content stance with safeguards, X-15) |
| Q80 | Music | Product | Decided → D80 (free-licensed tracks only, SHL-F09) |
| Q81 | Ranking Pokémon | Product | Decided → D81 (Smogon's official tiers, plus the VGC usage rank; no hand-made list), revised by D83 |
| Q83 | Rankings that fit the VGC focus and the full Pokédex | Product | Decided → D83 (competitive section: VGC usage now and best ever, then Doubles, then singles) |

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
| Q59 | Commit message convention | Technical | Decided → D53 (revised by D92: rules in architecture §12) |
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
| Q3 | Presenter cast per section | Product | Decided → D84 (Arcanine, Mew, Falinks, Metagross, Noctowl, Incineroar, Delphox; each with a personality that matches its hall). Still open to swaps before each hall is built. FORUM: Braviary (D89, closes Q85). |
| Q27 | Hall names and navigation structure | Product | Decided → D59, D60 |
| Q28 | Typography and color palette | Design | **Open.** Palette: Travertino provisional (D63; named Foro until D88), final choice after the first real pages. Typography: proposed as DP-2. |
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
| Q75 | **Battle engine check** (D74): confirm that `@pkmn/sim` supports Champions and its doubles rules, that outcomes can be forced (rolls, critical hits, accuracy, secondary effects, speed ties), that battle states can be saved and restored for branching, and **how fast it simulates**: turns per second in the browser and the time to copy a battle state, which decide how many playouts the win estimates can afford (AIA-F03, Phase 7). Done as a spike, like M0.3; the fallback for anything unsupported is decided then. | Phase 4 start |
| Q6 | Login method | Phase 5 |
| Q34 | Go web framework and database | Phase 5 |
| Q7 | Hosting for frontend and backend, on free tiers | First deployment |
| Q35 | Address: free subdomain (a paid domain breaks R7) | First deployment |
| Q84 | **Build or adopt the FORUM** (D85). Our own forum on the Go API and Angular fits the academy and the backend learning goal (R12), but trust levels, filters and moderation tools must be built. Discourse (open source) includes all of them, but needs its own server (R7: free hosting) and would look and behave like a separate site. | Phase 6 start |
| Q85 | FORUM presenter, cast with D84's two rules. Reviewed on 2026-11-17: Chatot, Mr. Mime, Smeargle, Grafaiai, Primarina, Unfezant, Conkeldurr, the eagles and other birds of prey, and the legendary birds (Tornadus in Therian Forme, Zapdos, Moltres). | Decided → D89 (Braviary, the *aquila* of SPQR) |
| Q86 | **Legal requirements for user content** (research): EU data protection (GDPR) and the duties of a hosting service under the Digital Services Act (reporting illegal content, giving reasons for removals); the minimum age to sign up in Spain; terms of use and privacy policy; what happens to posts when an account is deleted (ACC-F04); whether the public ACTA names the user (D96). | Phase 6 specification |
| Q87 | **Free tools for the CAPTCHA and the automatic filters** (R7), and how filtered posts reach the review queue (D87). | Phase 6 specification |
| Q88 | **Braviary acting alone on clear cases** (D90, option B of the review). Once its moderation runs, measure how often moderators agree with its proposals; if it proves reliable, let it remove obvious spam and flagrant abuse and apply the penalty by itself, with every decision open to appeal to a person. Revises D87 for those cases only. Prompt injection (a post written to make Braviary approve it or punish someone else) is part of that measurement (Q91). | After Braviary's moderation has run (Phase 7) |
| Q89 | **Daily riddle** (D94). One riddle a day by Delphox, the same for everyone, with hints that unlock during the day; it could also show as a small card at the entrance, still Delphox's riddle. Possible, not decided. | Phase 7 specification (AENIGMA) |
| Q90 | **Hint mode in every hall** (D94). A "give me a hint, not the answer" option, where each presenter gives a nudge in its own voice (for example Incineroar in the COLOSSEUM), useful for learning. Never Delphox outside AENIGMA (D82). | Phase 7 specification (assistant) |
| Q91 | **Account security checklist** (D98), part of the accounts specification. Proposed, not decided: prefer a sign-in that stores no passwords (Google or GitHub sign-in, or email links; tied to Q6), otherwise hash with Argon2id or bcrypt; store only email, display name and teams; sessions in HttpOnly, Secure, SameSite cookies, never tokens in localStorage; the server checks that every team or post belongs to the signed-in user, with a test per endpoint; parameterised SQL only (tied to Q34); secrets in the host's environment variables (`.env` is never committed); rate limits on sign-in; account deletion really deletes (ACC-F04). **From Phase 6:** posts rendered from a small Markdown subset and sanitised on the server. **From Phase 7:** a user's own AI key (Q8) stays in their browser and never reaches our server; post text is treated as data, never as instructions (prompt injection, Q88). | Phase 5 specification |
| Q92 | **Item usage** (D99, D100). Proposed, not decided: on each battle item's page, the Pokémon that hold it most and how often; in the ATHENAEUM, a ranking of the most used items in the regulation, each with its top holders; in LEGIO, the team's six items at a glance. All from the Smogon statistics already planned (D41). | Phase 3 specification |
| Q93 | **When each item entered Champions** (research, D101). Showdown's data says whether an item is available now, not since when. Options: compare Showdown's per-regulation Champions data (a mod for the previous regulation exists), or a small hand-written file with the items each regulation added. Also check, at each data refresh, Showdown's list of available items against the official regulation list. | M2.5 (regulation data) |
| Q94 | **CIRCUS, a hall for watching official VGC competition** (proposed by the owner on 2026-11-22, not decided; the owner leans to the name CIRCUS and, on 2026-11-23, to a single simple page). The ATHENAEUM shows what is used on Showdown's ladder (D41) and never covers official tournaments; the CIRCUS is where you **watch** the competition, not a second source of data. **Why CIRCUS:** the Circus Maximus and the Colosseum were different buildings for different shows. The amphitheatre (Colosseum, finished in 80 CE) held gladiator fights and beast hunts; the circus (from the 6th century BCE, far larger) held the chariot races, Rome's most followed competition, watched by huge crowds, with four factions (Reds, Whites, Blues, Greens) and star charioteers whose careers were recorded on stone (Gaius Appuleius Diocles, born in Lusitania). The COLOSSEUM stays where you fight your own battles; the CIRCUS is where you sit in the stands and watch the champions. The menu label stays a plain word (D59), so *circo* never appears alone. **One page, no rooms**, like LEGIO, ABACUS and the ATHENAEUM (Tool-like layout, design §9): (1) the **player**, the centre of the hall, embedding the official YouTube and Twitch channels (official embed players with click-to-load, never downloaded, re-uploaded or restreamed): the current or latest tournament, live while it runs; (2) a **side panel** with the event's facts: name, dates, place, game, regulation, winner when known, and links to the official site and community sources for full standings (we link instead of competing); (3) a **row of past replays** to choose from, mainly finals of past Internationals and Worlds, with season and event, growing backwards one season at a time; (4) the **top players of the season**, a short list with name, country and Championship Points, linking out for details. (5) **both players' teams beside the replay** (the owner wants this, 2026-11-23), each with a button to open it in LEGIO (Free format with warnings for earlier games, D27, D32). How: official VGC uses open team sheets (species, form, ability, item, moves, nature in Champions; Tera Type in Scarlet/Violet; never stats), and RK9 publishes the lists during the event. A team is fixed for the whole tournament, so no live data feed is needed: when a replay is added, its two players' lists are copied by hand with a source link. Teams appear on replays only; during a live stream the broadcast itself shows them. Stats are missing, so a team opened in LEGIO gets default spreads, labelled as such. No live game data exists (picks, HP): official matches run on consoles and publish no battle log; reading them from video with computer vision was looked at and set aside (it needs the video downloaded). **Proposed scope:** VGC only (no TCG, Pokémon GO or UNITE); Masters division only (Juniors and Seniors are minors); the big events of the official circuit (Internationals and Worlds). Not in the hall: standings tables, brackets, player profile pages, event hosting or matchmaking (non-goal; the FORUM and Showdown cover that). **Identity:** the circus as decoration, not structure: the player seen from the stands, faction colors as accents, the top players as a short honors inscription. **Data:** small and hand-curated in `pipeline/manual/`: per event its facts, source links and video IDs; per replay its two players and their team lists; per season the top players. No official open API. Presenter not chosen. | After Phase 3 (ATHENAEUM) |
| Q95 | **Other tournaments and the top players of the moment** (research, tied to Q94). Kept open on purpose: whether and how to cover Regionals, Special Events and big online tournaments later. For the best players now, sources to check: the official Championship Points standings (the season's own measure, also mirrored with history by community leaderboards), Travel Award standings per region (Victory Road), all-time points and earnings rankings (Limitless VGC), Liquipedia results. Showdown's ladder is not used: its usernames are anonymous. Check each source's terms before use. | Q94 specification |
| Q8 | AI model source. Options noted, not decided: the owner's own API key entered in settings (never stored or paid by the site), a provider's free tier, or a small model running in the browser. Must respect R7 (free resources); the turn advisor's steps 1–3 work without any model (D76). | Phase 7 |
| Q74 | AI assistant presenter. Magearna (the leaning) and Rotom were considered on 2026-11-09; neither fitted both the academy and an AI. | Decided → D82 (each hall's presenter is the assistant's voice) |
| Q82 | **AI assistant voices** (D82). Open, options noted: **hand-offs** between presenters (what passes along: a short structured summary of team, turn and question, not the whole conversation); **different models per presenter**, possible because only the voice depends on the model (tied to Q8); a **plain label** on every assistant panel saying it is an AI speaking through the character; a **switch that turns personas off** for a neutral academy voice, like D79's image fallback; **one shared core prompt** plus a short style card per presenter, in both languages; **how much character** the voice may show against D76's predictable tutor (numbers, evidence and assumptions drawn by code in neutral UI, never in character); each voice is an **original academy role**, not an imitation of the Pokémon's official personality; the companion mode (design §7) as the way to reach the assistant. | Phase 7 |

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
| P2 | **PokéPaste links**: import a team by pasting a `pokepast.es` link, and export a team to a new paste. **Reopened by the owner on 2026-11-19 → D95** (STR-F23 to STR-F26). | 2026-11-08 | Less used than plain Showdown text, which is already imported and exported (STR-F05, STR-F06). | — |
| P3 | **Costlier accessibility options**: a color-blind-friendly palette (about 4–8 h, one more token set), a high-contrast theme (about 6–10 h), spoken announcements of battle events for screen readers (about 6–10 h), a battle fully playable by ear, AAA compliance, a professional audit. | 2026-11-11 | The owner applies only low-cost measures (D78). | Tokens keep the palette and contrast options cheap if ever wanted. |
| P4 | **Visible user ranks**, possibly named after Roman military ranks. Not designed yet. | 2026-11-20 | The owner wants every user seen as the same for now (D97); trust levels stay internal. | Design first what a rank means and how it is earned, and check it doesn't undo D97's reason (no classes of users). LEGIO already uses the military theme, and Roman ranks need a plain name next to them (D59). |
