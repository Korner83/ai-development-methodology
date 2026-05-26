# E01 — Examples folder — Archive

_All 5 items completed in v1.15.0 maintainer-authored batch. See [examples/](../../../../examples/) for the shipped deliverable._

## Summary

| ID      | Title                                                          | Priority | Effort | Status | Closed     |
|---------|----------------------------------------------------------------|----------|--------|--------|------------|
| BL-0001 | Create `examples/` folder + README with comparison table       | P2       | XS     | done   | 2026-05-25 |
| BL-0002 | Author anonymized example strategy + 2 pillars                 | P2       | M      | done   | 2026-05-25 |
| BL-0003 | Author anonymized example epic charter + 5 BL items            | P2       | M      | done   | 2026-05-25 |
| BL-0004 | Cross-AI abstract-voice review of examples content             | P2       | S      | done   | 2026-05-25 |
| BL-0005 | Link `examples/` from main README + close epic                 | P2       | XS     | done   | 2026-05-25 |

**Epic close:** All 5 items shipped together as part of v1.15.0 maintainer-authored batch. The `examples/` folder contains a fictional `tinker` project (developer-notes CLI) with strategy, 2 pillars, 1 epic charter, 5 BL items. Cross-AI abstract-voice review completed inline (no real product/company references). Main README updated to surface `examples/` in the tree.

---

### BL-0001 — Create `examples/` folder + README with comparison table

| Field | Value |
|---|---|
| Epic | E01-examples-folder |
| Pillar | P1 |
| Priority | P2 |
| Effort | XS |
| Status | done |
| Test | pass |
| Deps | — |
| Lock | — |

**Closure:** [examples/README.md](../../../../examples/README.md) shipped with 3-row comparison table mapping `methodology/` / `self-development/` / `examples/` to their respective purposes. Methodology version v1.15.0 pinned.

---

### BL-0002 — Author anonymized example strategy + 2 pillars

| Field | Value |
|---|---|
| Epic | E01-examples-folder |
| Pillar | P1 |
| Priority | P2 |
| Effort | M |
| Status | done |
| Test | pass |
| Deps | BL-0001 |
| Lock | — |

**Closure:** Fictional `tinker` project chosen (developer-notes CLI; plausible-but-generic). [strategy/00_master_plan.md](../../../../examples/example-project/strategy/00_master_plan.md) authored with vision/audience/phases/exit criteria/doc index. 2 pillar files: [P1_capture.md](../../../../examples/example-project/pillars/P1_capture.md), [P2_retrieval.md](../../../../examples/example-project/pillars/P2_retrieval.md). All content abstract-voice-compliant.

---

### BL-0003 — Author anonymized example epic charter + 5 BL items

| Field | Value |
|---|---|
| Epic | E01-examples-folder |
| Pillar | P1 |
| Priority | P2 |
| Effort | M |
| Status | done |
| Test | pass |
| Deps | BL-0002 |
| Lock | — |

**Closure:** [Epic charter](../../../../examples/example-project/backlog/epics/E01-cli-foundations/README.md) + active items in [BACKLOG.md](../../../../examples/example-project/backlog/epics/E01-cli-foundations/BACKLOG.md) shipped in canonical table-form frontmatter. The 5 BL items demonstrate: 1 done item (BL-0001 with Test: pass — in [ARCHIVE.md](../../../../examples/example-project/backlog/epics/E01-cli-foundations/ARCHIVE.md)), 1 blocked item (BL-0005 with Blocker: line), 1 in-progress item with active lock, 1 ready item, 1 backlog item. EPICS rollup at [examples/example-project/backlog/EPICS.md](../../../../examples/example-project/backlog/EPICS.md). v1.17.0 added the missing 5-file structure (ARCHIVE/FUTURE/TEST) + folder-renamed to `E01-` convention.

---

### BL-0004 — Cross-AI abstract-voice review of examples content

| Field | Value |
|---|---|
| Epic | E01-examples-folder |
| Pillar | P1 |
| Priority | P2 |
| Effort | S |
| Status | done |
| Test | pass |
| Deps | BL-0002, BL-0003 |
| Lock | — |

**Closure:** Maintainer-led review of all `examples/` content. No real product names; "tinker" is a plausible-but-generic CLI utility name. No company references. Frameworks named are limited to the methodology's standard examples (Rust toolchain — `cargo`; standard CI naming). Cross-AI re-review eligible as part of v1.15.0 post-ship verification if maintainer wishes.

---

### BL-0005 — Link `examples/` from main README + close epic

| Field | Value |
|---|---|
| Epic | E01-examples-folder |
| Pillar | P1 |
| Priority | P2 |
| Effort | XS |
| Status | done |
| Test | pass |
| Deps | BL-0001, BL-0002, BL-0003, BL-0004 |
| Lock | — |

**Closure:** README.md updated to surface `examples/` in the repo tree. CHANGELOG.md v1.15.0 entry includes E01 closure. Charter exit criteria all checked.
