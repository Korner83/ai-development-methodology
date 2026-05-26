# E03 — Trim or split `09_git_workflow.md`

**Pillar (primary):** [P2 — Doc clarity](../../../pillars/P2_doc_clarity.md)
**Status:** active
**Phase:** Phase 1 — Foundation
**Started:** 2026-05-25
**Target close:** TBD (discovery-driven)
**Owner:** maintainer + AI coding agent

## Outcome (jobs-to-be-done)

When `methodology/09_git_workflow.md` approaches the 1,050-line soft cap (currently 986 lines after v1.6.0 added five sections), the maintainer wants to either trim it to a sustainable length or split it into focused subdocs, so the doc remains scannable and adopters aren't deterred by its length being the longest in the methodology corpus.

## Exit criteria (binary)

- [ ] `methodology/09_git_workflow.md` is either (a) under 800 lines after trimming OR (b) split into 2–3 focused docs with a top-level `09_git_workflow.md` that indexes them.
- [ ] No content present in the v1.6.0 version has been silently lost. Any removed sections are deliberately removed (with the deletion documented in the CHANGELOG entry) — not accidentally dropped.
- [ ] All inbound cross-references to `09_git_workflow.md` (from other methodology docs, README, brief, pillars) still resolve. If a section was moved or its slug changed, the inbound link is updated.
- [ ] The trim-vs-split decision is documented (in the epic's eventual closure note + CHANGELOG entry) with reasoning.
- [ ] If split: each resulting doc is under 700 lines.
- [ ] Closure note includes a clarity assessment comparing the post-change doc(s) to the v1.6.0 (pre-change) state — covers scannability, section count, and worst-case "longest unbroken stretch of prose" length. Does not depend on E02's semi-annual eval timing.

## KPIs

- **Long-term clarity:** the next semi-annual self-evaluation (E02 or its successor) confirms the affected doc(s) are clearer than the pre-change baseline. Forward-looking; not gating closure.
- **No regressions in cross-references:** post-change link scan finds zero new broken links from this change.

## Out of scope

- **Trimming other long docs.** Only `09_git_workflow.md` is targeted by this epic. Other long docs (`04_backlog_items.md` at 894 lines, `10_testing_and_verification.md` at 714) are within sustainable range; if they grow past ~1,050 in a future release, separate epics.
- **Adding new git-workflow content.** This epic is reductive / restructural, not additive. Any new content suggested during the trim is routed to a separate epic or filed for the next normal feature release.
- **Changing methodology design.** Trimming a section ≠ changing what the section says. If the trim surfaces "this rule no longer holds," route that to the semi-annual self-evaluation (E02), not this epic.

## Linked docs

- Pillar (primary): [P2 — Doc clarity](../../../pillars/P2_doc_clarity.md)
- Methodology references:
  - [09_git_workflow.md](../../../../methodology/09_git_workflow.md) — the subject doc
  - [methodology/02_pillars.md "Refinement pattern"](../../../../methodology/02_pillars.md#the-refinement-pattern) — pattern to follow if splitting (cross-link from any spun-off sub-docs back to the top-level)
- Related epics: E02 (semi-annual self-evaluation likely surfaces or confirms the clarity assessment that motivates this epic)

## Item roster

See [BACKLOG.md](BACKLOG.md) for active items (populated in Step 3), [ARCHIVE.md](ARCHIVE.md) for completed, [FUTURE.md](FUTURE.md) for deferred.

## Open questions

- **Trim or split?** A 986-line doc isn't inherently broken — but it's the longest. Trim feels cleaner if 200+ lines can come out without loss; split feels right if the content naturally cleaves into 2–3 focused topics (e.g., "Daily flow" / "Releases + hot-fixes" / "AI-agent autonomy").
- **If split: where does the canonical `09_git_workflow.md` slug live?** Options: (a) top-level indexes to subdocs; (b) the most foundational subdoc inherits the slug, others are siblings; (c) renumber so the split gets distinct numbers (09a, 09b, 09c).
- **Coordination with E02.** If the semi-annual self-evaluation also flags clarity issues in 09, fold the findings into this epic rather than fixing twice.

## Risks

- **Loss of useful content during trim.** Risk that "this section feels redundant" gets cut and turns out to be load-bearing. Mitigation: cross-AI review of the trim diff before ship; specifically ask "what did we lose?" not "is this shorter?"
- **Cross-reference breakage on split.** Splitting changes URLs/slugs; inbound links break. Mitigation: catalog inbound links before splitting; update each in the same PR.
- **Indecision between trim and split** stalls the epic. Mitigation: time-box the decision — if no clear answer in ~3 days of consideration, default to trim (lower-risk path).
