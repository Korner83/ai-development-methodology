# 2026 first semi-annual self-evaluation pass

_Skeleton seeded by BL-0006. Content populated by BL-0007 through BL-0010._

## Metadata

- **Date of pass:** 2026-05-25
- **Methodology version at eval:** v1.12.0
- **Reviewer model + session:** Opus 4.7 via fresh general-purpose agent (no prior turns referencing this project). Docs 00–05 batch: BL-0007.
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

_(empty)_

## Classification + dispositions

_Populated by BL-0009. Table of all findings with classification (`practice-wrong` / `docs-wrong` / `both`) and disposition (`patch release` / `file as item` / `defer`)._

_(empty)_

## Summary statistics

_Populated by BL-0010. Counts of findings by classification and by disposition. Time-to-complete the pass. Patch releases shipped from this pass._

_(empty)_

## Next eval date

_Recorded by BL-0010. Target: ~6 months out from this pass (~2026-11-25 if this pass completes on schedule)._

_(empty)_

## Maintainer signoff

_Awaiting signature on completion of BL-0010._

_(empty)_
