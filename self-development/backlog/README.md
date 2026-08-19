# Self-development backlog

This is the backlog for the **methodology project's self-development** (the methodology applied to its own development). Follow [`methodology/04_backlog_items.md`](../../methodology/04_backlog_items.md) for the canonical BL-#### format, ROI heuristic, lifecycle, and item rules — everything in this backlog uses that format unchanged.

## Structure

```
self-development/backlog/
├── README.md             # this file
├── EPICS.md              # rollup of all epics with status counts + pillar coverage
├── HUMAN_NEEDED.md       # items blocked on human-only action
└── epics/
    ├── E01-examples-folder/
    │   ├── README.md     # charter
    │   ├── BACKLOG.md    # active items
    │   ├── ARCHIVE.md    # done items
    │   └── FUTURE.md     # deferred items
    ├── E02-first-semiannual-self-evaluation/   # same shape as above
    ├── E03-git-workflow-trim/
    ├── E04-native-tool-templates/
    ├── E05-cheatsheet/
    ├── E06-bmad-v6-landscape-pass/
    ├── E07-agentic-workflow-pass/
    └── E08-role-briefs/
```

## ID space

- **Epic IDs:** `E<NN>` (zero-padded). Currently `E01` through `E08`. Folder names carry the `E` prefix (`E01-examples-folder`), per "Standard epic-folder structure" in [`03_epics.md`](../../methodology/03_epics.md).
- **Item IDs:** `BL-<####>` monotonic across all epics in this self-development backlog, and shared with `FUTURE.md` items so promotion needs no renumbering. Highest assigned: `BL-0033` (E08, v1.30.0).

Per the methodology's [project structure convention](../../templates/PROJECT_STRUCTURE.md): item IDs are repo-wide-monotonic within this backlog (so items can move between epics without renumbering and `grep BL-0042` is unambiguous within the self-development backlog).

## Workflow

Standard methodology workflow per [`methodology/04_backlog_items.md`](../../methodology/04_backlog_items.md). Three project-specific overrides:

1. **The autonomous loop MUST NOT modify abstract methodology docs in `methodology/` autonomously.** Cycle outputs that suggest methodology changes are surfaced to the maintainer; methodology updates ship as a normal release cycle. The full constraint set is in [`../AUTONOMOUS_LOOP.md`](../AUTONOMOUS_LOOP.md) "Hard constraints."
2. **All releases that touch `self-development/` ship as minor or patch versions of the public repo** — the work is in the public repo, but it's project-meta work, not methodology work. The abstract methodology in `methodology/` versions independently.
3. **WIP cap is 1 active epic** (not the methodology's typical 3). See `EPICS.md` "WIP cap note" for reasoning. The cap rises after epics close and the maintainer observes the loop's behavior.

## Cross-references

- **Master plan:** [`../strategy/00_master_plan.md`](../strategy/00_master_plan.md) — phases, pillar roadmap, doc index.
- **Pillars:** [`../pillars/`](../pillars/) — P1 through P9 capability layers; each epic charter names its primary pillar.
- **Methodology:** the abstract docs being applied here live at [`../../methodology/`](../../methodology/). They are read-only from this backlog's perspective unless the maintainer explicitly authorizes a methodology change in a separate release cycle.

## Status

Bootstrapped on 2026-05-25; the bootstrap completed long ago. As of v1.30.0: eight epics chartered, six done, one parked (E04, will not resume), one active (E08). Item IDs run to `BL-0033`. The live rollup is [`EPICS.md`](EPICS.md) — this section records origin, not current state.
