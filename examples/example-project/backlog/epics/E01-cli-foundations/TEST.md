# E01 — CLI foundations — Test scenarios

_Epic-specific acceptance + regression scenarios. The cross-epic manual-QA queue lives in [../../TEST_BACKLOG.md](../../TEST_BACKLOG.md)._

## Acceptance tests for exit criteria

Each row corresponds to an exit criterion in the [epic charter](README.md). Status reflects whether the acceptance scenario has been run + passed.

| ID    | Scenario                                                                                  | Status        |
|-------|-------------------------------------------------------------------------------------------|---------------|
| AT-01 | `tinker capture "test note"` returns in < 300ms; note retrievable in store               | not-tested       |
| AT-02 | `tinker capture` (no arg) opens `$EDITOR`; empty save = no note; non-empty = stored      | not-tested       |
| AT-03 | `tinker recent` returns last 20 notes for cwd ordered by timestamp desc                  | not-tested       |
| AT-04 | Install one-line works on macOS (brew), Linux (apt or cargo), Windows (choco or cargo)   | partial       |
| AT-05 | Full test suite (`cargo test`) green on all 3 OS in CI                                   | pass — BL-0001 |

## Regression scenarios to protect

Once an item closes with `Test: pass`, its acceptance scenario lands here as a regression to protect on every future change. Run before any v1.0-equivalent release.

| Area        | Scenario                                                | Last verified |
|-------------|---------------------------------------------------------|---------------|
| CI baseline | `cargo test` green on macOS / Linux / Windows           | BL-0001 close |

## Manual-QA scenarios (operator-driven)

Scenarios that can't be cheaply automated and need human eyes — typically UX feel, install-path friction, error-message clarity.

| Scenario                                                          | Cadence              | Notes |
|-------------------------------------------------------------------|----------------------|-------|
| Time the install flow on a fresh machine; goal < 60s              | Per minor release    | First-success-time KPI |
| `tinker capture` error messages on `EACCES` / no editor / disk full | Per minor release    | Error clarity check |
| `tinker recent` output readable in 80-col + 200-col terminals     | Per minor release    | Layout check |

## Conventions

- **Acceptance test IDs** use `AT-##` (epic-scoped, monotonic).
- **Status values** use the [Test enum](../../../../../methodology/04_backlog_items.md#test-enum) unchanged — all eight values, no subset: `not-tested` / `pending` / `manual-verified` / `partial` / `pass` / `fail: <detail>` / `regression-needed` / `n/a`.
- When an acceptance test maps to a closed item, cite the BL-### in the Status column (e.g., `pass — BL-0001`).
- Regression scenarios are append-only after first inclusion — never delete; mark `deprecated` if no longer relevant.
