# Audit brief — commissioning a cold external re-audit

**Purpose:** make running an independent audit a paste, not a design job. The first one
([2026-08-19, against `be93a05`](#the-2026-08-19-baseline-audit-what-it-found)) returned *"Not sound for
stated use"* and drove two releases of repair — **none of it verified by anyone but the sessions that
wrote it.**

**Who may run it.** Anyone **except** a session that authored the work under review. That is the whole
point and it is not negotiable: this project's defining defect has been claims asserted rather than
checked, and a session auditing its own output reproduces that defect one level up.

**Update the pin below at each release.** Everything else is reusable as written.

---

## The pin (current)

| | |
|---|---|
| Release | **v1.33.0** |
| Commit | `702ae5a6f5da72bfd911608d1dfd13a8d9db37d0` |
| Tree | `5939ee01eca20113551ddb7f605ba0a4b486dd85` |
| Tracked | 132 markdown files, 137 files total, 48 tags |
| Prior audit | 2026-08-19 against `be93a05` (v1.30.1) |

---

## The prompt

Paste this into a fresh session with no prior context on this repository.

```
Perform a cold, read-only baseline audit of the repository
github.com/Korner83/ai-development-methodology, pinned at tag v1.33.0
(commit 702ae5a6f5da72bfd911608d1dfd13a8d9db37d0).

POSTURE
- Read-only. Change no file, ref, issue, PR, release, tag, setting or workflow.
- Evidence-led. Separate every claim from its evidence. Cite file:line or a
  permalink at the pinned SHA for each finding.
- Do not trust the repository's own records. Re-derive every count, cap and
  parity claim from the tree. The repo's release entries have been wrong about
  their own tag counts three releases running.
- Adversarial by default. Ask what would have to be true for each claim to be
  false, then check that.

WHAT THIS PROJECT IS
A markdown-and-git methodology for running software projects where some
contributors are AI agents. 14 canonical docs in methodology/, six templates,
one installable skill, a worked fictional example, and self-development/ where
the methodology is applied to its own development. No runnable elements by
policy; one CI workflow running a secret scan.

SCORE IT ON THESE TWELVE DIMENSIONS, 0-10, each with an evidence paragraph
R1 purpose and scope · R2 conceptual coherence · R3 rule precision and
executability · R4 authority and source-of-truth integrity · R5 traceability
and handoff · R6 definition of done and verification · R7 coordination and
state safety · R8 human agency and autonomy · R9 AI safety and trust
boundaries · R10 portability and adoption · R11 evidence and generalizability
· R12 repository and release integrity.

R4, R6, R8 and R9 are core. If any core dimension scores below 7, or any
Critical finding stands, the verdict cannot be "sound".

FOUR FAILURE MODES THIS REPO HAS ACTUALLY EXHIBITED — look for recurrences
1. A claim asserted rather than checked. A prior release ran a "field by
   field" conformance check on YAML frontmatter that never invoked a parser;
   the file did not parse.
2. A rule restated on the surface built for copying, contradicting its own
   canonical statement a few dozen lines away. Check every pasteable block,
   checklist and skeleton against the section that defines it.
3. A count stated in the present tense that its own release invalidates.
4. A decision recorded and never executed. Cross-check decisions in
   self-development/evaluations/ against the tree.

VERIFY THE PRIOR AUDIT'S FIXES INDEPENDENTLY
The 2026-08-19 audit raised F-01 through F-11 (listed in this brief's next
section). All eleven are claimed fixed in v1.32.0 and v1.33.0. Confirm or
refute each from the pinned tree — do not read the changelog and agree with
it. Where a fix is real, say so; where it is partial or cosmetic, say that.

REQUIRED OUTPUT
- A one-line verdict, and the reasoning that forces it.
- Findings, each with: severity (Critical/High/Medium/Low), confidence, the
  conflicting claims quoted, a concrete failure scenario, a reproduction or
  derivation, a proposed correction, and the strongest counter-argument
  against your own finding.
- A claim-to-artifact traceability table: each public claim, its canonical
  source, its operational forms, the evidence, and a verdict.
- A mechanical-checks table: what you ran, how, and the result.
- Explicit limitations — what you could not test and why.
- Verified strengths, stated as specifically as the findings.

DO NOT
- Do not propose new conventions. This project's measured problem is that it
  has shipped sixteen conventions since v1.25.0 of which nine had never been
  used. Findings should more often subtract than add.
- Do not accept "documented as a known gap" as equivalent to fixed.
- Do not soften a Critical because the maintainer is a single person.
```

---

## The 2026-08-19 baseline audit: what it found

Give the auditor this list so the fixes can be checked rather than taken on faith. **All eleven are
claimed resolved.**

| ID | Sev | The finding, in one line | Claimed fix |
|---|---|---|---|
| F-01 | Critical | The lock was called "the authority" while lock commits live on feature branches and the trunk is PR-only — so two agents both acquire and neither can see the other | v1.32.0: authority is now conditional on visibility; opt-in shared-ref protocol added where the loser's non-fast-forward rejection *is* the compare-and-swap |
| F-02 | High | The `Test` enum had four values on the surfaces an agent pastes and eight in its canonical definition | v1.32.0: no-subset rule; every site carries all eight or links |
| F-03 | High | A sanctioned example recorded `pass (L3)` on a change requiring L4 — the token drives closure, the prose after it does not | v1.32.0: `pass` reserved for the required level; example now `partial (L3; L4 pending)` |
| F-04 | High | The installable skill's frontmatter did not parse, and carried a retired trunk exception | v1.32.0: quoted; exception removed; defers to the authority ladder |
| F-05 | High | Trust assigned by filename, so a `CLAUDE.md` edited inside an unreviewed PR is loaded as authority | v1.32.0: trust follows provenance; authority files read from the reviewed base commit |
| F-06 | High | "The AI doesn't act, period" and "requires per-operation approval" both governed destructive operations | v1.32.0: split into `agent-prohibited` and `approval-gated` on blast radius |
| F-07 | Medium | "No supply chain" while two actions ran from mutable major tags with a repo token | v1.32.0: both pinned to commit SHAs; claims narrowed rather than deleted |
| F-08 | Medium | Release evidence produced by an uncommitted external checker — no reader could reproduce a published number | v1.32.0: **declined a committed checker by maintainer decision.** Replaced with written reproducible commands. **A convention, not a control** |
| F-09 | Medium | No root instruction file; no epic carried `TEST.md`; partial adoption undeclared | v1.32.0: root `AGENTS.md`, all epics at five files, adoption profile published |
| F-10 | Medium | The "one-page" cheatsheet was 144 lines against its own <100 criterion | Fixed before the audit landed; 98 lines at v1.33.0 |
| F-11 | Low | A tag count stated in the present tense, wrong the moment its own tag was pushed | v1.32.0: as-of marker convention; corrections go forward |

**Two things the auditor should weigh rather than assume.** F-08's fix is deliberately weaker than a
control and the repo says so — judge whether the disclosure is adequate or whether the finding stands.
And the fixes to F-01 through F-06 were written and checked by the same session, with cross-AI
verification removed from that epic's exit criteria by maintainer decision.

---

## What the repo will tell you about itself, and where to distrust it

- [`RELEASE_EVIDENCE.md`](../RELEASE_EVIDENCE.md) — the commands behind every published count. **Run them
  rather than reading their outputs.**
- [`ADOPTION_PROFILE.md`](../ADOPTION_PROFILE.md) — what this instance adopts, adapts and omits. Written by
  the maintainer; check the omissions against the tree.
- [`2026-08-20-convention-sweep.md`](2026-08-20-convention-sweep.md) — records that **7 of 16 conventions
  added v1.25.0 → v1.31.0 have ever been exercised.** Verify the tally; it is the project's own most
  damaging finding about itself and therefore the one most worth confirming.
- [`STATUS.md`](../../STATUS.md) — claims one production project, no external adopters, NOT READY for
  closed beta. The production project is not inspectable; credit the disclosure, not the outcome.

## Filing what comes back

Findings land as `BL-####` items — in [`E00-intake`](../backlog/epics/E00-intake/README.md) if small and
unrelated, or in a chartered epic if they cluster. **A finding that is disputed is recorded with the
dispute**, not quietly dropped: the prior audit's value came partly from findings that were argued with
and partly from ones that were simply right, and the record should let a later reader tell which was which.
