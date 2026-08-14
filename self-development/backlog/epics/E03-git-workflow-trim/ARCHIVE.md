# E03 — Git workflow trim — Archive

_Completed items in this epic. All four shipped together in **v1.27.0** (2026-08-14)._

**Outcome:** `methodology/09_git_workflow.md` trimmed **1,026 → 798 lines** (−22%), 24 → 20 sections,
under the charter's 800-line exit criterion. Full analysis, execution log, and clarity assessment:
[`2026-05-09-git-workflow-decision.md`](../../../evaluations/2026-05-09-git-workflow-decision.md).

**Verification (all four items):** repo-wide anchor check across 86 tracked markdown files — zero
broken anchors; 85 inbound references to `09_git_workflow.md` verified. Content-loss check confirmed
every rule, table, and reasoning passage survives; only second tellings were removed.

**Authority note:** BL-0012 touches `methodology/` and is T2/T3 under the tier matrix. It was
executed at the maintainer's explicit direction ("finish and proceed do not stop until all done"),
which is what satisfies the maintainer-authored requirement — the change was human-directed, not
loop-initiated.

---

### BL-0011 — Analyze 09_git_workflow.md structure + decide trim-vs-split

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E03-git-workflow-trim              |
| Pillar   | P2                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | done                               |
| Test     | pass — decision doc exists, costs both options, commits to one with reasoning |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** Score each top-level section of `09_git_workflow.md` for trim potential vs.
split coherence, and decide which path BL-0012 executes.

**Done means:**

- [x] Decision document exists at `self-development/evaluations/2026-05-09-git-workflow-decision.md`.
- [x] Document lists both trim and split options with pros/cons.
- [x] Document commits to one path with explicit reasoning.
- [x] If split chosen: target sub-doc filenames named. *(N/A — trim chosen; the split layout is
      costed in the doc anyway so a future revisit doesn't start cold.)*
- [x] Item archived after validation.

**Resolution:** **Trim chosen.** The measurement drove it: the doc had grown to 1,026 lines (98% of
the soft cap, 40 more than the charter recorded), but its mean section was only ~43 lines — no
section was bloated. Length came from 24 genuine facets of one cohesive topic, which is the profile
that argues *against* splitting. Meanwhile ~120 lines were outright duplication (three appendix
sections restating content given better inline earlier). Splitting would also have spent a T3
restructure, broken the README's "fourteen short docs" identity claim, and scattered anchors across
three files. The split layout is costed in the decision doc for whoever faces this again.

Also corrected a measurement trap for the record: a naive `^## ` scan reports 29 sections; five of
those are template headings **inside code fences**. The real count is 24.

---

### BL-0012 — Execute trim or split per BL-0011 decision

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E03-git-workflow-trim              |
| Pillar   | P2                                 |
| Priority | P2                                 |
| Effort   | L                                  |
| Status   | done                               |
| Test     | pass — 798 lines (<800 criterion); content-loss check clean; every removal logged |
| Deps     | BL-0011                            |
| Lock     | —                                  |

**Why / Description:** Execute the trim decision: bring `09_git_workflow.md` under 800 lines without
losing any rule, table, or reasoning.

**Done means:**

- [x] `methodology/09_git_workflow.md` is under 800 lines (**798**) AND every removed section or
      paragraph is logged in `2026-05-09-git-workflow-decision.md`.
- [x] If split: N/A (trim path).
- [x] No content silently lost — each of the six cuts carries a "where the content still lives"
      entry; spot-checked that `worktree prune`, `filter-branch`, `reset --hard`, `--force-with-lease`,
      `clean -fd`, and the `revert` type all survive.
- [x] Item archived after validation.

**Resolution:** −228 lines (50 insertions, 277 deletions) across six cuts: three whole duplicate
appendices (commit examples, PR body skeleton, worktree command reference), the merge of the
destructive-command list into the affirmative list, a condensed operational-work section, and a
prose-density pass that collapsed second tellings.

The structural win beyond length: **destructive operations now have one home.** Previously an agent
consulted a negative list and an affirmative list that disagreed by omission on six operations; now
a single table answers "may I run this?" with ✓/⚠/✗ for every operation the doc covers.

Deliberate non-removal: the "Common mistakes" table, several rows of which restate rules stated
above. That repetition is the point — it is a corpus-wide convention that restates each rule in
failure form, and it appears in every methodology doc.

---

### BL-0013 — Update inbound cross-references + run link scan

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E03-git-workflow-trim              |
| Pillar   | P2                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | done                               |
| Test     | pass — repo-wide anchor scan across 86 files, zero broken |
| Deps     | BL-0012                            |
| Lock     | —                                  |

**Why / Description:** Catalog inbound references to `09_git_workflow.md`, update those the trim
invalidated, and confirm no new broken links.

**Done means:**

- [x] All inbound references to `methodology/09_git_workflow.md` resolve (85 references checked).
- [x] Link scan reports zero new broken links from this change.
- [x] Item archived after validation.

**Resolution:** Merging two sections renamed one anchor, breaking three inbound links — in
`11_human_roles.md` (the decision-ownership matrix's "pairs with" note) and twice in
`self-development/AUTONOMOUS_LOOP.md` (Constraint 3 and the history-rewrite negative-list row). All
three now point at `#what-ai-agents-can-and-cant-do-in-git--the-operation-table`.

One reference was deliberately **not** updated: `evaluations/2026-05-first-pass.md` cites the
affirmative list by name and line number. It is a dated historical eval; rewriting it would falsify
what that eval actually examined.

---

### BL-0014 — Author closure note with clarity assessment + close epic

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E03-git-workflow-trim              |
| Pillar   | P2                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | done                               |
| Test     | pass — closure note compares post-change to the v1.6.0 baseline on five measures |
| Deps     | BL-0012, BL-0013                   |
| Lock     | —                                  |

**Why / Description:** Author the clarity assessment the charter requires, comparing the trimmed doc
to the v1.6.0 baseline.

**Done means:**

- [x] Closure note exists with line-count, section-count, and scannability metrics.
- [x] `CHANGELOG.md` has the E03 closure entry (v1.27.0).
- [x] Charter exit criteria all checked.
- [x] Items archived; `EPICS.md` rollup reflects E03 `done`.

**Resolution:** The assessment's key finding is that **mean section length stayed flat (~41 → ~40)**
while total length fell 22%. That is the signal that the reduction came from deleting duplicate
sections and collapsing second tellings rather than thinning uniformly — a uniform thinning would
have shown a falling mean and a shrinking longest section. The reference tables that carry the doc's
load are all intact at full size.

Headroom went from 2% to 24% of the soft cap — roughly six releases of runway at this doc's
historical growth rate. Honest caveat recorded: `09` is still the corpus's longest doc, and the
duplication that made this trim easy will not be available next time. The split analysis stands
ready if it recurs.
