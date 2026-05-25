# Self-development backlog

This is the backlog for the **methodology project's self-development** (the methodology applied to its own development). Follow [`methodology/04_backlog_items.md`](../../methodology/04_backlog_items.md) for the canonical BL-#### format, ROI heuristic, lifecycle, and item rules — everything in this backlog uses that format unchanged.

## Structure

```
self-development/backlog/
├── README.md             # this file
├── EPICS.md              # rollup of all epics with status counts + pillar coverage
├── HUMAN_NEEDED.md       # items blocked on human-only action
└── epics/
    ├── 01-examples-folder/
    │   ├── README.md     # charter
    │   ├── BACKLOG.md    # active items (populated in Step 3)
    │   ├── ARCHIVE.md    # done items (created when first item closes)
    │   └── FUTURE.md     # deferred items (created when first deferral happens)
    ├── 02-first-semiannual-self-evaluation/
    │   └── README.md (and same shape as above)
    ├── 03-git-workflow-trim/
    ├── 04-native-tool-templates/
    └── 05-cheatsheet/
```

## ID space

- **Epic IDs:** `E<NN>` (zero-padded). Currently `E01` through `E05`.
- **Item IDs:** `BL-<####>` monotonic across all epics in this self-development backlog. Starts at `BL-0001` when Step 3 populates items.

Per the methodology's [project structure convention](../../templates/PROJECT_STRUCTURE.md): item IDs are repo-wide-monotonic within this backlog (so items can move between epics without renumbering and `grep BL-0042` is unambiguous within the self-development backlog).

## Workflow

Standard methodology workflow per [`methodology/04_backlog_items.md`](../../methodology/04_backlog_items.md). Two project-specific overrides:

1. **The autonomous loop (when active, after Step 4 of the bootstrap) MUST NOT modify abstract methodology docs in `methodology/` autonomously.** Cycle outputs that suggest methodology changes are surfaced to the maintainer; methodology updates ship as a normal release cycle.
2. **All releases that touch `self-development/` ship as minor or patch versions of the public repo** — the work is in the public repo, but it's project-meta work, not methodology work. The abstract methodology in `methodology/` versions independently.

## Cross-references

- **Master plan:** [`../strategy/00_master_plan.md`](../strategy/00_master_plan.md) — phases, pillar roadmap, doc index.
- **Pillars:** [`../pillars/`](../pillars/) — P1 through P9 capability layers; each epic charter names its primary pillar.
- **Methodology:** the abstract docs being applied here live at [`../../methodology/`](../../methodology/). They are read-only from this backlog's perspective unless the maintainer explicitly authorizes a methodology change in a separate release cycle.

## Status

Bootstrapped on 2026-05-25 as Step 2 of the self-development plan. Step 3 (item population in each epic's `BACKLOG.md`) is the next gate.
