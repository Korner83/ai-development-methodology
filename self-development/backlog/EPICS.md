# Epics

_Last refreshed: 2026-08-19 (E09 chartered from a six-repo external review; 7 done, **1 active**, 0 planned, 1 parked.)_

## Rollup

| Epic | Title | Pillar (primary + secondary) | Status | Phase | Items (open/done) | Next milestone |
|---|---|---|---|---|---|---|
| [E02](epics/E02-first-semiannual-self-evaluation/README.md) | First semi-annual methodology self-evaluation pass | P3 Doc currency + P2 Doc clarity | **done** (2026-05-25) | Phase 1 | 0 / 5 | First epic closed; cycle validated; next pass 2026-11-25. |
| [E01](epics/E01-examples-folder/README.md) | Examples folder | P1 Doc completeness + P6 Example richness | **done** (2026-05-25) | Phase 1 | 0 / 5 | Shipped in v1.15.0 (examples/ folder with tinker fictional project). |
| [E05](epics/E05-cheatsheet/README.md) | CHEATSHEET.md (one-page reference) | P1 Doc completeness | **done** (2026-05-25) | Phase 1 | — / 1 | Shipped in v1.15.0 (CHEATSHEET.md at repo root, ~80 lines). |
| [E03](epics/E03-git-workflow-trim/README.md) | Trim or split `09_git_workflow.md` | P2 Doc clarity | **done** (2026-08-14) | Phase 1 | 0 / 4 | Trim chosen over split; 1,026 → 798 lines (−22%), 24 → 20 sections, zero content lost. Shipped in v1.27.0. |
| [E04](epics/E04-native-tool-templates/README.md) | Native templates for Cursor / Aider / Continue.dev | P4 Tool compatibility | **parked — will not resume** (2026-08-14) | Phase 1 | 0 / 0 | Dropped by maintainer decision: `AGENTS.md` + adaptation is the permanent answer. Charter preserved with the reasoning. Reopens only if an adopter reports adaptation actually failing. |
| [E07](epics/E07-agentic-workflow-pass/README.md) | Agentic-workflow landscape pass (context integrity + spec-time verification) | P9 Self-improvement velocity + P1 Doc completeness | **done** (2026-08-14) | Phase 1 | 0 / 5 | Chartered and closed same day at maintainer direction; 5 items shipped in v1.29.0. Personas and severity tiers rejected in review. |
| [E06](epics/E06-bmad-v6-landscape-pass/README.md) | BMAD v6 landscape pass (context-handoff + review-triage conventions) | P9 Self-improvement velocity + P1 Doc completeness | **done** (2026-08-14) | Phase 1 | 0 / 6 | Chartered and closed same day at maintainer direction; 5 chartered items shipped in v1.25.0, plus BL-0021 promoted from FUTURE.md post-closure and shipped in v1.26.0. 4 Tier-2 ideas remain in FUTURE.md. |
| [E08](epics/E08-role-briefs/README.md) | Role briefs per phase, plus a second pass over the E07 source | P1 Doc completeness + P9 Self-improvement velocity | **done** (2026-08-19) | Phase 1 | 0 / 4 | Chartered and closed same day at maintainer direction; 4 items shipped in v1.30.0. Personas rejected a third time; three further findings held with reasoning in the charter. |
| [E09](epics/E09-external-landscape-pass/README.md) | External landscape pass over six repos (skills-spec conformance + item-level clarification marker) | P4 Tool compatibility + P1 Doc completeness | **active** (2026-08-19) | Phase 1 | 3 / 0 | Three items drafted and mechanically verified; all three held at `to-be-tested` pending cross-AI findings-verification — the same gate E06/E07/E08 used to reach `Test: pass`, and one the authoring session cannot run on itself. Unreleased. |

**Counts:** **1 active** (E09), 0 planned, 7 done (E01, E02, E03, E05, E06, E07, E08), 1 parked (E04 — will not resume). **One of two WIP slots is in use.**

### WIP cap note

**WIP cap = 2 active epics** (raised from 1 on E02 close, 2026-05-25). Reasoning: E02 closed cleanly end-to-end through the autonomous loop with the tier matrix in effect; the loop demonstrated discipline (escalate-on-doubt fired correctly; diff-verification caught real issues; maintainer-merge gate preserved). With one successful epic close on record, the cap can rise to 2 without inflating risk. The cap may rise to 3 (methodology default) after the second epic closes and the loop has demonstrated discipline across two distinct epic shapes.

## Pillar coverage

Inverse view: which epics touch each pillar.

| Pillar | Active epics | Planned epics | Coverage status |
|---|---|---|---|
| P1 Doc completeness | E09 (secondary) | — | E01 + E05 (primary) done in v1.15.0; E06 (secondary) done in v1.25.0; E08 (primary) done in v1.30.0 — role briefs close the paste-able-prompt gap; E09 adds the item-level clarification marker (unreleased) |
| P2 Doc clarity | — | — | E02 secondary (done v1.14.0); E03 primary (done v1.27.0 — 09 trimmed to 798 lines) |
| P3 Doc currency | — | — | E02 (primary) done 2026-05-25; next semi-annual pass due 2026-11-25 |
| P4 Tool compatibility | E09 (primary) | — | E04 (primary) parked 2026-08-14 — `AGENTS.md` + adaptation is the accepted answer, so the pillar no longer waits on native templates. E09 revives the pillar from the other end: rather than shipping per-tool templates, state which open format the skill already conforms to (unreleased) |
| P5 Adopter discoverability | E09 (tertiary) | — | Dormant (Phase 2 pillar) — E09's conformance line is the first change aimed at it since the campaign route was closed on 2026-08-19 |
| P6 Example richness | — | — | E01 (secondary) done in v1.15.0 (examples/ folder shipped) |
| P7 Community feedback loop | — | — | Dormant (Phase 2/3 pillar) |
| P8 Maintenance sustainability | — | — | Dormant (Phase 3 pillar) |
| P9 Self-improvement velocity | E09 (BL-0036) | — | Three landscape-import epics closed: E06 (BMAD, v1.25.0 to v1.26.0), E07 (agentic workflow, v1.29.0), and E08 (secondary — a re-read of E07's own source, v1.30.0). E09 is the fourth pass and the first to return mostly *rejections* — four of six sources yielded nothing new, which is itself the useful result |

**Observation:** Until E09 every pillar with a chartered epic had had it closed, and E04 — the last planned one — is parked by decision. **One WIP slot is now in use and the other is free, with nothing queued to put in it.** Note also that four of the seven closures (E03, E06, E07, E08) ran to completion inside a single maintainer-directed session rather than a sustained `active` period, so the cap has still never actually been contended; raising it to 3 (the methodology default) would be premature on that evidence. The pattern is worth naming on its own: same-day charter-to-close is now the norm rather than the exception here, which means the WIP cap is not the mechanism doing any work — maintainer attention is.

## Maintainer's next decision

**There is one, and it is a gate rather than a choice: run cross-AI findings-verification on E09 and either release it as v1.31.0 or send it back.** This is the same gate E06, E07 and E08 each passed before `Test: pass` — fresh session, different model, each item's `Done means:` as the checklist — and E06's returned two real failures out of eighteen checks, so it is not a formality. The session that authored the diff cannot run it. (The tier matrix's T2 requirement is separate and already met: it asks that the *maintainer* author substantive changes rather than the loop, and this epic was maintainer-directed throughout.) Until the gate runs, E09's three items stay at `to-be-tested`, the CHANGELOG entry stays under `[Unreleased]`, and no version has been bumped. Beyond that gate there is no backlog decision to make: E04 was parked by decision on 2026-08-14, and E08 and E09 were both chartered as deliberate acts rather than queue pulls. Chartering new work stays that way.

The binding constraint has moved off the backlog entirely: it is the **Phase 1 → Phase 2 transition** (closed-beta readiness per [`methodology/12`](../../methodology/12_milestone_evaluation.md)). That needs ≥ 2 external adopters recruited and structured feedback collected. **The active-campaign route was closed on 2026-08-19**: the maintainer deleted the staged distribution drafts on the position that a good project sells itself, so the passive channels already in place (GitHub topics, Pages, the awesome-list listings recorded in [P5](../pillars/P5_adopter_discoverability.md)) are now the whole of the discovery surface. `HUMAN_NEEDED.md` is consequently empty. `FEEDBACK.md` becomes load-bearing the moment it lands.

If work is wanted before then, the cheapest source is still the four Tier-2 ideas parked in [E06's FUTURE.md](epics/E06-bmad-v6-landscape-pass/FUTURE.md) — boundaries triad, epic context digest, brownfield discovery pass, human-review walkthrough. (The memory admission test was promoted from that list and shipped in v1.26.0.) Promoting any means re-opening E06 or chartering a successor.

**Worth noticing:** an empty backlog is a signal, not an achievement. It usually means either the project is genuinely between phases — which is the case here — or that nobody is filing what they notice. The next self-evaluation should check which. It should also check the opposite risk, which v1.25.0 through v1.30.0 made live: that work gets chartered because it is *available to do* rather than because anything demanded it. Three landscape passes and eleven-plus conventions have shipped without a single external adopter exercising them. **E09 is the fourth pass and was scoped against that fact rather than around it:** six sources reviewed, four rejected outright, one convention added, and its primary item aimed at adopter discoverability instead of at the rulebook. Whether that restraint was real or just better-narrated is a fair question for the next evaluation to put to it.

## Status legend

- **planned** — charter exists; work has not started. Does not count against WIP cap.
- **active** — work in progress; counts against WIP cap. Currently 1 of 2 slots used.
- **done** — all items closed, exit criteria met, charter frozen.
- **parked** — work halted; charter preserved, exit criteria not met. There is no `rejected` epic state, so a *decided-against* epic is `parked` with an explicit will-not-resume marker and the reasoning in its charter (see E04).

## How to use this file

- **Maintainer / contributor:** glance at the rollup to see status; click into an epic for its charter and items.
- **Cross-AI review or audit:** spot-check that pillar coverage reflects active work; spot-check that WIP cap is respected.
- **Autonomous loop (Phase 5+):** use this file to identify which active epics to pick items from per the [ROI heuristic](../../methodology/04_backlog_items.md#prioritization--the-roi-heuristic). **There is currently no active epic**, so there is no pickup target — the loop should halt and surface rather than promoting one itself (epic promotion is a maintainer decision).

## Refresh discipline

Update this rollup whenever:

- An epic's status changes (planned → active → done/parked).
- An item is added to or closed in any epic's `BACKLOG.md` (update the items column).
- A new epic is chartered (add a row).
- The WIP cap changes (re-check the rationale in this file).

Per the methodology, the rollup is a *navigation* aid — it should always reflect the current state of the underlying epic folders. Stale rollup = lost trust.
