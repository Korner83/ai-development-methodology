# Epics

_Last refreshed: 2026-05-25 (E02 closed; WIP cap raised to 2; awaiting maintainer choice of next active epic)._

## Rollup

| Epic | Title | Pillar (primary + secondary) | Status | Phase | Items (open/done) | Next milestone |
|---|---|---|---|---|---|---|
| [E02](epics/02-first-semiannual-self-evaluation/README.md) | First semi-annual methodology self-evaluation pass | P3 Doc currency + P2 Doc clarity | **done** (2026-05-25) | Phase 1 | 0 / 5 | First epic closed; cycle validated; next pass 2026-11-25. |
| [E01](epics/01-examples-folder/README.md) | Examples folder | P1 Doc completeness + P6 Example richness | planned | Phase 1 | 5 / 0 | Eligible for promotion to active (open WIP slot). |
| [E03](epics/03-git-workflow-trim/README.md) | Trim or split `09_git_workflow.md` | P2 Doc clarity | planned | Phase 1 | 4 / 0 | Eligible for promotion; some of the 28 T2 findings from E02 may land here. Note BL-0012 touches `methodology/` (T3-equivalent — maintainer handoff). |
| [E04](epics/04-native-tool-templates/README.md) | Native templates for Cursor / Aider / Continue.dev | P4 Tool compatibility | planned | Phase 1 | 0 / 0 | Eligible for promotion. |
| [E05](epics/05-cheatsheet/README.md) | CHEATSHEET.md (one-page reference) | P1 Doc completeness | planned | Phase 1 | 0 / 0 | Eligible for promotion; smallest scope of the four planned epics. |

**Counts:** **0 active**, 4 planned, 1 done.

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

**Observation:** With WIP cap at 2 and E02 closed, two of the four remaining planned epics can be active simultaneously. The maintainer's choice of which to promote next is open — see "Maintainer's next decision" below the rollup.

## Maintainer's next decision

E02 has closed; WIP cap is 2; one or two of the four planned epics can promote to active. ROI-ranked recommendation:

1. **E05 (CHEATSHEET.md)** — P1 + smallest effort (likely XS-S items). Highest near-term ROI per `04_backlog_items.md` heuristic. **Recommended first promotion.**
2. **E01 (Examples folder)** — P1 + medium effort. Examples are widely-requested by adopters; pairs well with E05's one-page reference.
3. **E03 (Trim/split 09_git_workflow.md)** — P2 + medium effort. Some of E02's 28 T2 findings flow naturally here; could batch the loop-notes follow-ups into E03's scope. **Note:** BL-0012 in E03 touches `methodology/` and is a T2-equivalent (maintainer-authored per tier matrix).
4. **E04 (Native templates Cursor/Aider/Continue.dev)** — P4 + medium-large effort. Depends on adopter feedback on which native templates are most useful; can wait until E01/E03/E05 produce that feedback signal.

A reasonable shape: promote **E05 + E01** to active (both P1, complementary scope, both serve adopter discoverability). Defer E03 + E04 until either the loop closes E05/E01 or the maintainer ships the 28 T2 follow-ups from E02.

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
