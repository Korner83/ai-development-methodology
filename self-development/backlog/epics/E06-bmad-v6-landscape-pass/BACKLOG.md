# E06 — BMAD v6 landscape pass — Active Backlog

_Items currently in scope for this epic. See [charter](README.md) for exit criteria._

**Epic status (as of 2026-08-14):** **planned**. Items below are NOT pickable by the
autonomous loop until the maintainer promotes E06 to active (WIP cap = 2; one slot used by
E03, one open — see `self-development/backlog/EPICS.md`). Every item proposes
`methodology/*.md` changes and is therefore **T2 (maintainer-authored)** per the
[charter's tier note](README.md#tier-note-authority): agents draft, the maintainer ships.

## Summary

| ID      | Title                                                               | Priority | Effort | Status  |
|---------|---------------------------------------------------------------------|----------|--------|---------|
| BL-0015 | Spec-as-sole-context handoff (Code Map) for M/L items               | P1       | M      | backlog |
| BL-0016 | Frozen-intent convention for approved goals / exit criteria         | P1       | S      | backlog |
| BL-0017 | Failure-layer triage for review findings                            | P1       | M      | backlog |
| BL-0018 | Verification-gap review lens + test-actually-ran audit              | P1       | S      | backlog |
| BL-0019 | Size budgets for context artifacts (item body, epic digest)         | P2       | S      | backlog |

---

### BL-0015 — Spec-as-sole-context handoff (Code Map) for M/L items

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E06-bmad-v6-landscape-pass         |
| Pillar   | P9                                 |
| Priority | P1                                 |
| Effort   | M                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** Today an item's body records *what* to do (`Done means:`), but the
codebase knowledge gathered while planning it lives only in the planning session's
conversation — so it dies on handoff, compaction, or a fresh session. Adopt the convention
that for M/L-effort items, planning **drains its investigation into the item body** as a
**Code Map** (files to touch with their roles, existing functions/utilities to reuse,
constraints and gotchas), written so that *a cold session can implement from the item alone*,
with no conversational context restated at dispatch. This is the item-level sibling of the
existing subagent-delegation rule and makes items genuinely resumable by any agent — which is
what a shared lockable backlog promises. (Source: BMAD `bmad-build` steps 02–03 — the spec
file is the sole context channel; the parent is forbidden from re-narrating context to the
implementer. Restate in our vocabulary: items, not specs.)

**Approach:**

1. Draft a "Code Map" subsection convention for `methodology/04_backlog_items.md` (likely
   inside the item-body anatomy section): when to include it (M/L efforts; skip for XS/S),
   what belongs (annotated paths, reuse pointers, constraints), what doesn't (prose
   architecture essays — link the pillar/architecture doc instead).
2. Define the handoff test: "could a fresh session with only this item body start implementing
   without re-investigating?" — mirror the existing senior-engineer/traceability test style.
3. Add the cold-handoff dispatch rule: when work is delegated (subagent, next session, another
   agent), point at the item; do not paste a summary that can drift from it.
4. Add a `Code Map` slot to the item skeleton in `templates/` where one exists.
5. Cross-link: `08_lessons_and_memory.md` active-context section (session state vs item
   knowledge — Code Map is durable, ACTIVE_CONTEXT is volatile) and `05` subagent rules.
6. Maintainer ships as a versioned release; cross-AI diff-verification before merge.

**Done means:**

- [ ] `methodology/04_backlog_items.md` defines the Code Map convention with an
      include/skip rule keyed to Effort, and the cold-handoff test.
- [ ] When an M/L item is delegated, the receiving agent's instruction is the item itself —
      the no-re-narration rule is stated where delegation is described.
- [ ] Distinction from `ACTIVE_CONTEXT.md` (durable item knowledge vs volatile session state)
      is stated in whichever doc hosts the convention.
- [ ] CHANGELOG entry ships in the same release; item moved to `ARCHIVE.md` after cross-AI
      validation passes.

**Files (probable):**

- `methodology/04_backlog_items.md` (modified)
- `methodology/05_locks_and_parallel_work.md` (delegation cross-link)
- `methodology/08_lessons_and_memory.md` (active-context cross-link)
- `templates/` item skeleton if present (Code Map slot)

**Notes:** T2 — touches `methodology/`; loop drafts, maintainer authors (charter tier note).
Watch the `04` line count (894 → soft cap 1,050); prefer tightening the existing body-anatomy
section over adding a new top-level section.

---

### BL-0016 — Frozen-intent convention for approved goals / exit criteria

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E06-bmad-v6-landscape-pass         |
| Pillar   | P9                                 |
| Priority | P1                                 |
| Effort   | S                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** Nothing today stops an agent mid-task from "helpfully" rewording an
item's goal or `Done means:` to match what it actually built — the drift is invisible because
the diff looks like editing, not scope change. Adopt a **frozen-intent** convention: once a
human approves an item's goal + acceptance criteria (or an epic charter's exit criteria), that
region is *human-owned* — agents may not modify it; if execution reveals it's wrong, the move
is **halt and renegotiate** (surface the conflict, get explicit re-approval), never silent
amendment. This completes a family: protected regions guard *code* zones (v1.23), the tier
matrix guards *authoritative docs*, frozen intent guards *approved work definitions*.
(Source: BMAD's `<frozen-after-approval reason="human-owned intent">` block in
`spec-template.md`.)

**Approach:**

1. Draft the rule for `methodology/04_backlog_items.md` (item lifecycle: what approval
   freezes) and `methodology/06_working_principles.md` (as the third member of the
   protected-regions family, under goal-driven execution).
2. Pick the marker syntax (charter open question): HTML comment, blockquote badge, or heading
   convention — must be greppable and render cleanly on GitHub.
3. Define the renegotiation path: who can thaw (the human who approved, or higher authority),
   and that the change lands as a visible edit with a one-line reason.
4. Reconcile with the existing scope-creep recovery protocol (stop → split → narrow) — frozen
   intent is *why* narrowing the original silently is prohibited; cross-link, don't duplicate.
5. Add the marker to item/charter skeletons in `templates/`.

**Done means:**

- [ ] `04` states what approval freezes and the halt-and-renegotiate rule; `06` places it in
      the protected-regions family with an anti-pattern row (agent rewords acceptance criteria
      to match the implementation).
- [ ] Marker syntax chosen and documented; templates carry it.
- [ ] Scope-creep recovery section cross-links frozen intent (no contradiction between the
      two).
- [ ] CHANGELOG entry ships in the same release; item moved to `ARCHIVE.md` after cross-AI
      validation passes.

**Files (probable):**

- `methodology/04_backlog_items.md` (modified)
- `methodology/06_working_principles.md` (modified)
- `templates/` item/charter skeletons (marker slot)

**Notes:** T2 — touches `methodology/`; loop drafts, maintainer authors.

---

### BL-0017 — Failure-layer triage for review findings

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E06-bmad-v6-landscape-pass         |
| Pillar   | P9                                 |
| Priority | P1                                 |
| Effort   | M                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** The v1.22 two-stage review orders *review passes* (spec-compliance,
then quality) but every *finding* still lands in one pile labeled "fix it." Adopt
**failure-layer triage**: classify each finding by the layer the defect entered, and route
the fix to that layer —

1. **Intent wrong** (the approved goal itself is mistaken) → halt, back to the human,
   re-approve (pairs with BL-0016's frozen intent);
2. **Plan/item wrong** (goal fine, the item's approach/Code Map led the code astray) → fix the
   item body first, then re-derive the code from it — **never patch code to compensate for a
   wrong plan** (named anti-pattern);
3. **Code wrong** → patch;
4. **Real but out of scope** → file to `FUTURE.md` or a new item, don't fix inline (extends
   the scope-creep protocol);
5. **Invalid** → reject with a one-line reason.

Processed in that order: an intent- or plan-level defect moots the code-level findings below
it. (Source: BMAD `step-04-review.md`'s five-bucket cascade — intent_gap / bad_spec / patch /
defer / reject; restated in our vocabulary.)

**Approach:**

1. Draft the triage table + cascade rule for `methodology/07_definition_of_done.md` Gate 1,
   extending the two-stage review subsection rather than adding a parallel section.
2. Add the "never patch code to compensate for a wrong plan" anti-pattern to `10`'s review
   guidance (near the cheating-agent section) and to `06`'s anti-pattern table if it fits an
   existing row.
3. Define the loop-escape: if the same item cycles intent/plan-level findings more than N
   times (suggest 2), stop and surface to the human — mirrors the unsolvable-issue
   "never force" stance in `12`.
4. Reconcile with cross-AI findings-verification (`10`): the verifier confirms the *bucket*,
   not just the finding.

**Done means:**

- [ ] `07` Gate 1 contains the five-bucket triage with cascade order and routing per bucket.
- [ ] The wrong-plan anti-pattern is named where reviews are described; out-of-scope findings
      route to FUTURE/new items instead of inline fixes.
- [ ] Cycle-escape threshold documented (repeat intent/plan findings ⇒ human).
- [ ] No contradiction with the two-stage review it extends (cross-AI check confirms).
- [ ] CHANGELOG entry ships in the same release; item moved to `ARCHIVE.md` after cross-AI
      validation passes.

**Files (probable):**

- `methodology/07_definition_of_done.md` (modified — Gate 1)
- `methodology/10_testing_and_verification.md` (modified — review guidance)
- `methodology/06_working_principles.md` (possible anti-pattern row)

**Notes:** T2 — touches `methodology/`; loop drafts, maintainer authors. Batches naturally
with BL-0018 into one "review rigor" release (charter open question — lean yes).

---

### BL-0018 — Verification-gap review lens + test-actually-ran audit

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E06-bmad-v6-landscape-pass         |
| Pillar   | P9                                 |
| Priority | P1                                 |
| Effort   | S                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** Our cheating-agent defenses audit *test quality* (who wrote them,
sampling impl/test pairs) but not *test coverage of the change* or *whether the tests
actually executed*. Add three sharp rules to DoD Gate 2 and `10`:

1. **Verification-gap lens:** one review pass asks, for each behavior this change introduces
   or alters, "**if this behavior broke, would any test fail?**" — its output is a list of
   untested behavior changes, not bugs.
2. **Test-actually-ran audit:** a test that exists but was skipped, filtered out, or never
   executed in the verifying run **counts as missing** — `Test: pass` requires the relevant
   tests to have *run*.
3. **Never edit the expectation to match the code:** when a test fails, the fix is the code or
   a renegotiated criterion (BL-0016) — adjusting the assertion to green is the named
   anti-pattern.

(Source: BMAD's Verification-Gap review layer and Matrix Test Audit in `bmad-build`.)

**Approach:**

1. Draft the verification-gap lens into `07` Gate 2 (automated tests) with a one-line
   cross-ref from Gate 1's review stages.
2. Add the ran-not-just-exists rule to `10`'s `Test:` field semantics (what evidence "pass"
   requires) and the expectation-editing anti-pattern next to the cheating-agent section.
3. Wire one line into the AUTONOMOUS_LOOP verify step and the skill's self-check list so the
   loop applies the lens without a human prompting it.

**Done means:**

- [ ] `07` Gate 2 includes the verification-gap question as a required review lens for
      behavior-changing work.
- [ ] `10` states that skipped/filtered/not-run tests count as missing for `Test: pass`, and
      names the expectation-editing anti-pattern.
- [ ] Loop template + skill self-check reference the lens (one line each).
- [ ] CHANGELOG entry ships in the same release; item moved to `ARCHIVE.md` after cross-AI
      validation passes.

**Files (probable):**

- `methodology/07_definition_of_done.md` (modified — Gate 2)
- `methodology/10_testing_and_verification.md` (modified)
- `templates/AUTONOMOUS_LOOP.md` (one-line addition)
- `skills/ai-dev-methodology/SKILL.md` (self-check line)

**Notes:** T2 — touches `methodology/`; loop drafts, maintainer authors. Batches with
BL-0017 (same target docs).

---

### BL-0019 — Size budgets for context artifacts

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E06-bmad-v6-landscape-pass         |
| Pillar   | P9                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** We cap exactly one artifact today (instruction file ≤ ~300 lines);
item bodies, epic charters, and memory entries have no size guidance, and oversized ones
silently degrade every agent that loads them — context is a cost even when it's correct.
Generalize the principle: publish **size targets with a split rule** for the artifacts agents
load routinely — e.g. item body ~1–2 pages (an item that can't fit is telling you to split
it: route to the existing scope-creep/split protocol), epic charter ~2–3 pages, memory entry
30–100 lines (already stated in `08` — consolidate, don't duplicate). Frame with the
one-sentence rationale: *a context artifact is a liability that must earn its length*.
(Source: BMAD's explicit token budgets — spec 900–1300 tokens, epic digest 800–1500 — and
`project-context-theory.md`; ours stay line/page-denominated since adopters don't measure
tokens.)

**Approach:**

1. Draft a compact budgets table (artifact → target → too-big-means) for
   `methodology/04_backlog_items.md` (item/charter budgets) with the split rule pointing at
   the existing scope-creep recovery section.
2. Reconcile `08`'s existing numbers (instruction file, memory entries) so every budget is
   stated once and cross-referenced, not repeated.
3. State budgets as defaults with an override note (a project may re-tune them in its
   instruction file), mirroring the DoD-overlay pattern.

**Done means:**

- [ ] A budgets table exists covering at minimum: item body, epic charter, instruction file,
      memory entry — each with a target and a "too big ⇒" action.
- [ ] Existing numbers in `08` are referenced, not duplicated; no two docs state different
      budgets for the same artifact.
- [ ] Split rule routes to the existing scope-creep protocol (no new mechanism).
- [ ] CHANGELOG entry ships in the same release; item moved to `ARCHIVE.md` after cross-AI
      validation passes.

**Files (probable):**

- `methodology/04_backlog_items.md` (modified — budgets table)
- `methodology/08_lessons_and_memory.md` (cross-reference reconciliation)

**Notes:** T2 — touches `methodology/`; loop drafts, maintainer authors. Related Tier-2
deferral: BL-0022 (per-epic context digest) builds on this if promoted.
