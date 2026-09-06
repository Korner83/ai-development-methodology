# ACTIVE_CONTEXT.md — volatile working state

**Baton, not journal.** Where the current session is, so the next one — or this one after a
context reset — can resume without re-deriving state from scratch. Per
[`methodology/08_lessons_and_memory.md` "Active context"](../../methodology/08_lessons_and_memory.md#active-context-the-volatile-working-file):
written *before* a context reset, read *first* on resume, then **verified against live `git log`
and item state**, which are authoritative when they disagree with this file.

Overwritten, not appended. The durable record lives in commits, `ARCHIVE.md`, and memory.

_Last updated: 2026-09-05._

## Current focus

**Nothing in flight.** `v1.34.0` staged on branch `claude/bl0059-audit-brief` from `main` at `702ae5a`.
`E00-intake` is standing with **one** open item; `E10` is `active` with zero open items, waiting on a
re-audit only an outside session can run.

## Shipped this session

Two items through intake, both of them decisions this project had already made and not carried out.

- **BL-0059 — architecture-layer routing is no longer its own convention.** It is now the top row of the
  failure-layer routing table, and the paragraph that treated it as a separate mechanism is gone. The
  cascade sentence generalised to *a finding at any layer cancels those below it*, which is what the
  ladder always meant. `CHEATSHEET.md` had zero headroom at 99, so the new rung was paid for by merging
  two lines rather than raising the cap — it is now 98. **Net: −2 lines, −1 named concept.** The corpus
  carries **15** named conventions, not 16.
- **BL-0062 — the audit brief.** `self-development/evaluations/AUDIT_BRIEF.md` makes commissioning an
  independent audit a paste: pinned commit and tree, ready prompt, twelve rubric dimensions with the four
  core ones named, and the prior audit's eleven findings beside their claimed fixes so an auditor checks
  them rather than believes them.

**Both were sweep decisions left unexecuted for sixteen days** — the second and third such case. That is a
pattern, and the sweep now says so rather than being quietly corrected.

## Known deviations carried forward

- **E10 is `active` with zero open items** and stays that way until a cold re-audit of the tagged tree
  returns a verdict. **Three releases of repair are now verified by nobody but their authors.** The brief
  removes the excuse; it does not remove the gap.
- **No committed checker**, by decision. Counts stay hand-maintained.
- **`E00`'s two deciding properties are still unrunnable** — the eviction rule has not fired and the
  intake ratio has no reporting date before 2026-11-25.

## Next steps

1. **Ship `v1.34.0`**, then **commission the re-audit** using the brief. Update its pin block first — it
   currently points at v1.33.0 and this release moves the target.
2. **BL-0058** (read the Agent File spec) is the only open intake item. Not urgent.
3. **The real ceiling is still external adoption.** Nine unexercised conventions is a no-users problem, not
   a documentation one, and no work inside this repo moves it.
