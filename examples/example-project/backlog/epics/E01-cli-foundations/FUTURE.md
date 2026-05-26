# E01 — CLI foundations — Future

_P3 / nice-to-have items for this epic. Not scheduled until the active scope is cleared. Uses Scheme B IDs (`BL-E01-F##`) per [04_backlog_items.md "FUTURE.md numbering"](../../../../../methodology/04_backlog_items.md#futuremd-numbering-two-valid-schemes); when promoted to BACKLOG, items are renumbered to monotonic `BL-####`._

## Summary

| ID         | Title                                               | Priority | Effort |
|------------|-----------------------------------------------------|----------|--------|
| BL-E01-F01 | Shell completions (bash/zsh/fish) for `tinker`      | P3       | S      |
| BL-E01-F02 | Color-coded `recent` output (configurable via env)  | P3       | XS     |
| BL-E01-F03 | `tinker --version` checks for newer release         | P3       | S      |

---

### BL-E01-F01 — Shell completions (bash/zsh/fish) for `tinker`

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E01-cli-foundations                |
| Pillar   | P1                                 |
| Priority | P3                                 |
| Effort   | S                                  |
| Status   | future                             |
| Test     | not-tested                         |
| Deps     | BL-0002, BL-0003, BL-0004          |
| Lock     | —                                  |

**Why / Description:** Tab completion improves the CLI experience but is a polish item — only worthwhile after the core commands stabilize. Defer until `capture` + `recent` + `search` (E02) have ship-quality interfaces.

**Files (probable):**

- `completions/tinker.bash`, `completions/_tinker` (zsh), `completions/tinker.fish`
- `Cargo.toml` (add `clap_complete` feature flag)

---

### BL-E01-F02 — Color-coded `recent` output (configurable via env)

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E01-cli-foundations                |
| Pillar   | P1                                 |
| Priority | P3                                 |
| Effort   | XS                                 |
| Status   | future                             |
| Test     | not-tested                         |
| Deps     | BL-0004                            |
| Lock     | —                                  |

**Why / Description:** `tinker recent` output is easier to scan when timestamps + cwd + git branch are color-coded. Respect `NO_COLOR` env var per [no-color.org](https://no-color.org/). Cheap polish but only matters after core retrieval ships.

**Files (probable):**

- `src/recent.rs` (extension)

---

### BL-E01-F03 — `tinker --version` checks for newer release

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E01-cli-foundations                |
| Pillar   | P1                                 |
| Priority | P3                                 |
| Effort   | S                                  |
| Status   | future                             |
| Test     | not-tested                         |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** Optional online-check on `tinker --version` to flag if a newer release exists on the GitHub Releases API. Off by default (privacy + offline-friendly); user opts in via `TINKER_UPDATE_CHECK=1`. Defer until v1.0 is shipping releases regularly.

**Files (probable):**

- `src/cli.rs` (version flag handler)
- `src/update_check.rs` (new)
