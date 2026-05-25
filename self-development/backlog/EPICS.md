# Epics

_Last refreshed: 2026-05-25 (Step 2 of self-development bootstrap)._

## Rollup

| Epic | Title | Pillar (primary + secondary) | Status | Phase | Items (open/done) | Next milestone |
|---|---|---|---|---|---|---|
| [E01](epics/01-examples-folder/README.md) | Examples folder | P1 Doc completeness + P6 Example richness | active | Phase 1 | 0 / 0 | First fully-worked example landed |
| [E02](epics/02-first-semiannual-self-evaluation/README.md) | First semi-annual methodology self-evaluation pass | P3 Doc currency + P2 Doc clarity | active | Phase 1 | 0 / 0 | Cold-read pass started |
| [E03](epics/03-git-workflow-trim/README.md) | Trim or split `09_git_workflow.md` | P2 Doc clarity | active | Phase 1 | 0 / 0 | Trim-vs-split decision made |
| [E04](epics/04-native-tool-templates/README.md) | Native templates for Cursor / Aider / Continue.dev | P4 Tool compatibility | planned | Phase 1 | 0 / 0 | TBD |
| [E05](epics/05-cheatsheet/README.md) | CHEATSHEET.md (one-page reference) | P1 Doc completeness | planned | Phase 1 | 0 / 0 | TBD |

**Counts:** 3 active, 2 planned, 0 done. **WIP cap:** 3 active (currently at limit; nothing else can move to `active` until one closes or one is parked).

## Pillar coverage

Inverse view: which epics touch each pillar.

| Pillar | Active epics | Planned epics | Coverage status |
|---|---|---|---|
| P1 Doc completeness | E01 (primary) | E05 (primary) | Active work in progress |
| P2 Doc clarity | E02 (secondary), E03 (primary) | — | Active work in progress |
| P3 Doc currency | E02 (primary) | — | Active work in progress |
| P4 Tool compatibility | — | E04 (primary) | No active work |
| P5 Adopter discoverability | — | — | Dormant (Phase 2 pillar) |
| P6 Example richness | E01 (secondary) | — | Active work in progress |
| P7 Community feedback loop | — | — | Dormant (Phase 2/3 pillar) |
| P8 Maintenance sustainability | — | — | Dormant (Phase 3 pillar) |
| P9 Self-improvement velocity | — | — | No epic; the bootstrap itself (Steps 0–4) is this pillar's first work |

**Observation:** P4 (Tool compatibility) is a Phase 1 primary pillar per the [master plan](../strategy/00_master_plan.md#3-pillar-roadmap), but E04 is currently `planned` not `active` because WIP cap (3) is reached. As soon as E01, E02, or E03 closes, E04 is the natural next promotion.

P9 is the cross-cutting mechanism; the bootstrap itself (Steps 0–4 of the self-development plan) is P9's first delivery vehicle. After Step 4 ships, the autonomous loop is P9's ongoing delivery.

## Status legend

- **planned** — charter exists; work has not started. Does not count against WIP cap.
- **active** — work in progress; counts against WIP cap. Currently 3 of 3 slots used.
- **done** — all items closed, exit criteria met, charter frozen.
- **parked** — work halted (priority shift, blocker, etc.); charter preserved, exit criteria not met.

## How to use this file

- **Maintainer / contributor:** glance at the rollup to see status; click into an epic for its charter and items.
- **Cross-AI review or audit:** spot-check that pillar coverage reflects active work; spot-check that WIP cap is respected.
- **Autonomous loop (Phase 5+):** use this file to identify which active epics to pick items from per the [ROI heuristic](../../methodology/04_backlog_items.md#prioritization--the-roi-heuristic).

## Refresh discipline

Update this rollup whenever:

- An epic's status changes (planned → active → done/parked).
- An item is added to or closed in any epic's `BACKLOG.md` (update the items column).
- A new epic is chartered (add a row).

Per the methodology, the rollup is a *navigation* aid — it should always reflect the current state of the underlying epic folders. Stale rollup = lost trust.
