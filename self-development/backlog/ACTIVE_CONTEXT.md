# ACTIVE_CONTEXT.md — volatile working state

_Last updated: 2026-09-15._

## Current focus

Prepared the user-approved v1.35.0 assurance-and-squads plan on
`codex/assurance-and-squads-v1.35`, based on `1d43c70` (v1.34.0).
See [E11](epics/E11-assurance-and-squads/README.md) and its [items](epics/E11-assurance-and-squads/BACKLOG.md).
E10 and E11 consume both active-epic slots; standing E00 is exempt.

## Decisions

Software-delivery scope; A1 default with mandatory A2/A3 controls by risk.
A2 verifier may be a separate human or fresh AI session using reproducible evidence;
A3 requires qualified human specialist verification. Parallel squads declare both
item WIP limits. Existing DoD, verification levels, and production restrictions remain.
The user approved implementation, not the resulting review verdict or release.

## Next steps

1. Independent reviewer checks the final branch against the approved plan and E11/TEST.md.
2. Maintainer records acceptance. BL-0063/0064 are under-review; BL-0065 is blocked
   on that handoff, with all locks released and the human-needed registry updated.
3. After review/acceptance, update item/epic states and complete the normal PR release
   process. v1.35.0 pins are prepared; no tag or release has been created.

## Local verification

Scenario walkthroughs and structural checks are recorded in E11/TEST.md.
No new unresolved local links; valid skill YAML; template parity; current-version
pins agree; line budgets preserved. The one doc-02 illustrative link placeholder
predates this branch. These are author checks, not independent assurance.

## Carried forward

E10 still awaits its independent re-audit; this task does not close it.
BL-0058 remains the unrelated open intake item. No executable checker or new CI.
