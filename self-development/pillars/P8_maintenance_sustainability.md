# P8 — Maintenance sustainability

> **Pillar goal:** the methodology operates with lean, sustainable maintenance overhead indefinitely — without burning out the maintainer. The *measure* of that capability is qualitative ("maintaining this should not feel like a second job") rather than a specific quarterly hour budget; the maintainer's personal time budget is private.
>
> **Last updated:** 2026-05-25

**Related:**
- Brief: [Capability layer 8](../brief/08_capability_layers.md#8-maintenance-sustainability)
- Strategy phase: [Phase 3 — Establishment](../strategy/00_master_plan.md#phase-3--establishment-12--24-months-from-phase-2-exit) (primary)
- Depends on: [P7 — Community feedback loop](P7_community_feedback_loop.md) (managing community is part of maintenance load)
- Feeds into: [P9 — Self-improvement velocity](P9_self_improvement_velocity.md) (the self-development cycle is the mechanism that keeps maintenance lean)
- Delivering epics: (none yet)

## 1. Overview

Burnout is the failure mode for solo-maintained projects. If the methodology requires more attention than the maintainer can give without burning out, the methodology fails — slowly, then suddenly.

The sustainability rule is qualitative: **maintaining this methodology must not start feeling like a second job** (see [brief/05_success_metrics.md "The one operational rule"](../brief/05_success_metrics.md#the-one-operational-rule)). The specific time budget is the maintainer's call (it's their time); the rule is that maintenance load stays at a level a single solo maintainer sustains in normal life. If maintenance starts to feel sustained-unsustainable for two consecutive quarters, the model is broken and needs intervention (scope reduction, co-maintainer, or methodology adjustment).

This pillar is **dormant in Phase 1** and **primary in Phase 3** because sustainability is only testable with sustained traction. Phase 1 is bootstrap (highly variable, project-establishment effort); Phase 2 is discovery (intermittent peaks for awesome-list submissions, etc.); Phase 3 is steady state.

## 2. What this pillar covers

| Surface | What "sustainable" means here |
|---|---|
| **Release cadence** | Releases happen as needed, not on a calendar. Sequential patch releases for trivial fixes (the v1.4.1 / v1.4.2 / v1.4.3 burst on 2026-05-25) are a smell, not a target. |
| **Issue / PR triage** | Per [STATUS.md](../../STATUS.md): no SLA. Triage happens opportunistically. The expectation is honest. |
| **Doc updates** | Per the [quarterly repo health audit](../../methodology/07_definition_of_done.md#periodic-repo-health-audits-quarterly) and [semi-annual self-evaluation](../../methodology/07_definition_of_done.md#methodology-self-evaluation-semi-annual). Cadenced, not continuous. |
| **Distribution work** | Opportunistic posts, awesome-list submissions when fit is clear, blog posts when natural. No content-marketing schedule. |
| **Community management** | Discussions / Issues responded to within "reasonable time" (subjective, but trending under a week). Per the no-SLA framing. |
| **Cycle operation** | Self-development cycle runs autonomously between user check-ins; check-ins are bounded (e.g., weekly or per-milestone). |

## 3. Exit criteria

The pillar is *delivered* (evergreen) when:

- [ ] Maintainer hours/quarter ≤40 averaged over the trailing 2 quarters (during Phase 3+).
- [ ] No release-burnout signals: sequential trivial patches stop happening (the v1.4.x burst was learning; doesn't repeat).
- [ ] Self-development cycle is operational and producing methodology improvements with maintainer time mostly going to review, not authoring.
- [ ] Community management overhead is bounded: maintainer can take 4-week breaks without major harm to the project.
- [ ] No accumulation of "I'll get to it" debt (issues, PRs, Discussions) longer than 90 days.

**Re-tested:** quarterly during Phase 3 and beyond; spot-checked whenever the maintainer notices "I'm tired."

## 4. Dependencies

**Depends on:**

- [P7 — Community feedback loop](P7_community_feedback_loop.md). Community management is a major time sink if not bounded; sustainability requires the community to be a *help*, not a *load*.
- All earlier pillars indirectly. Sustainability is the cumulative test of whether the project's other work has produced something that runs lean.

**Feeds into:**

- [P9 — Self-improvement velocity](P9_self_improvement_velocity.md). The cycle is the mechanism that reduces maintenance load by absorbing recurring work into the methodology itself.

## 5. Anti-patterns

- **Sprinting through accumulated work in one session.** Bursts (like the v1.4.x patches in one day) feel productive but produce uneven quality and don't model sustainable practice. They're acceptable as occasional learning-pushes; not as a steady-state operating mode.
- **Promising response SLAs the maintainer can't keep.** Setting expectations that can't be met erodes trust faster than honest no-SLA framing.
- **Saying yes to every feature suggestion.** Each yes adds maintenance load; many noes are needed to stay sustainable.
- **Treating the methodology as the maintainer's primary work indefinitely.** Solo maintainers have other things in their lives; the methodology must accommodate that.
- **Letting the project become identity** — "I am the methodology maintainer" → burnout when life shifts. Per [brief/01_vision.md](../brief/01_vision.md): "the methodology should outlive any individual maintainer's attention."
- **Not asking for help when overloaded.** The [STATUS.md "second contributor joins" trigger](../../STATUS.md) exists precisely so the maintainer can shift to shared infrastructure mode when needed.

## 6. Current state (v1.8.0)

**Untestable yet:**

- 2026-05-25 was a single day with 8 releases — not a steady state. Cannot infer sustainable maintenance hours from that.
- No external community to manage yet — feedback-loop overhead is zero.
- No external contributors → no PR review overhead.
- Self-development cycle not yet operational (gated on Step 4 of the bootstrap).

**What's set up for future sustainability:**

- [STATUS.md](../../STATUS.md) sets honest expectations (no SLA, lean maintenance).
- [Quarterly repo health audit](../../methodology/07_definition_of_done.md#periodic-repo-health-audits-quarterly) + [semi-annual self-evaluation](../../methodology/07_definition_of_done.md#methodology-self-evaluation-semi-annual) cadences are documented.
- CC BY 4.0 = no monetization pressure = no support-burden expectation.
- "Fork freely if you want a more actively-maintained version" is in the README and STATUS.md.

**Honest:** sustainability is the most speculative pillar in v1.8.0. The infrastructure is in place; the test happens over months of operation. The first real signal is whether maintainer hours stay reasonable in Q2 / Q3 2026 (post-launch-burst settled).

## 7. Delivering epics

(None yet. Likely Phase 3 epics: "First sustainability audit (Q2 retrospective)"; "Onboard co-maintainer (if/when trigger met)"; "CONTRIBUTING.md drafting.")
