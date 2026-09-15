# ACTIVE_CONTEXT.md — volatile working state

_Last updated: 2026-09-15._

## Current focus

Implementing the user-approved v1.35.0 assurance-and-squads plan on
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

1. Complete canonical guidance, then adoption surfaces and examples.
2. Run final structural and scenario checks; record evidence in E11/TEST.md.
3. Leave independent review and maintainer acceptance visibly pending until performed.

## Carried forward

E10 still awaits its independent re-audit; this task does not close it.
BL-0058 remains the unrelated open intake item. No executable checker or new CI.
