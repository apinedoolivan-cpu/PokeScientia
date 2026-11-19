# Pokescientia — Design and Interaction

**Version 1.13 — approved 2026-11-19** · Owner: @Alex

## Document status

Version 1.13, approved. Defines how Pokescientia looks, reads, moves and speaks. It applies the approved functional spec (`02`) and architecture (`04`); it does not add features.

- **Approved decisions** from the design exploration are recorded as **D58–D64** (section 15) and in the vision document.
- Items marked **Proposal DP-n** are still open: each is decided at its review point in the roadmap (D67) and then becomes a `D` entry. Approving this document does not approve them.
- The visual reference is the **"Pokescientia — Style Exploration"** design canvas (claude.ai artifact, private to the owner), row 8 "Pokescientia, Roman academy — consolidated set". When this document and the canvas disagree, this document wins.

## 1. Identity: a Roman academy of natural science

Pokescientia is a **Roman academy** (D58): a place of learning, strategy and spectacle, built of marble and travertine, lit by day and by torchlight at night.

Why Roman (decided 2026-11-06):

- **The name is Latin.** *Scientia* means knowledge.
- **The book is Roman.** The codex (a book with pages) took over from the scroll in the Roman era, which matches the Pokédex-as-a-book concept (D61).
- **It covers both halves of the project.** Rome had great libraries (knowledge) and the amphitheater (competition), the platform's main lens (R4).
- **Spanish comes from Latin**, so hall names feel natural in the primary language (R9).

Greek learning appears as **content, not as a second style**. Rome preserved and built on it, as Trajan's library did with its Greek and Latin halls. The Pokédex's model is Pliny the Elder's *Naturalis Historia*, which itself drew on Aristotle.

**What the identity avoids:** imperial political symbols (eagle standards, fasces) that have been appropriated by extremist movements; official Pokémon logos and Poké Ball imagery; anything that would make the site look official.

## 2. Brand and voice

| Element | Definition |
| --- | --- |
| Wordmark | `POKESCIENTIA` in Cinzel, letter-spaced, as a carved inscription |
| Tagline | *Academia de ciencias Pokémon* / *Academy of Pokémon sciences* |
| Emblem | An original laurel wreath around a five-pointed star, drawn as line art in the ornament color. Never a Poké Ball, never official marks. |
| Disclaimer | Visible in the footer of the entrance and on About (Constraints) |

**Voice:**

- Spanish uses **`tú`**: close and friendly, never formal. English is equally friendly.
- Texts are **informative and short**. The academy's elegance comes from the visuals, not from formal wording.
- **Presenters speak in the first person** ("Te doy la bienvenida a la Biblioteca…").
- **Latin appears only** in inscriptions, book titles and running heads (BIBLIOTHECA, LIBER I). Every Latin word is next to a plain explanation: the menu, a description, or the context.
- Competitive jargon (2HKO, spread) is used where players expect it, with a short explanation the first time it appears in a hall.

## 3. Halls and navigation

### Naming rule (D59)

**Function in the menu, theme in the world.** The navigation uses plain, instantly recognizable names in the active language. The Latin inscription appears in the hall itself: over the entrance doors, as the hall heading, and in the presenter's words. The Colosseum is the one exception: "Coliseo" is clear enough to be its own menu label.

### Hall map (D60)

| Menu (es) | Menu (en) | Inscription | Purpose | Wing | Module | Phase | Route (D17) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Inicio | Home | **ATRIUM** | Entrance, the doors to every hall | — | M0 | 0 | `/` |
| Pokédex | Pokédex | **BIBLIOTHECA** | The *Historia Naturalis*: every species, move, ability and item | Knowledge | M2 | 1 | `/pokedex`… |
| Equipos | Teams | **LEGIO** | Build a team of six and study its strengths and weaknesses | Strategy | M3 | 2 | `/teams` |
| Calculadora | Calculator | **ABACUS** | Damage, rolls and KO probabilities | Strategy | M4 | 3 | `/calculator` |
| Metajuego | Metagame | **ATHENAEUM** | What is used: common sets, partners, trends | Strategy | M4 | 3 | `/metagame` |
| Coliseo | Colosseum | **COLOSSEUM** | Turn-by-turn doubles battle testing, with an animated stage | Strategy and spectacle | M5 | 4 | `/colosseum` |
| Foro | Forum | **FORUM** | The public square: open a topic and discuss it, with teams, calculations and battles attached | Community | M9 | 6 | `/forum` |
| Quiz | Quiz | **AENIGMA** | Riddles and challenges | Knowledge | M7 | 7 | `/quiz` |

Strategy and information get more halls than spectacle, on purpose: battles are one part of the academy, not its center. The FORUM is the one community hall (D85): the Roman forum was where citizens met and argued, so the name says what the hall does in both languages. *Forum* is the Latin word; *foro* is its Spanish descendant.

**Halls that don't exist yet** appear at the entrance as **closed doors** with their phase ("Fase 3"), and are not navigable (resolves the open point in SHL rules).

### Navigation pattern (Proposal DP-1)

- **Desktop:** a top bar with the wordmark, the menu, the language switch and the theme switch, followed by the ornament band.
- **Phone:** the menu collapses into a "Salas" button that opens a full-screen list of halls, each with its inscription and one-line description.
- **Within a hall:** the hall header shows the presenter, the inscription and a short introduction. A breadcrumb in small capitals (BIBLIOTHECA · HISTORIA NATURALIS · LIBER I) shows depth.

## 4. Color

### Day and night (D62)

The light theme is **Día** (the forum in daylight); the dark theme is **Noche** (the forum by torchlight).

Which one shows:

1. The visitor's **manual choice**, if they made one (remembered, D43).
2. Otherwise, if they turned on **"Seguir la hora del día"**: Día from 07:00 to 20:00 local time, Noche otherwise.
3. Otherwise, the **device or browser setting** (`prefers-color-scheme`). This is the default.

### Palettes (D63)

**Travertino is the provisional palette** (named Foro until D88, same values). Pompeya, Mosaico and Púrpura imperial remain as alternatives; the final choice is made once real pages exist. Changing it means editing one tokens file (section 4, "Tokens").

**Travertino** — travertine, porphyry, bronze:

| Semantic token | Día | Noche | Used for |
| --- | --- | --- | --- |
| `--color-bg` | `#F4EFE6` | `#16120F` | Page background |
| `--color-desk` | `#EAE3D7` | `#0F0C0A` | Background behind the book |
| `--color-surface` | `#FFFFFF` | `#211B16` | Cards, header, panels |
| `--color-page` | `#FDFAF4` | `#241D17` | Book pages |
| `--color-niche` | `#EEE7DD` | `#2A221B` | Presenter niches, inset areas |
| `--color-text` | `#221B17` | `#F1E8DC` | Body text |
| `--color-text-muted` | `#625850` | `#B3A696` | Secondary text, labels |
| `--color-accent` | `#7A1F2B` | `#E39A8E` | Links, active states, bars |
| `--color-on-accent` | `#FFFFFF` | `#16120F` | Text on accent |
| `--color-ornament` | `#A8812E` | `#D9B05E` | Laurel, dentils, plinth borders (decoration only) |
| `--color-ornament-text` | `#7E5F1E` | `#D9B05E` | Ornament-colored text that must be readable |
| `--color-line` | `#E2D9CC` | `#3A3028` | Borders, dividers, bar tracks |
| `--color-warning-bg` / `-line` / `-text` | `#FBEFD9` / `#D9B76E` / `#7A4A0E` | `#3A2C14` / `#7A5E24` / `#F2C77A` | Rule warnings (STR-F04) |
| `--color-success` | `#3C6B3E` | `#8FC79A` | Checks in "doubles essentials" |

**Alternatives** (main values; full token sets are on the canvas):

| Palette | Día: bg / text / accent / ornament | Noche: bg / text / accent / ornament | Character |
| --- | --- | --- | --- |
| Pompeya | `#F6EEDF` / `#261A14` / `#9B2D20` / `#B7832B` | `#141010` / `#F3E6D6` / `#E8826C` / `#E0B25A` | Fresco red and ochre: warm and distinctive |
| Mosaico | `#F3F1EC` / `#1E2228` / `#1E5A74` / `#B5482E` | `#0F1518` / `#E6EEF0` / `#6DB7CC` / `#E0866A` | Teal tesserae and terracotta: calm and scientific |
| Púrpura imperial | `#F5F2EE` / `#211A1E` / `#5E2750` / `#A8812E` | `#170F14` / `#F1E6EA` / `#C79BD0` / `#D9B45A` | Tyrian purple and gold: luxurious |

### Type colors

The 18 type colors keep their familiar hues but are **adjusted to the theme**, so they stay recognizable and readable:

- Each type has a fixed hue and saturation (for example Fuego 18°/72%, Agua 212°/62%, Acero 208°/18%).
- **Día:** background at 87% lightness, text at 21%, border at 70%.
- **Noche:** background at 24% lightness, text at 86%, border at 38%, with reduced saturation.
- Type badges always show the **type name**, never color alone (D20).

The exact hue table lives with the tokens and is generated, not hand-picked per palette.

### Rules

- Components use **semantic tokens only**, never raw colors (architecture §8). A lint rule enforces it.
- Every text/background pair meets **WCAG AA** (4.5:1 for text, 3:1 for large text and UI shapes) in both modes and every palette. axe checks it in CI.
- `--color-ornament` is for decoration; text in ornament color uses `--color-ornament-text`.

## 5. Typography (Proposal DP-2)

| Role | Font | Rules |
| --- | --- | --- |
| **Inscriptions and names** | **Cinzel** (Roman inscriptional capitals), weights 400 and 600 | Wordmark, hall inscriptions, plinths, Pokémon names, book titles, running heads. Short texts only (about 40 characters at most). Letter-spaced for inscriptions. |
| **Text and data** | **Alegreya Sans**, weights 400, 500 and 700 | Everything else: menu, body text, buttons, tables, numbers. Numbers use tabular figures in stats and tables. |

- Both fonts are **SIL Open Font License**, self-hosted through Fontsource (architecture §8, R18).
- **Scale** (desktop; phones step down one level): 56 / 44 / 32 / 24 / 20 / 17 (body) / 15 / 13 px.
- **Line height:** 1.5 for body text, 1.05–1.2 for headings.
- Body text never goes below 15 px; labels never below 12 px.

## 6. Ornament and texture

| Motif | Where | Notes |
| --- | --- | --- |
| **Dentil band** | Under the header on every page | The signature divider |
| **Arch** | Entrance doors, presenter niches | Round top, flat base |
| **Plinth** | Under presenters and on door inscriptions | Cinzel text, ornament-colored border |
| **Laurel** | Emblem; optional accents (completed analyses, results) | Line art |
| **Roman numerals** | Book numbers (LIBER I), thumb index, page numbers | Arabic numerals for all data (stats, IDs, damage) |
| **Abacus beads** | ABACUS hall header | A small decorative abacus |

**Rules:**

- All ornaments are **original SVG line art drawn with tokens** (`currentColor` or semantic variables), so they follow palette and theme.
- Textures (marble, travertine, paper) are **optional and subtle**. Any texture file must be free-licensed, for example CC0 (R18). Sources are chosen when needed (Q29).
- Ornament never carries information.

## 7. Presenters

### Frame (Proposal DP-3)

The same frame in every hall: the presenter stands **under a Roman arch**, on a **plinth** with its name inscribed in Cinzel. It combines the "statue in a niche" and "bust and inscription" patterns explored on the canvas. The arch and plinth are the setting only: the Pokémon in it is shown alive, never as a statue (D91).

### Behavior

- **Phase 0–2 (D14):** the presenter appears in the hall header with a short introduction (one or two sentences). The introduction can be dismissed and stays dismissed.
- **Later:** an optional **companion** mode (a small portrait in a corner offering tips, which can be hidden) may be added. Not in the MVP.
- **Phase 7 (D82):** each presenter becomes the AI assistant's voice in its hall, as the hall's *genius loci*, and can hand a question to another presenter. All presenters are peers. The companion mode is a natural way to reach it; details are open (Q82).
- **Image treatment (Proposal DP-4):** official artwork in **original color** by default. A duotone or "statue" treatment of presenters is ruled out (D91): they will speak for the assistant, so they look alive.

### Cast (D84)

Four rules (D82, D84, D91, D94): a presenter's **lore or a clear symbol must tell what its hall does**, so it is believable as that hall's teacher; it has **a clear personality that matches that function**; that personality is **vivid and its own**, so that in Phase 7 talking to the assistant feels like talking to that presenter; and it has **a responsibility only when it does a real job** that passes the three tests below. Presenters are shown alive, in original color. The personality sets the tone of its introductions and, in Phase 7, of its assistant voice; it never changes facts or numbers (D76). Each voice is an original academy role, not an imitation of the Pokémon's official personality (Q82). Any presenter may be swapped before its hall is built.

| Hall | Presenter | Why |
| --- | --- | --- |
| ATRIUM | **Arcanine** (Kanto form) | The guardian dog at the door, as in the *cave canem* mosaics of Pompeian entrances; noble, loyal and honorable, once thought a legendary Pokémon |
| BIBLIOTHECA | **Mew** | Said to carry the DNA of every Pokémon: the natural keeper of a book about all of them |
| LEGIO | **Falinks** | Designed after a military formation, and literally a group of six |
| ABACUS | **Metagross** | Its Pokédex entries describe four brains that solve complex calculations faster than a supercomputer and analyze opponents precisely |
| ATHENAEUM | **Noctowl** | The owl of Athena, symbol of wisdom (our association, not Game Freak's); turns its head to think, and in lore sees several futures and chooses one after weighing them |
| COLOSSEUM | **Incineroar** | A wrestler for the arena, and a face of competitive play |
| FORUM | **Braviary** (Unova form) | The Roman *aquila*, the eagle that carried **SPQR**, "the Senate and People of Rome": the emblem of the people who met in the forum. Its lore calls it a motif for emblems, and the "soldiers of the sky" that fight tirelessly to protect their friends. Jupiter's eagle carried his will, and any bird links to messages |
| AENIGMA | **Delphox** | Named after Delphi and its oracle, famous for answering in riddles; in lore, its burn marks were read for divination |

### Personalities and responsibilities (D94)

Every presenter has a **personality**. A presenter has a **responsibility** only when it does a real job in the academy, beyond answering questions about its hall. Every presenter answers questions, and the way it answers (in words, by opening a tool already set up, by telling a story) is part of its personality, not a responsibility. A job counts as a responsibility only if it passes **all three tests**:

1. **It acts or produces something** that stays on the site after the conversation: a hidden post, a published thread, a changed team, a score.
2. **It owns a process:** it does the work at its own moment (every report, every week, every turn, every round), not only when asked.
3. **Without it, something stops happening:** removing the presenter leaves part of the academy with no one doing it. Removing only its answers leaves the hall working.

Like every voice, a responsibility follows D76: code produces every fact and number; the presenter decides how to say it and, where allowed, proposes actions. Responsibilities arrive with the assistant in Phase 7 unless stated otherwise. Future presenters are cast with the same test.

| Presenter | Personality | Responsibility | Way of answering (not a responsibility) |
| --- | --- | --- | --- |
| **Arcanine** (ATRIUM) | The old guard dog of the house. Warm, noble and unhurried; has greeted every visitor since the academy opened and is proud of the house. Talks about the other presenters like family ("Falinks will shout at you, but it means well"). Knows a little of every hall, never pretends to be an expert, and never lets anyone leave lost: every answer ends at a door | **None.** Guiding is giving information, and every presenter can already hand a question on (D82); making Arcanine the place every question goes through would make it the head, which D82 rules out | Points the way to the right hall |
| **Mew** (BIBLIOTHECA) | The naturalist who has met them all. Curious, playful and easily delighted; treats every species as a favorite, the obscure ones included, and always has one odd detail to share ("Did you know…?"). Wanders into trivia but always lands on the fact. Refuses to say which Pokémon is "best" and sends you to Noctowl | **None.** Its hall is pure knowledge | Tells the origin and inspiration of a Pokémon |
| **Falinks** (LEGIO) | The drill sergeant, a squad of six. Short, clipped orders, and it speaks as "we". Reports as an inspection: "Formation: … Weak flank: … Orders: …". Blunt about the team, never about the trainer. A well-covered team earns a salute, rare and meant | **Inspecting and fixing formations:** team critique (AIA-F01) plus proposed fixes the trainer accepts or rejects one by one, and an inspection offered when a team enters the COLOSSEUM or is attached to a FORUM post (AIA-F05). It warns and proposes; it never blocks (D27) | — |
| **Metagross** (ABACUS) | The reckoner. Calm, exact, never in a hurry. States its assumptions before its result ("Assuming Adamant, 32 SP in Attack…"), never rounds without saying so, and replaces "probably" with a percentage. Not cold, only precise; closes a result with one word: "Calculated." | **None.** Its hall is answered by the calculator itself | Sets up a calculation from a plain question ("Does my Flutter Mane knock out Incineroar in the sun?") and opens ABACUS with it loaded, assumptions shown |
| **Noctowl** (ATHENAEUM) | The night strategist. Measured and patient; pauses before answering, sets out options ("Two paths…") and explains why one wins. Unlike Metagross, at ease with uncertainty: the metagame is likelihoods, not certainties. Remembers how past regulations went and likes to point out patterns | **The metagame report:** writes the weekly "metagame of the week" thread in the FORUM (FOR-F13; a template in Phase 6, Noctowl's voice from Phase 7) and a briefing when a new regulation arrives (AIA-F06) | — |
| **Incineroar** (COLOSSEUM) | The showman in your corner. Loud and theatrical while a battle plays: narrates big plays, hypes a good read, loves a comeback. Between turns it drops the act and gives straight advice like a coach. Owns mistakes ("That one's on us") and never sugarcoats a losing position | **Coaching the battle:** the turn advisor (AIA-F03, D76) and a review after each battle that points out the two or three turns that decided it (AIA-F07) | — |
| **Braviary** (FORUM) | A proud, brave standard-bearer and the guardian of the square. Welcomes newcomers loudly, raises the best discussions high, and as a bird of prey swoops on abusive posts. Moderation first, messages second | **Reporting and moderation** (AIA-F04, D90): handles every report, may hide a post while it is reviewed, proposes the penalty; a moderator confirms | — |
| **Delphox** (AENIGMA) | The oracle. Enigmatic and playful; speaks in riddles while you play and explains plainly once you answer. Never mocks a wrong answer. Reads the future in the flames ("The embers say… a Water type?") | **Running the quiz** (AIA-F08): phrases each question as a riddle, gives the ladder of hints (QUZ-F03), accepts answers in your own words and keeps the score. A daily riddle is possible (Q89) | — |

Ideas kept open: a **daily riddle** by Delphox (Q89), and a **hint mode** in every hall, where each presenter gives a nudge in its own voice instead of the answer (Q90). Hints stay in each hall's own voice: Delphox does not give hints outside AENIGMA (D82).

**Braviary in detail (D89).** No Pokémon stands for public discussion itself, so, as with Arcanine at the ATRIUM, the cast follows a clearly Roman symbol given a fitting role.

- **The eagle of the people, not of war.** The *aquila* led the legions, but its standard also bore SPQR. In the FORUM it stands for the community the hall exists for, so it does not compete with LEGIO's Falinks: LEGIO forms the team, the eagle is the standard everyone gathers under.
- **The American look.** Braviary is a bald eagle in red, white and blue. The answer is the framing: the idea of an eagle as a state's emblem comes from Rome's *aquila*, so a national eagle is Rome's symbol reused; it is shown alive, in its own colors, like every presenter (D91).
- **The voice of moderation (Phase 7, D90).** When the assistant arrives, Braviary is the main way to report a post and to moderate. Users report by talking to it; it reads the post against the rules, says what it will do and why, may hide the post while it is reviewed, and proposes the penalty, which a moderator confirms. Its brave, protective temper suits the job: firm with abuse, warm with the people it guards.
- **Forum lore for its introductions** (texts present these as the academy's stories):
  - **Pliny's phoenix.** The *Natural History* reports a phoenix brought to Rome under Claudius in 47 CE and shown in the Comitium, the forum's place of assembly, which Pliny judged a fake: Rome's first viral hoax, and a good opening for the rules on false information.
  - **Pliny's pigeons.** During the siege of Mutina, Decimus Brutus sent letters tied to pigeons' feet (*Natural History*, book X): messages carried by air, fitting for reply notices.
  - ***Fama*,** the Roman goddess of rumor, who in Virgil flies about with countless eyes, ears and tongues: material for the voice, as what the guardian keeps in check.

**Considered and set aside:** Pikachu (fame, not meaning), Klefki (keys only), Girafarig/Farigiraf (a Janus link few would read) and Hisuian Arcanine (rock and statue, less alive) for ATRIUM; Alakazam (psychic and magic, not calculation) for ABACUS; Xatu (a passive seer, drawn from specific living cultures) for ATHENAEUM; Zoroark (illusion, not riddles) and Unown (no individual mind) for AENIGMA. For the FORUM: Chatot (mimics sounds, and tropical), Mr. Mime (the minstrel bringing news is not a Roman image), Smeargle (artistic painting more than messages), Grafaiai (a signature tag repeated for life, solitary and poisonous), Primarina (Greek sirens lure sailors to their death), Unfezant (one-to-one messages, kept as lore), Conkeldurr (its Roman concrete builds the square but says nothing about talking in it), Farigiraf (the Janus link again), Lycanroc (no lore of the Roman she-wolf), Exploud (a herald announces but doesn't discuss), Pidgeot, Talonflame, Hawlucha, Staraptor and Swellow (not eagles), Corviknight (a raven, steel rather than bronze, British in theme), Hisuian Braviary (loses the eagle's look), Yveltal (death), Tornadus in Therian Forme (not clearly an eagle; its other form is the wind god Fūjin; storms destroy), Zapdos (Jupiter's eagle holds thunderbolts, but it doesn't look like an eagle) and Moltres (Pliny's phoenix is an anecdote, not the hall's function, and a fourth fire-type presenter).

## 8. The Pokédex as a book: *Historia Naturalis* (D61)

### Structure

- The **BIBLIOTHECA** keeps one work, the ***Historia Naturalis***, divided into **nine books (*libri*)**, one per region: LIBER I · KANTO … LIBER IX · PALDEA.
- **Appendix books** hold moves, abilities, items, types and an A–Z index (D26 detail pages).
- **Scrolls** appear only as ornament (shelf details, chapter title pages), never as the reading format.

### Views

| View | What it shows | Feature |
| --- | --- | --- |
| **Shelf** | The *Historia Naturalis* on its shelf: nine books plus appendices; choosing one offers "Abrir el libro" or "Ver lista" | ARC-F01 entry point |
| **Codex** | One Pokémon per two-page spread (below) | ARC-F03, ARC-F04 |
| **List** | The fast grid with filters and sorting, across all books | ARC-F01, ARC-F02 |

A **"Libros / Lista"** switch is always available. The book is for reading; the list is for finding. Both show the same data and use the same URLs (D17).

### The spread

| Left page: identity | Right page: science |
| --- | --- |
| Running head (HISTORIA NATURALIS · LIBER I · KANTO), name, number, form tabs, artwork, types, height and weight | Base stats, abilities, type effectiveness, evolution chain, links to moves and to "Añadir a una legión" (ARC-F11) |

New sections (R16) are added as **extra pages** after the spread, reached by ribbons or links. The first is the **competitive page** (ARC-F14, D83): VGC, then Doubles, then Singles. In the List view the same section appears below the others.

### Navigation

- **Thumb index:** tabs cut into the page edge, one per book, labelled with Roman numerals and named for screen readers.
- **Previous / next** buttons, keyboard ← →, and swipe on touch screens.
- **Every page has its own URL** (`/es/pokedex/charizard`), so the book never hides shareable links.

### Page turn (Proposal DP-5)

| Context | Animation |
| --- | --- |
| Desktop | The page **turns on the spine** in 3D (GSAP) |
| Phone | The page **slides** sideways, following the finger |
| Reduced motion | A **crossfade**, always |

### On a phone

One page at a time: two tabs, "I · Identidad" and "II · Ciencia", with swipe between Pokémon.

## 9. Layout and page templates (Proposal DP-6)

- **Grid:** 12 columns, maximum content width 1440 px, outer margin 48 px on desktop and 16 px on phones.
- **Spacing scale:** 4, 8, 12, 16, 24, 32, 48 px.
- **Corners:** 2 px (stone-cut, almost square). Arches are the only round shapes.
- **Breakpoints:** phone below 640 px, tablet 640–1024 px, desktop above 1024 px. Everything works from 360 px (X-07).

| Template | Used by | Structure |
| --- | --- | --- |
| **Entrance** | ATRIUM | Title, row of hall doors (arch, presenter, plinth, label, description, phase) |
| **Hall header** | Every hall | Presenter niche, Latin inscription, one or two lines of introduction, hall controls on the right |
| **Shelf** | BIBLIOTHECA | Hall header, bookcase with books and appendices, selected-book panel |
| **Book** | Pokédex entries, appendix pages | Two-page spread, thumb index, previous/next |
| **List** | Pokédex list, moves, abilities, items | Filters, sortable grid or table |
| **Tool** | LEGIO, ABACUS, ATHENAEUM | Hall header, main work area (8 columns), analysis panels (4 columns); stacked on phones |
| **Stage** | COLOSSEUM | Full-width PixiJS stage with playback controls, the turn matrix and the turn history with its branches (Phase 4); laid out when Phase 4 is specified |

## 10. Components (`ui/`, D49)

Built on Angular CDK, styled with tokens, prefixed `ps-`. Pages use only these.

| Component | Purpose |
| --- | --- |
| `ps-button`, `ps-toggle-group` | Actions; segmented choices (Libros/Lista, format, stat system) |
| `ps-search` | Search field with results list (global and per hall) |
| `ps-type-badge` | Type name with its color (never color alone) |
| `ps-tier-badge` | Type tier letter (S to F) with an accessible label ("Rango de tipos: B"); its color supports the letter, never replaces it |
| `ps-stat-bar` | Labelled stat with value and bar |
| `ps-inscription` | Cinzel heading for halls, plinths and running heads |
| `ps-presenter` | Arch, artwork, plinth and dismissible introduction |
| `ps-pokemon-image` | Every Pokémon image: official image or the original fallback (a silhouette or type emblem drawn in the academy's line style), chosen by the image service (X-15) |
| `ps-music-control` | Play or pause, volume and track name in the header; off by default (SHL-F09) |
| `ps-hall-door` | Entrance door (open or closed) |
| `ps-book`, `ps-book-page`, `ps-thumb-index` | The codex and its navigation |
| `ps-card` | Surfaces such as team slots and panels |
| `ps-team-strip` | The active team (X-12): six small sprites with the team name, a switch and an import action; compact on phones. Placed by the shell in the halls that use teams; exact placement decided when built (M2.9) |
| `ps-notice` | Rule warnings and information (non-blocking, D27) |
| `ps-tabs`, `ps-dialog`, `ps-menu` | CDK-based tabs, dialogs, menus |
| `ps-roll-strip`, `ps-probability-bars` | ABACUS results (16 rolls, KO chances) |

## 11. Motion (Proposal DP-7)

**Character:** ceremonial and steady, like a heavy book or a procession. Nothing bounces or flashes.

| Animation | Description | Duration |
| --- | --- | --- |
| Hall entrance | Header fades in; presenter rises slightly into the niche | 400–600 ms |
| Door hover / focus | Door lifts a few pixels; plinth border brightens | 150 ms |
| Page turn | See section 8 | 500–700 ms |
| Stat bars | Fill from zero on first view | 400 ms, staggered |
| Team analysis update | Changed values highlight briefly | 300 ms |
| Theme switch | Colors crossfade | 200 ms |

- Easing: smooth deceleration (GSAP `power2.out`); no elastic or bounce easings.
- Animate only `transform` and `opacity` for performance.
- **Reduced motion (D20):** every animation above becomes a fade under 200 ms or is skipped. Nothing essential depends on motion.

## 12. Accessibility (visual rules)

- Focus is always visible: a 2 px outline in `--color-accent` with a 2 px offset.
- Touch targets are at least 44 × 44 px.
- Type, warnings and status always use text or icons as well as color. Bars (HP, stats) always show their value; coverage cells show their multiplier (D78).
- Every new screen is checked with the browser's color-blindness simulation (protanopia, deuteranopia, tritanopia, achromatopsia).
- Effects never flash more than three times per second (X-13); sound is never essential (X-14).
- Inscriptions in Latin are real text (not images), so screen readers read them, followed by their plain meaning where needed (for example with an accessible label).
- Contrast and focus are checked by axe in both modes (architecture §11).

## 13. Effect on other documents

- **Module names:** M2 is the Pokédex (BIBLIOTHECA), M3 Teams (LEGIO), M4 Calculator and metagame (ABACUS, ATHENAEUM), M5 the **battle stage** (COLOSSEUM), formerly "Animation Lab". Feature IDs (`ARC-`, `STR-`, `CMP-`, `LAB-`) do not change.
- **Routes and folders** in the architecture use the English menu words: `/teams`, `/calculator`, `/metagame`, `/colosseum`, `/forum`, `/quiz`.
- **D5** (even Greek–museum blend) is superseded by **D58**.

## 14. Open items

| Item | Decide by | Notes |
| --- | --- | --- |
| Final palette (D63) | After the first real pages (Phase 0–1) | Travertino is provisional (D88) |
| Presenter swaps (D84) | Before each hall is built | Cast decided; any presenter may still change |
| Texture sources (Q29) | When textures are needed | Free-licensed only |
| COLOSSEUM design | Phase 4 specification | Includes Three.js exploration (Q63) |
| FORUM design | Phase 6 specification | Thread list, thread page, attachment cards, votes, report and moderation screens; Braviary's frame and the report conversation (D89, D90) |
| Companion presenters | After the MVP | Optional; in Phase 7 a way to reach the assistant (D82, Q82) |

## 15. Decisions and proposals

### Approved (2026-11-06)

| ID | Decision |
| --- | --- |
| D58 | Visual identity: a Roman academy of natural science. Greek learning appears as content, not as a second style. Supersedes D5. |
| D59 | Naming: the menu uses plain names in the active language; halls carry Latin inscriptions. "Coliseo" is also its own menu label. |
| D60 | Hall map: ATRIUM, BIBLIOTHECA, LEGIO, ABACUS, ATHENAEUM, COLOSSEUM, AENIGMA (section 3). |
| D61 | The Pokédex is the *Historia Naturalis*: nine books plus appendices, read as a codex with thumb index and page turns; a List view is always available; scrolls are ornament only. |
| D62 | Themes are Día (light) and Noche (dark); the default follows the device; a manual choice is remembered; an optional mode follows the time of day. |
| D63 | Foro is the provisional palette; Pompeya, Mosaico and Púrpura imperial remain alternatives until real pages exist. (Renamed Travertino by D88.) |
| D64 | The battle stage is the COLOSSEUM (module M5, formerly "Animation Lab"); strategy and information halls outnumber spectacle. |

### Approved (2026-11-14)

| ID | Decision |
| --- | --- |
| D82 | Each hall's presenter is the AI assistant's voice in that hall (its *genius loci*); presenters are peers and can hand questions to each other. Details in Q82 (Phase 7). Supersedes the separate assistant figure (Q74). |

### Approved (2026-11-16)

| ID | Decision |
| --- | --- |
| D84 | Presenter cast (section 7): Arcanine, Mew, Falinks, Metagross, Noctowl, Incineroar, Delphox. Each fits its hall through lore or symbolism and has a personality that matches its function. Closes Q3. |
| D85 | The FORUM (menu Foro / Forum, route `/forum`), the community hall: Reddit-style topics, replies and votes, with attachments from the other halls (section 3). Presenter open (Q85), cast by D89. |
| D88 | The provisional palette Foro is renamed Travertino, with the same values (section 4). |
| D89 | FORUM presenter: Braviary, the *aquila* of SPQR, a proud guardian of the square with moderation as its role (section 7). Closes Q85. |
| D90 | In Phase 7 Braviary is the AI face of reporting and moderation; it proposes, a moderator confirms penalties, appeals go to a person (section 7). |
| D91 | Presenters are shown alive, in original color, each with a vivid personality of its own; no statue treatment for Braviary (section 7). Revises the image part of D89. |

### Approved (2026-11-19)

| ID | Decision |
| --- | --- |
| D94 | Every presenter has a personality; a responsibility only when it passes three tests (acts, owns a process, missed if removed). Responsibilities: Falinks inspects and fixes teams, Noctowl writes the metagame report, Incineroar coaches the battle, Delphox runs the quiz, Braviary moderates (D90). None for Arcanine, Mew and Metagross; their ways of answering are noted (section 7). |

### Proposals awaiting approval

Each proposal is decided on a real page at a fixed review point in the roadmap (D67): DP-2, DP-6 and DP-7 in M0.4; DP-1 in M0.6; DP-3 and DP-4 in M0.7; DP-5 in M1.5.

| ID | Proposal | Section |
| --- | --- | --- |
| DP-1 | Navigation: top bar on desktop, "Salas" full-screen menu on phones, hall header and breadcrumb | 3 |
| DP-2 | Typography: Cinzel for inscriptions and names, Alegreya Sans for everything else; scale and rules | 5 |
| DP-3 | Presenter frame: the presenter, shown alive, under a Roman arch on an inscribed plinth, same in every hall | 7 |
| DP-4 | Official artwork shown in original color by default | 7 |
| DP-5 | Page turn: on the spine (desktop), slide (phone), crossfade (reduced motion) | 8 |
| DP-6 | Layout: 12-column grid, spacing scale, 2 px corners, breakpoints, page templates | 9 |
| DP-7 | Motion: ceremonial character, durations and easing | 11 |
