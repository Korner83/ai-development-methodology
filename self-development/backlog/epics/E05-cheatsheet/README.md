# E05 — CHEATSHEET.md (one-page reference)

**Pillar (primary):** [P1 — Doc completeness](../../../pillars/P1_doc_completeness.md)
**Status:** done
**Phase:** Phase 1 — Foundation
**Started:** 2026-05-25
**Closed:** 2026-05-25 (v1.15.0 maintainer-authored batch — single-artifact epic, no formal items charted)
**Owner:** maintainer + AI coding agent

**Closure summary:** Shipped [`CHEATSHEET.md`](../../../../CHEATSHEET.md) at repo root. ~80 lines (under the 100-line cap). Covers: 4 planning layers, 3 discipline overlays + applied + evaluation, 4 working principles, hard rules, lock format + TTL, ROI heuristic, challenge-before-consenting prompt, tier matrix, milestones + scoring rubric, AUTONOMOUS_LOOP / HUMAN_NEEDED / FEEDBACK references, cross-AI two modes. Linked from main README. Methodology version v1.15.0 pinned.

## Outcome (jobs-to-be-done)

When an adopter wants a quick reference for the methodology's key patterns without re-reading the docs (mid-task lookup), they want a one-page CHEATSHEET, so they can pin it open during work and find the right rule in seconds.

## Exit criteria (binary)

- [ ] `CHEATSHEET.md` exists at repo root (sibling of README.md, CHANGELOG.md).
- [ ] Total length is under 100 lines (fits one screen / printed page; the entire point of the format).
- [ ] Covers at minimum:
  - The 4 planning layers (strategy / pillars / epics / items) with their time horizons and file locations.
  - The 3 discipline overlays (working principles / DoD / memory) with one-line summaries.
  - The 4 working principles with the canonical one-line phrasings.
  - The DoD hard rule (`Status: done` requires `Test: pass`).
  - The lock format and TTL convention.
  - The ROI heuristic table (Priority × Effort → action).
  - The challenge-before-consenting prompt.
  - The `AUTONOMOUS_LOOP.md` and `HUMAN_NEEDED.md` patterns.
- [ ] Linked from the main README (in TL;DR or "What's in the repo" area) and from `methodology/00_README.md`.
- [ ] Includes a "see the full doc for X" pointer for each major topic (cheatsheet is reference, not learning).

## KPIs

- **Reference signal (60 days post-ship):** ≥3 Discussions threads or external mentions reference "cheatsheet" or "quick reference" specifically. Backup measurement: GitHub Insights / Traffic tab if available at measurement time.
- **Adopter signal (90 days post-ship):** at least 1 adopter mentions the cheatsheet positively in Discussions or external mention.

## Out of scope

- **Tutorial content.** Cheatsheet is reference, not learning. New adopters should still read the methodology docs; the cheatsheet is for adopters who have already read and need quick lookup.
- **Per-tool variants.** One cheatsheet for the methodology, not per-tool. Tool-specific quick references are the vendor's job.
- **Multiple cheatsheets** (e.g., a "leader cheatsheet" + a "contributor cheatsheet"). Single page keeps it scannable; multiple cheatsheets defeat the purpose.
- **Print-optimized formatting.** Markdown rendering on GitHub is the primary surface; printable styling is nice-to-have but not in scope.

## Linked docs

- Pillar (primary): [P1 — Doc completeness](../../../pillars/P1_doc_completeness.md)
- Brief: [`brief/01_vision.md`](../../../brief/01_vision.md) — adopter-facing value
- Methodology: every doc in `methodology/` (the cheatsheet is essentially the TL;DR of all of them)
- Related epics: E01 (examples folder — both target P1; cheatsheet should mention the examples folder once it exists)

## Item roster

See [BACKLOG.md](BACKLOG.md) for active items (populated in Step 3 when this epic moves to active), [ARCHIVE.md](ARCHIVE.md) for completed, [FUTURE.md](FUTURE.md) for deferred.

## Open questions

- **Format: table-heavy or prose-light?** Tables compress more information per inch; prose may be more readable. Lean toward table-heavy with short prose intros per section.
- **Should it include a Mermaid diagram?** The README has two; a third on the cheatsheet might be redundant or might be the ideal at-a-glance summary. Decide based on how it scans at 100 lines.
- **Versioning:** does the cheatsheet version-bump with each methodology release, or only when content changes? Lean toward "only when content changes," with the methodology version it was last reviewed-against noted at the bottom.
- **Conflict with TL;DR section in main README:** the README has a TL;DR. The cheatsheet would overlap. Decide whether the cheatsheet replaces the README's TL;DR (move content) or duplicates with intentional redundancy (accept the drift cost).

## Risks

- **Scope creep beyond 100 lines.** "Just one more pattern" expands the cheatsheet to 200+ lines, defeating its purpose. Mitigation: enforce the 100-line cap as a hard exit criterion; cut content rather than expand the cap.
- **Cheatsheet drifts behind methodology updates.** A patch release might change a pattern; the cheatsheet doesn't get updated; adopters relying on it are misinformed. Mitigation: include cheatsheet review in every release's CHANGELOG checklist; flag during semi-annual eval.
- **Cheatsheet becomes the "real" entry point** and adopters skip the full docs. Mitigation: explicit "this is reference, not learning" framing at the top; pointers to full docs throughout.
