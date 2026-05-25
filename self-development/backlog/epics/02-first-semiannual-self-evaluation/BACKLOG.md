# E02 — First semi-annual methodology self-evaluation pass — Active Backlog

_Items currently in scope for this epic. See [charter](README.md) for exit criteria._

## Summary

| ID      | Title                                                              | Priority | Effort | Status         |
|---------|--------------------------------------------------------------------|----------|--------|----------------|
| BL-0006 | Create `evaluations/` folder + first eval report skeleton          | P1       | XS     | to-be-tested   |
| BL-0007 | Cross-AI cold-read of methodology docs 00–05 (planning + locks)    | P1       | M      | to-be-tested   |
| BL-0008 | Cross-AI cold-read of methodology docs 06–11 (disciplines + ops)   | P1       | M      | backlog        |
| BL-0009 | Classify surfaced gaps + assign dispositions + patch tiers         | P1       | M      | backlog        |
| BL-0010 | Finalize eval report + close epic                                  | P1       | S      | backlog        |

---

### BL-0006 — Create `evaluations/` folder + first eval report skeleton

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E02-first-semiannual-self-evaluation |
| Pillar   | P3                                 |
| Priority | P1                                 |
| Effort   | XS                                 |
| Status   | to-be-tested                       |
| Test     | not-tested                         |
| Deps     | —                                  |
| Lock     | —                                  |

**Run-1 execution note:** Work completed by the autonomous loop's first run on 2026-05-25. Three deliverables created (folder + 2 files); no methodology docs read; cross-AI validation gate is next. Awaiting maintainer review before flip to `Status: done` and move to `ARCHIVE.md`.

**Why / Description:** The methodology added a [semi-annual self-evaluation cadence](../../../../methodology/07_definition_of_done.md#methodology-self-evaluation-semi-annual) in v1.6.0; that cadence has no operating surface yet. This item creates the folder + skeleton that subsequent items (BL-0007, BL-0008, BL-0009) populate with findings. **This is skeleton-only work — no findings data is recorded in this item; no methodology docs are read; the cold-read happens in BL-0007/0008.** Pillar (secondary): P2 — Doc clarity.

**Approach:**

1. Create directory `self-development/evaluations/`.
2. Write `self-development/evaluations/2026-05-first-pass.md` as an *empty skeleton* with section headings only — no content yet:
   - `# 2026 first semi-annual self-evaluation pass`
   - `## Metadata` (placeholders for date, methodology version at eval, reviewer model + session, scope)
   - `## Cold-read findings (docs 00–05)` (empty; populated by BL-0007)
   - `## Cold-read findings (docs 06–11)` (empty; populated by BL-0008)
   - `## Classification + dispositions` (empty; populated by BL-0009)
   - `## Summary statistics` (empty; populated by BL-0010)
   - `## Next eval date` (empty; recorded by BL-0010)
3. Write `self-development/evaluations/README.md` (≤30 lines): one-paragraph intro that this folder holds eval reports; cadence reference; pointer to the methodology section that defines the cadence.
4. **Do NOT begin filling findings.** BL-0007 + BL-0008 are the cold-read; this item only prepares the structure.

**Done means:**

- [ ] Folder `self-development/evaluations/` exists.
- [ ] `self-development/evaluations/2026-05-first-pass.md` exists with all six section headings listed in the Approach (and no findings content under any heading).
- [ ] `self-development/evaluations/README.md` exists, is ≤30 lines, and references `methodology/07_definition_of_done.md` for the cadence.
- [ ] No methodology doc was read or analyzed during this item's execution (that's BL-0007 + BL-0008's scope).
- [ ] Item moved from `BACKLOG.md` to `ARCHIVE.md` after cross-AI validation passes.

**Files (probable):**

- `self-development/evaluations/2026-05-first-pass.md` (new)
- `self-development/evaluations/README.md` (new)

---

### BL-0007 — Cross-AI cold-read of methodology docs 00–05 (planning + locks)

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E02-first-semiannual-self-evaluation |
| Pillar   | P3                                 |
| Priority | P1                                 |
| Effort   | M                                  |
| Status   | to-be-tested                       |
| Test     | pass                               |
| Deps     | BL-0006                            |
| Lock     | —                                  |

**Run-2 execution note:** Cold-read completed by a fresh Opus 4.7 general-purpose agent on 2026-05-25 (no prior turns referencing this project). 23–25 findings landed across all six docs (3 stale / 12 unclear / 10 inconsistent per Opus's count; 23 distinct bullets per Sonnet's recount — discrepancy is bullet-counting only, every doc has substantive findings). Findings + Metadata block now populated in `self-development/evaluations/2026-05-first-pass.md`.

**Cross-AI validation (2026-05-25):** Fresh Sonnet 4.6 Explore agent (different model family, no prior context) verified Done-means criteria mechanically: (1) all 6 docs have finding entries — PASS; (2) file:line citations present and accurate — PASS (5 sampled, all grounded); (3) fresh session documented in Metadata — PASS. Spot-checked 3 random findings; all GROUNDED in cited text. Validation report logged in this session's loop-notes for the maintainer. Awaiting maintainer review before flip to `Status: done` and move to `ARCHIVE.md`.

**Why / Description:** Run a **fresh AI session** (no prior conversation context referencing the methodology project) over `methodology/00_README.md` through `methodology/05_locks_and_parallel_work.md` and surface drift between the docs and how the project / adopters actually use them. Findings get appended (not overwritten) to the skeleton from BL-0006. Pillar (secondary): P2 — Doc clarity.

**Approach:**

1. Spawn a fresh AI session (definition: new chat or new agent session with no turns referencing this project; ideally a different model family than was used to author the docs).
2. Session reads the six docs in order: 00, 01, 02, 03, 04, 05.
3. For each doc, session reports three categories of finding:
   - **Stale** — rules no longer in practice; claims that don't hold; references that resolved differently than expected.
   - **Unclear** — passages a fresh contributor wouldn't be able to apply without re-reading.
   - **Inconsistent** — cross-doc contradictions vs. what other docs in the methodology say.
4. Findings landed into `self-development/evaluations/2026-05-first-pass.md` under the "Cold-read findings (docs 00–05)" heading. Each finding cites file:line where applicable.
5. Each doc gets at least one finding entry (even "no issues found" is recorded — to prove the doc was actually read).

**Done means:**

- [ ] All six docs (00, 01, 02, 03, 04, 05) have at least one finding entry under "Cold-read findings (docs 00–05)".
- [ ] Each finding cites file:line where applicable.
- [ ] The session that produced the findings had no prior turns referencing the methodology project (documented in the eval report's Metadata section).
- [ ] Item moved from `BACKLOG.md` to `ARCHIVE.md` after cross-AI validation passes.

**Files (probable):**

- `self-development/evaluations/2026-05-first-pass.md` (append findings)

---

### BL-0008 — Cross-AI cold-read of methodology docs 06–11 (disciplines + ops + roles)

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E02-first-semiannual-self-evaluation |
| Pillar   | P3                                 |
| Priority | P1                                 |
| Effort   | M                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | BL-0006, BL-0007                   |
| Lock     | —                                  |

**Why / Description:** Same as BL-0007 applied to `methodology/06_working_principles.md` through `methodology/11_human_roles.md`. **Sequential to BL-0007 (not parallel):** BL-0008's verification asks for cross-doc inconsistencies between this batch and BL-0007's batch, which requires BL-0007's findings to be in the report first. Pillar (secondary): P2 — Doc clarity.

**Approach:**

1. Spawn a fresh AI session (per the "fresh session" definition in BL-0007).
2. The session reads BL-0007's findings first (to know what was already surfaced in docs 00–05), then reads docs 06, 07, 08, 09, 10, 11 in order.
3. Same report shape: stale / unclear / inconsistent per doc.
4. Findings landed into `self-development/evaluations/2026-05-first-pass.md` under "Cold-read findings (docs 06–11)".
5. Cross-doc inconsistencies between this batch and BL-0007's batch are explicitly flagged as a sub-list under the docs-06–11 heading.

**Done means:**

- [ ] All six docs (06, 07, 08, 09, 10, 11) have at least one finding entry under "Cold-read findings (docs 06–11)".
- [ ] Each finding cites file:line where applicable.
- [ ] Cross-doc inconsistencies between the two batches are explicitly flagged.
- [ ] The session that produced the findings was fresh (per definition; recorded in the eval report's Metadata).
- [ ] Item moved from `BACKLOG.md` to `ARCHIVE.md` after cross-AI validation passes.

**Files (probable):**

- `self-development/evaluations/2026-05-first-pass.md` (append findings)

---

### BL-0009 — Classify surfaced gaps + assign dispositions + patch tiers

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E02-first-semiannual-self-evaluation |
| Pillar   | P3                                 |
| Priority | P1                                 |
| Effort   | M                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | BL-0007, BL-0008                   |
| Lock     | —                                  |

**Why / Description:** Read the combined findings from BL-0007 + BL-0008, classify each gap on **two axes** — (a) the practice/docs framework from [`methodology/07_definition_of_done.md "Methodology self-evaluation"`](../../../../methodology/07_definition_of_done.md#methodology-self-evaluation-semi-annual), and (b) the patch-tier from [`templates/AUTONOMOUS_LOOP.md` "Tiered autonomy"](../../../../templates/AUTONOMOUS_LOOP.md#tiered-autonomy-for-authoritative-artifacts) — and assign a disposition. Effort raised from S to M to reflect the additional tier-classification work and the ~50-finding corpus (BL-0007 produced 23–25; BL-0008 expected to produce a similar count).

**Approach:**

1. Read all findings under both "Cold-read findings" sections of the eval report.
2. For each finding, **classify on two axes:**
   - **Practice/docs axis:** `practice-wrong` / `docs-wrong` / `both`.
   - **Patch tier axis:** `T0` (cosmetic — typos, dead anchors), `T1` (surgical — stale examples, single-paragraph clarifications), `T2` (substantive — rule rewording, new constraints), `T3` (architectural — new/removed docs, discipline restructure).
3. For each classification, **assign a disposition** consistent with the tier:
   - `T0` or `T1` + `docs-wrong` → patch branch (`methodology-patch/YYYY-MM-DD-NN`) with edit + CHANGELOG + cross-AI diff-verification; maintainer fast-forwards.
   - `T2` + `docs-wrong` → file as item in appropriate follow-up epic; maintainer authors the change.
   - `T3` + `docs-wrong` → flag in `loop-notes/` for maintainer; do not draft.
   - `practice-wrong` (any tier) → file as a memory entry candidate; surface to maintainer; no methodology edit.
   - `both` (any tier) → file an item to update both, sequenced docs-first; tier governs how the docs side is handled.
4. **Tier classification must itself be cross-AI verified** per the escalate-on-doubt rule: if the implementing session calls a finding T1 but the validator calls it T2, T2 wins.
5. Output a "Classification + dispositions" table in the eval report with columns: Finding ID, Practice/docs, Tier, Disposition, Target branch / item / loop-note.
6. **Do NOT execute T0/T1 patches in this item** — BL-0009 is classification + planning. The patches themselves are separate follow-up items (or, if trivial in number, a single batch item) so each patch branch gets its own cross-AI diff-verification gate.

**Done means:**

- [ ] Every finding from BL-0007 + BL-0008 has a practice/docs classification.
- [ ] Every finding has a patch tier (T0/T1/T2/T3).
- [ ] Tier classifications cross-AI verified by a fresh session (escalate-on-doubt rule applied).
- [ ] Every finding has a disposition consistent with its tier.
- [ ] No `both` gaps lack an open item (per E02 charter exit criterion 5).
- [ ] The eval report's "Classification + dispositions" table is populated with both axes.
- [ ] A separate sub-list enumerates the T0/T1 findings that BL-0010 (or follow-up items) will materialize as patch branches.
- [ ] Item moved from `BACKLOG.md` to `ARCHIVE.md` after cross-AI validation passes.

**Files (probable):**

- `self-development/evaluations/2026-05-first-pass.md` (populate Classification + dispositions table on both axes)

---

### BL-0010 — Finalize eval report + close epic

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E02-first-semiannual-self-evaluation |
| Pillar   | P3                                 |
| Priority | P1                                 |
| Effort   | S                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | BL-0009                            |
| Lock     | —                                  |

**Why / Description:** Complete the eval report (summary statistics, next eval date, maintainer signoff), ship any patch releases for `docs-wrong` gaps marked for immediate fix, and bring the epic to `to-be-tested` for maintainer approval. **The epic's final `Status: done` flip happens after maintainer review** — this item completes the *work* but does not itself close the epic autonomously.

**Approach:**

1. Populate the eval report's "Summary statistics" section: counts of findings by classification, counts by disposition, time-to-close estimate.
2. Record next semi-annual eval target date (~2026-11-25 or adjusted based on context).
3. Add maintainer signoff line to the report (left blank for maintainer to complete).
4. For each disposition flagged "patch release immediately": prepare the patch release as a separate commit chain (does not block this item's close).
5. Bring this item to `Status: to-be-tested`, halt, surface for cross-AI review + maintainer approval.

**Done means:**

- [ ] Summary statistics section is populated.
- [ ] Next eval date recorded (~6 months out).
- [ ] Maintainer signoff line present (awaiting signature).
- [ ] All "patch release immediately" dispositions have prepared changes (committed if maintainer authorizes).
- [ ] Epic E02 charter exit criteria are all checked.
- [ ] Item is at `Status: to-be-tested`, awaiting maintainer review for the epic-closure flip.
- [ ] Item moved from `BACKLOG.md` to `ARCHIVE.md` only after maintainer approves the epic closure.

**Files (probable):**

- `self-development/evaluations/2026-05-first-pass.md` (final population)
- `self-development/backlog/EPICS.md` (rollup update on epic close)
- `CHANGELOG.md` (epic closure entry)
