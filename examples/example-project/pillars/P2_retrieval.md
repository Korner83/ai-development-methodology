# P2 — Retrieval

_Pillar definition. Following the [02_pillars.md](../../../methodology/02_pillars.md) skeleton._

## What this pillar is

The capability layer that lets users find a previously-captured note quickly. The bar: from "I remember writing about X" to having the note open in < 5 seconds.

## Why it's second in the dependency chain

Retrieval is downstream of capture (P1). If capture is unreliable, retrieval has nothing to retrieve well. P2 depends on P1's storage format and context attachment.

## What 10/10 retrieval looks like

- `tinker recent` returns the last N notes for the current directory in < 200ms.
- `tinker search <query>` does full-text search across all notes with relevance ranking; returns in < 500ms for stores up to 10,000 notes.
- Output is human-readable (terminal-formatted) and pipe-friendly (newline-separated when piped).
- Filters by date range, by directory, by git branch, by calendar event.
- Results include enough context (date, dir, branch) for the user to recognize which note they wanted.

## What 0/10 retrieval looks like

- Multi-second search.
- No ranking — results in arbitrary order.
- Output unreadable without pipe-to-`less`.
- No filters — user has to grep through everything.

## What's NOT in this pillar

- **Editing notes after retrieval.** Separate sub-feature (would be P2.1 or a later refinement); v1 ships retrieval as read-only.
- **Visualization** (charts of notes-per-day, etc.). Out of scope.

## Connections to other pillars

- **Input from P1 (Capture).** Retrieval consumes P1's stored format. Schema changes in P1 break P2 — coordinated changes required.
- **Output to (future) P5 — Export.** Not yet chartered; would let users export notes to other formats (markdown, JSON).

## Status

**Phase 1 — Foundation.** Active.

## Refinement history

- v1.0: initial definition.
