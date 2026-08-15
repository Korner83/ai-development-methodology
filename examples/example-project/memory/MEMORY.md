# Memory index

One line per entry. Read on every session; the hook says *when* the entry matters, so a contributor
can decide from this list alone whether to open it. Format and discipline:
[`08_lessons_and_memory.md`](../../../methodology/08_lessons_and_memory.md).

Every entry here passed the [admission test](../../../methodology/08_lessons_and_memory.md#the-admission-test-derivable-from-source-is-never-stored):
none of it is derivable by reading the repo. The crate layout, the `clap` version, and the test
command are all absent on purpose — a contributor reads those live.

## Active

- [Capture path is latency-critical](feedback_capture_path_latency.md) — before adding *anything* to the `tinker capture` code path. **Pinned.**
- [Storage backend is deliberately undecided](project_storage_backend_pending.md) — before touching `src/storage.rs` or anything that writes a note.
- [Crash-durability harness](reference_crash_durability_harness.md) — when writing or changing a durability test.

## Archived

Kept for lineage, dropped from the live index. See [`archive/`](archive/).

- ~~[`$VISUAL` took precedence over `$EDITOR`](archive/project_editor_precedence.md)~~ — retired 2026-05-24; the special case it guarded no longer exists.
