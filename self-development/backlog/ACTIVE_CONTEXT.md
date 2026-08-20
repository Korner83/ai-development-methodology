# ACTIVE_CONTEXT.md — volatile working state

**Baton, not journal.** Where the current session is, so the next one — or this one after a
context reset — can resume without re-deriving state from scratch. Per
[`methodology/08_lessons_and_memory.md` "Active context"](../../methodology/08_lessons_and_memory.md#active-context-the-volatile-working-file):
written *before* a context reset, read *first* on resume, then **verified against live `git log`
and item state**, which are authoritative when they disagree with this file.

Overwritten, not appended. The durable record lives in commits, `ARCHIVE.md`, and memory.

_Last updated: 2026-08-20._

## Current focus

**E10 — External baseline audit remediation.** `active`, **all 14 items closed**, staged for a single
`v1.32.0`. Branch `claude/methodology-audit-plan-ccfebc`; **nothing committed, nothing merged.**

Every audit finding is addressed — the Critical, all five High, all four Medium. The epic stays `active`
because its closing gate is a fresh cold re-audit, which this session cannot run on itself.

## Shipped this session

The skill parses under strict YAML (it did not — nobody on a spec-compliant loader could install it).
Retired trunk exception gone; the skill defers to `00`'s authority ladder. **The lock's authority claim
now matches what git enforces**, with an opt-in shared-ref protocol where the loser's push rejection *is*
the compare-and-swap. **Destructive operations split** into `approval-gated` and `agent-prohibited` on
blast radius — which resolves the "user direction overrides everything" vs "the AI doesn't act, period"
conflict without amending either. **Trust follows provenance**, not filename. One `Test` enum, no subsets.
`pass` reserved for the required level. Counts carry an as-of marker. Actions SHA-pinned and the
supply-chain claim narrowed. Root `AGENTS.md` added. Adoption profile published, all ten epic folders
brought to five files, release-evidence commands written down, a surface map added to `00`, and a sweep
finding **6 of 16 conventions have ever been exercised**.

## Decisions that shaped it

- **No runnable elements, no new CI.** A committed integrity checker was declined. **F-08 and F-11 now
  have a convention, not a control** — hand-maintained counts can drift again, and the next occurrence
  will be found by a reader rather than a build. Stated in the charter rather than hidden.
- **The cross-AI gate was removed** from this epic's exit criteria. The methodology's cross-AI convention
  is untouched for adopters.
- **The epic's own paperwork was cut back** partway through, after it grew larger than the doc changes it
  described. An epic about overlapping normative copies is the worst place to add ceremony.

## Known deviations carried forward

- **BL-0040 was held at `under-review`** on a frozen-intent criterion ("net-negative in lines") that the
  work met in substance but not in letter, and closed only by explicit maintainer decision. The rule held
  under inconvenience, which was the useful part. BL-0051 hit the same shape and was *trimmed to fit*
  instead — two lines of merging beat a decision.
- **The "every template carries a version stamp" criterion is recommended for removal**, not fulfilment.
  The sweep's reasoning: a stamp in a template is a copy that goes stale on the adopter's disk where
  nothing can refresh it, while `SKILL.md` and `CHEATSHEET.md` are read *from* the repo and already carry
  one. The criterion was asking for the drift this epic spent its time removing.
- **The seven version-pin sites still read `v1.31.0`** and move at release time, not before.

## Next steps

1. **Review the diff.** Nothing is committed: 23 modified files, plus the E10 epic folder, root
   `AGENTS.md`, `ADOPTION_PROFILE.md`, `RELEASE_EVIDENCE.md`, the convention sweep, and nine back-filled
   `TEST.md` files.
2. **Two maintainer decisions** from the sweep, neither blocking: retire the house-verbosity setting
   (a removed section ⇒ **MAJOR**), and whether root `AGENTS.md` should carry the context-integrity canary
   (the sweep recommends yes).
3. **At release:** bump the seven version-pin sites to `v1.32.0`, rename `[Unreleased]`, annotated tag,
   two pushes. **The pins move in the release commit, not before** — the ordering rule this epic added.
4. **Then a fresh cold re-audit.** It is E10's closing gate and **this session cannot satisfy it**; a
   session auditing its own work is the defect the epic repaired.
