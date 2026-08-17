# ACTIVE_CONTEXT.md — volatile working state

**Baton, not journal.** Where the current session is, so the next one — or this one after a
context reset — can resume without re-deriving state from scratch. Per
[`methodology/08_lessons_and_memory.md` "Active context"](../../methodology/08_lessons_and_memory.md#active-context-the-volatile-working-file):
written *before* a context reset, read *first* on resume, then **verified against live `git log`
and item state**, which are authoritative when they disagree with this file.

Overwritten, not appended. The durable record lives in commits, `ARCHIVE.md`, and memory.
If a line here is worth keeping, it belongs in one of those instead.

_Last updated: 2026-08-14 — after E03 closed (v1.27.0)._

## Current focus

Nothing in flight. **No active epic**, no open items in any epic, working tree clean.
Three releases shipped today: v1.25.0, v1.26.0, v1.27.0.

## Recent changes (this session)

- **v1.25.0** (PR #22): Code Map, frozen intent, failure-layer routing, verification-gap
  question, size budgets. E06 chartered → executed → closed.
- **v1.26.0** (PR #23): memory admission test; post-v1.25 consistency; `FEEDBACK.md` +
  `ACTIVE_CONTEXT.md` instantiated; six stale anchors fixed; `STATUS.md`'s false
  direct-to-main claim retired.
- **v1.27.0**: E03 closed — `09_git_workflow.md` trimmed 1,026 → 798 lines (−22%), trim chosen
  over split, zero content lost, one anchor renamed and three inbound links repaired.
- Repo hygiene: `main` synced, all stale worktrees and merged branches removed.

## Next steps

The backlog is no longer the binding constraint — the milestone is.

1. **Publish the distribution drafts** — top entry in [HUMAN_NEEDED.md](HUMAN_NEEDED.md) and the
   sole blocker on closed beta (adopter discoverability 6/10 decides the verdict under *no area
   averaged away*). **Maintainer-only**; no agent should do this.
2. **The backlog is empty** — zero active, zero planned. E04 (native Cursor/Aider/Continue.dev
   templates) was parked by maintainer decision on 2026-08-14: `AGENTS.md` + adaptation is the
   permanent answer. Chartering new work is now a deliberate act, not picking the next queued
   thing; the loop should halt and surface rather than promoting anything itself.
3. **Four Tier-2 deferrals** remain in
   [E06's FUTURE.md](epics/E06-bmad-v6-landscape-pass/FUTURE.md).
4. **Semi-annual self-evaluation due 2026-11-25** — it should check whether the v1.25.0–v1.27.0
   conventions are actually being used or have become dead text.

## Watch out for

- **Check `origin/main` before branching.** This session lost time to a stale local `main`:
  v1.24.0 had merged while work was in flight, which collided on the version number and on two
  files. Rebase-and-renumber cost more than the fetch would have.
- **The version number is claimed in four places** (`README.md` badge, two prose lines,
  `CHEATSHEET.md` pin) plus the `CHANGELOG` heading. Missing one is the easy error.

## Not here on purpose

Durable lessons (the stale-`main` one above is a candidate for a memory entry), decisions with
lasting force, and anything another session would need *after* this work ships. Those go to
`memory/`, the changelog, or the item body — not to a file that gets overwritten.
