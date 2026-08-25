# `tinker` — cross-epic manual-QA queue

_Cross-epic test scenarios that span multiple epics or don't belong to any single one. Epic-specific scenarios live in each epic's `TEST.md`._

## Active manual-QA scenarios

| ID    | Scenario                                                                          | Affects (epics)   | Cadence              | Status   |
|-------|-----------------------------------------------------------------------------------|-------------------|----------------------|----------|
| QA-01 | Fresh-machine install timed end-to-end; target < 60s on macOS / Linux / Windows  | E01, E03 (pkging) | Per minor release    | not-tested  |
| QA-02 | Note round-trip across capture → search → edit (with E02 search shipped)         | E01, E02          | Per minor release    | n/a (E02 not yet active) |
| QA-03 | Calendar-event integration (when E02's calendar feature ships)                   | E02               | Per minor release    | n/a (E02 not yet active) |

## Acceptance-test inventory (pointers to epic TEST.md files)

| Epic | TEST.md | Active scenarios |
|------|---------|------------------|
| E01 — CLI foundations | [epics/E01-cli-foundations/TEST.md](epics/E01-cli-foundations/TEST.md) | AT-01 through AT-05 |
| E02 — Search + filters (not yet chartered) | _(no TEST.md yet)_ | — |
| E03 — Install + packaging (not yet chartered) | _(no TEST.md yet)_ | — |

## Conventions

- **QA IDs** use `QA-##` (cross-epic, monotonic) to distinguish from epic-scoped `AT-##`.
- Per-epic acceptance tests live in `epics/<E##-slug>/TEST.md`. This file holds only scenarios that span ≥ 2 epics.
- "Status" mirrors the [Test enum](../../../methodology/04_backlog_items.md#test-enum).
- When a cross-epic scenario passes, it lands in the affected epics' regression-scenarios sections + an entry here marks the last-verified date.

## How this fits the methodology

This file is the operator-facing queue that pairs with the per-epic `TEST.md` files (see [`methodology/03_epics.md` "Standard epic-folder structure"](../../../methodology/03_epics.md#standard-epic-folder-structure)). The autonomous loop can pick up automated test work; manual QA stays with the human operator and the cadence is enforced before each milestone declaration per [`methodology/12_milestone_evaluation.md`](../../../methodology/12_milestone_evaluation.md).
