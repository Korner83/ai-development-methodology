# Epics

_Last refreshed: 2026-08-14 (post-v1.26.0 consistency pass; E06 closed with 6 archived items; 4 done, 1 active, 1 planned; WIP cap = 2; one slot still open if maintainer wants concurrency)._

## Rollup

| Epic | Title | Pillar (primary + secondary) | Status | Phase | Items (open/done) | Next milestone |
|---|---|---|---|---|---|---|
| [E02](epics/E02-first-semiannual-self-evaluation/README.md) | First semi-annual methodology self-evaluation pass | P3 Doc currency + P2 Doc clarity | **done** (2026-05-25) | Phase 1 | 0 / 5 | First epic closed; cycle validated; next pass 2026-11-25. |
| [E01](epics/E01-examples-folder/README.md) | Examples folder | P1 Doc completeness + P6 Example richness | **done** (2026-05-25) | Phase 1 | 0 / 5 | Shipped in v1.15.0 (examples/ folder with tinker fictional project). |
| [E05](epics/E05-cheatsheet/README.md) | CHEATSHEET.md (one-page reference) | P1 Doc completeness | **done** (2026-05-25) | Phase 1 | — / 1 | Shipped in v1.15.0 (CHEATSHEET.md at repo root, ~80 lines). |
| [E03](epics/E03-git-workflow-trim/README.md) | Trim or split `09_git_workflow.md` | P2 Doc clarity | **active** (2026-05-25, v1.16.0) | Phase 1 | 4 / 0 | Promoted to active per maintainer direction. Several E02 T2 findings flow here. BL-0012 touches `methodology/` (T3-equivalent — maintainer handoff). |
| [E04](epics/E04-native-tool-templates/README.md) | Native templates for Cursor / Aider / Continue.dev | P4 Tool compatibility | planned | Phase 1 | 0 / 0 | Defer until closed-beta milestone work reveals which native templates adopters actually need. |
| [E06](epics/E06-bmad-v6-landscape-pass/README.md) | BMAD v6 landscape pass (context-handoff + review-triage conventions) | P9 Self-improvement velocity + P1 Doc completeness | **done** (2026-08-14) | Phase 1 | 0 / 6 | Chartered and closed same day at maintainer direction; 5 chartered items shipped in v1.25.0, plus BL-0021 promoted from FUTURE.md post-closure and shipped in v1.26.0. 4 Tier-2 ideas remain in FUTURE.md. |

**Counts:** **1 active** (E03), 1 planned (E04), 4 done (E01, E02, E05, E06).

### WIP cap note

**WIP cap = 2 active epics** (raised from 1 on E02 close, 2026-05-25). Reasoning: E02 closed cleanly end-to-end through the autonomous loop with the tier matrix in effect; the loop demonstrated discipline (escalate-on-doubt fired correctly; diff-verification caught real issues; maintainer-merge gate preserved). With one successful epic close on record, the cap can rise to 2 without inflating risk. The cap may rise to 3 (methodology default) after the second epic closes and the loop has demonstrated discipline across two distinct epic shapes.

## Pillar coverage

Inverse view: which epics touch each pillar.

| Pillar | Active epics | Planned epics | Coverage status |
|---|---|---|---|
| P1 Doc completeness | — | — | E01 + E05 (primary) done in v1.15.0; E06 (secondary) done in v1.25.0 |
| P2 Doc clarity | E03 (primary) | — | E02 secondary (done in v1.14.0); E03 primary (active since v1.16.0) |
| P3 Doc currency | — | — | E02 (primary) done 2026-05-25; next semi-annual pass due 2026-11-25 |
| P4 Tool compatibility | — | E04 (primary) | Planned |
| P5 Adopter discoverability | — | — | Dormant (Phase 2 pillar) |
| P6 Example richness | — | — | E01 (secondary) done in v1.15.0 (examples/ folder shipped) |
| P7 Community feedback loop | — | — | Dormant (Phase 2/3 pillar) |
| P8 Maintenance sustainability | — | — | Dormant (Phase 3 pillar) |
| P9 Self-improvement velocity | — | — | First dedicated epic (E06) closed 2026-08-14 — external-landscape import intake, shipped as v1.25.0; pillar otherwise carried by the bootstrap itself |

**Observation:** With WIP cap at 2 and 4 epics done, only E04 remains planned and one WIP slot is open. E06 closed without ever consuming a slot (chartered and executed same-day under maintainer direction), so the cap was never contended. WIP cap may rise to 3 (methodology default) after one more epic closes through the normal `active` path if the loop's discipline holds.

## Maintainer's next decision

One planned epic remains (E03 is active since 2026-05-25 and holds one WIP slot):

1. **E04 (Native templates Cursor/Aider/Continue.dev)** — P4 + medium-large effort. Depends on adopter feedback on which native templates are most useful; might pair well with closed-beta milestone work once external adopters provide signal.

Also available without chartering new work: the five Tier-2 ideas parked in [E06's FUTURE.md](epics/E06-bmad-v6-landscape-pass/FUTURE.md) (boundaries triad, memory admission test, epic context digest, brownfield discovery pass, human-review walkthrough). Promoting any of them means re-opening E06 or chartering a successor.

Suggested: **keep E04 deferred** until alpha → closed-beta milestone work reveals which native templates adopters actually want; finish E03 to free the second slot.

Alternatively the maintainer may pause new-epic promotion and prioritize Phase 1 → Phase 2 milestone work (closed beta readiness per `methodology/12`): activate distribution plan, recruit ≥ 2 external adopters, collect structured feedback. The `FEEDBACK.md` triage flow becomes load-bearing at this transition.

## Status legend

- **planned** — charter exists; work has not started. Does not count against WIP cap.
- **active** — work in progress; counts against WIP cap. Currently 1 of 2 slots used (E03).
- **done** — all items closed, exit criteria met, charter frozen.
- **parked** — work halted (priority shift, blocker, etc.); charter preserved, exit criteria not met.

## How to use this file

- **Maintainer / contributor:** glance at the rollup to see status; click into an epic for its charter and items.
- **Cross-AI review or audit:** spot-check that pillar coverage reflects active work; spot-check that WIP cap is respected.
- **Autonomous loop (Phase 5+):** use this file to identify which active epics to pick items from per the [ROI heuristic](../../methodology/04_backlog_items.md#prioritization--the-roi-heuristic). With WIP cap at 2 and 1 slot currently used (E03), E03's `BACKLOG.md` is the active pickup target.

## Refresh discipline

Update this rollup whenever:

- An epic's status changes (planned → active → done/parked).
- An item is added to or closed in any epic's `BACKLOG.md` (update the items column).
- A new epic is chartered (add a row).
- The WIP cap changes (re-check the rationale in this file).

Per the methodology, the rollup is a *navigation* aid — it should always reflect the current state of the underlying epic folders. Stale rollup = lost trust.
