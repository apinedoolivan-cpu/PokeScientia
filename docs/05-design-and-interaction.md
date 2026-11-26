# Pokescientia — Design and Interaction

**Version 1.22 — approved 2026-11-26** · Owner: @Alex

## Document status

Version 1.22, approved. Defines how Pokescientia looks, reads, moves and speaks. It applies the approved functional spec (`02`) and architecture (`04`); it does not add features.

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
| Pokédex | Pokédex | **BIBLIOTHECA** | The *Historia Naturalis*: every species, move and ability; with the ARMAMENTARIUM (items), the HERBARIUM (berries) and the PANTHEON (legendary and similar Pokémon) as books on its shelves (D110) | Knowledge | M2 | 1 | `/pokedex`… |
| Equipos | Teams | **LEGIO** | Build a team of six and study its strengths and weaknesses | Strategy | M3 | 2 | `/teams` |
| Calculadora | Calculator | **ABACUS** | Damage, rolls and KO probabilities | Strategy | M4 | 3 | `/calculator` |
| Estrategia | Strategy | **ATHENAEUM** | How competitive play works and what is used: fundamentals, glossary, common sets, partners, trends | Strategy and knowledge | M4 | 3 | `/strategy` |
| Torneos | Tournaments | **CIRCUS** | Watch the big official VGC tournaments, with both teams beside each game, and the season's best players | Spectacle | M10 | 3 | `/tournaments` |
| Coliseo | Colosseum | **COLOSSEUM** | Turn-by-turn doubles battle testing, with an animated stage | Strategy and spectacle | M5 | 4 | `/colosseum` |
| Foro | Forum | **FORUM** | The public square: open a topic and discuss it, with teams, calculations and battles attached | Community | M9 | 6 | `/forum` |
| Quiz | Quiz | **AENIGMA** | Riddles and challenges | Knowledge | M7 | 7 | `/quiz` |

Strategy and information get more halls than spectacle, on purpose: battles are one part of the academy, not its center. The FORUM is the one community hall (D85): the Roman forum was where citizens met and argued, so the name says what the hall does in both languages. *Forum* is the Latin word; *foro* is its Spanish descendant. The CIRCUS is the spectacle of other people's battles (D102): the Circus Maximus held Rome's chariot races, a different building and show from the Colosseum's gladiators, so the COLOSSEUM is where you fight and the CIRCUS is where you watch the champions. *Circus* appears only as the inscription, with the racetrack in its imagery; the menu says Torneos / Tournaments (D59).

**Halls that don't exist yet** appear at the entrance as **closed doors** with their phase ("Fase 3"), and are not navigable (resolves the open point in SHL rules).

### Navigation pattern (Proposal DP-1)

- **Desktop:** a top bar with the wordmark, the menu, the language switch, the theme switch (Solrock or Lunatone, D113) and, at the far right, a gear icon for **Settings** (D112), followed by the ornament band. From Phase 5 the gear becomes the account menu.
- **Phone:** the menu collapses into a "Salas" button that opens a full-screen list of halls, each with its inscription and one-line description.
- **Utility pages stay plain (D112):** Settings, About and the not-found page use the academy's fonts, colors and ornament band, but no Latin inscription, no presenter and no lore. Settings is a simple page of sections (Preferences, Your data, and later Account), with plain labels.
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
| **Roman numerals** | Book numbers (LIBER I), thumb index, page numbers, the FORUM's rule tablets (TABULA I) | Arabic numerals for all data (stats, IDs, damage) |
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

**Presenters are not meant to be Roman** (D105): no Pokémon is. Each fits through its lore, personality and role in the hall; a Roman link (Arcanine's *cave canem*, Braviary's *aquila*, Rillaboom's *praeco*) is a bonus, never a requirement.

| Hall | Presenter | Why |
| --- | --- | --- |
| ATRIUM | **Arcanine** (Kanto form) | The guardian dog at the door, as in the *cave canem* mosaics of Pompeian entrances; noble, loyal and honorable, once thought a legendary Pokémon |
| BIBLIOTHECA | **Mew** | Said to carry the DNA of every Pokémon: the natural keeper of a book about all of them |
| LEGIO | **Falinks** | Designed after a military formation, and literally a group of six |
| ABACUS | **Metagross** | Its Pokédex entries describe four brains that solve complex calculations faster than a supercomputer and analyze opponents precisely |
| ATHENAEUM | **Noctowl** | The owl of Athena, symbol of wisdom (our association, not Game Freak's); turns its head to think, and in lore sees several futures and chooses one after weighing them. The real Athenaeum, founded by Hadrian in Rome, was a school, so the owl presides over a hall that teaches (D106) |
| CIRCUS | **Rillaboom** | The herald of the games, like the Roman *praeco*: a drummer whose troop is led by whoever wins a drumming battle, and a face competitive players know (the most used Pokémon on the Champions VGC ladder in Regulation M-C) |
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
| **Noctowl** (ATHENAEUM) | The night strategist. Measured and patient; pauses before answering, sets out options ("Two paths…") and explains why one wins. Unlike Metagross, at ease with uncertainty: the metagame is likelihoods, not certainties. Remembers how past regulations went and likes to point out patterns. Also the patient teacher (D106): no question is too basic, it answers a beginner as seriously as an expert, and points to the right fundamentals page | **The metagame report:** writes the weekly "metagame of the week" thread in the FORUM (FOR-F13; a template in Phase 6, Noctowl's voice from Phase 7) and a briefing when a new regulation arrives (AIA-F06) | — |
| **Incineroar** (COLOSSEUM) | The showman in your corner. Loud and theatrical while a battle plays: narrates big plays, hypes a good read, loves a comeback. Between turns it drops the act and gives straight advice like a coach. Owns mistakes ("That one's on us") and never sugarcoats a losing position | **Coaching the battle:** the turn advisor (AIA-F03, D76) and a review after each battle that points out the two or three turns that decided it (AIA-F07) | — |
| **Rillaboom** (CIRCUS) | The herald of the games. Warm, rhythmic and generous with praise; opens every event with a drum roll, builds the tension before a final and celebrates the winner, whoever it is. Never takes sides: it respects whoever performs best, as its troop follows its best drummer. Gentle off the stage, values harmony, and loves telling you which match not to miss | **Announcing the big events** (CIR-F07, D105), from Phase 3 and by code, without the assistant: its door at the ATRIUM shows the next or current event and when it airs, and while one is live a small notice appears in every hall | — |
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
  - **The Twelve Tables.** Rome's first written law, put up in the Forum so every citizen could read it: the origin of the LEX FORI (D96), and Braviary's way of introducing the rules.
  - **The *provocatio*.** A Roman citizen could appeal a magistrate's punishment to the people: the guardian swoops, but never has the last word.

**Rillaboom in detail (D105).** No Pokémon is a herald, so, as with every hall, the cast follows a fitting role.

- **The announcer, not a competitor.** A drum marks the start, builds the tension and celebrates the win, which is a herald's job. Charizard and the other stars of competitive play would be competitors standing in the stands; Incineroar already holds that spirit in the COLOSSEUM.
- **Spectacle and competition in one.** Its troop chooses its leader through a drumming battle, a contest won by performance, which is the analogy the CIRCUS rests on: watching competitive play as a show. Gigantamax gives it a forest of drums for the big moments.
- **A face players know.** It led usage on the Champions VGC ladder in Regulation M-C and has been a VGC staple for years, often beside Incineroar: the fighter in the COLOSSEUM and the announcer in the CIRCUS reflect real competitive history.
- **The Roman role.** The *praeco* announced the games, the races and the winners to the crowd; texts can use the word in introductions, never in buttons (D59).

**Civic framing of the FORUM (D96, D97).** The hall carries Roman civic life through parts it already has, never through new mechanics:

- **LEX FORI:** the rules page shows twelve bronze tablets, *TABULA I* to *TABULA XII*: a Cinzel heading with the Roman numeral, the rule in plain language beneath in Alegreya Sans. Tablets I–VI say what is expected, VII–IX the penalty ladder, X–XII the user's rights. Moderation messages cite a tablet ("TABULA IV") next to its plain title.
- **ACTA:** the public log, styled as a posted notice: date, tablet, action, reason.
- ***Provocatio*:** the appeal button keeps a plain label ("Apelar" / "Appeal"); the Latin word appears in its explanation.
- ***Suffragium*:** only in introductions and help texts; vote buttons stay plain icons and words (D59).
- **One kind of user (D97):** no badges, titles, ranks or level marks on posts or profiles. Every author is shown the same way.

**Considered and set aside:** Pikachu (fame, not meaning), Klefki (keys only), Girafarig/Farigiraf (a Janus link few would read) and Hisuian Arcanine (rock and statue, less alive) for ATRIUM; Alakazam (psychic and magic, not calculation) for ABACUS; Xatu (a passive seer, drawn from specific living cultures) for ATHENAEUM; Zoroark (illusion, not riddles) and Unown (no individual mind) for AENIGMA. For the FORUM: Chatot (mimics sounds, and tropical), Mr. Mime (the minstrel bringing news is not a Roman image), Smeargle (artistic painting more than messages), Grafaiai (a signature tag repeated for life, solitary and poisonous), Primarina (Greek sirens lure sailors to their death), Unfezant (one-to-one messages, kept as lore), Conkeldurr (its Roman concrete builds the square but says nothing about talking in it), Farigiraf (the Janus link again), Lycanroc (no lore of the Roman she-wolf), Exploud (a herald announces but doesn't discuss), Pidgeot, Talonflame, Hawlucha, Staraptor and Swellow (not eagles), Corviknight (a raven, steel rather than bronze, British in theme), Hisuian Braviary (loses the eagle's look), Yveltal (death), Tornadus in Therian Forme (not clearly an eagle; its other form is the wind god Fūjin; storms destroy), Zapdos (Jupiter's eagle holds thunderbolts, but it doesn't look like an eagle) and Moltres (Pliny's phoenix is an anecdote, not the hall's function, and a fourth fire-type presenter). For the CIRCUS: Rapidash (the one horse with competitive lore, "very competitive… in the hopes of racing", but racing is not the analogy and it is unknown in competitive play), Mudsdale (labour, not speed), Zebstrika and Cyclizar (speed without competition), Glastrier, Spectrier and Keldeo (a king's steeds and justice), Meowscarada (a stage magician and a trickster: the modern circus), Hawlucha (a showman, but wrestling is Incineroar's), Quaquaval, Primarina and Meloetta (dancers and singers), Mr. Mime, Mr. Rime, Chatot and Blacephalon (mimicry or clowns), Victini (victory itself, but absent from current games and no spectacle), Greninja (a bond with its trainer, but a ninja hides), Charizard (a fierce competitor, not an announcer), and Kingambit, Garchomp, Urshifu and Salamence (meta Pokémon with nothing to present).

## 8. The Pokédex as a book: *Historia Naturalis* (D61)

### Structure

- The **BIBLIOTHECA** keeps one work, the ***Historia Naturalis***, divided into **nine books (*libri*)**, one per region: LIBER I · KANTO … LIBER IX · PALDEA.
- **Appendix books** hold moves, abilities, types and an A–Z index (D26 detail pages).
- **The other books** (D110): the **ARMAMENTARIUM** (items), the **HERBARIUM** (berries) and the **PANTHEON** (Legendary, Mythical, Ultra Beast and Paradox Pokémon), below.
- **One bookcase, three shelves** (D110): the *Historia Naturalis* on the top shelf, the appendices below it, the other books on the third. Every section is a book, opened the same way: codex, chapters, thumb index, page turns, and the List view always available. There are no rooms or doors in the library.
- **Bookmarks** are the labels, in every book: ribbons on the page edge with a short word ("Restringido", "Resistencia"…), never color alone. Which bookmarks each book carries is settled when it is built.
- **Scrolls** appear only as ornament (shelf details, chapter title pages), never as the reading format.

### Views

| View | What it shows | Feature |
| --- | --- | --- |
| **Shelf** | The bookcase (D110): the *Historia Naturalis*'s nine books, the appendices, and the ARMAMENTARIUM, HERBARIUM and PANTHEON; choosing a book offers "Abrir el libro" or "Ver lista" | ARC-F01 entry point |
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

### The ARMAMENTARIUM (D99, D100, D110)

- **A book on the third shelf,** titled ARMAMENTARIUM (the Roman armoury) with "Objetos" / "Items" beside it. Roman libraries kept their books in cabinets (*armaria*), which the title recalls; the book itself opens like any other. Reached from the shelf, the global search and any link to an item. Mew presents it as part of the BIBLIOTHECA.
- **Chapters by category** (Poké Balls, medicine, held items, Mega Stones, evolution items and so on), in the thumb index. Berries are not here: they have the HERBARIUM.
- **The list** opens on items available in the current game, with "Ver todos" for every item (ARC-F09).
- **Item pages are book pages.** Battle items get a two-page spread: icon, names, category and description on the left; the current-game mark and their links (Mega form, the Pokémon it works for) on the right. Other items get a single page.
- Designed in M1.7 (section 14).

### The HERBARIUM (D111)

- **The book of plants,** titled HERBARIUM with "Bayas" / "Berries" beside it, after the herbals of the Roman era (Pliny's books on plants, Dioscorides's herbal). On the third shelf, beside the ARMAMENTARIUM.
- **Chapters by battle use** (a draft, settled when built): resistance (the berries that halve a super-effective hit), healing (HP), cures (status), pinch (a stat raised at low HP), retaliation (hurting or reacting to the attacker), and training and others.
- **Each berry is a two-page spread:** names, flavours, firmness and size on the left; battle effect, Natural Gift type and power, Fling and availability in the current game on the right. Availability is a fact on the page, not a bookmark.
- **Bookmarks:** the berry's functions (several where they apply) and, from Phase 3, "commonly used".
- **Opens on all berries.** Botanical illustration fits the book: line drawings in the ornament color, original, never copied from the games.
- Designed in M1.13 (section 14).

### The PANTHEON (D108, D109, D110)

- **A book on the third shelf,** titled PANTHEON, with "Legendarios y singulares" / "Legendaries and Mythicals" beside it. Reached from the shelf, the global search, the category bookmark on every entry and the glossary. Mew presents it, a Mythical among its own kind.
- **The temple to all the gods.** Rome took in gods from other peoples, so Pokémon of any mythology belong here; the dome can appear as the book's frontispiece, as ornament only.
- **Four chapters:** Legendary (with two parts, Sub-legendary and Restricted), Mythical, Ultra Beast and Paradox. The last two carry the line "No son legendarios, aunque a menudo se confunden con ellos" / "Not legendaries, though often taken for them".
- **Each chapter** opens with its short text and whether it is allowed in the current regulation (an allowed/not-allowed mark with words, never color alone); its pages list the members as small portraits that open their *Historia Naturalis* entries.
- **The category bookmark** (`ps-bookmark`) on every entry's codex page: "Legendario · Restringido", "Singular", "Ultraente", "Paradoja", linking to its chapter.
- Designed in M1.12 (section 14).

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
| **Book** | Every BIBLIOTHECA book: Pokédex entries, appendix pages, the ARMAMENTARIUM, HERBARIUM and PANTHEON (D110) | Two-page spread, thumb index, bookmarks, previous/next |
| **List** | Pokédex list, moves, abilities, items | Filters, sortable grid or table |
| **Tool** | LEGIO, ABACUS, ATHENAEUM, CIRCUS | Hall header, main work area (8 columns), analysis panels (4 columns); stacked on phones. In the CIRCUS the player is the main area, with the event panel and the two teams at the side and the row of replays and the top players below |
| **Stage** | COLOSSEUM | Full-width PixiJS stage with playback controls, the turn matrix and the turn history with its branches (Phase 4); laid out when Phase 4 is specified |

## 10. Components (`ui/`, D49)

Built on Angular CDK, styled with tokens, prefixed `ps-`. Pages use only these.

| Component | Purpose |
| --- | --- |
| `ps-button`, `ps-toggle-group` | Actions; segmented choices (Libros/Lista, format, stat system) |
| `ps-search` | Search field with results list (global and per hall) |
| `ps-type-badge` | Type name with its color (never color alone) |
| `ps-bookmark` | A label as a ribbon on the page edge with a short word ("Legendario · Restringido", "Resistencia"), linking to its chapter; used by every BIBLIOTHECA book (D110) |
| `ps-tier-badge` | Type tier letter (S to F) with an accessible label ("Rango de tipos: B"); its color supports the letter, never replaces it |
| `ps-stat-bar` | Labelled stat with value and bar |
| `ps-inscription` | Cinzel heading for halls, plinths and running heads |
| `ps-presenter` | Arch, artwork, plinth and dismissible introduction |
| `ps-term` | A competitive term with its glossary definition on hover, focus or tap, a dotted underline in the text color, never color alone (X-16, D107) |
| `ps-pokemon-image` | Every Pokémon image: official image or the original fallback (a silhouette or type emblem drawn in the academy's line style), chosen by the image service (X-15) |
| `ps-theme-switch` | The Día/Noche switch in the header: Solrock or Lunatone as a pixel sprite for the current theme (whole-step scaling, pixelated rendering), a plain sun or moon when official images are off; spoken label and tooltip with the action and the Pokémon's name (SHL-F05, D113) |
| `ps-music-control` | Play or pause, volume and track name in the header; off by default (SHL-F09) |
| `ps-hall-door` | Entrance door (open or closed) |
| `ps-book`, `ps-book-page`, `ps-thumb-index` | The codex and its navigation |
| `ps-card` | Surfaces such as team slots and panels |
| `ps-team-strip` | The active team (X-12): six small sprites with the team name, a switch and an import action; compact on phones. Placed by the shell in the halls that use teams; exact placement decided when built (M2.9) |
| `ps-team-sheet` | The read-only team sheet (STR-F24): one card per member with image, types, item, ability, nature, spread, stats and moves, under the team name, author and notes; columns on wide screens, a print style without navigation. Built in M2.10 |
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
| Theme switch | Colors crossfade; Solrock and Lunatone swap with a short spin (a fade only with reduced motion) | 200 ms |

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

- **Module names:** M2 is the Pokédex (BIBLIOTHECA), M3 Teams (LEGIO), M4 Calculator and strategy (ABACUS, ATHENAEUM), M5 the **battle stage** (COLOSSEUM), formerly "Animation Lab". Feature IDs (`ARC-`, `STR-`, `CMP-`, `LAB-`) do not change.
- **Routes and folders** in the architecture use the English menu words: `/teams`, `/calculator`, `/strategy`, `/tournaments`, `/colosseum`, `/forum`, `/quiz`.
- **D5** (even Greek–museum blend) is superseded by **D58**.

## 14. Open items

| Item | Decide by | Notes |
| --- | --- | --- |
| Final palette (D63) | After the first real pages (Phase 0–1) | Travertino is provisional (D88) |
| Presenter swaps (D84) | Before each hall is built | Cast decided; any presenter may still change |
| Texture sources (Q29) | When textures are needed | Free-licensed only |
| Theme switch (D113) | M0.6–M0.7 | The sprite's size and scale beside the header's fonts; whether the pixel style sits well with the academy; the place on phones |
| Bookcase and bookmarks (D110) | M1.5 | The three shelves, how a book is taken and opened, the bookmark ribbon; reused by every book |
| ARMAMENTARIUM design (D99) | M1.7 | Its chapters and the item page as a book page (spread or single page) |
| PANTHEON design (D108) | M1.12 | Its four chapters, the allowed mark, the frontispiece, the category bookmark on the entry |
| HERBARIUM design (D111) | M1.13 | Its chapters, the berry spread, the bookmarks, the botanical line drawings |
| COLOSSEUM design | Phase 4 specification | Includes Three.js exploration (Q63) |
| CIRCUS design | M3.9 | The player area, the team lists beside it, the replay row, Rillaboom's frame and the herald's notice; the racetrack imagery |
| ATHENAEUM design | M3.4–M3.5 | The two sides, what is used and how it works; the fundamentals page with its written part and live part; roles on usage pages; the glossary page. The term tooltip (`ps-term`) is designed earlier, in M1.10 (D106, D107) |
| FORUM design | Phase 6 specification | Thread list, thread page, attachment cards, votes, report and moderation screens; Braviary's frame and the report conversation (D89, D90); the LEX FORI tablets, the ACTA and the appeal (D96); no visible ranks (D97) |
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

### Approved (2026-11-20)

| ID | Decision |
| --- | --- |
| D96 | Roman civic life frames the FORUM: the rules as the LEX FORI in twelve tablets, appeals as *provocatio*, the public ACTA log, *suffragium* in texts only; real-world politics is off-topic (section 7). |
| D97 | Every user looks the same: trust levels are internal, with no badges, titles or ranks on posts or profiles (section 7). Revises D87 in visibility only. |

### Approved (2026-11-21)

| ID | Decision |
| --- | --- |
| D99 | The ARMAMENTARIUM: the BIBLIOTHECA's room for items, with cabinets by category; no menu entry and no presenter of its own (Mew presents it) (section 8). Revised by D110: a book, not a room. |
| D100 | Every item is shown: battle items with the full page, the rest with encyclopedic data; the list opens on items available in the current game (section 8). Revises D31. |

### Approved (2026-11-24 to 2026-11-26)

| ID | Decision |
| --- | --- |
| D102 | The CIRCUS (menu Torneos / Tournaments, route `/tournaments`), a Spectacle hall for watching official VGC competition, one page with no rooms (section 3). |
| D105 | CIRCUS presenter: Rillaboom, the herald (*praeco*), with announcing the big events as its responsibility from Phase 3. Presenters are not meant to be Roman (section 7). |
| D106 | The ATHENAEUM teaches as well as showing the metagame: menu Estrategia / Strategy, route `/strategy`, two sides (what is used, how it works); Noctowl as the patient teacher (sections 3, 7). Revises the label in D60. |
| D107 | Teaching content: fundamentals pages written once with a live part from data, roles on usage pages, a glossary with the `ps-term` tooltip from Phase 1 (sections 9, 10, 14). |
| D108 | The PANTHEON: the BIBLIOTHECA's room for Legendary, Mythical, Ultra Beast and Paradox Pokémon, a rotunda of niches; no menu entry and no presenter of its own (Mew presents it) (section 8). Revised by D110: a book, not a room. |
| D109 | Category labels: Legendary (Sub-legendary or Restricted), Mythical, Ultra Beast, Paradox, shown as bookmarks (sections 8, 10). |
| D110 | The BIBLIOTHECA is one bookcase of three shelves and every section is a book, opened the same way; labels are bookmarks (`ps-bookmark`). Revises the cabinets of D99, the item card and the PANTHEON's rotunda (section 8). |
| D111 | The HERBARIUM, the book of berries: chapters by battle use (draft), berry spreads, bookmarks for functions; opens on all berries (section 8). |
| D112 | Settings: a plain page at `/settings` from a gear icon at the right of the header; utility pages (Settings, About, not-found) stay plain, without inscription or presenter (section 3). |
| D113 | The theme switch shows Solrock (Día) or Lunatone (Noche) as pixel sprites for the current theme, with a plain sun and moon fallback (sections 3, 10, 11). Solgaleo and Lunala preferred if a way is found (P5). |

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
