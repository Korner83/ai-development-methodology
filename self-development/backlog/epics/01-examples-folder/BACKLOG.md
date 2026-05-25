# E01 — Examples folder — Active Backlog

_Items currently in scope for this epic. See [charter](README.md) for exit criteria._

**Epic status (as of v1.12.0):** `planned` — E01 is not active. Items below are visible but **not pickable by the autonomous loop** until E02 closes and E01 is promoted to active. WIP cap = 1 per maintainer-deliberate choice (see backlog [README.md](../../README.md) "WIP cap note").

## Summary

| ID      | Title                                                          | Priority | Effort | Status      |
|---------|----------------------------------------------------------------|----------|--------|-------------|
| BL-0001 | Create `examples/` folder + README with comparison table       | P2       | XS     | backlog     |
| BL-0002 | Author anonymized example strategy + 2 pillars                 | P2       | M      | backlog     |
| BL-0003 | Author anonymized example epic charter + 5 BL items            | P2       | M      | backlog     |
| BL-0004 | Cross-AI abstract-voice review of examples content             | P2       | S      | backlog     |
| BL-0005 | Link `examples/` from main README + close epic                 | P2       | XS     | backlog     |

---

### BL-0001 — Create `examples/` folder + README with comparison table

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E01-examples-folder                |
| Pillar   | P1                                 |
| Priority | P2                                 |
| Effort   | XS                                 |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** Create the `examples/` folder at the repo root with a README that explains the relationship between `examples/`, abstract `methodology/`, and `self-development/`. This is the foundational item for E01 — subsequent items deposit content into this folder. Pillar (secondary): P6 — Example richness.

**Approach:**

1. Create directory `examples/` at repo root (sibling of `methodology/`, `templates/`, `self-development/`).
2. Write `examples/README.md` containing:
   - One-paragraph intro: this folder shows what an adopter project looks like when it adopts the methodology.
   - A 3-row comparison table: `examples/` (illustrative fictional project) / abstract `methodology/` (the rules) / `self-development/` (the methodology applied to its own development).
   - Pointer back to `methodology/00_README.md`.
   - Methodology version the examples are pinned to.

**Done means:**

- [ ] Directory `examples/` exists at repo root.
- [ ] `examples/README.md` contains a 3-row comparison table.
- [ ] A cross-AI reader correctly maps each artifact type to its purpose after one read of the README.
- [ ] Methodology version is current and noted.
- [ ] Item moved from `BACKLOG.md` to `ARCHIVE.md` after cross-AI validation passes.

**Files (probable):**

- `examples/README.md` (new)

---

### BL-0002 — Author anonymized example strategy + 2 pillars

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E01-examples-folder                |
| Pillar   | P1                                 |
| Priority | P2                                 |
| Effort   | M                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | BL-0001                            |
| Lock     | —                                  |

**Why / Description:** Create a fictional but plausible example project's strategy master plan and 2 pillar files, demonstrating how the methodology's `01_strategy.md` and `02_pillars.md` skeletons are filled in for a real project. Pillar (secondary): P6 — Example richness.

**Approach:**

1. Pick a fictional project that's plausible but generic (e.g., a small SaaS productivity tool, a developer CLI utility, a research-team notebook system). Document the choice in `examples/example-project/README.md`.
2. Author `examples/example-project/strategy/00_master_plan.md` following the methodology's strategy-doc skeleton.
3. Author 2 pillar files (`P1_<area>.md`, `P2_<area>.md`) with dependency relationship + capability shape.
4. All content passes the abstract-voice rule extended to examples: no real project names, no real company references.

**Done means:**

- [ ] `examples/example-project/strategy/00_master_plan.md` exists with all five sections from `01_strategy.md`.
- [ ] 2 pillar files exist using the skeleton from `02_pillars.md`.
- [ ] Cross-AI abstract-voice check passes (see BL-0004).
- [ ] Fictional project doesn't accidentally resemble a real product (sanity check by maintainer).
- [ ] Item moved from `BACKLOG.md` to `ARCHIVE.md` after cross-AI validation passes.

**Files (probable):**

- `examples/example-project/README.md` (new)
- `examples/example-project/strategy/00_master_plan.md` (new)
- `examples/example-project/pillars/P1_<area>.md` (new)
- `examples/example-project/pillars/P2_<area>.md` (new)

---

### BL-0003 — Author anonymized example epic charter + 5 BL items

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E01-examples-folder                |
| Pillar   | P1                                 |
| Priority | P2                                 |
| Effort   | M                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | BL-0002                            |
| Lock     | —                                  |

**Why / Description:** Demonstrate the methodology's `03_epics.md` and `04_backlog_items.md` skeletons by filling in one epic charter and 5 BL items for the example project from BL-0002. Pillar (secondary): P6 — Example richness.

**Approach:**

1. Charter one epic at `examples/example-project/backlog/epics/01-<slug>/README.md` per `03_epics.md`.
2. Populate that epic's `BACKLOG.md` with 5 BL-#### items in the **table-form frontmatter** required by `04_backlog_items.md` (lines 91–116).
3. Include 1 item demonstrating P1 priority, 1 item with `Status: blocked` + `Blocker:` line, 1 item with `Status: done` + `Test: pass`.
4. Include `EPICS.md` rollup at `examples/example-project/backlog/EPICS.md`.

**Done means:**

- [ ] Epic charter has all sections from `03_epics.md`.
- [ ] All 5 items use the **table-form frontmatter** per `04_backlog_items.md` lines 91–106 (not the bold-label shorthand).
- [ ] Each item has body sections: `**Why / Description:**`, `**Approach:**` (where multi-step), `**Done means:**` (checkboxes), `**Files (probable):**`.
- [ ] The `done` item demonstrates the hard rule (`Status: done` requires `Test: pass`).
- [ ] The `blocked` item demonstrates the `HUMAN_NEEDED.md` candidate pattern.
- [ ] Item moved from `BACKLOG.md` to `ARCHIVE.md` after cross-AI validation passes.

**Files (probable):**

- `examples/example-project/backlog/epics/01-<slug>/README.md` (new)
- `examples/example-project/backlog/epics/01-<slug>/BACKLOG.md` (new)
- `examples/example-project/backlog/EPICS.md` (new)

---

### BL-0004 — Cross-AI abstract-voice review of examples content

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E01-examples-folder                |
| Pillar   | P1                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | BL-0002, BL-0003                   |
| Lock     | —                                  |

**Why / Description:** A fresh AI session reviews all `examples/` content to verify no abstract-voice violations: no real project names, no real company references, no specific framework names beyond methodology's accepted examples, no domain jargon revealing a source project.

**Approach:**

1. Spawn a fresh AI session with no prior context.
2. Session reads all files under `examples/` and reports potential violations with file:line specificity.
3. Apply fixes (rewrite or remove); re-run review if substantial changes.

**Done means:**

- [ ] Cross-AI report returns "no violations found" OR all flagged issues have been addressed.
- [ ] The session that produced the report was fresh (per BL-0007's "fresh session" definition).
- [ ] Item moved from `BACKLOG.md` to `ARCHIVE.md` after cross-AI validation passes.

**Files (probable):**

- (read-only; potentially edits to `examples/**` if violations found)

---

### BL-0005 — Link `examples/` from main README + close epic

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E01-examples-folder                |
| Pillar   | P1                                 |
| Priority | P2                                 |
| Effort   | XS                                 |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | BL-0001, BL-0002, BL-0003, BL-0004 |
| Lock     | —                                  |

**Why / Description:** Update the main README's "What's in the repo" tree to include `examples/`, then bring the epic to `to-be-tested` for maintainer-approved closure. **The epic's final `Status: done` flip happens after maintainer review** — this item completes the *work* but does not autonomously close the epic.

**Approach:**

1. Update `README.md` tree to show `examples/` alongside `methodology/`, `templates/`, `self-development/`.
2. Update `CHANGELOG.md` with E01 closure entry.
3. Verify all charter exit criteria are checked.
4. Bring item to `Status: to-be-tested`; halt for maintainer approval before flipping items to `done` and the epic to `done`.
5. After maintainer approval: move all 5 items from `BACKLOG.md` to `ARCHIVE.md`; update `EPICS.md` rollup.

**Done means:**

- [ ] `README.md` tree includes `examples/`.
- [ ] `CHANGELOG.md` has E01 closure entry.
- [ ] Charter exit criteria all checked.
- [ ] Item at `Status: to-be-tested`, awaiting maintainer review.
- [ ] After maintainer approval: ARCHIVE.md contains all 5 items; EPICS.md rollup reflects E01 `done`.

**Files (probable):**

- `README.md` (tree update)
- `CHANGELOG.md` (closure entry)
- `self-development/backlog/EPICS.md` (rollup)
- `self-development/backlog/epics/01-examples-folder/ARCHIVE.md` (new on close)
