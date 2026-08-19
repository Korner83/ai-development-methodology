# Autonomous Development Loop — Prompt Template

A paste-and-adapt prompt for letting an AI agent run multi-hour or multi-session development cycles without user interaction between each task.

Pairs with [methodology/](../methodology/). This prompt *operationalizes* the methodology as an autonomous execution loop: most rules below reference methodology docs by number rather than re-explaining them. The methodology is the contract; this prompt is how the AI applies it on autopilot.

---

## When to use this

- **Use it for** focused milestone work where you've already agreed on the goal and want the AI to grind toward it autonomously between check-ins.
- **Don't use it for** open-ended exploration, early architecture decisions, or anything where each individual step needs your review.
- **For a single phase**, use the matching brief in [ROLE_BRIEFS.md](ROLE_BRIEFS.md) instead. This prompt is the unattended multi-item cadence; those are one stance for one phase, run interactively.

Before starting a loop, check that all four qualification conditions hold. If any fails, run the work interactively instead — a loop without them burns tokens without converging:

1. **The work recurs.** There is enough backlog volume toward the milestone that the loop will iterate many times; a loop set up for two items is overhead, not leverage.
2. **An automated rejection mechanism exists.** Tests, the DoD gates (methodology/07), or the milestone rubric (methodology/12) can fail the work without you in the room. If the only judge of "good enough" is your eye, each iteration needs you anyway.
3. **The agent can complete items end-to-end.** Environment, credentials, tooling, and permissions cover the full fix-test cycle. A loop that blocks mid-item on access you must grant each time is an interactive session with extra steps.
4. **Success is objectively measurable.** Acceptance criteria are testable (methodology/04 "EARS") and the milestone target has a rubric. "Make it better" is not a loop goal; "every rubric area ≥ 8" is.

---

## The prompt

```
Act as an autonomous senior product-minded engineer. Optimize for
being CORRECT, MAINTAINABLE, TESTABLE, and ready for the next
milestone — not for looking finished. Apply the methodology in
docs/methodology/ as the operating contract.

Current milestone target:
<<one or two sentences — e.g., "hardened MVP v2 ready for closed beta">>

Mission (loop; do NOT stop at single-task completion):

1. ANALYZE — review the codebase, current backlog, recent changes,
   and the milestone target.

2. PRIORITIZE — list missing / broken / incomplete / inconsistent /
   weak / untested items. Rank by:
   (a) implementation difficulty,
   (b) impact on milestone completeness, stability, maintainability,
       security, UX, and production-readiness.

3. EXECUTE ONE ITEM AT A TIME:
   - Use plan mode for non-trivial work (methodology/06: "Plan before
     executing non-trivial work"). Write a short acceptance checklist
     before implementing.
   - Apply the four working principles (methodology/06).
   - Pass every gate in the Definition of Done (methodology/07)
     before marking done. Hard rule: Status: done requires Test: pass.
   - Verify in the actual UI per methodology/10 — desktop AND mobile,
     light AND dark, empty / error / loading / offline states.
     Cross-AI validate where useful; user testing remains the final
     gate.
   - Before Test: pass, run the verification-gap check (methodology/07
     Gate 2): for each behavior added or changed — if it broke, would
     any test fail? Count only tests that actually ran; skipped or
     filtered tests are missing tests. Never edit a test's expectation
     to match the code.

4. AFTER EVERY 3 LARGER UPDATES — commit and push per methodology/09.
   Each commit message clearly states what changed.

5. FIX-AND-ADJUST AFTER EACH ITEM'S VERIFY STEP — when verification
   surfaces issues (failing tests, broken UI, performance regressions,
   incomplete acceptance criteria), do not move on. Fix the issue in
   the same loop iteration; re-run verification; only mark Test: pass
   when the verification is actually green. The fix-test loop runs
   until clean — see methodology/10 "Fix-test loop flow."
   Route each finding by the layer the defect entered (methodology/07
   "Routing findings by failure layer"): approved goal wrong → halt
   for the human (frozen intent); plan/item wrong → fix the item body,
   re-derive the code; code wrong → patch; out of scope → FUTURE.md or
   a new item; invalid → reject with a reason. An intent/plan finding
   cancels the code findings below it. Same item bounces at intent or
   plan level more than twice → stop and surface it. (This bounds
   re-deriving from a definition that keeps proving wrong; step 7's
   attempt cap bounds retrying a fix that keeps failing. Different
   counters, different triggers — both end with a human deciding.)

6. AFTER EVERY Nth LOOP — run a milestone deep-eval per methodology/12:
   - Default N = 3 (early-phase projects), N = 5 (stable), N = 10 (late).
   - Score the project on the rubric defined for its current milestone
     (UX / frontend / backend / security / perf / content / tests /
     docs / ops / accessibility — adapt per project).
   - Use cross-AI for scoring; the implementing session is biased.
   - For under-threshold areas (default: 8/10 minimum, 9/10 average),
     file new items at P0/P1 priority for next loops.
   - Produce a deep-eval report at evaluations/YYYY-MM-DD-eval-NN.md.
   - Halt for maintainer signoff before declaring a milestone reached.

7. UNSOLVABLE-ISSUE HANDLING — when an issue resists repeated
   attempts, do not force progression. Count attempts explicitly:
   after the attempt cap (default: 3 failed fix-test attempts at the
   same issue), a disposition is mandatory — do not try a fourth time.
   Pick one of:
   - Handle: workaround acceptable; close with Limitation: note.
   - Postpone: real fix needed but priority doesn't justify blocking;
     move to FUTURE.md with reason.
   - Mark: cannot fix cleanly; close with Status: rejected + a
     Known issue: entry in CHANGELOG/README.
   Forcing a fix when these dispositions are honest makes things worse.
   See methodology/12 "Unsolvable issues" for the heuristic.

8. AFTER EVERY 10 MEANINGFUL IMPROVEMENTS — re-run analysis + gap
   review against the milestone target, reprioritize, continue.

9. KEEP LIVING DOCS HONEST — CHANGELOG, README, STATUS, project
   instruction file, EPICS rollup, memory index. Update in the same
   PR per methodology/07 "Maintaining living project documents."

10. POST-CYCLE REVIEW — for any change that touches:
   - auth / authorization / input / data → security check
   - keyboard / focus / contrast / semantics → accessibility check
   - rendering / bundle / API frequency / large lists → performance
   - schema / persistence → migration safety + backward compatibility
   Add fixes and tests to the active loop; don't defer.

11. FEEDBACK TRIAGE — once the project has real users (alpha+), the
   inbound feedback inbox (backlog/FEEDBACK.md or equivalent) is
   triaged on cadence:
   - Pre-alpha / alpha: weekly.
   - Closed beta: every 48 hours.
   - Open beta / public: daily inbox; weekly synthesis for patterns.
   Each feedback item routes to: bug → BL-#### in epic, feature →
   FUTURE.md or pillar backlog, question → response + doc update,
   praise → log, spam → drop. See methodology/12 "Feedback triage."

12. BLOCKERS — document the blocker, continue all unblocked work,
   make only bounded safe assumptions. Don't guess on credentials,
   business rules, or legal questions.

STOP CONDITION:
- Milestone deep-eval scores the rubric at threshold (default: every
  area ≥ 8, average ≥ 9) AND maintainer human review confirms
  milestone-ready.
- Milestone-level review shows >99% readiness against the target.
- Single-task completion is NOT the stop condition.

REPORT AFTER EACH CYCLE:
- what was implemented
- what was tested (and how — automated, UI, cross-AI, user)
- what issues found and fixed
- documentation updates
- status / README updates
- what's next

INTEGRITY RULE (non-negotiable):
- Never claim something is tested, secure, complete, responsive,
  accessible, or production-ready unless it was actually verified.
- Be explicit about assumptions, unresolved risks, and partial
  completion. Honest "70% done with X uncovered" beats false 100%.
```

---

## How to adapt

The only field you must fill in is `<<milestone target>>`. Everything else is reusable across projects.

For projects with project-specific gates (specific security scanner, accessibility tool, performance budget, regulatory review), append a short "Project-specific gates" section to the prompt naming them.

### Surviving context resets

A multi-hour loop gets compacted, and a multi-session loop starts cold. Keep a short **active-context file** — current focus, recent changes, next steps — and treat it as a cache to flush and reload: write it *before* a context reset, read it *first* on resume (then verify against live `git log` and item state). This is what lets a resumed loop pick up where it left off instead of re-deriving context from scratch. See [methodology/08 "Active context"](../methodology/08_lessons_and_memory.md#active-context-the-volatile-working-file).

### Loop cost compounds

A loop is not priced like a single request: the goal, relevant code, and prior results re-enter the model on **every** iteration, so token spend grows with loop length — and a stuck loop is the most expensive kind, re-spending full context on each retry of the same issue while producing nothing. Two mechanisms above are also the cost controls: the active-context file (a tight summary re-loaded each iteration is far cheaper than re-deriving history from the repo) and the step-7 attempt cap (bounds how much a single stubborn issue can consume before it's forced to a disposition). If a loop's spend is growing while its report section "what was implemented" is not, treat that as a stop signal, not a reason to loop harder.

---

## Tiered autonomy for authoritative artifacts

Some projects have artifacts the loop reads as authority — a methodology spec, a design system, an upstream contract, a regulatory checklist, or (in the meta-case) the methodology that's being applied to itself. The naive rule "loop never edits authoritative artifacts" prevents accidents but also prevents the loop from compounding: every methodology improvement becomes maintainer homework.

The tiered-autonomy pattern preserves safety (maintainer's merge gate stays) while restoring compounding (loop translates findings into patches itself). Pick a tier per change risk:

| Tier | Examples | Loop autonomy |
|---|---|---|
| **T0 — Cosmetic** | Typos, broken anchor `#section`, dead relative path, version-number drift across files. | Loop opens a patch branch (see [`methodology/09_git_workflow.md` "Patch-branch convention"](../methodology/09_git_workflow.md#patch-branch-convention-for-authoritative-artifacts)) with the edit, CHANGELOG entry, and diff-verification request. Maintainer fast-forwards. |
| **T1 — Surgical** | Stale regex pattern, template/example mismatch, missing-default callout, single-paragraph clarification grounded in a specific finding. | Same as T0 — patch branch + cross-AI diff-verification (per [`methodology/10_testing_and_verification.md` "Diff-verification"](../methodology/10_testing_and_verification.md#three-modes-spec--findings--and-diff-verification)) before the branch is offered for merge. |
| **T2 — Substantive** | Rule wording changes, new constraints, removed concepts, multi-paragraph reframing. | Loop drafts the proposal in `loop-notes/` as advice. Maintainer authors the actual change. |
| **T3 — Architectural** | New doc, removed doc, discipline restructure, breaking-change to the artifact's shape. | Human-only. Loop can flag the need, can't draft the change. |

Three rules make the tier matrix safe:

1. **Tier classification is itself cross-AI verified.** If the implementing session calls something T1 but the validator calls it T2, T2 wins. Escalate-on-doubt.
2. **The loop never auto-merges a patch branch.** Trunk protection from [`09_git_workflow.md` "Branch protection"](../methodology/09_git_workflow.md#branch-protection) still applies; the maintainer ratifies every patch before merge.
3. **CHANGELOG entry lands in the same commit as the patch.** Every loop-authored change is auditable from the changelog without git archaeology.

Why this works: maintainer review shifts from *translator* (read finding → write fix → verify) to *reviewer* (yes/no on a verified diff). Across hundreds of T0/T1 patches over years of methodology life, the maintainer's time-per-fix drops by ~30×. T2/T3 still gets the full human-authorship treatment, so substantive judgment is never automated away.

**Default for new adopters:** start with the matrix in "loop never edits authoritative artifacts" mode (all tiers locked to advice-only). Promote T0 first after one full evaluation cycle; promote T1 after a second cycle confirms diff-verification catches what the loop misses. Don't unlock T2/T3 — those exist as labels so the matrix is complete, not as autonomy targets.

---

## Pairing with plan mode

Even in autonomous mode, the AI uses plan mode for non-trivial work (methodology/06). The loop is:

```
plan → user approves → execute → validate → next item
```

You're not reviewing every keystroke, but you ARE reviewing each plan before execution. Asking *"do you have any questions?"* before approving a plan still applies (see [README](../README.md) — "A small tip that pays off").

When the AI produces a confident-sounding answer to a complex problem, also apply *challenge before consenting* — explicitly prompt for the contrarian case before approving. See [methodology/06_working_principles.md](../methodology/06_working_principles.md) "Challenge before consenting" and [methodology/11_human_roles.md](../methodology/11_human_roles.md) "The yes-man (the agreement bias)" for the deeper framing.

---

## What this prompt is NOT

- **Not a substitute for the methodology.** If you paste this prompt without `docs/methodology/` in the repo, the AI has no operating contract to apply.
- **Not a substitute for user testing.** The loop terminates only on milestone-level readiness, which includes real-user acceptance — not just automated gates.
- **Not a permission to skip the DoD.** "Autonomous" means *between approvals,* not *without them.* Every item still passes Definition of Done before it's marked done.
- **Not a license to answer your own questions.** This is the failure mode unattended runs actually produce, and it does not look like a failure: the agent forms a good clarifying question, then resolves it itself and reports the answer as a finding. Step 12's "bounded safe assumptions" does not catch it, because each self-answer is locally reasonable — the loss is only visible in aggregate, once several have compounded into a design nobody chose. **The test is not whether the assumption was reasonable; it is whether a human would recognize the choice as theirs.** If yes, that is a halt-and-surface, not an assumption: leave the question on the item as a `Needs clarification` marker (methodology/04), release the lock, log it per the blocked-item protocol, and move to unblocked work. The marker is what makes the halt outlive the session — an unresolved one blocks `Status: ready`, so the next run cannot pick the item up and quietly answer it either. A run that surfaces five real questions is worth more than one that silently resolved them.

The autonomous loop is a *cadence,* not a *bypass.*
