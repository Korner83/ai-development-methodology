# E02 — First semi-annual methodology self-evaluation pass — Active Backlog

_Items currently in scope for this epic. See [charter](README.md) for exit criteria._

## Summary

| ID      | Title                                                              | Priority | Effort | Status      |
|---------|--------------------------------------------------------------------|----------|--------|-------------|
| BL-0006 | Create `evaluations/` folder + first eval report template          | P1       | XS     | ready       |
| BL-0007 | Cross-AI cold-read of methodology docs 00–05 (planning + locks)    | P1       | M      | backlog     |
| BL-0008 | Cross-AI cold-read of methodology docs 06–11 (disciplines + ops)   | P1       | M      | backlog     |
| BL-0009 | Classify surfaced gaps + assign dispositions                       | P1       | S      | backlog     |
| BL-0010 | Finalize eval report + close epic                                  | P1       | S      | backlog     |

---

### BL-0006 — Create `evaluations/` folder + first eval report template

**Pillar:** P3 — Doc currency
**Priority:** P1
**Effort:** XS
**Status:** ready
**Test:** not-tested
**Lock:** —
**Deps:** —

**Goal:** Create the `self-development/evaluations/` folder and the first eval report template so subsequent items have a structured place to land findings.

**Plan:**

1. Create `self-development/evaluations/` directory.
2. Write `self-development/evaluations/2026-05-first-pass.md` skeleton with sections:
   - Metadata (date, methodology version at eval, reviewer model + session, scope).
   - Findings per doc (table: doc path / gap class / disposition).
   - Summary statistics (gaps surfaced, classified, addressed).
   - Next eval date (target: ~6 months out).
3. Write `self-development/evaluations/README.md` (1-paragraph intro: this folder holds eval reports; cadence is semi-annual per `methodology/07_definition_of_done.md`).

**Verification:** Folder exists; template file exists with all sections; README.md exists with cadence reference.

---

### BL-0007 — Cross-AI cold-read of methodology docs 00–05 (planning + locks)

**Pillar:** P3 — Doc currency (secondary: P2 — Doc clarity)
**Priority:** P1
**Effort:** M
**Status:** backlog
**Test:** not-tested
**Lock:** —
**Deps:** BL-0006

**Goal:** A fresh AI session reads `methodology/00_README.md` through `methodology/05_locks_and_parallel_work.md` cold (no prior context) and surfaces drift between docs and how the project / adopters actually use them.

**Plan:**

1. Spawn an Explore agent with no prior session context.
2. Agent reads the six docs in order: 00, 01, 02, 03, 04, 05.
3. For each doc, agent reports: (a) anything that reads as stale (rules no longer in practice, claims that don't hold, references that resolved differently than expected); (b) anything unclear; (c) any cross-doc inconsistencies vs. what other docs say.
4. Findings written to `self-development/evaluations/2026-05-first-pass.md` under a "Cold-read findings (docs 00–05)" section.

**Verification:** Each of the 6 docs has at least one finding entry (even "no issues found" counts); findings reference specific file:line where applicable.

---

### BL-0008 — Cross-AI cold-read of methodology docs 06–11 (disciplines + ops + roles)

**Pillar:** P3 — Doc currency (secondary: P2 — Doc clarity)
**Priority:** P1
**Effort:** M
**Status:** backlog
**Test:** not-tested
**Lock:** —
**Deps:** BL-0006

**Goal:** A fresh AI session reads `methodology/06_working_principles.md` through `methodology/11_human_roles.md` cold and surfaces drift.

**Plan:**

1. Spawn an Explore agent with no prior session context (separate from BL-0007 to keep each batch reviewable independently).
2. Agent reads the six docs in order: 06, 07, 08, 09, 10, 11.
3. Same report shape as BL-0007: stale / unclear / inconsistent.
4. Findings appended to `self-development/evaluations/2026-05-first-pass.md` under a "Cold-read findings (docs 06–11)" section.

**Verification:** Each of the 6 docs has at least one finding entry; cross-doc inconsistencies between this batch and BL-0007's batch are explicitly flagged.

---

### BL-0009 — Classify surfaced gaps + assign dispositions

**Pillar:** P3 — Doc currency
**Priority:** P1
**Effort:** S
**Status:** backlog
**Test:** not-tested
**Lock:** —
**Deps:** BL-0007, BL-0008

**Goal:** Read the combined findings from BL-0007 + BL-0008, classify each gap as "practice is wrong" / "docs are wrong" / "both", and assign a disposition (patch release / file as item / defer to FUTURE.md).

**Plan:**

1. Read all findings in `self-development/evaluations/2026-05-first-pass.md`.
2. For each finding, classify per the methodology's three-way framework (per [`methodology/07_definition_of_done.md "Methodology self-evaluation"`](../../../../methodology/07_definition_of_done.md#methodology-self-evaluation-semi-annual)).
3. For each classification, assign a disposition:
   - "Practice wrong" → file as a memory entry candidate; surface to maintainer; no methodology change.
   - "Docs wrong" → either ship a patch release immediately (if severity warrants) OR file as item in appropriate epic (E02 itself, or follow-up epic).
   - "Both" → file an item to update both; severity-triaged.
4. Update the eval report with classifications + dispositions in a table.

**Verification:** Every finding has a classification; every classification has a disposition; no "both" gaps lack an open item (per E02 exit criterion 5).

---

### BL-0010 — Finalize eval report + close epic

**Pillar:** P3 — Doc currency
**Priority:** P1
**Effort:** S
**Status:** backlog
**Test:** not-tested
**Lock:** —
**Deps:** BL-0009

**Goal:** Finalize the eval report, record the next semi-annual eval date, ship any required patch releases, and close E02.

**Plan:**

1. Finalize `self-development/evaluations/2026-05-first-pass.md`: summary statistics, next eval date (~2026-11-25 or as adjusted), maintainer signoff line.
2. Ship any patch releases for "docs wrong" gaps that warrant immediate fix.
3. Verify all E02 exit criteria in the charter are checked off.
4. Move all 5 BL items (BL-0006 through BL-0010) from `BACKLOG.md` to `ARCHIVE.md`.
5. Update `EPICS.md` rollup: E02 status → `done`, item counts → 0 open / 5 done. WIP cap frees a slot (E04 or E05 can promote).

**Verification:** Charter exit criteria all checked; ARCHIVE.md contains all 5 items; EPICS.md reflects E02 done + WIP cap update.
