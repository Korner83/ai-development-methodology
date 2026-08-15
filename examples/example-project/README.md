# `tinker` — example adopter project

_Fictional. Generated as a worked example of the [AI Development Methodology](../../methodology/) applied to a project from scratch. Not a real product._

## What `tinker` is

A small command-line utility for capturing developer notes during coding sessions. Notes are associated with a working directory + a calendar event (when one is in progress). Built for solo developers who want a low-friction way to log context that would otherwise be lost.

**Target user:** an individual developer; not a team product.

**Distribution:** open-source CLI on package managers; one-line install.

**Business model:** free, MIT-licensed; no paid tier in v1.

## How `tinker` adopts the methodology

The artifacts under this folder match the methodology's prescribed shape:

| Methodology layer | `tinker`'s instance |
|---|---|
| Strategy master plan | [strategy/00_master_plan.md](strategy/00_master_plan.md) |
| Pillars | [pillars/P1_capture.md](pillars/P1_capture.md), [pillars/P2_retrieval.md](pillars/P2_retrieval.md) |
| Epic rollup | [backlog/EPICS.md](backlog/EPICS.md) |
| First epic charter | [backlog/epics/E01-cli-foundations/README.md](backlog/epics/E01-cli-foundations/README.md) |
| Active items in that epic | [backlog/epics/E01-cli-foundations/BACKLOG.md](backlog/epics/E01-cli-foundations/BACKLOG.md) (4 items) |
| Archived items | [backlog/epics/E01-cli-foundations/ARCHIVE.md](backlog/epics/E01-cli-foundations/ARCHIVE.md) (1 done item — BL-0001) |
| Deferred (P3) items | [backlog/epics/E01-cli-foundations/FUTURE.md](backlog/epics/E01-cli-foundations/FUTURE.md) (3 items using Scheme B IDs `BL-E01-F##`) |
| Epic acceptance + regression tests | [backlog/epics/E01-cli-foundations/TEST.md](backlog/epics/E01-cli-foundations/TEST.md) |
| Cross-epic manual-QA queue | [backlog/TEST_BACKLOG.md](backlog/TEST_BACKLOG.md) |
| Work blocked on human agency | [backlog/HUMAN_NEEDED.md](backlog/HUMAN_NEEDED.md) (1 active — the storage-backend decision blocking BL-0005) |
| Volatile session state | [backlog/ACTIVE_CONTEXT.md](backlog/ACTIVE_CONTEXT.md) (mid-item on BL-0002) |
| Lessons-learned memory | [memory/MEMORY.md](memory/MEMORY.md) + 3 active entries + 1 archived |

This is the minimum-viable set for an adopter to see the methodology operationalized. A real adopter project would add more pillars, more epics, more items as the project grew; this example shows the starting shape.

Conventions worth looking at specifically, because they are easier to copy than to describe:

- **[Code Maps](../../methodology/04_backlog_items.md#the-code-map--writing-m-items-for-cold-handoff)** on the two Effort-M items (BL-0002, BL-0005) — annotated paths, the utility to reuse, and the constraint that isn't obvious from the code. The S/XS items keep a plain `Files (probable):` list, which is the point: the upgrade is keyed to effort, not applied everywhere.
- **[Frozen intent](../../methodology/04_backlog_items.md#frozen-intent--approved-goals-are-human-owned)** markers on BL-0002 and on the E01 charter — the approved goal and criteria are human-owned; everything else in the body stays editable.
- **The blocked-item protocol, end to end.** BL-0005 is `blocked` with `Lock: —` released, a `Blocker:` line in the body, and a matching entry in [`HUMAN_NEEDED.md`](backlog/HUMAN_NEEDED.md) — so the agent moved on instead of sitting on a lock waiting for a decision it can't make. Trace those three files together; the protocol only makes sense as a set.
- **[Memory](memory/MEMORY.md), including what does *not* go in it.** Three active entries and one archived. Every entry passes the [admission test](../../methodology/08_lessons_and_memory.md#the-admission-test-derivable-from-source-is-never-stored) — nothing derivable from reading the repo. One is `pinned` (the latency budget: its own success makes it look unused, which is why sweeps must not archive it), and the [archived one](memory/archive/project_editor_precedence.md) shows the healthy end state — the lesson became a test, so the entry retired.
- **[Active context](backlog/ACTIVE_CONTEXT.md)** caught mid-item: what a session would need to resume BL-0002 without re-deriving it, and an explicit note on what deliberately isn't there.

## Things NOT included (intentionally)

- **Source code.** This is docs-only; a real adopter would have `src/`, `tests/`, etc. alongside. The paths in the Code Maps and memory entries refer to files that don't exist here.
- **CHANGELOG / README of the project itself.** A real adopter would have these; we showed only the methodology artifacts.
- **Project instruction file** (`CLAUDE.md` / `AGENTS.md`). A real adopter starts from [`templates/`](../../templates/); reproducing one here would just be the template with `tinker` substituted in.
- **`FEEDBACK.md`.** Deliberate: `tinker` is pre-alpha with no users, and the [triage flow](../../methodology/12_milestone_evaluation.md#the-feedback-triage-flow) only becomes load-bearing at alpha and beyond. An empty inbox would demonstrate the file, not the practice.
- **Full backlog.** 5 items in one epic; a real project would have 30+ items across multiple epics.

## Methodology version

Built against methodology **v1.28.0**.
