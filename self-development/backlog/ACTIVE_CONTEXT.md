# ACTIVE_CONTEXT.md — volatile working state

**Baton, not journal.** Where the current session is, so the next one — or this one after a
context reset — can resume without re-deriving state from scratch. Per
[`methodology/08_lessons_and_memory.md` "Active context"](../../methodology/08_lessons_and_memory.md#active-context-the-volatile-working-file):
written *before* a context reset, read *first* on resume, then **verified against live `git log`
and item state**, which are authoritative when they disagree with this file.

Overwritten, not appended. The durable record lives in commits, `ARCHIVE.md`, and memory.

_Last updated: 2026-08-25._

## Current focus

**E00 — Intake**, opened 2026-08-25 as a **standing** epic that never closes. Branch
`claude/focused-mode-intake`, cut from `main` at `495b113` (v1.32.0).

It is the **dogfood run for focused mode**: same `BL-####` format, same frozen intent, same
`Status`/`Test` hard rule, same six DoD gates, same lock — **no epic charter above it.** The design and
the condition that would promote it into `methodology/` live in
[`E00/FUTURE.md`](epics/E00-intake/FUTURE.md). **Nothing about focused mode is published as a convention,
deliberately** — seven of sixteen conventions added v1.25.0 → v1.31.0 have ever been exercised, so this
one gets used before it gets written. That ordering has never happened in this project.

## Shipped this session

- **`E00-intake`** with all five files. Three items filed, one closed.
- **BL-0057 closed** — the template version-stamp criterion is **dropped**, not fulfilled. The v1.32.0
  sweep decided that on 2026-08-20 and **nobody executed it**; it sat open in the master plan for five
  days while the release it came from shipped. A decision recorded and not executed is the same failure as
  a claim asserted and not checked. It had no epic and was too small to charter — **that is precisely the
  gap intake closes, demonstrated on the first item rather than argued for.**
- **BL-0058 / BL-0059 filed** — read the Agent File spec and decide on a conformance line; fold
  architecture-layer routing into failure-layer routing (the sweep's second unexecuted decision).
- **Landscape triage of `alvinreal/awesome-opensource-ai`** recorded in `E00/FUTURE.md` as BL-0061.
  Roughly nine tenths is runtime infrastructure and not applicable. Agent File is the one pick, because it
  is the only entry that solves state portability with a *file format* rather than a running service —
  the same wager this methodology makes.

## Design finding from the first hour

**A standing epic breaks the WIP cap on a literal reading** — permanently `active` means one of two slots
gone forever. Resolved as a **declared deviation**: the cap limits concurrent *chartered* effort and
intake is not chartered effort. Recorded in `E00`'s charter and in `EPICS.md` rather than read into the
rule. This is the kind of thing that surfaces from using a convention and not from writing one.

## Known deviations carried forward

- **E10 is still `active` with zero open items.** Its closing gate is a fresh cold re-audit of the tagged
  `v1.32.0` tree by a session that did not author the fixes. Unrun.
- **No committed checker.** Counts stay hand-maintained; the next drift is found by a reader, not a build.
- **AT-05 and AT-06 in `E00/TEST.md` are unrunnable yet** — the eviction rule has not fired and the intake
  ratio has no reporting date until 2026-11-25. They are the two properties that decide whether intake was
  worth building, and they are recorded as `not-tested` rather than omitted.

## Next steps

1. **Ship this as `v1.33.0`** — self-development work is capped at minor or patch by project override, and
   this adds new artifacts, so MINOR.
2. **Work BL-0058 and BL-0059** when there is appetite; both are small and neither is urgent.
3. **The re-audit of v1.32.0** remains E10's gate and this session's blind spot.
4. **2026-11-25 semi-annual pass** — first intake-ratio report, first chance to fire the eviction rule,
   and the re-pin check on the two SHA-pinned actions.
