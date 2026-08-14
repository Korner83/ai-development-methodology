# E06 — BMAD v6 landscape pass — Archive

_Completed items in this epic. All five shipped together in **v1.25.0** (2026-08-14)._

**Lifecycle note (honest record):** this epic went `planned → done` without an `active` period.
The items were chartered and executed in the same session, at the maintainer's explicit
direction ("proceed with integrating the good things into our solution"). That direction is
what satisfies the charter's **T2 / maintainer-authored** tier requirement — the changes were
human-directed, not loop-initiated. The compressed lifecycle is recorded rather than
back-filled: the WIP cap was never consumed because the epic never sat in `active`.

**Shared verification (all five items):** cross-AI findings-verification in a fresh session on
a different model than the authoring session, run against the full diff with each item's
`Done means:` as the checklist. Result: 16 PASS / 2 FAIL on first pass; both failures
(BL-0016 marker-not-in-templates, BL-0019 budget misattribution) were fixed, along with every
MAJOR and MINOR quality finding, before merge. Anchor integrity verified programmatically
across all new intra-repo links; `04_backlog_items.md` confirmed at 1,018 lines, under the
1,050-line soft cap.

---

### BL-0015 — Spec-as-sole-context handoff (Code Map) for M/L items

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E06-bmad-v6-landscape-pass         |
| Pillar   | P9                                 |
| Priority | P1                                 |
| Effort   | M                                  |
| Status   | done                               |
| Test     | pass — cross-AI findings-verification, fresh session + different model (v1.25.0 diff) |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** An item's body recorded *what* to do, but the codebase knowledge
gathered while planning it lived only in the planning session's conversation — so it died on
handoff, compaction, or a fresh session. Adopted the convention that for M/L-effort items,
planning **drains its investigation into the item body** as a **Code Map** (files to touch
with their roles, existing utilities to reuse, constraints and gotchas), written so *a cold
session can implement from the item alone*, with no conversational context restated at
dispatch.

**Done means:**

- [x] `methodology/04_backlog_items.md` defines the Code Map convention with an include/skip
      rule keyed to Effort, and the cold-handoff test.
- [x] When an M/L item is delegated, the receiving agent's instruction is the item itself —
      the no-re-narration rule is stated where delegation is described.
- [x] Distinction from `ACTIVE_CONTEXT.md` (durable item knowledge vs volatile session state)
      is stated in whichever doc hosts the convention.
- [x] CHANGELOG entry shipped in the same release (v1.25.0); item archived after cross-AI
      validation passed.

**Files (actual):**

- `methodology/04_backlog_items.md` — "The Code Map" section, `Files (probable)` pointer,
  dispatch rule, both item skeletons, worked example upgraded to a Code Map.
- `CHEATSHEET.md` — "Item-body conventions + size budgets".

**Resolution:** Shipped in v1.25.0. Two review findings folded in: the doc's own worked
example (BL-0428, Effort M) still carried a bare `Files (probable)` list and was upgraded to
a Code Map so the doc follows its own rule; and the dispatch rule gained a carve-out for
subagents given a *slice* of an item, which the untouched `05` delegation guidance still
models. Deferred sibling: [BL-0022](FUTURE.md) (per-epic context digest).

---

### BL-0016 — Frozen-intent convention for approved goals / exit criteria

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E06-bmad-v6-landscape-pass         |
| Pillar   | P9                                 |
| Priority | P1                                 |
| Effort   | S                                  |
| Status   | done                               |
| Test     | pass — cross-AI findings-verification, fresh session + different model (v1.25.0 diff) |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** Nothing stopped an agent mid-task from "helpfully" rewording an item's
goal or `Done means:` to match what it actually built — drift that is invisible because the
diff looks like editing, not scope change. Adopted a **frozen-intent** convention: once a
human approves an item's goal + acceptance criteria (or an epic charter's exit criteria),
that region is *human-owned*; if execution reveals it's wrong, the move is **halt and
renegotiate**, never silent amendment.

**Done means:**

- [x] `04` states what approval freezes and the halt-and-renegotiate rule; `06` places it in
      the declared-boundary family with an anti-pattern row.
- [x] Marker syntax chosen and documented; templates carry it.
- [x] Scope-creep recovery cross-links frozen intent (no contradiction between the two).
- [x] CHANGELOG entry shipped in the same release (v1.25.0); item archived after cross-AI
      validation passed.

**Files (actual):**

- `methodology/04_backlog_items.md` — "Frozen intent" section, marker, lock-holder carve-out,
  both recovery flows, item skeleton slot, mistake row.
- `methodology/03_epics.md` — charter Outcome + exit criteria frozen; charter marker.
- `methodology/06_working_principles.md` — "Frozen intent (approved work definitions)" under
  Principle 4; anti-pattern row.
- `templates/CLAUDE.md`, `templates/AGENTS.md` — frozen-intent hard rule.
- `CHEATSHEET.md` — hard-rule line.

**Resolution:** Shipped in v1.25.0. This item **failed its first cross-AI pass on two
counts**, both fixed before merge. (1) The marker was specified as a badge placed "directly
above" the frozen region — but the frozen sections (`Why / Description:` and `Done means:`)
are *non-contiguous*, separated by `Approach:`, so one badge could not fence them; the marker
now sits once below the frontmatter table and *names* the sections it covers. (2) The rule
covered epic charters but `03_epics.md` was untouched and no skeleton carried the marker;
both now do. A third finding moved the section from Principle 3 to **Principle 4**, where the
"goal holds still while you work toward it" logic actually lives.

---

### BL-0017 — Failure-layer triage for review findings

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E06-bmad-v6-landscape-pass         |
| Pillar   | P9                                 |
| Priority | P1                                 |
| Effort   | M                                  |
| Status   | done                               |
| Test     | pass — cross-AI findings-verification, fresh session + different model (v1.25.0 diff) |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** The v1.22 two-stage review ordered *review passes* but every *finding*
still landed in one pile labeled "fix it." Adopted **failure-layer triage**: classify each
finding by the layer the defect entered (intent / plan / code / out-of-scope / invalid) and
route the fix to that layer, processed in cascade order so an upper-layer finding cancels the
code-level findings below it. Names the anti-pattern *never patch code to compensate for a
wrong plan.*

**Done means:**

- [x] `07` Gate 1 contains the five-bucket triage with cascade order and routing per bucket.
- [x] The wrong-plan anti-pattern is named where reviews are described; out-of-scope findings
      route to FUTURE/new items instead of inline fixes.
- [x] Cycle-escape threshold documented (repeat intent/plan findings ⇒ human).
- [x] No contradiction with the two-stage review it extends (cross-AI check confirms).
- [x] CHANGELOG entry shipped in the same release (v1.25.0); item archived after cross-AI
      validation passed.

**Files (actual):**

- `methodology/07_definition_of_done.md` — "Routing findings by failure layer" in Gate 1.
- `methodology/10_testing_and_verification.md` — mistake row.
- `methodology/06_working_principles.md` — anti-pattern row.
- `templates/AUTONOMOUS_LOOP.md` — step 5 routing.
- `CHEATSHEET.md` — routing table.

**Resolution:** Shipped in v1.25.0. Review surfaced a structural gap: the Intent bucket had
*no producing stage* — stage 1 asked only "does the change satisfy the criteria?", which can
never yield an Intent-layer finding. Stage 1 now also asks "are the criteria themselves
right?" The escape hatch was also reconciled with v1.24.0's **attempt cap** (merged from
`main` mid-flight): that cap bounds retrying a *fix* that keeps failing, this bounds
re-deriving from a *definition* that keeps proving wrong.

---

### BL-0018 — Verification-gap review lens + test-actually-ran audit

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E06-bmad-v6-landscape-pass         |
| Pillar   | P9                                 |
| Priority | P1                                 |
| Effort   | S                                  |
| Status   | done                               |
| Test     | pass — cross-AI findings-verification, fresh session + different model (v1.25.0 diff) |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** The cheating-agent defenses audited *test quality* but not *coverage of
the change* or *whether the tests actually executed*. Added three rules: the verification-gap
lens ("if this behavior broke, would any test fail?", output = untested behavior changes, not
bugs); a test that exists but was skipped or filtered counts as missing; and never edit the
expectation to match the code.

**Done means:**

- [x] `07` Gate 2 includes the verification-gap question as a required review lens for
      behavior-changing work.
- [x] `10` states that skipped/filtered/not-run tests count as missing for `Test: pass`, and
      names the expectation-editing anti-pattern.
- [x] Loop template + skill self-check reference the lens.
- [x] CHANGELOG entry shipped in the same release (v1.25.0); item archived after cross-AI
      validation passed.

**Files (actual):**

- `methodology/07_definition_of_done.md` — "The verification-gap question" in Gate 2.
- `methodology/10_testing_and_verification.md` — ran-only rule, verification-gap section,
  cheating-agent defense, two mistake rows.
- `templates/AUTONOMOUS_LOOP.md` — step 3 check.
- `skills/ai-dev-methodology/SKILL.md` — self-check row.
- `CHEATSHEET.md` — verification-gap section.

**Resolution:** Shipped in v1.25.0. Review caught the new text *weakening* an existing rule:
Gate 2 already said absolutely that "skipped tests … are not 'passing'", while the new lens
allowed a gap to be closed with "a documented reason it can't have one" — transitively
permitting a skipped test through the gate. The exception now routes to the already-sanctioned
`manual-verified` + `regression-needed` path instead. A duplication finding also trimmed the
rule from three full statements across two docs down to one canonical statement plus a linked
practical elaboration.

---

### BL-0019 — Size budgets for context artifacts

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E06-bmad-v6-landscape-pass         |
| Pillar   | P9                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | done                               |
| Test     | pass — cross-AI findings-verification, fresh session + different model (v1.25.0 diff) |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** Only one artifact was capped (the instruction file); item bodies, epic
charters, and memory entries had no size guidance, and oversized ones silently degrade every
agent that loads them. Published size targets with a defined "too big ⇒" response for each,
framed as *a context artifact is a liability that must earn its length*.

**Done means:**

- [x] A budgets table exists covering item body, epic charter, instruction file, memory entry
      — each with a target and a "too big ⇒" action.
- [x] Existing numbers in `08` are referenced, not duplicated; no two docs state different
      budgets for the same artifact.
- [x] Split rule routes to the existing scope-creep protocol (no new mechanism).
- [x] CHANGELOG entry shipped in the same release (v1.25.0); item archived after cross-AI
      validation passed.

**Files (actual):**

- `methodology/04_backlog_items.md` — "Size budgets" top-level section.
- `CHEATSHEET.md` — budget defaults line.

**Resolution:** Shipped in v1.25.0. **Failed its first cross-AI pass** on the single-sourcing
criterion: the table asserted an instruction-file cap of "~300 max" and attributed it to `08`,
but `08` says "a few hundred lines" and illustrates with 200 — the 300 actually came from
`templates/CLAUDE.md`. Both `08`-owned rows now carry links instead of numbers, with an
explicit note that a second copy would drift. A second finding promoted the section from a
`###` under "Body sections" to a top-level `##`, since three of its four rows describe
artifacts owned by `03` and `08` rather than item bodies.

---

### BL-0021 — Derivable-from-source admission test for memory and instruction entries

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E06-bmad-v6-landscape-pass         |
| Pillar   | P9                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | done                               |
| Test     | pass — repo-wide consistency check; no conflict with the v1.20 archival lifecycle it complements |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** `08`'s "do not save" list already ruled out "patterns derivable from
reading the current code," but only as one bullet among seven, with no general criterion behind
it. Promoted the bullet into an explicit **admission test**: if a contributor can learn it by
reading the repo right now, it is read live and never written down; only intent, rationale,
policy, and observed pitfalls earn a line. Paired with the audit rule that a consolidation pass
**ends smaller or equal, never larger**, and with the asymmetry that keeps it honest — a rule
that is working erases its own evidence, so low reference frequency is never grounds for
retirement.

**Done means:**

- [x] `08` states the admission test with a not-stored / stored contrast.
- [x] The "ends smaller or equal" audit rule is stated and tied to the size budgets.
- [x] The admission/retirement asymmetry is stated and cross-linked to the archival lifecycle
      and the `pinned` flag, so the new rule cannot be read as licence to prune working rules.
- [x] CHANGELOG entry shipped in the same release (v1.26.0).

**Files (actual):**

- `methodology/08_lessons_and_memory.md` — "The admission test: derivable from source is never
  stored", under "What NOT to save as memory".

**Resolution:** Promoted from [FUTURE.md](FUTURE.md) at maintainer direction and shipped in
v1.26.0, **after E06 had already closed** — recorded here rather than by re-opening the epic,
since the charter's exit criteria (BL-0015…BL-0019) were genuinely met at closure and
back-dating them would falsify the record. E06's item count reflects six archived items against
five chartered; the four remaining Tier-2 deferrals stay in `FUTURE.md`.
