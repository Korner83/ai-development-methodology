# P1 — Doc completeness

> **Pillar goal:** for every common situation an adopter encounters, the methodology has explicit, findable guidance.
>
> **Last updated:** 2026-05-25

**Related:**
- Brief: [Capability layer 1](../brief/08_capability_layers.md#1-doc-completeness)
- Strategy phase: [Phase 1 — Foundation](../strategy/00_master_plan.md#phase-1--foundation-current--3-months) (primary)
- Depends on: nothing (foundational)
- Feeds into: [P2 — Doc clarity](P2_doc_clarity.md) (clarity is improvement on top of completeness)
- Delivering epics: (none yet)

## 1. Overview

This is the first pillar because nothing else works without it. Gaps in coverage send adopters away — a methodology that's good on 8 of 10 needed surfaces feels incomplete; adopters either improvise (and get burned) or leave for a more complete option.

Doc completeness asks: for each common adopter situation, does the methodology say something specific? Not "we have a section about that area" but "an adopter who lands here gets actionable guidance." The bar is *findable + actionable*, not just *present*.

## 2. What this pillar covers

| Surface | What "complete" means here |
|---|---|
| **Planning** (strategy / pillars / epics / items) | Every layer has a doc that explains its shape, lifecycle, and required content. |
| **Discipline** (working principles / DoD / memory) | Every discipline has a doc with rules + anti-patterns + concrete examples. |
| **Operations** (locks / git workflow / testing) | Every operational surface has rules + protocols + recovery patterns. |
| **Human dimension** (roles / decision ownership) | The human side of AI-driven workflow is named, not assumed. |
| **Templates** | Every AI tool with significant adopter share has a template (or adapted template). |
| **Worked example** | At least one concrete worked example exists (the self-development folder). |
| **Operational adopter questions** | "How do I cut a release?" "What if I'm doing brownfield adoption?" "How do I handle a hot-fix?" — each has explicit guidance. |
| **Edge cases** | "What happens when the lock TTL expires?" "What goes in HUMAN_NEEDED.md?" "When should I deviate from the ROI heuristic?" — each named. |

## 3. Exit criteria

The pillar is *delivered* (not done — it's evergreen) when:

- [ ] All 12 methodology docs have been reviewed in the most recent semi-annual self-evaluation pass with no "missing" gaps surfaced by cross-AI review.
- [x] Each of the 6 supported AI tools (Claude Code, OpenAI Codex, Google Antigravity, Cursor, Aider, Continue.dev) has a usable starting template — either native (3: CLAUDE.md, AGENTS.md, and AGENTS.md again for Antigravity) or adaptable (3, from AGENTS.md). Adaptation is the accepted permanent answer; the epic that proposed native files for the latter three (E04) was parked 2026-08-14.
- [ ] At least one worked example folder exists in the repo (the `self-development/` folder satisfies this as of v1.7.0).
- [ ] Every Discussions / Issues thread tagged as a "how do I" question has a recorded response (from maintainer or community) within 30 days that either links to an existing doc as the answer or is logged as a methodology gap candidate for the next release.

**Re-tested:** every semi-annual self-evaluation pass (per [methodology/07_definition_of_done.md](../../methodology/07_definition_of_done.md#methodology-self-evaluation-semi-annual)). The fourth criterion above only becomes testable once Discussions activity exists; until then, treat as N/A.

**Health indicators** (not binary, but worth watching):

- Adopter questions repeat across multiple threads with no existing answer → likely a gap to file.
- "I had to read this three times" feedback → completeness might be OK but pairs with a clarity (P2) issue.

## 4. Dependencies

**Depends on:** nothing. This is the foundational pillar.

**Feeds into:**

- **P2 Doc clarity** — completeness is necessary but insufficient; the next pillar makes the complete docs actually readable.
- **P3 Doc currency** — completeness must be maintained as the methodology evolves; currency keeps it true.
- **P5 Adopter discoverability** — discoverability is downstream of having complete enough docs to make discovery worthwhile.

## 5. Anti-patterns

- **Writing a doc to fill a section heading rather than because adopters need it.** Empty stubs are worse than missing sections.
- **Repeating content across docs** because each section "should be self-contained." Cross-references > duplication. Drift will follow duplication.
- **Adding sections without testing whether adopters find them.** A complete-but-buried doc is functionally missing.
- **Over-specifying** — writing 800 lines when 200 would do. Completeness is "covers the surface," not "exhausts the surface."
- **Treating completeness as binary** — the surface area grows as adopters use the methodology in new contexts. Re-evaluate continuously.

## 6. Current state (v1.8.0)

**Strong:**

- 12 methodology docs cover planning, discipline, operations, human roles.
- 6 templates cover the major AI tools and the working phases (CLAUDE.md, AGENTS.md, AGENT_KICKOFF.md, AUTONOMOUS_LOOP.md, PROJECT_STRUCTURE.md, ROLE_BRIEFS.md — the last added in v1.30.0).
- v1.5.0 added 4 substantive new sections (stdlib growth loop, verification taxonomy, brownfield onboarding, decision matrix).
- v1.6.0 added 5 more (self-evaluation cadence, lock-file management, squash-vs-merge, AI-autonomy-in-git, release tagging, hot-fix workflow).
- `self-development/` worked example exists.

**Known gaps (as of v1.8.0):**

- No anonymized real-project examples beyond the self-development folder. (Tracked as a potential Phase 2 epic.)
- No CHEATSHEET.md / one-page reference. (Deferred; the brief and TL;DR sections serve this partially.)

**Honest:** completeness is the most-developed pillar currently. The next ~3 months of Phase 1 work is incremental polish, not major additions.

## 7. Delivering epics

(None yet. Epics get added here as Step 2 of the self-development bootstrap charters them.)
