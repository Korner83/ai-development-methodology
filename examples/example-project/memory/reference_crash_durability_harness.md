---
name: crash-durability-harness
description: When writing or changing a durability test — how the 100-simulated-crash run works and why it kills the process rather than mocking.
metadata:
  type: reference
---

The durability guarantee ("zero notes lost") is tested by **killing a real child process
mid-write, 100 times**, not by mocking a failed write. The harness lives in
`tests/storage_crash.rs` and is described in the epic's
[TEST.md](../backlog/epics/E01-cli-foundations/TEST.md).

Shape of the run: spawn `tinker capture` as a child, `SIGKILL` it at a randomized offset inside the
write window, then reopen the store and assert every acknowledged note is present and parseable.

**Why:** a mocked write failure tests the error branch the author *imagined*. The failure this
product actually has to survive is the laptop lid closing mid-capture — partial writes, torn
records, an fsync that never returned. Only a real kill produces those states, and they are exactly
the states that turn "capture is free" into "capture ate my note." `SIGKILL` specifically, because
anything catchable lets cleanup code run that will not run in the real failure.

**How to apply:** when adding a durability test, extend this harness rather than writing a mocked
sibling — a second, weaker durability test that passes is worse than none, because it makes the
suite look like it covers the case. If the storage backend changes (see
[storage-backend-pending](project_storage_backend_pending.md)), the harness survives: it asserts
against the public read surface, not the on-disk format.

**Prior art:** the kill-and-reopen pattern is standard practice for embedded-store durability
suites; SQLite's own test corpus is the canonical public reference if you need to extend the
failure-injection points beyond a randomized offset.
