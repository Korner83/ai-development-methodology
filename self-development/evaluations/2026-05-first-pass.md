# 2026 first semi-annual self-evaluation pass

_Skeleton seeded by BL-0006. Content populated by BL-0007 through BL-0010._

## Metadata

- **Date of pass:** 2026-05-25
- **Methodology version at eval:** v1.12.0
- **Reviewer model + session:**
  - Docs 00–05 batch (BL-0007): Opus 4.7 via fresh general-purpose agent (no prior turns referencing this project).
  - Docs 06–11 batch (BL-0008): Opus 4.7 via fresh general-purpose agent (no prior turns referencing this project, including no exposure to BL-0007's authoring session).
- **Scope:** abstract methodology docs `methodology/00_README.md` through `methodology/11_human_roles.md`. **Out of scope for this pass:** `self-development/`, `templates/`, `brief/`, README.md, CHANGELOG.md.
- **Cadence reference:** [`methodology/07_definition_of_done.md "Methodology self-evaluation (semi-annual)"`](../../methodology/07_definition_of_done.md#methodology-self-evaluation-semi-annual)

## Cold-read findings (docs 00–05)

_Populated by BL-0007. Each doc gets at least one finding entry (even "no issues found" counts as proof of read). Findings cite file:line where applicable. Categories: stale / unclear / inconsistent._

### methodology/00_README.md

**Stale:**
- Reading-path table omits doc 11 from the "New contributor" and "Picking up a specific item" rows — `methodology/00_README.md:122-123` — both rows stop at doc 10. But doc 11 (human roles) is now described at line 56 as "Read it alongside the disciplines for the full picture." A new contributor following the recommended reading order would never encounter it. Either add 11 to the relevant rows or change line 56 to acknowledge 11 as optional/later.
- "Operational supports" cluster in the mental model (`methodology/00_README.md:93-103`) lists three items — Locks, Git workflow, Testing — but the prose only enumerates docs 05, 09, 10. The "How to read these docs" table (line 122) treats 11 as a peer of 06-08, while the mental-model diagram never accounts for 11. The diagram is stale relative to the doc set; it predates 11_human_roles.md being added as a co-equal slot.

**Unclear:**
- The `EPICS.md` link in the "working day" loop (`methodology/00_README.md:203`) uses the literal placeholder `(#)` instead of a real relative path — a fresh contributor would not know whether it lives at `backlog/EPICS.md`, `EPICS.md`, or somewhere else. The actual location is established in `03_epics.md:74-86`; the README should link there or to the conventional path.
- "The autonomous-loop prompt template" link at `methodology/00_README.md:236` resolves to `../templates/AUTONOMOUS_LOOP.md`. Since `methodology/` and `templates/` are sibling folders at the repo root, `../templates/AUTONOMOUS_LOOP.md` resolves correctly only if the reader is viewing the rendered doc from `methodology/`. The link works, but it's unclear to a cold reader whether `AUTONOMOUS_LOOP.md` is a methodology artifact or a project artifact; doc 00 never explains the templates/ folder.

**Inconsistent:**
- The hard-rules table (`methodology/00_README.md:184-194`) lists 9 rules but omits "AI agents never override locks" from doc 05 (`05_locks_and_parallel_work.md:494`). Doc 05 phrases this as a binding rule for agents; doc 00's summary doesn't surface it. Either the rule should be added to the table or doc 05 should soften its phrasing.
- The Authority section (`methodology/00_README.md:362-369`) lists six precedence layers but does not mention the autonomous-loop's Constraint 1 (loop forbidden from editing `methodology/*` autonomously, per v1.12.0 changelog). This constraint is a hard rule for the self-development project but is not surfaced in 00 — a reasonable omission if treated as project-specific, but worth noting since the README's hard-rules table claims to enumerate "the smallest set of inviolable constraints."

### methodology/01_strategy.md

**Stale:**
- _(none)_

**Unclear:**
- The "Document Index template" (`methodology/01_strategy.md:316-331`) shows numbered docs starting at 01 (`01_market.md`), but earlier in the same doc the supporting-doc table (`methodology/01_strategy.md:80-95`) shows the same numbering starting at 00 for the master plan. A reader trying to file `00_master_plan.md` and then add `01_market.md` from the template would notice the master plan never appears in the index template — is the convention "master plan is implicit, index lists only supporting docs" or "master plan is row 00"? The two patterns appear to differ; pick one.
- Re-evaluation cadence guidance is split: doc 01 (`methodology/01_strategy.md:251-268`) describes per-doc cadence as a checklist, but the actual frequency words ("quarterly," "monthly," "on metric breach") are templates the project fills in. A new project gets no recommended default. The DoD section "Methodology self-evaluation (semi-annual)" recommends 6 months for methodology; strategy docs are silent on what a reasonable default would be.

**Inconsistent:**
- Doc 01 says strategy docs are "snapshots, not living documents" (`methodology/01_strategy.md:274`) and pillars are "living" (`methodology/02_pillars.md:155`). But doc 02's versioning section also says material design changes "use the refinement pattern" rather than overwriting — which is effectively versioning. The contrast is sharper in prose than in practice; both layers archive prior versions for material changes. The "living vs snapshot" terminology may mislead a cold reader into thinking pillars get edited destructively.

### methodology/02_pillars.md

**Stale:**
- _(none)_

**Unclear:**
- The pillar inventory table (`methodology/02_pillars.md:65-75`) is labeled "illustrative" but uses the exact P1-P9 numbering and naming that the self-development project's own pillars derive from. A cold reader could plausibly mistake this for the canonical mapping. The text immediately below (line 77) clarifies this is a generic example, but the proximity of the table to the dependency graph (line 85-98) — which uses the same labels — invites confusion about whether these are placeholder names or required pillar names.
- "Refinement docs" path is given as `docs/architecture/architecture_refinement_vN.md` (`methodology/02_pillars.md:180`) "or a similar path the project agrees on." But pillar docs themselves live at `docs/pillars/`; the relationship between `docs/architecture/` and `docs/pillars/` is not introduced anywhere. A new project setting up its folder structure has no guidance on whether `docs/architecture/` is a sibling, optional, or required.

**Inconsistent:**
- Doc 02 says pillars are bound by strategy and that strategy outranks pillars when they conflict (`methodology/02_pillars.md:368-369`). Doc 00's authority section (`methodology/00_README.md:362-369`) restates this. But doc 01 also says the same thing (`methodology/01_strategy.md:469-475`). The rule appears in three places with three different phrasings — minor risk of drift if any one updates without the others.

### methodology/03_epics.md

**Stale:**
- _(none)_

**Unclear:**
- The transition diagram (`methodology/03_epics.md:287-294`) shows `planned → parked` and `parked → done` paths with a comment "(close out, exit criteria met somehow)" — the parenthetical "somehow" is vague. Under what circumstances does a parked epic legitimately close out as done without resuming to active first? The state-machine diagram at line 382-393 shows the same transition but no longer carries the "somehow" caveat. Either explain the case or remove the transition.
- "WIP cap of 3" is recommended (`methodology/03_epics.md:50`), then "Smaller teams should run fewer; larger teams *with truly independent workstreams* can run more" (line 58). The v1.12.0 changelog records the self-development project dropped to WIP=1 based on this guidance. A new solo maintainer reading doc 03 cold would still see "3" as the headline number — the "smaller teams should run fewer" caveat is buried in the next paragraph. Surfacing a "default 3, solo: 1" recommendation up front would help.

**Inconsistent:**
- The Epic charter template (`methodology/03_epics.md:151-195`) shows `Started: YYYY-MM-DD` as a frontmatter field, but the prose explanation (line 217) says "Use `—` while in `planned`." The template doesn't show the `—` form; a contributor copy-pasting the template into a `planned` epic would fill in a date that contradicts the rule. Add `Started: — (or YYYY-MM-DD when active)` to the template.
- Doc 03 (`methodology/03_epics.md:300`) says closing an epic "requires every exit-criteria checkbox to be true." Doc 07 (`methodology/07_definition_of_done.md`) doesn't explicitly mandate epic-level closure rules — epic closure is item-aggregation, not item-DoD. The two docs aren't contradictory, but the close-out checklist in `03_epics.md:407-417` is functionally a "DoD for epics" that doc 07 doesn't acknowledge. Cross-link or move epic-close-out under doc 07's umbrella for symmetry.

### methodology/04_backlog_items.md

**Stale:**
- The grep examples (`methodology/04_backlog_items.md:813-839`) all use a pattern like `^\| \*\*Pillar\*\* +\|` — that is, a frontmatter table where field names are wrapped in `**bold**`. But the frontmatter template earlier in the doc (lines 95-106 and the skeleton at lines 707-717) shows plain field names without bold (`| Pillar | P<#> |`, not `| **Pillar** | P<#> |`). The grep examples will return zero matches against items filed per the canonical template. Either the template gains `**bold**` or the grep examples drop the `\*\*` wrappers. (The v1.12.0 changelog C1 fix explicitly rewrote 14 items to "table form" without mention of bold field names — strong signal that the plain-table version is the canonical one and the grep examples are stale.)

**Unclear:**
- Two FUTURE.md numbering schemes (`methodology/04_backlog_items.md:48-66`) are described as "either is fine," but the doc doesn't say where the choice is recorded. A new contributor joining a project mid-flight has to either grep `FUTURE.md` and guess from the IDs they see, or hope someone wrote the choice down somewhere. The doc should recommend recording the choice in the project's instruction file or the backlog README.
- The "ID collision under concurrency" section (`methodology/04_backlog_items.md:844-846`) describes the resolution pattern but doesn't say how to *avoid* the collision in the first place. A team filing many items in parallel would want guidance on, e.g., reserving an ID range per session. The current text is post-hoc recovery, not prevention.

**Inconsistent:**
- The status enum lists 8 values (`methodology/04_backlog_items.md:226`), but the lifecycle diagram (lines 466-479) only shows transitions for 7 — `to_be_tested` is used but `to-be-tested` (with hyphens) is the enum value. The diagram uses underscores because mermaid requires them in state names, but a cold reader sees inconsistent naming. A footnote on the diagram explaining the hyphen→underscore mapping would help.
- The "Coupled fields" table (`methodology/04_backlog_items.md:346-357`) shows "Item just picked up; work starting" as `Lock: <id>@<now+TTL>`, `Status: in-progress`, `Test: not-tested` — but doc 05's acquire protocol (`methodology/05_locks_and_parallel_work.md:90-107`) describes step 4 as "set `Lock: <your-id>@<now + TTL>`. Optionally also flip the `Status` field to `in-progress` in the same edit." Doc 04 treats the status flip as automatic; doc 05 treats it as optional. They should agree (recommend: always flip together, which is what the lifecycle implies anyway).

### methodology/05_locks_and_parallel_work.md

**Stale:**
- _(none)_

**Unclear:**
- TTL recommendations (`methodology/05_locks_and_parallel_work.md:271-277`) list five tiers — but the "default to 2 hours" guidance (line 281) is in prose below the table. A cold reader scanning the table would see five options and have to read prose to know which to pick when in doubt. Move the default callout into the table caption or bold it in the prose.
- The "Expired locks" investigation flow (`methodology/05_locks_and_parallel_work.md:211-236`) describes git commands and partial-work recovery but doesn't say what to do when the holder ID identifies a still-active agent (e.g., an agent that's still alive but lost track of its lock). Should you contact the agent's owner? Re-acquire silently? The current text assumes the prior holder is gone — but expired locks can also indicate a slow holder who hasn't refreshed. Add a "what if the holder is still alive?" branch.

**Inconsistent:**
- Doc 05 says "Subagent does not touch the lock; the orchestrator remains the lock-holder throughout" (`methodology/05_locks_and_parallel_work.md:292-294`). This is consistent with doc 04's Lock field rule that "only the lock-holder may change `Status`, `Test`, and the body" (`methodology/04_backlog_items.md:115`). But doc 04 names "the lock-holder" as the editor; doc 05 names "the orchestrator" — the two terms refer to the same role for subagent flows but a cold reader could plausibly think a subagent is a distinct lock-holder. Add a sentence in doc 04 acknowledging subagent flows defer to the orchestrator's lock.
- TTL ceiling is stated as "Maximum 24 hours, refreshed" for "Coordinated multi-day work (rare)" (`methodology/05_locks_and_parallel_work.md:277`). The Common Mistakes table on the same doc (line 466) flags "TTL set to 24 hours by default" as wrong. The two messages are reconcilable (24h is the *ceiling for rare cases*, not the *default*), but a fresh contributor might read them as contradictory. A clarifying note would help.

## Cold-read findings (docs 06–11)

_Populated by BL-0008. Same shape as docs-00–05 section above. Cross-doc inconsistencies between this batch and BL-0007's batch are explicitly flagged as a sub-list at the end of this section._

### methodology/06_working_principles.md

**Stale:**
- _(none)_

**Unclear:**
- The section "Plan before executing non-trivial work" (`methodology/06_working_principles.md:132-168`) is presented as a separate rule alongside the four principles, but the doc's title is "Working Principles" and the section "How the four principles interact" (line 237-246) and the canonical short-form checklist (lines 298-323) both treat the count as exactly four. A cold reader hits the plan rule and wonders whether it's "Principle 5" by another name, an "auxiliary rule," or genuinely outside the principles. The doc never resolves the count. Add a sentence in "Plan before executing" saying "this is not a fifth principle; it's the gating rule for *when* the four principles start applying."
- "Challenge before consenting" (`methodology/06_working_principles.md:202-233`) introduces an "invert the default" pattern with a literal prompt block (lines 210-215). The doc does not say how often to actually invoke this — every plan? Only "high-stakes" ones? The "When to use it" list (lines 219-225) names five triggers but the first is "Before approving any plan for non-trivial work," which would make this a *required* part of every plan-mode invocation, not a contextual escalation. A cold contributor reading both the "plan before executing" section and "challenge before consenting" cannot tell whether the contrarian-case prompt is mandatory-with-every-plan or reserved-for-stakes. Pick one.

**Inconsistent:**
- The "Anti-patterns the principles forbid" table (`methodology/06_working_principles.md:277-290`) maps each anti-pattern to a single principle (P1/P2/P3/P4). But "Bundling a small refactor into a bug fix" (line 288) is mapped to P3 only — yet the canonical short form (line 311) for P3 says "Match existing style. Do not refactor unrelated code." The bundling violates BOTH P2 (extra scope = extra code that wasn't asked for) and P3 (surgical scope). The table forces a single mapping where the actual principles are mutually reinforcing — which the doc itself acknowledges at line 246 ("Speculative abstractions (P2) bundle into adjacent files (P3)"). Either drop the single-mapping convention or let rows have multiple values.
- "Authority" section (`methodology/06_working_principles.md:327-331`) says "The principles do not outrank explicit user direction. They do outrank assumed user direction." This is consistent with the global Authority chain in 00 (line 360-369), but doc 06 never names the doc-07 (DoD) relationship in the same paragraph. The "How these interact with Definition of Done" section earlier (line 250-257) describes the principles and DoD as orthogonal gates, but the Authority section treats only user-direction-vs-principles. A cold reader who finishes 06 doesn't know whether DoD outranks principles, principles outrank DoD, or they're peers. Doc 07's own Authority section (line 484-486) treats DoD as outranking "we'll fix it later" — but neither doc names "what happens when principle 2 (simplicity) says inline a helper but DoD gate 4 (docs updated) would force a new doc page describing the now-deleted helper" type contradictions.

### methodology/07_definition_of_done.md

**Stale:**
- _(none)_

**Unclear:**
- The "Periodic doc audits" guidance (`methodology/07_definition_of_done.md:323`) says "Quarterly, do a pass: read every living document and ask 'is this still true?'" — but the same doc's "Methodology self-evaluation (semi-annual)" section (line 339-371) prescribes a similar pass at *half* the cadence specifically for the methodology docs. A cold reader picking up the doc-audit work has to figure out whether the methodology docs are *included in the quarterly pass* (and the semi-annual is a deeper version), *excluded from the quarterly pass* (because the semi-annual covers them), or *both* (which would mean the methodology gets touched twice in some quarters). The two sections need a sentence saying which one wins for the methodology specifically.
- The "Maintaining living project documents" table (`methodology/07_definition_of_done.md:215-225`) lists "Memory index" with update trigger "When a memory entry is added or removed." But doc 08 (`methodology/08_lessons_and_memory.md:220-224`) prescribes the trigger as "Every new memory entry adds an index line in the same commit. Every removed entry removes its line. Every renamed entry updates its line." The 08 wording is action-prescriptive (same commit); the 07 trigger is event-naming. A cold reader looking at 07's "Update trigger" cell could mistakenly think a follow-up commit is acceptable. Make 07 mirror 08's "same commit" phrasing.

**Inconsistent:**
- The "six gates" count appears in 00 (line 145, 194), 07 (`methodology/07_definition_of_done.md:27`, line 184), but the six gates are: 1) Code review loop, 2) Automated tests pass, 3) Actual UI verification, 4) Documentation updated, 5) Final verification loop, 6) Backlog state correct. Gate 5 is *itself* a re-run of gates 1+2+3 (see lines 100-108: "re-read the entire diff... re-run the test suite... re-run the UI smoke test"). A cold contributor may reasonably count this as 5 gates + 1 meta-loop, not 6 peers. The doc presents them as peers; the lived structure is 5-and-a-loop. Add a sentence acknowledging gate 5 is the loop, not a parallel discipline.
- Gate 6 (`methodology/07_definition_of_done.md:111-122`) requires "The item moved from the epic's `BACKLOG.md` to `ARCHIVE.md`" and "epic's rollup count incremented." But doc 04 (`methodology/04_backlog_items.md` ARCHIVE rules) is the canonical source for archive mechanics and doc 03 owns the EPICS rollup format. A cold contributor would need 07+03+04 to actually execute Gate 6 — and 07 only links to 04, not 03. Add the 03 link in Gate 6.
- The "DoD checklist (copy into your project's instruction file)" (`methodology/07_definition_of_done.md:392-418`) uses ASCII dashes — `Lock: -` (line 410) — while every other place in the methodology (e.g., `methodology/00_README.md:204` "Lock: —") uses the em-dash. Copy-paste from the checklist into a backlog item produces a `Lock: -` that won't match the regex/grep patterns the doc-04 grep examples already struggle with (per BL-0007's findings on doc 04). Pick em-dash or hyphen-minus and propagate.

### methodology/08_lessons_and_memory.md

**Stale:**
- _(none)_

**Unclear:**
- "Memory entry template" (`methodology/08_lessons_and_memory.md:144-165`) shows frontmatter with `name:`, `description:`, `metadata.type:` fields. But the worked examples at lines 326-405 (`feedback-trust-internal-types`, `project-content-deletion-flow`) and the index pattern at lines 198-206 (`[Title](file.md) — one-line hook`) don't make clear whether the index `Title` should mirror the frontmatter `name` (kebab slug like `feedback-trust-internal-types`) or the `description` (full sentence like "Don't add defensive type-checks..."). The example at line 200 uses `[Title](file.md)` as a placeholder, with no example of a real index row. The MEMORY.md in the CLAUDE.md context for the parent project uses prose titles ("[beta_strategy.md](beta_strategy.md) — Closed beta in two waves"), not slugs — but a cold contributor working from doc 08 alone would have to guess.
- The promotion path (`methodology/08_lessons_and_memory.md:453-509`) defines four stages but Stage 2→3 (memory → instruction file) requires "It's been referenced explicitly in 3+ contributor sessions" (line 474). For an AI-driven workflow, "contributor session" is ambiguous: does an AI agent's session count? Multiple agents loading the same memory in parallel sessions in the same hour — is that 1 or 3? Doc 11 frames sessions as the unit of AI work, but doc 08's promotion bar uses "session" without anchoring it. Define the unit.

**Inconsistent:**
- "What goes in memory" Type 1 (`methodology/08_lessons_and_memory.md:101-110`) and "Trigger 2" (lines 236-240) both name "2 or more times in different contexts" as the bar for writing a feedback entry. But the promotion path Stage 1→2 prose (lines 466-468) says "the same category of mistake has occurred twice." All three say "2+", "2 or more", and "twice" — verbally consistent — but doc 04 (per BL-0007 findings) and doc 05 have their own "twice" triggers that aren't cross-linked. Doc 08's "Trigger 2" should explicitly note: "this is the same '2+ occurrences' bar used for the recurring-fix discipline elsewhere in the methodology."
- The two-layer claim (`methodology/08_lessons_and_memory.md:27-53`) defines Layer 1 as "the project-instruction file" and Layer 2 as "the memory directory." But the promotion path (lines 453-462) lists *four* layers: one-off → memory → instruction file → methodology. The reader gets a 2-layer model in the body and a 4-layer model in the promotion section. The 4-layer view is the more accurate one (one-off lives in conversation; methodology is universal). Either call it "four-layer" up front, or rename the promotion path "the durability ladder" so it doesn't contradict the headline "two layers" terminology.

### methodology/09_git_workflow.md

(Note: doc 09 includes the new v1.13.0 "Patch-branch convention" sub-section. Evaluated.)

**Stale:**
- _(none)_

**Unclear:**
- The patch-branch convention (`methodology/09_git_workflow.md:78-100`, new in v1.13.0) introduces `<area>-patch/YYYY-MM-DD-NN` as the branch shape. The examples (lines 88-92) show `methodology-patch`, `designsystem-patch`, `spec-patch` — but the doc never says how a project *chooses* an area prefix, or whether the prefix has to be pre-registered. A new project adopting the convention has no guidance on: "should I add a new area each time I get a new authoritative artifact, or maintain a fixed registry of areas?" The "Branch naming" section earlier (lines 38-71) treats prefixes (`feature/`, `fix/`, etc.) as a fixed list; the patch-branch convention reads as open-ended. Either name it open-ended explicitly or provide a default list (e.g., "common areas: methodology, designsystem, spec, runbook").
- The new sub-section says "the autonomous loop **never auto-merges a patch branch**" (line 100) but the table at lines 545-569 lists `gh pr merge` with a ⚠ ("only with the user's explicit OK"), not ✗ (never). A cold reader cannot reconcile: is patch-branch merge under "never" (matching the patch-branch wording) or "with OK" (matching the table)? Likely the intent is "patch-branch merge to trunk is a maintainer-only act" — but two parts of the same doc say it with different specificity.

**Inconsistent:**
- The patch-branch convention requires "a CHANGELOG entry, and (where applicable) a cross-AI verification note" land in the same patch branch (line 96). But the "CHANGELOG entry" requirement is doc 07's Gate 4 territory, and the "cross-AI verification note" is doc 10's diff-verification territory. The patch-branch sub-section in doc 09 quietly bundles obligations from 07 and 10 without flagging them as "you also need to satisfy 07 Gate 4 and 10 diff-verification before this patch is mergeable." A cold contributor reading only 09 would think "CHANGELOG entry + verification note" is the full requirement; they'd miss the DoD's other gates that still apply (e.g., backlog state correct, automated tests where applicable to the patch).
- The "What AI agents can and can't do in git" table (`methodology/09_git_workflow.md:545-569`) lists `git pull --ff-only` (line 551) as ✓ "Read-only sync." But `git pull --ff-only` is *not* read-only — it can modify the working tree (a fast-forward updates files in place, can change HEAD, and conflicts with uncommitted local changes by refusing). The doc's own definition of "read-only inspection" at line 547 (`git status / git diff / git log / git show`) sets the bar that `--ff-only` does not actually meet. Either re-label the row (e.g., "Idempotent sync") or move `pull --ff-only` out of the read-only cluster.
- The patch-branch convention's claim that "Review is yes/no on a concrete change, not translate-finding-into-fix" (line 96) implicitly contradicts the decision-ownership matrix in doc 11 (lines 229-251) where most code decisions still have "Human reviews" or "Human decides" columns set even when the AI proposes. The patch branch doesn't change the underlying ownership — it just packages it. The new sub-section reads as if patch-branching shifts something material in the ownership matrix; nothing in doc 11 was updated to reflect that. Either align the wording (patch-branch convention is a *packaging* mechanism, not an *autonomy* mechanism) or update doc 11's matrix.

### methodology/10_testing_and_verification.md

(Note: doc 10 includes the new v1.13.0 "Two modes: findings-verification and diff-verification" sub-section. Evaluated.)

**Stale:**
- _(none)_

**Unclear:**
- The new "Two modes" sub-section (`methodology/10_testing_and_verification.md:560-574`, new in v1.13.0) defines findings-verification as "checking *completeness and correctness of claims*" and diff-verification as a check on "grounded / correct / scoped." But the doc doesn't say what to do when a finding's diff-verification *partially* fails — e.g., the proposed edit is correct and scoped but the original cited content has a different problem the finding didn't name. Is that PASS, FAIL, or PARTIAL? The PASS/FAIL binary is asserted (line 574); the partial case is left to the maintainer. Cold contributors running diff-verification need guidance on partial cases — file a new finding? Reject the patch? Accept with a note?
- "Verification levels: matching depth to risk" (`methodology/10_testing_and_verification.md:578-640`) defines L0–L4 levels. The mapping table at lines 597-608 says e.g. "User-facing fix or small feature" requires "L0, L1, L2." But the verification checklist template at lines 421-457 (used in PR test plans) doesn't carry level annotations. A cold contributor producing a PR for an L2 change vs. an L4 change uses the same checklist. The doc *says* (line 614-622) "the item's `Test:` field can carry the level reached" — but the checklist that lands in the PR doesn't. Either add an `L#` row to the checklist, or note that the level lives only on the backlog item.
- The findings-verification mode (lines 564) describes the validator as checking "this BL-#### item's Done-means are all satisfied" — but "Done-means" is a term that doesn't appear anywhere else in the methodology. The DoD section (doc 07) uses "gates" or "DoD criteria." The autonomous-loop template (per the cross-reference) may use "Done means" but a cold contributor reading only 10 wouldn't know. Either use "DoD gates" consistently or define "Done-means" at first use.

**Inconsistent:**
- The "Two modes" sub-section's diff-verification (line 572) says the maintainer's role becomes "ratification, not original review." But doc 09's patch-branch convention (line 96) says "The maintainer reviews diffs, not findings." The two phrasings are close but not identical: "ratification" implies signing off on someone else's review; "reviews diffs" implies the maintainer *does* the review. The two docs co-shipped in v1.13.0 should pick one frame.
- "User testing is the final gate" (`methodology/10_testing_and_verification.md:644-678`) establishes user acceptance as the terminal verification. But the order of operations diagram (lines 670-672) — "Automated tests → UI verification loop → Cross-AI validation → User testing → Ship" — places cross-AI before user testing. The new "Two modes" sub-section (lines 560-574) describes diff-verification as a gate for patch branches; it's not clear whether diff-verification on a patch-branch fix needs to also run *user testing* before merge (since patch-branch fixes for methodology docs typically don't have a "user" in the user-testing sense). The order-of-operations diagram applies to user-observable changes; the patch-branch fix-to-methodology case is a gap.

### methodology/11_human_roles.md

**Stale:**
- _(none)_

**Unclear:**
- "When to skip" (`methodology/11_human_roles.md:176-179`) lists three conditions allowing the human to skip the pre-implementation architectural review. The first is "The change is small (effort `XS` or `S`)." But effort sizes are defined in doc 04 (`methodology/04_backlog_items.md:151-156`) — XS is "Under 2 hours" — and the methodology nowhere defines what "small" means *independent of effort.* A cold contributor working on an item without a stamped effort label (e.g., a hotfix not yet in the backlog) has no XS/S anchor to apply. Either reference doc 04's table or define "small" inline.
- The "decision-ownership matrix" (`methodology/11_human_roles.md:229-251`) shows rows like "Bug fix (small, well-scoped, in code AI wrote)" with both "AI decides" ✓ and "Human reviews" ✓ checked. The semantic of two boxes checked is not defined: does "AI decides AND human reviews" mean (a) AI ships, human catches issues post-hoc; (b) AI proposes a fix, human approves before commit; (c) AI commits but doesn't merge until human signs off? The matrix legend at lines 254-259 explains each column individually but never two-column combinations. The combinations are doing work in the table; their semantics need a line.
- "Pricing, business model, contractual terms" (`methodology/11_human_roles.md:246`) is in the human-only column — but the methodology is silent on whether the *strategy doc* (`methodology/01_strategy.md`) covers this (the BL-0007 doc-01 review showed it does) or whether the line item is purely operational. A cold reader could interpret "pricing" as "the operational pricing decision when launching a feature" (operational, definitely human-only) or "the documented pricing strategy in the strategy doc" (also human-only, but a strategy artifact that gets re-evaluated periodically). Different read; different application.

**Inconsistent:**
- The "skills that grow less critical" list (`methodology/11_human_roles.md:200-204`) includes "Pure code-writing speed" and "Memorizing framework APIs." But the methodology's working principles (doc 06) demand contributors verify their code carefully, follow surgical-change discipline, and pass the DoD gates — all of which require enough code reading and writing fluency to recognize anti-patterns and bundled refactors. The "less critical" framing in doc 11 could be read as "you no longer need to be able to code competently," which contradicts the per-item supervisory work doc 11 itself describes (lines 44-55: "Knowing when to let an agent run and when to intervene... Fixing output by refining the prompt"). The intent is clearly "speed of typing matters less," but the surface reads as "ability matters less." Sharpen.
- "Hard-coded ownership" sub-section (`methodology/11_human_roles.md:271-280`) lists "Never run production deploys autonomously" as one of four absolute rules. The 00 README's hard-rules table (`methodology/00_README.md:184-194`) names this rule. But doc 11's list also includes "Never bypass pre-commit hooks" (line 278) — which IS in 00's hard-rules table (line 190) — and "Never force-push" (line 277) — also in 00 (line 187). However, doc 11 omits "Status: done requires Test: pass" (which is also in 00's hard rules at line 186) and "Never steal a live lock" (in 00 at line 191). A reader treating doc 11 as canonical for "hard-coded ownership" would not see those two. The "hard rules" inventory should match between 00 and 11 — either say "these are the git/ops hard rules; see 00 for the full inventory" or list all of them.
- The decision-ownership matrix (`methodology/11_human_roles.md:229-251`) and the AI-agents-can-do table in 09 (`methodology/09_git_workflow.md:545-569`) cover overlapping operations. For example: "Database schema change" (11, line 239) is human-decides; but "git commit on a feature branch" (09, line 549) is AI ✓. A schema change requires a commit. The two tables don't acknowledge each other's existence — doc 11 has a "Pairs with" note (line 543, in doc 09's affirmative-list section) but doc 11's matrix doesn't reciprocally cite doc 09. The non-reciprocal cross-link increases the risk of one table drifting without the other.

### Cross-batch inconsistencies (00–05 vs 06–11)

- **"Six gates" vs. omitted gate.** Doc 00 (`methodology/00_README.md:145, 194`) and doc 07 (`methodology/07_definition_of_done.md:27, 184`) both name "six gates." BL-0007 didn't flag this in doc 00. The Gate-5 collapse issue (Gate 5 is the loop, not a peer gate) flagged in this batch suggests both 00 and 07 should be updated together; doc 00's hard-rules row "The DoD's six gates apply to every item" (line 194) will need to track whatever 07 settles on.
- **Em-dash vs hyphen-minus for `Lock: —`.** BL-0007 flagged doc 04's grep examples (`methodology/04_backlog_items.md:813-839`) as using a bold-wrapped field pattern that doesn't match the canonical plain-table form. This batch found doc 07's checklist (`methodology/07_definition_of_done.md:410`) uses `Lock: -` (ASCII hyphen) while doc 00 (line 204) uses `Lock: —` (em-dash). Both ends of the methodology have character-level inconsistencies in lock-field display; a fix should pick one character and propagate through 00, 04, 07.
- **The "2+ occurrences" trigger fragmentation.** BL-0007 noted doc 04's lifecycle implies status-flip-with-lock is automatic, doc 05 treats it as optional. This batch found doc 08's "2+ in different contexts" rule for writing feedback (line 236-240) is the *project-side* expression of the *same* fundamental "twice = rule" pattern that drives lock TTL discipline, expired-lock policy, and the promotion path. The methodology has at least four "twice triggers a rule" mechanisms (doc 04 lifecycle, doc 05 lock-expiry follow-up, doc 08 memory write, doc 08 promotion) but never names this as a meta-pattern. A cold reader sees it as four ad-hoc rules; in practice it's one principle applied four ways.
- **Authority chain — DoD ranking vs. principles.** BL-0007's doc-00 review noted the Authority section (lines 362-369) lists six precedence layers including "Hard rules" and "Working principles and Definition of Done." Doc 06 (line 327-331) and doc 07 (line 484-486) both have their own Authority sections that name user-direction-vs-rule but neither cross-references the other. The result is: 00 says principles and DoD are co-equal (layer 3); 06 implies DoD is downstream of principles ("How DoD relates to other parts" line 473-481 lists principles first); 07 says principles and DoD are mutually orthogonal ("Both required and they are not the same gate," line 252). All three positions are reasonable; the cross-doc presentation is what's incoherent. Pick a single frame for the principles↔DoD relationship and apply across 00/06/07.
- **Lock-overriding language.** BL-0007 found doc 00's hard-rules table omits "AI agents never override locks" (from `methodology/05_locks_and_parallel_work.md:494`). This batch found doc 09's affirmative table at line 545-569 lists destructive operations but doesn't include any lock-related row, and doc 11's "hard-coded ownership" list (line 275-278) covers four absolutes but skips locks. The lock-override rule is in doc 05; doc 00 doesn't surface it; docs 09 and 11 silently inherit the gap. The rule is consistent in spirit across the batch but consistently missing from the "this is the hard floor" tables in 00/09/11.

## Classification + dispositions

_Populated by BL-0009. Each row maps one finding to (practice/docs axis, tier axis, disposition). Tier ladder: T0 cosmetic / T1 surgical / T2 substantive / T3 architectural. Escalate-on-doubt: when between T1 and T2, classified as T2._

| ID | Source | Practice/docs | Tier | Disposition | Notes |
|---|---|---|---|---|---|
| F01 | doc 00, Stale #1 | docs-wrong | T1 | Ship now (v1.14.0) | Add doc 11 to reading-path table rows for "New contributor" and "Picking up a specific item" at `methodology/00_README.md:122-123`. |
| F02 | doc 00, Stale #2 | docs-wrong | T2 | Loop-notes (maintainer authors) | Mental-model diagram (lines 93-103) predates doc 11; needs a 4th cluster slot or re-framing. Substantive reframing. |
| F03 | doc 00, Unclear #1 | docs-wrong | T0 | Ship now (v1.14.0) | Replace `EPICS.md(#)` placeholder anchor on `methodology/00_README.md:203` with explicit `backlog/EPICS.md` path. Cosmetic broken-link fix. |
| F04 | doc 00, Unclear #2 | docs-wrong | T1 | Ship now (v1.14.0) | Add a one-line note near `methodology/00_README.md:236` explaining `templates/` is a sibling folder of methodology artifacts. |
| F05 | doc 00, Inconsistent #1 | docs-wrong | T2 | Loop-notes (maintainer authors) | Hard-rules table omits "AI agents never override locks" (doc 05:494). Adding a hard rule is a substantive change to an authoritative list. |
| F06 | doc 00, Inconsistent #2 | docs-wrong | T2 | Loop-notes (maintainer authors) | Authority section silent on autonomous-loop Constraint 1; substantive call about whether project-specific constraints belong in the universal README. |
| F07 | doc 01, Unclear #1 | docs-wrong | **T2** (escalated from T1 per Sonnet tier-verify) | Loop-notes (maintainer authors) | Adding the sentence requires picking a convention (master plan implicit vs. row 00) — that's a policy decision, not a clarification of existing text. |
| F08 | doc 01, Unclear #2 | docs-wrong | T2 | Loop-notes (maintainer authors) | Strategy docs silent on default re-eval frequency; substantive guidance addition for a previously template-only field. |
| F09 | doc 01, Inconsistent #1 | docs-wrong | T2 | Loop-notes (maintainer authors) | "Snapshots vs living" terminology drift across 01/02; substantive reframing of the lifecycle vocabulary. |
| F10 | doc 02, Unclear #1 | docs-wrong | T1 | Ship now (v1.14.0) | Add clarifying line near `methodology/02_pillars.md:65-75` reinforcing "illustrative" intent of the P1-P9 table. |
| F11 | doc 02, Unclear #2 | docs-wrong | T2 | Loop-notes (maintainer authors) | Relationship between `docs/architecture/` and `docs/pillars/` is undefined; substantive folder-convention guidance addition. |
| F12 | doc 02, Inconsistent #1 | docs-wrong | T1 | Ship now (v1.14.0) | Strategy-outranks-pillars rule duplicated in 00/01/02; add reciprocal cross-refs so a future edit to one surfaces the other two. |
| F13 | doc 03, Unclear #1 | docs-wrong | **T2** (escalated from T1 per Sonnet tier-verify) | Loop-notes (maintainer authors) | Clarifying the `parked → done` transition either (a) removes a state-machine edge or (b) defines a new rule for an undocumented case. Either is substantive. |
| F14 | doc 03, Unclear #2 | docs-wrong | **T2** (escalated from T1 per Sonnet tier-verify) | Loop-notes (maintainer authors) | "Solo: 1" is not in the source doc — adding it as a recommended default is new prescriptive guidance, not a clarification. |
| F15 | doc 03, Inconsistent #1 | docs-wrong | T0 | Ship now (v1.14.0) | Epic charter template at `methodology/03_epics.md:151-195`: change `Started: YYYY-MM-DD` to `Started: — (or YYYY-MM-DD when active)` to match prose rule. |
| F16 | doc 03, Inconsistent #2 | docs-wrong | T2 | Loop-notes (maintainer authors) | Epic close-out is functionally a DoD for epics but doc 07 doesn't acknowledge it; cross-link or restructure. Substantive cross-doc framing. |
| F17 | doc 04, Stale #1 | docs-wrong | T1 | Ship now (v1.14.0) | Drop the `\*\*` bold wrappers from grep examples at `methodology/04_backlog_items.md:813-839` to match canonical plain-table template. |
| F18 | doc 04, Unclear #1 | docs-wrong | T1 | Ship now (v1.14.0) | Recommend recording the FUTURE.md numbering choice in the project's instruction file or backlog README; add to `methodology/04_backlog_items.md:48-66`. |
| F19 | doc 04, Unclear #2 | docs-wrong | T2 | Loop-notes (maintainer authors) | ID-collision-prevention guidance missing; substantive addition of new prevention guidance to a discipline doc. |
| F20 | doc 04, Inconsistent #1 | docs-wrong | T1 | Ship now (v1.14.0) | Add footnote to lifecycle diagram (`methodology/04_backlog_items.md:466-479`) explaining hyphen→underscore mapping for mermaid state names. |
| F21 | doc 04, Inconsistent #2 | docs-wrong | **T2** (escalated from T1 per Sonnet tier-verify) | Loop-notes (maintainer authors) | "Optionally" in doc 05 may be a deliberate hedge; making it mandatory is a rule-wording change in the lock-discipline doc that governs concurrent work. Maintainer decides which framing is canonical. |
| F22 | doc 05, Unclear #1 | docs-wrong | T0 | Ship now (v1.14.0) | Promote "default to 2 hours" callout into the table caption or bold prose at `methodology/05_locks_and_parallel_work.md:271-281`. Cosmetic emphasis fix. |
| F23 | doc 05, Unclear #2 | docs-wrong | T2 | Loop-notes (maintainer authors) | Expired-locks investigation flow needs a "what if the holder is still alive?" branch; substantive addition of new policy case. |
| F24 | doc 05, Inconsistent #1 | docs-wrong | T1 | Ship now (v1.14.0) | Add a sentence in doc 04 acknowledging subagent flows defer to the orchestrator's lock; align "lock-holder" (doc 04) vs "orchestrator" (doc 05) vocabulary. |
| F25 | doc 05, Inconsistent #2 | docs-wrong | T1 | Ship now (v1.14.0) | Add clarifying note that 24h is the *ceiling for rare cases*, not the *default*, on `methodology/05_locks_and_parallel_work.md:277` vs line 466. |
| F26 | doc 06, Unclear #1 | docs-wrong | T1 | Ship now (v1.14.0) | Add a sentence at "Plan before executing" (line 132-168) saying "this is not a fifth principle; it's the gating rule." |
| F27 | doc 06, Unclear #2 | docs-wrong | T2 | Loop-notes (maintainer authors) | "Challenge before consenting" — mandatory or contextual? Substantive call on whether contrarian-case prompt is required at every plan or only at-stakes. |
| F28 | doc 06, Inconsistent #1 | docs-wrong | T2 | Loop-notes (maintainer authors) | Anti-patterns table single-mapping convention contradicts the docs' own acknowledgment of cross-principle reinforcement; substantive table restructure. |
| F29 | doc 06, Inconsistent #2 | docs-wrong | T2 | Loop-notes (maintainer authors) | Principles vs DoD ranking unstated; substantive cross-doc Authority chain alignment (see also F46 cross-batch entry). |
| F30 | doc 07, Unclear #1 | docs-wrong | T1 | Ship now (v1.14.0) | Specify which doc-audit pass (quarterly vs semi-annual) covers the methodology specifically; add a sentence at `methodology/07_definition_of_done.md:323`. |
| F31 | doc 07, Unclear #2 | docs-wrong | T1 | Ship now (v1.14.0) | Make 07's "Memory index" update-trigger mirror 08's "same commit" phrasing at `methodology/07_definition_of_done.md:215-225`. |
| F32 | doc 07, Inconsistent #1 | docs-wrong | T2 | Loop-notes (maintainer authors) | Gate 5 is the loop, not a peer gate; substantive reframing of the "six gates" count and structure. |
| F33 | doc 07, Inconsistent #2 | docs-wrong | T1 | Ship now (v1.14.0) | Add the doc 03 cross-link in Gate 6 (epic rollup) at `methodology/07_definition_of_done.md:111-122`. |
| F34 | doc 07, Inconsistent #3 | docs-wrong | T0 | Ship now (v1.14.0) | Change `Lock: -` to `Lock: —` (em-dash) in the DoD checklist at `methodology/07_definition_of_done.md:410`. Cosmetic character fix; see also F47 cross-batch. |
| F35 | doc 08, Unclear #1 | docs-wrong | T1 | Ship now (v1.14.0) | Add a real index-row example (e.g., kebab-slug + sentence hook) at `methodology/08_lessons_and_memory.md:198-206`. |
| F36 | doc 08, Unclear #2 | docs-wrong | T2 | Loop-notes (maintainer authors) | Define the "session" unit for the promotion bar; substantive definition addition for AI-driven workflows. |
| F37 | doc 08, Inconsistent #1 | docs-wrong | T1 | Ship now (v1.14.0) | Add cross-link in doc 08 "Trigger 2" noting "this is the same '2+ occurrences' bar used elsewhere in the methodology." |
| F38 | doc 08, Inconsistent #2 | docs-wrong | T2 | Loop-notes (maintainer authors) | Two-layer vs four-layer contradiction at `methodology/08_lessons_and_memory.md:27-53` vs lines 453-462; substantive vocabulary reframing. |
| F39 | doc 09, Unclear #1 | docs-wrong | T1 | Ship now (v1.14.0) | Clarify whether patch-branch area prefix is open-ended or registered; add a default list (e.g., "common areas: methodology, designsystem, spec, runbook"). |
| F40 | doc 09, Unclear #2 | docs-wrong | **T2** (escalated from T1 per Sonnet tier-verify) | Loop-notes (maintainer authors) | Adding a patch-branch-specific ✗ row to the AI-autonomy table changes the specificity of an autonomy rule in the most safety-critical table in the methodology. Maintainer authors. |
| F41 | doc 09, Inconsistent #1 | docs-wrong | T1 | Ship now (v1.14.0) | Add explicit cross-link in patch-branch sub-section to doc 07 (Gate 4) and doc 10 (diff-verification); flag that other DoD gates still apply. |
| F42 | doc 09, Inconsistent #2 | docs-wrong | T0 | Ship now (v1.14.0) | Re-label `git pull --ff-only` row in `methodology/09_git_workflow.md:545-569` — not strictly read-only. Cosmetic mislabel. |
| F43 | doc 09, Inconsistent #3 | docs-wrong | T2 | Loop-notes (maintainer authors) | Patch-branch convention as packaging vs autonomy mechanism; substantive cross-doc ownership-matrix alignment with doc 11. |
| F44 | doc 10, Unclear #1 | docs-wrong | T2 | Loop-notes (maintainer authors) | Diff-verification partial-failure semantics undefined; substantive new policy on PASS/FAIL/PARTIAL outcomes. |
| F45 | doc 10, Unclear #2 | docs-wrong | T1 | Ship now (v1.14.0) | Note in `methodology/10_testing_and_verification.md:578-640` that verification level lives only on the backlog item, not the PR checklist (or add an `L#` row to the checklist). |
| F46 | doc 10, Unclear #3 | docs-wrong | T1 | Ship now (v1.14.0) | Replace "Done-means" with "DoD gates" at `methodology/10_testing_and_verification.md:564` (or define "Done-means" at first use). |
| F47 | doc 10, Inconsistent #1 | docs-wrong | T1 | Ship now (v1.14.0) | Align "ratification" (doc 10:572) vs "reviews diffs" (doc 09:96); pick one phrase. |
| F48 | doc 10, Inconsistent #2 | docs-wrong | T2 | Loop-notes (maintainer authors) | Order-of-operations gap for patch-branch fix-to-methodology case (no "user" in user-testing sense); substantive new policy on terminal-verification for non-user-facing patches. |
| F49 | doc 11, Unclear #1 | docs-wrong | T1 | Ship now (v1.14.0) | Reference doc 04's XS/S effort definitions inline at `methodology/11_human_roles.md:176-179`, or define "small" inline. |
| F50 | doc 11, Unclear #2 | docs-wrong | T2 | Loop-notes (maintainer authors) | Define the semantic of two-column-checked combinations in the decision-ownership matrix; substantive policy clarification. |
| F51 | doc 11, Unclear #3 | docs-wrong | T1 | Ship now (v1.14.0) | Clarify "Pricing, business model, contractual terms" line item — operational pricing vs strategy doc pricing — at `methodology/11_human_roles.md:246`. |
| F52 | doc 11, Inconsistent #1 | docs-wrong | T1 | Ship now (v1.14.0) | Sharpen "skills that grow less critical" at `methodology/11_human_roles.md:200-204` from "ability matters less" → "typing speed matters less". |
| F53 | doc 11, Inconsistent #2 | docs-wrong | T2 | Loop-notes (maintainer authors) | Hard-coded ownership inventory mismatch between doc 00 and doc 11; substantive cross-doc enumeration alignment (see also F58 cross-batch). |
| F54 | doc 11, Inconsistent #3 | docs-wrong | T1 | Ship now (v1.14.0) | Add reciprocal "Pairs with doc 09" cross-link in doc 11's decision-ownership matrix at `methodology/11_human_roles.md:229-251`. |
| F55 | Cross-batch #1 | docs-wrong | T2 | Loop-notes (maintainer authors) | "Six gates" framing needs joint update across 00 and 07; see F32. Substantive coordinated rewrite. |
| F56 | Cross-batch #2 | docs-wrong | T0 | Ship now (v1.14.0) | Em-dash vs hyphen-minus for `Lock: —` — pick one character and propagate across 00, 04, 07. Cosmetic but multi-file. |
| F57 | Cross-batch #3 | docs-wrong | T2 | Loop-notes (maintainer authors) | Name the "twice = rule" meta-pattern (currently expressed ad-hoc in docs 04/05/08); substantive new conceptual framing. |
| F58 | Cross-batch #4 | docs-wrong | T2 | Loop-notes (maintainer authors) | Authority chain — DoD vs principles ranking — coordinated alignment across 00/06/07. Substantive cross-doc reframing (see F29). |
| F59 | Cross-batch #5 | docs-wrong | T2 | Loop-notes (maintainer authors) | Lock-override rule missing from "hard floor" tables in 00/09/11; substantive cross-doc enumeration alignment (see F05 and F53). |

### Ship plan for v1.14.0

This batch is the maintainer's coherent v1.14.0 patch set. T0 cosmetic + T1 surgical findings that meaningfully reduce future cold-read friction. Grouped by target file.

**`methodology/00_README.md`**
- **F01:** Add doc 11 to reading-path table rows "New contributor" and "Picking up a specific item" at lines 122-123.
- **F03:** Replace `EPICS.md(#)` placeholder anchor on line 203 with explicit `backlog/EPICS.md` path.
- **F04:** Add a one-line note near line 236 explaining `templates/` is a sibling folder of methodology artifacts.
- **F12 (also touches 01/02):** Add reciprocal cross-refs between the three Authority restatements at 00:362-369, 01:469-475, 02:368-369.
- **F56 (cross-batch):** Normalize `Lock: —` to em-dash (or hyphen-minus — maintainer picks one) at line 204.

**`methodology/01_strategy.md`**
- **F07:** Reconcile numbering between supporting-doc table (lines 80-95) and Document Index template (lines 316-331); add a sentence specifying convention.
- **F12 (also touches 00/02):** Reciprocal Authority cross-ref at 01:469-475.

**`methodology/02_pillars.md`**
- **F10:** Add clarifying line near lines 65-75 reinforcing "illustrative" intent of the P1-P9 table.
- **F12 (also touches 00/01):** Reciprocal Authority cross-ref at 02:368-369.

**`methodology/03_epics.md`**
- **F13:** Clarify the `parked → done` transition at lines 287-294; remove "(somehow)" parenthetical.
- **F14:** Surface "default 3, solo: 1" WIP recommendation up front at line 50.
- **F15:** Change `Started: YYYY-MM-DD` to `Started: — (or YYYY-MM-DD when active)` in the Epic charter template at lines 151-195.

**`methodology/04_backlog_items.md`**
- **F17:** Drop `\*\*` bold wrappers from grep examples at lines 813-839 to match canonical plain-table template.
- **F18:** Recommend recording the FUTURE.md numbering choice in the project's instruction file or backlog README; add to lines 48-66.
- **F20:** Add footnote to lifecycle diagram (lines 466-479) explaining hyphen→underscore mapping for mermaid state names.
- **F21:** Align "automatic" vs "optional" status-flip-with-lock — recommend always-flip-together; reciprocal edit on doc 05.
- **F24:** Add a sentence acknowledging subagent flows defer to the orchestrator's lock; align "lock-holder" vocabulary with doc 05.
- **F56 (cross-batch):** Normalize `Lock: —` to em-dash in any examples in this doc.

**`methodology/05_locks_and_parallel_work.md`**
- **F21 (reciprocal):** Align acquire-protocol step 4 wording with doc 04's lifecycle (status-flip is automatic, not optional).
- **F22:** Promote "default to 2 hours" callout into the TTL table caption or bold prose at lines 271-281.
- **F25:** Add clarifying note that 24h is the *ceiling for rare cases*, not the *default*, at line 277 vs line 466.

**`methodology/06_working_principles.md`**
- **F26:** Add a sentence at "Plan before executing" (lines 132-168) saying "this is not a fifth principle; it's the gating rule for *when* the four principles start applying."

**`methodology/07_definition_of_done.md`**
- **F30:** Specify which doc-audit pass (quarterly vs semi-annual) covers the methodology; add a sentence at line 323.
- **F31:** Make "Memory index" update-trigger mirror 08's "same commit" phrasing at lines 215-225.
- **F33:** Add doc 03 cross-link in Gate 6 (epic rollup) at lines 111-122.
- **F34:** Change `Lock: -` to `Lock: —` (em-dash) in the DoD checklist at line 410.
- **F56 (cross-batch):** Normalize same `Lock: —` character throughout the doc.

**`methodology/08_lessons_and_memory.md`**
- **F35:** Add a real index-row example (e.g., kebab-slug + sentence hook) at lines 198-206.
- **F37:** Add cross-link in "Trigger 2" noting the "2+ occurrences" bar is shared across the methodology.

**`methodology/09_git_workflow.md`**
- **F39:** Provide default list of common patch-branch areas (e.g., methodology, designsystem, spec, runbook) at lines 78-100.
- **F40:** Reconcile "never auto-merges a patch branch" (line 100) with `gh pr merge` ⚠ (line 545-569); make the table cell row-specific for patch branches.
- **F41:** Add explicit cross-link in patch-branch sub-section to doc 07 (Gate 4) and doc 10 (diff-verification).
- **F42:** Re-label `git pull --ff-only` row at line 551 — not strictly read-only (use "Idempotent sync" or move out of read-only cluster).
- **F47 (also touches 10):** Pick one phrase between "ratification" (10:572) and "reviews diffs" (09:96); align.

**`methodology/10_testing_and_verification.md`**
- **F45:** Note that verification level lives only on the backlog item, not the PR checklist, at lines 578-640 (or add `L#` row).
- **F46:** Replace "Done-means" with "DoD gates" at line 564 (or define at first use).
- **F47 (also touches 09):** Align phrasing with patch-branch convention.

**`methodology/11_human_roles.md`**
- **F49:** Reference doc 04's XS/S effort definitions inline at lines 176-179, or define "small" inline.
- **F51:** Clarify "Pricing, business model, contractual terms" — operational pricing vs strategy-doc pricing — at line 246.
- **F52:** Sharpen "skills that grow less critical" at lines 200-204 from "ability matters less" to "typing speed matters less".
- **F54:** Add reciprocal "Pairs with doc 09" cross-link in doc 11's decision-ownership matrix at lines 229-251.

### Summary statistics (preview for BL-0010)

**Total findings classified:** 59

**By source batch:**
- BL-0007 (docs 00-05): 25 findings (F01-F25)
- BL-0008 (docs 06-11): 29 findings (F26-F54)
- Cross-batch inconsistencies: 5 findings (F55-F59)

**Practice/docs axis distribution:**
- `docs-wrong`: 59 (all findings)
- `practice-wrong`: 0
- `both`: 0

(All findings are docs-wrong because cold-read findings are by construction discrepancies in the docs themselves — practice gaps weren't a discovery target of BL-0007/0008. Maintainer note: practice-wrong items would surface through memory-entry candidates, not cold reads, so the absence here is expected.)

**Tier axis distribution (post tier-verification):**
- T0 (cosmetic): 6 findings — F03, F15, F22, F34, F42, F56
- T1 (surgical): **25** findings — F01, F04, F10, F12, F17 (shipped in v1.13.0), F18, F20, F24, F25, F26, F30, F31, F33, F35, F37, F39, F41, F45, F46, F47, F49, F51, F52, F54
- T2 (substantive): **28** findings — F02, F05, F06, F07*, F08, F09, F11, F13*, F14*, F16, F19, F21*, F23, F27, F28, F29, F32, F36, F38, F40*, F43, F44, F48, F50, F53, F55, F57, F58, F59
- T3 (architectural): 0 findings

(\* = escalated T1 → T2 by fresh-Sonnet tier-verifier per escalate-on-doubt rule.)

**Disposition distribution:**
- **Shipped in v1.13.0:** 1 (F17, the demonstration patch).
- **Shipped in v1.14.0:** 30 patches (all T0 + remaining T1 after escalations).
- **Loop-notes (maintainer authors, T2 substantive):** 28 findings — deferred to next eval cycle or staged maintainer-authored patches.
- **Human-only (T3 architectural):** 0 findings.

**T2/T3 items requiring maintainer-authored future work:** 28 (all T2; no T3 in this pass).

**Escalation-on-doubt audit:** During classification, several findings were borderline T1/T2 and resolved T2 per the escalation rule. Notable cases: F09 ("snapshots vs living"), F11 (architecture vs pillars folder relationship), F19 (ID-collision prevention), F27 (mandatory vs contextual contrarian prompt), F38 (two-layer vs four-layer terminology), F50 (two-column matrix semantics). These are surface-clarification-shaped but each implies a downstream policy or vocabulary choice the maintainer should own.

## Summary statistics

**Pass duration:** 2026-05-25 (single-day pass; bootstrap, eval cycle, and patch ship all on the same date because the self-development project shipped its bootstrap and ran the first eval cycle in one session).

**Total findings classified:** 59
- BL-0007 (docs 00–05): 25 findings (3 stale / 12 unclear / 10 inconsistent)
- BL-0008 (docs 06–11): 29 findings (0 stale / 14 unclear / 15 inconsistent)
- Cross-batch inconsistencies: 5 findings

**Practice/docs axis:** 59 / 0 / 0 (`docs-wrong` / `practice-wrong` / `both`). All findings were docs-wrong by construction of the cold-read mechanism. Practice gaps would be surfaced through memory-entry candidates and runtime observations, not cold reads — and the loop-notes captured a few of those separately.

**Tier axis (post tier-verification):** T0 6 / T1 25 / T2 28 / T3 0. The 5 T1 → T2 escalations (per Sonnet's escalate-on-doubt verification on a 10-finding sample) are documented in the classification table.

**Patches shipped:**
- **v1.13.0** (2026-05-25, earlier): 1 patch — F17 grep-examples fix in `methodology/04_backlog_items.md`, demonstration of the tier-matrix mechanism.
- **v1.14.0** (2026-05-25, this pass closure): 30 patches across 12 methodology files — all T0 + remaining T1 after escalations. Cross-AI diff-verified per the new diff-verification mode.

**Patches deferred to maintainer authorship:** 28 (all T2). Logged in `self-development/loop-notes/2026-05-25.md` with the relevant context for the maintainer's authorship cycle.

**End-state of methodology files:** 11 of 12 methodology docs (00–11) received at least one patch this pass. Doc 11 received the most (4 patches); docs 06 and 03 received the fewest (1 patch each). No methodology doc structure was changed; all patches stay within existing section shapes.

## Next eval date

**Target:** 2026-11-25 (~6 months from this pass, per the [semi-annual cadence](../../methodology/07_definition_of_done.md#methodology-self-evaluation-semi-annual)).

**Adjustment rule:** if a significant methodology release ships before that date, the next eval may be brought forward by 1–2 months to cold-read the new material. If no material methodology change happens in the 6-month window, the eval can be deferred by up to 2 months.

**Process improvements to apply at the next pass:**
1. **Spawn cold-read agents in `general-purpose` role** (or equivalent with Write/Edit tools), not `Explore` — established as standard practice this pass (lesson #1 in loop-notes).
2. **Use per-category `_(none)_` empty markers** for deterministic Done-means verification (lesson #2 in loop-notes).
3. **Two-axis classification (practice/docs + tier)** is now the standard, not an option. The v1.13.0 tier matrix is the default operating model.
4. **Tier classifications are cross-AI verified** per escalate-on-doubt. The 5 escalations this pass demonstrate the rule catches over-claiming consistently.

## Maintainer signoff

```
Reviewed by: _________________________
Date:         _________________________
Verdict:      [ ] Accept — close E02 at Status: done.
              [ ] Conditional accept — minor revisions before close.
              [ ] Reject — return to loop with feedback.
Notes:
```

_Awaiting maintainer signoff to close E02. Once signed, BL-0006/0007/0008/0009/0010 flip from `to-be-tested` to `done` and move to `ARCHIVE.md`; E02 charter moves from `active` to `done` in EPICS.md._
