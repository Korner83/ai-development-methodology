# E10 — External baseline audit remediation — Active Backlog

_Items currently in scope for this epic. See [charter](README.md) for exit criteria._

**Epic status (as of 2026-08-20):** **active, no open items.** All fourteen chartered items are closed —
see [ARCHIVE.md](ARCHIVE.md). Every finding from the external audit is addressed: the Critical, all five
High, and the four Medium. Staged for a single `v1.32.0`.

**Two decisions shaped the shape of it.** A committed integrity checker and any new CI were **declined** —
this repo ships no runnable elements — so F-08 closes as a reproducible written procedure rather than a
control, and the cost is stated in the charter instead of hidden. The **cross-AI gate was removed** from
this epic's exit criteria.

## Summary

| ID | Title | Priority | Effort | Status |
|----|-------|----------|--------|--------|
| — | _(no open items — all fourteen archived)_ | — | — | — |

## What stands between this and closing

The epic stays `active` because two exit criteria are not things a working session can tick:

1. **The release has not happened.** Nothing is committed. The seven version-pin sites still read
   `v1.31.0` and move in the release commit, not before — per the ordering rule this epic itself added.
2. **The closing gate is a fresh cold re-audit** against the final tree, returning no Critical and no
   High. It must be run by a session that did not author these fixes; **this session cannot satisfy it**,
   and claiming otherwise would be the exact defect the epic repaired.

## Two maintainer decisions carried out of the sweep

Recorded in [the convention sweep](../../../evaluations/2026-08-20-convention-sweep.md), not duplicated
here. Neither blocks the release:

- **Retire the house-verbosity setting?** No mechanism, no user, no evidence — but retiring it is a
  removed section and therefore a **MAJOR** bump under this repo's own SemVer table.
- **Should the root `AGENTS.md` carry the context-integrity canary?** The sweep recommends yes: the
  alternative is a repository publishing a safety convention it declined to use, which is the shape of the
  finding it just fixed.
