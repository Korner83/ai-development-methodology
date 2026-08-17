# E04 — Native templates for Cursor, Aider, Continue.dev

**Pillar (primary):** [P4 — Tool compatibility](../../../pillars/P4_tool_compatibility.md)
**Status:** parked — **will not resume** (2026-08-14, maintainer decision)
**Phase:** Phase 1 — Foundation
**Started:** — (never activated; no items were ever filed)
**Closed:** 2026-08-14 — decided against, see "Why this epic was dropped" below
**Owner:** maintainer + AI coding agent

> **Frozen intent** — Outcome and exit criteria approved and now closed. The charter below is
> preserved unchanged as the record of what was proposed; only this header and the closing
> section are new. Do not edit the original text to make it agree with the decision.

## Why this epic was dropped

**Maintainer decision, 2026-08-14: `AGENTS.md` + adaptation is the permanent answer for Cursor,
Aider, and Continue.dev — not an interim state waiting on native templates.**

The reasoning that closed it:

- **Maintenance surface for a thin gain.** Three more template files, each needing to stay in
  sync with `AGENTS.md` on every release, to save adopters a rename and a small edit. The
  charter's own Risks section already predicted the failure mode: *"Native templates diverge
  from AGENTS.md subtly over time, breaking the 'AGENTS.md is the canonical superset' claim."*
- **The vendor conventions are still moving.** The charter's own open questions couldn't settle
  Cursor's `.cursorrules`-vs-`.cursor/rules/` split or Continue.dev's location. Shipping
  snapshots of unstable conventions produces files that are wrong within months and that
  adopters trust anyway because they came from upstream.
- **No adopter has asked.** The epic was always gated on demand signal that never arrived —
  and per the [first self-evaluation](../../../evaluations/2026-05-25-eval-01.md), no external
  adopter has used a non-Claude tool with this methodology at all yet. Building for a need
  nobody has reported is exactly what the epic said it would wait for.

**What replaces it:** nothing new is needed. `AGENTS.md` is already the vendor-neutral superset,
the README's tool table already names the target filename for each tool, and "adapt AGENTS.md"
is now documented as the *answer* rather than a placeholder.

**What would reopen it:** an adopter reporting that adaptation actually failed them — that
`AGENTS.md` carried an assumption their tool couldn't honour. That is a real bug in the
superset claim, and it would justify either a native template or a fix to `AGENTS.md`. Demand
alone ("it'd be nice to have") is not enough; the maintenance-drift risk above outweighs it.

**Lifecycle note:** epics have no `rejected` state — the enum is `planned | active | done |
parked` — so this is recorded as `parked` with an explicit will-not-resume marker. See the
[EPICS.md](../../EPICS.md) legend.

## Outcome (jobs-to-be-done)

When an adopter using Cursor, Aider, or Continue.dev arrives at the repo, they want a native-named template they can drop into their project with minimal modification, so they don't have to manually adapt `AGENTS.md` and possibly miss tool-specific conventions in the process.

## Exit criteria (binary)

- [ ] `templates/cursorrules.md` (or equivalent — investigate Cursor's actual expected location: `.cursor/rules/` directory vs single `.cursorrules` file) exists with content adapted from `AGENTS.md` for Cursor's specific conventions.
- [ ] `templates/CONVENTIONS.md` exists for Aider, following Aider's documented project-instruction file convention.
- [ ] `templates/continue-context.md` (or equivalent — investigate Continue.dev's actual expected location: `.continue/context.md`) exists for Continue.dev.
- [ ] Each native template has been loaded into its target tool and a spot-check confirms that ≥3 methodology-specific terms (e.g., "WIP limit", "exit criteria", "lock TTL", "DoD hard rule", "ROI heuristic") appear in the agent's context window when queried with "what process rules apply to this repo?" or equivalent.
- [ ] The README's "AI tool support" table is updated: each tool that previously said "adapt AGENTS.md" now points to a native template.
- [ ] The native templates are documented as *derived from AGENTS.md* with a clear "drift-prevention" note explaining that AGENTS.md is the canonical superset and native templates are tracked when AGENTS.md changes.

## KPIs

- **Reduced friction signal:** fewer "how do I use this with Cursor / Aider / Continue?" Discussions threads after ship (passive measurement).
- **Cross-tool adoption signal:** at least 1 adopter reports using two or more of (Cursor, Aider, Continue.dev) with these templates within 90 days of ship.

## Out of scope

- **Templates for not-yet-mainstream tools.** Aider, Cursor, Continue.dev are well-established; emerging tools (e.g., Codeium-coding-specific, Jules-specific) can be added in future epics as their share grows.
- **Tool-specific tutorials.** Templates only. "How to use Cursor effectively" is the vendor's job; this epic only provides the methodology-loading file.
- **Custom-domain Cursor / Aider / Continue templates** (e.g., a Python-specific Cursor template). The methodology stays language-agnostic; adopters layer language-specific instructions on top in their own usage.
- **Maintaining the templates per-vendor-release.** Templates are snapshot at the version current at ship time; adopters fork and update as their tool evolves. The maintainer doesn't track every vendor release.

## Linked docs

- Pillar (primary): [P4 — Tool compatibility](../../../pillars/P4_tool_compatibility.md)
- Brief: [`brief/07_tech.md`](../../../brief/07_tech.md) — names the tools in scope
- Methodology: [`templates/AGENTS.md`](../../../../templates/AGENTS.md) — the canonical superset all native templates derive from
- Related epics: (none directly; E01 examples folder could reference native templates if useful)

## Item roster

See [BACKLOG.md](BACKLOG.md) for active items (populated in Step 3 when this epic moves to active), [ARCHIVE.md](ARCHIVE.md) for completed, [FUTURE.md](FUTURE.md) for deferred.

## Open questions

- **Cursor template location:** `.cursor/rules/<file>.md` directory pattern (newer Cursor convention) vs `.cursorrules` single file (older convention)? Cursor docs recommend the directory pattern for new projects; templates should follow recommendation.
- **Aider's `CONVENTIONS.md`:** Aider also uses `.aider.conf.yml` for tool config. Should the template be just `CONVENTIONS.md` (project-instruction layer) or include a sample `.aider.conf.yml` too? Lean toward just `CONVENTIONS.md` to keep scope tight.
- **Continue.dev's `.continue/context.md`:** Continue's project-instruction conventions are less stable than Cursor's or Aider's. Investigate current best practice.
- **Drift between AGENTS.md and native templates:** if AGENTS.md gets a v2 update, do native templates re-derive automatically or only on maintainer pass? Lean toward maintainer pass (semi-annual self-evaluation catches the drift).

## Risks

- **Tool conventions change.** Cursor, Aider, Continue.dev are all under active development; their instruction-file conventions may shift in the coming months. Native templates that worked at ship time may become stale. Mitigation: include version stamps; track in semi-annual self-evaluation.
- **Native templates diverge from AGENTS.md** subtly over time, breaking the "AGENTS.md is the canonical superset" claim. Mitigation: cross-reference diff at every semi-annual eval.
- **Adopters expect tool-specific tutorials** in addition to templates. Mitigation: clear "templates only" framing in template headers; route tutorial requests to vendor docs.
