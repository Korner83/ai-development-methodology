# E00 — Intake — Archive

_Closed and rejected intake items. Append-only._

---

### BL-0057 — Drop the template version-stamp criterion

`Status: done` · `Test: pass` — the criterion no longer appears as unmet in the master plan; no template gained a stamp, by design

**Files:** `self-development/strategy/00_master_plan.md`.

A Phase 1 exit criterion required all six templates to carry a current methodology version stamp. **It was
unmet from the day it was written** — no template ever carried one — and it sat open across every release
since.

The v1.32.0 convention sweep decided to **drop it rather than fulfil it**: a version stamp inside a
template is a copy that goes stale on the adopter's disk, where nothing can refresh it. The stamp belongs
in `SKILL.md` and `CHEATSHEET.md`, which are read *from* the repo, and both already carry one. **The
criterion was asking for exactly the drift v1.32.0 spent its time removing.**

**The reason this is intake's first item is the point.** The sweep made that decision on 2026-08-20 and
nobody executed it — the criterion stayed open in the master plan for five more days while the release it
came from shipped. **A decision recorded and not executed is the same failure as a claim asserted and not
checked**, which is the entire finding class the audit raised. It was too small to charter and had no epic
to belong to, so before this file existed it had nowhere to go except a paragraph in an evaluation that
nothing reads on a schedule.

That is the gap intake closes, demonstrated on the first try rather than argued for.

---

### BL-0059 — Fold architecture-layer routing into failure-layer routing

`Status: done` · `Test: pass` — one ladder, one definition; `grep -rn "architecture-layer"` returns no convention of that name

**Files:** `methodology/07_definition_of_done.md` (−1), `CHEATSHEET.md` (−1).

The v1.32.0 sweep found that "architecture-layer failure routing" (v1.29.0) was not a separate convention —
it is one more rung on the ladder that failure-layer routing (v1.25.0) already defines. **The sweep's
decision was merge, and like the version-stamp criterion it was recorded and not executed.** That is now
twice in one sweep, which is a pattern rather than an oversight.

**The architecture is now the top row of the routing table**, where every other layer already lives, and
the paragraph that sat beside the table describing it as a separate thing is gone. The cascade sentence
generalised from *"an intent- or plan-level finding cancels the code-level findings below it"* to a finding
at **any** layer cancelling those below — which is what the ladder always meant and what the special-cased
paragraph obscured.

**`CHEATSHEET.md` had zero headroom** at 99 against a hard <100 criterion, and it restates the ladder. The
new rung was paid for by merging the block's opening and closing lines rather than by raising the cap —
the file is now **98**, and the corpus carries one fewer named convention than it did this morning.

**Net: −2 lines and −1 concept.** Small, and it is the first change in this project's history whose purpose
was to make the corpus smaller rather than more complete.

---

### BL-0062 — Write the audit brief so commissioning a re-audit is a paste

`Status: done` · `Test: pass` — every SHA, count and finding in the brief was re-derived from the tagged tree, not copied from the changelog

**Files:** `self-development/evaluations/AUDIT_BRIEF.md` (new).

E10's closing gate is a cold re-audit by a session that did not author the fixes, and it has not run.
**Two releases of repair — eleven findings, a lock-semantics rewrite, a destructive-operation
reclassification, a trust-boundary change — are verified by nobody but the sessions that wrote them.**

The obstacle was never willingness; it was that commissioning the audit meant *designing* it first. The
brief removes that: a pinned commit and tree, a paste-able prompt, the twelve rubric dimensions with the
four core ones named, the eleven prior findings with their claimed fixes so they can be checked rather
than believed, and a list of the four failure modes this repo has actually exhibited so an auditor knows
where to look.

**Two instructions in it are deliberately uncomfortable.** *Do not trust the repository's own records* —
including `RELEASE_EVIDENCE.md`, whose commands should be run rather than read. And *do not propose new
conventions*: a project that has shipped sixteen and exercised seven does not need an auditor adding to
the pile, so findings should more often subtract than add.

**It does not run the audit and it is not evidence.** E10 stays `active` until someone else does.

---

### BL-0066 — Provenance for repo-supplied agent config that executes

`Status: done` · `Test: pass` — fresh-context review of the diff (no blocking findings; all seven should-fix applied); pasteable block in root `AGENTS.md` diffs clean against 13's; new anchors resolve

**Files:** `methodology/13_ai_safety_and_prompt_injection.md`, `AGENTS.md`, `templates/AGENTS.md`,
`templates/CLAUDE.md`.

**The clarification was answered yes**: on 2026-09-25 the maintainer directed implementation, which is also
the approval of this item's intent. 13's scope line now says it governs which repo-supplied agent config an
agent lets run, as well as which instructions it obeys.

Trust follows provenance already covered instruction text, *believed* because of where it sits. Agent
config committed to the repo — hook definitions, MCP server lists — is *run* because of where it sits, on the
harness's next event in that tree, before anyone has read the diff. One paragraph beside the provenance
rule, one threat-model row.

**Surface walk, per 00's map:** the pasteable block names agent-config files among those read from the
base commit and gained one line forbidding auto-run (root `AGENTS.md` 56 → 57 of 60, byte-identical to
13's block). Both templates carry it in substance, as "agent-harness" hooks so it cannot be read as
licence to skip the repo's git hooks — which the block separately says never to weaken. `SKILL.md` carries
none of the provenance rule and links to 13, so it is unchanged. **Deliberately not propagated:** 13's
closing advice to adopters (prefer tools that re-ask on config change; keep launch-deciding settings in
user config) — maintainer-level guidance that belongs in one place.

The agent-of-empires README's line asking AI agents to star the project was *not* added to 13 as an
example: 13 has enough examples, and a named third-party repo in a safety doc ages badly.

---

### BL-0067 — Tests that wait on work: no fixed sleeps

`Status: done` · `Test: pass` — fresh-context review found every `Done means` bullet met; `#why-must-fail-first` resolves

**Files:** `methodology/10_testing_and_verification.md`.

Intent approved by the maintainer's direction to implement on 2026-09-25. One subsection under "Automated
tests": wait on an observable condition with a deadline; a deadline bounds failure, it does not establish
completion; before asserting something did not happen, establish that it could have — cross-linked to
"must fail first", whose defect a vacuous negative assertion is.

**Surface walk:** no row in 00's map restates 10's test-writing guidance, so there was no fan-out. No new
enum, gate or checklist field.

---

### BL-0068 — Worktree hygiene gaps in `09`

`Status: done` · `Test: pass` — fresh-context review; its git-semantics corrections (lock scope, locked move, hook exit status, LFS example) applied

**Files:** `methodology/09_git_workflow.md`.

Filed in `FUTURE.md` on 2026-09-25 so three items from one source would not trip the eviction rule;
promoted and closed in the same change when the maintainer directed implementation of all three. It
never sat open in `BACKLOG.md`, so the eviction rule was not engaged.

Five bullets under a new "Creation and cleanup hazards" heading in the worktree section: branch from a
freshly fetched base (with `--no-track`), a failing `post-checkout` hook makes `git worktree add` exit
non-zero although the tree exists, never remove the default branch's checkout in a bare-repo layout,
`git worktree lock` guards only against git itself, and move aside before deleting.

**Review caught a pre-existing error on the way:** the cleanup note placed `worktree remove --force` on the
✗ rows of the operation table; the table has always put it on ⚠ (`approval-gated`). Corrected, and the
new bullet no longer repeats it.
