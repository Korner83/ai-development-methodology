---
name: editor-precedence
description: (Archived 2026-05-24) `$VISUAL` used to take precedence over `$EDITOR`; the special case is gone.
metadata:
  type: project
  status: archived
---

> **Archived 2026-05-24.** Retired because the thing it guarded no longer exists — BL-0003
> standardized on a single resolution order and deleted the special case. Kept for lineage per
> [archive, don't destroy](../../../../methodology/08_lessons_and_memory.md#archive-dont-destroy-the-memory-lifecycle).

`tinker capture` with no argument opens an editor. The original implementation checked `$VISUAL`
first, then `$EDITOR`, then fell back to `vi`.

**Why:** `$VISUAL` vs `$EDITOR` is a genuine POSIX distinction — `$EDITOR` is meant to be usable on
a dumb terminal, `$VISUAL` assumes a full-screen-capable one. Two contributors independently
"simplified" the check down to `$EDITOR` alone, which silently ignored the preference of anyone who
sets both. The entry existed because the code looked redundant and was not.

**How to apply:** *(no longer applicable)* — check `$VISUAL` before `$EDITOR`; do not collapse them.

**What replaced it:** BL-0003 settled on `$VISUAL` → `$EDITOR` → `vi` as documented, tested
behaviour with a test asserting the precedence. The rule now lives in the test, which is the right
home for it: an executable assertion beats a memory entry a contributor has to remember to read.
That transition — memory entry becomes a test, entry gets archived — is the healthy end state for
this kind of lesson.
