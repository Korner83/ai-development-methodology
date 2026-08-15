---
name: storage-backend-pending
description: Before touching `src/storage.rs` or anything that writes a note — the backend choice is deliberately unresolved and is a human decision.
metadata:
  type: project
  status: active
---

The note-storage backend is **not chosen yet**, and that is deliberate. The open question is
SQLite vs. plain JSONL files, tracked on
[BL-0005](../backlog/epics/E01-cli-foundations/BACKLOG.md) and registered in
[`HUMAN_NEEDED.md`](../backlog/HUMAN_NEEDED.md).

The trade-off in one line: **SQLite** buys richer `recent` and search queries — which is most of
[P2 — Retrieval](../pillars/P2_retrieval.md) — at the cost of a C dependency inside a CLI whose
distribution promise is a one-line install. **JSONL** keeps the install trivial and makes P2
meaningfully harder.

**Why:** this is a durable architecture commitment with a real migration cost once notes exist in
the wild, and it trades a *distribution promise* against a *query capability*. Those are product
decisions, not engineering ones — an agent has no basis to rank them, and the failure mode is
quiet: an agent that "just picks one to unblock itself" produces working code that silently
forecloses the decision. The item is blocked rather than in-progress precisely so that can't happen.

**How to apply:** do not choose. If work requires the storage layer, route it through the
`write` / `read_by_cwd` / `read_all` surface BL-0005 defines and keep the backend behind it — that
surface is what makes the eventual decision cheap. If a task appears to *need* the decision made,
that task is blocked too: say so and pick something else.

**Retire this entry when the decision lands** — at that point the thing it guards is gone, the
rationale belongs in an architecture note, and this becomes archivable.
