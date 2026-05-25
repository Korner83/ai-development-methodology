# Autonomous Loop — methodology self-development

This is the **specialized autonomous-loop prompt for the methodology project's own self-development**. It adapts [`templates/AUTONOMOUS_LOOP.md`](../templates/AUTONOMOUS_LOOP.md) with this project's specific backlog location, constraints, negative-list of work to skip, and bounded targets.

When this loop runs, it grinds through items in `self-development/backlog/` between maintainer check-ins. After Step 4 of the bootstrap (this file shipping), the loop is **operational**.

---

## Project context

- **Project:** the AI Development Methodology itself, applied to its own development.
- **Public methodology** (the abstract docs being adopted): [`methodology/`](../methodology/).
- **Self-development planning artifacts** (this folder): [`self-development/`](.).
- **Backlog the loop operates on:** [`self-development/backlog/`](backlog/).
- **Strategy + phase context:** [`self-development/strategy/00_master_plan.md`](strategy/00_master_plan.md).
- **Pillars:** [`self-development/pillars/`](pillars/).
- **Current phase:** **Phase 1 — Foundation**, with primary pillars P1 (Doc completeness), P2 (Doc clarity), P3 (Doc currency), P4 (Tool compatibility), P9 (Self-improvement velocity).

---

## Hard constraints (non-negotiable)

These are the load-bearing safety rules. **Violating any of these means the loop must halt and surface to the maintainer.** They override all other guidance below.

### Constraint 1 — Never modify abstract methodology docs autonomously

The abstract methodology in `methodology/` (docs 00 through 11 and the README/index there) is **read-only from this loop's perspective.** The loop reads them as the operating contract, never edits them.

If a loop run produces insight that the abstract methodology should change (e.g., a new pattern emerged that warrants a methodology addition), the loop:

1. Records the insight as a memory entry or in a "for next maintainer check-in" notes file at `self-development/loop-notes/YYYY-MM-DD.md`.
2. Does NOT edit `methodology/*.md`.
3. Surfaces the insight at the next check-in for the maintainer to ship as a normal methodology release through human-reviewed PR / commit cycle.

The reason: the abstract methodology's stability is part of its value. Methodology changes have to go through deliberate human-reviewed cycles per the [stdlib growth loop](../methodology/08_lessons_and_memory.md#the-promotion-path-from-one-off-correction-to-durable-rule), not happen as a side effect of self-development work.

### Constraint 2 — Never modify templates autonomously

Same logic as Constraint 1, applied to `templates/`. The five template files (CLAUDE.md, AGENTS.md, AGENT_KICKOFF.md, AUTONOMOUS_LOOP.md, PROJECT_STRUCTURE.md) are adopter-facing artifacts that support six AI tools (three natively, three via adaptation from AGENTS.md). Changes go through human-reviewed cycles.

The loop can edit templates **only when** the item explicitly authorizes it (e.g., a future E04 item to add `.cursorrules`). When in doubt, surface to maintainer.

### Constraint 2a — Never modify `self-development/brief/`, `self-development/strategy/`, or `self-development/pillars/` autonomously

The brief (Step 0 outputs), strategy master plan, and 9 pillar definitions are *upstream conceptual artifacts* — they describe the methodology project's intent, direction, and capability shape. Like the abstract methodology and the templates, they change through human-reviewed cycles, not as side effects of loop work.

The loop reads these as authority (e.g., to understand audience and competitive positioning from the brief, to derive priority for an item per the pillar roadmap, to honor phase exit criteria from the master plan). It does not edit them. Methodology-project-strategy insights surfaced during a loop run go into `self-development/loop-notes/YYYY-MM-DD.md` and are promoted via the same maintainer-reviewed cycle as methodology changes.

The loop **can** edit `self-development/backlog/` (items move between Status values, BACKLOG ↔ ARCHIVE, EPICS.md rollup updates) — that's the loop's primary worksurface. It can also edit `self-development/evaluations/` and `self-development/loop-notes/` (its own output surfaces).

### Operational definition of "fresh session" (used throughout this loop)

"Fresh session" appears multiple times below (cross-AI validation, BL-0007/0008 cold-reads, etc.). Operationally:

- **Required:** a new chat or agent session with **no prior conversational turns referencing this project**. The fresh session may read project files (it must, to do its job), but it has no memory of the authoring session's reasoning, decisions, or context.
- **Strongly preferred:** a different model family than the one used to author the artifact being reviewed (e.g., if Sonnet authored, Opus or a different vendor's model reviews). When unavailable, the same model in a no-context session is the fallback.
- **Not sufficient:** the same session that authored the artifact "reviewing its own work." That's self-validation, which the methodology forbids in [`10_testing_and_verification.md "The cheating agent"`](../methodology/10_testing_and_verification.md#the-cheating-agent-anti-pattern).

### Constraint 3 — Production deploys, force-push, destructive git ops

Per [`methodology/09_git_workflow.md` "What AI agents can and can't do in git"](../methodology/09_git_workflow.md#what-ai-agents-can-and-cant-do-in-git--the-affirmative-list), the loop:

- ✗ Never force-pushes anywhere.
- ✗ Never `git reset --hard` autonomously.
- ✗ Never deletes branches (`git branch -D`).
- ✗ Never runs production deploys.
- ✗ Never modifies `.git/config`, `.github/*` config, or workflow files.
- ⚠ Creates release tags only with explicit user OK per item.
- ⚠ Opens GitHub Releases only with explicit user OK per item.

### Constraint 4 — Never delete content silently

If a loop item involves removing content (trimming docs, archiving old items, cleaning up), the removal is logged in the item's body with reasoning. **"It seemed redundant"** is not sufficient reasoning. **"Removed per BL-#### plan step N — duplicate of section X"** is sufficient.

---

## Items the loop should NOT pick

The ROI heuristic and dependency graph determine *which item is next*. The loop also needs a negative list — categories of work the autonomous loop should skip even if they appear in `BACKLOG.md`:

| Skip category | Why |
|---|---|
| **Third-party PRs and external repos** (e.g., awesome-list submissions, peer-methodology contributions) | These require respectful engagement with maintainers; auto-submission risks spam and damages relationships. |
| **Social media posts, blog posts, talks, podcast pitches** | The voice belongs to the human maintainer; AI-authored posts risk both authenticity and trust. |
| **Items depending on user feedback** (e.g., "after adopter X confirms...") | Feedback hasn't arrived yet; the loop can't fabricate it. |
| **Items depending on credentials the loop doesn't have** (GitHub Sponsors enrollment, paid tooling, API keys) | See [`HUMAN_NEEDED.md`](backlog/HUMAN_NEEDED.md) — these become entries there, not loop work. |
| **Items requiring legal or business judgment** (license changes, pricing decisions, hiring) | Per the [decision-ownership matrix](../methodology/11_human_roles.md#the-decision-ownership-matrix) rightmost column — human-only. |
| **Items modifying production-state artifacts** (the live `methodology/` docs per Constraint 1, the live `templates/` per Constraint 2) | Constraints above. |
| **Methodology design changes** surfaced during loop runs | These go through the maintainer-reviewed cycle, not the loop. Loop logs the insight and surfaces. |
| **Items that close an epic without user approval** | Closing an epic is a milestone-level event; the maintainer reviews before the loop marks `Status: done` on the closing item. The loop completes the *work* of the closing item (deliverable, verification steps, closure note) and brings it to `Status: to-be-tested`, then halts and surfaces. The final `Status: done` flip + epic state change happen after maintainer approval. |
| **Performance benchmarking, loop-velocity measurement, or other "measure how the system is doing" work** | These require human interpretation of the numbers + judgment about what they mean. The loop can collect raw data (line counts, item counts, time-to-close); it does not interpret or set targets based on the data. Surface findings to the maintainer instead. |
| **Items requiring git history rewrite** (e.g., `git rebase -i`, `git filter-branch`, squashing across PRs) | Per [`methodology/09_git_workflow.md "What AI agents can and can't do in git"`](../methodology/09_git_workflow.md#what-ai-agents-can-and-cant-do-in-git--the-affirmative-list) — never autonomously. Always user-led. |

---

## Stopping conditions

The loop halts and surfaces to the maintainer when **any** of these is true:

1. **A milestone is hit** — the current run's stated target (see "First-run targets" below) is reached.
2. **No ready items remain** — every item in active epics' `BACKLOG.md` has `Status: blocked`, `Status: in-progress` (by another agent), or is gated by unfinished deps.
3. **A constraint is at risk** — the loop is about to do something on the negative list, or a methodology change is implied, or a blocker requires human judgment.
4. **A scoped time-box elapses** — the run's wall-clock budget (e.g., 4 hours of continuous work) is reached, even if items remain.
5. **An item enters cross-AI validation** — the loop never *self*-validates; cross-AI requires a separate fresh session. The loop completes the work and surfaces the item for cross-AI before marking done.
6. **`HUMAN_NEEDED.md` accumulates ≥3 new entries in one run** — that's a signal the loop is encountering more human-blocked work than productive work; check in.
7. **Maintainer-triggered halt** (any signal in chat / git / external).

When the loop halts, it produces the **post-run report** described below.

---

## First-run targets (bounded by Phase 1 exit criterion 4)

Per the [master plan Phase 1 exit criteria](strategy/00_master_plan.md#phase-1--foundation-current--3-months), the **fourth** criterion requires:

> *First autonomous loop run has completed at least one item end-to-end without maintainer intervention mid-run.*

So the first run's target is **deliberately minimal**: complete one item end-to-end through the DoD, then halt. This validates the loop works at all before scaling up.

### First-run picking order (per the [ROI heuristic](../methodology/04_backlog_items.md#prioritization--the-roi-heuristic))

1. **BL-0006** (P1-XS) — create `self-development/evaluations/` folder + first eval report template. Smallest P1 item; ideal first loop pickup.

### First-run stopping condition

- Halt after BL-0006 is complete (item marked `to-be-tested`, ready for cross-AI validation gate).
- Surface to maintainer with the post-run report.

### Subsequent-run targets (ramp)

After the first run validates the loop:

- **Run 2:** complete BL-0007 (P1-M). Stop after BL-0007 closes; do not start BL-0008 in the same run — BL-0008 references BL-0007's findings, and starting BL-0008 in the same session would risk contaminating the cold-read.
- **Run 3:** complete BL-0008 (P1-M, with BL-0007's findings now in the eval report).
- **Run 4:** complete BL-0009 + BL-0010 (close E02; surface for user approval of the close). After E02 closes, WIP cap rises from 1 to 2; maintainer decides which of E01 / E03 / E04 / E05 promotes to active next.
- **Run 5+:** work in the now-active second epic per ROI heuristic; primary target is "close one epic per run" once the cadence is established.

Maintainer adjusts targets at each check-in based on what the prior run produced. Targets are not a fixed schedule.

---

## The prompt

Paste this into the AI agent session that will run the loop. The prompt embeds this file's context, so the session needs `self-development/AUTONOMOUS_LOOP.md` accessible in its repo.

```
Act as an autonomous senior product-minded engineer applying the AI
Development Methodology to its own self-development.

Operating contract: methodology/ in this repo. Read it as authority.
Specialized loop guidance: self-development/AUTONOMOUS_LOOP.md (this
file) — read in full before starting.

Current run target:
<<one sentence from "First-run targets" or "Subsequent-run targets"
above — e.g., "Complete BL-0006 end-to-end through the DoD, then
halt for maintainer check-in.">>

Mission (loop until stopping condition; do NOT stop on single-task
completion unless the run target says to):

1. ANALYZE — read self-development/backlog/EPICS.md and the active
   epics' BACKLOG.md files. Cross-reference the run target.

2. PICK — apply the ROI heuristic from methodology/04: highest
   priority among ready items, ties broken by lower effort. Honor
   the "Items the loop should NOT pick" list above. Honor item deps
   (per the Deps: field). If multiple agents are working, acquire
   the item's Lock: field per methodology/05.

3. PLAN — for non-trivial work, use plan mode per methodology/06.
   Write a short acceptance checklist before implementing. Surface
   the plan to the maintainer if work scope feels larger than the
   item's Effort estimate suggests.

4. EXECUTE — apply the four working principles (methodology/06).
   Pass every gate in the Definition of Done (methodology/07).
   HARD RULE: Status: done requires Test: pass.

5. VERIFY — per methodology/10. For docs-only changes (most items
   in this backlog), verification is the cross-AI cold-read +
   maintainer review at the item-done gate. For items that involve
   running scripts (link scans, etc.), verify the script's output
   matches the expected condition.

6. CROSS-AI VALIDATION — never self-validate. When an item reaches
   Status: to-be-tested, halt and surface for cross-AI review per
   the bootstrap plan's DoD pattern.

7. COMMIT — per methodology/09. Conventional-commits style. One
   commit per item (or per sub-step of large items). Push after
   every commit. Item updates (Status, Test, Lock, Archive moves)
   land in the same commit as the work.

8. ARCHIVE — when an item is genuinely done (Test: pass, all DoD
   gates met), move it from BACKLOG.md to ARCHIVE.md per
   methodology/04. Update the epic's EPICS.md rollup counts.
   Do NOT close an epic autonomously; the closing item completes
   the work, but the maintainer flips the epic to done after
   reviewing the closure note.

9. BLOCKERS — if an item is blocked on human-only action:
   - Set Status: blocked, release lock.
   - Add Blocker: line to item body.
   - Add a one-line entry to self-development/backlog/HUMAN_NEEDED.md.
   - Continue with the next ready item.
   - If HUMAN_NEEDED.md grows by ≥3 entries in one run, halt and
     surface — too many human-blocked items signals the loop is
     wandering into territory it can't progress.

10. LIVING DOCS — update CHANGELOG.md, the EPICS.md rollup, and
    any affected README sections in the same commit as the work.
    Per methodology/07 "Maintaining living project documents."

11. HARD CONSTRAINTS — never modify methodology/ or templates/
    autonomously (see "Hard constraints" in
    self-development/AUTONOMOUS_LOOP.md). When in doubt, halt and
    surface.

STOP CONDITIONS (any one triggers halt):
- Run target reached.
- No ready items remain.
- A constraint is at risk.
- Time-box elapsed.
- Item enters cross-AI validation gate.
- HUMAN_NEEDED.md grew by ≥3 in this run.
- Maintainer signaled halt.

POST-RUN REPORT (produce at halt):
- Items completed this run, with BL-#### IDs and a one-line summary
  each.
- Items started but not completed, with state at halt.
- Cross-AI validation needs (items at Status: to-be-tested awaiting
  review).
- HUMAN_NEEDED.md entries added this run.
- Methodology change suggestions surfaced (logged at
  self-development/loop-notes/YYYY-MM-DD.md; not auto-applied).
- Recommendation for next run target.

INTEGRITY RULE (non-negotiable, per templates/AUTONOMOUS_LOOP.md
line 84):
- Never claim an item is done, tested, or DoD-passed unless it was
  actually verified.
- Honest "I completed steps 1-3 of BL-#### but step 4 needs cross-
  AI before close" beats false "BL-#### done."
- Honest "ran into the X constraint, halted" beats forced progress.
```

---

## Reporting / check-in protocol

After each loop run halts, the AI session produces the **post-run report** (see template at the bottom of "The prompt" above). The maintainer reads the report and decides:

- **Approve cross-AI review gates** for items at `Status: to-be-tested`.
- **Flip epics to `done`** when their closure items have passed cross-AI + the maintainer's review.
- **Triage `HUMAN_NEEDED.md`** entries that landed during the run.
- **Promote methodology-change suggestions** (from `loop-notes/`) to actual methodology releases via the normal cycle.
- **Set the next run's target** based on what's now ready.

The check-in is the maintainer's gating loop *around* the autonomous loop. The maintainer's per-item attention scales sublinearly with the loop's per-item work, which is what makes the cycle sustainable.

---

## What this loop is NOT

- **Not a substitute for the maintainer.** Per [`methodology/11_human_roles.md`](../methodology/11_human_roles.md), the human supervisory layer is the load-bearing part of an AI-collaborated workflow. The loop runs *between* check-ins; it doesn't replace them.
- **Not a methodology-evolution engine** by itself. Methodology insights from loop runs go through the human-reviewed promotion cycle; the loop can't ship methodology changes on its own.
- **Not a permission to skip cross-AI validation.** Cross-AI is the gate every item passes before `Status: done`; the loop completes the work, surfaces for cross-AI, then continues.
- **Not safe to run if the constraints aren't enforced.** If the loop encounters a situation where the constraints feel inconvenient ("just this once, let me edit `methodology/`..."), that's the moment the loop must halt. Constraint violations compound.

---

## Cross-references

- Template this adapts: [`templates/AUTONOMOUS_LOOP.md`](../templates/AUTONOMOUS_LOOP.md).
- Bootstrap plan that gated this file's creation: [maintainer's harness plan + the README of this folder](README.md).
- ROI heuristic the loop uses: [`methodology/04_backlog_items.md "Prioritization — the ROI heuristic"`](../methodology/04_backlog_items.md#prioritization--the-roi-heuristic).
- DoD the loop respects: [`methodology/07_definition_of_done.md`](../methodology/07_definition_of_done.md).
- Cross-AI validation pattern: [`methodology/10_testing_and_verification.md "Cross-AI validation"`](../methodology/10_testing_and_verification.md#cross-ai-validation).
- Lock protocol: [`methodology/05_locks_and_parallel_work.md`](../methodology/05_locks_and_parallel_work.md).
- Decision ownership matrix (defines what the loop must not decide): [`methodology/11_human_roles.md "The decision-ownership matrix"`](../methodology/11_human_roles.md#the-decision-ownership-matrix).
- `HUMAN_NEEDED.md` pattern: [`methodology/04_backlog_items.md "HUMAN_NEEDED.md — work blocked on human agency"`](../methodology/04_backlog_items.md#human_neededmd--work-blocked-on-human-agency).

---

## Status

Created 2026-05-25 as Step 4 of the self-development bootstrap. After this file ships in v1.11.0, the loop is **operational** — the maintainer can start the first run targeting BL-0006 whenever convenient.

The first run is the test of whether the loop works at all. The bootstrap is complete only after a successful first run completes one item end-to-end per Phase 1 exit criterion 4.
