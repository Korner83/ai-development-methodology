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
