# HUMAN_NEEDED.md

Tasks blocked on human action. Each entry links to the originating BL item. Add an entry when you
set `Status: blocked` and the blocker is human-only — not waiting on another agent, not waiting on a
dependency an agent can resolve.

Per the [methodology pattern](../../../methodology/04_backlog_items.md#human_neededmd--work-blocked-on-human-agency),
this is a **passive registry**: items land here via the blocked-item protocol, the human scans it
when they check in, and the agent moves on to the next ready item instead of holding a lock.

## Active

- [BL-0005](epics/E01-cli-foundations/BACKLOG.md#bl-0005--note-storage-format-finalized-durability--schema)
  — **pick the storage backend: SQLite or JSONL.** Human-only because it is a durable architecture
  commitment with a migration cost, not a coding task: SQLite buys richer `recent`/search queries at
  the price of a C dependency in a "one-line install" CLI; JSONL keeps the install trivial and makes
  P2 retrieval harder. The agent has written up both sides in the item body and has no basis to
  choose between a distribution promise and a query capability. Blocks BL-0002 (which writes through
  the storage layer). Added 2026-05-22.

## Recently unblocked (last 30 days)

- ~~[BL-0001]~~ — approve the crate name `tinker` on the package registry before the first publish.
  Done 2026-05-18; item resumed and shipped.

_(Older unblocked items live in their epic's `ARCHIVE.md`.)_

## What does NOT belong here

- Items blocked on another agent's work — that is the `Deps:` field plus the lock.
- Items an agent could unblock by reading the repo or asking one clarifying question.
- Long-form context. One line plus the link; the reasoning lives in the item body.
