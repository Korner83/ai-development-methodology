# Epics

_Last refreshed: 2026-05-25 (E01 + E05 closed in v1.15.0; 3 epics done total; WIP cap at 2; E03 + E04 eligible for next active slots)._

## Rollup

| Epic | Title | Pillar (primary + secondary) | Status | Phase | Items (open/done) | Next milestone |
|---|---|---|---|---|---|---|
| [E02](epics/02-first-semiannual-self-evaluation/README.md) | First semi-annual methodology self-evaluation pass | P3 Doc currency + P2 Doc clarity | **done** (2026-05-25) | Phase 1 | 0 / 5 | First epic closed; cycle validated; next pass 2026-11-25. |
| [E01](epics/01-examples-folder/README.md) | Examples folder | P1 Doc completeness + P6 Example richness | **done** (2026-05-25) | Phase 1 | 0 / 5 | Shipped in v1.15.0 (examples/ folder with tinker fictional project). |
| [E05](epics/05-cheatsheet/README.md) | CHEATSHEET.md (one-page reference) | P1 Doc completeness | **done** (2026-05-25) | Phase 1 | — / 1 | Shipped in v1.15.0 (CHEATSHEET.md at repo root, ~80 lines). |
| [E03](epics/03-git-workflow-trim/README.md) | Trim or split `09_git_workflow.md` | P2 Doc clarity | planned | Phase 1 | 4 / 0 | Eligible for promotion (open WIP slot). Some E02 T2 findings flow here. BL-0012 touches `methodology/` (T3-equivalent — maintainer handoff). |
| [E04](epics/04-native-tool-templates/README.md) | Native templates for Cursor / Aider / Continue.dev | P4 Tool compatibility | planned | Phase 1 | 0 / 0 | Eligible for promotion (open WIP slot). |

**Counts:** **0 active**, 2 planned, 3 done.

### WIP cap note

**WIP cap = 2 active epics** (raised from 1 on E02 close, 2026-05-25). Reasoning: E02 closed cleanly end-to-end through the autonomous loop with the tier matrix in effect; the loop demonstrated discipline (escalate-on-doubt fired correctly; diff-verification caught real issues; maintainer-merge gate preserved). With one successful epic close on record, the cap can rise to 2 without inflating risk. The cap may rise to 3 (methodology default) after the second epic closes and the loop has demonstrated discipline across two distinct epic shapes.

## Pillar coverage

Inverse view: which epics touch each pillar.

| Pillar | Active epics | Planned epics | Coverage status |
|---|---|---|---|
| P1 Doc completeness | — | E01 (primary), E05 (primary) | Planned; activates after E02 closes |
| P2 Doc clarity | E02 (secondary) | E03 (primary) | E02 secondary in active work; E03 planned |
| P3 Doc currency | E02 (primary) | — | **Active work in progress** |
| P4 Tool compatibility | — | E04 (primary) | Planned |
| P5 Adopter discoverability | — | — | Dormant (Phase 2 pillar) |
| P6 Example richness | — | E01 (secondary) | Planned via E01 |
| P7 Community feedback loop | — | — | Dormant (Phase 2/3 pillar) |
| P8 Maintenance sustainability | — | — | Dormant (Phase 3 pillar) |
| P9 Self-improvement velocity | — | — | No epic; the bootstrap itself (Steps 0–4 of the self-development plan) is this pillar's first work |

**Observation:** With WIP cap at 2 and 3 epics now done, 2 planned epics remain. The maintainer may promote either or both per ROI heuristic. WIP cap may rise to 3 (methodology default) after one more epic closes if the loop's discipline holds.

## Maintainer's next decision

ROI-ranked recommendation for the remaining 2 planned epics:

1. **E03 (Trim/split 09_git_workflow.md)** — P2 + medium effort. Some of E02's 28 T2 findings flow naturally here; could batch the loop-notes follow-ups into E03's scope. **Note:** BL-0012 in E03 touches `methodology/` and is a T2-equivalent (maintainer-authored per tier matrix).
2. **E04 (Native templates Cursor/Aider/Continue.dev)** — P4 + medium-large effort. Depends on adopter feedback on which native templates are most useful; might pair well with closed-beta milestone work once external adopters provide signal.

Both can be active simultaneously (WIP cap at 2). Suggested: **promote E03 first** (closes more methodology-level cleanup); **defer E04** until alpha → closed-beta milestone work reveals which native templates adopters actually want.

Alternatively the maintainer may pause new-epic promotion and prioritize Phase 1 → Phase 2 milestone work (closed beta readiness per `methodology/12`): activate distribution plan, recruit ≥ 2 external adopters, collect structured feedback. The `FEEDBACK.md` triage flow becomes load-bearing at this transition.

## Status legend

- **planned** — charter exists; work has not started. Does not count against WIP cap.
- **active** — work in progress; counts against WIP cap. Currently 1 of 1 slot used.
- **done** — all items closed, exit criteria met, charter frozen.
- **parked** — work halted (priority shift, blocker, etc.); charter preserved, exit criteria not met.

## How to use this file

- **Maintainer / contributor:** glance at the rollup to see status; click into an epic for its charter and items.
- **Cross-AI review or audit:** spot-check that pillar coverage reflects active work; spot-check that WIP cap is respected.
- **Autonomous loop (Phase 5+):** use this file to identify which active epics to pick items from per the [ROI heuristic](../../methodology/04_backlog_items.md#prioritization--the-roi-heuristic). With WIP cap at 1, only E02 is currently pickable.

## Refresh discipline

Update this rollup whenever:

- An epic's status changes (planned → active → done/parked).
- An item is added to or closed in any epic's `BACKLOG.md` (update the items column).
- A new epic is chartered (add a row).
- The WIP cap changes (re-check the rationale in this file).

Per the methodology, the rollup is a *navigation* aid — it should always reflect the current state of the underlying epic folders. Stale rollup = lost trust.
