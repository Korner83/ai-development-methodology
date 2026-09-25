# E00 — Intake — Future / deferred

_Deferred, not rejected. Promote by moving an entry into `BACKLOG.md` unchanged; the `BL-####` space is
shared, so promotion needs no renumbering._

---

### BL-0060 — Publish focused mode to `methodology/`

**The design, so it is not re-derived.** Two ways to run a backlog, differing in exactly one dimension:

| Element | Cascade mode | Focused mode |
|---|---|---|
| Upstream linkage | strategy → pillar → epic → item | **none required** |
| Epic charter, exit criteria | required | **skipped** |
| Item format, frozen intent, `Status`/`Test`, DoD gates, lock, Code Map at M+ | required | **identical** |

**Nothing that protects correctness is relaxed.** What is dropped is a charter the work was never going to
earn. Mode is a property of the **item**, not the project: a team runs the cascade for its roadmap and
intake for interrupts, in the same backlog, in the same week.

**One hard rule blocks the obvious version.** *"Items live in exactly one epic; new items always go into a
specific epic"* is in `00`'s hard-rules table, so allowing epic-less items is a hard-rule amendment and a
**MAJOR** bump. The cheap route — the one [E00](README.md) is running now — is a **standing intake epic**:
the rule stays literally true, filing takes seconds, and nothing published changes. The expensive route is
to amend the rule, which is conceptually cleaner and costs a major version plus a changed rule adopters
have already pasted into their own instruction files.

**The part worth publishing is not the mode — it is the measurement.** Report the share of closed items
that arrived through intake rather than the cascade, and read a high ratio as evidence *against the
cascade*. If most real work bypasses four planning layers, those layers are not earning their cost and
should be trimmed rather than enforced harder. **This methodology has no other mechanism that can tell it a
layer is not worth its cost** — it took an external auditor to notice that nine of sixteen conventions had
never been used.

**Source:** maintainer, 2026-08-25 — requirements churn and short-notice tickets make the four-layer
cascade a tax on work that will not outlive the sprint.

**Target:** `methodology/03_epics.md` (the standing-epic shape) and `methodology/04_backlog_items.md` (the
mode as an item property), plus a line in `12` for the ratio report.

**Why it is deferred rather than chartered:** it would be the seventeenth convention added since v1.25.0,
and only seven of the first sixteen have ever been exercised. **This one gets used before it gets
written** — that ordering has never once happened in this project, and doing it in the other order is what
produced the finding class the last release repaired.

**Symptom that would justify promoting it:** `E00` has held real items through at least one semi-annual
pass, the intake ratio has been reported once, and the eviction rule has fired at least once — meaning
intake demonstrably feeds the cascade rather than replacing it. Absent that, publishing it is a guess with
a table around it.

---

### BL-0061 — Landscape runners-up from the 2026-08-25 triage

Ranked below Agent File (BL-0058) and recorded so the next pass does not re-triage the same list.

- **KaibanJS** — a Kanban board as the multi-agent coordination primitive; the closest structural peer to
  the `BL-####` backlog, in code rather than markdown. Would inform F-01's coordination question from the
  side that actually built it. *Promote if:* the shared-ref lock protocol gets exercised and proves
  awkward.
- **A2A Protocol** — agent-to-agent communication. The same problem as the lock, approached where a shared
  file is not the medium. *Promote if:* an adopter runs agents that cannot share a repo.
- **Conductor OSS** — durable, resilient event-driven orchestration. **Not a candidate for adoption**: it
  *is* the external coordinator `05` explicitly declines. Worth citing by name in `05`'s variants section
  so the declined alternative has a concrete referent instead of a category.

**Rejected outright, with reasons, so they are not reconsidered:** MemPalace and OpenViking (runtime memory
services against a markdown memory layer — the trade `08` already refuses); DSPy (would treat
`ROLE_BRIEFS.md` as optimizable artifacts; interesting, wrong axis, needs a runtime); and the entire
inference, training, serving and data-pipeline majority of the list, which governs a different layer of
the stack than this methodology does.

**Method caveat, recorded because it bounds every verdict above:** the triage ranked candidates from
one-line README descriptions and opened no repositories.

---

### BL-0068 — Worktree hygiene gaps in `09`

Deferred from the same 2026-09-25 read of `agent-of-empires/agent-of-empires` (at `c2bc548`) that filed
BL-0066 and BL-0067. Held here rather than filed so that three open intake items from one source do not
trip the eviction rule on the strength of a shared *source* rather than a shared *theme*.

`09`'s "Worktrees for parallel agents" section covers creation, removal and the symlink hazard. AoE's
`docs/guides/worktrees.md` handles five cases it does not:

- **Branch from a freshly fetched base**, not the local ref — otherwise the new tree starts stale. The same
  visibility point as D1's lock finding: state is only authoritative where it has been fetched.
- **`post-checkout` hooks fire on `git worktree add`** and commonly fail in a fresh tree that lacks the
  environment they expect; the tree is still usable.
- **Never remove the checkout holding the default branch**, even with force.
- **`git worktree lock` is not a guard** against tooling that unlocks before its own removals.
- **Relocate before deleting** — moving an abandoned tree aside keeps cleanup reversible, which matters
  because `remove --force` sits on the ✗ rows of the operation table.

*Promote if:* an adopter or this repo's own loop hits one of the five, or the next edit to `09`'s worktree
section is already open. Not a new convention either way — five sentences inside an existing section.
