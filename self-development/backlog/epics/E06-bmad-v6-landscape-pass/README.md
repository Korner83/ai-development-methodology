# E06 — BMAD v6 landscape pass (context-handoff + review-triage conventions)

**Pillar (primary):** [P9 — Self-improvement velocity](../../../pillars/P9_self_improvement_velocity.md)
**Pillar (secondary):** [P1 — Doc completeness](../../../pillars/P1_doc_completeness.md)
**Status:** planned
**Phase:** Phase 1 — Foundation
**Started:** — (not yet active; chartered 2026-08-14)
**Target close:** TBD (items ship one-per-release like the v1.20–v1.23 landscape passes)
**Owner:** maintainer + AI coding agent

## Outcome (jobs-to-be-done)

When the maintainer reviews a peer methodology and finds mechanisms that close real gaps in
ours, they want those findings converted into scoped, individually-shippable backlog items —
rather than a loose notes file — so each idea either ships in a versioned methodology release
or is explicitly deferred/rejected with reasoning, and nothing valuable evaporates.

This epic is the intake for the **BMAD-METHOD v6.11.0 review of 2026-08-14** (full analysis:
`self-development/brief/03_competitive_landscape.md`, local-only/gitignored). Five Tier-1
ideas are chartered as items; five Tier-2 ideas are parked in [FUTURE.md](FUTURE.md).

## Exit criteria (binary)

- [ ] Each of BL-0015…BL-0019 is resolved: **shipped** in a versioned methodology release,
      **moved to FUTURE.md**, or **rejected** — with the decision and reasoning recorded in the
      item (and in the CHANGELOG for shipped ones).
- [ ] No shipped item duplicates a convention already present in `methodology/` (the v1.20–v1.23
      imports are the known overlap risk; each item's draft names what it extends).
- [ ] Every shipped change is markdown-only: no scripts, no installers, no new runtime
      dependencies (trust posture unchanged).
- [ ] The competitive-landscape brief's BMAD entry is marked reviewed/current at close (or
      annotated stale if BMAD v7 shipped meanwhile).

## KPIs

- **Import velocity:** ≥1 item shipped per methodology release cycle while the epic is active
  (matching the v1.20–v1.23 one-pass-per-release rhythm). Not gating.
- **Durability:** at the next semi-annual self-evaluation, shipped conventions are still
  present and referenced (not reverted or dead text). Forward-looking; not gating closure.

## Out of scope

- **Personas, menus, party-mode.** Rejected in the review — token overhead + tooling coupling;
  our challenge-prompt / cross-AI / decision-ownership mechanisms cover the goals.
- **Installers, web bundles, platform targeting.** Contradicts the documented no-CLI decision
  (`brief/07_tech.md`).
- **Elicitation/brainstorming catalogs.** Conflicts with the kickoff stance "ask only what you
  genuinely cannot guess."
- **Any executable tooling** (memlog-style derived artifacts, validators, snapshot renderers).
  The idea "deterministic jobs shouldn't be judgment calls" stays as advice; scripts remain
  the adopter's stack decision.
- **Public comparison content.** The analysis stays in the gitignored brief per the v1.17.1
  decision; nothing in this epic adds competitor comparisons to committed docs.

## Tier note (authority)

**Every item in this epic proposes changes to `methodology/*.md` ⇒ T2 under the tier matrix.**
The autonomous loop MUST NOT execute these edits (loop Constraint 1). The loop/agents may
*draft* proposed wording in `loop-notes/` or in the item body; the maintainer authors and
ships each change as a normal versioned release. Template-only portions (e.g. BL-0015/BL-0016
touching `templates/`) are T1-eligible only if the maintainer explicitly splits them out.

## Linked docs

- Pillars: [P9 — Self-improvement velocity](../../../pillars/P9_self_improvement_velocity.md)
  (primary), [P1 — Doc completeness](../../../pillars/P1_doc_completeness.md) (secondary)
- Analysis source: `self-development/brief/03_competitive_landscape.md` (**local-only,
  gitignored** — ask the maintainer for the file; it is not in the public repo)
- Methodology targets: [`04_backlog_items.md`](../../../../methodology/04_backlog_items.md),
  [`06_working_principles.md`](../../../../methodology/06_working_principles.md),
  [`07_definition_of_done.md`](../../../../methodology/07_definition_of_done.md),
  [`10_testing_and_verification.md`](../../../../methodology/10_testing_and_verification.md),
  [`08_lessons_and_memory.md`](../../../../methodology/08_lessons_and_memory.md)
- Precedent: CHANGELOG v1.20.0–v1.23.0 (the prior landscape-informed passes and their format)

## Item roster

See [BACKLOG.md](BACKLOG.md) for active items (BL-0015…BL-0019), [ARCHIVE.md](ARCHIVE.md) for
completed, [FUTURE.md](FUTURE.md) for deferred (BL-0020…BL-0024).

## Open questions

- **Batching:** BL-0017 and BL-0018 both touch `07` + `10` — ship as one release (one
  coherent "review rigor" pass) or two? Lean: one release, two CHANGELOG bullets.
- **Where does the Code Map convention live** (BL-0015): inside `04_backlog_items.md` as an
  item-body section, or as a template fragment? Lean: `04` defines it, templates carry a slot.
- **Frozen-intent marker syntax** (BL-0016): HTML comment (`<!-- frozen-after-approval -->`),
  a blockquote badge, or a heading convention? Must stay greppable and render cleanly on
  GitHub. Decide during drafting.

## Risks

- **Convention bloat.** Five additions to already-long docs (`04` is 894 lines) push against
  the ~1,050-line soft cap and against doc clarity (P2). Mitigation: each item names its target
  section and adds, not appends — prefer tightening existing sections over new ones; if `04`
  would cross the cap, coordinate with the E03 pattern (trim/split) first.
- **Import without fit.** BMAD's mechanics assume a single-pipeline orchestrator; ours assumes
  parallel peers. Mitigation: each item's draft must restate the idea in *our* vocabulary
  (items/locks/DoD), not BMAD's (specs/build steps) — the brief's §6 table is the mapping.
- **Duplicating prior imports.** v1.21 EARS and v1.22 two-stage review are adjacent to
  BL-0015/BL-0017. Mitigation: exit criterion 2; drafts must cross-link what they extend.
- **BMAD v7 ships mid-epic** and invalidates source pointers. Mitigation: pointers in the brief
  are commit-pinned (`c96b7d1`); ideas stand on their own once restated in our vocabulary.
