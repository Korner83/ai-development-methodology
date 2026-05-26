# E01 — CLI foundations — Archive

_Completed and rejected items for this epic. Historical record only — never edit past entries._

## Summary

| ID      | Title                                | Status | Closed       |
|---------|--------------------------------------|--------|--------------|
| BL-0001 | Scaffold project + CI for 3 OS       | done   | (fictional)  |

---

### BL-0001 — Scaffold project + CI for 3 OS

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E01-cli-foundations                |
| Pillar   | P1                                 |
| Priority | P0                                 |
| Effort   | M                                  |
| Status   | done                               |
| Test     | pass                               |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** Without project scaffolding + CI for all 3 target OS (macOS, Linux, Windows), no subsequent item could claim cross-platform correctness. Foundation item.

**Approach:**
1. `cargo new tinker` (Rust per strategy doc 02 — fictional).
2. GitHub Actions workflow: matrix build on `ubuntu-latest`, `macos-latest`, `windows-latest`.
3. Test runner: `cargo test` on all 3.

**Done means:**

- [x] Repo skeleton committed.
- [x] CI runs green on all 3 OS for the placeholder test.
- [x] README explains how to run tests locally.

**Files:**

- `Cargo.toml`, `src/main.rs`, `.github/workflows/ci.yml`, `README.md`.

**Closure note:** First item shipped in the epic; established the multi-OS CI baseline every subsequent item now depends on.
