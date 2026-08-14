# Epics

_Last refreshed: 2026-08-14 (E06 chartered from the BMAD v6.11 landscape review; 3 done, 1 active, 2 planned; WIP cap = 2; one slot still open if maintainer wants concurrency)._

## Rollup

| Epic | Title | Pillar (primary + secondary) | Status | Phase | Items (open/done) | Next milestone |
|---|---|---|---|---|---|---|
| [E02](epics/E02-first-semiannual-self-evaluation/README.md) | First semi-annual methodology self-evaluation pass | P3 Doc currency + P2 Doc clarity | **done** (2026-05-25) | Phase 1 | 0 / 5 | First epic closed; cycle validated; next pass 2026-11-25. |
| [E01](epics/E01-examples-folder/README.md) | Examples folder | P1 Doc completeness + P6 Example richness | **done** (2026-05-25) | Phase 1 | 0 / 5 | Shipped in v1.15.0 (examples/ folder with tinker fictional project). |
| [E05](epics/E05-cheatsheet/README.md) | CHEATSHEET.md (one-page reference) | P1 Doc completeness | **done** (2026-05-25) | Phase 1 | — / 1 | Shipped in v1.15.0 (CHEATSHEET.md at repo root, ~80 lines). |
| [E03](epics/E03-git-workflow-trim/README.md) | Trim or split `09_git_workflow.md` | P2 Doc clarity | **active** (2026-05-25, v1.16.0) | Phase 1 | 4 / 0 | Promoted to active per maintainer direction. Several E02 T2 findings flow here. BL-0012 touches `methodology/` (T3-equivalent — maintainer handoff). |
| [E04](epics/E04-native-tool-templates/README.md) | Native templates for Cursor / Aider / Continue.dev | P4 Tool compatibility | planned | Phase 1 | 0 / 0 | Defer until closed-beta milestone work reveals which native templates adopters actually need. |
| [E06](epics/E06-bmad-v6-landscape-pass/README.md) | BMAD v6 landscape pass (context-handoff + review-triage conventions) | P9 Self-improvement velocity + P1 Doc completeness | planned | Phase 1 | 5 / 0 | Chartered 2026-08-14 from the BMAD v6.11 review: 5 T2 items (BL-0015…BL-0019) + 5 deferrals in FUTURE.md; ships one-per-release like the v1.20–v1.23 passes. |

**Counts:** **1 active** (E03), 2 planned (E04, E06), 3 done (E01, E02, E05).

### WIP cap note

**WIP cap = 2 active epics** (raised from 1 on E02 close, 2026-05-25). Reasoning: E02 closed cleanly end-to-end through the autonomous loop with the tier matrix in effect; the loop demonstrated discipline (escalate-on-doubt fired correctly; diff-verification caught real issues; maintainer-merge gate preserved). With one successful epic close on record, the cap can rise to 2 without inflating risk. The cap may rise to 3 (methodology default) after the second epic closes and the loop has demonstrated discipline across two distinct epic shapes.

## Pillar coverage

Inverse view: which epics touch each pillar.

| Pillar | Active epics | Planned epics | Coverage status |
|---|---|---|---|
| P1 Doc completeness | — | E06 (secondary) | E01 + E05 (primary) both done, shipped in v1.15.0; E06 adds landscape-informed completeness work |
| P2 Doc clarity | E03 (primary) | — | E02 secondary (done in v1.14.0); E03 primary (active since v1.16.0) |
| P3 Doc currency | — | — | E02 (primary) done 2026-05-25; next semi-annual pass due 2026-11-25 |
| P4 Tool compatibility | — | E04 (primary) | Planned |
| P5 Adopter discoverability | — | — | Dormant (Phase 2 pillar) |
| P6 Example richness | — | — | E01 (secondary) done in v1.15.0 (examples/ folder shipped) |
| P7 Community feedback loop | — | — | Dormant (Phase 2/3 pillar) |
| P8 Maintenance sustainability | — | — | Dormant (Phase 3 pillar) |
| P9 Self-improvement velocity | — | E06 (primary) | First dedicated epic chartered (E06, planned 2026-08-14) — external-landscape import intake; previously covered by the bootstrap itself |

**Observation:** With WIP cap at 2 and 3 epics done, 2 planned epics remain (E04, E06) and one WIP slot is open. The maintainer may promote either per ROI heuristic. WIP cap may rise to 3 (methodology default) after one more epic closes if the loop's discipline holds.

## Maintainer's next decision

ROI-ranked recommendation for the 2 planned epics (E03 was promoted to active on 2026-05-25 and holds one WIP slot):

1. **E06 (BMAD v6 landscape pass)** — P9 + small/medium per item. Five independent T2 items (BL-0015…BL-0019) that ship one-per-release like the v1.20–v1.23 landscape passes; the loop may draft wording, the maintainer authors each release. Fits the open WIP slot without disturbing E03. BL-0017 + BL-0018 batch naturally into one "review rigor" release.
2. **E04 (Native templates Cursor/Aider/Continue.dev)** — P4 + medium-large effort. Depends on adopter feedback on which native templates are most useful; might pair well with closed-beta milestone work once external adopters provide signal.

Suggested: **promote E06 when ready for the next methodology release cycle**; **keep E04 deferred** until alpha → closed-beta milestone work reveals which native templates adopters actually want.

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
