# Pokescientia — Progress Log

Session log (D65). Newest entry first. Each session, in a chat or in Claude Code, adds one short entry: what was done, what is next, and anything worth remembering. Milestone status lives in the checkboxes of [`06-roadmap-and-milestones.md`](06-roadmap-and-milestones.md); decisions live in [`01-vision-and-requirements.md`](01-vision-and-requirements.md) and [`00-decision-map.md`](00-decision-map.md).

**How to start a new session:** read [`CLAUDE.md`](../CLAUDE.md), this file (latest entry first), the decision map and the documents the topic touches. The documents, not past chats, are the project's memory.

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
