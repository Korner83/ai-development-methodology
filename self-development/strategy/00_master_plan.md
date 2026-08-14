# 00 — Master plan

> **Plan goal:** sequence the methodology project's evolution from "lean reference artifact published by a solo maintainer" to "self-improving methodology referenced as one of the named options in AI-coding discussions" — without scaling maintainer hours linearly with adoption.
>
> **Last updated:** 2026-05-25 (Step 1 of self-development bootstrap)

**Related:**
- Brief (upstream): [self-development/brief/](../brief/) — vision, audience, competitive landscape, market gaps, success metrics, distribution, tech, capability layers
- Pillars (downstream): [self-development/pillars/](../pillars/) — nine capability layers derived from this plan
- Methodology: [methodology/01_strategy.md](../../methodology/01_strategy.md) — the strategy-doc skeleton this plan follows

---

## 1. Vision (condensed)

A portable, file-based methodology for software projects where humans and AI agents collaborate as peers. Markdown + git. No SaaS. No vendor lock-in. CC BY 4.0. Designed to make AI-collaborated software development sustainable past week 3 — for solo devs, small mixed teams, indie hackers, and engineering leaders — without enterprise overhead.

The methodology gets better over time via a **self-improving cycle**: insights from running the methodology on its own development become methodology improvements; the improved methodology improves the next cycle. Quality compounds without scaling maintainer hours.

Full vision in [brief/01_vision.md](../brief/01_vision.md).

---

## 2. Phases

Four phases, each with binary exit criteria. Phases gate: until the prior phase's exit criteria are met, the next phase's work is opportunistic at best.

### Phase 1 — Foundation (current → ~3 months)

**Goal:** methodology is complete, self-development bootstrap is operational, abstract docs are stable.

**Exit criteria (all must hold):**

- [ ] Self-development bootstrap Steps 0–4 are shipped (v1.7.0 through ~v1.x with autonomous loop config).
- [ ] No known self-contradictions in the abstract methodology docs in `methodology/` (per the latest semi-annual self-evaluation pass).
- [ ] All five template files exist in `templates/` (CLAUDE.md, AGENTS.md, AGENT_KICKOFF.md, AUTONOMOUS_LOOP.md, PROJECT_STRUCTURE.md), each with current methodology version stamp and verified against the methodology's required shape. (External-adoption testing is tracked as a **health indicator**, not a phase-exit criterion — adopter behavior is uncontrollable.)
- [ ] First autonomous loop run has completed at least one item end-to-end without maintainer intervention mid-run.

**Active pillars:** P1 Doc completeness, P2 Doc clarity, P3 Doc currency, P4 Tool compatibility, P9 Self-improvement velocity (cycle bootstrap).

**Indicator of phase health:** if maintainer hours exceed ~40/quarter sustained in this phase, the foundation work is too heavy and should be scoped down rather than pushed through.

### Phase 2 — Discovery (3 → 12 months from Phase 1 exit)

**Goal:** adopters find the methodology, first stories emerge, contributor pipeline starts.

**Exit criteria (all must hold):**

- [ ] External adoption signal exists — baseline discoverability indicators (stars, traffic, search-found rate). No specific star count; see [brief/05_success_metrics.md "What's NOT a success metric"](../brief/05_success_metrics.md#what-success-is-not) for why.
- [ ] Externally-authored adoption stories exist — at least one substantive public account (blog post, conference talk, podcast mention, public engineering blog) where someone says "we use this and here's how it shaped the project."
- [ ] At least one accepted upstream contribution from an external contributor — substantive PR (not patch), proving a contributor pipeline is forming.
- [ ] Self-development loop has produced methodology releases attributed to the autonomous cycle (not just self-development cleanup).
- [ ] At least one maintained external fork exists (where "maintained" = commits in the last 60 days at exit time).

**Active pillars:** P5 Adopter discoverability, P6 Example richness, P7 Community feedback loop become primary. Phase 1 pillars (P1–P4, P9) continue as baseline.

**Indicator of phase health:** discoverability signals climb but no adoption stories appear → people are bookmarking, not using; investigate friction (see [brief/05_success_metrics.md "Counter-signals"](../brief/05_success_metrics.md#counter-signals--when-things-are-failing-not-succeeding)).

### Phase 3 — Establishment (12 → 24 months from Phase 2 exit)

**Goal:** methodology is on the field map; companies adopt internally; the methodology has earned a seat at the table when AI-coding methodologies are compared.

**Exit criteria (all must hold):**

- [ ] The methodology appears in public field discussions on its own merit (blog posts, talks, papers comparing AI-coding methodologies). No specific count target — appearance at all is the signal.
- [ ] At least one team or company publicly uses the methodology as their internal standard (engineering blogs, hiring docs, public talks) and is still using it 12+ months later (public + sustained).
- [ ] At least one maintained adaptation / fork exists for a specific niche (e.g., regulated industry, research teams). "Maintained" = commits within 60 days.
- [ ] Maintainer time has stayed sustainable across the phase — qualitative; the rule is "if maintaining this feels like a second job, something has to change." See [brief/05_success_metrics.md "The one operational rule"](../brief/05_success_metrics.md#the-one-operational-rule).

**Active pillars:** P8 Maintenance sustainability becomes primary (now testable because traction exists). All other pillars continue as baseline.

**Indicator of phase health:** maintainer time stops feeling sustainable → reduce scope or invite co-maintainer per [STATUS.md](../../STATUS.md).

### Phase 4 — Maturity (24+ months from Phase 3 exit, open-ended)

**Goal:** cross-pollination to peer methodologies; cycle has shifted methodology significantly; project has moved to shared-infrastructure mode.

**Exit criteria (open-ended; the project lives here indefinitely):**

- [ ] Patterns originally in this methodology have been adopted by other methodologies in the field (verifiable via cross-project CHANGELOGs). Generative for the field is the strongest possible signal.
- [ ] The self-development cycle has produced patterns the solo maintainer wouldn't have discovered alone — measured by the maintainer's "this came from the cycle" notes in CHANGELOG (see [brief/05_success_metrics.md "Sustained signals"](../brief/05_success_metrics.md#sustained-signals-multi-year)).
- [ ] Project is operating in "shared infrastructure" mode (per [brief/06_distribution.md](../brief/06_distribution.md)): ≥3 external maintainers with substantive contributions; CODE_OF_CONDUCT.md and CONTRIBUTING.md present; second maintainer with merge permissions.

**No explicit "Phase 5."** Phase 4 is the steady state. If the project shifts beyond it (e.g., becomes a foundation-backed project, is forked into a new direction by a larger team), that's a separate strategic event, not a planned phase.

---

## 3. Pillar roadmap

Which pillars are *primary* (under active development) vs *baseline* (maintained but not the focus) at each phase:

| Pillar | Phase 1 | Phase 2 | Phase 3 | Phase 4 |
|---|---|---|---|---|
| P1 Doc completeness | **primary** | baseline | baseline | baseline |
| P2 Doc clarity | **primary** | baseline | baseline | baseline |
| P3 Doc currency | **primary** | **primary** | baseline | baseline |
| P4 Tool compatibility | **primary** | baseline | baseline | baseline |
| P5 Adopter discoverability | dormant | **primary** | baseline | baseline |
| P6 Example richness | dormant | **primary** | baseline | baseline |
| P7 Community feedback loop | dormant | **primary** | **primary** | baseline |
| P8 Maintenance sustainability | dormant | dormant | **primary** | baseline |
| P9 Self-improvement velocity | **primary** | **primary** | **primary** | **primary** |

**Reading the table:** *primary* means epics are actively chartered against the pillar in that phase; *baseline* means the pillar is maintained (drift catches via self-evaluation) but no new epics aim at it; *dormant* means the pillar exists and is named but isn't actionable until a later phase.

P9 (Self-improvement velocity) is primary in every phase because the self-development cycle is the cross-cutting mechanism that improves the methodology regardless of which pillar is being worked.

**Note on P4 (Tool compatibility) being primary in Phase 1:** the original capability-layer seed in [brief/08_capability_layers.md](../brief/08_capability_layers.md) had Tool compatibility at P6, downstream of discoverability and examples. The Step 0 cross-AI review resequenced it to P4 because tool compatibility is a *prerequisite* for adoption — adopters who land on the repo immediately ask "does this work with my tool?" before reading further. Compatibility belongs in the foundation work alongside the doc-quality pillars, not in the adoption push that follows.

---

## 4. Document index

This plan is the entry point. Supporting research and pillar definitions live in adjacent docs.

### Strategy docs (this folder)

- **`00_master_plan.md`** (this doc) — vision, phases, pillar roadmap, doc index.
- No other strategy docs at this time; supporting research is in the brief (see below). Supplementary strategy docs may be added as Phase boundaries shift or specific topics need dedicated treatment (e.g., a roadmap doc, a re-evaluation history doc).

### Brief docs (`../brief/`)

The brief is the upstream input to this plan. Treat as supporting research:

- [`brief/00_brief.md`](../brief/00_brief.md) — TL;DR
- [`brief/01_vision.md`](../brief/01_vision.md) — vision detail
- [`brief/02_audience.md`](../brief/02_audience.md) — primary + secondary segments
- `brief/03_competitive_landscape.md` — maintainer-private competitive analysis (gitignored from v1.17.1; lives on maintainer's disk for reference)
- `brief/04_market_gaps.md` — maintainer-private market-gap analysis (gitignored from v1.17.1; same reason)
- [`brief/05_success_metrics.md`](../brief/05_success_metrics.md) — qualitative success indicators (early + sustained); one operational rule on maintainer time; counter-signals
- [`brief/06_distribution.md`](../brief/06_distribution.md) — channels and sustainability
- [`brief/07_tech.md`](../brief/07_tech.md) — tech surface
- [`brief/08_capability_layers.md`](../brief/08_capability_layers.md) — the nine layers that became pillars

### Pillar docs (`../pillars/`)

- P1–P9 (see pillar roadmap above; one file per pillar at `../pillars/P<N>_<slug>.md`).

### Methodology (the abstract docs being applied here)

- [`methodology/00_README.md`](../../methodology/00_README.md) — methodology index
- [`methodology/01_strategy.md`](../../methodology/01_strategy.md) — strategy-doc skeleton this plan follows
- [`methodology/02_pillars.md`](../../methodology/02_pillars.md) — pillar-doc skeleton the pillars follow

---

## 5. Re-evaluation protocol

This plan re-evaluates on two cadences:

**Phase-transition re-evaluation.** When a phase's exit criteria are met, the next phase becomes active. Before that transition: re-read this plan and the brief; assess whether the next phase's exit criteria still make sense given what's been learned; revise if needed; commit the revised plan as a release.

**Semi-annual self-evaluation.** Tied to the methodology's [self-evaluation cadence](../../methodology/07_definition_of_done.md#methodology-self-evaluation-semi-annual). Even within a phase, every six months: re-read this plan and the pillar set; classify gaps as "practice is wrong" / "docs are wrong" / "both"; ship revisions.

**Memory-driven re-evaluation.** If the [stdlib growth loop](../../methodology/08_lessons_and_memory.md#the-promotion-path-from-one-off-correction-to-durable-rule) surfaces a cluster of memory entries about strategy or pillar shape, that's a signal to re-evaluate ad-hoc rather than waiting for the semi-annual.

No more frequent than that. Plans change deliberately, not in panic.

---

## 6. What this plan deliberately does NOT include

- **A calendar timeline.** Phase exit criteria are binary; phases complete when criteria are met, not by date. The "~3 months / ~12 months" hints above are expectation-setters, not commitments.
- **Resource commitments.** Solo maintainer; effort is opportunistic. The plan accommodates "free Saturday" and "busy month" equally.
- **Specific epic / item content.** Those emerge from Step 2 and Step 3 of the bootstrap. Pre-committing them here would defeat the gating model.
- **Marketing strategy details.** Distribution channels are covered in [brief/06_distribution.md](../brief/06_distribution.md); specific campaign work is epic-level, not strategy-level.
- **Predictions about which methodology improvements the cycle will produce.** Those emerge from running the cycle.

---

## 7. Status

Drafted 2026-05-25 as Step 1 of the self-development bootstrap. Cross-AI reviewed and maintainer-approved before ship in **v1.8.0**. Lives at `self-development/strategy/00_master_plan.md` in the public repo.

The next step is Step 2 (first epics) — chartering 3–5 epics against the Phase 1 primary pillars. Gated on this plan's stability.
