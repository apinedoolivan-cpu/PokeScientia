# Pokescientia — Progress Log

Session log (D65). Newest entry first. Each session, in a chat or in Claude Code, adds one short entry: what was done, what is next, and anything worth remembering. Milestone status lives in the checkboxes of [`06-roadmap-and-milestones.md`](06-roadmap-and-milestones.md); decisions live in [`01-vision-and-requirements.md`](01-vision-and-requirements.md) and [`00-decision-map.md`](00-decision-map.md).

**How to start a new session:** read [`CLAUDE.md`](../CLAUDE.md), this file (latest entry first), the decision map and the documents the topic touches. The documents, not past chats, are the project's memory.

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
