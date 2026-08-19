# ACTIVE_CONTEXT.md — volatile working state

**Baton, not journal.** Where the current session is, so the next one — or this one after a
context reset — can resume without re-deriving state from scratch. Per
[`methodology/08_lessons_and_memory.md` "Active context"](../../methodology/08_lessons_and_memory.md#active-context-the-volatile-working-file):
written *before* a context reset, read *first* on resume, then **verified against live `git log`
and item state**, which are authoritative when they disagree with this file.

Overwritten, not appended. The durable record lives in commits, `ARCHIVE.md`, and memory.
If a line here is worth keeping, it belongs in one of those instead.

_Last updated: 2026-08-19 — after E09 closed (v1.31.0)._

## Current focus

Nothing in flight. **No active epic**, no open items in any epic, working tree clean.

## Recent changes (this session)

- **v1.31.0**: E09 chartered → executed → closed. A landscape pass over six external repos
  requested by the maintainer. **Four of the six yielded nothing new** — the value had already
  been taken by earlier passes. Three items:
  - **BL-0034** the skill now states it is written in the Agent Skills open format. Conformance
    was verified field by field against the normative frontmatter table *before* the claim was
    written, and the record is kept in the item so it can be re-run rather than trusted. Also
    corrects an attribution: the README credited cross-tool support to the `skills` CLI, but the
    portability comes from the format.
  - **BL-0035** `Needs clarification` marker in `04` — a one-line greppable note for a question
    the author could not answer; an unresolved one blocks `Status: ready`. Reuses the
    frozen-intent marker shape. Wired into `00`'s pickup checklist, `ROLE_BRIEFS.md` brief 2, and
    `AUTONOMOUS_LOOP.md`, where it gives BL-0033's never-self-answer caution somewhere to put the
    halted question.
  - **BL-0036** records: rejections in the charter, two deferrals in `FUTURE.md`, and Spec Kit's
    convergence command logged against **BL-0023** in E06's `FUTURE.md` as a second independent
    source for the brownfield ratify idea.
- **Correction pass, same release.** An independent session re-derived every count from the tree
  rather than the records and found **six stale enumerations, three of them gates**: the
  `self-development/AUTONOMOUS_LOOP.md` Constraint 2 list governing what the loop may edit, a
  Phase 1 exit criterion in the master plan, and `P1`'s self-evaluation gate scoped to 12 docs
  against 14 — meaning `12` and `13` had never been inside the gate that exists to catch drift.
  Also swept `P3` (the doc-currency pillar, and the stalest file in the repo), `P6`, `P9`, the tag
  count, and the cheatsheet line count.
- **`CHEATSHEET.md` back under its 100-line cap** — 144 → 99, over cap since v1.20.0. It was also
  missing blast radius and role briefs, so trimming and wiring-in were one item, not two.

## Known deviations carried forward

- **Cross-AI findings-verification was waived** for E09 by maintainer decision. E06, E07 and E08
  each passed it before `Test: pass`; E06's returned 16 PASS / 2 FAIL with both failures real.
  **E09 is the first landscape pass to close without it.** Flagged for the semi-annual evaluation
  due 2026-11-25 — the question is whether this is a standing trade or a one-off.
- **No template carries a methodology version stamp**, which a Phase 1 exit criterion in the
  master plan requires. Surfaced during the correction pass and recorded as unmet rather than
  quietly dropped.

## Next steps

The backlog is not the binding constraint — the milestone is.

1. **Phase 1 → Phase 2** still needs ≥ 2 external adopters and structured feedback. The
   active-campaign route was closed by decision on 2026-08-19; the passive channels recorded in
   [P5](../pillars/P5_adopter_discoverability.md) are the whole discovery surface.
2. **Semi-annual self-evaluation due 2026-11-25.** Its charge now covers v1.25.0 through v1.31.0,
   plus the two deviations above.
3. If work is wanted before then, the cheapest source is the four Tier-2 ideas in
   [E06's FUTURE.md](epics/E06-bmad-v6-landscape-pass/FUTURE.md) and the two in
   [E09's](epics/E09-external-landscape-pass/FUTURE.md).
