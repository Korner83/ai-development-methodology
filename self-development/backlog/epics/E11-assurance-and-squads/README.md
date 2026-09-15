# E11 — Assurance and multidisciplinary software squads

**Pillar (primary):** P1 — Doc completeness
**Pillar (secondary, optional):** P2 — Doc clarity
**Status:** active
**Phase:** Phase 1
**Started:** 2026-09-15
**Target close:** TBD — after review and acceptance
**Owner:** repository maintainer + AI documentation contributor
**Assurance:** A2 — material operating-rule changes; adopting the proposed profile for this epic explicitly
**Accountable owner:** repository maintainer (the human directing this change)

## Outcome (jobs-to-be-done)

When software contributors work across UX, customer, and engineering boundaries, they want risk-based evidence and clear human accountability, so small squads can deliver without losing verification or ownership.

## Capability owners

The repository maintainer owns customer intent, product/UX, technical delivery, verification coordination, security-policy judgment, and accountable acceptance. The AI contributor authors the docs and performs local consistency checks. Independent verification remains a separate reviewer/session; it is not claimed by the author.

## Exit criteria (binary)

- [x] A0–A3 assurance, human accountability, capability coverage, queue limits, rotation readiness, and optional asset graduation are defined in existing canonical documents without weakening existing gates.
- [x] Adoption templates, packaged skill, and solo/squad examples follow those rules and preserve line budgets.
- [ ] Scenario and structural checks have recorded results; independent verification and maintainer acceptance are recorded before closure.
- [x] v1.35.0 release documentation and pins are consistent, with unvalidated adoption status explicit.

## KPIs

- Zero broken local links or heading anchors introduced; zero line-budget violations.
- Every scenario in [TEST.md](TEST.md) has an observed result, separate from independent review.

## Out of scope

Standalone non-software workflows; mandated job titles; executable validators or additional CI; production execution changes; retroactive reassessment of archived work; the unrelated E10 re-audit.

## Linked docs

- User-approved implementation plan, 2026-09-15; report reviewed against v1.34.0 (`1d43c70`). This charter records the agreed scope; the attachment is not a required handoff dependency.
- [DoD](../../../../methodology/07_definition_of_done.md), [human roles](../../../../methodology/11_human_roles.md), [release evidence](../../../RELEASE_EVIDENCE.md).

## Release arrangements

This is a non-runtime documentation artifact: deployment recovery, production monitoring, and a runtime operational owner are not applicable. The repository maintainer owns release acceptance and repository operation. Existing git history and PR review preserve a reviewable recovery path. No release tag or production action is part of this implementation.

## Item roster

- BL-0063 — Define assurance and squad operating rules.
- BL-0064 — Propagate adoption guidance and worked examples.
- BL-0065 — Verify consistency and prepare v1.35.0.

## History

- 2026-09-15: chartered at explicit maintainer direction. E10 plus E11 consume the two active-epic slots; standing E00 remains exempt. No subagents requested or used.
- 2026-09-15: item ordering clarified as soft dependencies: adoption and verification can work against the canonical draft while its final acceptance is pending. Goals and acceptance criteria are unchanged.
