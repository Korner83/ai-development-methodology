# Examples

This folder shows what an adopter project looks like when it adopts the methodology. Pinned to **v1.28.0**.

## Three artifact types, three purposes

| Folder | Purpose | Read this when |
|---|---|---|
| **[`methodology/`](../methodology/)** | The abstract rules (the *what* and *why*). | Learning the methodology; deciding whether to adopt it. |
| **[`self-development/`](../self-development/)** | The methodology applied to its own development (a real, meta, instance). | Seeing the methodology used on a non-trivial project; understanding how the autonomous loop actually runs. |
| **`examples/`** *(this folder)* | A fully-worked illustrative project (`tinker`, a fictional developer-notes CLI). | Seeing how the abstract docs translate to concrete artifacts on a hypothetical adopter project; lifting patterns directly. |

The three are complementary: read `methodology/` to understand the rules; read `self-development/` to see them on a real project; read `examples/` to see them on a synthetic project that strips out the meta-ness.

## What's in here

- [`example-project/README.md`](example-project/README.md) — the fictional `tinker` project's intro.
- [`example-project/strategy/00_master_plan.md`](example-project/strategy/00_master_plan.md) — strategy doc following the [01_strategy.md](../methodology/01_strategy.md) skeleton.
- [`example-project/pillars/`](example-project/pillars/) — two example pillars following the [02_pillars.md](../methodology/02_pillars.md) skeleton.
- [`example-project/backlog/EPICS.md`](example-project/backlog/EPICS.md) — epic rollup.
- [`example-project/backlog/epics/E01-cli-foundations/`](example-project/backlog/epics/E01-cli-foundations/) — one epic with all 5 standard files (README, BACKLOG, ARCHIVE, FUTURE, TEST) demonstrating the canonical table-form frontmatter from [04_backlog_items.md](../methodology/04_backlog_items.md) and the [03_epics.md "Standard epic-folder structure"](../methodology/03_epics.md#standard-epic-folder-structure).
- [`example-project/backlog/TEST_BACKLOG.md`](example-project/backlog/TEST_BACKLOG.md) — cross-epic manual-QA queue (pairs with each epic's per-epic `TEST.md`).
- [`example-project/backlog/HUMAN_NEEDED.md`](example-project/backlog/HUMAN_NEEDED.md) — the blocked-item protocol in full: BL-0005 is `blocked`, its lock is released, its body carries a `Blocker:` line, and the registry entry says what only a human can decide. Read the three together — the protocol only makes sense as a set.
- [`example-project/backlog/ACTIVE_CONTEXT.md`](example-project/backlog/ACTIVE_CONTEXT.md) — volatile session state, caught mid-item, with an explicit note on what deliberately isn't in it.
- [`example-project/memory/`](example-project/memory/) — the [two-layer memory](../methodology/08_lessons_and_memory.md) with three active entries and one archived. Shows the entry format, a `pinned` entry (a latency budget whose own success makes it look unused), the [admission test](../methodology/08_lessons_and_memory.md#the-admission-test-derivable-from-source-is-never-stored) applied — nothing derivable from the repo is stored — and an [archived entry](example-project/memory/archive/project_editor_precedence.md) showing the healthy retirement path: the lesson became a test, so the entry retired.

## About the fictional project

`tinker` is a deliberately fictional developer-notes CLI. It does not resemble any specific real product — the goal is to be plausible enough that the methodology artifacts look realistic, while generic enough that adopters can map their own project's shape onto it. The example does *not* include working source code; it's docs-only, the same scope this methodology project itself produces.

## Abstract-voice rule

All content in this folder follows the same abstract-voice constraint as the methodology docs themselves: no real product names, no specific company references, no domain jargon revealing a source project. The example was reviewed by a fresh cross-AI session for abstract-voice compliance before ship.
