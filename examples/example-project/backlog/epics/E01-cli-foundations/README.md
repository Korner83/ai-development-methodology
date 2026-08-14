# E01 — CLI foundations

_Example epic charter. Following the [03_epics.md](../../../../../methodology/03_epics.md) skeleton._

**Pillar (primary):** [P1 — Capture](../../../pillars/P1_capture.md)
**Status:** active
**Phase:** Phase 1 — Foundation
**Started:** (fictional date)
**Target close:** ~6 weeks
**Owner:** maintainer + AI coding agent

> **Frozen intent** — Outcome and exit criteria approved by maintainer on
> 2026-05-18. Agents do not edit them; halt and renegotiate instead.

## Outcome (jobs-to-be-done)

When a developer wants to capture a quick note in the middle of a coding session, they want a `tinker capture` command that works in one keystroke from anywhere on the system, so the note exists by the time their attention returns to the code.

## Exit criteria (binary)

- [ ] `tinker capture "<text>"` writes a note with auto-attached context (cwd, git branch).
- [ ] `tinker capture` (no arg) opens `$EDITOR` for multi-line input.
- [ ] `tinker recent` lists the last 20 notes for the current directory.
- [ ] Cross-platform install works on macOS, Linux, Windows.
- [ ] Test suite covers the capture/recent flow; CI green on all 3 OS.

## KPIs

- **Capture latency:** < 300ms p95 on a 2020-era laptop.
- **Crash recovery:** zero notes lost across 100 simulated crashes (test).

## Out of scope

- **Search.** That's a separate epic (E02 — not yet chartered).
- **Sync.** Phase 2+ pillar.
- **GUI.** `tinker` is CLI-only by strategy.

## Item roster

See [BACKLOG.md](BACKLOG.md) for active items; [ARCHIVE.md](ARCHIVE.md) for completed.
