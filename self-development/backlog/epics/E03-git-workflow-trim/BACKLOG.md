# E03 — Trim or split `09_git_workflow.md` — Active Backlog

_Items currently in scope for this epic. See [charter](README.md) for exit criteria._

**Epic status (as of v1.12.0):** `planned` — E03 is not active. Items below are visible but **not pickable by the autonomous loop** until E02 closes and E03 is promoted to active. WIP cap = 1 per maintainer-deliberate choice (see backlog [README.md](../../README.md) "WIP cap note").

## Summary

| ID      | Title                                                              | Priority | Effort | Status      |
|---------|--------------------------------------------------------------------|----------|--------|-------------|
| BL-0011 | Analyze 09_git_workflow.md structure + decide trim-vs-split        | P2       | S      | backlog     |
| BL-0012 | Execute trim or split per BL-0011 decision                         | P2       | L      | backlog     |
| BL-0013 | Update inbound cross-references + run link scan                    | P2       | S      | backlog     |
| BL-0014 | Author closure note with clarity assessment + close epic           | P2       | S      | backlog     |

---

### BL-0011 — Analyze 09_git_workflow.md structure + decide trim-vs-split

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E03-git-workflow-trim              |
| Pillar   | P2                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** Read `methodology/09_git_workflow.md` (986 lines, longest methodology doc, approaching the 1,050-line soft cap), score each top-level section for trim potential vs. split coherence, and decide whether to trim (target: under 800 lines) or split (target: 2–3 docs each under 700 lines). The decision is documented as a separate file so BL-0012 has a clear scope.

**Approach:**

1. Read `methodology/09_git_workflow.md` in full.
2. For each top-level section (24 sections identified): note approximate line count and topic group.
3. Score trim opportunities: sections that could lose 30%+ without losing meaning.
4. Score split opportunities: natural section groupings + cross-reference density (low density = clean split point).
5. Document the decision (trim, split, or hybrid) in `self-development/evaluations/2026-05-09-git-workflow-decision.md` with reasoning.

**Done means:**

- [ ] Decision document exists at `self-development/evaluations/2026-05-09-git-workflow-decision.md`.
- [ ] Document lists both trim and split options with pros/cons.
- [ ] Document commits to one path with explicit reasoning.
- [ ] If split chosen: target sub-doc filenames named.
- [ ] Item moved from `BACKLOG.md` to `ARCHIVE.md` after cross-AI validation passes.

**Files (probable):**

- `self-development/evaluations/2026-05-09-git-workflow-decision.md` (new)

---

### BL-0012 — Execute trim or split per BL-0011 decision

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E03-git-workflow-trim              |
| Pillar   | P2                                 |
| Priority | P2                                 |
| Effort   | L                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | BL-0011                            |
| Lock     | —                                  |

**Why / Description:** Execute the trim-vs-split decision from BL-0011. Result: either `methodology/09_git_workflow.md` is under 800 lines after trimming, OR it has been split into 2–3 focused docs each under 700 lines. **Scope-bound:** if mid-execution the work appears to require more than L effort (5 days), halt and surface for splitting this item into smaller follow-ups per the methodology's [scope-creep recovery](../../../../methodology/04_backlog_items.md#scope-creep-mid-task).

**Approach (branches based on BL-0011 decision):**

**If trim:**
1. Identify and execute cuts per BL-0011's analysis (target: 200+ lines removed).
2. Preserve all section *intent*; cut only redundancy, verbose phrasing, over-numbered subsections, and stacked defensive caveats.
3. Each removed paragraph or section logged in BL-0011's decision doc with "removed because X" reasoning.

**If split:**
1. Create split files (e.g., `09a_git_daily_flow.md`, `09b_git_releases.md`, `09c_git_ai_autonomy.md`).
2. Move sections per BL-0011's grouping.
3. Top-level `09_git_workflow.md` becomes an index pointing to splits.
4. Update `methodology/00_README.md` doc index.

**Done means:**

- [ ] If trim: `methodology/09_git_workflow.md` is under 800 lines AND every removed section/paragraph is logged in `2026-05-09-git-workflow-decision.md`.
- [ ] If split: 2–3 sub-docs exist; each is under 700 lines; top-level `09_git_workflow.md` is an index; `methodology/00_README.md` doc index updated.
- [ ] No content silently lost (cross-AI diff review confirms all removals were deliberate).
- [ ] Item moved from `BACKLOG.md` to `ARCHIVE.md` after cross-AI validation passes.

**Files (probable):**

- `methodology/09_git_workflow.md` (modified or split)
- `methodology/09a_*.md`, `methodology/09b_*.md`, `methodology/09c_*.md` (new, if split)
- `methodology/00_README.md` (doc index update if split)
- `self-development/evaluations/2026-05-09-git-workflow-decision.md` (append removal log)

**Notes:** This item touches `methodology/*.md` and thus violates the autonomous-loop **Constraint 1** (never modify abstract methodology docs autonomously). The loop CANNOT execute this item autonomously; it must surface to the maintainer for human-authored execution. This is a known limitation; the loop's role for this item is to *prepare* (BL-0011 decision) and then halt for maintainer handoff.

---

### BL-0013 — Update inbound cross-references + run link scan

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E03-git-workflow-trim              |
| Pillar   | P2                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | BL-0012                            |
| Lock     | —                                  |

**Why / Description:** Catalog all inbound references to `methodology/09_git_workflow.md` (or sections within), update each to reflect the trim/split, and confirm no new broken links via a repo-wide link scan. This item is the cleanup pass after BL-0012's substantive change.

**Approach:**

1. Grep the repo for `09_git_workflow.md` references — methodology docs, README, brief docs, strategy docs, pillar docs, backlog charters, items.
2. For each reference: if trimmed, confirm the target section still exists; if split, redirect to the new sub-doc.
3. Run the PowerShell link-scan script over the repo's `.md` files.
4. Fix any new broken links surfaced.

**Done means:**

- [ ] All inbound references to `methodology/09_git_workflow.md` resolve.
- [ ] Link scan reports zero new broken links from this change.
- [ ] Item moved from `BACKLOG.md` to `ARCHIVE.md` after cross-AI validation passes.

**Files (probable):**

- Various inbound-reference files (cataloged during execution)

---

### BL-0014 — Author closure note with clarity assessment + close epic

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E03-git-workflow-trim              |
| Pillar   | P2                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | BL-0012, BL-0013                   |
| Lock     | —                                  |

**Why / Description:** Author the closure note required by E03's exit criteria (clarity assessment comparing post-change to v1.6.0 baseline), then bring the epic to `to-be-tested` for maintainer-approved closure. **The epic's final `Status: done` flip happens after maintainer review** — this item completes the *work* but does not autonomously close the epic.

**Approach:**

1. Compare post-change doc(s) to the v1.6.0 baseline: total line count, section count, longest unbroken stretch of prose, subjective scannability.
2. Append closure note to `self-development/evaluations/2026-05-09-git-workflow-decision.md`.
3. Update `CHANGELOG.md` with E03 closure entry.
4. Verify all charter exit criteria are checked.
5. Bring item to `Status: to-be-tested`; halt for maintainer approval.

**Done means:**

- [ ] Closure note exists with line-count, section-count, scannability metrics.
- [ ] `CHANGELOG.md` has E03 closure entry.
- [ ] Charter exit criteria all checked.
- [ ] Item at `Status: to-be-tested`, awaiting maintainer review.
- [ ] After maintainer approval: ARCHIVE.md contains BL-0011 through BL-0014; EPICS.md rollup reflects E03 `done`.

**Files (probable):**

- `self-development/evaluations/2026-05-09-git-workflow-decision.md` (closure note)
- `CHANGELOG.md` (E03 closure entry)
- `self-development/backlog/EPICS.md` (rollup)
- `self-development/backlog/epics/E03-git-workflow-trim/ARCHIVE.md` (new on close)
