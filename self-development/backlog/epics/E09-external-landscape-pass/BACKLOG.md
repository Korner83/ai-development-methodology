# E09 — External landscape pass — Active Backlog

_Items currently in scope for this epic. See [charter](README.md) for exit criteria._

**Epic status (as of 2026-08-19):** **active**. All three items are drafted and mechanically
verified; **all three sit at `to-be-tested` pending cross-AI findings-verification.** Nothing here
is `done` and nothing has been released.

> **Open gate — cross-AI findings-verification.** Every prior landscape pass reached `Test: pass`
> the same way: a fresh session on a different model than the authoring one, run against the full
> diff with each item's `Done means:` as the checklist
> ([10 — three modes](../../../../methodology/10_testing_and_verification.md#three-modes-spec--findings--and-diff-verification)).
> It is not ceremony — E06's returned **16 PASS / 2 FAIL** and both failures were real. The
> authoring session ran the mechanical checks (links, anchors, greppability, size budgets, spec
> conformance) and cannot run this one: an AI checking its own work against its own checklist is
> the [cheating-agent](../../../../methodology/10_testing_and_verification.md) shape the
> methodology names. **Maintainer action:** run it, fix what it returns, then flip these to
> `done` / `Test: pass` and release as v1.31.0.
>
> **On tiers — T2 is already satisfied.** Every file touched is authoritative content ⇒ **T2**
> under the [tier matrix](../../../../templates/AUTONOMOUS_LOOP.md#tiered-autonomy-for-authoritative-artifacts),
> whose requirement is that the *maintainer* authors substantive changes rather than the loop
> drafting them autonomously. This epic was chartered and executed inside a maintainer-directed
> session — the same basis [E08 recorded](../E08-role-briefs/ARCHIVE.md) for satisfying T2. The
> matrix's *diff*-verification mechanism belongs to T0/T1 patch branches and does not apply here.

## Summary

| ID | Title | Priority | Effort | Status |
|----|-------|----------|--------|--------|
| BL-0034 | Declare Agent Skills format conformance | P2 | XS | to-be-tested |
| BL-0035 | Inline clarification marker for backlog items | P2 | S | to-be-tested |
| BL-0036 | Record the pass and close the epic | P2 | S | to-be-tested |

---

### BL-0034 — Declare Agent Skills format conformance

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E09-external-landscape-pass        |
| Pillar   | P4                                 |
| Priority | P2                                 |
| Effort   | XS                                 |
| Status   | to-be-tested                       |
| Test     | manual-verified — frontmatter checked field by field against the normative spec table; cross-AI findings-verification outstanding |
| Deps     | —                                  |
| Lock     | —                                  |

> **Frozen intent** — `Why / Description:` and `Done means:` approved by maintainer on
> 2026-08-19. Agents do not edit them; halt and renegotiate instead.

**Why / Description:** `skills/ai-dev-methodology/SKILL.md` already conforms to the Agent Skills
open format, and nothing in the repo says so. Adopters evaluating whether the skill will load in
their tool have to infer it. A conformance line is the cheapest thing this repo can do for
[P5](../../../pillars/P5_adopter_discoverability.md), which the milestone evaluation scored below
the rubric minimum, and it is a statement of fact rather than another rule to learn.

**Done means:**

- [x] The normative specification is read before anything is written, and the frontmatter is
      checked field by field against it.
- [x] A conformance line exists in `skills/ai-dev-methodology/SKILL.md`.
- [x] A conformance line exists in `README.md` beside the install instructions.
- [x] Exactly those two places.
- [x] The wording names an open format and does not compare this project to a peer methodology.
- [x] The verification record states which fields were checked and against what.

**Files (actual):** `skills/ai-dev-methodology/SKILL.md` (+2), `README.md` (+2).

**Verification record (reproducible).** Source of truth: the Agent Skills specification, read at
`agentskills.io/specification` (normative copy: `docs/specification.mdx` in `agentskills/agentskills`).
Checked against its frontmatter table on 2026-08-19:

| Field | Spec constraint | Ours | Verdict |
|---|---|---|---|
| `name` | required; ≤64 chars; lowercase alphanumeric + hyphens; no leading/trailing/consecutive hyphen; **must match parent directory** | `ai-dev-methodology`, 18 chars, dir `skills/ai-dev-methodology/` | pass |
| `description` | required; 1–1024 chars; says what and when | 472 chars; states triggers and topics | pass |
| `license` | optional; license name or bundled-file reference | `CC-BY-4.0` | pass, permitted |
| unknown fields | only `name`, `description`, `license`, `compatibility`, `metadata`, `allowed-tools` are defined | none beyond the three above | pass |
| body | no format restrictions; keep `SKILL.md` under 500 lines | 131 lines | pass |

`compatibility` was considered and deliberately **omitted** — the spec says most skills do not need
it, and ours has no environment requirement beyond reading markdown. To re-verify later, re-read
the spec's frontmatter table and re-run the same five checks; the repo ships no validator and
should not, per the no-code stance. The spec's own `skills-ref validate` tool would do it for
anyone who wants a mechanical check.

**Resolution:** The wording deliberately reframes what the README already claimed. It previously
attributed cross-tool support to the `skills` CLI installer; the actual reason is the format, and
the installer is one way to deliver it. Saying so is both more accurate and more useful to an
adopter whose tool is not on the list. Checked against the v1.17.2 tribal-signaling decision: the
sentence names a file format, not a peer methodology, and cannot be used to position this project
against a competitor.

---

### BL-0035 — Inline clarification marker for backlog items

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E09-external-landscape-pass        |
| Pillar   | P1                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | to-be-tested                       |
| Test     | manual-verified — anchors, links, greppability and size budgets checked; cross-AI findings-verification and cold read outstanding |
| Deps     | —                                  |
| Lock     | —                                  |

> **Frozen intent** — `Why / Description:` and `Done means:` approved by maintainer on
> 2026-08-19. Agents do not edit them; halt and renegotiate instead.

**Why / Description:** An item can be filed with a question its author could not answer, and there
is nowhere to put the question. Epic charters have an "Open questions" section and a closing gate
that requires them answered or explicitly deferred
([`03`](../../../../methodology/03_epics.md)); items have no equivalent. The result is that the
question either lives in someone's head or gets silently guessed at implementation time.

BL-0033 (v1.30.0) named exactly this failure for unattended mode — an agent answering its own
clarifying questions and proceeding — and gave it a caution without a mechanism. This is the
mechanism.

**Done means:**

- [x] `04_backlog_items.md` documents a one-line greppable marker, reusing the frozen-intent shape.
- [x] An unresolved marker blocks `Status: ready`.
- [x] An autonomous loop never resolves one itself; it routes to `HUMAN_NEEDED.md`.
- [x] Resolution deletes the marker and folds the answer into the body.
- [x] One sentence distinguishes it from Principle 1.
- [x] `templates/ROLE_BRIEFS.md` brief 2 mentions the marker.
- [x] `templates/AUTONOMOUS_LOOP.md` carries the never-self-answer rule.
- [x] `04_backlog_items.md` grows by ≤ 25 lines and stays under the 1,050-line cap. **+16, at 1,036.**

**Files (actual):** `methodology/04_backlog_items.md` (+16 — new subsection, plus the `ready` enum
row and the "Refined" transition), `methodology/00_README.md` (the daily-pickup checklist),
`templates/AUTONOMOUS_LOOP.md` (existing caution wired to the marker),
`templates/ROLE_BRIEFS.md` (brief 2, +2).

**Resolution:** Two decisions are worth recording because both were close calls.

**The loop template was not given a new rule.** The never-self-answer caution already existed there
in full, from BL-0033. What it lacked was somewhere for the halted question to live, so the edit
wires the existing caution to the new marker instead of restating it — the failure `07` names as
*when all the docs disagree, the docs all lose*. The added half-sentence is the one thing the old
caution could not say: the marker makes the halt outlive the session, so the *next* run cannot pick
the item up and quietly answer it either.

**The daily-pickup checklist in `00` was updated even though it is technically redundant.** With
the marker folded into the definition of `ready`, an item carrying one cannot be `ready` anyway.
But that checklist already redundantly spells out `no unresolved Deps:`, which means readers use it
as the operative list — and a list used as a checklist that is missing a condition is worse than no
list. Consistency won over minimalism.

**Not touched:** the `examples/` project, pinned at v1.28.0. Adding a worked example of the marker
there is a reasonable follow-up but is out of this epic's scope.

---

### BL-0036 — Record the pass and close the epic

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E09-external-landscape-pass        |
| Pillar   | P9                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | to-be-tested                       |
| Test     | manual-verified — records written and cross-checked; epic cannot close until the gate above clears |
| Deps     | BL-0034, BL-0035                   |
| Lock     | —                                  |

**Why / Description:** Attribution for imported ideas lives in the CHANGELOG by standing decision,
and a landscape pass that does not record what it *declined* invites the next pass to re-litigate
it. E08 is the precedent: personas were rejected a third time because the first two rejections were
recorded.

**Done means:**

- [x] CHANGELOG entry drafted under `[Unreleased]` with provenance lines naming the Agent Skills
      format and Spec Kit as the two sources actually drawn on.
- [x] The two deferred ideas are in [FUTURE.md](FUTURE.md) with source and promotion symptom.
- [x] BL-0023 in [E06's FUTURE.md](../E06-bmad-v6-landscape-pass/FUTURE.md) notes the second,
      independent source converging on the same brownfield move.
- [x] `EPICS.md` rollup, counts and pillar-coverage table updated.
- [ ] **Blocked on the verification gate**, all of it release-time work: version bump to v1.31.0; the README
      badge and its two prose version references; `STATUS.md`'s version line; the README repo-stats
      sentence (**~17,400 lines / 114 files / longest doc ~1,036** — currently reads 17,000 / 110 /
      1,020, and goes stale the moment this merges); charter exit criteria checked; epic marked
      done. Listed rather than half-done, because a partial bump is the staleness class v1.30.1
      spent three fixes cleaning up.

**Resolution:** Deliberately left under `[Unreleased]` rather than cut as v1.31.0. The release
number, the badge and the epic's `done` marker are all claims that the work passed its gates, and
one gate has not run. Bumping them now would be the exact thing
[`07`](../../../../methodology/07_definition_of_done.md) forbids — a completion claim ahead of the
verification that backs it.
