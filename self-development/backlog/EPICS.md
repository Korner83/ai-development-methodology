# Epics

_Last refreshed: 2026-08-14 (E03 closed — `09_git_workflow.md` trimmed to 798 lines, v1.27.0; 5 done, 0 active, 1 planned; WIP cap = 2, both slots now free)._

## Rollup

| Epic | Title | Pillar (primary + secondary) | Status | Phase | Items (open/done) | Next milestone |
|---|---|---|---|---|---|---|
| [E02](epics/E02-first-semiannual-self-evaluation/README.md) | First semi-annual methodology self-evaluation pass | P3 Doc currency + P2 Doc clarity | **done** (2026-05-25) | Phase 1 | 0 / 5 | First epic closed; cycle validated; next pass 2026-11-25. |
| [E01](epics/E01-examples-folder/README.md) | Examples folder | P1 Doc completeness + P6 Example richness | **done** (2026-05-25) | Phase 1 | 0 / 5 | Shipped in v1.15.0 (examples/ folder with tinker fictional project). |
| [E05](epics/E05-cheatsheet/README.md) | CHEATSHEET.md (one-page reference) | P1 Doc completeness | **done** (2026-05-25) | Phase 1 | — / 1 | Shipped in v1.15.0 (CHEATSHEET.md at repo root, ~80 lines). |
| [E03](epics/E03-git-workflow-trim/README.md) | Trim or split `09_git_workflow.md` | P2 Doc clarity | **done** (2026-08-14) | Phase 1 | 0 / 4 | Trim chosen over split; 1,026 → 798 lines (−22%), 24 → 20 sections, zero content lost. Shipped in v1.27.0. |
| [E04](epics/E04-native-tool-templates/README.md) | Native templates for Cursor / Aider / Continue.dev | P4 Tool compatibility | planned | Phase 1 | 0 / 0 | Defer until closed-beta milestone work reveals which native templates adopters actually need. |
| [E06](epics/E06-bmad-v6-landscape-pass/README.md) | BMAD v6 landscape pass (context-handoff + review-triage conventions) | P9 Self-improvement velocity + P1 Doc completeness | **done** (2026-08-14) | Phase 1 | 0 / 6 | Chartered and closed same day at maintainer direction; 5 chartered items shipped in v1.25.0, plus BL-0021 promoted from FUTURE.md post-closure and shipped in v1.26.0. 4 Tier-2 ideas remain in FUTURE.md. |

**Counts:** **0 active**, 1 planned (E04), 5 done (E01, E02, E03, E05, E06).

### WIP cap note

**WIP cap = 2 active epics** (raised from 1 on E02 close, 2026-05-25). Reasoning: E02 closed cleanly end-to-end through the autonomous loop with the tier matrix in effect; the loop demonstrated discipline (escalate-on-doubt fired correctly; diff-verification caught real issues; maintainer-merge gate preserved). With one successful epic close on record, the cap can rise to 2 without inflating risk. The cap may rise to 3 (methodology default) after the second epic closes and the loop has demonstrated discipline across two distinct epic shapes.

## Pillar coverage

Inverse view: which epics touch each pillar.

| Pillar | Active epics | Planned epics | Coverage status |
|---|---|---|---|
| P1 Doc completeness | — | — | E01 + E05 (primary) done in v1.15.0; E06 (secondary) done in v1.25.0 |
| P2 Doc clarity | — | — | E02 secondary (done v1.14.0); E03 primary (done v1.27.0 — 09 trimmed to 798 lines) |
| P3 Doc currency | — | — | E02 (primary) done 2026-05-25; next semi-annual pass due 2026-11-25 |
| P4 Tool compatibility | — | E04 (primary) | Planned |
| P5 Adopter discoverability | — | — | Dormant (Phase 2 pillar) |
| P6 Example richness | — | — | E01 (secondary) done in v1.15.0 (examples/ folder shipped) |
| P7 Community feedback loop | — | — | Dormant (Phase 2/3 pillar) |
| P8 Maintenance sustainability | — | — | Dormant (Phase 3 pillar) |
| P9 Self-improvement velocity | — | — | First dedicated epic (E06) closed 2026-08-14 — external-landscape import intake, shipped as v1.25.0; pillar otherwise carried by the bootstrap itself |

**Observation:** With 5 epics done, **both WIP slots are now free** and only E04 remains planned. Two of the five closures (E03, E06) ran to completion inside a single maintainer-directed session rather than through a sustained `active` period, so the cap has still never actually been contended. Raising it to 3 (the methodology default) would be premature on that evidence — the cap should rise when concurrency is real, not when the counter allows it.

## Maintainer's next decision

One planned epic remains, and both WIP slots are free:

1. **E04 (Native templates Cursor/Aider/Continue.dev)** — P4 + medium-large effort. Depends on adopter feedback on which native templates are most useful; might pair well with closed-beta milestone work once external adopters provide signal.

Also available without chartering new work: the four remaining Tier-2 ideas in [E06's FUTURE.md](epics/E06-bmad-v6-landscape-pass/FUTURE.md) (boundaries triad, epic context digest, brownfield discovery pass, human-review walkthrough — the memory admission test was promoted and shipped in v1.26.0). Promoting any of them means re-opening E06 or chartering a successor.

Suggested: **keep E04 deferred** until alpha → closed-beta milestone work reveals which native templates adopters actually want. With no active epic and no doc-quality work outstanding, the binding constraint is no longer the backlog — it is the Phase 1 → Phase 2 transition below.

Alternatively the maintainer may pause new-epic promotion and prioritize Phase 1 → Phase 2 milestone work (closed beta readiness per `methodology/12`): activate distribution plan, recruit ≥ 2 external adopters, collect structured feedback. The `FEEDBACK.md` triage flow becomes load-bearing at this transition.

## Status legend

- **planned** — charter exists; work has not started. Does not count against WIP cap.
- **active** — work in progress; counts against WIP cap. Currently 0 of 2 slots used.
- **done** — all items closed, exit criteria met, charter frozen.
- **parked** — work halted (priority shift, blocker, etc.); charter preserved, exit criteria not met.

## How to use this file

- **Maintainer / contributor:** glance at the rollup to see status; click into an epic for its charter and items.
- **Cross-AI review or audit:** spot-check that pillar coverage reflects active work; spot-check that WIP cap is respected.
- **Autonomous loop (Phase 5+):** use this file to identify which active epics to pick items from per the [ROI heuristic](../../methodology/04_backlog_items.md#prioritization--the-roi-heuristic). **There is currently no active epic**, so there is no pickup target — the loop should halt and surface rather than promoting one itself (epic promotion is a maintainer decision).

## Refresh discipline

Update this rollup whenever:

- An epic's status changes (planned → active → done/parked).
- An item is added to or closed in any epic's `BACKLOG.md` (update the items column).
- A new epic is chartered (add a row).
- The WIP cap changes (re-check the rationale in this file).

Per the methodology, the rollup is a *navigation* aid — it should always reflect the current state of the underlying epic folders. Stale rollup = lost trust.
