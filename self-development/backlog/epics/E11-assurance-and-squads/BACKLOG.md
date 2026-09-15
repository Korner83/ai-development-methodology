# E11 — Active backlog

## Summary

| ID | Title | Priority | Effort | Status |
|---|---|---|---|---|
| BL-0063 | Define assurance and squad operating rules | P1 | M | under-review |
| BL-0064 | Propagate adoption guidance and worked examples | P1 | M | in-progress |
| BL-0065 | Verify consistency and prepare v1.35.0 | P1 | S | ready |

### BL-0063 — Define assurance and squad operating rules

| Field | Value |
|---|---|
| Epic | E11-assurance-and-squads |
| Pillar | P1 |
| Priority | P1 |
| Effort | M |
| Status | under-review |
| Test | partial — local checks complete; independent review and acceptance pending |
| Deps | — |
| Lock | — |
| Assurance | A2 — material |
| Accountable owner | repository maintainer |

**Why / Description:** Implement the approved risk-based software-squad plan without creating competing verification rules or weaker production controls.

**Done means:** A0–A3, conditional item fields, human capability ownership, independent verification and acceptance, parallel-squad queue limits, rotation readiness, and optional reusable-asset graduation are coherent with existing gates. Independent review and maintainer acceptance are recorded.

**Code Map:** `methodology/07_definition_of_done.md` owns the assurance overlay; `11_human_roles.md` owns responsibilities and review capacity. `03_epics.md` owns charter fields; `04_backlog_items.md` owns conditional metadata and cold handoff (1,036 lines before edits, cap 1,050). `10_testing_and_verification.md` already owns cumulative L0–L4 levels. `06_working_principles.md` owns simplicity. `00_README.md` and root README carry the unqualified peers framing. Preserve existing anchors and enums; link between these definitions rather than duplicating tables.

**Verification:** [TEST.md](TEST.md) scenarios plus full diff review. Independent review and acceptance pending.

### BL-0064 — Propagate adoption guidance and worked examples

| Field | Value |
|---|---|
| Epic | E11-assurance-and-squads |
| Pillar | P1 |
| Priority | P1 |
| Effort | M |
| Status | in-progress |
| Test | pending |
| Deps | BL-0063 |
| Lock | codex-e11@2026-09-15T16:02Z |
| Assurance | A2 — inherited operating-rule changes |
| Accountable owner | repository maintainer |

**Why / Description:** Make the approved practices discoverable at project setup and daily use, with realistic software-squad examples.

**Done means:** Relevant templates and skill link to canonical guidance; examples cover solo and three-person squads, material review, and blocked cases; examples are labeled illustrative, not evidence of external adoption. Independent review and maintainer acceptance are recorded.

**Code Map:** `templates/AGENTS.md` and `CLAUDE.md` share an operating-contract section and adopter-relative links. `AGENT_KICKOFF.md`, `ROLE_BRIEFS.md`, and `AUTONOMOUS_LOOP.md` supply phase prompts; role briefs cap at 200 lines. `skills/ai-dev-methodology/SKILL.md` has YAML frontmatter and a version pin. `examples/README.md` indexes a v1.28.0 fictional project; keep that historical pin separate from the new v1.35.0 squad walkthrough.

**Verification:** Template parity, skill YAML parsing, links/anchors, line counts, and scenario walkthroughs in [TEST.md](TEST.md). Independent review and acceptance pending.

### BL-0065 — Verify consistency and prepare v1.35.0

| Field | Value |
|---|---|
| Epic | E11-assurance-and-squads |
| Pillar | P2 |
| Priority | P1 |
| Effort | S |
| Status | ready |
| Test | not-tested |
| Deps | BL-0063, BL-0064 |
| Lock | — |
| Assurance | A2 — inherited release assurance |
| Accountable owner | repository maintainer |

**Why / Description:** Verify the final documentation tree and prepare a reviewable release with honest evidence.

**Done means:** Final-tree structural checks and all planned scenarios are recorded, release pins agree, line budgets hold, independent verification and maintainer acceptance are recorded, and no unperformed release or review is claimed.

**Verification:** Follow [release evidence](../../../RELEASE_EVIDENCE.md); record commands/method and results in [TEST.md](TEST.md). No runtime product or automated behavioral suite exists in this docs-only repository; structural checks do not constitute specialist or independent assurance.

**Frozen intent:** All three item goals and acceptance criteria derive from the user-approved implementation plan on 2026-09-15. Do not weaken them to close the items.
