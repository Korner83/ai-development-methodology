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
| First epic charter | [backlog/epics/01-cli-foundations/README.md](backlog/epics/01-cli-foundations/README.md) |
| Items in that epic | [backlog/epics/01-cli-foundations/BACKLOG.md](backlog/epics/01-cli-foundations/BACKLOG.md) (5 items) |

This is the minimum-viable set for an adopter to see the methodology operationalized. A real adopter project would add more pillars, more epics, more items as the project grew; this example shows the starting shape.

## Things NOT included (intentionally)

- **Source code.** This is docs-only; a real adopter would have `src/`, `tests/`, etc. alongside.
- **CHANGELOG / README of the project itself.** A real adopter would have these; we showed only the methodology artifacts here.
- **Memory directory.** Would exist on a real adopter project; not shown to keep the example focused.
- **Full backlog.** 5 items in one epic; a real project would have 30+ items across multiple epics.

## Methodology version

Built against methodology **v1.15.0**.
