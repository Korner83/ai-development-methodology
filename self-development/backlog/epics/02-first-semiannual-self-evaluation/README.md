# E02 — First semi-annual methodology self-evaluation pass

**Pillar (primary):** [P3 — Doc currency](../../../pillars/P3_doc_currency.md)
**Pillar (secondary):** [P2 — Doc clarity](../../../pillars/P2_doc_clarity.md)
**Status:** active
**Phase:** Phase 1 — Foundation
**Started:** 2026-05-25
**Target close:** TBD (the first pass is opportunistic; the *cadence's* first scheduled run is ~2026-11-25)
**Owner:** maintainer + cross-AI reviewer (fresh session, no prior context)

## Outcome (jobs-to-be-done)

When the methodology has accumulated ~6 months of active use and ~1.x releases, the maintainer wants to systematically re-read every methodology doc cold and classify gaps as "practice is wrong" / "docs are wrong" / "both", so drift between docs and practice gets caught before it compounds into "the methodology is a fossil."

## Exit criteria (binary)

- [ ] Every methodology doc (`methodology/00_README.md` through `11_human_roles.md`) has been read cold by at least one fresh AI session as part of this evaluation.
- [ ] All gaps surfaced are classified in a single eval report at `self-development/evaluations/2026-NN-<topic>.md` (folder created when this item ships).
- [ ] Each classified gap has a disposition: closed in a patch release (link to release), filed as an item in the appropriate epic (link to item), or explicitly deferred to `FUTURE.md` (with reason).
- [ ] The next self-evaluation date is recorded in the eval report (semi-annual cadence: ~6 months out).
- [ ] No methodology doc still contains a gap classified as "practice is wrong AND docs are wrong" without an open item to address it. (Some gaps are acceptable as long as they're tracked, not buried.)

## KPIs

- **Drift items found:** target range 5–15 for the first run (low signals the eval was shallow; high signals the methodology was drifting badly).
- **Time to complete pass:** target ≤8 hours of maintainer time (cross-AI does the cold-read; maintainer does the classification + disposition).
- **Release count from eval outputs:** target 1–3 patch releases land within 30 days of pass close (otherwise the gaps surfaced aren't being acted on).

## Out of scope

- **Auditing the `self-development/` docs.** This pass covers `methodology/` only. The `self-development/` folder has its own evolution per the bootstrap plan; auditing it is a separate concern (likely a future epic).
- **Methodology design changes.** Gaps closed by editing existing docs are in scope. Adding *new* sections or restructuring beyond gap-fix is not — those go through normal feature releases. (E.g., if the eval surfaces "we need a doc about X," that becomes a Phase 2 epic, not part of this eval.)
- **Updating the brief or strategy docs.** The brief was just authored (v1.7.0); not subject to drift review yet. Deferred to a future eval.
- **Auditing third-party content** (peer methodology landscape in `brief/03_competitive_landscape.md`). The competitive landscape has its own snapshot-update cadence noted in the brief itself.

## Linked docs

- Pillar (primary): [P3 — Doc currency](../../../pillars/P3_doc_currency.md)
- Pillar (secondary): [P2 — Doc clarity](../../../pillars/P2_doc_clarity.md)
- Strategy: [00_master_plan.md](../../../strategy/00_master_plan.md) (Phase 1 exit criterion: "no known self-contradictions in abstract methodology docs per latest self-evaluation pass")
- Methodology references:
  - [07_definition_of_done.md "Methodology self-evaluation (semi-annual)"](../../../../methodology/07_definition_of_done.md#methodology-self-evaluation-semi-annual) — the cadence pattern this epic instantiates
  - [08_lessons_and_memory.md "The promotion path"](../../../../methodology/08_lessons_and_memory.md#the-promotion-path-from-one-off-correction-to-durable-rule) — the mechanism for promoting eval-surfaced gaps to methodology updates
- Related epics: E03 (`09_git_workflow.md` trim is likely surfaced by this eval; coordinate)

## Item roster

See [BACKLOG.md](BACKLOG.md) for active items (populated in Step 3), [ARCHIVE.md](ARCHIVE.md) for completed, [FUTURE.md](FUTURE.md) for deferred.

## Open questions

- Should this first pass be opportunistic (run now while there's momentum) or wait until the actual ~6-month mark (2026-11-25)? Pro-opportunistic: validates the cadence. Pro-wait: the methodology has only been at v1.x for hours; not enough drift to find.
- Should cross-AI review use one fresh session or multiple (one per topic area)? The methodology says "fresh session"; how many depends on context budget.
- How to handle "the doc is fine but I disagree with it on reflection"? That's not drift — that's design preference change. Out of scope for the eval; route to a separate design discussion.

## Risks

- **First-pass overhead.** The first eval has setup costs (creating the `evaluations/` folder, defining the report format) that subsequent passes don't. Risk: epic ships but the cadence doesn't sustain because the first overhead set wrong expectations. Mitigation: explicitly note "first-pass overhead is one-time" in the eval report.
- **Cross-AI review of a methodology written largely by AI sessions.** Risk of bias (the reviewer was trained on similar content). Mitigation: structured prompt with specific criteria; multiple reviewers if context allows; maintainer judgment as final arbiter.
- **Surfaced gaps overwhelm the patch release cycle.** If the eval finds 30 gaps, fixing them all blocks other work. Mitigation: triage by severity; ship critical fixes immediately, batch others into a feature release.
