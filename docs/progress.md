# Pokescientia — Progress Log

Session log (D65). Newest entry first. Each session, in a chat or in Claude Code, adds one short entry: what was done, what is next, and anything worth remembering. Milestone status lives in the checkboxes of [`06-roadmap-and-milestones.md`](06-roadmap-and-milestones.md); decisions live in [`01-vision-and-requirements.md`](01-vision-and-requirements.md) and [`00-decision-map.md`](00-decision-map.md).

**How to start a new session:** read [`CLAUDE.md`](../CLAUDE.md), this file (latest entry first), the decision map and the documents the topic touches. The documents, not past chats, are the project's memory.

---

## 2026-11-26 · Default language (D114)

- **Done:**
  - Checked the defaults: the theme already follows the browser until the user chooses (D62); the language fell back to Spanish (D51).
  - Decided D114: with no saved choice, the site opens in the browser's first preferred language that is Spanish or English, otherwise in English. Spanish stays the primary language (R9, D1). Acceptance criteria added for a first visit (SHL-F04, X-04).
  - Docs updated: vision v1.37, modules v1.26, architecture v1.18, CLAUDE.md.
- **Next:** M0.1 when the owner is ready.
- **Notes:** the two U19 entries are still to renumber.

---

## 2026-11-26 · The theme switch (D113)

- **Done:**
  - Decided D113: the theme switch in the header shows the current theme as a pixel sprite, Solrock in Día and Lunatone in Noche, with a label saying what the click does and a plain sun and moon when official images are off. Built in M0.6 (plain) and M0.7 (sprites).
  - Parked P5: official artwork as decoration (such as TCG Pocket's Solgaleo and Lunala painting in the library), and Solgaleo and Lunala for the switch, which the owner prefers; any readable way to use them is preferred over Solrock and Lunatone.
  - Docs updated: vision v1.36, modules v1.25, design v1.22, roadmap v1.24, decision map, CLAUDE.md.
- **Next:** M0.1 when the owner is ready.
- **Notes:** the two U19 entries are still to renumber.

---

## 2026-11-26 · Settings (D112)

- **Done:**
  - Explored a themed LARARIUM for the user's own space and set it aside: a settings page has no idea behind it for the theme to carry, and a Latin name would make it harder to recognise.
  - Decided D112: a plain Settings page at `/settings`, from a gear at the right of the header, private. It grows with the phases: preferences and clearing local data (Phase 1, M1.11), the full backup of teams and preferences (Phase 2, M2.3), the Account section (Phase 5), the persona switch if Q82 adopts it (Phase 7). Utility pages (Settings, About, not-found) stay plain. A username route was rejected: it doesn't exist before accounts and reads as a public profile.
  - Features SHL-F10, SHL-F11, ACC-F06, U27; STR-F07 shares the backup file.
  - Docs updated: vision v1.35, modules v1.24, architecture v1.17, design v1.21, roadmap v1.23, decision map, CLAUDE.md.
- **Next:** M0.1 when the owner is ready.
- **Notes:**
  - Personal bookmarks in Settings were suggested and not chosen.
  - The two U19 entries are still to renumber.

---

## 2026-11-25 · One bookcase, and the HERBARIUM (D110, D111)

- **Done:**
  - Decided D110: the BIBLIOTHECA is one bookcase with three shelves: the *Historia Naturalis*, the appendices, and the other books (ARMAMENTARIUM, HERBARIUM, PANTHEON). Every section is a book opened the same way; there are no rooms, doors, cabinets or rotunda; labels are bookmarks. Revises D99 and D108 and the item card. Details at the Phase 1 design reviews.
  - Decided D111: the HERBARIUM, the book of berries (route `/berries`). Chapters by battle use as a draft, berry spreads, bookmarks for functions and, from Phase 3, "commonly used"; availability is shown but is not a bookmark; opens on all berries.
  - Features ARC-F17, DAT-F20, U26; new milestone M1.13, Phase 1 closes with M1.14.
  - Docs updated: vision v1.34, modules v1.23, data strategy v1.10, architecture v1.16, design v1.20, roadmap v1.22, CLAUDE.md.
- **Next:** explore the LARARIUM; M0.1 when the owner is ready.
- **Notes:**
  - The owner may want bookmarks in every book, the *Historia Naturalis* included; decided when each book is built.
  - The two U19 entries are still to renumber.

---

## 2026-11-25 · The PANTHEON (D108, D109)

- **Done:**
  - Reviewed the remaining Roman ideas. Set aside: TABULARIUM, ANNALES, FASTI, THERMAE, TRIUMPHUS, TABULAE, ACTA DIURNA, NUMISMATA and ITINERARIA (the last two are not covered by the Pokédex: locations and every game's sprites remain out of scope). Still to explore: the LARARIUM (a private page for settings and data) and the HORTUS (berries).
  - Decided D108: the PANTHEON, a room of the BIBLIOTHECA for Legendary, Mythical, Ultra Beast and Paradox Pokémon (route `/legendaries`, Mew presents it). The Roman Pantheon took in other peoples' gods, so no Roman legendary is needed.
  - Decided D109: one label per Pokémon from Showdown's tags: Legendary (Sub-legendary or Restricted), Mythical (separate from Legendary), Ultra Beast, Paradox; each group's legality from the regulation data. Myths are not included for now.
  - Features ARC-F15, ARC-F16, DAT-F19, U25; new milestone M1.12, Phase 1 closes with M1.13.
  - Docs updated: vision v1.33, modules v1.22, data strategy v1.9, architecture v1.15, design v1.19, roadmap v1.21, CLAUDE.md.
- **Next:** explore the LARARIUM and the HORTUS; M0.1 when the owner is ready.
- **Notes:**
  - To check in M1.12: the official Spanish term for Restricted, and whether the Champions data carries every category tag.
  - The two U19 entries are still to renumber.

---

## 2026-11-24 · The ATHENAEUM teaches (D106, D107)

- **Done:**
  - Reviewed the Roman concepts still unused. LUDUS (a hall for learning) was set aside: guides written by hand go stale every regulation and would be written twice.
  - Decided R23 and D106: the ATHENAEUM teaches as well as showing the metagame, with two sides, what is used and how it works. Menu Estrategia / Strategy, route `/strategy`, wing Strategy and knowledge. Noctowl is also its patient teacher (personality, not a responsibility). Hadrian's Athenaeum, a school, is its lore.
  - Decided D107: fundamentals pages written once (mechanics only) with a live part from usage data, starting with ten concepts (CMP-F16, DAT-F18); roles on usage pages (CMP-F17); a glossary (DAT-F17) with tooltips from Phase 1 (X-16, `ps-term`) and a glossary page in Phase 3 (CMP-F18). User stories U23, U24.
  - New milestones M1.10 (glossary and tooltips) and M3.5 (fundamentals). Later milestones renumbered: Music M1.11, Phase 1 closes with M1.12; the threat list is M3.6, the CIRCUS M3.8 and M3.9, Phase 3 closes with M3.11. References in D69 and D102 updated.
  - Docs updated: vision v1.32, modules v1.21, data strategy v1.8, architecture v1.14, design v1.18, roadmap v1.20, CLAUDE.md.
- **Next:** unchanged; M0.1 when the owner is ready.
- **Notes:**
  - Earlier progress entries keep the milestone numbers of their day.
  - The two U19 entries are still to renumber.

---

## 2026-11-24 · The CIRCUS settled, with Rillaboom (D102–D105)

- **Done:**
  - Checked that commit `34cfb03` matches the files sent.
  - Chose the presenter. Reviewed horses (Rapidash, Mudsdale, Zebstrika, Cyclizar, Glastrier, Spectrier, Keldeo), showmen (Meowscarada, Hawlucha, Quaquaval, singers and mimics), Victini, Charizard, Greninja and meta Pokémon. The owner chose **Rillaboom**: a face competitive players know, and a drummer whose troop is led by whoever wins a drumming battle, which joins competition and spectacle without leaning to racing or to the modern circus. As a drummer it is the herald (*praeco*), an announcer rather than a competitor.
  - Settled the hall: D102 (the CIRCUS, one page, VGC and Masters only, Internationals and Worlds, Phase 3 after the ATHENAEUM, route `/tournaments`), D103 (the page: YouTube player, event panel, past replays, both teams beside each replay opening in LEGIO, the season's top players), D104 (coverage only where every replay's teams are public, so from the 2023 season at most; hand-curated data with sources; embeds only, privacy-enhanced and on click; players' data limited), D105 (Rillaboom, announcing the big events from Phase 3 by code, at the ATRIUM and in every hall while live; presenters need not be Roman). R22, U20–U22, M10 (CIR-F01 to CIR-F07), DAT-F16, M3.7 and M3.8 added. Closes Q94; Q95 reworded.
  - Docs updated: vision v1.31, modules v1.20, data strategy v1.7, architecture v1.13, design v1.17, roadmap v1.19, decision map, CLAUDE.md, README.
- **Next:** open; exploring ideas. M0.1 whenever the owner chooses.
- **Notes:**
  - The roadmap's version note was missing version 1.18 (the ARMAMENTARIUM); added.
  - YouTube's embedded player refuses to play if the page sends no address (HTTP Referer): the Content Security Policy and referrer policy must allow for it at deployment.

---

## 2026-11-23 · A simpler CIRCUS (Q94)

- **Done:**
  - Checked that commit `5918037` matches the files sent.
  - The owner found the four-room CIRCUS out of line with the other halls: only the BIBLIOTHECA has rooms, because of its size. Reshaped Q94 as one page for watching: the player with the current or latest tournament, a side panel with the event's facts and source links, a row of past replays, and the season's top players as a short list.
  - Dropped from the hall: standings, brackets, player profile pages and the room names (PULVINAR, SPINA, AURIGAE, FASTI).
  - The owner wants both players' teams beside each replay, opening in LEGIO. Checked how: official VGC uses open team sheets (everything but stats) and RK9 publishes them during the event; teams are fixed for the whole tournament, so they are copied by hand when a replay is added. Replays only; live streams show teams on the broadcast.
  - Looked for live game data (picks, HP): none exists, since official matches run on consoles. Computer-vision tools that read battles from video exist, but need the video downloaded; set aside.
  - Docs updated: decision map.
- **Next:** open; exploring ideas. Presenter for the CIRCUS still to choose.
- **Notes:**
  - The hand-curated data: event facts, video IDs, each replay's two team lists, and a top-players list per season.
  - Open team sheets have no stats, so teams opened in LEGIO get default spreads, labelled.

---

## 2026-11-23 · CIRCUS for official VGC competition (Q94)

- **Done:**
  - Checked the CIRCUS name against history: the Circus Maximus (chariot races) and the Colosseum (gladiators and beast hunts) were different buildings and shows, so the name stands apart from the COLOSSEUM. The owner leans to CIRCUS.
  - Reshaped Q94 around the circus: PULVINAR (the built-in player with team lists beside each game), SPINA (the current season and its events), AURIGAE (player pages as career inscriptions, after Diocles), FASTI (past seasons). Past seasons are now in scope, with teams from earlier games labelled as approximations in the tools.
  - Docs updated: decision map.
- **Next:** open; exploring ideas. Presenter for the CIRCUS still to choose.
- **Notes:**
  - The menu keeps a plain label (D59), so *circo* never appears alone.

---

## 2026-11-22 · A hall for official VGC competition (Q94, Q95)

- **Done:**
  - The owner proposed covering competition itself: the official circuit's big events, the best players and their games. Checked that the ATHENAEUM never covers this: it uses only Showdown ladder statistics (D41), which exclude official tournaments.
  - Weighed it as a hall and found it passes the items test (halls split by what you do): following the competition is its own activity, separate from studying usage.
  - Recorded the idea as Q94, not decided: VGC only, Masters only, Internationals and Worlds first; calendar, event pages with open team lists that open in LEGIO, ABACUS and the COLOSSEUM, player pages, embedded official streams; no hosting. Names noted: LUDI, CIRCUS, FASTI.
  - Opened Q95 (research): other tournaments later, and sources for the top players of the moment (Championship Points standings, Travel Award standings, Limitless VGC rankings, Liquipedia).
  - Docs updated: decision map.
- **Next:** open; exploring ideas. M0.1 whenever the owner chooses.
- **Notes:**
  - The 2027 LAIC (São Paulo, 20–22 November 2026, Regulation M-C) was the season's first International; sources still disagreed on the Masters final that night, an example of why results need checking.
  - Official events run several games (VGC, TCG, Pokémon GO, UNITE); only VGC is in scope.

---

## 2026-11-21 · Items and the ARMAMENTARIUM (D99–D101)

- **Done:**
  - Reviewed how items are covered. They live in the BIBLIOTHECA's appendix (ARC-F09, description and category only) and inside common sets in the ATHENAEUM. Found a gap: no item legality, though Champions has a much smaller item pool than earlier games.
  - Weighed an items hall and set it aside: halls are split by what you do, and item lookups belong to the library.
  - Decided D99: the ARMAMENTARIUM, a room of the BIBLIOTHECA with cabinets by category; no menu entry, Mew presents it.
  - Decided D100 (revises D31): every item in PokéAPI's data (2,223), battle items with the full page, the rest with encyclopedic data; the list opens on items available in the current game.
  - Decided D101: item availability from Showdown's Champions data (166 of 587 items available on 2026-11-21); marks and warnings in the team editor.
  - Opened Q92 (item usage on item pages, in the ATHENAEUM and in LEGIO; Phase 3) and Q93 (when each item entered Champions, and checking Showdown's list against the official one; M2.5).
  - Docs updated: vision v1.30, modules v1.19, data strategy v1.6, architecture v1.12, design v1.16, roadmap v1.18, decision map, CLAUDE.md.
- **Next:** open; exploring ideas. M0.1 whenever the owner chooses.
- **Notes:**
  - Showdown's data includes Poké Balls (marked `Past`), so "battle item" means "in Showdown's data", not "holdable".
  - The build grows to about 9,800 prerendered pages; the Phase 0 spike measures prerender time.

---

## 2026-11-21 · Pace of the project

- **Done:**
  - Reviewed the planning stage: about 3.5 weeks, 46 commits, all documentation, no code yet.
  - The owner explained the pace: there is no deadline, the project is a hobby for relaxing and exploring ideas, and right now the aim is a general understanding of the technologies and of Claude before coding.
  - CLAUDE.md now records this under "Current phase": sessions may be pure exploration, and Claude doesn't push to start M0.1. Not given a D-number, since it describes how the owner works rather than the product.
- **Next:** open; exploring ideas and the tools. M0.1 whenever the owner chooses.
- **Notes:**
  - Ideas for distant phases can stay as short notes until their phase comes close, so the specs don't grow faster than they can be kept consistent.
  - A small throwaway experiment (for example, a scratch Angular app or a tiny page built with Claude Code) counts as exploration and doesn't start M0.1.

---

## 2026-11-20 · Low-cost security (D98)

- **Done:**
  - Reviewed where security matters, keeping it the project's last priority. Through Phase 4 nothing leaves the browser (teams in IndexedDB, preferences in localStorage), so the risk is very low; it starts with accounts (Phase 5), then the FORUM (Phase 6) and the AI assistant (Phase 7).
  - Decided D98: low-cost measures only, like D78. Now: imported text never rendered as HTML and validated (architecture guideline 10); `npm audit` and Dependabot in M0.2; a Content Security Policy at the first deployment. Costlier measures are not planned.
  - Opened Q91: the account security checklist for the Phase 5 specification (no stored passwords if possible, cookie sessions, ownership checks, parameterised SQL, secrets, rate limits, real deletion), plus server-side sanitising of posts (Phase 6) and the user's AI key and prompt injection (Phase 7). Q88 now weighs prompt injection.
  - Docs updated: vision v1.29, architecture v1.11, roadmap v1.17, decision map, CLAUDE.md.
- **Next:** unchanged; M0.1 when the owner is ready.

---

## 2026-11-20 · Roman politics in the FORUM (D96, D97)

- **Done:**
  - Listed the Roman concepts the academy doesn't use yet. The owner raised politics and law, among Rome's most lasting contributions, which has no room as a hall.
  - Decided D96: the FORUM, the centre of Roman civic life, carries it through parts it already has. The rules are the LEX FORI, twelve tablets after the Twelve Tables (FOR-F15). Appeals are the *provocatio*. The moderation log is the public ACTA (FOR-F16). Votes are called *suffragium* in texts only. Real-world politics is off-topic. The economy, offices as ranks and a Senate were not adopted.
  - Decided D97: every user looks the same. Trust levels stay as D87 sets them, against repeat accounts, but are internal and never shown (revises D87 in visibility only).
  - Parked P4: visible user ranks, possibly Roman military ranks, not designed yet.
  - Docs updated: vision v1.28, modules v1.18, design v1.15, roadmap v1.16, decision map, CLAUDE.md.
- **Next:** unchanged; M0.1 when the owner is ready.
- **Notes:**
  - The tablets' wording is written in the Phase 6 specification; whether the ACTA names users is part of Q86.
  - The vision's user stories have two U19 entries (PokéPaste from D95, and FORUM votes and reports). Not fixed here; to renumber in a later session.

---

## 2026-11-19 · PokéPaste reopened (D95)

- **Done:**
  - Compared Showdown's team import and export with PokéPaste. PokéPaste uses the same Showdown export text; it adds title, author, notes, a readable page and a short link. Showdown's own teambuilder has an "Upload to PokePaste" button.
  - Checked PokéPaste's source code again: `/json` gives text, title, author and notes, readable from any website; `/create` is a public form. Code last changed in 2021.
  - Decided D95 (revises D70, closes P2 and Q71): import from a PokéPaste link (STR-F23), team sheet (STR-F24), author and notes (STR-F25), optional export to PokéPaste (STR-F26), user story U19. The importer now states its defaults for missing lines (STR-F05) and the export writes `Level: 50` (STR-F06).
  - New milestone M2.10 (PokéPaste and the team sheet); closing Phase 2 becomes M2.11.
  - Docs updated: vision v1.27, modules v1.17, data strategy v1.5, architecture v1.10, design v1.14, roadmap v1.15, decision map.
- **Next:** unchanged; M0.1 when the owner is ready.

---

## 2026-11-19 · Presenter personalities and responsibilities (D94)

- **Done:**
  - Wrote a full personality for each of the eight presenters, following Braviary's model (design §7).
  - Defined when a presenter has a responsibility: it acts or produces something, owns a process, and would be missed if removed. Ways of answering (Arcanine pointing the way, Mew telling origins, Metagross setting up a calculation) are personality, not responsibilities.
  - Decided D94: responsibilities for Falinks (inspection and fixes, AIA-F05), Noctowl (weekly metagame report and regulation briefings, AIA-F06), Incineroar (turn advisor and battle review, AIA-F07), Delphox (runs the quiz, AIA-F08, with a ladder of hints built by code, QUZ-F03), plus Braviary's moderation (D90). None for Arcanine, Mew and Metagross.
  - Opened Q89 (Delphox's daily riddle, possible) and Q90 (a hint mode in every hall, in each presenter's voice).
  - Docs updated: vision v1.26, modules v1.16, design v1.13, roadmap v1.14, decision map, CLAUDE.md.
- **Next:** unchanged; M0.1 when the owner is ready.

---

## 2026-11-18 · The /commit-message skill (D93)

- **Done:**
  - Checked how Claude Code will follow the commit rules: it loads CLAUDE.md automatically, but "read §12 first" can be skipped, and in a fresh session it only sees the diff.
  - Decided D93: a `/commit-message` Claude Code skill (`.claude/skills/commit-message/SKILL.md`) that reads architecture §12 and the staged changes and drafts the message. Added to M0.1; from then on every commit message comes from it. Skills are Claude Code's current format for custom slash commands (custom commands were merged into skills).
  - Docs updated: vision v1.25, architecture v1.9, roadmap v1.13, CLAUDE.md.
- **Next:** unchanged; M0.1 when the owner is ready.

---

## 2026-11-18 · Commit message rules in one place (D92)

- **Done:**
  - Compared a Copilot commit message with the prepared one for `f6d4a48`. Copilot's put D90 in the decision map (it lives in the vision; the map got Q88), missed Q88 and the DP-3/DP-4 wording, used "update" in the summary, and was organized by file, partly because our own rule said "one bullet per area or file group".
  - Confirmed that only Copilot read `.github/commit-instructions.md`; Claude follows CLAUDE.md. The owner uses Claude's messages, so the file was a third copy of the rules.
  - Decided D92: the full rules live only in architecture §12, rewritten: body organized by what changed with one bullet per ID, then versions; a table of where each ID lives; add/revise/close verbs; no guessed reasons. Deleted `.github/commit-instructions.md` and the Copilot setting in `.vscode/settings.json` (editor settings kept). CLAUDE.md tells Claude Code to read §12 before writing a message.
  - Docs updated: vision v1.24, architecture v1.8, decision map, CLAUDE.md.
- **Next:** unchanged; M0.1 when the owner is ready.

---

## 2026-11-17 · Braviary as the voice of moderation (D90, D91)

- **Done:**
  - Decided D90 (option A): in Phase 7, Braviary is the AI face of reporting and moderation. Users report by talking to it; it reads the post against the rules, explains, may hide the post while it is reviewed and proposes the penalty; a moderator confirms penalties and appeals go to a person (D87 unchanged). New feature AIA-F04.
  - Option B (Braviary acting alone on obvious spam and flagrant abuse) appealed to the owner; opened as Q88, to decide once its proposals prove reliable.
  - Decided D91: presenters are shown alive, in original color, each with a vivid personality of its own, so in Phase 7 talking to the assistant feels like talking to that presenter. Dropped the statue treatment for Braviary (revises D89).
  - Docs updated: vision v1.23, modules v1.15, design v1.12, roadmap v1.12, decision map, CLAUDE.md.
- **Next:** unchanged; M0.1 when the owner is ready.

---

## 2026-11-17 · FORUM presenter (D89)

- **Done:**
  - Cast the FORUM (Q85). As with the ATRIUM, no Pokémon stands for the hall's function (public discussion), so the choice follows a clearly Roman symbol with a fitting role.
  - Decided D89: **Braviary** (Unova form) as the Roman *aquila*, the eagle that carried SPQR, "the Senate and People of Rome": the emblem of the forum's people, not of war. Its role leans to moderation: a proud, brave guardian that protects its comrades (its lore) and swoops on abusive posts. Jupiter's eagle and any bird still link to messages.
  - Its American look is handled by the framing and by trying the bronze statue treatment of DP-4 on it in M0.7. (Statue dropped the same day by D91.)
  - Forum lore kept for its introductions: Pliny's phoenix shown in the Comitium in 47 CE and judged fake; Pliny's pigeons at Mutina; *Fama*, the goddess of rumor.
  - Reviewed and set aside: Chatot, Mr. Mime, Smeargle, Grafaiai, Primarina, Unfezant, Conkeldurr, Farigiraf, Lycanroc, Exploud, the other birds of prey, Corviknight, Hisuian Braviary, Yveltal, Tornadus (Therian Forme), Zapdos and Moltres (reasons in design §7).
  - Lore checked on Bulbapedia, PokémonDB and veekun (Braviary, Smeargle, Grafaiai, Conkeldurr, Tornadus); Pliny checked in the *Natural History*, book X.
  - Docs updated: vision v1.22, modules v1.14, design v1.11, roadmap v1.11, decision map, CLAUDE.md.
- **Next:** unchanged; M0.1 when the owner is ready.

---

## 2026-11-16 · The FORUM (D85–D88)

- **Done:**
  - Recovered the forum idea. It was dropped earlier only as a name for the metagame hall, because "foro" suggests discussion; now it is that hall: the FORUM (Foro in the menu), where users open topics and others discuss them, like Reddit (R21, D85). A post can attach a team, Pokémon, calculation or battle from the other halls, shown already analysed.
  - Placed it as Phase 6, right after accounts; the quiz and the AI assistant move to Phase 7 (D86). Merging it into Phase 5 was set aside: too large a phase, and the forum needs its own specification.
  - Reviewed how forums handle moderation and decided on layers (D87): limits by design, entrance limits, trust levels (as in Discourse and Stack Overflow), filters that hold posts for review (as Reddit's AutoModerator), reports, public rules with a penalty ladder and appeals.
  - Renamed the provisional palette Foro to Travertino (D88).
  - Opened Q84 (build or adopt Discourse), Q85 (FORUM presenter), Q86 (legal requirements and minimum age), Q87 (free CAPTCHA and filter tools).
  - Docs updated: vision v1.21, modules v1.13 (new M9 `FOR`), data strategy v1.4, architecture v1.7, design v1.10, roadmap v1.10, decision map, CLAUDE.md, README.
- **Next:** unchanged; M0.1 when the owner is ready.
- **Notes:**
  - *Forum* is the Latin word and *foro* its Spanish descendant: menu Foro / Forum, inscription FORUM, route `/forum`.
  - A public deployment must come before Phase 6.

---

## 2026-11-16 · Presenter cast (D84)

- **Done:**
  - Settled the cast (Q3) with one rule: the Pokémon's lore or a clear symbol must tell what its hall does. Each presenter also gets a clear personality that matches its function (owner's rule).
  - Decided D84: Arcanine (ATRIUM, Kanto form), Mew (BIBLIOTHECA), Falinks (LEGIO), Metagross (ABACUS), Noctowl (ATHENAEUM), Incineroar (COLOSSEUM), Delphox (AENIGMA).
  - Changes from the tentative cast: Metagross over Alakazam (its lore is about calculation; Alakazam's is psychic and magic), Noctowl over Xatu (a strategist, not a passive seer), Delphox over Zoroark and Unown (the oracle of Delphi and its riddles), Arcanine for ATRIUM (the *cave canem* guardian, noble and friendly) over Pikachu, Klefki and Farigiraf.
  - Lore checked on WikiDex (Metagross, Alakazam, Xatu, Noctowl, Delphox, Klefki, Girafarig, Growlithe, Arcanine).
  - Docs updated: vision v1.20, modules v1.12, design v1.9 (cast table with reasons and first personality sketches), decision map, CLAUDE.md.
- **Next:** unchanged; M0.1 when the owner is ready. The first presenter text (Arcanine) is written in M0.7.
- **Notes:**
  - The personalities are first sketches; they are refined when each hall's introduction is written and, for the assistant voices, in Phase 6 (Q82).
  - Two links are ours, not Game Freak's: Noctowl as Athena's owl and Arcanine as the *cave canem* dog. Texts should present them as the academy's reading.

---

## 2026-11-15 · Competitive section, VGC first (D83)

- **Done:**
  - Reviewed D81: it showed singles tiers, against the VGC focus and with many Pokémon unranked.
  - Decided D83 (Q83): a **competitive section** in every entry, built only from Smogon's data. VGC first (Phase 3): current usage rank, best usage rank ever in any VGC format (new DAT-F15, from Smogon's archive), common sets. Then Doubles (Smogon Doubles tier of the most recent generation where the Pokémon was legal) and Singles (Champions and National Dex), both from Phase 1.
  - Checked in `@pkmn/dex` 0.11.0: Doubles tiers exist for Generations 5–9 (e.g. Incineroar DOU in 7–9; Mega Kangaskhan DUber in 7, its last generation).
  - Docs updated: vision v1.19, modules v1.11, data strategy v1.3, design v1.8, roadmap v1.9, decision map.
- **Open:** the archive's real extent and the rating cut-off are confirmed in M3.3 (assumption in data strategy §8).
- **Next:** unchanged; M0.1 when the owner is ready.
- **Notes:**
  - Commit `ef47bc3` was built from files prepared before `df76819`, so it reverted the presenters decision (then also numbered D82) in the docs. The next commit restores it and renumbers this decision to D83 and Q83. Lesson: full files must be prepared from the latest `main`.

---

## 2026-11-14 · Presenters as the assistant's voice (D82)

- **Done:**
  - Revisited Q74: no single Pokémon fits both the Roman academy and an AI (Magearna reads as steampunk, Rotom as appliances).
  - Decided D82: the assistant has no figure of its own. Each hall's presenter is its voice in that hall, as the hall's *genius loci*. Presenters are peers (ATRIUM is not the head) and can hand questions to each other.
  - Opened Q82 for Phase 6 details: hand-offs, different models per presenter (tied to Q8), AI label, personas-off switch, prompts and style cards, how much character against D76.
  - Q3 gains a casting criterion: each presenter must be believable as the teacher of its hall.
  - Docs updated: vision v1.18, modules v1.10, design v1.7, roadmap v1.8, decision map.
- **Next:** unchanged; M0.1 when the owner is ready.
- **Notes:**
  - The assistant is the last thing built; nothing before Phase 6 depends on D82. The only earlier requirement (analyses callable without the UI) already exists.
  - With D82, Unown may suit AENIGMA better than Zoroark (an illusionist giving hints); to weigh when casting.

---

## 2026-11-13 · Ranking Pokémon (D81)

- **Done:**
  - Discussed ranking every Pokémon, as type tiers do for type combinations. Options weighed: a hand-made list, usage bands, a computed score, Smogon's tiers.
  - First outcome (2026-11-12): a hand-made S–F list for the Champions roster. Dropped: too much to maintain, and most of the Pokédex would stay unranked.
  - Decided D81 (Q81): show **Smogon's official tiers** in every entry, read from Showdown's data: Champions singles and National Dex singles. For VGC, which has no tiers, the same line shows Smogon's Champions VGC usage rank from Phase 3. No ranking is kept by hand. New features DAT-F14 (M0.9) and ARC-F14 (M1.3, usage rank in M3.4).
  - Checked in `@pkmn/dex` / `@pkmn/mods` 0.11.0: 383 Pokémon and forms legal in Champions (singles: 15 Uber, 32 OU, 72 UU, 243 RU…; doubles: nearly all DOU, so not shown). National Dex tiers cover nearly every Pokémon.
  - Docs updated: vision v1.17, modules v1.9, data strategy v1.2, roadmap v1.7, decision map.
- **Next:** unchanged; M0.1 when the owner is ready.
- **Notes:**
  - Commit `d124d26` added a patch file instead of applying it; the next commit removes it and carries the final D81.
  - Architecture §4 step 6 (manual files) doesn't list the type tier file; to fix when the pipeline is built, or now if the owner prefers.

---

## 2026-11-11 · Planning stage summary

First entry. Covers all planning done between 2026-11-02 and 2026-11-11 in a single long chat, now closed in favour of shorter chats per topic.

- **Done:**
  - Documents 00–06 and `CLAUDE.md` written and approved. Requirements R1–R20, decisions D1–D80.
  - **Product:**
    - A Roman academy of natural science with seven halls: ATRIUM, BIBLIOTHECA, LEGIO, ABACUS, ATHENAEUM, COLOSSEUM, AENIGMA.
    - The Pokédex is the *Historia Naturalis* book.
    - Spanish first, English second; Día and Noche themes.
  - **Technical:**
    - Angular 22 with static prerendering, a separate data pipeline, local-first storage.
    - `@smogon/calc` for damage; `@pkmn/sim` as the COLOSSEUM's battle referee.
  - **Ideas added in the final days:**
    - The active team that follows you between halls, and calculations with your own team (D68, D69).
    - Type tiers from the owner's list in `pipeline/manual/type-tiers.csv` (D71), and team or member coverage view (D72).
    - The COLOSSEUM as turn-by-turn battle testing, with chosen chance, branching history and a simple rival (D73–D75).
    - The AI assistant as a turn advisor and tutor, sharing the rival's action scoring (D76, D77).
    - Low-cost accessibility (D78).
    - Fan-content safeguards with a one-switch image fallback (D79).
    - Free-licensed music only (D80).
- **Open, each with its moment:**
  - Phase 0–1 design reviews:
    - DP-2, DP-6 and DP-7 in M0.4
    - DP-1 in M0.6
    - DP-3 and DP-4 in M0.7
    - DP-5 in M1.5
  - Presenter cast (Q3), final palette (Q28), texture sources (Q29).
  - Later phases:
    - battle engine check (Q75) and Three.js exploration (Q63) at Phase 4
    - login and Go stack (Q6, Q34) at Phase 5
    - AI model and assistant presenter (Q8, Q74) at Phase 6
    - hosting and address (Q7, Q35) at first deployment
  - Parked ideas P1–P3: fakémon, PokéPaste links, costlier accessibility options.
- **Next:**
  - The owner may keep exploring and deepening ideas before coding. New ideas go to the decision map first, in short chats per topic.
  - When ready, start **M0.1, Workspace and tooling**, with Claude Code in VS Code's terminal (roadmap §3).
- **Notes:**
  - Claude never commits. The owner commits everything to `main`.
  - Copilot's commit messages proved unreliable for documentation commits: they list files but not meaning, and twice described code that doesn't exist. Use the messages prepared in the chat, or rewrite Copilot's first line.
  - Commit `6f79b93` has a wrong message and overwrote the roadmap; `21543ee` restored it and explains.
