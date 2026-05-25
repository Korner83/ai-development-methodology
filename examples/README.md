# Examples

This folder shows what an adopter project looks like when it adopts the methodology. Pinned to **v1.15.0**.

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
- [`example-project/backlog/epics/01-cli-foundations/`](example-project/backlog/epics/01-cli-foundations/) — one epic charter + 5 BL items in the canonical table-form frontmatter from [04_backlog_items.md](../methodology/04_backlog_items.md).

## About the fictional project

`tinker` is a deliberately fictional developer-notes CLI. It does not resemble any specific real product — the goal is to be plausible enough that the methodology artifacts look realistic, while generic enough that adopters can map their own project's shape onto it. The example does *not* include working source code; it's docs-only, the same scope this methodology project itself produces.

## Abstract-voice rule

All content in this folder follows the same abstract-voice constraint as the methodology docs themselves: no real product names, no specific company references, no domain jargon revealing a source project. The example was reviewed by a fresh cross-AI session for abstract-voice compliance before ship.
