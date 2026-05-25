# `tinker` — Strategy Master Plan

_Fictional adopter strategy doc. Demonstrates the [01_strategy.md](../../../methodology/01_strategy.md) skeleton._

## Vision (one sentence)

A command-line tool that makes capturing developer notes as low-friction as a `git commit` — so context that would normally be lost gets preserved, retrievable, and tied to the work it described.

## Audience

**Primary:** solo developers who already use the command line for most of their workflow. They want a tool that fits where they already are, not another app to switch to.

**Anti-audience:** team-collaboration users who want shared notes with permissions, threading, and a web UI. `tinker` is single-user only by design; team-shared notes is a different product.

## Business outcomes

- Free, open-source, MIT.
- Funded by maintainer's other work; no monetization plan in v1.
- Success = adoption count, not revenue. KPI: 1,000 weekly active installs by 6 months post-public-launch.

## Phases

### Phase 1 — Foundation (current → 3 months)

**Goal:** working CLI with the core capture + retrieval flow.

**Exit criteria (binary):**

- [ ] `tinker capture` writes a note to local store; survives reboot.
- [ ] `tinker recent` retrieves the last N notes for the current directory.
- [ ] `tinker search <query>` returns matching notes ranked by recency.
- [ ] Install is one command on macOS, Linux, Windows (3 OS minimum).
- [ ] Test suite covers capture + retrieval + search; CI green on all 3 OS.

### Phase 2 — Polish (3–6 months)

**Goal:** ship to closed beta of trusted developers; collect feedback; reach open-beta-ready quality.

**Exit criteria (binary):**

- [ ] Calendar-event integration works on macOS (calendar API). Windows + Linux integrations deferred to Phase 3.
- [ ] Notes link to git commits when in a repo.
- [ ] Closed beta of ≥ 5 trusted developers; ≥ 80% would recommend.
- [ ] Crash rate < 0.5% over a 30-day window.
- [ ] Milestone deep-eval scores ≥ 9 average across all areas (UX, perf, content quality, docs, test coverage, security).

### Phase 3 — Open beta (6–9 months)

**Goal:** public on package managers; gather organic adoption signal.

**Exit criteria (binary):**

- [ ] Available on Homebrew, Apt, Cargo, Chocolatey.
- [ ] One blog post + Show HN.
- [ ] 100 weekly-active installs measured.
- [ ] ≥ 3 community contributors landed.

### Phase 4 — v1.0 (12 months target)

**Goal:** declare v1 (drop "beta" label); commit to stability + support cadence.

**Exit criteria (binary):**

- [ ] All P0/P1 items from beta closed.
- [ ] Documentation complete; setup time < 5 minutes for a new user.
- [ ] 500 weekly-active installs.
- [ ] Milestone deep-eval scores ≥ 9 average, no area below 8.

## Document index

| # | Doc | Purpose |
|---|---|---|
| 00 | [Master plan](00_master_plan.md) | This file — vision, phases, doc index. |
| 01 | _(not yet authored)_ Market research | Survey of existing developer-notes tools; differentiation. |
| 02 | _(not yet authored)_ Tech stack | Language choice (Rust), distribution mechanics. |
| 03 | _(not yet authored)_ Privacy + data handling | Where notes live; what gets sent off-device (nothing in v1). |

## Re-evaluation

Cadence: at every phase exit + when a Phase exit criterion isn't met within 50% of the target window.

## Version history

| Version | Date | Notes |
|---|---|---|
| v1.0 | (fictional date) | Initial strategy doc. |
