# E01 — CLI foundations — Active Backlog

_4 example items demonstrating the canonical [04_backlog_items.md](../../../../../methodology/04_backlog_items.md) frontmatter shape. (BL-0001 already shipped — see [ARCHIVE.md](ARCHIVE.md).)_

## Summary

| ID      | Title                                                   | Priority | Effort | Status      |
|---------|---------------------------------------------------------|----------|--------|-------------|
| BL-0002 | `tinker capture "<text>"` writes note + auto-attaches context | P1       | M      | in-progress |
| BL-0003 | `tinker capture` (no arg) opens `$EDITOR`               | P1       | S      | ready       |
| BL-0004 | `tinker recent` lists last 20 for cwd                   | P1       | S      | backlog     |
| BL-0005 | Note storage format finalized (durability + schema)     | P0       | M      | blocked     |

---

### BL-0002 — `tinker capture "<text>"` writes note + auto-attaches context

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E01-cli-foundations                |
| Pillar   | P1                                 |
| Priority | P1                                 |
| Effort   | M                                  |
| Status   | in-progress                        |
| Test     | not-tested                         |
| Deps     | BL-0001, BL-0005                   |
| Lock     | claude-sess-9d12@2026-05-25T18:00Z |

**Why / Description:** Core capture command. Writes a note with auto-attached context (cwd, git branch if applicable). Foundation for the entire P1 capability.

**Approach:**
1. Parse arg(s) with `clap`.
2. Detect cwd + git branch (if any) via `std::env` + shelling to `git symbolic-ref`.
3. Write to the note store from BL-0005's schema.
4. Return in < 300ms (KPI).

**Done means:**

- [ ] Capture command exists and writes a note durably.
- [ ] Context auto-attached (cwd + git branch where applicable).
- [ ] p95 latency < 300ms on test machine.
- [ ] Test exercises the capture + the durability across simulated crash.

**Files (probable):**

- `src/cli.rs`, `src/capture.rs`, `tests/capture.rs`.

---

### BL-0003 — `tinker capture` (no arg) opens `$EDITOR`

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E01-cli-foundations                |
| Pillar   | P1                                 |
| Priority | P1                                 |
| Effort   | S                                  |
| Status   | ready                              |
| Test     | not-tested                         |
| Deps     | BL-0002                            |
| Lock     | —                                  |

**Why / Description:** Multi-line notes need an editor; not every note fits in a single CLI arg.

**Approach:** Spawn `$EDITOR` (default `vi`) with a temp file; on editor exit, read the temp file as the note body. Same auto-context attachment as BL-0002.

**Done means:**

- [ ] No-arg invocation opens `$EDITOR`.
- [ ] Editor exit with non-empty file → note captured.
- [ ] Editor exit with empty file → command exits without saving (no empty notes).
- [ ] Test exercises the flow with a stub editor.

**Files (probable):**

- `src/capture.rs` (extension), `tests/capture_editor.rs`.

---

### BL-0004 — `tinker recent` lists last 20 for cwd

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E01-cli-foundations                |
| Pillar   | P1                                 |
| Priority | P1                                 |
| Effort   | S                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | BL-0002                            |
| Lock     | —                                  |

**Why / Description:** Smallest retrieval surface — proves the capture/retrieval round-trip works before E02's full search lands.

**Approach:** Query the note store by cwd; order by timestamp desc; return last 20. Terminal-format the output (with date + preview).

**Done means:**

- [ ] `tinker recent` returns last 20 for current directory.
- [ ] Output is readable in terminal AND pipe-friendly (newline-separated when stdout is a pipe).
- [ ] Test exercises the flow with seed data.

**Files (probable):**

- `src/recent.rs`, `tests/recent.rs`.

---

### BL-0005 — Note storage format finalized (durability + schema)

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E01-cli-foundations                |
| Pillar   | P1                                 |
| Priority | P0                                 |
| Effort   | M                                  |
| Status   | blocked                            |
| Test     | not-tested                         |
| Deps     | —                                  |
| Lock     | —                                  |

**Blocker:** Maintainer decision needed on storage backend: SQLite (richer queries, but C dependency) vs. plain JSONL files (no deps, but harder search). Logged in `backlog/HUMAN_NEEDED.md`.

**Why / Description:** Storage format is the contract between P1 (Capture) and P2 (Retrieval). It must be decided before either feature can fully ship. Schema lock-in early prevents later painful migrations.

**Approach:**

1. Maintainer picks backend (SQLite vs JSONL).
2. Author the schema: `note_id`, `text`, `timestamp`, `cwd`, `git_branch`, `calendar_event` (nullable).
3. Document the schema in `docs/storage.md`.
4. Build a thin storage layer that other items consume.

**Done means:**

- [ ] Storage backend chosen + documented.
- [ ] Schema documented.
- [ ] Storage layer implemented with: write, read-by-cwd, read-all.
- [ ] Tests: 100 simulated crashes; zero notes lost.

**Files (probable):**

- `docs/storage.md` (new), `src/storage.rs` (new), `tests/storage_crash.rs`.
