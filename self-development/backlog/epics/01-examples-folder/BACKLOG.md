# E01 — Examples folder — Active Backlog

_Items currently in scope for this epic. See [charter](README.md) for exit criteria._

## Summary

| ID      | Title                                                          | Priority | Effort | Status      |
|---------|----------------------------------------------------------------|----------|--------|-------------|
| BL-0001 | Create `examples/` folder + README with comparison table       | P2       | XS     | ready       |
| BL-0002 | Author anonymized example strategy + 2 pillars                 | P2       | M      | backlog     |
| BL-0003 | Author anonymized example epic charter + 5 BL items            | P2       | M      | backlog     |
| BL-0004 | Cross-AI abstract-voice review of examples content             | P2       | S      | backlog     |
| BL-0005 | Link `examples/` from main README + close epic                 | P2       | XS     | backlog     |

---

### BL-0001 — Create `examples/` folder + README with comparison table

**Pillar:** P1 — Doc completeness (secondary: P6 — Example richness)
**Priority:** P2
**Effort:** XS
**Status:** ready
**Test:** not-tested
**Lock:** —
**Deps:** —

**Goal:** Create the `examples/` folder at repo root and its README.md so subsequent items have a place to drop content.

**Plan:**

1. Create `examples/` directory at repo root.
2. Write `examples/README.md` containing:
   - One-paragraph intro: this folder shows what an adopter project looks like when it adopts the methodology.
   - A 3-row comparison table mapping `examples/` (illustrative fictional project) / abstract `methodology/` (the rules) / `self-development/` (the methodology applied to its own development).
   - Pointer back to `methodology/00_README.md`.
   - Note that examples are pinned to a methodology version; current version stated.
3. Verify: a cross-AI reader correctly maps the three artifact types after one read (per E01 exit criterion 5).

**Verification:** README exists; comparison table is 3 rows; methodology version is current (v1.9.0 or later).

---

### BL-0002 — Author anonymized example strategy + 2 pillars

**Pillar:** P1 — Doc completeness (secondary: P6 — Example richness)
**Priority:** P2
**Effort:** M
**Status:** backlog
**Test:** not-tested
**Lock:** —
**Deps:** BL-0001

**Goal:** Create a fictional but plausible example project's strategy master plan and 2 pillar files, demonstrating how the methodology's `01_strategy.md` and `02_pillars.md` skeletons are filled in for a real project.

**Plan:**

1. Pick a fictional project that's plausible but generic — e.g., a small SaaS productivity tool, a developer-facing CLI utility, or a research-team notebook system. Document the project choice in `examples/example-project/README.md`.
2. Author `examples/example-project/strategy/00_master_plan.md` following the methodology's strategy-doc skeleton — vision, 3 phases with binary exit criteria, pillar roadmap, doc index.
3. Author 2 pillar files (`P1_<area>.md`, `P2_<area>.md`) showing dependency relationship + capability shape.
4. All content must pass abstract-voice rule extended to examples: no real project names, no real company references, no specific framework names beyond methodology's accepted examples.

**Verification:** Strategy doc has all 5 sections from `01_strategy.md`; pillars use the skeleton from `02_pillars.md`; abstract-voice check passes (cross-AI scan); fictional project doesn't accidentally resemble a real product (sanity check).

---

### BL-0003 — Author anonymized example epic charter + 5 BL items

**Pillar:** P1 — Doc completeness (secondary: P6 — Example richness)
**Priority:** P2
**Effort:** M
**Status:** backlog
**Test:** not-tested
**Lock:** —
**Deps:** BL-0002

**Goal:** Demonstrate the methodology's `03_epics.md` and `04_backlog_items.md` skeletons by filling in one epic charter and 5 BL items for the example project from BL-0002.

**Plan:**

1. Charter one epic at `examples/example-project/backlog/epics/01-<slug>/README.md` — primary pillar from BL-0002, JTBD outcome, binary exit criteria, out-of-scope.
2. Populate that epic's `BACKLOG.md` with 5 BL-#### items, each with full frontmatter (Pillar / Priority / Effort / Status / Test / Lock) and body (goal + plan + verification).
3. Include 1 item demonstrating a P1 priority, 1 item with `Status: blocked` and `Blocker:` line, 1 item with `Status: done` and `Test: pass` (showing the closed state).
4. Include EPICS.md rollup at `examples/example-project/backlog/EPICS.md` showing the one epic.

**Verification:** Epic charter has all sections from `03_epics.md`; items follow `04_backlog_items.md` shape; the "done" item demonstrates the hard rule (`Status: done` requires `Test: pass`); the blocked item demonstrates the `HUMAN_NEEDED.md` candidate pattern.

---

### BL-0004 — Cross-AI abstract-voice review of examples content

**Pillar:** P1 — Doc completeness
**Priority:** P2
**Effort:** S
**Status:** backlog
**Test:** not-tested
**Lock:** —
**Deps:** BL-0002, BL-0003

**Goal:** Run a fresh AI session over all `examples/` content to verify no abstract-voice violations (no real project names, no domain leakage, no accidentally-real company references) before ship.

**Plan:**

1. Spawn a fresh Explore agent with no prior context.
2. Agent reads all files under `examples/` and reports any potential abstract-voice violations: real product names, real company references, specific framework names beyond methodology's accepted examples, domain-specific jargon that gives away a source project.
3. Agent reports findings with file:line specificity.
4. Apply fixes (rewrite or remove offending content); re-run review if substantial changes.

**Verification:** Cross-AI report returns "no violations found" OR all flagged issues have been addressed.

---

### BL-0005 — Link `examples/` from main README + close epic

**Pillar:** P1 — Doc completeness
**Priority:** P2
**Effort:** XS
**Status:** backlog
**Test:** not-tested
**Lock:** —
**Deps:** BL-0001, BL-0002, BL-0003, BL-0004

**Goal:** Update the main README's "What's in the repo" tree to include `examples/`, then close E01 by verifying all exit criteria are met.

**Plan:**

1. Update `README.md` tree to show `examples/` alongside `methodology/`, `templates/`, `self-development/`.
2. Update CHANGELOG with E01 closure entry.
3. Verify all 5 exit criteria in `README.md` (the charter) are checked off.
4. Move all 5 BL items from `BACKLOG.md` to `ARCHIVE.md` (create `ARCHIVE.md` if not exists).
5. Update `EPICS.md` rollup: E01 status → `done`, item counts → 0 open / 5 done.

**Verification:** Charter exit criteria all checked; ARCHIVE.md contains all items; EPICS.md rollup is accurate; main README tree includes examples/.
