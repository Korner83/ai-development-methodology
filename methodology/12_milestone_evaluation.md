# 12 — Milestone-driven evaluation and feedback flow

> **Purpose:** define how a project measures *whether it is ready for the next milestone* — beyond per-item DoD. Per-item gates (doc 07) catch whether a single change is correct; this doc catches whether the *accumulated* changes have moved the project closer to its goals. Pairs with the autonomous-loop pattern in `templates/AUTONOMOUS_LOOP.md`.

Per-item testing alone is insufficient at scale. A hundred items can each pass their DoD while the *overall* product is unfit to ship. The milestone-evaluation loop catches the gap.

This doc operationalizes four ideas:

1. **Milestones are explicit waypoints** (alpha → closed beta → open beta → first public → general availability), each with binary readiness criteria.
2. **Periodic deep-eval** runs every Nth loop iteration to score the project against the *next* milestone, not against ad-hoc gates.
3. **Per-area scoring** uses a 0–10 rubric across the dimensions that matter for this project (UX, frontend, backend, security, performance, content quality — adapted per project).
4. **Unsolvable issues are first-class** — the loop labels them, sequences around them, and never forces progression that would make things worse.

The whole structure exists to keep loops honest: per-item green ≠ milestone-ready.

---

## Why per-item DoD is not enough

The per-item DoD (doc 07) asks: *did this change pass its own gates?* It catches single-change defects.

It does not catch:

- **Compounded UI debt** — every change individually fine; the product collectively feels broken because consistency degraded across a dozen changes.
- **Cross-cutting performance regressions** — each item shipped its perf budget; the aggregate page load is now 8 seconds because no item owned the sum.
- **Security drift** — no single item introduced a vulnerability; the combination of three items exposed an IDOR.
- **Strategy/pillar drift** — items shipped per their epic charters; the epics themselves drifted from the pillar; pillar drifted from the strategy; the project is now solving a different problem than it set out to solve.
- **User-experience cohesion** — twelve features land; users still can't accomplish their job because no one tested the *journey* end-to-end.
- **Content quality erosion** — copy was written per-item by different agents; the product's voice is now inconsistent.

The milestone-evaluation loop is the corrective. Every Nth iteration of the autonomous loop, the project scores itself against the *next milestone's* readiness criteria — not against per-item DoD. The aggregate matters; per-item green is necessary but not sufficient.

---

## Milestones: the readiness waypoints

A project moves through a sequence of named readiness states. The names matter because they communicate *expected quality* to internal contributors and external observers.

### The standard sequence

| Milestone | Audience | Bar |
|---|---|---|
| **Pre-alpha** | Maintainer only | Code compiles, primary happy path works, no public exposure. Internal-only validation. |
| **Alpha** | Trusted internal users (≤ 5) | Core feature set demonstrably works; obvious bugs absent; UI may be rough; no SLA. |
| **Closed beta — wave 1 (friends)** | Maintainer's network (≤ 10) | Stable enough that friends will trust it for real (low-stakes) use. Acquisition signals start being measurable. |
| **Closed beta — wave 2 (strangers)** | Curated external users (≤ 50) | Onboarding works for users without context. Failure modes have explanations. Feedback flow is operational. |
| **Open beta** | Public, opt-in | Anyone can sign up. Free tier is meaningful. Quality bar is "trustworthy enough that bad PR is unlikely." |
| **First public final (v1.0)** | Public, advertised | The project's headline promise is delivered. Pricing (if any) is committed. Removal of "beta" label means the maintainer is willing to be quoted on its readiness. |
| **General availability** | Public, scale-tested | Has handled meaningful load; ops on-call exists; SLA published. |

Projects adapt the sequence. A solo CLI tool may collapse `closed beta` and `open beta` into one. A regulated-industry product may insert `compliance review` between open beta and v1.0. A research artifact may skip the betas entirely and ship to "public preview" directly. **Pick the sequence that fits the project; name it explicitly in the strategy doc.**

### Each milestone is binary

A milestone is reached or it isn't. "We're sort of in beta" is a smell — it means the team is calling itself one thing while operating as another. The readiness criteria for the milestone are the binary check.

### Each milestone has explicit readiness criteria

The criteria live in the strategy master plan (doc 01) or in a dedicated `milestones.md` referenced from there. Format suggestion:

```markdown
## Milestone: Closed beta (wave 2)

**Audience:** ~50 curated strangers (acquisition via 3 channels).

**Readiness criteria (binary):**

- [ ] Onboarding flow tested by ≥ 3 strangers without maintainer intervention; ≥ 2 succeeded.
- [ ] Crash rate < 1% over 7-day window.
- [ ] All P0 + P1 items closed.
- [ ] Pricing page published if monetization is a beta concern; deferred otherwise.
- [ ] Feedback inbox has a defined triage cadence (e.g., within 48h).
- [ ] Scoring rubric (see below) averages ≥ 9.0/10 across all areas with no area below 8.0.

**Exit criterion:** maintainer reviews the rubric and signs off explicitly.
```

The criteria are the eval target. Per-item DoD continues to gate individual changes; readiness criteria gate milestones.

---

## The scoring rubric: 0–10 per area

The rubric is the operational tool the milestone-evaluation loop uses. It scores the project on the dimensions that matter for this project, on a 0–10 scale.

### Standard scoring areas

Adapt per project. A common starting set:

| Area | What 10/10 means | What 0/10 means |
|---|---|---|
| **UX/UI** | Every flow lands; no broken states; navigation is unambiguous; visual quality is at-or-above adopter expectations for this product class. | Users get stuck; key flows broken; visual quality embarrassing. |
| **Frontend** | No console errors; assets cached correctly; bundle size under budget; works in target browsers + viewports. | Console errors per page; load times exceed budget; broken in target browsers. |
| **Backend** | All APIs respond correctly; no N+1 queries on hot paths; error responses are structured; uptime > target. | APIs throw 500s on common inputs; slow queries; opaque errors. |
| **Security** | Auth/authz correct; input validation present; no exposed secrets; OWASP-relevant categories audited. | IDOR present; secrets in commits; auth bypass possible. |
| **Performance** | p50 / p95 latencies under budget; bundle sizes under budget; perf budget enforced in CI. | Pages > 5s on target hardware; perf budget unenforced. |
| **Test coverage** | Behavior tests cover all critical paths; regression tests for every fixed bug; suite runs in CI. | Critical paths untested; bugs recur because regression tests missing. |
| **Content quality** | Copy is consistent in voice; no typos in user-visible text; placeholder content removed; translations (if any) parity-checked. | Inconsistent voice; placeholder text in production; broken translations. |
| **Documentation** | Adopter can set up the project from README alone; key concepts have docs; CHANGELOG honest. | Setup requires asking; docs contradict code; CHANGELOG outdated. |
| **Operational readiness** | Deploy is reversible; monitoring exists; incident response documented; on-call rotation defined if applicable. | Deploys break things irreversibly; no monitoring; no incident playbook. |
| **Accessibility** | Keyboard navigation works; focus states visible; contrast meets WCAG AA; screen reader can use core flows. | Keyboard navigation broken; focus invisible; failed contrast; screen reader blocked. |

**Add or drop areas based on the project's domain.** A regulated-industry product adds `Compliance`. A research artifact adds `Reproducibility`. A consumer mobile app adds `Mobile UX (iOS vs Android parity)`. **Document the chosen areas + 10/10 definition per area in the strategy doc or `milestones.md`.** A score is only meaningful if "10/10" has a project-specific definition.

### AI can help define the areas

When a strategy is drafted, the maintainer can ask a fresh AI session: *"For a project of shape X with users Y and milestone Z, what are the right scoring areas, and what does 10/10 mean for each?"* The AI's first-pass list, refined by the maintainer, is the project's rubric. This is a one-time setup activity per milestone; the rubric stabilizes across the milestone's eval cycles.

### Score thresholds (default starting point)

For a project to declare it has reached a milestone:

- **Minimum score per area: 8/10.** No area can be under-served. An average of 9 with a 4 in security is a security-broken product; the minimum-per-area rule prevents averaging away critical gaps.
- **Average across all areas: 9.0/10.** Overall quality matters; if every area is 8, the product is shippable but rough; 9 average means it feels like a finished thing.
- **Project may raise these thresholds** for high-stakes milestones (e.g., GA: minimum 9, average 9.5). Project may lower them for early milestones (e.g., alpha: minimum 6, average 7). Pick deliberately and document in strategy.

### Scoring discipline

Each periodic deep-eval produces a single rubric pass. Scores are integers 0–10 with a one-paragraph justification per area (cite evidence — specific items, bug reports, test results, log samples, user feedback). The justification is more important than the number; the number is the summary.

**Use cross-AI for scoring, not the implementing session.** A session that wrote the code is biased toward charity. A fresh session with read-only access to the codebase, the strategy doc, the rubric, and recent test/log/feedback data scores more honestly.

---

## The periodic deep-eval cadence

The per-item DoD runs every item. The periodic deep-eval runs every Nth loop iteration.

### Picking N

- **N = 3** for early-phase projects, where direction may still be uncertain and frequent rubric checks keep the team aligned to the strategy.
- **N = 5** for stable-phase projects, where loops are productive and frequent evaluation would slow throughput.
- **N = 10** for late-phase projects approaching maturity, where evaluation focuses on regressions rather than direction.

Adopters tune per project. The point is *predictable cadence*, not a specific number. A team that "evaluates whenever it feels right" doesn't evaluate.

### What runs in a deep-eval

1. **Re-read the next milestone's readiness criteria.** Re-establish what "ready" means.
2. **Score each rubric area** (cross-AI session, evidence-cited justifications).
3. **Compare scores to thresholds.** Identify which areas are under threshold.
4. **For each under-threshold area:**
   - Identify the items / commits / behaviors driving the low score.
   - File new items in the appropriate epic to address them.
   - Re-prioritize: under-threshold areas get P0/P1 priority for the next loop cycles.
5. **Identify unsolvable issues** (see next section) and route them.
6. **Produce an eval report** in `evaluations/YYYY-MM-DD-milestone-eval-NN.md` with: scores per area, items filed, milestone-readiness verdict.
7. **Maintainer signoff on the eval report.** Same gate as the semi-annual self-evaluation (doc 07).

### When N=3, here's the loop shape

```
Loop 1: items → DoD → ship.
Loop 2: items → DoD → ship.
Loop 3: items → DoD → ship → DEEP EVAL → fix-and-adjust based on scores → file new items.
Loop 4: items (including new ones from Loop-3 eval) → DoD → ship.
Loop 5: items → DoD → ship.
Loop 6: items → DoD → ship → DEEP EVAL → ...
```

The deep-eval is not a separate loop; it's an extra step at the end of every Nth loop. The next loop picks up the items the deep-eval filed.

### When to skip the cadence

- **The deep-eval reveals a milestone is already met.** Move to the next milestone; reset N to that milestone's cadence.
- **A blocker emerges that makes scoring moot.** Address the blocker first; the next loop's deep-eval covers the missed cycle.
- **The project is between milestones** (e.g., shipping post-1.0 maintenance). The cadence may drop to N = 10+ or pause until the next major milestone is defined.

---

## Unsolvable issues: handle, postpone, or mark — never force

Some issues do not yield to additional loop iterations. The methodology is honest about this.

### The three legitimate dispositions

| Disposition | When to use | What it means |
|---|---|---|
| **Handled** | A workaround exists that's good enough for the current milestone. | Item closes with `Status: done`; a `Limitation:` note in the item body documents the workaround. |
| **Postponed** | The issue's correct fix is real but its priority doesn't justify blocking the current milestone. | Item moves to `FUTURE.md` with a postponement reason; re-surface at the next milestone planning cycle. |
| **Marked (known-broken)** | The issue can't be fixed cleanly within the project's constraints, and forcing a fix would make things worse. | Item closes with `Status: rejected` + a `Known issue:` documentation entry in CHANGELOG / README. User-facing if it affects users. |

### What "forcing a fix would make things worse" looks like

- **The fix requires a refactor whose scope exceeds the original problem.** A 50-line bug fix becomes a 5000-line architectural rewrite; the rewrite introduces new bugs at higher rate than the original bug caused harm.
- **The fix is a hack that papers over a structural issue.** The hack will accumulate technical debt; the next eval cycle will surface it again at higher cost.
- **The fix requires breaking a public contract** (API, file format, URL scheme) and the breakage cost exceeds the issue cost.
- **Multiple loop iterations have produced regressions, not progress.** Pattern recognition: if loops N, N+1, N+2 all attempted the same issue and each shipped a regression, the issue is not loop-solvable.
- **The implementing agent and cross-AI validator disagree** on whether a proposed fix is correct, after multiple iterations. Confidence on both sides has degraded; ship-quality fix is unlikely from the current approach.

### The discipline of marking

When an issue is **marked**:

1. The item gets `Status: rejected` (per doc 04 lifecycle).
2. The item body documents *why* (one paragraph): what was tried, why it failed, what would be required to fix it.
3. A `Known issue:` entry lands in the user-facing documentation (CHANGELOG.md "Known issues" section; README.md "Limitations" section).
4. If the issue affects users, the documentation is honest about the impact + workaround.
5. The next milestone-evaluation cycle considers whether the issue still warrants marking (situations change; what was unsolvable in alpha may be solvable in beta).

**The discipline matters because the alternative is worse.** A team that refuses to mark issues will either ship broken work or stall indefinitely. The methodology's stance: marking is honest; forced progression is dishonest.

---

## Human review remains the final gate

Even when the rubric scores 9+ across the board and the milestone criteria are met, the maintainer's human review is the final gate before milestone declaration.

### Why

The rubric measures what it knows how to measure. A 10/10 UX score from a cross-AI session and an unbiased automated test suite still cannot replace a human's intuition about whether the product *feels right*. The methodology defers to human judgment on intuition-grade questions (per [doc 11 "Decision-ownership matrix"](11_human_roles.md#the-decision-ownership-matrix) → human-only column).

### What the human review checks

After the rubric passes and items are closed:

1. **Actual user testing.** Real users (or representative testers) try the product unscripted. The maintainer watches and notes friction the rubric didn't catch.
2. **Strategy alignment.** Does what shipped match the strategy's intent? Not just "did we ship X" but "is X the X we meant to ship."
3. **Trade-offs revisited.** Did the loop optimize for the rubric in ways that hurt unmeasured dimensions? (Goodhart's law applies to rubrics too.)
4. **Confidence to claim the milestone.** Would the maintainer be comfortable telling external users "we're now in beta"? The intuition matters.

### After the review

- **If accepted:** the milestone is declared. CHANGELOG entry. README badge updated. Maintainer announces (per project's distribution plan).
- **If accepted with conditions:** specific gaps filed as P0 items; one more loop cycle resolves; re-review.
- **If rejected:** rubric was misleading or the maintainer's intuition surfaces something the rubric missed. The rubric itself may need refinement (file as a rubric-update item).

---

## The feedback triage flow

Once a milestone is reached (especially closed beta or later), real users start submitting feedback. The backlog must support fast triage so feedback doesn't pile up unprocessed.

### The flow

```
Inbound feedback (email / GitHub Discussion / form / app-internal report)
    ↓
Single inbox: backlog/FEEDBACK.md (append-only NDJSON or single markdown file)
    ↓
Triage cadence (every N hours / daily / weekly — pick per project)
    ↓
For each feedback item:
    ├─ Classify: bug / feature request / question / praise / spam.
    ├─ If bug: file as BL-#### in appropriate epic with `Reported-by:` field.
    ├─ If feature request: file in FUTURE.md or relevant pillar's backlog.
    ├─ If question: respond + consider whether the docs need an addition.
    ├─ If praise: log for sentiment tracking; consider testimonial use.
    └─ If spam: drop.
    ↓
Reply to the user (where possible) with what was filed + ID.
    ↓
The next loop cycle picks up the new items per ROI heuristic.
```

### Why this matters

- **Feedback is the leading indicator** of milestone-progression risk. A spike in bug reports at closed-beta wave-2 is a signal the milestone declaration was premature.
- **Slow triage erodes user trust.** A user who reports a bug and never hears back stops reporting. The information channel closes.
- **The backlog stays connected to reality.** Without a feedback flow, the backlog becomes an internal-only artifact disconnected from what users actually hit.

### The FEEDBACK.md pattern

Two formats work:

**Format A — single markdown file**, one section per feedback item:

```markdown
# Feedback inbox

## FB-0001 — 2026-05-25 — Email — "Onboarding broken on Safari"

Reported by: jane@example.com
Triaged by: maintainer
Disposition: filed as BL-0428 in E03 (browser-compat epic)
Reply sent: 2026-05-26 12:00 UTC

> Original message:
> "I tried signing up and the page just stays blank in Safari…"
```

**Format B — append-only NDJSON** (for projects with feedback volume that justifies tooling):

```json
{"id":"FB-0001","ts":"2026-05-25T14:00Z","src":"email","reporter":"jane@example.com","subject":"Onboarding broken on Safari","status":"triaged","filed_as":"BL-0428"}
```

Either is fine. Pick one and stay consistent.

### Triage cadence recommendation

- **Pre-alpha / alpha:** weekly. Volume is low; cadence is just discipline.
- **Closed beta:** every 48 hours. Real users; trust depends on responsiveness.
- **Open beta / public:** daily or sub-daily for inbox; weekly for synthesis (patterns across items).

The cadence is a project decision, but **a cadence must exist**. "We'll get to it when we get to it" is the failure mode.

---

## How this doc fits the rest of the methodology

- **Per-item DoD ([doc 07](07_definition_of_done.md))** continues to gate every change. This doc adds an *aggregate* gate on top.
- **Working principles ([doc 06](06_working_principles.md))** apply at item-level. Milestone evaluation tests whether the principles were *consistently* applied across many items.
- **Cross-AI validation ([doc 10](10_testing_and_verification.md))** is the mechanism the scoring rubric uses. The rubric is the *what*; cross-AI is the *how*.
- **The autonomous loop ([`templates/AUTONOMOUS_LOOP.md`](../templates/AUTONOMOUS_LOOP.md))** runs the per-item work; this doc defines the periodic deep-eval that runs every Nth iteration.
- **Backlog items ([doc 04](04_backlog_items.md))** are where deep-eval outcomes land: new items for under-threshold areas, postponed items for unsolvable-now issues, marked items for permanently-rejected ones.
- **Strategy ([doc 01](01_strategy.md))** is where milestones + readiness criteria live. The rubric areas + thresholds live in strategy or in a `milestones.md` referenced from strategy.
- **Decision-ownership matrix ([doc 11](11_human_roles.md))** establishes that milestone declarations + final acceptance are human-only.

---

## A worked example of the loop in action

A fictional project at end of Loop 3 (the deep-eval loop). The project's milestone target is "Closed beta wave 2"; rubric is the standard 10-area set; thresholds are minimum 8, average 9.

**Loop 3 wraps:**

1. Per-item DoD passed on all 4 items shipped in Loops 1–3.
2. Deep-eval triggers. Fresh Sonnet session reads strategy, milestones doc, recent commits, test output, and the current user-feedback queue.
3. Scores:
   - UX/UI: 8 (one onboarding step still confuses ~30% of testers — close to threshold but acceptable).
   - Frontend: 9.
   - Backend: 7 ← **below threshold.** (Slow login query under load; structured-error coverage incomplete.)
   - Security: 9.
   - Performance: 8.
   - Test coverage: 6 ← **below threshold.** (Three new endpoints shipped without test coverage.)
   - Content quality: 9.
   - Documentation: 8.
   - Operational readiness: 7 ← **below threshold.** (No incident playbook; deploy-rollback untested.)
   - Accessibility: 8.
   - **Average: 7.9. Below 9.0 milestone threshold.**
4. Deep-eval files new items:
   - 2 P0 items in backend epic (login-query optimization; error-response audit).
   - 1 P0 item in QA epic (backfill tests for the 3 new endpoints).
   - 1 P1 item in ops epic (write the incident playbook; test the rollback).
5. **Unsolvable check:** none in this batch — all four items have known solutions.
6. **Milestone-readiness verdict:** NOT READY. Continue loops.

**Loops 4–5 close the new items.**

**Loop 6 wraps; deep-eval runs again:**

- Scores: average 9.2, no area below 8. **THRESHOLD MET.**
- Maintainer reviews the eval report.
- Maintainer runs actual user testing (3 strangers, 2 succeed unsupervised).
- Maintainer signs off: closed beta wave 2 declared.

**The cycle moves to the next milestone (open beta) with its own readiness criteria and (possibly) a refined rubric.**

---

## Authority

When the milestone evaluation and per-item DoD conflict — e.g., an item passes its DoD but moves a rubric area further from threshold — **the rubric wins** for milestone progression. The item still ships (its DoD is valid); the deep-eval simply files compensating items to bring the area back.

When the maintainer's human review and the rubric conflict — e.g., rubric says READY but the maintainer's intuition says NOT READY — **the maintainer wins**. The rubric measures what it knows; the maintainer measures the unmeasured (per [doc 11](11_human_roles.md)).

When the unsolvable-issue heuristic says "mark" and a contributor's energy says "let's try one more time" — **the heuristic wins by default**, overridden only by explicit maintainer authorization. The cost of forcing the issue exceeds the cost of marking it.

---

**Next:** with the milestone evaluation pattern in place, the methodology has its full vertical: strategy → pillars → epics → items → DoD per item → milestone eval across items → human review at milestone declaration. Adopters can run a project end-to-end through this stack with high autonomy and high quality.
