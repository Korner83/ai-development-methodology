# P1 — Capture

_Pillar definition. Following the [02_pillars.md](../../../methodology/02_pillars.md) skeleton._

## What this pillar is

The capability layer that lets users write a note quickly, from any context, without breaking their current flow. The bar: capture latency must feel like `git commit` — sub-second from intent to "captured."

## Why it's first in the dependency chain

Without capture working well, retrieval (P2) has nothing to retrieve. The capture experience is the user's first impression and the gate to all downstream value. Optimize capture before adding any retrieval feature.

## What 10/10 capture looks like

- `tinker capture "<note>"` returns in < 300ms on a typical dev machine.
- The note is durably stored before the command returns (no async loss on crash).
- The context (working directory, git branch if any, calendar event if active) is automatically attached.
- The command works with stdin pipe, with one-shot arg, and with no-arg (opens `$EDITOR`).
- Errors are loud and recoverable (clear message; never silent failure).

## What 0/10 capture looks like

- Multi-second latency.
- Notes lost on crash.
- Context not attached; user has to specify it manually every time.
- One input mode only (forcing a workflow that doesn't fit the user).
- Silent failures.

## What's NOT in this pillar

- **Editing existing notes.** That's P2 (retrieval) — you have to retrieve before you can edit.
- **Sync between devices.** That's a Phase 2+ pillar (P4 — Multi-device sync, not yet chartered).
- **Sharing notes with others.** Out of scope; `tinker` is single-user (per strategy).

## Connections to other pillars

- **Output to P2 (Retrieval).** Capture's storage format is the input to retrieval. The schema is a shared contract; both pillars must agree.
- **Input from P3 (Context detection — not yet chartered).** Future pillar that improves what counts as "context"; for now P1 owns the basic context attachment.

## Status

**Phase 1 — Foundation.** Active.

## Refinement history

- v1.0: initial definition.
