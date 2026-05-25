# Evaluations

This folder holds **semi-annual methodology self-evaluation reports** for the methodology project.

## Cadence

Per [`methodology/07_definition_of_done.md "Methodology self-evaluation (semi-annual)"`](../../methodology/07_definition_of_done.md#methodology-self-evaluation-semi-annual): one pass every six months. The cadence catches drift between the abstract methodology docs and how the project / adopters actually use them.

## What each report contains

Each report is one markdown file named `YYYY-MM-<topic>.md` and follows this structure:

- **Metadata** — pass date, methodology version at eval time, reviewer session details, scope.
- **Cold-read findings** — what fresh-session reviewers reported about each methodology doc, classified as stale / unclear / inconsistent with file:line citations.
- **Classification + dispositions** — each finding tagged `practice-wrong` / `docs-wrong` / `both` and routed to `patch release` / `file as item` / `defer`.
- **Summary statistics** — counts by classification and disposition; pass duration.
- **Next eval date** — target for the next semi-annual pass.
- **Maintainer signoff** — final approval before the pass closes.

## Why these reports live in `self-development/`

Per the methodology, self-evaluation is itself a methodology artifact — applied to the methodology project here. Adopters can use these reports as worked examples of how the self-evaluation cadence is operationalized on a real (if meta) project.

## Status of this folder

Seeded 2026-05-25 via BL-0006 (E02). First pass (`2026-05-first-pass.md`) is populated by BL-0007 through BL-0010 — currently a skeleton awaiting cold-read findings.
