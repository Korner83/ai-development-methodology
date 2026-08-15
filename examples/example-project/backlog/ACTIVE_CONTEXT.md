# ACTIVE_CONTEXT.md

**Baton, not journal.** Volatile session state so a resumed or fresh session doesn't re-derive it.
Written *before* a context reset, read *first* on resume — then verified against live `git log` and
item state, which win whenever they disagree with this file. Overwritten, not appended. Format:
[`08_lessons_and_memory.md`](../../../methodology/08_lessons_and_memory.md#active-context-the-volatile-working-file).

_Last updated: 2026-05-23._

## Current focus

[BL-0002](epics/E01-cli-foundations/BACKLOG.md) — `tinker capture "<text>"` with auto-attached
context. Lock held by `claude-sess-9d12`, expires 2026-05-25T18:00Z.

## Recent changes

- Arg parsing done via `clap` derive, following the `recent` subcommand's pattern.
- cwd detection working; git-branch detection working *inside* a repo.

## Next steps

1. Make branch detection degrade to `None` outside a git repo — currently it errors, which fails
   the item's third acceptance criterion.
2. Write the capture test, including the cold p95 measurement.

## Blocked on

Nothing right now — but the write path is a stub against BL-0005's storage layer, which is
[blocked on a human decision](HUMAN_NEEDED.md). BL-0002 can be finished and tested against the
stub; it cannot be marked `done` until the real layer exists.

## Watch out for

- **The 300ms cold budget** is easy to blow from this item specifically, since everything here runs
  on the capture path. See the pinned memory entry
  [capture-path-latency](../memory/feedback_capture_path_latency.md) before adding anything inline.

## Not here on purpose

Durable lessons (they go to [`memory/`](../memory/MEMORY.md)), decisions with lasting force (the
item body or an architecture note), and anything the *next* contributor needs after this item
closes. This file gets overwritten; none of that would survive.
