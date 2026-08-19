# E09 — External landscape pass — Future / deferred items

_Ideas from the 2026-08-19 six-repo review that are good fits but lose the ROI contest against the
three chartered items. Deferred, not rejected — outright rejections live in the
[charter's "Out of scope"](README.md#out-of-scope). Promote by moving an entry into
`BACKLOG.md` unchanged; this backlog uses the repo-wide monotonic `BL-####` space for future
items too, per [`backlog/README.md`](../../README.md), so promotion needs no renumbering._

_Both entries are `methodology/`-touching ⇒ **T2** (maintainer-authored) under the tier matrix._

---

### BL-0037 — Baseline-before-rule sequencing when authoring a rule

Rule pressure-testing already exists (shipped v1.22.0, applied at the memory promotion path in
[`08`](../../../../methodology/08_lessons_and_memory.md)), but it tests a rule that has already
been written. The sharper sequence runs the pressure scenario **first, without the rule**, records
the specific rationalizations the agent reaches for, and only then writes the minimal rule that
counters *those* — rather than the failure the author imagined. The rewrite loop is the same idea
one level up: when a new rationalization appears, add the counter and re-run.

Deferred because it changes how rules get authored rather than adding one, which makes it a
restructure of the promotion path rather than an addition to it — and this pass is deliberately
adding one convention. **Source:** the skill-authoring discipline in `obra/superpowers`
(`skills/writing-skills`). **Target:** `08_lessons_and_memory.md` promotion path; possibly the T2
row of the tier matrix in `templates/AUTONOMOUS_LOOP.md`.

**Symptom that would justify promoting it:** a shipped rule that turns out to counter a failure
nobody actually had, or a rule that gets reworded more than once because the first two versions
did not bind.

### BL-0038 — Cross-artifact coverage check across the planning chain

A consistency pass asking whether every epic exit criterion has at least one item that advances
it, and whether every item ladders up to a criterion — orphans in both directions. `EPICS.md`
already carries the pillar-coverage table as the epic→pillar half of this, and
[`00`](../../../../methodology/00_README.md) states the chain rule that each layer constrains the
one below, but nothing checks the chain after the fact.

Deferred on fit, not on value. The source runs this over three generated artifacts (spec, plan,
tasks) that are derived from each other and can therefore drift mechanically; our chain is four
*planning layers* authored at different times and horizons, where the same check is more
judgement than comparison. It may belong in the semi-annual evaluation rubric rather than as a
standing convention. **Source:** the cross-artifact analysis command in `github/spec-kit`.
**Target:** `12_milestone_evaluation.md` rubric, or `03_epics.md` closing checklist.

**Symptom that would justify promoting it:** an epic closing with exit criteria that no shipped
item actually advanced, or items discovered late to have no parent criterion.
