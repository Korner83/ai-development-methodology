# E09 — External landscape pass — Archive

_All three items shipped together in **v1.31.0** (2026-08-19)._

**Lifecycle note:** like E06, E07 and E08, this epic ran `active → done` inside one
maintainer-directed session. That direction is what satisfies the **T2 / maintainer-authored**
requirement — human-directed, not loop-initiated.

**Shared verification.** Mechanical, on the final tree with counts taken last: rendering-link and
anchor check clean across every tracked markdown file; `04_backlog_items.md` at 1,036 of a 1,050
cap (grew 16 against a self-imposed 25); `ROLE_BRIEFS.md` 199/200; `README.md` 333/350;
`SKILL.md` against the format's 500-line recommendation. Format conformance was checked field by
field against the normative Agent Skills frontmatter table *before* the claim was written.

**Cross-AI findings-verification was waived by maintainer decision on 2026-08-19** — not run, not
passed. E06, E07 and E08 each passed it before `Test: pass`, and E06's returned 16 PASS / 2 FAIL
with both failures real. **This epic therefore carries one verification step fewer than the three
landscape passes before it.** Recorded because a waiver that goes unwritten becomes an assumption
that the gate ran. The cold read of the new `04` section also did not happen.

What partially covers the gap, without having been chartered as it: an independent session
re-derived every count in the repo from the tree rather than from the records, and found six stale
enumerations — three of them gates. That pass shipped in this same release. It is the same *shape*
as cross-AI validation and it caught real defects, but it examined counts rather than this epic's
`Done means:` checklists, so it is not a substitute for the waived gate.

**Disk-full incident, same session.** Partway through closing, drive D: hit 0 bytes free. A failed
write truncated this file to 0 bytes and git could not write its index. Nothing was lost — the
uncommitted work was copied off the disk before anything else was attempted, and this file was
restored from the commit. Worth recording for the same reason the tag gap was: it is a practice
failure the docs never anticipated, and the recovery worked only because the work had already been
committed and pushed once.

---

### BL-0034 — Declare Agent Skills format conformance

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E09-external-landscape-pass        |
| Pillar   | P4                                 |
| Priority | P2                                 |
| Effort   | XS                                 |
| Status   | done                               |
| Test     | pass — frontmatter checked field by field against the normative spec table (record below); cross-AI findings-verification waived by maintainer decision 2026-08-19 |
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
| Status   | done                               |
| Test     | pass — anchors, links, greppability and size budgets checked; cross-AI findings-verification and cold read waived by maintainer decision 2026-08-19 |
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
| Status   | done                               |
| Test     | pass — records written and cross-checked against the final tree |
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
- [x] Release-time work done in one pass: bumped to **v1.31.0** across every live version claim
      (README badge + two prose refs + the repo-stats sentence, `CHEATSHEET.md` pin, `STATUS.md`,
      and the `SKILL.md` version stamp the correction pass added); charter exit criteria checked;
      epic marked done. Done together rather than piecemeal, because a partial bump is the
      staleness class v1.30.1 spent three fixes cleaning up — and which the correction pass in this
      same release found in five more places.

**Resolution:** Deliberately left under `[Unreleased]` rather than cut as v1.31.0. The release
number, the badge and the epic's `done` marker are all claims that the work passed its gates, and
one gate has not run. Bumping them now would be the exact thing
[`07`](../../../../methodology/07_definition_of_done.md) forbids — a completion claim ahead of the
verification that backs it.
