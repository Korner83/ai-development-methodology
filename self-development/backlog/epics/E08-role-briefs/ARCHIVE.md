# E08 — Role briefs per phase — Archive

_All four items shipped together in **v1.30.0** (2026-08-19)._

**Lifecycle note:** like E06 and E07, this epic ran `active → done` inside one maintainer-directed
session. That direction is what satisfies the **T2 / maintainer-authored** requirement — human-
directed, not loop-initiated. Both WIP slots stayed free in practice.

**Shared verification:** repo-wide rendering-link check across all 100 tracked markdown files —
**966 links, zero broken.** The checker models fenced blocks and inline code so it measures what a
reader can actually click, per the method note in v1.28.1; the adopter-relative links in
`templates/CLAUDE.md` and `templates/AGENTS.md` are excluded by design, as that release established.
Line caps: `README.md` 331 (cap 350), `templates/ROLE_BRIEFS.md` 197 (self-imposed 200), longest
methodology doc `04_backlog_items.md` 1,020 (cap 1,050). Markdown-only diff.

---

### BL-0030 — Write `templates/ROLE_BRIEFS.md`

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E08-role-briefs                    |
| Pillar   | P1                                 |
| Priority | P2                                 |
| Effort   | M                                  |
| Status   | done                               |
| Test     | pass — six briefs present; cold read confirms every brief links to its rules doc and restates none |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** Six lifecycle phases had documented rules but no paste-able prompt. Only
`AGENT_KICKOFF.md` and `AUTONOMOUS_LOOP.md` existed as prompts, so every other phase was entered by
reconstructing its stance from memory.

**Done means:**

- [x] Covers the six phases lacking a prompt: epic chartering, item authoring, implementation,
      review, verification, milestone evaluation.
- [x] Each brief has a stance sentence, behavioral instructions, a rules link, and a fenced
      paste-able block.
- [x] The two existing prompts are referenced, not duplicated.
- [x] No rule restated in full — verified by cold read.
- [x] 197 lines, under the 200 ceiling.

**Files (actual):** `templates/ROLE_BRIEFS.md` (new).

**Resolution:** Shipped in v1.30.0. The design decision that makes it safe is negative: a brief
carries **no rules of its own.** Each one names a stance and hands off. That is what keeps it from
becoming a second copy of the methodology that goes stale silently — the failure `07` names as
*when all the docs disagree, the docs all lose*. Two briefs carry a constraint that is not obvious
from their source doc and would otherwise be re-litigated: the review brief routes findings by
**layer, not severity** (severity tiers were rejected in E07), and the evaluation brief forbids
fixing anything in the same session that scored it.

Personas stayed rejected for the third time. The distinction held throughout: a brief describes a
stance a *phase* requires; a persona describes a character an *agent* adopts.

---

### BL-0031 — Wire role briefs into the doc set and close E07's open question

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E08-role-briefs                    |
| Pillar   | P1                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | done                               |
| Test     | pass — 966-link repo-wide check clean; every new reference resolves |
| Deps     | BL-0030                            |
| Lock     | —                                  |

**Done means:**

- [x] `README.md` repo tree and a usage pointer after the autonomous-loop line.
- [x] `methodology/00_README.md` gains a reading-path row for working one phase at a time.
- [x] `templates/AGENT_KICKOFF.md` and `templates/AUTONOMOUS_LOOP.md` link to it reciprocally —
      kickoff points forward to the ordinary phases, the loop points sideways for single-phase work.
- [x] E07's charter and its `FUTURE.md` both record the question as resolved and chartered here.
      **Outcome and Exit criteria untouched.**
- [x] Repo-wide anchor check clean.

**Files (actual):** `README.md`, `methodology/00_README.md`, `templates/AGENT_KICKOFF.md`,
`templates/AUTONOMOUS_LOOP.md`,
`self-development/backlog/epics/E07-agentic-workflow-pass/README.md` and `FUTURE.md`.

**Resolution:** Shipped in v1.30.0. E07's `FUTURE.md` was the easy miss — it asserted the thread was
open *and unscoped*, which two separate sentences elsewhere would have contradicted. Closing an open
question means closing every place that describes it as open, not just the charter.

---

### BL-0032 — Add blast radius as a required verification dimension

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E08-role-briefs                    |
| Pillar   | P9                                 |
| Priority | P1                                 |
| Effort   | S                                  |
| Status   | done                               |
| Test     | pass — seventh dimension and checklist line present; `10` at 782 lines, under the 1,050 cap |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** The six required verification dimensions were all *states of the surface you
changed*. Nothing made **"what else consumes what I changed, and did I check one of each?"** a
standing question, so shared code reached through a different configuration profile, platform build,
feature flag, or tenant went unverified by default.

**Done means:**

- [x] Seventh dimension in `10_testing_and_verification.md`, in the same shape as the six above it.
- [x] Matching line added to the paste-able verification checklist.
- [x] The limit stated in the same breath, not footnoted.
- [x] Generalized past the source's case to shared libraries, flag variants, platform builds,
      multi-tenant configs, API consumers.
- [x] `10` stays under the cap (754 → 782).

**Files (actual):** `methodology/10_testing_and_verification.md`. `CHEATSHEET.md` deliberately
untouched — it does not enumerate the dimensions, so there was nothing to extend, and it is already
over its own 100-line target at 144.

**Resolution:** Shipped in v1.30.0. Sourced from a re-read of E07's source transcript rather than a
new landscape pass — E07 extracted five ideas and this was in the residue. Written as a **row on an
existing list, not a new named convention**, deliberately: this is the third convention-adding pass
in a short window and the repo still has zero external adopters, so anything that costs a reader a
new concept had to justify itself. A dimension costs nothing extra to learn once the other six are
known.

The honest limit is stated inline rather than buried, because the failure mode of this dimension is
over-trust: it is only as good as your ability to enumerate consumers, and when they are not
enumerable it degrades into "run the full suite," which the doc already required. The real
protection in that case is contract tests at the boundary, and the section says so.

---

### BL-0033 — Name the unattended-mode failure: self-answered clarifying questions

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E08-role-briefs                    |
| Pillar   | P9                                 |
| Priority | P2                                 |
| Effort   | XS                                 |
| Status   | done                               |
| Test     | pass — caution present in both loop files, phrased as an operational test |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** Observed, not theorized. Running with approvals bypassed, the source's agent
produced good clarifying questions and then resolved them itself. The existing guard — "make only
bounded safe assumptions" — does not catch it, because each self-answer is locally reasonable and
the loss is only visible in aggregate.

**Done means:**

- [x] Caution added to the "What this prompt is NOT" list in `templates/AUTONOMOUS_LOOP.md`, beside
      the existing *cadence, not a bypass* line.
- [x] Stated operationally: the test is not whether the assumption was reasonable, but whether a
      human would recognize the choice as theirs.
- [x] Routes to the blocked-item protocol rather than inventing a new mechanism.
- [x] Mirrored in `self-development/AUTONOMOUS_LOOP.md`, which has the same section.
- [x] No new named concept introduced.

**Files (actual):** `templates/AUTONOMOUS_LOOP.md`, `self-development/AUTONOMOUS_LOOP.md`.

**Resolution:** Shipped in v1.30.0. One line in each file. It earns its place because the failure is
invisible by construction: by the time a human reads the run output, the decisions have been
reformatted as findings, and nothing in the artifact distinguishes a question that was answered by
the maintainer from one the agent answered for itself. The closing line is the part that changes
behavior — *a run that surfaces five real questions is worth more than one that silently resolved
them* — because it removes the incentive to appear productive by not asking.
