# E03 — Trim or split `09_git_workflow.md` — Active Backlog

_Items currently in scope for this epic. See [charter](README.md) for exit criteria._

## Summary

| ID      | Title                                                              | Priority | Effort | Status      |
|---------|--------------------------------------------------------------------|----------|--------|-------------|
| BL-0011 | Analyze 09_git_workflow.md structure + decide trim-vs-split        | P2       | S      | ready       |
| BL-0012 | Execute trim or split per BL-0011 decision                         | P2       | L      | backlog     |
| BL-0013 | Update inbound cross-references + run link scan                    | P2       | S      | backlog     |
| BL-0014 | Author closure note with clarity assessment + close epic           | P2       | S      | backlog     |

---

### BL-0011 — Analyze 09_git_workflow.md structure + decide trim-vs-split

**Pillar:** P2 — Doc clarity
**Priority:** P2
**Effort:** S
**Status:** ready
**Test:** not-tested
**Lock:** —
**Deps:** —

**Goal:** Read the current `methodology/09_git_workflow.md` (986 lines) carefully, identify natural split points and trim candidates, and decide whether to trim (target: under 800 lines) or split (target: 2–3 docs each under 700 lines).

**Plan:**

1. Read `methodology/09_git_workflow.md` in full.
2. List the top-level sections (already known from prior grep): branch protection / naming / commit cadence / commit message convention / lock-file management / PR discipline / squash-merge / pre-commit hooks / never amend / worktrees / destructive commands / AI agent autonomy / production deploys / release tagging / hot-fix / conflict resolution / audit trail / PR body skeleton / conventional commit examples / worktree command reference / operational work / connections / common mistakes / authority.
3. For each section, note approximate line count and topic group:
   - **Daily flow:** branch protection, naming, commit cadence, commit messages, lock-file management, PR discipline, squash/merge, pre-commit hooks, never amend, conflict resolution, audit trail.
   - **Releases + hot-fixes:** release tagging + hot-fix workflow.
   - **AI-agent operations:** worktrees, destructive commands, AI agent autonomy, production deploys.
   - **Operational work:** operational work section.
   - **Reference appendices:** PR body skeleton, conventional commit examples, worktree command reference.
4. Score trim opportunities: sections that could lose ~30%+ without losing meaning.
5. Score split opportunities: natural section groupings + cross-reference density (low density = clean split point).
6. Document decision (trim, split, or hybrid) in `self-development/evaluations/2026-05-09-git-workflow-decision.md` with reasoning.

**Verification:** Decision document exists; lists both options considered with pros/cons; commits to one path with explicit reasoning.

---

### BL-0012 — Execute trim or split per BL-0011 decision

**Pillar:** P2 — Doc clarity
**Priority:** P2
**Effort:** L
**Status:** backlog
**Test:** not-tested
**Lock:** —
**Deps:** BL-0011

**Goal:** Execute the trim-vs-split decision from BL-0011. Result: either `methodology/09_git_workflow.md` is under 800 lines after trimming, OR it has been split into 2–3 focused docs each under 700 lines.

**Plan:**

This item branches based on BL-0011's decision:

**If trim:**
1. Identify and execute cuts per BL-0011's analysis (target: 200+ lines removed).
2. Preserve all section *intent*; cut only redundancy, verbose phrasing, over-numbered sub-subsections, and stacked defensive caveats.
3. Each removed paragraph or section logged in BL-0011's decision doc with "removed because X" reasoning (so it's not silent loss).

**If split:**
1. Identify split files (e.g., `09a_git_daily_flow.md`, `09b_git_releases.md`, `09c_git_ai_autonomy.md`).
2. Move sections per BL-0011's grouping.
3. Top-level `09_git_workflow.md` becomes an index pointing to the splits.
4. Update `methodology/00_README.md` doc index to reflect new files.
5. Each subdoc has its own "How this connects" + "Common mistakes" + "Authority" sections (or shared if applicable).

**Verification:** Per BL-0011 decision: target line counts met; no content silently lost (cross-AI diff review confirms all removed material was deliberate); methodology doc count remains 12 if trimmed, 13–14 if split.

---

### BL-0013 — Update inbound cross-references + run link scan

**Pillar:** P2 — Doc clarity
**Priority:** P2
**Effort:** S
**Status:** backlog
**Test:** not-tested
**Lock:** —
**Deps:** BL-0012

**Goal:** Catalog all inbound references to `methodology/09_git_workflow.md` (or sections within), update each to reflect the trim/split, and confirm no new broken links via a repo-wide link scan.

**Plan:**

1. Grep the repo for `09_git_workflow.md` references — methodology docs, README, brief docs, strategy docs, pillar docs, backlog charters, items.
2. For each reference:
   - If trimmed: confirm the target section still exists; update anchor if section slug changed.
   - If split: redirect to the new subdoc.
3. Run a PowerShell link-scan script (per the pattern used in v1.3.1 honesty pass and v1.7.0 brief verification) over the entire repo's .md files.
4. Fix any new broken links surfaced.

**Verification:** Link scan reports zero new broken links; all inbound references resolve.

---

### BL-0014 — Author closure note with clarity assessment + close epic

**Pillar:** P2 — Doc clarity
**Priority:** P2
**Effort:** S
**Status:** backlog
**Test:** not-tested
**Lock:** —
**Deps:** BL-0012, BL-0013

**Goal:** Author the closure note required by E03's exit criteria (clarity assessment comparing post-change to v1.6.0 baseline), then close the epic.

**Plan:**

1. Compare post-change doc(s) to the v1.6.0 baseline:
   - Total line count (before: 986; after: target).
   - Section count.
   - Longest unbroken stretch of prose (a quick proxy for scannability).
   - Subjective: is it easier to scan? Easier to find a specific rule?
2. Write closure note at `self-development/evaluations/2026-05-09-git-workflow-decision.md` (appending to BL-0011's decision doc): post-change measurements + clarity assessment.
3. Update CHANGELOG with E03 closure entry (the trim/split is a methodology release: minor if structural, patch if pure trim).
4. Verify all 6 exit criteria in the charter are checked off.
5. Move BL-0011 through BL-0014 from `BACKLOG.md` to `ARCHIVE.md`.
6. Update `EPICS.md` rollup: E03 status → `done`, item counts → 0 open / 4 done. WIP cap frees a slot.

**Verification:** Closure note exists with all metrics; charter exit criteria all checked; ARCHIVE.md updated; EPICS.md reflects E03 done + WIP cap update.
