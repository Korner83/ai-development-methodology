# E07 — Agentic-workflow landscape pass — Archive

_All five items shipped together in **v1.29.0** (2026-08-14)._

**Lifecycle note:** like E06, this epic ran `planned → done` inside one maintainer-directed session
("lets plan this implementation from 1 to point 5", then "yes please start implementing"). That
direction is what satisfies the **T2 / maintainer-authored** requirement — human-directed, not
loop-initiated. The WIP cap was never consumed.

**Shared verification:** repo-wide anchor check across all tracked markdown, run after BL-0026's
section rename — **zero broken**. Every touched doc confirmed under the 1,050-line soft cap
(`04` 1,020 · `06` 358 · `07` 544 · `08` 671 · `10` 754). Markdown-only diff.

---

### BL-0025 — Context-integrity canary

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E07-agentic-workflow-pass          |
| Pillar   | P9                                 |
| Priority | P1                                 |
| Effort   | S                                  |
| Status   | done                               |
| Test     | pass — convention documented with protocol and stated limits; both templates carry the rule |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** The two-layer memory design rests on an assumption nothing checks — that the
instruction file is *still in context*. It is read at session start; as context fills, the earliest
content is dropped first, and nothing announces it. The agent keeps working, equally confident, with
the project's rules no longer applying. Adopted a **canary**: the instruction file requires a short
marker at the start of every response, and the marker's **absence** is the signal.

**Done means:**

- [x] `08` documents the convention, the marker requirement, and — the part that makes it useful —
      the **protocol when it vanishes** (stop, re-read, rehydrate from active context, or restart).
- [x] The stated limits are in the same section, not a footnote: detects loss not decay, produces
      false positives, and some harnesses strip leading tokens.
- [x] Both templates carry the rule where an agent actually reads it.

**Files (actual):** `methodology/08_lessons_and_memory.md` ("The context-integrity canary" plus a
contents-table row); `templates/CLAUDE.md`, `templates/AGENTS.md` ("Context integrity" section).

**Resolution:** Shipped in v1.29.0. Deliberately framed as *a smoke alarm, not proof of safety* —
no gate depends on it, and the section says so explicitly, because a detector that produces both
false positives and false negatives is exactly the kind of thing a reader over-trusts. Text marker
rather than an emoji, keeping the corpus free of pictographs (a cross-AI review in v1.25.0 flagged
our only emoji as an outlier and it was removed).

---

### BL-0026 — Spec-verification as a third cross-AI mode

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E07-agentic-workflow-pass          |
| Pillar   | P9                                 |
| Priority | P1                                 |
| Effort   | M                                  |
| Status   | done                               |
| Test     | pass — third mode documented; 4 inbound anchors repointed; repo-wide anchor check zero broken |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** Cross-AI validation ran only *after* work existed — findings-verification on
a finished item, diff-verification on a proposed patch. Nothing checked whether the **plan itself**
was factually grounded before implementation. Added **spec-verification**: a fresh session checks the
item body and its Code Map against the real codebase — grounded (do these files and functions exist),
coherent (does the approach fit what is actually there), sufficient (would executing it satisfy the
goal) — before any code is written.

**Done means:**

- [x] `10`'s "Two modes" becomes **three**, with spec-verification first and the same PASS/FAIL plus
      citations output shape.
- [x] The rationale is tied to failure-layer routing: an intent/plan finding cancels everything
      beneath it, so catching those layers *earliest* beats routing them best.
- [x] Keyed to effort (M+), with the honest note that it is ceremony on an XS fix.
- [x] All four inbound references to the renamed section updated; anchor check clean.

**Files (actual):** `methodology/10_testing_and_verification.md` (section renamed plus new mode);
`methodology/04_backlog_items.md` (Code Map points at it); anchors repointed in `CHEATSHEET.md`,
`methodology/07`, `methodology/09`, `templates/AUTONOMOUS_LOOP.md`.

**Resolution:** Shipped in v1.29.0. The riskiest item of the five, entirely because of the rename:
`#two-modes-...` was referenced from four files, and the visible link *text* was stale in two of them
even after the anchors were repointed — caught by checking text as well as targets. This is the
shift-left of the v1.25.0 routing work: v1.25.0 taught us to *route* plan-layer defects well; this
moves the check to before the code exists, where the fix is editing a paragraph.

---

### BL-0027 — Write docs at the altitude that survives change

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E07-agentic-workflow-pass          |
| Pillar   | P1                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | done                               |
| Test     | pass — rule stated with a one-question test and cross-linked to the memory admission test |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** v1.26.0 added the memory **admission test** — derivable from source is never
stored — but stated it only for memory entries. System documentation had no equivalent, so it kept
accumulating implementation detail that goes false the first time someone rewrites the
implementation, silently, while still being read as authority.

**Done means:**

- [x] `07`'s living-documents playbook says document **interactions and contracts, not
      implementations**.
- [x] The test is one question: *if I rewrote this implementation tomorrow, would this paragraph
      become false?*
- [x] Cross-linked to `08`'s admission test as the same principle on a different artifact.

**Files (actual):** `methodology/07_definition_of_done.md` ("Write docs at the altitude that survives
change").

**Resolution:** Shipped in v1.29.0. The framing that earns it: *a confidently wrong document costs
more than an absent one* — the absent one sends you to the code, and the code is never out of date.

---

### BL-0028 — Refactor, don't fit: architecture-invalidating change

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E07-agentic-workflow-pass          |
| Pillar   | P9                                 |
| Priority | P2                                 |
| Effort   | XS                                 |
| Status   | done                               |
| Test     | pass — routing extended one level up; anti-pattern row added |
| Deps     | BL-0026                            |
| Lock     | —                                  |

**Why / Description:** Failure-layer routing stopped at the item: intent, plan, code. But a finding
can be bigger than any item — an external requirement changed and the *architecture* no longer fits
it. Without naming that layer, the default is to wedge the new requirement into the old
architecture, producing a codebase that "works" while every future item pays interest.

**Done means:**

- [x] `07`'s routing section extends the same rule one level up, and says the fix is a
      strategy/pillar-level re-evaluation rather than something an item absorbs quietly.
- [x] `06` gains the matching anti-pattern row.

**Files (actual):** `methodology/07_definition_of_done.md` ("When the architecture is what's wrong");
`methodology/06_working_principles.md` (anti-pattern table).

**Resolution:** Shipped in v1.29.0. Smallest item in the epic — it is the architecture-scale sibling
of *never patch code to compensate for a wrong plan*, and reuses that section rather than starting a
new one.

---

### BL-0029 — Output verbosity as a project setting

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E07-agentic-workflow-pass          |
| Pillar   | P1                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | done                               |
| Test     | pass — setting documented in 08 with the cut-filler/keep-reasoning boundary; both templates carry it |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** The corpus had **zero** guidance on response verbosity, so every contributor
either re-negotiated it per session or accepted the default by inertia. It costs twice: tokens, and —
larger — reader attention, since a four-paragraph answer to a one-line question trains the reader to
skim, and skimming is how a real caveat gets missed.

**Done means:**

- [x] `08` names it as an instruction-file setting with a stated default (technical and direct; no
      praise preamble, no restating the question).
- [x] The boundary is explicit: **cut filler, never cut reasoning.**
- [x] Both templates carry a "Communication style" section.

**Files (actual):** `methodology/08_lessons_and_memory.md` ("Setting the house verbosity" plus a
contents-table row); `templates/CLAUDE.md`, `templates/AGENTS.md`.

**Resolution:** Shipped in v1.29.0, and deliberately *not* adopted as the source's "caveman mode".
Dropping *"great question"* costs nothing; dropping the *why* dismantles the methodology — Principle
1 requires stated assumptions, plan-mode requires the reasoning, the DoD requires an honest account
of what failed. The section says that an agent which responds to terseness guidance by becoming
confidently silent about its uncertainty is worse than a wordy one, and that this means the setting
is too aggressive.
