# Epics

_Last refreshed: 2026-05-25 (v1.12.0 — Opus cross-check recommended WIP cap reduction)._

## Rollup

| Epic | Title | Pillar (primary + secondary) | Status | Phase | Items (open/done) | Next milestone |
|---|---|---|---|---|---|---|
| [E02](epics/02-first-semiannual-self-evaluation/README.md) | First semi-annual methodology self-evaluation pass | P3 Doc currency + P2 Doc clarity | **active** | Phase 1 | 5 / 0 | BL-0006 ready for first loop pickup |
| [E01](epics/01-examples-folder/README.md) | Examples folder | P1 Doc completeness + P6 Example richness | planned | Phase 1 | 5 / 0 | Promoted to active after E02 closes |
| [E03](epics/03-git-workflow-trim/README.md) | Trim or split `09_git_workflow.md` | P2 Doc clarity | planned | Phase 1 | 4 / 0 | Promoted after E02 closes; note BL-0012 touches `methodology/` and requires maintainer handoff |
| [E04](epics/04-native-tool-templates/README.md) | Native templates for Cursor / Aider / Continue.dev | P4 Tool compatibility | planned | Phase 1 | 0 / 0 | Promoted after E02 closes; competes with E01 + E03 for the active slot |
| [E05](epics/05-cheatsheet/README.md) | CHEATSHEET.md (one-page reference) | P1 Doc completeness | planned | Phase 1 | 0 / 0 | Promoted after E02 + (E01 or E03) close |

**Counts:** **1 active**, 4 planned, 0 done.

### WIP cap note

**WIP cap = 1 active epic** (not the methodology's typical 3). Reasoning: this is a **solo-maintained project that has never closed an epic before**. Per [`methodology/03_epics.md`](../../methodology/03_epics.md) "Smaller teams should run fewer," and per the Opus-level cross-check applied at v1.12.0, starting at 1 active epic until at least one epic closes is the conservative + methodology-faithful choice. The cap will rise to 2 after E02 closes and the maintainer has observed the loop's behavior. May rise to 3 (methodology default) after the second epic closes.

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

**Observation:** With WIP cap at 1, only E02 progresses. This is deliberate — the first epic-close cycle validates the autonomous loop's discipline before more parallel work is invited. Phase 1 work on other pillars (P1, P2, P4 primary) waits until E02 closes.

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
