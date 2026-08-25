# E10 — External baseline audit remediation

**Pillar (primary):** [P2 — Doc clarity](../../../pillars/P2_doc_clarity.md)
**Pillar (secondary):** [P8 — Maintenance sustainability](../../../pillars/P8_maintenance_sustainability.md)
**Status:** active (2026-08-20)
**Phase:** Phase 1 — Foundation
**Started:** 2026-08-20 (chartered at maintainer direction, in response to an external audit)
**Target close:** one release, `v1.32.0`
**Owner:** maintainer + AI coding agent

> **Frozen intent** — Outcome and exit criteria approved by maintainer on 2026-08-20.
> Agents do not edit them; halt and renegotiate instead.

## Outcome (jobs-to-be-done)

When a cold agent reads this methodology and reaches a rule, it wants **exactly one answer** — so that
*following the docs* and *following the docs correctly* are the same act.

An external cold, read-only audit of `be93a05` (v1.30.1) returned **"Not sound for stated use"**:
1 Critical, 5 High, 4 Medium, 1 Low. **Ten of the eleven findings still stood at v1.31.0**, verified
against the working tree rather than inferred from the changelog.

The pattern underneath most of them: **the authoritative statement is usually right, and the surface
shaped for *copying* is wrong.** The pasteable DoD checklist, the frontmatter table you paste when filing
an item, the recording example, the destructive-ops rule of thumb. A cold agent copies the wrong one
because it is the one presented for copying.

**The job is to make the rules already written decidable — and to reduce their number, not raise it.**

## Exit criteria (binary)

- [ ] Each item resolved — shipped, deferred, or rejected with reasoning.
- [ ] For each finding, a grep across `methodology/`, `templates/`, `skills/` and `CHEATSHEET.md` returns
      **one** governing statement; every line the audit cited is it or links to it.
- [ ] The skill's frontmatter loads under a strict `yaml.safe_load`, verified by running it.
- [ ] No claim in `SECURITY.md` or `README.md` is contradicted by anything under `.github/`.
- [ ] Every change is markdown or config. **No executable file is added to the tree.**
- [ ] Every touched doc under its line cap, counts taken after the final edit.
- [ ] The acceptance rows in [TEST.md](TEST.md) are run and recorded, not left `not-tested`.

## KPIs

- [`04_backlog_items.md`](../../../../methodology/04_backlog_items.md) net line change **0** — it is at
  1,036 of a 1,050 cap.
- `CHEATSHEET.md` ≤ 99, `ROLE_BRIEFS.md` ≤ 199, `README.md` ≤ 340.
- **Net new named concepts across the whole epic: two** (the destructive-operation class names, and the
  shared-ref lock protocol). An epic responding to "too many overlapping rules" that ships a pile of new
  ones has failed at its own job.

## Out of scope

**Rejected — a committed integrity checker, and any CI beyond what exists.** Considered and declined by
maintainer decision on 2026-08-20: this repository ships no runnable elements, and that is a stance, not
an oversight. **The cost is stated rather than hidden** — F-08 and F-11 get a convention, not a control,
so hand-maintained counts can drift again. What replaces the checker is that the commands are written
down and reproducible by any reader. Pinning two existing action refs to commit SHAs is config, not
infrastructure, and is in scope.

**Rejected — persona agents.** Fifth consideration, fifth decline. Recorded because role-boundary work is
the neighbourhood the question keeps arriving from.

**Rejected — softening a rule to fit practice.** Amending [`03`](../../../../methodology/03_epics.md)'s
five-file epic rule to grandfather the eight closed epics is the concrete case, and it is declined: the
rule stands, the practice catches up.

**Not this epic — recruiting adopters (audit opportunity O-03).** Already the Phase 1 → Phase 2 blocker
in [`EPICS.md`](../../EPICS.md).

## Linked docs

- Pillars: [P2](../../../pillars/P2_doc_clarity.md), [P8](../../../pillars/P8_maintenance_sustainability.md), [P1](../../../pillars/P1_doc_completeness.md), [P3](../../../pillars/P3_doc_currency.md), [P4](../../../pillars/P4_tool_compatibility.md)
- Source: an external cold read-only baseline audit of `be93a05` (v1.30.1), dated 2026-08-19. Held
  local-only; findings reproduced with file:line evidence in each item.
- **This is the first epic driven by an external review of *this repo*** rather than of other repos.

## Item roster

See [BACKLOG.md](BACKLOG.md) for open items and [ARCHIVE.md](ARCHIVE.md) for closed ones. Deferred ideas
in [FUTURE.md](FUTURE.md). Acceptance rows in [TEST.md](TEST.md).

## Risks

- **The reconciliation becomes a rewrite.** Ten findings across nine docs is the shape that turns into a
  restructure, which [`STATUS.md`](../../../../STATUS.md)'s contribution bar declines. Mitigation: every
  `Done means:` is phrased as *which sentence now says what*, and the concept count is capped at two.
- **The remediation out-bulks the thing remediated.** Named because it already happened once: the first
  pass produced more epic paperwork than doc changes, and was cut back on 2026-08-20. An epic about
  overlapping normative copies is the worst possible place to add ceremony.
- **F-08 stays open by choice.** No control replaces the checker. The next drift will be found by a
  reader, not by a build — the same way this one was.
- **Fixing the destructive-operation split makes agents bolder somewhere.** Collapsing three framings
  means picking the least restrictive reading for at least one row. The production subset stays absolute;
  only the git subset moves, and it moves to wording `templates/AGENTS.md` already ships.
