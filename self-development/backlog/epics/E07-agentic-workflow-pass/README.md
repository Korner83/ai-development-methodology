# E07 — Agentic-workflow landscape pass (context integrity + spec-time verification)

**Pillar (primary):** [P9 — Self-improvement velocity](../../../pillars/P9_self_improvement_velocity.md)
**Pillar (secondary):** [P1 — Doc completeness](../../../pillars/P1_doc_completeness.md)
**Status:** done (2026-08-14)
**Phase:** Phase 1 — Foundation
**Started:** 2026-08-14 (chartered and executed same day, at maintainer direction)
**Closed:** 2026-08-14 — all five items shipped in v1.29.0
**Owner:** maintainer + AI coding agent

> **Frozen intent** — Outcome and exit criteria approved by maintainer on 2026-08-14.
> Agents do not edit them; halt and renegotiate instead.

## Outcome (jobs-to-be-done)

When the maintainer reviews a peer agentic workflow and finds mechanisms that close real gaps, they
want those converted into scoped, individually-shippable items — so each either ships in a versioned
release or is explicitly rejected with reasoning.

Source: a review of a Unity-based agentic workflow (specialised agents per phase, context "start
tokens", "caveman" output compression, a doc orchestrator). Five ideas passed the fit test; the rest
were rejected in the review itself.

## Exit criteria (binary)

- [x] Each of BL-0025…BL-0029 is resolved — shipped, deferred, or rejected with reasoning.
- [x] No shipped item duplicates an existing convention. (The v1.25.0–v1.26.0 additions are the
      overlap risk; each item names what it extends.)
- [x] Every change is markdown-only — no scripts, no runtime dependencies.
- [x] Repo-wide anchor check clean after BL-0026's section rename.

## Out of scope (rejected in review, recorded here)

- **Severity tiers on review findings** (Blocker / Warning / Nit). We route by *layer*, not severity
  — layer says where to fix, severity only says how loud to be. A second axis reintroduces the noise
  the routing was built to remove.
- **Named agent personas.** Rejected for the same reason as in E06: token cost per turn, coupling to
  persona-capable tooling, and our challenge-prompt + cross-AI + decision-ownership mechanisms
  already cover the goals. *(See "Open questions" — role **briefs** without personas may be worth
  revisiting.)*
- **Split doc architecture, manual agent triggering, human story pre-filtering.** Already present.
- **Platform-specific (Unity) and context-window-size practices.** We stay tool-agnostic.

## Linked docs

- Pillars: [P9](../../../pillars/P9_self_improvement_velocity.md), [P1](../../../pillars/P1_doc_completeness.md)
- Precedent: CHANGELOG v1.20.0–v1.23.0 and v1.25.0 (prior landscape passes)
- Analysis: recorded in this charter and in the item Resolutions; the source was a described
  workflow rather than a public repo, so there is no commit to pin.

## Item roster

See [ARCHIVE.md](ARCHIVE.md) — all five closed. [BACKLOG.md](BACKLOG.md) is empty.

## Open questions

- **Role briefs per phase.** The source workflow assigns each phase a named agent with a role
  description (spec generator, spec reviewer, plan generator, plan reviewer, implementer, deep
  reviewer, doc orchestrator). We rejected *personas*, but the underlying idea — each phase has a
  different optimal **stance**, and only two of ours are captured as paste-able prompts
  (`AGENT_KICKOFF.md`, `AUTONOMOUS_LOOP.md`) — is a real gap. Raised by the maintainer during
  execution; deliberately **not** folded into this epic to avoid scope creep mid-flight.
  **Resolved 2026-08-19** — chartered as [E08](../E08-role-briefs/README.md) and shipped in
  v1.30.0 as [`templates/ROLE_BRIEFS.md`](../../../../templates/ROLE_BRIEFS.md). Personas stayed
  rejected; the briefs carry a stance per phase and link to the rules rather than restating them.
  A re-read of this epic's source during that pass also surfaced two gaps E07 did not extract
  (blast-radius verification, self-answered clarifying questions under unattended runs), both
  filed on E08. This charter's Outcome and Exit criteria are unchanged.

## Risks

- **Convention fatigue.** This is the second landscape pass in one day; v1.25.0 added five
  conventions and this adds five more. Adopters have to absorb them. Mitigation: three of the five
  are single sections, and two live in templates where they are read rather than remembered.
- **The canary invites over-trust.** A detector that produces false positives and false negatives can
  make a session *feel* verified. Mitigated by stating its limits in the same breath as the rule.
