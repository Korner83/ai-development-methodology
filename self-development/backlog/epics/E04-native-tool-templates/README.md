# E04 — Native templates for Cursor, Aider, Continue.dev

**Pillar (primary):** [P4 — Tool compatibility](../../../pillars/P4_tool_compatibility.md)
**Status:** planned
**Phase:** Phase 1 — Foundation
**Started:** — (not yet active)
**Target close:** TBD (depends on E01, E02, or E03 closing to free a WIP slot)
**Owner:** maintainer + AI coding agent

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
