# E01 — Examples folder

**Pillar (primary):** [P1 — Doc completeness](../../../pillars/P1_doc_completeness.md)
**Pillar (secondary):** [P6 — Example richness](../../../pillars/P6_example_richness.md)
**Status:** done
**Phase:** Phase 1 — Foundation
**Started:** 2026-05-25
**Closed:** 2026-05-25 (v1.15.0 maintainer-authored batch)
**Owner:** maintainer + AI coding agent

**Closure summary:** Shipped [`examples/`](../../../../examples/) folder containing a fictional `tinker` developer-notes CLI as the worked example. Includes README + comparison table; example-project README; strategy master plan with 4 phases + binary exit criteria; 2 pillar files (P1 Capture, P2 Retrieval); EPICS rollup; 1 epic charter; 5 BL items in canonical table-form frontmatter demonstrating all major Status values (done / in-progress / ready / backlog / blocked) and the lock format. All content abstract-voice-compliant.

## Outcome (jobs-to-be-done)

When an adopter wants to see how the abstract methodology applies to a real project, they want concrete worked examples in the repo, so they can lift patterns directly rather than re-derive them from abstract docs alone.

## Exit criteria (binary)

- [ ] `examples/` folder exists at repo root (sibling of `methodology/`, `templates/`, `self-development/`).
- [ ] At least one fully-worked anonymized example set exists: 1 strategy master plan + 2–3 pillar files + 1 epic charter + 5+ BL items with full frontmatter and bodies.
- [ ] `examples/README.md` includes a 3-row comparison table mapping the three (`examples/` / abstract `methodology/` / `self-development/`) with a one-sentence purpose per row; a cross-AI reader can correctly map each artifact type to its purpose after one read.
- [ ] All anonymized content passes the methodology's abstract-voice rule extended to examples: no project names, no domain references that identify a real source project, no specific framework names beyond the methodology's accepted examples (Claude Code, Cursor, etc.).
- [ ] Examples are linked from the main README's "What's in the repo" tree.

## KPIs

- **Adopter signal:** examples are referenced in at least 1 adopter post / Discussions thread within 90 days of ship (passive measurement via search + repo activity).
- **Maintainer self-check:** the examples folder is something the maintainer would point a new adopter at without caveat (subjective but useful).

## Out of scope

- **Multiple-language examples.** English only. Translation is out of scope per [`brief/07_tech.md`](../../../brief/07_tech.md).
- **Code-shaped examples** (e.g., a worked example with actual source files). This methodology project is docs-only; code examples need a paired code-project adopter and aren't generatable from the methodology alone. Deferred to `FUTURE.md` for if/when a willing adopter provides material.
- **Anonymizing an entire real-project backlog.** One epic + 5 items is sufficient; a full backlog (50+ items) is overkill for the demonstration purpose. If adopters request more depth, file a follow-up epic.
- **Examples for niche adopter types** (regulated industry, research teams). Generic-startup-style example only in this epic; niche variants are Phase 2+ work via E04-style template adaptations.

## Linked docs

- Pillar (primary): [P1 — Doc completeness](../../../pillars/P1_doc_completeness.md)
- Pillar (secondary): [P6 — Example richness](../../../pillars/P6_example_richness.md)
- Strategy: [00_master_plan.md](../../../strategy/00_master_plan.md) (Phase 1 — Foundation)
- Methodology references:
  - [01_strategy.md](../../../../methodology/01_strategy.md) — example strategy doc shape
  - [02_pillars.md](../../../../methodology/02_pillars.md) — example pillar shape
  - [03_epics.md](../../../../methodology/03_epics.md) — example epic charter shape
  - [04_backlog_items.md](../../../../methodology/04_backlog_items.md) — example item shape
- Related epics: E05 (CHEATSHEET.md — both target P1 Doc completeness)

## Item roster

See [BACKLOG.md](BACKLOG.md) for active items (will be populated in Step 3 of the self-development bootstrap), [ARCHIVE.md](ARCHIVE.md) for completed, [FUTURE.md](FUTURE.md) for deferred.

## Open questions

- Should the example be a fictional project (clean, but obviously fake) or an anonymized real one (more useful, but anonymization is real work)?
- Should the example include "things that went wrong" — a worked example of recovery from a failure mode? More valuable but harder to fabricate honestly without a real source.
- Should `examples/` use the same `BL-####` ID space as `self-development/`, or its own (`BL-####` reset to 1, with prefix indication)?

These resolve when Step 3 charters items inside this epic.

## Risks

- **Anonymization quality.** A poorly-anonymized example could leak source-project details, violating the methodology's abstract-voice rule. Mitigation: have a cross-AI session review for abstract-voice violations before ship.
- **Example becomes outdated** as the methodology evolves. Mitigation: include the methodology version (v1.x) the example was built against; flag during semi-annual self-evaluation when version drift > 2 minor releases.
- **Example sets expectations** the methodology can't deliver in real projects (the example is too smooth). Mitigation: include at least one "we hit X friction here" note to model honest practice.
