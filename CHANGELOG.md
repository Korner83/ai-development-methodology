# Changelog

All notable changes to this methodology are documented here.
Updated per the Definition of Done in [methodology/07_definition_of_done.md](methodology/07_definition_of_done.md).

This is the single source of truth for the changelog.

---

## [Unreleased]

(nothing yet)

---

## v1.0.1 — 2026-05-24

### Feat — `templates/AUTONOMOUS_LOOP.md` (2026-05-24)

Adds a paste-and-adapt prompt template for long autonomous AI dev sessions. Tells the AI to apply the methodology as a continuous *analyze → prioritize → execute → validate → repeat* loop with a milestone-level stop condition (not per-task completion). Includes the integrity rule: never claim something is tested / secure / complete / production-ready unless actually verified.

Compressed from a real production-tested ~85-line autonomous-engineer prompt down to ~50 lines, with most rules referenced via methodology docs rather than restated inline.

Use cases: focused milestone work where the goal is agreed and the AI should grind toward it autonomously between check-ins. Not for exploratory work where each step needs review.

README updated to mention the new template (file tree + new "For long autonomous sessions" subsection).

---

## v1.0.0 — Initial public release (2026-05-24)

First public version. Extracted from a real production project's working practice and republished as a portable abstract methodology.

### Feat — Eleven-doc methodology set

The complete set lives under `methodology/`:

- [00_README.md](methodology/00_README.md) — index, mental model, doc index, adoption guides.
- [01_strategy.md](methodology/01_strategy.md) — master plan + supporting research + phase roadmap + re-evaluation protocol.
- [02_pillars.md](methodology/02_pillars.md) — sequential capability layers + refinement pattern.
- [03_epics.md](methodology/03_epics.md) — charters, JTBD outcomes, exit criteria, WIP limit, pre-epic planning.
- [04_backlog_items.md](methodology/04_backlog_items.md) — BL-### format, fields, status enums, lifecycle, resolution notes.
- [05_locks_and_parallel_work.md](methodology/05_locks_and_parallel_work.md) — file-based TTL locks + subagent delegation pattern.
- [06_working_principles.md](methodology/06_working_principles.md) — the four principles + plan-before-execute + tools-the-agent-uses.
- [07_definition_of_done.md](methodology/07_definition_of_done.md) — six gates, the hard rule, docs-maintenance patterns, quarterly repo health audits.
- [08_lessons_and_memory.md](methodology/08_lessons_and_memory.md) — two-layer memory + memory-as-leading-indicator feedback loop.
- [09_git_workflow.md](methodology/09_git_workflow.md) — branch protection, conventional commits, worktrees, destructive-command discipline, operational work patterns.
- [10_testing_and_verification.md](methodology/10_testing_and_verification.md) — automated tests, actual-UI fix-test loop, cross-AI validation, user testing as the final gate.

### Feat — Instruction-file templates for AI tools

`templates/` contains paste-and-adapt starter files for the project-instruction file:

- [templates/CLAUDE.md](templates/CLAUDE.md) — for Claude Code.
- [templates/AGENTS.md](templates/AGENTS.md) — vendor-neutral (OpenAI Codex, Google Antigravity, etc.).

The README's "AI tool support" section maps each AI tool to its expected filename.

### Feat — Field-tested in production

[EVALUATION.md](EVALUATION.md) is the honest field report: what the methodology covers, what was missing when compared to real practice, what got added in this release, and what remains deliberately out of scope. Coverage mapping plus practical pros and cons.

### Chore — Repo scaffolding

- [LICENSE](LICENSE) — CC BY 4.0 (attribution-required).
- [README.md](README.md) — TL;DR, problems-it-solves table, kickoff guide with AI prompts, AI tool support, attribution guidance.
- [STATUS.md](STATUS.md) — maintenance posture (lean — PRs welcome but no SLA; CC BY 4.0 means anyone can fork).

### Out of scope on this release

- Project-specific deploy commands, monitoring stacks, CI providers — by design (project choice).
- An `examples/` folder with anonymized real artifacts — future work, noted in EVALUATION.md.
- A one-page CHEATSHEET — README's TL;DR currently serves this; revisit if requested.
