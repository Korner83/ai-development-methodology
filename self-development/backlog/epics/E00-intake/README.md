# E00 — Intake

**Pillar (primary):** [P9 — Self-improvement velocity](../../../pillars/P9_self_improvement_velocity.md)
**Status:** active (2026-08-25) — **standing; this epic does not close**
**Phase:** all phases
**Started:** 2026-08-25
**Target close:** never
**Owner:** maintainer

> **Frozen intent** — Outcome and exit criteria approved by maintainer on 2026-08-25.
> Agents do not edit them; halt and renegotiate instead.

## Outcome (jobs-to-be-done)

When work arrives that is **real, small, and not worth a charter** — a short-notice task, a changed
requirement, a decision recorded in one pass and left unexecuted — the maintainer wants somewhere to file
it in seconds under the full item discipline, so that *not planning it* does not also mean *not gating it*.

**This is the dogfood run for "focused mode."** The idea is described in
[FUTURE.md](FUTURE.md); it is deliberately **not published in `methodology/`** and will not be until this
repo has used it on real work. Sixteen conventions shipped v1.25.0 → v1.31.0 and only seven have ever been
exercised. **This one gets used before it gets written.**

## What intake is, in one line

**Same item, no charter.** A `BL-####` filed here carries the full eight-field table, frozen intent on its
`Done means:`, the `Status`/`Test` hard rule, the six DoD gates, the lock protocol, and a Code Map at
Effort M+ — **identical to a cascade item.** The only thing it lacks is a strategy → pillar → epic chain
above it.

Nothing that protects correctness is relaxed. What is skipped is a charter the work was never going to
earn.

## Exit criteria (binary)

This epic has no exit. It has an **eviction rule** instead:

- [ ] Whenever three or more open intake items share a theme, they are **promoted** into a real chartered
      epic and leave this backlog.
- [ ] Every intake item still passes the same DoD as any other item. No exceptions, ever.
- [ ] The intake ratio is reported at each semi-annual evaluation — see below.

## The measurement that justifies it

**Report the share of closed items that came through intake rather than the cascade, at every semi-annual
pass.** Read a high ratio as evidence *against the cascade*, not against the people using it: if most real
work bypasses four planning layers, those layers are not earning their cost and should be trimmed rather
than enforced harder.

**This repo currently has no mechanism that can tell it a planning layer is not worth its cost.** It took
an outside auditor to notice that nine of sixteen conventions had never been used. The intake ratio is the
first signal this project has that points the other way — at the corpus rather than at the work.

## Out of scope

**A second item format, or a lighter Definition of Done.** Both would recreate the exact drift the v1.32.0
audit spent eleven findings repairing. If the gates can be skipped for urgent work then they were never
gates, and urgency is already carried by `Priority: P0`.

**Publishing focused mode to `methodology/`.** Not until it has been used here. See [FUTURE.md](FUTURE.md)
for the design and the promotion trigger.

## Declared deviation: the WIP cap

`E00` is `active` permanently, so on a literal reading it **occupies one of the two WIP slots forever** —
which would leave a single slot for all real work.

**Recorded as a deviation rather than fixed by re-reading the rule:** a standing intake epic is exempt
from the WIP cap, because the cap exists to limit *concurrent chartered effort* and intake is not chartered
effort. This is a real design finding produced by the first hour of dogfooding, and it is exactly the kind
of thing that would have gone unnoticed had the convention been published first and used later.

## Linked docs

- Design and promotion trigger: [FUTURE.md](FUTURE.md)
- Rollup: [`EPICS.md`](../../EPICS.md) · Items: [BACKLOG.md](BACKLOG.md)
- Sibling: [E10](../E10-external-audit-remediation/README.md), whose convention sweep produced two of the
  first items filed here.

## Risks

- **Intake becomes the default and the cascade rots.** Mitigated by the eviction rule and by the ratio
  being *reported* rather than merely available. If the ratio is high the answer is to trim the cascade,
  not to close intake.
- **It becomes a to-do list with no gate.** The one thing that would make this worthless. Mitigated by the
  DoD applying unchanged: an intake item that cannot reach `Test: pass` does not close, exactly like any
  other.
- **It is convention number seventeen.** Named honestly. The difference is that this one has a reported
  need behind it and is being *used before it is published* — which no other convention in this corpus can
  claim.
