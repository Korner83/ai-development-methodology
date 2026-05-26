# Changelog

All notable changes to this methodology are documented here.
Updated per the Definition of Done in [methodology/07_definition_of_done.md](methodology/07_definition_of_done.md).

This is the single source of truth for the changelog.

---

## [Unreleased]

(nothing yet)

---

## v1.17.0 — 2026-05-26

### Epic-folder convention reconciled with real adopter practice

After surveying the WayWhisper backlog (the methodology's primary production adopter), three gaps surfaced between what the methodology documented and what real projects need:

1. **Epic folder naming was ambiguous.** Methodology said `<NN>-<slug>/` (e.g., `07-content-protection/`). Real practice and the WayWhisper convention use `E<NN>-<slug>/` (e.g., `E07-content-protection/`). The `E` prefix prevents grep collisions between epic numbers and item numbers / dates, and matches the EPICS rollup's `E07` rows.
2. **Per-epic file set was under-specified.** Methodology said `TEST.md` was optional. Real projects make all 5 files standard (`README` + `BACKLOG` + `ARCHIVE` + `FUTURE` + `TEST`). Ship empty-but-present rather than missing.
3. **Cross-epic QA queue not documented.** Real projects keep a `backlog/TEST_BACKLOG.md` at the backlog root for QA scenarios that span ≥ 2 epics. The methodology had no pattern for this.

### Methodology changes

- **`methodology/03_epics.md` "Standard epic-folder structure"** (renamed from "Epic directory layout") — naming convention canonicalized to `E<NN>-<slug>`; 5 standard files documented; cross-epic `TEST_BACKLOG.md` pattern introduced.
- **`methodology/03_epics.md` "TEST.md template"** — extended with a third optional table for manual-QA scenarios; conventions for `AT-##` IDs, status values mirroring the Test enum, append-only regression scenarios; new sub-section on cross-epic `TEST_BACKLOG.md` using `QA-##` IDs.
- **`methodology/00_README.md`, `04_backlog_items.md`, `05_locks_and_parallel_work.md`, `09_git_workflow.md`** — all path references updated from `<NN>-<slug>` to `E<NN>-<slug>`.
- **`templates/AGENT_KICKOFF.md`** — Step 3c updated to use the new convention; added pointer to `03_epics.md "Standard epic-folder structure"`.
- **`CHEATSHEET.md`** — planning-layers table updated; new sub-line documenting the 5-file standard + optional `TEST_BACKLOG.md`.

### Example improvements

The `examples/example-project/` worked example previously shipped with only 2 files per epic (`README.md` + `BACKLOG.md`). v1.17.0 brings it up to the 5-file standard:

- **Folder renamed** `01-cli-foundations` → `E01-cli-foundations`.
- **`ARCHIVE.md` added** — BL-0001 (Scaffold project + CI for 3 OS) moved from BACKLOG to ARCHIVE with closure note. Demonstrates the archival pattern correctly (`Status: done` items don't stay in active BACKLOG).
- **`FUTURE.md` added** — 3 example deferred items using Scheme B IDs (`BL-E01-F01`, `BL-E01-F02`, `BL-E01-F03`). Demonstrates the deferred-but-named-and-grep-able pattern.
- **`TEST.md` added** — 5 acceptance tests mapping to charter exit criteria; 1 regression scenario from BL-0001's close; 3 manual-QA scenarios with cadences. Uses the new `AT-##` ID convention.
- **`backlog/TEST_BACKLOG.md` added** — cross-epic manual-QA queue with 3 example scenarios using `QA-##` IDs.
- **`BACKLOG.md` cleaned up** — BL-0001 removed (now in ARCHIVE); summary table reflects only active items.

### Self-development consistency

The methodology's own self-development project (`self-development/backlog/epics/`) was on the old naming convention (`01-examples-folder`, etc.). All 5 folders renamed to `E<NN>-` to match the new standard:

```
01-examples-folder              → E01-examples-folder
02-first-semiannual-self-eval   → E02-first-semiannual-self-evaluation
03-git-workflow-trim            → E03-git-workflow-trim
04-native-tool-templates        → E04-native-tool-templates
05-cheatsheet                   → E05-cheatsheet
```

All references in EPICS.md + cross-doc links updated. The 5-file structure expansion (ARCHIVE, FUTURE, TEST) for active self-development epics is deferred to a follow-up commit since those epics (E03 active; E04 planned) have light item counts that don't yet justify all 5 files. Standard applies when populated.

### Process note

**First PR-workflow release** (PR #3). The earlier in-day commits bypassed PR review under maintainer authorization (one-off operational concession); v1.17.0 establishes the PR-default discipline going forward. Every methodology change from this release onward should pass through PR review — even solo maintainer work benefits from the review-surface artifact, and adopters see in the commit history that the project follows its own rules.

### Notable for adopters upgrading from v1.16.0 or earlier

- **Rename your epic folders** to `E<NN>-<slug>/` (e.g., `07-content-protection` → `E07-content-protection`). The `git mv` is one-line per folder; update `EPICS.md` link references.
- **Add the missing standard files** to each epic folder (`ARCHIVE.md`, `FUTURE.md`, `TEST.md`) — empty-but-present is fine. WayWhisper-style 5-file pattern.
- **Consider adding `backlog/TEST_BACKLOG.md`** if your QA volume warrants a cross-epic queue.
- **Existing `<NN>-<slug>/` folders are not invalid** — the methodology still works if you don't rename — but new projects should default to the `E<NN>-` convention.

---

## v1.16.0 — 2026-05-25

### Methodology adjustments per maintainer feedback

Three substantive refinements to the methodology informed by reviewing a real adopter backlog (WayWhisper) and the maintainer's direct feedback on v1.15.0:

**1. Expanded Test enum** ([doc 04](methodology/04_backlog_items.md#test-enum)).

Old enum: `not-tested | pass | fail: <detail> | regression-needed` (4 values).
New enum: `not-tested | pending | manual-verified | partial | pass | fail: <detail> | regression-needed | n/a` (8 values).

Additions:
- **`pending`** — tests exist (written or scaffolded) but not yet executed. The intermediate state before `pass` or `fail`.
- **`manual-verified`** — verified by a human (UI walkthrough, manual reproduction) without automated tests. Acceptable for `Status: done` when automation is impractical AND a `regression-needed` follow-up item exists. Adopted from observing WayWhisper's `manual-verified` usage in real items.
- **`partial`** — some test surface passes; some is missing or pending. Cannot transition to `done`; explicit limitation.
- **`n/a`** — item has no testable behavior (folder creation, README edit, repo-state chore). Acceptable for `done` with body-documented reason.

The hard rule is correspondingly extended: **`Status: done` requires `Test: pass`, `manual-verified` (with regression-needed follow-up), or `n/a` (with body-documented reason).** The two narrow extensions exist to keep the methodology honest about real-world cases without becoming an escape hatch; both require explicit documentation and are auditable in the next eval cycle.

The Test field is also now documented as accepting **free-form artifact references after the enum value** (file paths, PR numbers): `Test: pass — apps/api/src/test/admin.test.ts (19 tests)`. Adopted from observing WayWhisper's real-world usage where Test fields routinely carry test-artifact pointers for traceability.

**2. Status enum tolerance** ([doc 04](methodology/04_backlog_items.md#acceptable-project-specific-aliases)).

The canonical 8-value Status enum stays unchanged. Three project-specific aliases are now explicitly acceptable:

- **`todo`** as an alias for `backlog` (WayWhisper uses this).
- **`future`** for items living in `FUTURE.md` (not a transition state; flips to `backlog`/`ready` on promotion).
- **`parked`** for items set aside indefinitely when `blocked` doesn't fit (no concrete blocker; deprioritized).

**Adding aliases is fine; inventing new lifecycle states is not.** New states are T2/T3 methodology-change candidates.

**3. Multi-level scoring** ([doc 12](methodology/12_milestone_evaluation.md#picking-the-rubrics-scope-project--pillar--epic--item)).

The deep-eval rubric can now apply at four levels of granularity:

- **Project-wide** (default for most projects — single aggregate score).
- **Per-pillar** (when pillars are decoupled enough that one strong pillar shouldn't paper over a weak one).
- **Per-epic** (when an epic represents significant scope deserving its own quality check).
- **Per-item / user-story** (heavy ceremony; reserve for items where the user-story bar is the whole milestone gate).

**Mixed scope is allowed** — score project-wide for most areas + per-pillar for security + per-item for one critical user-flow item, if that's what the project needs.

**4. Expanded default scoring areas** ([doc 12](methodology/12_milestone_evaluation.md#standard-scoring-areas)).

The standard rubric area list grew from 10 → 20 to cover more product surfaces explicitly:

| New area | What 10/10 means |
|---|---|
| **Database** | Normalized schema; reversible migrations; indexes match query patterns; clean slow-query log. |
| **Authentication** | Login flows work; session lifetime sensible; no auth bypass. |
| **Authorization** | Owner-derived from server-trusted session, never request body. RLS or equivalent at every privacy-sensitive boundary. |
| **Accessibility — testing** (separate from Accessibility — design) | Automated a11y checks in CI; manual screen-reader QA on critical flows. |
| **CI / CD** | Every push runs full pipeline; deploys scripted + reversible; staging mirrors production. |
| **Paywall / monetization** | Pricing visible + correct; checkout works; entitlements documented; refund tested. |
| **Administration / operator tools** | Operators have UI for common ops; audit-logged; CLI alternatives for emergencies. |
| **Internationalization** | Strings externalized; RTL support if relevant; locale-aware formatting. |
| **Privacy + data handling** | Per-user data scoped correctly; deletion + export work; retention enforced. |
| **Brand + voice** | Consistent visual identity; tone matches strategy doc; no off-brand assets in production. |
| **Onboarding** | New user reaches first-success under project's N-minute target. |

The standard set now includes 20 areas. Adopters still pick the subset that fits their project + add domain-specific ones (Compliance, Reproducibility, Tenant isolation, etc.).

### Authentic-rubric-vs-theater guardrails

Doc 12 also gains explicit guardrails so scoring stays honest:

- Scores are integers 0–10 **with an evidence-cited paragraph per area** (the paragraph is what the maintainer reads; the number is the summary).
- **Specific evidence, not summaries** ("p95 = 1.2s, exceeds 800ms budget per `docs/perf.md`" beats "performance has issues").
- **Cross-AI scores, not self-scores** (the implementing session is biased; cross-AI samples evidence claims to verify they're not fabricated).

### CHEATSHEET updates

[`CHEATSHEET.md`](CHEATSHEET.md) now reflects: full Status + Test enums with aliases + the free-form artifact-reference pattern; the multi-level scoring scope options; the expanded default area list.

### Self-development project progress

**E03 (Trim/split 09_git_workflow.md) promoted to active.** EPICS rollup updated: 1 active (E03), 1 planned (E04), 3 done (E01, E02, E05). E03's backlog has 4 items pending; the loop may pick them up under standard ROI.

**First periodic deep-eval ran** (`self-development/evaluations/2026-05-25-eval-01.md`). Scored on a methodology-tailored 9-area rubric. **Result: NOT READY for closed beta** — average 8.11 / 10, but Adopter discoverability scored 6 / 10 (below the 7 minimum-area threshold for the closed-beta target). The dominant blocker: zero external promotion has happened. Distribution materials drafted; maintainer-led publication pending.

**Distribution materials staged** under `self-development/distribution/` (Show HN draft, awesome-lists PRs, blog post, Discussions seeds). The autonomous loop drafted; the maintainer publishes (per the methodology's "voice belongs to the maintainer" rule for external posts).

### Notable for adopters

- If you were using `Test: not-tested` to flag "I just haven't written tests yet but they're coming", switch to `Test: pending` for clearer signal.
- If you were stuck flipping to `Status: done` on items that genuinely have no testable behavior (a folder creation, a README edit), use `Test: n/a` with a one-line body explanation. This is now legitimate, no longer a workaround.
- If your project's pillars are decoupled enough that one pillar's quality could mask another's drift, switch your deep-eval to per-pillar scoring this cycle.
- The expanded area list isn't a checklist to fill out — it's a menu to pick from. Most projects use 6–12 areas; using all 20 is overkill for most.

---

## v1.15.0 — 2026-05-25

### New methodology pattern: milestone-driven evaluation + scoring rubric

**Doc 12 introduced.** A new methodology doc — [`methodology/12_milestone_evaluation.md`](methodology/12_milestone_evaluation.md) — operationalizes the aggregate gate that per-item DoD (doc 07) does not cover. Per-item DoD catches single-change defects; per-milestone evaluation catches compounded UI debt, cross-cutting perf regressions, security drift, strategy drift, content-quality erosion, and the rest of the "all items green; product unfit to ship" failure mode.

The pattern operationalizes four ideas:

1. **Milestones are named waypoints with binary readiness criteria.** Default sequence: pre-alpha → alpha → closed-beta wave 1 → closed-beta wave 2 → open beta → first public (v1.0) → GA. Adapters adjust per project.
2. **Periodic deep-eval runs every Nth loop iteration** — N = 3 for early phase, 5 for stable, 10 for late. Score the project on a 0–10 rubric per area against the *next milestone's* readiness criteria.
3. **Scoring rubric per area** — defaults: UX/UI, frontend, backend, security, performance, test coverage, content quality, documentation, operational readiness, accessibility. Adopters add/drop areas per project domain. AI can help define areas during strategy setup.
4. **Default thresholds** — minimum 8/10 per area, average 9/10 across all. No area can be averaged away. Projects raise thresholds for high-stakes milestones (GA: 9/9.5), lower for early (alpha: 6/7).

**Unsolvable issues are first-class.** Three legitimate dispositions when a fix resists multiple loop attempts: **handle** (workaround + Limitation note), **postpone** (FUTURE.md with reason), **mark** (Status: rejected + Known issue documentation). The methodology's stance: marking is honest; forced progression is dishonest.

**Human review remains the final gate** even when the rubric scores at threshold. The maintainer verifies the *unmeasured* dimensions: real user testing, strategy alignment, trade-offs the rubric didn't see, intuition-grade confidence. Goodhart's law applies to rubrics too.

**Feedback triage flow** — once users exist (alpha+), inbound feedback lands in a single inbox (`backlog/FEEDBACK.md`) and gets triaged on a cadence appropriate to the milestone (weekly alpha → 48h closed beta → daily public). Each item routes to bug / feature / question / praise / spam.

### New artifacts shipped

- **[`CHEATSHEET.md`](CHEATSHEET.md)** — one-page quick reference at repo root. ~80 lines (under 100-line cap per E05 charter). Covers all hard rules, the tier matrix, ROI heuristic, lock format, milestones + scoring, and links to full docs for each topic. **Reference, not learning** — full docs remain the source of truth.
- **[`examples/`](examples/)** — fictional `tinker` project (developer-notes CLI) showing the methodology applied end-to-end. Includes strategy master plan with 4 phases + binary exit criteria; 2 pillar files (P1 Capture, P2 Retrieval); EPICS rollup; 1 epic charter; 5 BL items in canonical table-form frontmatter demonstrating all major Status values. All content abstract-voice-compliant (no real product/company references).

### Methodology changes

- **`methodology/00_README.md`** — new section "Why foundational work matters" with a mermaid diagram showing the cascade from brief → goals/milestones → planning → execution → periodic gates → milestone declaration. The diagram explicitly contrasts the foundation-first path with the ad-hoc-work-no-compass failure mode (drift → rework → abandonment). New mental-model sub-section "Plus: the evaluation dimension" introduces doc 12. The main "How the layers connect" diagram extended with a fourth grouping for milestone evaluation. Reading-path table extended with two new rows: "Auditing existing project's process health" and "Running an autonomous loop / scaling AI-assisted work" — both anchored on doc 12.
- **`methodology/12_milestone_evaluation.md`** (new file) — full pattern documented; ~330 lines covering milestones, rubric, periodic-eval cadence, unsolvable handling, human-review gate, feedback triage, worked example.
- **`templates/AUTONOMOUS_LOOP.md`** — extended with: explicit fix-and-adjust gate after each item's verify step (step 5); periodic deep-eval cadence after every Nth loop (step 6); unsolvable-issue handling (step 7); feedback triage (step 9). Stop conditions now include "milestone deep-eval at threshold + maintainer human review confirms ready."
- **`self-development/AUTONOMOUS_LOOP.md`** — adopted the pattern for this project specifically: N = 3 during Phase 1; project-tailored rubric (doc completeness, doc clarity, doc currency, cross-doc consistency, adopter discoverability, tool compatibility, self-improvement velocity, governance integrity); explicit milestone sequence with current state (Alpha met; Closed beta pending external adopters).

### E02 close + WIP cap raised + E01 + E05 close (all three in same release)

- **E02 (first semi-annual self-evaluation pass)** closed earlier this day post-v1.14.0 by maintainer signoff in `self-development/evaluations/2026-05-first-pass.md`. All 5 items (BL-0006/0007/0008/0009/0010) flipped to `Status: done` and moved to E02's `ARCHIVE.md`. **WIP cap raised from 1 to 2** in `self-development/backlog/EPICS.md`.
- **E01 (Examples folder)** closed in v1.15.0; all 5 items in `ARCHIVE.md`; charter Status: active → done.
- **E05 (CHEATSHEET.md)** closed via single-artifact ship; charter Status: planned → done.
- **EPICS rollup** updated: 3 done (E01, E02, E05), 2 planned (E03, E04). The maintainer's next-promotion decision recommends E03 first if continuing autonomous loop work; defer E04 until closed-beta milestone work reveals which native templates adopters actually need.

### Notable for adopters

If you adopt the methodology after v1.15.0:

- Read [`methodology/12_milestone_evaluation.md`](methodology/12_milestone_evaluation.md) when you start your second epic. Doc 12 is the gate that prevents your fast-shipping AI loop from drifting from your strategy.
- The default thresholds (8 min per area, 9 average) are starting points — tune per project, document the choice in strategy.
- The unsolvable-issue heuristic (handle/postpone/mark) is the most-frequently-needed-but-least-applied rule on AI-assisted projects. Make it part of the team's vocabulary.
- The feedback triage flow is load-bearing once you have users. Set the cadence per milestone before you announce alpha.

---

## v1.14.0 — 2026-05-25

### Methodology batch patch — first semi-annual eval cycle complete

The first full self-evaluation cycle on the methodology (E02 in `self-development/`) completes here. Across BL-0006 (skeleton) → BL-0007 (cold-read docs 00–05, 25 findings) → BL-0008 (cold-read docs 06–11, 29 findings + 5 cross-batch) → BL-0009 (two-axis classification of all 59) → BL-0010 (eval-report finalization), the cycle produced **30 patches across all 12 methodology docs**, all shipped here as the cycle's output.

The patches were authored by the autonomous loop, cross-AI tier-verified (5 over-claimed T1s escalated to T2 per escalate-on-doubt), and cross-AI diff-verified on the assembled batch before merge. Maintainer review on the eval report's signoff block closed E02.

**Patches by file:**

- **`methodology/00_README.md`** — reading-path table now includes doc 11; broken `EPICS.md` placeholder anchor fixed (now → `03_epics.md#epic-rollup-epicsmd`); `templates/` folder explained at first reference; Authority section adds reciprocal cross-refs to 01 + 02.
- **`methodology/01_strategy.md`** — Authority section reciprocal cross-ref to 00 + 02.
- **`methodology/02_pillars.md`** — generic P1–P9 inventory now explicitly marked non-canonical (was "illustrative"; now "**illustrative, not canonical** … Do not copy P1–P9 above as your project's pillars"); Authority section reciprocal cross-ref.
- **`methodology/03_epics.md`** — epic-charter template `Started:` field shows the `—` form for `planned` epics (was `YYYY-MM-DD` only, contradicting the prose rule).
- **`methodology/04_backlog_items.md`** — FUTURE.md numbering choice should be recorded in `CLAUDE.md`/`AGENTS.md`/backlog README; lifecycle-diagram explains why mermaid state names use underscores while enum values use hyphens; lock-edit rule acknowledges subagent flows defer to the orchestrator's lock (links to 05).
- **`methodology/05_locks_and_parallel_work.md`** — TTL "default 2 hours" promoted to a bold callout above the table (was buried in prose below); 24h ceiling clarified as "NOT the default" with explicit anti-pattern callout.
- **`methodology/06_working_principles.md`** — "Plan before executing non-trivial work" explicitly marked not a fifth principle (clarifies the count of principles stays at four; this is the gating rule for when the four start applying).
- **`methodology/07_definition_of_done.md`** — quarterly doc-audit scope clarified (covers project living docs; methodology docs get the semi-annual deeper pass); Memory index trigger now mirrors 08's "same commit" phrasing; Gate 6 cross-links 03 (epic rollup format) + 04 (archive mechanics); DoD checklist `Lock: -` (ASCII hyphen) → `Lock: —` (em-dash) to match every other location.
- **`methodology/08_lessons_and_memory.md`** — concrete index-row example added (kebab-slug filename + actionable hook); "Trigger 2: 2+ occurrences" explicitly named as the shared methodology threshold for promotion.
- **`methodology/09_git_workflow.md`** — common patch-branch area prefixes table added (methodology / designsystem / spec / runbook / compliance) with guidance that each project records its allowed prefixes; patch-branch section cross-links to 07 Gate 4 + 10 diff-verification; `git pull --ff-only` row re-labeled "Idempotent sync" (was misleadingly labeled "Read-only sync").
- **`methodology/10_testing_and_verification.md`** — verification levels noted as living on the backlog item (not the PR checklist) for audit trail continuity; "Done-means" term-of-art disambiguated with link to 04's item template; "ratification" → "reviews diffs" framing aligned with 09.
- **`methodology/11_human_roles.md`** — XS/S effort definitions cross-linked to 04's effort scale; "Pricing, business model, contractual terms" row clarifies operational price-list edits inside an approved model are AI-eligible (the *decision* is human-only); "ability matters less" sharpened to "typing speed matters less" (the original phrasing was too broad and read as anti-engineer); decision-ownership matrix gets reciprocal "Pairs with 09" cross-link.

**5 findings escalated T1 → T2 per Sonnet tier-verifier (escalate-on-doubt):** F07 (01 numbering convention — picking a policy), F13 (03 parked→done state-machine — defines new rule or removes edge), F14 (03 "solo: 1" recommendation — new prescriptive default), F21 (04/05 status-flip mandatory — rule wording in lock doc), F40 (09 patch-branch ✗ row — changes AI-autonomy table specificity). All five deferred to maintainer authorship via `self-development/loop-notes/2026-05-25.md`; will land in subsequent maintainer-authored releases.

**Cross-AI diff-verification:** fresh Sonnet 4.6 Explore agent verified the batch on grounded/correct/scoped per `methodology/10` diff-verification mode. Verification log in the commit message of `methodology-patch/2026-05-25-01` branch.

**E02 (first semi-annual self-evaluation) close:**

- All 5 E02 items (BL-0006/0007/0008/0009/0010) at `Status: to-be-tested`, awaiting maintainer signoff in the eval report.
- Eval report fully populated: `self-development/evaluations/2026-05-first-pass.md` (Metadata, Cold-read findings 00–05, Cold-read findings 06–11, Cross-batch inconsistencies, Classification + dispositions, Ship plan, Summary statistics, Next eval date, Maintainer signoff block).
- Next eval target: 2026-11-25.
- 28 T2 findings logged in loop-notes for the next maintainer-authored release cycle.
- After maintainer signoff: BL-0006..0010 flip to `done` + move to `ARCHIVE.md`; E02 charter flips `active → done`; WIP cap rises to 2; the maintainer promotes one of E01/E03/E04/E05 to active.

### Self-development loop runs (Runs 1–4 summary)

Documented in detail in `self-development/loop-notes/2026-05-25.md`. The autonomous loop ran four times across a single day, producing the v1.13.0 adaptation (Run 2's findings → Run 4-equivalent patch demo), the cold-read corpus (Runs 2 + 3), the classification + ship-plan (Run 4), and finally the v1.14.0 batch ship. This is the first complete self-improvement cycle: methodology → loop → findings → classification → patches → methodology.

---

## [Pre-v1.14.0] Self-development loop Runs 1–3 (2026-05-25)

_These notes were under `[Unreleased]` and are now folded into v1.14.0's narrative above._

### Self-development loop Run 3 (2026-05-25) — BL-0008

First run under v1.13.0's tier matrix. Fresh Opus 4.7 general-purpose agent (no prior context, including no exposure to BL-0007's authoring session) cold-read methodology docs 06–11 and landed **29 findings** (0 stale / 14 unclear / 15 inconsistent) under `## Cold-read findings (docs 06–11)`, plus **5 cross-batch inconsistencies** with BL-0007's docs 00–05 batch. Cross-AI validation (fresh Sonnet 4.6 Explore agent, findings-verification mode): **PASS on all four Done-means criteria**, 5/5 sampled citations verified, 3/3 spot-checks grounded.

- Zero stale findings — the methodology's content holds up to current practice; gaps are at clarity and cross-doc consistency axes.
- The two new v1.13.0 sub-sections (patch-branch convention in 09; two-modes diff-verification in 10) were evaluated with full rigor and surfaced real gaps (unspecified area-prefix policy, ambiguous partial-diff PASS/FAIL, conflicting "never auto-merge" framing).
- Per-category `_(none)_` convention from Run 2's loop-notes applied throughout — Done-means verification is now deterministic.
- Sequential two-batch structure (BL-0007 → BL-0008) did real work: 4 cross-batch findings can only be produced by reading the prior batch first.
- BL-0008 now at `Status: to-be-tested`, Test: `pass` (pending cross-AI return); awaiting maintainer done-flip + ARCHIVE move.

Combined corpus across BL-0007 + BL-0008: **~54 findings** queued for BL-0009's two-axis classification (practice/docs framework + patch-tier T0–T3 per v1.13.0). T0/T1 + docs-wrong findings will spawn `methodology-patch/*` branches with cross-AI diff-verification; T2/T3 findings stay in loop-notes for maintainer authorship.

Next run target: BL-0009 + BL-0010 (close E02). EPICS rollup: E02 at 2/0 (+3 to-be-tested).

---

## v1.13.0 — 2026-05-25

### Methodology adaptation — tiered autonomy on authoritative artifacts (2026-05-25)

A maintainer-authored adaptation in response to a structural critique surfaced after Run 2: the original `Constraint 1` ("loop never edits `methodology/` autonomously") was over-broad, reducing self-*development* to self-*evaluation*. The loop could discover methodology gaps but couldn't translate them into fixes — every improvement became maintainer homework, breaking the compounding promise of self-improving cycles.

**The adaptation: tiered autonomy with maintainer-merge gate.**

The loop's permission to *change* the methodology now scales with patch risk (T0/T1 enabled with cross-AI diff-verification, T2/T3 advice-only). The maintainer's role shifts from *translator* (read finding → write fix → verify) to *reviewer* (yes/no on a verified diff). Trunk protection is preserved — the loop never merges, the maintainer ratifies every patch.

**Methodology changes:**

- **`templates/AUTONOMOUS_LOOP.md`** — new section "Tiered autonomy for authoritative artifacts" with the four-tier matrix (T0 cosmetic / T1 surgical / T2 substantive / T3 architectural) and the three safety rules (tier classification cross-AI verified, never auto-merge, CHANGELOG in same commit).
- **`methodology/09_git_workflow.md`** — new section "Patch-branch convention for authoritative artifacts" defining the `<area>-patch/YYYY-MM-DD-NN` branch naming (generic — adopters can apply to methodology, design systems, regulatory checklists, etc.).
- **`methodology/10_testing_and_verification.md`** — extended cross-AI validation with a "Two modes: findings-verification and diff-verification" sub-section. Diff-verification is the gate for the patch-branch convention; the validator checks grounded/correct/scoped on every loop-proposed edit.
- **`self-development/AUTONOMOUS_LOOP.md`** — Constraints 1, 2, 2a rewritten from "never modify autonomously" to the tier matrix applied to methodology/templates/brief+strategy+pillars respectively. T0/T1 enabled with diff-verification; T2/T3 disabled (loop drafts in `loop-notes/`, maintainer authors).

**Demonstration patch (first self-improvement output of the cycle):**

- **`methodology/04_backlog_items.md` lines 813–839 — stale grep examples fixed.** Run 2's cold-read identified this as the only Tier-A finding: the grep patterns used `\| \*\*Pillar\*\* +\|` regex against `**bold**` field names, but v1.12.0's C1 fix rewrote items to plain-table form (no markdown bold). Examples returned zero matches against compliant items. Patch removes the `\*\*` wrappers (and stale `\`backtick\`` wrappers around status values) from all eight examples. This is the *first* methodology change produced by the self-development cycle — discovered by the loop, fixed on this adaptation branch as the proof of concept, will land via the same patch-branch convention going forward.
  - **Cross-AI diff-verification (2026-05-25):** Fresh Sonnet 4.6 Explore agent verified per the new diff-verification mode in `methodology/10`. **PASS on all three axes:** grounded (canonical template + real BL items confirm plain field names; pre-patch examples would return zero matches), correct (patched examples mentally match BL-0007's real `Lock` and BL-0008's real `Status` lines; the one intentional non-change at line 833 — `\*\*Resolution:\*\*` for body-text headings — correctly preserved), scoped (git diff is exactly 8 line changes confined to the cited code block; no whitespace or adjacent-text drift). No follow-up needed in other docs.

**Backlog updates:**

- **BL-0009 charter extended** — classification now happens on two axes (practice/docs framework + patch tier T0–T3). Tier classification is itself cross-AI verified per escalate-on-doubt. Effort raised S → M to reflect dual-axis work and the ~50-finding corpus. T0/T1 findings spawn separate patch-branch items rather than executing in BL-0009 (each patch gets its own diff-verification gate).

**Why this is a methodology release, not a self-development internal change:** the tier matrix + patch-branch convention + diff-verification mode are generic patterns. Any adopter with authoritative artifacts (design systems, regulatory checklists, upstream contracts, upstream specs, or — in our case — a methodology) can apply them. They don't depend on this project's specific shape.

---

### Self-development loop runs (2026-05-25) — Run 1 + Run 2

The autonomous loop ran twice on 2026-05-25 against the E02 (first semi-annual self-evaluation) backlog. No methodology files changed — both runs operate on `self-development/` only, per the loop's hard constraints. Surfaced findings + observations queued for the next maintainer-reviewed methodology release.

- **Run 1 — BL-0006 (evaluations skeleton).** Seeded `self-development/evaluations/` with `README.md` and `2026-05-first-pass.md` skeleton (six section headings, all empty placeholders). No methodology docs read. Status: `to-be-tested`, awaiting maintainer review.
- **Run 2 — BL-0007 (cold-read of methodology docs 00–05).** Fresh Opus 4.7 general-purpose agent (no prior context) cold-read all six docs and landed 23–25 findings under `## Cold-read findings (docs 00–05)` (3 stale / 12 unclear / 10 inconsistent). Cross-AI validation via fresh Sonnet 4.6 Explore agent: PASS on all three Done-means criteria, 5/5 sampled citations grounded, 3/3 spot-checked findings grounded. Status: `to-be-tested`, Test: `pass`, awaiting maintainer review.

**Methodology-modification recommendations surfaced by Run 2** (logged in [`self-development/loop-notes/2026-05-25.md`](self-development/loop-notes/2026-05-25.md); not auto-applied per Constraint 1):

- **Tier A — patch immediately:** `methodology/04_backlog_items.md` grep examples (lines 813–839) use stale `\*\*bold\*\*` field-name regex that returns zero matches against v1.12.0 plain-table items.
- **Tier B — clarify in patch release:** ~6 cross-doc agreement / missing default callouts (reading-path table omits doc 11; WIP-cap default presentation; Lock+Status coupling "automatic" vs "optional" mismatch; etc.).
- **Tier C — defer or treat as known limitations:** ~18 vaguer findings (e.g., the "strategy outranks pillars" rule restated in three docs with drift risk).
- **Operational pattern from Run 2:** "fresh session" definition in `AUTONOMOUS_LOOP.md` should clarify that cold-read agents need Write/Edit tools (use `general-purpose`, not `Explore`).

Formal classification + disposition for all findings happens in BL-0009; this is a preview.

**Bootstrap status:** loop is operational. E02 BL-0006 and BL-0007 complete (work + cross-AI), awaiting maintainer's done-flip. Next run target: BL-0008 (cold-read of methodology docs 06–11).

---

## v1.12.0 — 2026-05-25

### Chore — Opus cross-check applied to the bootstrap; eight fixes before Run 1 (2026-05-25)

After v1.11.0 declared the bootstrap complete and the autonomous loop operational, an Opus-tier cross-check ran against the entire `self-development/` folder as a coherent system (not per-step like prior reviews). The Opus reviewer surfaced one blocker plus seven supporting issues that the per-step Sonnet-tier reviews missed because each saw only one step at a time.

**Critical (blockers fixed before Run 1):**

- **C1 — All 14 BL-#### items rewritten to methodology-conformant frontmatter.** Prior items used a `**Pillar:** P3` bold-label shorthand format. The methodology in [`methodology/04_backlog_items.md` lines 91–116](methodology/04_backlog_items.md) requires a **table-form frontmatter** with `| Field | Value |` shape (`Epic`, `Pillar`, `Priority`, `Effort`, `Status`, `Test`, `Deps`, `Lock` — 8 required fields, table form). The greppable-metadata patterns in the methodology depend on this shape. All 14 items now use the table form. Body sections also restructured: prior items used `**Goal:** / **Plan:** / **Verification:**`; methodology requires `**Why / Description:** / **Approach:** / **Done means:** (checkboxes) / **Files (probable):**`. The `Done means:` checkbox section — load-bearing per `04_backlog_items.md` lines 374–404 as the item-level exit criteria — was missing from every item and is now present.
- **C2 — Master plan Phase 1 exit criterion 3 reworded.** Was: "All five templates exist *and have been tested by at least one external session.*" The italicized half is adopter-dependent (maintainer can't tick it autonomously) — same anti-pattern that was caught in P4's exit criteria during v1.8.0 cross-AI review but survived in the master plan one level up. Now: external-adoption testing is tracked as a **health indicator**, not a phase-exit criterion.
- **C3 — Template-count vs tool-count terminology drift fixed in 5 places.** Prior text variously said "5 templates" / "6 tools" / "all six major AI coding tools" in master plan, AUTONOMOUS_LOOP, brief/08, P1, P4. The canonical framing now (consistent everywhere): **5 template files in `templates/` supporting 6 AI tools — 3 natively (CLAUDE.md, AGENTS.md, AGENTS.md again for Antigravity), 3 via adaptation from AGENTS.md (Cursor, Aider, Continue.dev). E04 in the backlog tracks promoting the latter to native templates.**

**Should-fix (applied):**

- **S1 — WIP cap dropped from 3 to 1.** Per `methodology/03_epics.md` "Smaller teams should run fewer" — and per the Opus cross-check — a solo-maintained project that has never closed an epic should start at 1 active. E02 stays active; E01 + E03 + E04 + E05 are now all `planned`. WIP cap rises after the first epic-close. Documented in `self-development/backlog/EPICS.md` "WIP cap note" and `self-development/backlog/README.md` Workflow section.
- **S2 — `AUTONOMOUS_LOOP.md` Constraint 2a extended.** Was: "Never modify `self-development/strategy/` or `self-development/pillars/` autonomously." Now also covers `self-development/brief/` (the upstream-of-strategy artifact that prior constraint missed).
- **S3 — BL-0006 plan tightened.** Was ambiguous about "create template" vs "create first eval report." Now: explicit "**skeleton-only work — no findings data is recorded in this item; no methodology docs are read; the cold-read happens in BL-0007/0008.**" Plus a Done-means checkbox: "No methodology doc was read or analyzed during this item's execution."
- **S5 — "Fresh session" defined operationally in AUTONOMOUS_LOOP.md.** Was used multiple times (cross-AI validation, BL-0007/0008 cold-reads) without definition. Now: a new chat/agent session with no prior turns referencing this project; strongly preferred to be a different model family than the one that authored the artifact being reviewed.
- **S7 — BL-0007 + BL-0008 changed from parallel to sequential.** Was: "Run 2 — BL-0007 and BL-0008 (can be done in parallel sessions if context allows)." But BL-0008's verification asks for cross-doc inconsistencies vs. BL-0007's batch — which requires BL-0007's findings to be in the report first. Now: Run 2 = BL-0007 only; Run 3 = BL-0008.

**Additional improvements surfaced by the cross-check:**

- BL-0012 explicitly marked as touching `methodology/*` and thus requiring maintainer handoff (the loop's Constraint 1 forbids it from executing this item autonomously). The loop's role is to prepare via BL-0011 and then halt for human-authored execution.
- BL-0007/0008/0009/0010 now explicitly bring their items to `Status: to-be-tested` and halt for maintainer approval before flipping to `done` (per S6 epic-closure handling).

**What was NOT changed:**

- Pillar dependency chain (P1→P2→P3→P4→P5→P6→P7→P8→P9) stays as defined in v1.8.0; the cross-check confirmed it's coherent.
- Strategy phases (Foundation / Discovery / Establishment / Maturity) stay as defined; exit criteria all binary except C2's fix.
- Epic charters (E01–E05) unchanged in scope; only the items below them changed in format.

**Verification:** confirmed via PowerShell that `self-development/evaluations/` and `self-development/loop-notes/` directories do NOT yet exist — BL-0006 has real work to do when Run 1 fires.

**Bootstrap status after this release:**

- ✓ Steps 0–4 shipped (v1.7.0 → v1.11.0)
- ✓ Opus-tier cross-check applied with all critical + key should-fix issues addressed (v1.12.0)
- **Ready for Run 1** of the autonomous loop, targeting BL-0006 (P1-XS) end-to-end through DoD.

---

## v1.11.0 — 2026-05-25

### Feat — Self-development bootstrap, Step 4 (final): autonomous loop is operational (2026-05-25)

**Step 4 of the self-development bootstrap — the final step.** Ships `self-development/AUTONOMOUS_LOOP.md` (282 lines), the specialized loop prompt for this project. After this release, the autonomous loop is **operational** — the maintainer can start the first run targeting BL-0006 whenever convenient.

**New file `self-development/AUTONOMOUS_LOOP.md`** adapts [`templates/AUTONOMOUS_LOOP.md`](templates/AUTONOMOUS_LOOP.md) with this project's specifics:

- **Project context** — points the loop at `self-development/backlog/`, references the master plan and pillars, names the current Phase 1 primary pillars.
- **Hard constraints (non-negotiable):**
  - **Constraint 1** — never modify abstract `methodology/` docs autonomously. Insights logged to `self-development/loop-notes/YYYY-MM-DD.md`; methodology changes ship via normal release cycle.
  - **Constraint 2** — never modify `templates/` autonomously.
  - **Constraint 2a** — never modify `self-development/strategy/` or `self-development/pillars/` autonomously. Worksurface is `self-development/backlog/`, `self-development/evaluations/`, `self-development/loop-notes/`.
  - **Constraint 3** — production deploys, force-push, destructive git ops, GitHub Release creation — never autonomously.
  - **Constraint 4** — never delete content silently; removals logged with reasoning in item bodies.
- **Items the loop should NOT pick** — 8-row negative list covering third-party PRs, social media work, items depending on user feedback, items requiring credentials, legal/business judgment, methodology design changes, epic-closure approvals, performance benchmarking, and git history rewrites.
- **Stopping conditions** — 7 binary conditions: run target reached / no ready items / constraint at risk / time-box elapsed / item entered cross-AI validation gate / HUMAN_NEEDED.md grew by ≥3 / maintainer halt.
- **First-run targets** — bounded per Phase 1 exit criterion 4: complete BL-0006 (P1-XS, smallest P1 item) end-to-end through DoD, then halt. Validates the loop works at all before scaling up.
- **Subsequent-run target ramp** — Run 2: BL-0007 + BL-0008; Run 3: BL-0009 + BL-0010 (close E02); Run 4+: opportunistic E01 + E03 work.
- **The adapted prompt** — paste-and-go for an AI agent session running the loop. Embeds the constraint references; cross-links every methodology section the loop applies.
- **Post-run report template** — structured for maintainer action: items completed, items started but not completed, cross-AI validation needs, HUMAN_NEEDED.md additions, methodology-change suggestions surfaced (logged to `loop-notes/`, not auto-applied), recommendation for next run target.
- **Integrity rule** — strong: "Never claim an item is done, tested, or DoD-passed unless it was actually verified. Honest partial progress beats false completion."

**Cross-AI review applied before ship.** Per the bootstrap plan's DoD ("stopping conditions clear? constraints prevent damage to abstract docs? targets concrete?"), a fresh Explore agent reviewed cold. Verdict: **ship with one enhancement + two clarifications.** All three applied:

1. **Constraint 2a added** — the original Constraints 1 + 2 covered `methodology/` and `templates/` but didn't explicitly cover `self-development/strategy/` and `self-development/pillars/`. Reviewer flagged this as implicit in Phase 1 but worth making explicit for Phase 2+ work.
2. **Negative-list row on epic closure** — clarified that the loop completes the closing item's *work* (deliverable + verification + closure note) and brings it to `Status: to-be-tested`, then halts. The final `Status: done` flip happens after maintainer approval.
3. **Negative-list row on performance benchmarking + git history rewrite** — added as new categories of work the loop should not pick autonomously.

The reviewer's overall assessment: all stopping conditions are mechanically detectable; Constraints 1 + 2 (now + 2a) are clear and enforceable; targets are concrete and phase-aligned; reporting protocol is actionable; integrity rule is strong.

**README updates:**

- `What's in the repo` tree now shows `self-development/AUTONOMOUS_LOOP.md`.
- Line-count claim refreshed (~11,000 → ~11,400); file count 51 → 52.

**Bootstrap status — COMPLETE:**

- ✓ Step 0 (brief) — v1.7.0
- ✓ Step 1 (strategy + pillars) — v1.8.0
- ✓ Step 2 (first epics) — v1.9.0
- ✓ Step 3 (first items) — v1.10.0
- ✓ Step 4 (autonomous loop setup) — **this release (v1.11.0)** — **the cycle is now operational**
- Step 5+ — continuous cycle runs gated only on the maintainer triggering each run

**What's now possible:** the maintainer can start the first autonomous loop run at any time. Per the loop's first-run target, the first run targets only BL-0006 and halts after completion — validates the loop works before scaling up. After Run 1's success, subsequent runs ramp toward closing E02, then opportunistic E01 + E03 work.

**The self-improving cycle this entire bootstrap was building toward is now live.**

---

## v1.10.0 — 2026-05-25

### Feat — Self-development bootstrap, Step 3: 14 BL-#### items across 3 active epics (2026-05-25)

Step 3 of the self-development bootstrap. Populates each active epic's `BACKLOG.md` with 4–5 BL-#### items, each with full frontmatter (Pillar / Priority / Effort / Status / Test / Lock / Deps) and body (Goal / Plan / Verification). Total: 14 items, BL-0001 through BL-0014.

**Three new `BACKLOG.md` files** in `self-development/backlog/epics/`:

- **`01-examples-folder/BACKLOG.md`** (5 items, BL-0001 to BL-0005, all P2 — epic doesn't gate Phase 1 exit) — folder setup → strategy/pillars example → epic + items example → cross-AI abstract-voice review → close. Sequentially dependent.
- **`02-first-semiannual-self-evaluation/BACKLOG.md`** (5 items, BL-0006 to BL-0010, all P1 — epic gates Phase 1 exit per master plan criterion 2) — eval folder + template → cross-AI cold-read of methodology docs 00–05 → cold-read of docs 06–11 (parallelizable) → classify gaps → finalize report + close.
- **`03-git-workflow-trim/BACKLOG.md`** (4 items, BL-0011 to BL-0014, all P2) — analyze + decide trim-vs-split → execute → update cross-references → closure note with clarity assessment.

**Priority discipline** follows the master plan's Phase 1 exit criteria: E02 items P1 (semi-annual self-evaluation gates Phase 1 exit), E01 + E03 items P2 (planned but not blocking). ROI ordering follows: pick P1 items first (BL-0006 first, then BL-0007/0008 in parallel, then BL-0009, then BL-0010), then move to P2 work within E01 and E03.

**Cross-AI review applied before ship.** Per the bootstrap plan's DoD ("specific enough for cold pickup? Effort realistic? ROI ordering coherent?"), a fresh Explore agent reviewed all 14 items cold. Verdict: **ship with no revisions required.** Spot-checks:

- **Cold pickup:** all 14 items workable without asking maintainer for clarification. Three items (BL-0007, BL-0008, BL-0012) flagged with minor guidance-tightening opportunities but explicitly non-blocking.
- **Effort estimates:** all defensible (XS/S/M/L distribution matches plan scope per item).
- **ROI ordering:** Phase-aware, dependency-clean, no circular deps; correctly front-loads P1 work in E02.
- **Frontmatter completeness:** all 14 items have complete tables (Pillar, Priority, Effort, Status, Test, Lock, Deps where relevant).
- **Hard-rule compliance:** no item has `Status: done` inappropriately; dependency graph acyclic.

**README updates:**

- Line-count claim refreshed (~10,600 → ~11,000); file count 48 → 51.
- Tree unchanged (no new folders this release; only `BACKLOG.md` files added inside existing epic folders).

**Bootstrap status:**

- ✓ Step 0 (brief) — v1.7.0
- ✓ Step 1 (strategy + pillars) — v1.8.0
- ✓ Step 2 (first epics) — v1.9.0
- ✓ Step 3 (first items) — this release (v1.10.0)
- Pending: Step 4 (autonomous loop setup) — `self-development/AUTONOMOUS_LOOP.md` adapted from the template with this project's targets + constraints. **This is the last step before the cycle becomes operational.**

Step 4 ships as the next minor release; after Step 4, the autonomous loop can start running between user check-ins.

---

## v1.9.0 — 2026-05-25

### Feat — Self-development bootstrap, Step 2: first 5 epic charters (2026-05-25)

Step 2 of the self-development bootstrap. Charters the first 5 epics that move the methodology forward in Phase 1 (Foundation), respecting the methodology's WIP cap of 3 active. The backlog scaffolding (README + EPICS.md rollup + HUMAN_NEEDED.md) is also seeded.

**New folder `self-development/backlog/`** with:

- **`README.md`** — backlog workflow doc, mostly a pointer to [`methodology/04_backlog_items.md`](methodology/04_backlog_items.md). Two project-specific overrides: (1) the autonomous loop (once operational after Step 4) MUST NOT modify abstract methodology docs autonomously; (2) all self-development releases ship as minor/patch versions of the public repo.
- **`EPICS.md`** — rollup table of 5 epics with status, pillar coverage (forward + inverse), and WIP cap discipline. Currently 3 active / 2 planned / 0 done.
- **`HUMAN_NEEDED.md`** — empty seed for items blocked on human-only action.

**Five new epic charters in `self-development/backlog/epics/`** following the [`methodology/03_epics.md`](methodology/03_epics.md) skeleton:

| Epic | Pillar (primary + secondary) | Status | Charter focus |
|---|---|---|---|
| **E01 — Examples folder** | P1 + P6 | active | `examples/` folder at repo root with at least one fully-worked anonymized example (strategy doc + 2-3 pillars + 1 epic + 5+ BL items). Closes the longstanding "no examples/ folder" gap. |
| **E02 — First semi-annual self-evaluation pass** | P3 + P2 | active | Instantiates the [self-evaluation cadence](methodology/07_definition_of_done.md#methodology-self-evaluation-semi-annual) added in v1.6.0. Cold-read every methodology doc, classify gaps as "practice wrong / docs wrong / both," ship fixes. |
| **E03 — Trim or split `09_git_workflow.md`** | P2 | active | `09_git_workflow.md` at 986 lines is the longest methodology doc, approaching the 1,050 soft cap. Trim or split. Decision documented. |
| **E04 — Native templates for Cursor / Aider / Continue.dev** | P4 | planned | Reduce friction for adopters using these tools — currently they adapt `AGENTS.md`. Native templates with drift-prevention notes. |
| **E05 — CHEATSHEET.md** | P1 | planned | One-page quick reference (under 100 lines) covering the methodology's key patterns. |

**Cross-AI review applied before ship.** Per the bootstrap plan's DoD, a fresh Explore agent reviewed the charters cold and reported four revisions, all applied:

1. **E01 exit criterion 5** — replaced subjective "explains the relationship" with binary 3-row comparison table check ("a cross-AI reader can correctly map each artifact type to its purpose after one read").
2. **E03 exit criteria** — added new criterion requiring the closure note to include a clarity assessment comparing post-change to v1.6.0 baseline (so E03 closure doesn't depend on E02's future eval timing). Moved the forward-looking clarity measurement from KPI to "Long-term clarity" reframing.
3. **E04 exit criterion 4** — tightened smoke-test definition: was "tool reads it, methodology rules show up"; now ≥3 specific methodology terms (e.g., "WIP limit", "exit criteria", "lock TTL") appear in agent context when queried.
4. **E05 KPI 1** — reframed from unverifiable "top-5 most-viewed files" to binary "≥3 Discussions threads or external mentions reference 'cheatsheet' or 'quick reference' within 60 days," with GitHub Insights as backup if available.

Pillar alignment, out-of-scope rigor, and WIP discipline were all confirmed solid by the reviewer.

**README updates:**

- `What's in the repo` tree now shows `self-development/backlog/`.
- Line-count claim refreshed (~10,100 → ~10,600); file count 40 → 48.

**Bootstrap status:**

- ✓ Step 0 (brief) — v1.7.0
- ✓ Step 1 (strategy + pillars) — v1.8.0
- ✓ Step 2 (first epics) — this release (v1.9.0)
- Pending: Step 3 (first items — populate each active epic's `BACKLOG.md` with 3-10 BL-#### items)
- Pending: Step 4 (autonomous loop setup)

Step 3 ships as the next minor release when ready.

---

## v1.8.0 — 2026-05-25

### Feat — Self-development bootstrap, Step 1: strategy master plan + 9 pillars (2026-05-25)

Step 1 of the self-development bootstrap. Converts the Step 0 brief (shipped in v1.7.0) into a strategy master plan with four binary-exit-criteria phases and nine capability-layer pillar definitions. The strategy + pillars together are now the substrate Step 2 (epics) will charter against.

**New file `self-development/strategy/00_master_plan.md`** (~175 lines)

The strategy master plan for the methodology project itself. Sections:

- **Vision (condensed)** — methodology + self-improving cycle in one paragraph; full vision in [brief/01_vision.md](self-development/brief/01_vision.md).
- **Four phases** with binary exit criteria each:
  - **Phase 1 — Foundation** (~3 months): methodology complete; self-development bootstrap operational. Exits on bootstrap Steps 0–4 shipped + no known self-contradictions + all 6 tool templates + first autonomous loop run.
  - **Phase 2 — Discovery** (3–12 months): adopters find the methodology; first stories emerge. Exits on ≥500 stars + ≥10 adoption stories + ≥5 contributions + ≥2 cycle-attributed releases + ≥1 maintained fork.
  - **Phase 3 — Establishment** (12–24 months): on the field map; companies adopt internally. Exits on ≥5 comparison-venue references + ≥3 company adoptions + ≥2 niche forks + sustained ≤40 hours/quarter.
  - **Phase 4 — Maturity** (24+ months, open-ended): cross-pollination to peers; cycle has shifted methodology. Open-ended exit; steady state.
- **Pillar roadmap** — 9-row table showing which pillars are *primary* vs *baseline* vs *dormant* at each phase. P9 (Self-improvement velocity) is primary across all four phases as the cross-cutting mechanism.
- **Document index** — pointers to brief (upstream research), pillars (downstream definitions), methodology (the abstract skeletons followed).
- **Re-evaluation protocol** — three cadences: phase-transition, semi-annual (per [methodology/07_definition_of_done.md](methodology/07_definition_of_done.md)), memory-driven (per the stdlib growth loop).

**Nine new pillar files in `self-development/pillars/`** (~85-95 lines each)

Each follows the [methodology/02_pillars.md](methodology/02_pillars.md) skeleton adapted for a docs-only project (no schema/API/configuration sections; instead: sub-capabilities, exit criteria, dependencies, anti-patterns, current state, delivering epics).

- **P1 — Doc completeness** (foundational; primary in Phase 1).
- **P2 — Doc clarity** (depends on P1; primary in Phase 1).
- **P3 — Doc currency** (depends on P2; primary in Phase 1 + 2).
- **P4 — Tool compatibility** (depends on P3; primary in Phase 1). Resequenced from P6 → P4 during Step 0 review because tool compatibility is a prerequisite for adoption, not downstream of examples.
- **P5 — Adopter discoverability** (depends on P4, P2, P3; primary in Phase 2).
- **P6 — Example richness** (depends on P5, P2; primary in Phase 2).
- **P7 — Community feedback loop** (depends on P5, P6; primary in Phase 2 + 3).
- **P8 — Maintenance sustainability** (depends on P7; primary in Phase 3).
- **P9 — Self-improvement velocity** (depends on P1, P3, P7, P8; primary across all phases — the compounding mechanism).

**Cross-AI review applied before ship.** Per the bootstrap plan's DoD, a fresh Explore agent reviewed the master plan + 9 pillars cold (no prior context from the authoring session) and reported five revisions, all applied before this release:

1. **P1 exit criteria** — tightened the "within ~5 minutes" criterion to a binary form ("response within 30 days links to existing doc or logs gap candidate"); moved subjective indicators to a "Health indicators" section.
2. **P2 exit criteria** — consolidated the three semi-subjective criteria (cross-AI report, senior-engineer-cold-read test, AI-bloat indicators) into one binary form tied to the most recent semi-annual self-evaluation; moved the senior-engineer test to "Health indicators."
3. **P4 exit criteria** — removed the adopter-dependent criterion ("at least one adopter has reported using across two tools") from exit criteria (uncontrollable) and moved to "Health indicators." Replaced with maintainer-testable criterion ("cross-AI review found no tool-specific protocols in `methodology/`").
4. **P8 pillar goal** — reworded from goal-shaped ("stays current with ≤40 hours/quarter sustained") to capability-shaped ("operates with lean, sustainable maintenance overhead indefinitely"). The hour budget remains as a measure, not the capability itself.
5. **Master plan §3 (pillar roadmap)** — added a one-paragraph note explaining the P4 resequencing context (from P6 to P4 during Step 0 review), so future phase re-evaluations have the reasoning visible.

The reviewer also noted one quality-of-life suggestion (cross-reference table in master plan showing which brief metrics feed which phase) — deferred to a future patch release rather than blocking this ship.

**README updates:**

- `What's in the repo` tree shows `self-development/strategy/` and `self-development/pillars/`.
- Line-count claim refreshed (~9,100 → ~10,100); file count 30 → 40.

**Bootstrap status:**

- ✓ Step 0 (brief) — v1.7.0
- ✓ Step 1 (strategy + pillars) — this release (v1.8.0)
- Pending: Step 2 (first epics)
- Pending: Step 3 (first items)
- Pending: Step 4 (autonomous loop)

Step 2 ships as the next minor release when ready.

---

## v1.7.0 — 2026-05-25

### Feat — Self-development bootstrap, Step 0: the brief (2026-05-25)

The methodology is now applied to its own development as a self-improving cycle. A new top-level `self-development/` folder hosts the work; this release ships Step 0 (the brief), which back-engineers the project's intent into the eight inputs the methodology's own Step 0 prescribes.

**New folder `self-development/`** — top-level folder for the methodology applied to itself. Mirrors the layout in [`templates/PROJECT_STRUCTURE.md`](templates/PROJECT_STRUCTURE.md). Grows as subsequent bootstrap steps complete (Step 1: strategy + pillars → v1.8.0; Step 2: epics; Step 3: items; Step 4: autonomous loop; Step 5+: continuous loop runs).

**Nine new files in `self-development/brief/`** — eight detail files plus one TL;DR index:

- `00_brief.md` — TL;DR index with at-a-glance table linking the eight detail files.
- `01_vision.md` — what the methodology is for; 1-year and 3-year success horizons; what success is NOT.
- `02_audience.md` — four primary segments (solo + AI; small mixed teams; indie hackers / startup founders; engineering leaders adding AI to existing workflows) plus three secondary (AI-tool builders, educators, researchers) plus explicit non-audience.
- `03_competitive_landscape.md` — nine named alternatives surveyed: GitHub Spec Kit (~106k★), BMAD, Ralph loop, stdlib pattern, AGENTS.md standard, GSD, nano-spec, vendor docs, academic papers. Each entry: what it does well, where it falls short, relationship to this methodology.
- `04_market_gaps.md` — nine concrete gaps the alternatives leave unaddressed (cheating-agent anti-pattern, locks for humans+agents, challenge-before-consenting prompt, four-layer planning, DoD coupled to item, HUMAN_NEEDED.md, ROI heuristic, self-evaluation cadence, decision-ownership matrix).
- `05_success_metrics.md` — concrete 1-year (6 metrics) and 3-year (6 metrics) outcomes plus what's NOT a metric plus counter-signals plus review cadence.
- `06_distribution.md` — distribution channels (primary + secondary + out of scope), lean-maintainer sustainability model (≤40 hours/quarter target), when this transitions from "reference artifact" to "shared infrastructure."
- `07_tech.md` — markdown + git substrate, in-scope tooling, deliberate non-goals (no CI for docs, no translation infrastructure, no CLI for the methodology itself).
- `08_capability_layers.md` — nine capability layers that become pillars in Step 1, with explicit sequential dependencies.

**Cross-AI review applied before ship.** Per the bootstrap plan's DoD, a fresh Explore agent reviewed the brief cold (no prior context from the authoring session) and reported four minor revisions, all applied before this release:

1. `01_vision.md` — hedged "twice as fast" claim (was presented as fact; now framed as a hypothesis worth acting on, with adopter telemetry called out as a thing the 1-year metrics aim to surface).
2. `03_competitive_landscape.md` — added explicit snapshot-in-time note (the inverse "no peer has X" claims needed this hedge so future readers don't treat them as permanent statements).
3. `02_audience.md` — added problem-bridge paragraph linking the four segments to a single underlying problem ("software projects accumulate methodology debt fast when AI agents are in the contributor mix").
4. `08_capability_layers.md` — resequenced Tool compatibility from P6 → P4 (prerequisite for adoption, not downstream of examples). Adopter discoverability and Example richness shifted to P5 and P6 accordingly. Dependency diagram and 00_brief.md TL;DR table updated to match.

**README updates:**

- `What's in the repo` tree now shows `self-development/`.
- Line-count claim refreshed (~8,200 → ~9,100); file count 21 → 30 (per the convention of excluding `.github/` from the tree count).

**Bootstrap plan reference.** This release is Step 0 of the gated bootstrap plan described in the maintainer's harness plan file. Step 1 (strategy + pillars) is gated on this brief being stable. Each subsequent step gates on the previous step's DoD passing (cross-AI review + maintainer approval).

---

## v1.6.0 — 2026-05-25

### Feat — Methodology self-evaluation cadence + five git-workflow additions (2026-05-25)

Closes two gaps: a meta-layer for keeping the methodology docs honest as practice evolves, and five concrete git practices that adopters routinely re-derive.

**`methodology/07_definition_of_done.md` — new section "Methodology self-evaluation (semi-annual)"** (~40 lines)

Sits as a parallel concept to the existing "Periodic repo health audits (quarterly)" subsection — same shape, different surface. The quarterly audit checks code health; the semi-annual self-evaluation checks doc health. Names the failure mode (methodology and practice drift apart over months), the cadence (every six months), the protocol (re-read every doc cold; classify gaps as "practice is wrong" / "docs are wrong" / "both"; ship updates via the existing promotion loop), and the reverse case (a doc that gets ahead of practice and never gets used). Explicit cross-references to the existing "Memory as a leading indicator" and "Promotion path" patterns so the new section sits within the lessons-learned ecosystem rather than standing alone.

**`methodology/09_git_workflow.md` — five new sections** (~260 lines total)

The doc was solid on day-to-day flow but missing several patterns adopters consistently hit. Each new section sits at its natural point in the existing flow:

- **"Lock-file management"** (~60 lines) — after Commit message convention. The rule (lock files are committed), a table of when agents should update them (yes for explicit dependency changes, no for spurious `npm install` diffs), how to discard spurious lock-file diffs, what to do when the diff is huge, and why this matters specifically for AI-agent workflows where unintended transitive bumps bloat PRs.
- **"Squash, merge, or rebase — picking the trunk-merge strategy"** (~40 lines) — after PR discipline. Comparison of the three GitHub merge strategies with a default recommendation (squash) and explicit exceptions (monorepos, multi-step refactors where per-commit attribution matters, `git bisect` precision needs).
- **"What AI agents can and can't do in git — the affirmative list"** (~60 lines) — after Destructive command discipline (which is the negative list). A 23-row table pairing each common git/`gh` operation with an autonomy level (✓ / ⚠ / ✗) and the principle that *reversibility maps to autonomy*. Pairs with the decision-ownership matrix in `11_human_roles.md`.
- **"Release tagging and semantic versioning"** (~70 lines) — after Production deploys. When to cut a release (three triggers); SemVer rules with a heuristic for when to bump MAJOR vs MINOR vs PATCH ("if an adopter who pinned to the previous version would have to do work to upgrade, it's at least a MINOR; if they'd have to change their existing usage, it's a MAJOR"); release commit shape; annotated vs lightweight tags; two-step push pattern (commit then tag); release-notes-vs-CHANGELOG relationship; four anti-patterns including sequential patch releases for trivial fixes (the day's own bad habit, now codified as a thing not to do).
- **"Hot-fix workflow"** (~50 lines) — right after Release tagging. When justified (high bar: outage, security vuln, regression, data-integrity issue); eight-step protocol (branch from tag not main, scope ruthlessly, test per DoD, file P0 item, PR review at urgency-not-skipped pace, cherry-pick to release branches if any, tag patch release, archive); post-mortem write-up with three concrete questions; what hot-fixes are NOT (not a DoD bypass, not an audit-trail skip, not a scope-expansion vehicle).

**Mechanical:** README line-count claim refreshed (~8,000 → ~8,200); longest-doc claim refreshed (~900 → ~1,000) — `methodology/09_git_workflow.md` is now the longest at 986 lines, taking the spot from `methodology/04_backlog_items.md` (895).

Discovery: user asked "what would you add to `09_git_workflow.md`?" plus an explicit ask for a self-evaluation cadence that "merges smoothly with existing logic." Both addressed; all five git-workflow proposals shipped together.

---

## v1.5.1 — 2026-05-25

### Docs — Decouple `HUMAN_NEEDED.md` from the autonomous loop (2026-05-25)

The v1.5.0 docs cross-wired `HUMAN_NEEDED.md` and the autonomous loop in three places — describing the loop as "surfacing" blocked items to `HUMAN_NEEDED.md` at check-in time. That overstated the coupling. `HUMAN_NEEDED.md` is a **passive registry**, not an actively-managed surface: items land in it via the normal blocked-item protocol (agent sets `Status: blocked`, releases lock, adds the `**Blocker:**` line, adds the one-line entry); humans scan it when they check in; the loop simply stops touching blocked items because they leave the ready set.

Three places updated:

- `methodology/00_README.md` — the "long-term multi-session work" section's autonomous-loop bullet no longer says the loop "surfaces" blocked items; it says blocked items leave the ready set via the normal protocol, and the loop stops touching them.
- `methodology/04_backlog_items.md` — the `HUMAN_NEEDED.md` section's "How this interacts" subsection removed the "Autonomous loops" bullet entirely. Replaced with a one-paragraph framing: "The file is a passive registry, not an actively-managed surface — the autonomous loop does not interact with `HUMAN_NEEDED.md` directly."
- `README.md` — the "Long autonomous runs..." table row now reads "Stops at milestone, when no ready items remain, or on user check-in" instead of "Stops on milestone or surfaces blockers to `HUMAN_NEEDED.md`."

The `HUMAN_NEEDED.md` pattern itself is unchanged — the file, the protocol, the cross-references to locks and the decision-ownership matrix all stay.

---

## v1.5.0 — 2026-05-25

### Feat — Long-term multi-session work + HUMAN_NEEDED.md + ROI prioritization + PROJECT_STRUCTURE template (2026-05-25)

Closes several gaps around the methodology's "work compounds across sessions, contributors, and tools" property — making explicit the mechanisms that were implicit, plus a new template for the folder layout adopters need.

**`methodology/04_backlog_items.md` — new section "Prioritization — the ROI heuristic"** (~50 lines)

Names the default rule for picking the next item: **highest-impact-per-effort**. With `Priority:` (P0–P3) and `Effort:` (XS–XL) both required on every active item, the picking order falls out as a small table (P1-XS first; P2-M defer unless scheduled; P3-any belongs in `FUTURE.md`). Explicit "when to deviate" guidance: user-direction wins, near-met epic-exit-criteria wins locally, just-unblocked-dependency wins for context-freshness. Used directly by the autonomous loop to converge on milestone outcomes rather than meandering through interesting-but-low-impact work.

**`methodology/04_backlog_items.md` — new section "`HUMAN_NEEDED.md` — work blocked on human agency"** (~80 lines)

A dedicated file at `backlog/HUMAN_NEEDED.md` (sibling of `EPICS.md`) tracking items blocked on human-only action: physical actions, credentials AI doesn't have, legal/ethical judgment, decisions reserved for humans (per the [decision-ownership matrix](methodology/11_human_roles.md)), in-person testing. Protocol: agent sets `Status: blocked`, releases the lock, adds a `**Blocker:**` line in the body, adds a one-line entry to `HUMAN_NEEDED.md` linking the BL item, and moves on to the next ready item. Prevents deadlock on human-gated work; gives humans a single place to scan pending delegations. Skeleton + "what doesn't belong here" rules + cross-references to locks/decision-matrix/autonomous-loop included.

**`methodology/00_README.md` — new section "How the system enables long-term, multi-session work"** (~40 lines)

Makes explicit the property adopters were having to derive: work *compounds across time* without depending on a single contributor's continuous attention. Names the three mechanisms (plans persist in files; backlog is the queue; autonomous loop runs unsupervised) and the patterns that exploit them (drop-and-resume, hand-off between agents, vendor switching, multi-day milestone push). This is what makes the methodology suitable for long-running projects, not just current-session work.

**`templates/PROJECT_STRUCTURE.md`** — new template (~140 lines)

A recommended folder structure and file-naming convention for projects adopting the methodology. Covers:

- **Top-level layout** — `docs/{strategy,pillars,planning,architecture,operations,audits,methodology}/`, `backlog/`, `memory/`, plus the conventional file roles at each level.
- **File-naming patterns** — strategy docs `NN_topic.md`, pillars `P<#>_<slug>.md`, epic folders `NN-slug`, work items `BL-####` monotonic repo-wide, memory entries `<type>_<topic>.md`, runbooks `<scenario>_runbook.md`, audits `<topic>_audit_YYYY-MM-DD.md`.
- **ID-space rules** — work-item IDs (`BL-####`) are repo-wide-monotonic, never per-epic, so items can move between epics without renumbering and `grep BL-0428` is unambiguous.
- **"What lives where" quick-reference table** — most common questions ("Why does this product exist?" → `docs/strategy/00_master_plan.md`) mapped to file paths.
- **Project-instruction filename per AI tool** — Claude Code / Codex / Antigravity / Cursor / Aider / Continue.
- **Explicit non-goals** — project-specific code layout, CI/CD configs, external trackers, specific test frameworks.

**`README.md` — five new "Why this exists" rows** linking to the methodology sections above: long-term multi-session, ROI prioritization, HUMAN_NEEDED, autonomous loop convergence, ARCHIVE/FUTURE searchability.

**`README.md` — Diagram 2 updated** to show `backlog/HUMAN_NEEDED.md` alongside `backlog/EPICS.md` at the backlog root.

**Mechanical:** README line-count claim refreshed (~7,500 → ~8,000); file count 20 → 21; "longest doc" ~780 → ~900 (`04_backlog_items.md` grew from 778 to 894 lines with the two new sections).

Research origin: a survey of patterns from a real production project's `backlog/` and `docs/` folders. Project-specific patterns (e.g., `OWNER_ACTIONS.md`, `docs/operations/SUPPORT_RUNBOOK.md`, `docs/audits/*`) were abstracted into project-agnostic guidance (`HUMAN_NEEDED.md`, runbook naming conventions, integrity-check archiving). No project-specific names or domain references introduced.

---

## v1.4.3 — 2026-05-25

### Docs — Drop oddly-specific "every six months" claim from README benefits bullet (2026-05-25)

The "What you get" section had a bullet reading *"The same mistake stops happening every six months. Memory entries make recurring fixes a one-time cost."* The "every six months" cadence was an oddly specific claim that implied measured frequency. Replaced with *"The same mistake doesn't come back."* — same point, no false precision.

---

## v1.4.2 — 2026-05-25

### Docs — Diagram refinements: pillars labeled as long-term goals + items sized by contributor type (2026-05-25)

Two diagram-label refinements based on maintainer feedback:

- **Pillars relabeled "long-term capability goals"** (was "capability layers · evergreen"). Both diagrams. Pillars are the closest thing the methodology has to long-term goals; making that explicit helps adopters see the link to their own product roadmap.
- **Items sized by contributor type, not by calendar.** Was "1–2 week units of work"; now "1–2 weeks for humans · daily for AI" (Diagram 1) and "sized to the contributor: 1–2 weeks for humans · daily for AI" (Diagram 2). Reflects what's true in mixed-contributor projects — the same backlog item that takes a human 1–2 weeks of focused work might take an AI agent hours-to-days. Item *scope* is the constant; calendar time is contributor-dependent.

Diagram-only change in this release. If the underlying methodology docs (especially `methodology/04_backlog_items.md` and the "Effort: XS–XL" sizing guidance) should be updated to reflect contributor-aware sizing more explicitly, that's a separate follow-up.

---

## v1.4.1 — 2026-05-25

### Docs — Two Mermaid diagrams added to README + v1.3.1 → v1.4.0 reference bumps (2026-05-25)

Two diagrams give visitors and adopters a visual entry point alongside the prose:

**New section "How it fits together"** (right after TL;DR) — conceptual diagram showing the four planning layers (Strategy → Pillars → Epics → Items) cascading downward, three discipline overlays (Working Principles / Definition of Done / Memory) binding every change, and three operational supports (Locks / Git Workflow / Fix-Test Loop) making the day-to-day navigable. Colors map to function (planning blue, disciplines amber, supports green).

**New section "How the work cascades"** (right after "What's in the repo") — data-cascade diagram with file paths, from Step 0 (your brief, BEFORE the methodology kicks in) → `docs/strategy/` → `docs/pillars/` → optional `docs/planning/` → `backlog/epics/NN-slug/` → individual BL-XXXX items inside each epic's `BACKLOG.md`. Includes the four-file shape of each epic folder (README/BACKLOG/ARCHIVE/FUTURE) and the item frontmatter schema (Pillar / Status / Test / Lock / Priority / Effort). Explicitly notes the "one ticket type" design — feature, bugfix, task, and user-story-shaped items all use the same BL-XXXX format, no Jira-style taxonomy.

Both diagrams use Mermaid markdown blocks (no separate image files) so they render natively on GitHub, edit as text, and live in git — consistent with the methodology's "markdown + git only, no SaaS" framing.

**Mechanical:** two stale "v1.3.1" references in the README (TL;DR + Status section) bumped to v1.4.0. Should have been bumped at v1.4.0 ship; folded in here.

---

## v1.4.0 — 2026-05-25

### Feat — Four methodology additions: stdlib growth loop, verification taxonomy, brownfield onboarding, decision-ownership matrix (2026-05-25)

Closes four real gaps surfaced by external research comparing this methodology to its peers (GitHub Spec Kit, BMAD Method, Geoffrey Huntley's Ralph loop and stdlib pattern, et al.). Each addition is a section within an existing methodology doc — no new doc number, no restructure.

**`08_lessons_and_memory.md` — new section "The promotion path: from one-off correction to durable rule"** (~70 lines)

Names the explicit promotion loop: one-off correction → memory entry → instruction file → methodology addition (and the reverse loop for demotion and deletion). The existing doc already had two of the four stages (Trigger 2: "Same correction 2+ times" → memory; "Memory as a leading indicator" → methodology). The new section adds the missing middle stage (memory → instruction file) and frames the whole pipeline as a named loop. Peers — particularly Geoffrey Huntley's [stdlib pattern](https://ghuntley.com/specs/) — make this loop the centerpiece of their methodology; this addition adopts the discipline without dropping the existing planning hierarchy.

**`10_testing_and_verification.md` — new section "Verification levels: matching depth to risk"** (~80 lines)

Graduates the binary `Test: pass` field into a five-level taxonomy (L0 type check → L1 automated tests → L2 actual-UI loop → L3 cross-AI validation → L4 user testing). Includes a mapping from change class (typo / refactor / new feature / schema migration / security-sensitive / production hotfix) to required levels, with an optional level annotation in the item's `Test:` field (e.g., `Test: pass (L3)`). The DoD's hard rule (`Status: done` requires `Test: pass`) is unchanged — the taxonomy clarifies *what `pass` means* for the specific change. Closes the "unusually strict for trivial work / unusually loose for risky work" gap surfaced in peer-methodology research.

**`00_README.md` — new section "Brownfield reality check (when adoption fights headwinds)"** (~70 lines)

Explicit staging (Stage A → E) for adopting the methodology in legacy projects where the team hasn't asked for new process: start with personal-discipline adoption, add the lock protocol when AI parallelism creates collisions, apply DoD to a single epic, open the planning layer for new work only, backfill pillars and strategy last. Includes "what NOT to do" anti-patterns (don't reformat the existing backlog all at once, don't ask non-contributors to read 12 docs, don't litigate the past) and a "when brownfield adoption fails" honest failure-mode section. The existing "Adopting in an existing project" 8-step list remains — the new section addresses harder cases where that gentle staging assumes too much buy-in.

**`11_human_roles.md` — new section "The decision-ownership matrix"** (~100 lines)

A RACI-lite matrix mapping 21 decision types (code style → naming → refactor → bug fix → new feature → library choice → schema → API shape → auth → architecture → production deploy → destructive operations → strategy → pricing → hiring → legal) to five ownership columns (AI proposes / AI decides / Human reviews / Human decides / Human-only). Includes guidance on how to adapt for project risk tolerance, hard-coded rightmost-column rows (production deploys, force-push, destructive operations) that match the methodology's existing hard rules, an "ownership is unclear" escalation protocol, and an explicit cross-reference to the memory promotion loop above. Peer methodologies (per external research) consistently flagged this as the #1 missing artifact for teams adopting AI-collaborated workflows.

**Mechanical updates:**

- `README.md` line-count claim refreshed (~7,100 → ~7,500). The four additions added ~320 lines of methodology content; longest doc remains `04_backlog_items.md` at 778 lines.
- No new doc files. The four additions all extend existing docs. Doc count stays at 12 (00–11).

Discovery: all four additions came from a research pass that surveyed ~14 peer methodologies including GitHub Spec Kit, BMAD Method, Ralph loop, stdlib pattern, AGENTS.md standard, GSD, nano-spec, plus academic papers (Agentsway, Agile V) and vendor docs (Anthropic, OpenAI). The gaps these additions close were ranked by recurrence across peers — these were the four that came up most often.

### Docs — README rewrite (benefit-led + competitive context) + new `templates/AGENT_KICKOFF.md` (2026-05-24)

README rewritten — cut from 348 to 220 lines (~37% compression). Motivated by external feedback that the README "felt AI-written" and was missing benefit-led framing plus context on how this methodology relates to the wider ecosystem of AI-collaboration methodologies that now exists.

**Added:**

- **"What you get"** — a benefits-led section (10 bullets) right after the TL;DR. Each bullet maps to a specific methodology element (DoD hard rule, locks, memory entries, working principles, fix-test loop, challenge-before-consenting, cross-AI validation, vendor-neutral templates). Adopters see the value-prop before the mechanics.
- **"What's similar, what's different"** — honest comparison to 7 peer methodologies discovered via external research: [GitHub Spec Kit](https://github.com/github/spec-kit) (~106k★), [BMAD Method](https://github.com/bmad-code-org/BMAD-METHOD), Geoffrey Huntley's [Ralph loop](https://ghuntley.com/ralph/) and [stdlib pattern](https://ghuntley.com/specs/), the [AGENTS.md standard](https://agents.md/), [Get Shit Done (GSD)](https://www.prafulls.me/blogs/gsd-spec-driven-development), and [nano-spec](https://github.com/tao-hpu/nano-spec). Includes explicit "this methodology has 0 stars at the time of writing and is solo-maintained" disclosure so the comparison isn't oversold.
- New **`templates/AGENT_KICKOFF.md`** — the 40-line Step 2 planning-mode prompt that was bloating the README, extracted to its own file with a pointer from the README.

**Compressed:**

- "Why this exists" table: 16 rows → 10 highest-value rows; 3-column format (Problem / Why / Solution) → 2-column (Problem → Solution).
- "Why it works (the short version)" subsection removed — meta-commentary that just rephrased the table.
- "A small tip that pays off" subsection removed — the same advice already lives in Step 3's four-phrases bullet list.
- Step 0 prose: ~25 lines → 1 paragraph (substance kept, repetition dropped).
- Step 2 prompt: 40+ lines → 1 sentence + link to `templates/AGENT_KICKOFF.md`.
- "Permissions and vendor compatibility": ~13 lines → 5 lines, same content denser.
- Two parallel comparison sections ("What makes this different" + "How this relates to specific methodologies") merged into the new "What's similar, what's different" section. The Agile/Scrum/Kanban/Shape Up/XP comparison was replaced with the contemporary AI-methodology landscape (Spec Kit, BMAD, Ralph, etc.) — peers that didn't exist when v1.0 was framed.

Repo total now: 7,152 lines across 21 files (the README displays a tree of 20, excluding the `.github/FUNDING.yml` metadata file from the prior commit).

Research surfaced ~14 peer methodologies (Spec Kit alone has ~106k stars), confirming the README needed to position this work in the current landscape rather than only against pre-AI methodologies. Several peer methodologies provided concrete language for distinguishing strengths — most notably the "cheating agent" anti-pattern, file-based locks for humans+agents using the same protocol, and the challenge-before-consenting copy-paste prompt, none of which appear in peer methodologies surveyed.

---

## v1.3.1 — 2026-05-24

### Docs — Add "Permissions and vendor compatibility" section to README (2026-05-24)

New README section addresses three reader questions: (1) what the CC BY 4.0 license actually permits in practice (private, commercial, open-source use; fork, modify, redistribute, charge for derivatives; ship inside a paid product; use with paid, free, self-hosted, or on-prem AI tools — only obligation is attribution); (2) whether the methodology is compatible with AI tool vendor acceptable-use policies (Anthropic, OpenAI, Google, Cursor, Continue, Aider, etc.) — yes, because the methodology calls no vendor API and asks AI agents to do nothing restricted under any major AUP, and the project-instruction file (`CLAUDE.md`, `AGENTS.md`, `.cursorrules`, `.continue/context.md`) is the vendor-supported mechanism for project context; (3) how the methodology's safety practices (no production deploys by agents, no force-push to trunk, no hook bypass, no destructive commands autonomously, branch protection + PR-only by default, cross-AI validation + user testing as final gates) align with vendor AUPs rather than conflicting with them.

Includes a clear "not endorsed by, partnered with, or affiliated with any AI tool vendor" disclaimer and a "not legal advice" disclaimer for adopters operating under specific compliance requirements (regulated industry, data residency, classified work, government procurement).

Added because adopters considering the methodology were uncertain whether using it with their preferred AI tool would put them at odds with vendor policies. The answer is no, and the answer should live in the README rather than be left for adopters to infer.

### Chore — Honesty pass on v1.3.0 (2026-05-24)

Three small fixes for facts that drifted or never matched reality. The methodology applies to itself; a repo whose README mis-states its own size and whose CHANGELOG links to a deleted file fails its own DoD Gate 4.

- `README.md:84` — line-count claim updated from ~6,100 to ~7,100 (actual: 7,115 lines across 19 files; v1.3.0's "refreshed" claim was 16.5% low). "Longest single doc" updated from ~700 to ~780 (actual longest: `methodology/04_backlog_items.md` at 778 lines).
- `README.md:263–267` — "The two templates have identical content" softened to "substantially identical." AGENTS.md is the superset by 22 lines (~11%), with vendor-neutral sections on plan-mode discipline, tool-install guidance, verification order, and an operational-safety rule that Claude Code's harness covers implicitly. Symlink advice updated to recommend pointing CLAUDE.md → AGENTS.md so the superset stays the source of truth.
- `CHANGELOG.md:151` — broken link `[EVALUATION.md](EVALUATION.md)` in the v1.0.0 historical entry rewritten to plain text + parenthetical pointing to the v1.3.0 removal entry. Historical narrative preserved; broken link removed.
- `README.md:19, 334` — two stale "Currently at v1.2.0" references bumped to v1.3.1 (this release). These should have been bumped at v1.3.0 ship; they weren't, completing the picture of v1.3.0 documentation drift that this honesty pass closes.

Discovered via an external fresh-eyes audit on 2026-05-24 (the same day v1.3.0 shipped). Each fix would have been caught at the time by stricter Gate 4 / Gate 5 application; this release closes that gap and the audit findings are now folded back into the project's working practice.

---

## v1.3.0 — 2026-05-24

### Docs — README: new Step 0 (the brief is a prerequisite) + Step 3 made realistic (2026-05-24)

Two substantive README changes that close a methodology-honesty gap.

**New Step 0 — "Before this methodology kicks in (the brief)":** explicit acknowledgment that the methodology does NOT solve the upstream work — product / market / user / business / tech stack decisions. Lists the 7 questions a project needs written, defensible answers to before Step 1 can produce anything useful (what / who / success / competitors / viability / stack / capability layers → pillars). Names a common failure mode (treating `docs/strategy/` and `docs/pillars/` as a substitute for upstream thinking rather than the *recording layer* for already-validated decisions) and the resulting velocity illusion (shipping confidently-built wrong product). Mentions Lean Canvas, JTBD interviews, Five Forces, etc. as candidate frameworks without prescribing.

**Revised Step 3 — "Ongoing development":** removed the unrealistic "paste this 30-line prompt at the start of every session" framing. The project-instruction file (`CLAUDE.md` / `AGENTS.md`) is what AI tools read automatically; nothing to paste. Replaced with four short steering phrases for when the AI drifts ("Do you have any questions?", "What's wrong with this plan?", "Use plan mode", "Stop — split this item"). AUTONOMOUS_LOOP remains the explicit-paste path for dedicated milestone work; everything else runs from the instruction file.

Adjacent cleanup: the "small tip that pays off" intro no longer references a "prompt above."

### Docs — README "How this relates to specific methodologies" comparison (2026-05-24)

The "What makes this different" section now includes a comparison table mapping the major prior methodologies (Agile Manifesto, Scrum, Kanban, Shape Up, Extreme Programming) to what this methodology adopts vs. what it does differently. Plus a coexistence paragraph: runs inside Scrum (sprints as scheduling overlay), layers on top of Kanban (adds upstream planning), complements XP directly, not designed to replace SAFe or other enterprise frameworks.

Addresses the common first-read question: "where does this fit relative to what I already know?"

### Chore — Remove `EVALUATION.md` from public repo (2026-05-24)

The gap-analysis report that triggered v1.1.0 and v1.2.0 is no longer worth carrying as a top-level repo artifact. The gaps it identified are mostly closed (see those releases); a stale "here's what's missing" doc at the root would mislead new readers about the current state of the methodology.

Internal copy preserved as a dated snapshot in the source project's docs folder. Ongoing maintenance flows through this `CHANGELOG.md` instead — release-by-release, in the format the methodology itself prescribes (see [methodology/07_definition_of_done.md](methodology/07_definition_of_done.md) "Changelog — the practical patterns").

`README.md` updated: four references to `EVALUATION.md` rewritten (now pointing at `CHANGELOG.md` where appropriate); file tree no longer lists `EVALUATION.md`; line count refreshed (~6,100 lines across 19 files).

---

## v1.2.0 — 2026-05-24

### Feat — Backlog mechanics: practical artifacts from real-practice comparison (2026-05-24)

Closes nine gaps identified by comparing the methodology's backlog spec against an actual production project's backlog. The methodology had the conceptual model right; these additions provide the operational templates and recovery guidance that real practice has invented.

**`methodology/03_epics.md` additions:**

- **Rollup table now has a "Next milestone" column** — human-readable "what's the next visible shipment" gives at-a-glance status without opening the epic. Open/Done collapsed to one combined column to keep the table readable.
- **Pillar Coverage section** — inverse table showing which epics touch each pillar. Useful for "what's active on pillar X right now?" queries and pillar audits.
- **Last-refresh metadata** — pattern for the freshness note at the top of `EPICS.md` so readers see what shipped since the last sweep and any known count drift.
- **`TEST.md` template** — proper template with two sections: "Acceptance tests for exit criteria" + "Regression scenarios to protect (with last-verified date)." Plus when-to-use and when-to-skip guidance.

**`methodology/04_backlog_items.md` additions:**

- **`BACKLOG.md` structure section** — defines the summary-table-at-top pattern (one line per item: `ID | Title | Priority | Effort | Status`) before the detailed item blocks. Massively improves scannability for epics with 20+ items.
- **Coupled fields: `Lock` + `Status` + `Test`** — table of valid combinations for typical outcomes (item picked up, code merged, blocked, etc.). The three fields are coupled; the table shows what valid joint states look like for each outcome.
- **"When things go sideways" recovery patterns** — unified guidance for: tests fail (keep lock, fix in same PR), external blocker (release lock, set blocked, leave `**Blocker:**` note), scope creep (stop, split, file follow-ups), expired-own-lock recovery, reopening a `done` item.
- **Greppable metadata: specific `rg` query patterns** — example commands for "all P0 items," "all unlocked items," "all in-progress items," "all blocked items with context," "find next BL-ID," etc. Plus the ID collision rule.
- **`FUTURE.md` numbering: two valid schemes** — names the choice between monotonic project-wide IDs vs. epic-scoped F-prefixed IDs. Both are valid; project picks one and documents it.
- **TL;DR for a fresh contributor** — one-paragraph quick-start so a contributor (human or AI) can pick up an item cold without reading the rest of the doc.

Synthesized from focused gap analysis between the methodology's backlog docs (03_epics, 04_backlog_items) and a real production project's `backlog/README.md` + `EPICS.md` + sample epic folder.

### Chore — Document workflow exception in `STATUS.md` (2026-05-24)

The methodology's own [09_git_workflow.md](methodology/09_git_workflow.md) requires PR-only merges to the trunk and forbids direct commits, but this repo is solo-maintained and has been using direct-to-main commits since v1.0.0. `STATUS.md` now names the exception explicitly: why it's deliberate, why the rule's reason-for-existing doesn't apply in a solo-maintained context, and the trigger for revisiting (second contributor joins → adopt branch protection + PR flow). Frames the exception via the methodology's own authority hierarchy.

Also fixed a stale `MIT license` reference in `STATUS.md` (license is CC BY 4.0; the wrong name slipped through when the license was switched from MIT during v1.0 prep).

---

## v1.1.0 — 2026-05-24

### Feat — New doc `methodology/11_human_roles.md` (2026-05-24)

Adds the methodology's missing "human side": how human contributors stay meaningfully engaged when AI agents do most of the implementation work. The bottleneck has shifted from execution to specification and supervision; this doc says what humans *do* now that AI does most of the typing.

Sections include: the shifted bottleneck (code-as-commodity vs. spec-as-asset), the new supervisory layer (agent-sized chunks, when to let the AI run vs. intervene, prompt-refinement over manual fixes, pre-implementation architectural review), four anti-patterns (the cheating agent, the yes-man / agreement bias, the stranger in your own code, the loss of tribal knowledge), specification as the primary artifact (state machines, decision tables, schema-first definitions, Given/When/Then), and the new human skills (architectural thinking, unambiguous specification, supervisory skill, taste, system thinking across abstraction layers).

Synthesized from external analysis of AI integration in a software team plus the methodology's existing patterns.

### Feat — `methodology/06_working_principles.md` adds "Challenge before consenting" (2026-05-24)

Per-decision defense against the AI agreement bias. AI models default to helpful agreement; when the stakes are high, invert the default and prompt the AI to challenge rather than confirm. Includes copy-paste prompt ("what's wrong with this plan? what's the strongest case AGAINST? what would a senior engineer poke holes in?").

When to use: before approving plans, mid-incident, when evaluating architectures, after a confident-sounding answer, when you notice you're agreeing with the AI a lot.

### Feat — `methodology/10_testing_and_verification.md` adds "The cheating agent" anti-pattern (2026-05-24)

Warns about the failure mode where AI writes both the implementation and the tests that validate its (broken) implementation — the green test suite looks like done; no human in the loop catches it. Defenses: test-first / TDD as an AI-collaboration discipline, cross-AI validation of test suites, human review of test names and acceptance criteria, periodic random audits of AI-written test/implementation pairs.

Includes the deeper implication: the test suite is the durable artifact (survives language/framework migration when it captures intent correctly); implementation is replaceable. Test quality matters MORE in an AI-assisted workflow, not less.

### Chore — Cross-doc updates

- `methodology/00_README.md`: doc 11 added to doc index; mental model now includes "the applied dimension"; "Starting a new project from scratch" reading order extended to include doc 11.
- `README.md` (repo): file tree updated (12 docs instead of 11); total line count updated; "Why this exists" table grew by three rows (humans drift from loop, AI-agreement bias, cheating agent) pointing at the relevant docs.
- `templates/AUTONOMOUS_LOOP.md`: "Pairing with plan mode" section now references the challenge-before-consenting pattern.

---

## v1.0.1 — 2026-05-24

### Feat — `templates/AUTONOMOUS_LOOP.md` (2026-05-24)

Adds a paste-and-adapt prompt template for long autonomous AI dev sessions. Tells the AI to apply the methodology as a continuous *analyze → prioritize → execute → validate → repeat* loop with a milestone-level stop condition (not per-task completion). Includes the integrity rule: never claim something is tested / secure / complete / production-ready unless actually verified.

Compressed from a real production-tested ~85-line autonomous-engineer prompt down to ~50 lines, with most rules referenced via methodology docs rather than restated inline.

Use cases: focused milestone work where the goal is agreed and the AI should grind toward it autonomously between check-ins. Not for exploratory work where each step needs review.

README updated to mention the new template (file tree + new "For long autonomous sessions" subsection).

---

## v1.0.0 — Initial public release (2026-05-24)

First public version. Extracted from a real production project's working practice and republished as a portable abstract methodology.

### Feat — Eleven-doc methodology set

The complete set lives under `methodology/`:

- [00_README.md](methodology/00_README.md) — index, mental model, doc index, adoption guides.
- [01_strategy.md](methodology/01_strategy.md) — master plan + supporting research + phase roadmap + re-evaluation protocol.
- [02_pillars.md](methodology/02_pillars.md) — sequential capability layers + refinement pattern.
- [03_epics.md](methodology/03_epics.md) — charters, JTBD outcomes, exit criteria, WIP limit, pre-epic planning.
- [04_backlog_items.md](methodology/04_backlog_items.md) — BL-### format, fields, status enums, lifecycle, resolution notes.
- [05_locks_and_parallel_work.md](methodology/05_locks_and_parallel_work.md) — file-based TTL locks + subagent delegation pattern.
- [06_working_principles.md](methodology/06_working_principles.md) — the four principles + plan-before-execute + tools-the-agent-uses.
- [07_definition_of_done.md](methodology/07_definition_of_done.md) — six gates, the hard rule, docs-maintenance patterns, quarterly repo health audits.
- [08_lessons_and_memory.md](methodology/08_lessons_and_memory.md) — two-layer memory + memory-as-leading-indicator feedback loop.
- [09_git_workflow.md](methodology/09_git_workflow.md) — branch protection, conventional commits, worktrees, destructive-command discipline, operational work patterns.
- [10_testing_and_verification.md](methodology/10_testing_and_verification.md) — automated tests, actual-UI fix-test loop, cross-AI validation, user testing as the final gate.

### Feat — Instruction-file templates for AI tools

`templates/` contains paste-and-adapt starter files for the project-instruction file:

- [templates/CLAUDE.md](templates/CLAUDE.md) — for Claude Code.
- [templates/AGENTS.md](templates/AGENTS.md) — vendor-neutral (OpenAI Codex, Google Antigravity, etc.).

The README's "AI tool support" section maps each AI tool to its expected filename.

### Feat — Field-tested in production

`EVALUATION.md` was the honest field report shipped in v1.0.0: what the methodology covered, what was missing when compared to real practice, what got added in this release, and what remained deliberately out of scope. Coverage mapping plus practical pros and cons. (Removed in v1.3.0 — see that entry above for rationale.)

### Chore — Repo scaffolding

- [LICENSE](LICENSE) — CC BY 4.0 (attribution-required).
- [README.md](README.md) — TL;DR, problems-it-solves table, kickoff guide with AI prompts, AI tool support, attribution guidance.
- [STATUS.md](STATUS.md) — maintenance posture (lean — PRs welcome but no SLA; CC BY 4.0 means anyone can fork).

### Out of scope on this release

- Project-specific deploy commands, monitoring stacks, CI providers — by design (project choice).
- An `examples/` folder with anonymized real artifacts — future work, noted in EVALUATION.md.
- A one-page CHEATSHEET — README's TL;DR currently serves this; revisit if requested.
