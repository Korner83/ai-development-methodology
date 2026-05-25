# P7 — Community feedback loop

> **Pillar goal:** adopter experience flows back into the methodology via Discussions, Issues, PRs, and direct contact — and shapes future iterations.
>
> **Last updated:** 2026-05-25

**Related:**
- Brief: [Capability layer 7](../brief/08_capability_layers.md#7-community-feedback-loop)
- Strategy phase: [Phase 2 — Discovery](../strategy/00_master_plan.md#phase-2--discovery-3--12-months-from-phase-1-exit) (primary), continuing into [Phase 3 — Establishment](../strategy/00_master_plan.md#phase-3--establishment-12--24-months-from-phase-2-exit)
- Depends on: [P5 — Adopter discoverability](P5_adopter_discoverability.md), [P6 — Example richness](P6_example_richness.md)
- Feeds into: [P3 — Doc currency](P3_doc_currency.md), [P9 — Self-improvement velocity](P9_self_improvement_velocity.md)
- Delivering epics: (none yet)

## 1. Overview

The methodology improves through real-world friction. Without a feedback loop, the maintainer is improvising; with one, the methodology incorporates lessons from contexts the maintainer hasn't personally experienced.

This pillar is currently **dormant** because there isn't enough adoption to generate community feedback. The Discussions feature was enabled in an earlier session with a welcome thread seeded; there are no external participants yet.

The pillar activates as Phase 2 progresses (adopters arrive) and becomes primary in Phase 3 (sustained external contribution). Until then, the only feedback loop is the maintainer's own usage of the methodology on this project — which is real signal, but not the same as multi-adopter feedback.

## 2. What this pillar covers

| Surface | What "feedback flowing" means here |
|---|---|
| **GitHub Discussions** | Adopters share adoption stories, ask "is this approach reasonable for X?", report drift between docs and practice. |
| **GitHub Issues** | Concrete issues filed: broken links, factual errors, gaps in coverage. Maintainer triages without SLA. |
| **GitHub PRs** | External contributors submit changes — corrections, additions, clarifications. Maintainer reviews and merges per the [git workflow](../../methodology/09_git_workflow.md). |
| **Direct contact** | Email, X, LinkedIn DMs where adopters share experience the maintainer would otherwise not see. |
| **Adopter case studies** | Blog posts, talks, papers where adopters publicly document their use of the methodology. |
| **Pattern recognition** | Maintainer notices clusters in the above (3+ adopters hit the same friction) and surfaces them as methodology improvements per the [stdlib growth loop](../../methodology/08_lessons_and_memory.md#the-promotion-path-from-one-off-correction-to-durable-rule). |

## 3. Exit criteria

The pillar is *delivered* when:

- [ ] Discussions feature is active (at least 5 external participants in any threads).
- [ ] Issues have been filed by external contributors and triaged (at least 5 resolved or closed-with-explanation).
- [ ] ≥5 external PRs have been merged with substantive content (not patches).
- [ ] Maintainer has notes ("I learned X from adopter Y") in at least 3 CHANGELOG entries — evidence the loop has shaped methodology decisions.
- [ ] At least 2 public adopter case studies exist (blog posts, talks, etc.) — separate from those required by P6, but with overlap.

**Re-tested:** quarterly during Phase 2 + Phase 3; less frequently once steady-state established.

## 4. Dependencies

**Depends on:**

- [P5 — Adopter discoverability](P5_adopter_discoverability.md). No adopters → no community → no loop.
- [P6 — Example richness](P6_example_richness.md). Adopters who see examples are more likely to contribute; abstract docs alone produce less engagement.

**Feeds into:**

- [P3 — Doc currency](P3_doc_currency.md). Feedback surfaces drift faster than maintainer-only audits.
- [P9 — Self-improvement velocity](P9_self_improvement_velocity.md). Community feedback is a major input to the self-development cycle; loop runs benefit from external signal.

## 5. Anti-patterns

- **Closing issues / Discussions without engagement.** Better to leave open and acknowledge "I see this and will get to it" than mark closed when the issue isn't resolved.
- **Promising response SLA the maintainer can't keep.** Per [STATUS.md](../../STATUS.md): no SLA. Honest about that; don't promise otherwise.
- **Treating community feedback as authoritative over methodology design.** The community surfaces real gaps; the maintainer (or future steering group) decides what to do about them. Feedback informs; doesn't dictate.
- **Letting feedback piling up without triage.** A backlog of unaddressed Discussions / Issues signals neglect to new visitors. Either close (with reason) or respond.
- **Adding every suggested feature.** Most suggestions are real but not aligned with the methodology's scope. Honest "this is out of scope" beats reluctant inclusion that bloats the docs.
- **Confusing engagement metrics with quality.** 100 Discussions threads of "I have a question" isn't community; 5 threads of "here's how we adapted X and what we learned" is.

## 6. Current state (v1.8.0)

**Strong:**

- Discussions feature is enabled and a welcome thread is seeded.
- The repo is publicly browsable and adopters can engage at any time.

**Known gaps:**

- Zero external participants in any Discussions thread as of v1.8.0.
- Zero external Issues filed.
- Zero external PRs merged.
- No adopter case studies exist.
- No `CONTRIBUTING.md` file (deferred per [STATUS.md](../../STATUS.md) until "second contributor joins" trigger).
- No CODE_OF_CONDUCT.md (same).

**Honest:** this pillar is dormant. Its activation depends on Phase 2 work succeeding (discovery → adoption). The pillar is named and infrastructure exists; the loop just hasn't started.

## 7. Delivering epics

(None yet. Likely Phase 2 epics once discovery produces adopter contact: "First adopter response policy"; "CONTRIBUTING.md drafting (when contributor pipeline forms)"; "Adopter case study commission / amplification.")
