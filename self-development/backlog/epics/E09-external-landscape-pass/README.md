# E09 — External landscape pass over six repos (skills-spec conformance + item-level clarification marker)

**Pillar (primary):** [P4 — Tool compatibility](../../../pillars/P4_tool_compatibility.md)
**Pillar (secondary):** [P1 — Doc completeness](../../../pillars/P1_doc_completeness.md)
**Status:** done (2026-08-19)
**Phase:** Phase 1 — Foundation
**Started:** 2026-08-19 (chartered at maintainer direction)
**Closed:** 2026-08-19 — all three items shipped in v1.31.0
**Owner:** maintainer + AI coding agent

> **Frozen intent** — Outcome and exit criteria approved by maintainer on 2026-08-19.
> Agents do not edit them; halt and renegotiate instead.

## Outcome (jobs-to-be-done)

When the maintainer evaluates a batch of external projects, they want the pass to end with the
*smallest* set of changes that survive scrutiny — so that the review is not itself a reason to
add conventions.

Six repos were reviewed on 2026-08-19 at maintainer request:
`addyosmani/agent-engineer`, `agentskills/agentskills`, `obra/superpowers`,
`NousResearch/hermes-agent`, `msitarzewski/agency-agents`, `github/spec-kit`.

**Most of the value was already extracted by earlier passes.** The CHANGELOG records
superpowers, Spec Kit and Hermes Agent each being mined before: v1.20.0 memory archival
(Hermes), v1.21.0 EARS (Spec Kit/Kiro), v1.22.0 constitution check (Spec Kit) plus two-stage
review and rule pressure-testing (superpowers/BMAD). Four of the six yield nothing new.

Two things do, and they are deliberately asymmetric in kind:

1. **A compatibility signal, not a rule.** The Agent Skills format is an open specification.
   `skills/ai-dev-methodology/SKILL.md` already conforms to it; nothing says so. Declaring it
   costs one sentence and serves the pillar that is actually binding.
2. **One convention that closes a hole the last pass named and did not fix.** BL-0033 (v1.30.0)
   identified the unattended-mode failure — an agent answering its own clarifying questions —
   and gave it a caution but no mechanism. Spec Kit's inline clarification marker is that
   mechanism, and it fits an item-level gap that already existed: epic charters have an
   "Open questions" section with a closing gate ([`03`](../../../../methodology/03_epics.md));
   items have no equivalent.

This epic adds **one** named convention. That is the point of it, not a limitation of it.

## Exit criteria (binary)

- [x] Each of BL-0034 through BL-0036 is resolved — shipped, deferred, or rejected with reasoning.
- [x] The conformance claim was **verified before it was written** — the normative spec read,
      the frontmatter checked field by field — and the check is recorded, not asserted.
- [x] The conformance wording is a format claim, not peer positioning (see "Out of scope").
- [x] The clarification marker reuses the existing frozen-intent marker shape rather than
      inventing a second one, and is distinguished in one sentence from Principle 1 in
      [`06`](../../../../methodology/06_working_principles.md).
- [x] Every change is markdown-only — no scripts, no runtime dependencies.
- [x] Repo-wide rendering-link check clean; every touched methodology doc under the 1,050-line cap.
      **Counts taken after the final edit**, per the v1.30.1 correction.

## KPIs

- `04_backlog_items.md` grows by **≤ 25 lines** (it is the longest doc at 1,020 of a 1,050 cap).
- Zero new named concepts beyond the one marker.
- Conformance declared in exactly two places (skill + README); no third copy to drift.

## Out of scope

**Rejected — persona agents (`msitarzewski/agency-agents`).** Fourth consideration, fourth
decline. 230+ agent personalities across 15 divisions is the most complete version of the idea
we have seen, and it does not change the reasoning from E06, E07 and E08: token cost per turn,
coupling to persona-capable tooling, and the fact that our challenge-prompt, cross-AI and
decision-ownership mechanisms already cover the goal.
[`templates/ROLE_BRIEFS.md`](../../../../templates/ROLE_BRIEFS.md) is the deliberate
alternative — a brief describes a stance for a phase, a persona describes a character for an
agent. **Recorded here so the fifth pass does not re-litigate it.**

**Rejected — bundling `references/` into the skill (`agentskills/agentskills`).** The spec's
progressive-disclosure model would let the skill carry the 14 methodology docs and work offline.
Declined by maintainer decision on 2026-08-19: it duplicates ~17,000 lines into a second
location and creates a permanent sync burden against [P3](../../../pillars/P3_doc_currency.md).
Link-out stays the single source of truth. The symptom that would justify revisiting is
concrete: an adopter reporting that an agent without network access got the operating contract
and none of the depth.

**No adoption — `NousResearch/hermes-agent`.** Its curator memory pattern was already imported
in v1.20.0 (archive-don't-destroy). The remainder — messaging gateways, provider adapters,
terminal backends, session search, cron scheduling — is runtime-framework machinery with no
markdown-methodology analogue. Its agent-authored *executable* skills conflict directly with the
no-code stance.

**No adoption — `addyosmani/agent-engineer`.** A course on *building* agents (Vertex AI, ADK,
MCP, A2A). This methodology governs *projects that use* agents — a different axis, not a
competing answer on the same one. Its authoring principles ("link, don't duplicate"; "honest
about trade-offs") are already our doc altitude, the memory admission test, and `STATUS.md`.

**Deferred, not rejected — two ideas**, recorded in [FUTURE.md](FUTURE.md): superpowers'
baseline-before-rule sequencing, and Spec Kit's cross-artifact coverage check.

## Linked docs

- Pillars: [P4](../../../pillars/P4_tool_compatibility.md), [P1](../../../pillars/P1_doc_completeness.md), [P5](../../../pillars/P5_adopter_discoverability.md)
- Parent thread: [E08's BL-0033](../E08-role-briefs/ARCHIVE.md) — named the failure this epic gives a mechanism to.
- Precedent: CHANGELOG v1.25.0 (E06), v1.29.0 (E07), v1.30.0 (E08) — three prior landscape passes.
- Sources: the six repos named above, all public. Full internal comparison is held local-only in
  `self-development/brief/03_competitive_landscape.md` (gitignored by policy — see `.gitignore`).

## Item roster

See [ARCHIVE.md](ARCHIVE.md) — all three closed. [BACKLOG.md](BACKLOG.md) is empty.

## Risks

- **Convention fatigue, fourth pass.** v1.25.0 added five conventions, v1.29.0 five, v1.30.0 a
  template plus two sharpenings — with **zero external adopters** exercising any of them, a fact
  [`EPICS.md`](../../EPICS.md) already names against itself. This epic's mitigation is
  structural: it ships **one** convention, and its primary item is not a convention at all but a
  compatibility signal aimed at the constraint that is actually binding (adopters, not rules).
  If the pass had produced five more rules, chartering it would have been the wrong call.
- **A conformance claim that stops being true.** The spec can change; our skill can drift. The
  claim names the format, not a version, and the frontmatter check is cheap enough to repeat —
  the semi-annual currency pass (P3, next due 2026-11-25) is the natural place. Recorded in the
  item's resolution so the check is reproducible rather than remembered.
- **A marker that becomes a to-do list.** In Spec Kit the marker sits in a generated spec that a
  human then answers. Ours sits in a hand-authored item, where the risk is that it accumulates
  instead of blocking. Mitigated by binding it to the `ready` gate: an item carrying an
  unresolved marker cannot be picked up, so the marker has teeth or it has none.

## Closing note

**One exit criterion is met by waiver rather than by passing.** Cross-AI findings-verification was
waived by maintainer decision on 2026-08-19; the criterion above covers the mechanical checks,
which did run and are reproducible. The three landscape passes before this one each cleared that
gate. Recorded in [ARCHIVE.md](ARCHIVE.md) and in the v1.31.0 CHANGELOG entry rather than folded
into a checkbox, so the next evaluation can weigh it.

**KPIs met.** `04_backlog_items.md` grew 16 lines against a ≤25 budget, landing at 1,036 of a 1,050
cap. One new named concept, as chartered. Conformance declared in exactly two places.
