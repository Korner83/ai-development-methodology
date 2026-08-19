# E08 — Role briefs per phase, plus a second pass over the E07 source

**Pillar (primary):** [P1 — Doc completeness](../../../pillars/P1_doc_completeness.md)
**Pillar (secondary):** [P9 — Self-improvement velocity](../../../pillars/P9_self_improvement_velocity.md)
**Status:** done (2026-08-19)
**Phase:** Phase 1 — Foundation
**Started:** 2026-08-19 (chartered and executed same day, at maintainer direction)
**Closed:** 2026-08-19 — all four items shipped in v1.30.0
**Owner:** maintainer + AI coding agent

> **Frozen intent** — Outcome and exit criteria approved by maintainer on 2026-08-19.
> Agents do not edit them; halt and renegotiate instead.

## Outcome (jobs-to-be-done)

When a contributor starts a phase of work that has documented rules but no paste-able prompt, they
want a short brief that states the *stance* that phase requires and points at the doc holding the
rules — so the phase is entered deliberately rather than reconstructed from memory each time.

Two sources fed this epic:

1. **E07's open question** — the source workflow assigns each phase a named agent with a role
   description. We rejected *personas* twice (E06, E07), but the underlying point stands: each
   phase has a different optimal stance, and only two of ours existed as paste-able prompts
   (`AGENT_KICKOFF.md`, `AUTONOMOUS_LOOP.md`).
2. **A re-read of the same source transcript**, which surfaced two gaps E07 did not extract. Both
   are sharpenings of existing sections rather than new named conventions — deliberately so, since
   this is the third convention-adding pass in a short window and onboarding cost is real.

## Exit criteria (binary)

- [x] Each of BL-0030 through BL-0033 is resolved — shipped, deferred, or rejected with reasoning.
- [x] `templates/ROLE_BRIEFS.md` exists, covers exactly the phases that lack a paste-able prompt,
      and **links to the rules rather than restating them** — a restated rule is a defect, per
      [`07` "When all the docs disagree, the docs all lose"](../../../../methodology/07_definition_of_done.md#when-all-the-docs-disagree-the-docs-all-lose).
- [x] E07's open question is marked resolved with a pointer to this epic.
- [x] Every change is markdown-only — no scripts, no runtime dependencies.
- [x] Repo-wide anchor check clean; every touched methodology doc under the 1,050-line cap.

## KPIs

- Six briefs, each naming its rules doc. **Met** — six briefs.
- `ROLE_BRIEFS.md` under 200 lines. **Met** — 197.
- Zero rules restated in full from a methodology doc, checked by cold read. **Met.**

## Out of scope

**Rejected — named agent personas.** Third time this has been considered and declined; the
reasoning from E06 and E07 stands unchanged: token cost per turn, coupling to persona-capable
tooling, and the fact that our challenge-prompt, cross-AI, and decision-ownership mechanisms
already cover the goals. A brief describes a stance for a phase; a persona describes a character
for an agent. This epic shipped the first and not the second.

**Held, with reasoning — three findings from the transcript re-read.** Deferred rather than
rejected; each names the symptom that would justify revisiting.

- **Two-level acceptance criteria.** The source derives *technical* acceptance criteria from a
  client-language user story, then keeps a mapping table proving that satisfying the technical set
  satisfies the original. A genuine item-level gap:
  [`03`](../../../../methodology/03_epics.md) maps epic exit criteria to tests in `TEST.md`, and
  [`11`](../../../../methodology/11_human_roles.md) recommends Given/When/Then, but neither gives
  the two-level structure. **Held** because it is a whole new item-body convention that only pays
  off when someone *else* writes your stories in a language that omits your layer. Revisit if an
  adopter reports that shape.
- **Chronological task ordering** so that replanning a later step never invalidates completed
  earlier ones. Real, but one clause; `Approach` and the `Deps` field in
  [`04`](../../../../methodology/04_backlog_items.md) already house sequencing. Not worth an item.
- **Spec and plan as two separately-reviewed artifacts at two altitudes.** The source keeps the
  spec at contract altitude — which types, which interfaces, which signatures — and pushes *how
  each method body works* into a per-task plan reviewed on its own. The stated reason is sound:
  implementation detail in the spec means that discovering a better implementation while planning
  forces a spec rewrite, so either the spec goes stale or the better implementation loses. We hold
  the same content in **one** artifact (the item body, `Done means:` plus optional `Approach`) and
  get the review ladder from the three cross-AI modes instead of from artifact separation.
  **Held** because splitting the item body is a restructure of `04`, not an addition to it, and
  the altitude rule plus spec-verification already capture most of the benefit. The symptom that
  would justify revisiting is concrete: Effort L+ items showing spec churn caused by planning
  discoveries.

**Already covered — verified during the pass, no action.** The source's "spec request file" (the
answered questions and change requests preserved as an artifact) is already required by the
[Code Map](../../../../methodology/04_backlog_items.md#the-code-map--writing-m-items-for-cold-handoff),
which carries "which approach was rejected and why."

## Linked docs

- Pillars: [P1](../../../pillars/P1_doc_completeness.md), [P9](../../../pillars/P9_self_improvement_velocity.md)
- Parent thread: [E07's open question](../E07-agentic-workflow-pass/README.md#open-questions)
- Precedent: CHANGELOG v1.25.0 (E06) and v1.29.0 (E07) — the two prior landscape passes over the
  same and an adjacent source.
- Source: the same described Unity workflow behind E07. Not a public repo, so there is no commit
  to pin; the transcript is external input and was not copied into this repo.

## Item roster

See [ARCHIVE.md](ARCHIVE.md) — all four closed. [BACKLOG.md](BACKLOG.md) is empty.

## Risks

- **Convention fatigue, third pass.** v1.25.0 added five, v1.29.0 added five, and this adds a
  template plus two section-level sharpenings — with **zero external adopters** to say which of
  them earn their keep. Mitigation is structural rather than promissory: BL-0032 and BL-0033 add
  no new named concept (a row on an existing list, a caution on an existing rule), and
  `ROLE_BRIEFS.md` is a *template* — read when used, not memorized. The real check is the
  semi-annual evaluation, whose charge now covers v1.25.0 through v1.30.0.
- **Briefs drifting from the docs they summarize.** The failure mode is a brief that restates a
  rule, the rule changes, and the brief silently lies. Mitigated by the link-don't-restate exit
  criterion and by a cold read before close.
