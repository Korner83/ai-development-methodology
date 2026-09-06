# Self-development backlog

This is the backlog for the **methodology project's self-development** (the methodology applied to its own development). Follow [`methodology/04_backlog_items.md`](../../methodology/04_backlog_items.md) for the canonical BL-#### format, ROI heuristic, lifecycle, and item rules — everything in this backlog uses that format unchanged.

## Structure

```
self-development/backlog/
├── README.md             # this file
├── EPICS.md              # rollup of all epics with status counts + pillar coverage
├── ACTIVE_CONTEXT.md     # volatile working-state baton
├── FEEDBACK.md           # inbound feedback inbox (untrusted by default)
├── HUMAN_NEEDED.md       # items blocked on human-only action
└── epics/
    ├── E00-intake/        # standing; never closes
    ├── E01-examples-folder/
    │   ├── README.md     # charter
    │   ├── BACKLOG.md    # active items
    │   ├── ARCHIVE.md    # done items
    │   ├── FUTURE.md     # deferred items
    │   └── TEST.md       # epic acceptance + regression scenarios
    ├── E02-first-semiannual-self-evaluation/   # same shape as above
    ├── E03-git-workflow-trim/
    ├── E04-native-tool-templates/
    ├── E05-cheatsheet/
    ├── E06-bmad-v6-landscape-pass/
    ├── E07-agentic-workflow-pass/
    ├── E08-role-briefs/
    ├── E09-external-landscape-pass/
    └── E10-external-audit-remediation/
```

**The five-file shape is the methodology's, per ["Standard epic-folder structure"](../../methodology/03_epics.md).**
This diagram documented four for a long time and the filesystem matched the diagram rather than the
methodology — an external audit caught it (F-09). **All eleven epics carry all five files.** The nine
back-filled `TEST.md` files are empty-but-present and point at the real verification record in each
`ARCHIVE.md`; no acceptance scenarios were reconstructed, because back-filling rows that never ran would
be fabricated evidence. The rule was not weakened to fit the practice.

## ID space

- **Epic IDs:** `E<NN>` (zero-padded). Currently `E00` through `E10`; `E00` is the standing intake epic and does not close. Folder names carry the `E` prefix (`E01-examples-folder`), per "Standard epic-folder structure" in [`03_epics.md`](../../methodology/03_epics.md).
- **Item IDs:** `BL-<####>` monotonic across all epics in this self-development backlog, and shared with `FUTURE.md` items so promotion needs no renumbering. Highest assigned: `BL-0062` (E00, 2026-09-05).

Per the methodology's [project structure convention](../../templates/PROJECT_STRUCTURE.md): item IDs are repo-wide-monotonic within this backlog (so items can move between epics without renumbering and `grep BL-0042` is unambiguous within the self-development backlog).

## Workflow

Standard methodology workflow per [`methodology/04_backlog_items.md`](../../methodology/04_backlog_items.md). Three project-specific overrides:

1. **The autonomous loop MUST NOT modify abstract methodology docs in `methodology/` autonomously.** Cycle outputs that suggest methodology changes are surfaced to the maintainer; methodology updates ship as a normal release cycle. The full constraint set is in [`../AUTONOMOUS_LOOP.md`](../AUTONOMOUS_LOOP.md) "Hard constraints."
2. **All releases that touch `self-development/` ship as minor or patch versions of the public repo** — the work is in the public repo, but it's project-meta work, not methodology work. The abstract methodology in `methodology/` versions independently.
3. **WIP cap is 2 active epics** (not the methodology's typical 3). Raised from 1 on E02's close. See `EPICS.md` "WIP cap note" for reasoning. The cap has still never actually been contended, so there is no evidence for raising it further. **`E00-intake` is exempt** — it is standing rather than chartered, and a permanently-active epic would otherwise eat a slot forever. Declared in its charter as a deviation rather than read into the rule.
4. **Focused mode is dogfooded, not published.** `E00` runs it; [`E00/FUTURE.md`](epics/E00-intake/FUTURE.md) holds the design and the condition that would promote it into `methodology/`. Nothing about it is a published convention yet, deliberately.

## Cross-references

- **Master plan:** [`../strategy/00_master_plan.md`](../strategy/00_master_plan.md) — phases, pillar roadmap, doc index.
- **Pillars:** [`../pillars/`](../pillars/) — P1 through P9 capability layers; each epic charter names its primary pillar.
- **Adoption profile:** [`../ADOPTION_PROFILE.md`](../ADOPTION_PROFILE.md) — what this repo adopted, adapted and omitted, with reasons. Read it before treating this directory as a worked reference.
- **Release evidence:** [`../RELEASE_EVIDENCE.md`](../RELEASE_EVIDENCE.md) — the commands behind every published count, and the line budgets that bind this repo.
- **Methodology:** the abstract docs being applied here live at [`../../methodology/`](../../methodology/). They are read-only from this backlog's perspective unless the maintainer explicitly authorizes a methodology change in a separate release cycle.

## Status

Bootstrapped on 2026-05-25; the bootstrap completed long ago. As of 2026-09-05: eleven epics, eight done, one parked (E04, will not resume), one active (E10), one standing (E00 intake). Item IDs run to `BL-0062`. The live rollup is [`EPICS.md`](EPICS.md) — this section records origin, not current state.

**This paragraph was stale by two epics, twenty-two item IDs and a WIP cap when an external audit read it.** It is the second-order form of the finding E10 exists to fix: a hand-maintained record drifts, and nothing notices until someone outside reads it. **No check will catch the next one** — a committed checker was declined — so the only defences are that this section says what it is (origin, not current state), that it points at the file that is, and that [`../RELEASE_EVIDENCE.md`](../RELEASE_EVIDENCE.md) makes the counts reproducible by anyone who cares to look.
