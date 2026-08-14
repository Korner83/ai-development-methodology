# ACTIVE_CONTEXT.md — volatile working state

**Baton, not journal.** Where the current session is, so the next one — or this one after a
context reset — can resume without re-deriving state from scratch. Per
[`methodology/08_lessons_and_memory.md` "Active context"](../../methodology/08_lessons_and_memory.md#active-context-the-volatile-working-file):
written *before* a context reset, read *first* on resume, then **verified against live `git log`
and item state**, which are authoritative when they disagree with this file.

Overwritten, not appended. The durable record lives in commits, `ARCHIVE.md`, and memory.
If a line here is worth keeping, it belongs in one of those instead.

_Last updated: 2026-08-14 — after v1.25.0 merged._

## Current focus

Post-v1.25.0 consistency pass on branch `docs/post-v1.25-consistency`: closing the gaps the
release itself opened (repo content that predates the new conventions) plus the two files the
methodology specifies but this repo never instantiated.

## Recent changes (this session)

- **v1.25.0 merged** (`b9a68dd`, PR #22): Code Map, frozen intent, failure-layer routing,
  verification-gap question, size budgets. Epic E06 chartered → executed → closed.
- `main` synced, three stale worktrees and two merged branches removed.
- Six stale cross-doc anchors fixed; repo-wide anchor check is clean.
- Examples project brought up to the Code Map rule and now demonstrates frozen intent.

## Next steps

Consistency pass is complete and cut as **v1.26.0**; the PR is the last step of this session.
What is genuinely next, for whoever picks this up:

1. **Publish the distribution drafts** — now the top entry in
   [HUMAN_NEEDED.md](HUMAN_NEEDED.md), and the only thing holding the closed-beta milestone.
   Maintainer-only; no agent should do this.
2. **E03** (`09_git_workflow.md` trim/split) is the one active epic — BL-0011 decides
   trim-vs-split, and BL-0012 is maintainer-authored (T2) with a Code Map now in place.
3. **Four Tier-2 deferrals** remain in
   [E06's FUTURE.md](epics/E06-bmad-v6-landscape-pass/FUTURE.md); BL-0021 was promoted out of
   that list in v1.26.0.
4. **Semi-annual self-evaluation due 2026-11-25** — it should specifically check whether the
   v1.25.0/v1.26.0 conventions are actually being used or have become dead text.

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
