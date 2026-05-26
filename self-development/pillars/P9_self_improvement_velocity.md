# P9 — Self-improvement velocity

> **Pillar goal:** the methodology improves itself via the self-development cycle, faster than ad-hoc maintenance could — and the loop's outputs compound across phases.
>
> **Last updated:** 2026-05-25

**Related:**
- Brief: [Capability layer 9](../brief/08_capability_layers.md#9-self-improvement-velocity)
- Strategy phase: **all four phases** (primary throughout — this is the cross-cutting mechanism)
- Depends on: [P1 Doc completeness](P1_doc_completeness.md), [P3 Doc currency](P3_doc_currency.md), [P7 Community feedback loop](P7_community_feedback_loop.md), [P8 Maintenance sustainability](P8_maintenance_sustainability.md)
- Feeds into: every other pillar (the loop's outputs become methodology improvements that elevate every layer)
- Delivering epics: (none yet)

## 1. Overview

This is the **compounding mechanism** for the entire project. If the methodology gets better on its own through the self-development cycle, every other pillar benefits. If the cycle stalls, the methodology is static.

The cycle structure (per the [self-development bootstrap plan](../../README.md) and [self-development/strategy/00_master_plan.md](../strategy/00_master_plan.md)):

```
1. Apply the methodology to its own development.
2. Notice gaps, friction, missing patterns during loop runs.
3. Memory entries surface; clusters become methodology improvements.
4. Improvements ship as methodology releases.
5. Next loop run benefits from improved methodology.
```

This is the only pillar that's **primary in every phase** of the strategy. Phase 1 bootstraps the cycle (Steps 0–4 of the self-development bootstrap); Phase 2+ exercises the cycle and harvests improvements.

The pillar's existence is what makes the project's vision sustainable: maintainer hours don't scale linearly with adoption because the cycle absorbs recurring work into the methodology itself.

## 2. What this pillar covers

| Cycle component | What "operational" means here |
|---|---|
| **Self-development folder** | `self-development/` exists, is populated through Step 4 of the bootstrap, mirrors the methodology's own [PROJECT_STRUCTURE.md](../../templates/PROJECT_STRUCTURE.md). |
| **Autonomous loop** | `self-development/AUTONOMOUS_LOOP.md` adapted from the template; constraints, stopping conditions, targets defined. Loop can run unsupervised between user check-ins. |
| **Memory hygiene** | The loop records insights as memory entries (or notes that become memory entries). Maintainer reviews memory periodically per the [stdlib growth loop](../../methodology/08_lessons_and_memory.md#the-promotion-path-from-one-off-correction-to-durable-rule). |
| **Methodology promotion** | Clusters of memory entries become methodology improvements via the existing promotion path. Improvements ship as releases. |
| **Cycle attribution** | CHANGELOG entries explicitly note "this came from the self-development cycle" for shifts the loop produced. |
| **Cycle health** | Cycle operates within constraints (doesn't damage abstract methodology docs autonomously, surfaces blockers to HUMAN_NEEDED.md, etc.). |

## 3. Exit criteria

The pillar is *delivered* (evergreen) when:

- [ ] Steps 0–4 of the self-development bootstrap are shipped (v1.7.0 through v1.x with autonomous loop config).
- [ ] At least one autonomous loop run has completed end-to-end without maintainer intervention mid-run.
- [ ] The cycle has shipped methodology improvements (not just self-development cleanup); CHANGELOG entries attribute specific changes to cycle output. See [brief/05_success_metrics.md "Early signals"](../brief/05_success_metrics.md#early-signals-within-12-months).
- [ ] The cycle has surfaced patterns the solo maintainer wouldn't have discovered alone — measured by the maintainer's "this came from the cycle" notes in CHANGELOG. See [brief/05_success_metrics.md "Sustained signals"](../brief/05_success_metrics.md#sustained-signals-multi-year).
- [ ] The cycle has not damaged the abstract methodology docs via the autonomous loop (no incidents where the loop touched `methodology/*.md` without explicit user direction).

**Re-tested:** every methodology release that came from the cycle (per the attribution criterion); quarterly during Phase 2 to verify cycle health.

## 4. Dependencies

**Depends on:**

- [P1 — Doc completeness](P1_doc_completeness.md). The cycle can only improve what exists. A methodology with gaps too large can't be improved by the cycle alone.
- [P3 — Doc currency](P3_doc_currency.md). The cycle works on the current methodology; stale docs send the cycle in the wrong direction.
- [P7 — Community feedback loop](P7_community_feedback_loop.md). Cycle improvements are even better when informed by community feedback (Phase 2+).
- [P8 — Maintenance sustainability](P8_maintenance_sustainability.md). The cycle is what makes sustainability achievable; the two are mutually reinforcing.

**Feeds into:** every other pillar. Cycle outputs are methodology improvements that elevate every other capability layer.

## 5. Anti-patterns

- **Treating the cycle as autonomous in everything.** The cycle has constraints (no autonomous changes to abstract methodology docs; no third-party PRs; no production deploys). Letting the loop expand its scope produces incidents.
- **Setting milestone targets the loop can't reach.** If the loop's target is "achieve 500 stars," the loop has no leverage — that's adopter behavior. Targets must be actionable by the loop itself.
- **Skipping the user check-in.** The user is the gate at the milestone level. Cycle runs that bypass user review and ship directly to main bypass the methodology's own DoD.
- **Letting cycle outputs ship without cross-AI review.** The methodology's [cross-AI validation](../../methodology/10_testing_and_verification.md#cross-ai-validation) is a gate; the cycle doesn't skip it.
- **Mistaking activity for improvement.** A cycle that runs and runs but produces no real methodology improvements is overhead, not value. Measure outputs (releases shipped, patterns surfaced), not runtime.
- **Ignoring the cycle's cost in compute / tokens.** The cycle runs on AI tools that cost money. Sustainable cost is part of P8 sustainability; not a separate concern but worth noting here.

## 6. Current state (v1.8.0)

**Bootstrap progress:**

- ✓ Step 0 (brief) shipped in v1.7.0.
- ✓ Step 1 (strategy + pillars) shipping in v1.8.0 (this release).
- Pending: Step 2 (first epics) — will ship as the next release.
- Pending: Step 3 (first items) — will ship after Step 2.
- Pending: Step 4 (autonomous loop config) — will ship after Step 3. **This is the moment the pillar becomes truly testable.**
- Pending: Step 5+ (loop runs) — operational after Step 4.

**Cycle health (pre-operational):**

- Constraints are spelled out in the bootstrap plan (loop must NOT modify abstract methodology docs autonomously, etc.).
- The [stdlib growth loop](../../methodology/08_lessons_and_memory.md#the-promotion-path-from-one-off-correction-to-durable-rule) and [memory-as-leading-indicator](../../methodology/08_lessons_and_memory.md#memory-as-a-leading-indicator-for-methodology-gaps) patterns are in place in the abstract methodology to receive cycle outputs.
- [Semi-annual self-evaluation cadence](../../methodology/07_definition_of_done.md#methodology-self-evaluation-semi-annual) is the meta-check on whether the cycle is producing real improvements.

**Honest:** this pillar is the most ambitious and most speculative. The infrastructure is being built in v1.7.0 → v1.x; whether the cycle actually produces compounding improvements is testable only after Step 4 ships and the loop has run for some weeks. Until then, the pillar's exit criteria are aspirational.

## 7. Delivering epics

(None yet. The bootstrap steps 2–4 are essentially this pillar's first epic-like work — they belong as proper epics in Step 2 of the bootstrap.)
