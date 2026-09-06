# Epics

_Last refreshed: 2026-09-05 (E00 closed BL-0059 and BL-0062; 8 done, 1 active + 1 standing, 0 planned, 1 parked.)_

## Rollup

| Epic | Title | Pillar (primary + secondary) | Status | Phase | Items (open/done) | Next milestone |
|---|---|---|---|---|---|---|
| [E00](epics/E00-intake/README.md) | Intake — real work not worth a charter | P9 Self-improvement velocity | **standing** (2026-09-05) | all | 1 / 3 | Never closes. The dogfood run for "focused mode": same item format, same gates, no epic above it. **Exempt from the WIP cap by declared deviation** — the cap limits concurrent chartered effort and intake is not chartered effort. Its first three closed items were all work with no epic to belong to — including **both** sweep decisions that had been recorded and left unexecuted, and the audit brief that unblocks E10's closing gate. |
| [E02](epics/E02-first-semiannual-self-evaluation/README.md) | First semi-annual methodology self-evaluation pass | P3 Doc currency + P2 Doc clarity | **done** (2026-05-25) | Phase 1 | 0 / 5 | First epic closed; cycle validated; next pass 2026-11-25. |
| [E01](epics/E01-examples-folder/README.md) | Examples folder | P1 Doc completeness + P6 Example richness | **done** (2026-05-25) | Phase 1 | 0 / 5 | Shipped in v1.15.0 (examples/ folder with tinker fictional project). |
| [E05](epics/E05-cheatsheet/README.md) | CHEATSHEET.md (one-page reference) | P1 Doc completeness | **done** (2026-05-25) | Phase 1 | — / 1 | Shipped in v1.15.0 (CHEATSHEET.md at repo root, 97 lines at close — the "~80" recorded here until 2026-08-19 was never accurate). Drifted to 144 and sat over E05's 100-line hard exit criterion from v1.20.0 until the v1.31.0 trim. **It is 98 lines today** — two lines of margin after the v1.34.0 trim, and nothing enforces the cap. BL-0049 shipped the budget as a written, reproducible command rather than a check; the committed checker was declined. |
| [E03](epics/E03-git-workflow-trim/README.md) | Trim or split `09_git_workflow.md` | P2 Doc clarity | **done** (2026-08-14) | Phase 1 | 0 / 4 | Trim chosen over split; 1,026 → 798 lines (−22%), 24 → 20 sections, zero content lost. Shipped in v1.27.0. |
| [E04](epics/E04-native-tool-templates/README.md) | Native templates for Cursor / Aider / Continue.dev | P4 Tool compatibility | **parked — will not resume** (2026-08-14) | Phase 1 | 0 / 0 | Dropped by maintainer decision: `AGENTS.md` + adaptation is the permanent answer. Charter preserved with the reasoning. Reopens only if an adopter reports adaptation actually failing. |
| [E07](epics/E07-agentic-workflow-pass/README.md) | Agentic-workflow landscape pass (context integrity + spec-time verification) | P9 Self-improvement velocity + P1 Doc completeness | **done** (2026-08-14) | Phase 1 | 0 / 5 | Chartered and closed same day at maintainer direction; 5 items shipped in v1.29.0. Personas and severity tiers rejected in review. |
| [E06](epics/E06-bmad-v6-landscape-pass/README.md) | BMAD v6 landscape pass (context-handoff + review-triage conventions) | P9 Self-improvement velocity + P1 Doc completeness | **done** (2026-08-14) | Phase 1 | 0 / 6 | Chartered and closed same day at maintainer direction; 5 chartered items shipped in v1.25.0, plus BL-0021 promoted from FUTURE.md post-closure and shipped in v1.26.0. 4 Tier-2 ideas remain in FUTURE.md. |
| [E08](epics/E08-role-briefs/README.md) | Role briefs per phase, plus a second pass over the E07 source | P1 Doc completeness + P9 Self-improvement velocity | **done** (2026-08-19) | Phase 1 | 0 / 4 | Chartered and closed same day at maintainer direction; 4 items shipped in v1.30.0. Personas rejected a third time; three further findings held with reasoning in the charter. |
| [E09](epics/E09-external-landscape-pass/README.md) | External landscape pass over six repos (skills-spec conformance + item-level clarification marker) | P4 Tool compatibility + P1 Doc completeness | **done** (2026-08-19) | Phase 1 | 0 / 3 | Chartered and closed same day at maintainer direction; three items shipped in v1.31.0. Four of six sources rejected outright. Cross-AI findings-verification waived by maintainer decision — the first landscape pass to close without it. |
| [E10](epics/E10-external-audit-remediation/README.md) | External baseline audit remediation | P2 Doc clarity + P8 Maintenance sustainability | **active** (2026-08-20) | Phase 1 | 0 / 14 | Chartered 2026-08-20 against an external cold audit of `be93a05` that returned **"Not sound for stated use"**. Ten of eleven findings still stood at v1.31.0. **Every Critical and High one is closed** and staged for a single `v1.32.0`: the skill parses, the trunk exception is gone, the `Test` enum has one definition, `pass` is reserved for the required level, destructive operations split into two disjoint classes, trust follows provenance, and the lock's authority claim matches what git enforces. **All fourteen items closed** — every Critical, High and Medium finding. Also shipped: SHA-pinned actions with the supply-chain claim narrowed, this repo's first root instruction file, an adoption profile, the surface map, the release-evidence commands, and a sweep finding that **only 6 of 16 conventions added v1.25.0–v1.31.0 have ever been exercised.** Stays `active` until the release lands and a fresh cold re-audit clears it — a session cannot audit its own work. **A committed checker and any new CI were declined — F-08 closes as a convention, not a control.** |

**Counts:** **1 active** (E10) + **1 standing** (E00, WIP-exempt), 0 planned, 8 done (E01, E02, E03, E05, E06, E07, E08, E09), 1 parked (E04 — will not resume). E00 does not close and does not consume a WIP slot; the exemption is declared in its charter rather than read into the rule.

### WIP cap note

**WIP cap = 2 active epics** (raised from 1 on E02 close, 2026-05-25). Reasoning: E02 closed cleanly end-to-end through the autonomous loop with the tier matrix in effect; the loop demonstrated discipline (escalate-on-doubt fired correctly; diff-verification caught real issues; maintainer-merge gate preserved). With one successful epic close on record, the cap can rise to 2 without inflating risk. The cap may rise to 3 (methodology default) after the second epic closes and the loop has demonstrated discipline across two distinct epic shapes.

**`E00-intake` is exempt from the cap.** It is `standing`, not chartered — it never closes, so on a literal reading it would occupy one of two slots permanently and leave a single slot for all real work. The cap limits *concurrent chartered effort*; intake is not chartered effort. **Recorded as a declared deviation rather than a re-reading of the rule**, and it is a design finding the dogfood run produced in its first hour — the kind that would have gone unnoticed had focused mode been published first and used later.

## Pillar coverage

Inverse view: which epics touch each pillar.

| Pillar | Active epics | Planned epics | Coverage status |
|---|---|---|---|
| P1 Doc completeness | E09 (secondary) | — | E01 + E05 (primary) done in v1.15.0; E06 (secondary) done in v1.25.0; E08 (primary) done in v1.30.0 — role briefs close the paste-able-prompt gap; E09 adds the item-level clarification marker (unreleased) |
| P2 Doc clarity | E10 (primary) | — | E02 secondary (done v1.14.0); E03 primary (done v1.27.0 — 09 trimmed to 798 lines). E10 is the first clarity work driven by an outside reader rather than by the maintainer's own re-read, and it targets a failure the pillar had not named: the *authoritative* statement is usually right, and the surface shaped for copying is the one that is wrong |
| P3 Doc currency | — | — | E02 (primary) done 2026-05-25; next semi-annual pass due 2026-11-25 |
| P4 Tool compatibility | E09 (primary) | — | E04 (primary) parked 2026-08-14 — `AGENTS.md` + adaptation is the accepted answer, so the pillar no longer waits on native templates. E09 revives the pillar from the other end: rather than shipping per-tool templates, state which open format the skill already conforms to (unreleased) |
| P5 Adopter discoverability | E09 (tertiary) | — | Dormant (Phase 2 pillar) — E09's conformance line is the first change aimed at it since the campaign route was closed on 2026-08-19 |
| P6 Example richness | — | — | E01 (secondary) done in v1.15.0 (examples/ folder shipped) |
| P7 Community feedback loop | — | — | Dormant (Phase 2/3 pillar) |
| P8 Maintenance sustainability | E10 (secondary) | — | **Partly awake.** The audit named the missing integrity checker as the root cause of the recurring count drift; a committed checker was **declined** on 2026-08-20 because this repo ships no runnable elements. E10 writes the evidence commands down instead, which is weaker on purpose and recorded as such. The pillar's real work is still ahead |
| P9 Self-improvement velocity | E09 (BL-0036) | — | Three landscape-import epics closed: E06 (BMAD, v1.25.0 to v1.26.0), E07 (agentic workflow, v1.29.0), and E08 (secondary — a re-read of E07's own source, v1.30.0). E09 is the fourth pass and the first to return mostly *rejections* — four of six sources yielded nothing new, which is itself the useful result |

**Observation:** Until 2026-08-20 every pillar with a chartered epic had had it closed, both WIP slots were free, and nothing was queued. **E10 changes the shape of the observation rather than just the counts.** Five of the eight closures (E03, E06, E07, E08, E09) ran to completion inside a single maintainer-directed session rather than a sustained `active` period, so the cap has still never been contended and raising it to 3 would be premature on that evidence. But the more useful pattern is the one the audit exposed: **eleven-plus conventions shipped across four landscape passes, and an outside reader found ten live defects in the rules those passes were adding to.** Same-day charter-to-close was not the cause, and speed is not the finding — every one of the ten was a contradiction between two copies of a rule, or a claim published without being checked. E10 is the first epic here that is expected to take more than a session, and the first whose exit criterion is somebody else's verdict.

## Maintainer's next decision

**Two decisions block work, and both are on E10.** They are carried as `Needs clarification` markers on their items, which means the items cannot reach `ready` until they are answered — the first real use of the convention v1.31.0 shipped.

- **D1 — the lock mechanism (T3, human-only).** The audit's single Critical finding is that a lock committed to a feature branch is invisible to anyone pulling trunk, so under this methodology's own PR-only rule two agents can both acquire the same item and neither can see the other. The choice is between stating a **visibility precondition** — the lock has authority only where it is visible — with a shared-ref acquisition protocol offered opt-in, or making trunk-anchored acquisition **mandatory**. The first keeps every hard rule intact and the release MINOR. The second amends *never commit directly to the trunk* and makes it **v2.0.0**. It is a judgement made without data: no adopter has ever paid the round-trip cost of the stronger protocol, because there are no adopters.
- **D2 — the `Test` enum (T2).** Whether the canonical set is the eight-value enum, and whether a no-subset rule binds: a surface reproduces all eight, or carries none and links. Blocks BL-0043 and through it BL-0044.

**One judgement still carries forward from E09.** It was the first landscape pass to close *without* cross-AI findings-verification — waived by maintainer decision. E06's run of that gate returned 16 PASS / 2 FAIL with both failures real, so the waiver traded a step that has demonstrably caught defects for speed. It is on the record for the evaluation due 2026-11-25, and **E10's charter makes the gate non-waivable for that epic** — repairing a class of "claims asserted rather than checked" while asserting the repair would be the same defect one level up.

The binding constraint has moved off the backlog entirely: it is the **Phase 1 → Phase 2 transition** (closed-beta readiness per [`methodology/12`](../../methodology/12_milestone_evaluation.md)). That needs ≥ 2 external adopters recruited and structured feedback collected. **The active-campaign route was closed on 2026-08-19**: the maintainer deleted the staged distribution drafts on the position that a good project sells itself, so the passive channels already in place (GitHub topics, Pages, the awesome-list listings recorded in [P5](../pillars/P5_adopter_discoverability.md)) are now the whole of the discovery surface. `HUMAN_NEEDED.md` is consequently empty. `FEEDBACK.md` becomes load-bearing the moment it lands.

If work is wanted before then, the cheapest source is still the four Tier-2 ideas parked in [E06's FUTURE.md](epics/E06-bmad-v6-landscape-pass/FUTURE.md) — boundaries triad, epic context digest, brownfield discovery pass, human-review walkthrough. (The memory admission test was promoted from that list and shipped in v1.26.0.) Promoting any means re-opening E06 or chartering a successor.

**Worth noticing:** an empty backlog is a signal, not an achievement. It usually means either the project is genuinely between phases — which is the case here — or that nobody is filing what they notice. The next self-evaluation should check which. It should also check the opposite risk, which v1.25.0 through v1.30.0 made live: that work gets chartered because it is *available to do* rather than because anything demanded it. Three landscape passes and eleven-plus conventions have shipped without a single external adopter exercising them. **E09 is the fourth pass and was scoped against that fact rather than around it:** six sources reviewed, four rejected outright, one convention added, and its primary item aimed at adopter discoverability instead of at the rulebook. Whether that restraint was real or just better-narrated is a fair question for the next evaluation to put to it.

## Status legend

- **planned** — charter exists; work has not started. Does not count against WIP cap.
- **active** — work in progress; counts against WIP cap. Currently 1 of 2 slots used (E10).
- **done** — all items closed, exit criteria met, charter frozen.
- **parked** — work halted; charter preserved, exit criteria not met. There is no `rejected` epic state, so a *decided-against* epic is `parked` with an explicit will-not-resume marker and the reasoning in its charter (see E04).

## How to use this file

- **Maintainer / contributor:** glance at the rollup to see status; click into an epic for its charter and items.
- **Cross-AI review or audit:** spot-check that pillar coverage reflects active work; spot-check that WIP cap is respected.
- **Autonomous loop (Phase 5+):** use this file to identify which active epics to pick items from per the [ROI heuristic](../../methodology/04_backlog_items.md#prioritization--the-roi-heuristic). **E10 is active but is not a pickup target.** Every one of its items edits `methodology/`, `templates/` or a root policy file, which makes them T2 or T3 under the tier matrix — maintainer-authored, loop-disabled. Two also carry unresolved `Needs clarification` markers, which independently blocks `ready`. The loop should halt and surface rather than promoting an epic itself (epic promotion is a maintainer decision).

## Refresh discipline

Update this rollup whenever:

- An epic's status changes (planned → active → done/parked).
- An item is added to or closed in any epic's `BACKLOG.md` (update the items column).
- A new epic is chartered (add a row).
- The WIP cap changes (re-check the rationale in this file).

Per the methodology, the rollup is a *navigation* aid — it should always reflect the current state of the underlying epic folders. Stale rollup = lost trust.
