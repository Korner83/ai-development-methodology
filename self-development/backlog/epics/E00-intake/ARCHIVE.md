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
