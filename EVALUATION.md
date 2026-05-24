# Evaluation — Methodology vs. Real Practice

> Field notes from a comparison between this methodology (theoretical) and the practice in the source project that originated it (real). Written abstractly so it transplants: no project name, no domain references.

This is a self-audit. It lists what the methodology already captures, what real practice has invented that the methodology missed, and what's still uncovered after the latest revision.

---

## TL;DR

The methodology is **good but incomplete.** It captures the right shape — four planning layers, three discipline overlays, file-based locks, fix-test loops — and the strategy/pillars/epics/items templates are actually being followed in real practice (a meaningful validation). But four real-practice patterns were missing:

| Gap | Severity | Now addressed? |
|---|---|---|
| Pre-epic **planning layer** between strategy and epics. | High — it's a fourth common layer the methodology ignored. | Yes — added to [03_epics.md](methodology/03_epics.md) "Pre-epic planning." |
| **Operational concerns** (deploys, pipelines, runbooks, on-call). | Medium — most projects need it; methodology said nothing. | Yes — added to [09_git_workflow.md](methodology/09_git_workflow.md) "Operational work." |
| Concrete **AI-agent playbook** details (TTL specifics, lock-release coupling, subagent pattern). | Medium — methodology had the concept; real practice had the operational steps. | Yes — strengthened in [05_locks_and_parallel_work.md](methodology/05_locks_and_parallel_work.md). |
| **Resolution-note pattern** for rejected items. | Low — but useful for traceability. | Yes — added to [04_backlog_items.md](methodology/04_backlog_items.md). |

And five user-requested additions, also landed in this revision:

| Addition | Where |
|---|---|
| Plan mode before non-trivial tasks. | [06_working_principles.md](methodology/06_working_principles.md) |
| Cross-AI validation (separate AI does perf/logic/security checks). | [10_testing_and_verification.md](methodology/10_testing_and_verification.md) |
| User testing is the final gate. | [10_testing_and_verification.md](methodology/10_testing_and_verification.md) |
| AI installs MCPs / plugins / skills as needed. | [06_working_principles.md](methodology/06_working_principles.md) |
| Memory → methodology feedback loop. | [08_lessons_and_memory.md](methodology/08_lessons_and_memory.md) |

**Verdict:** the methodology was 85% complete before this revision. After it, ~95%. The remaining 5% is genuinely project-specific and probably shouldn't be in a portable methodology at all.

---

## Coverage mapping

What the methodology covers, what real practice does, where they diverge.

| Real-practice concern | Methodology doc that addresses it | Coverage quality | Notes |
|---|---|---|---|
| **Long-term strategy** | [01_strategy.md](methodology/01_strategy.md) | ✅ Full | Real strategy docs follow the template (vision/version/phases/re-evaluation/version-history). Validated. |
| **Pillars** (durable capability layers) | [02_pillars.md](methodology/02_pillars.md) | ✅ Full | Real pillars follow goal/sections/tables/mermaid/Next-footer convention. Validated. |
| **Pre-epic planning / design docs** | [03_epics.md](methodology/03_epics.md) "Pre-epic planning" | ✅ Now covered | Was the biggest gap. Real projects have a `docs/planning/` layer holding pre-charter design work; the methodology now names this explicitly. |
| **Epics** (3–12 week delivery containers) | [03_epics.md](methodology/03_epics.md) | ✅ Full | Real epic charters follow the template; WIP limit is observed; out-of-scope sections are used. Validated. |
| **Backlog items** (BL-### format) | [04_backlog_items.md](methodology/04_backlog_items.md) | ✅ Full | Real items follow the frontmatter format. Resolution-note pattern was the only addition needed. |
| **Resolution notes** on rejected/non-obvious-done items | [04_backlog_items.md](methodology/04_backlog_items.md) "Resolution notes" | ✅ Now covered | Real practice uses `**Resolution:**` blocks. Methodology now documents this. |
| **File-based locks with TTL** | [05_locks_and_parallel_work.md](methodology/05_locks_and_parallel_work.md) | ✅ Full | The strongest correspondence between methodology and practice. The 2-hour TTL, subagent pattern, and lock-release-with-status coupling now spelled out concretely. |
| **AI Agent Playbook** (12-step protocol for picking items) | [05_locks_and_parallel_work.md](methodology/05_locks_and_parallel_work.md) | ✅ Now covered | Real practice had a richer protocol in `backlog/README.md`; methodology now incorporates the key steps. |
| **Working principles for LLM-coding** | [06_working_principles.md](methodology/06_working_principles.md) | ✅ Full | Four principles cover the major failure modes. Plan-mode and MCP-install added in this revision. |
| **Plan-mode discipline** | [06_working_principles.md](methodology/06_working_principles.md) "Plan before executing" | ✅ Now covered | Real practice already uses plan-mode for non-trivial tasks; methodology now requires it. |
| **MCP / plugin / skill install** | [06_working_principles.md](methodology/06_working_principles.md) "Tools the agent uses" | ✅ Now covered | Methodology now sanctions installing helpful tools rather than reinventing. |
| **Definition of Done** with hard rule | [07_definition_of_done.md](methodology/07_definition_of_done.md) | ✅ Full | Six gates, the hard rule (`Status: done` requires `Test: pass`), no exceptions. |
| **Two-layer memory system** | [08_lessons_and_memory.md](methodology/08_lessons_and_memory.md) | ✅ Full | Project-instruction file + memory dir. Templates provided. |
| **Memory → methodology feedback loop** | [08_lessons_and_memory.md](methodology/08_lessons_and_memory.md) "Memory as a leading indicator" | ✅ Now covered | Real practice has a memory directory full of recurring fixes that suggest methodology gaps; the loop is now named. |
| **Git workflow** (branches, PRs, worktrees, destructive ops) | [09_git_workflow.md](methodology/09_git_workflow.md) | ✅ Full | Real practice follows this; the worktree-for-parallel-agents pattern is documented. |
| **Operational concerns** (deploys, pipelines, runbooks, on-call) | [09_git_workflow.md](methodology/09_git_workflow.md) "Operational work" | ✅ Now covered | Was completely missing. Methodology now points at the patterns that transfer. |
| **Testing — automated** | [10_testing_and_verification.md](methodology/10_testing_and_verification.md) | ✅ Full | Behavior tests, regression tests, full-suite discipline. |
| **Testing — actual UI fix-test loop** | [10_testing_and_verification.md](methodology/10_testing_and_verification.md) | ✅ Full | Specifically for frontend: required dimensions (theme/viewport/auth/empty/error), the loop pattern. |
| **Cross-AI validation** (different AI audits the work) | [10_testing_and_verification.md](methodology/10_testing_and_verification.md) "Cross-AI validation" | ✅ Now covered | A separate AI doing perf/logic/security/penetration checks catches blind spots; this is now sanctioned. |
| **User testing as final gate** | [10_testing_and_verification.md](methodology/10_testing_and_verification.md) "User testing" | ✅ Now covered | Real users always beat automated tests; methodology now says so explicitly. |
| **CLAUDE.md / AGENTS.md / per-AI instruction files** | [templates/CLAUDE.md](templates/CLAUDE.md), [templates/AGENTS.md](templates/AGENTS.md) | ✅ Now covered | Vendor-neutral and Claude-specific starter templates provided; naming guide for other tools (Cursor, Codex, Antigravity, Aider) in README. |

---

## Findings sheet

A flat list of every concrete finding from the field comparison.

### What's there (real practice confirms the methodology works)

- Strategy docs in real practice follow the template exactly (vision + version + phases + re-evaluation + version history). The template is not aspirational; it's the actual shape.
- Pillars in real practice use the goal/sections/tables/mermaid/Next-footer pattern. The sequential dependency chain holds.
- Epic charters use JTBD outcomes, binary exit criteria, KPIs, and explicit out-of-scope sections. The pattern is being followed.
- BL-### items use the frontmatter table format with all the named fields. Status enums match.
- The lock mechanism — file-based, TTL, em-dash-for-unlocked — is the actual coordination primitive.
- The Definition of Done hard rule (`Status: done` requires `Test: pass`) is enforced.
- The two-layer memory system (project instructions + memory directory) is in active use; the memory directory has accumulated dozens of entries.
- Git workflow (branches, PRs, worktrees, no force-push to trunk) is the lived practice.
- The UI fix-test loop is the actual verification practice for frontend changes.

### What was missing (now added)

- **Planning layer** between strategy/pillars and epics. Real practice has a `docs/planning/` folder with detailed design work that informs epics before chartering. The methodology had no name for this.
- **Operational concerns** entirely. The methodology said nothing about deploys, data pipelines, runbooks, on-call. Real practice has detailed deploy procedures, safety boundaries, and a clear "user-only commands" pattern.
- **Concrete AI Agent Playbook steps.** The methodology described the concept of locks but real practice had a 12-step operational protocol — including the subagent pattern (parent holds lock, subagent does work without touching the lock) — that wasn't formalized.
- **Resolution notes** on rejected items. Real practice uses `**Resolution:**` blocks to document *why* an item was rejected. Useful for preventing the same idea from being re-filed.
- **Plan-mode discipline.** Real practice uses plan-mode for non-trivial tasks; the methodology didn't require it.
- **MCP / plugin / skill install.** Real practice has the AI install tools (MCP servers, IDE plugins, libraries) as needed. The methodology didn't sanction this.
- **Cross-AI validation.** A separate AI auditing the work catches what the implementing AI missed. Now an explicit gate.
- **User testing is the final gate.** Implicit before, explicit now. Cross-AI validation is great; real users finding things is better.
- **Memory → methodology feedback loop.** When memory entries cluster around a topic, the methodology likely has a gap. Now a named practice (review quarterly).

### What's still missing (acknowledged, not addressed)

These are genuinely project-specific and probably should NOT be in a portable methodology — they belong in the project's own docs:

- **Specific deploy commands** for your platform (Vercel, Fly.io, Hetzner, etc.). Each project picks; methodology can't.
- **Specific monitoring stack** (Grafana, Datadog, etc.). Project choice.
- **Specific CI provider** (GitHub Actions, GitLab CI, etc.). Project choice.
- **Specific test framework** (Vitest, Jest, Playwright, etc.). Project choice.
- **Domain-specific quality gates** (e.g., audio quality checks, image rendering checks, ML model evaluation). Project choice.
- **Team structure and hiring plans.** Strategy doc territory, but very project-specific.
- **Pricing strategy** in detail. Strategy doc territory.

These are correctly absent from the methodology. They'd be project-specific noise if they were in.

---

## Practical pros & cons

### Pros of following the methodology (from real-practice experience)

- **Faster contributor onboarding.** New humans pick up the project structure in ~30 minutes; new AI sessions read the project-instruction file and can start working within minutes.
- **Audit trail for everything.** Every state change is a git commit. Three months later, you can reconstruct *why* something was done.
- **Lock mechanism prevents real collisions.** With multiple AI sessions running on the same repo, the file-based lock has prevented genuine duplicate work multiple times.
- **The hard rule (`done` requires `pass`) catches half-truths.** Items that "should be done" don't slip through; they're caught at the test gate.
- **The UI fix-test loop catches what tests miss.** Frontend changes that pass tests but break layout/theme/empty-state are caught before ship, not after a user reports.
- **Memory entries are gold.** Recurring fixes captured in memory have prevented the same bug from being reintroduced multiple times.
- **Pillar layer reduces scope drift.** Knowing which pillar an epic advances stops "should we also do X" creep.
- **Strategy versioning preserves intent.** Old strategy versions explain why a current decision was made.

### Cons of following the methodology (real costs)

- **Overhead at the start.** Setting up the structure (strategy doc, pillars, first epic, first items) takes a day or two for a new project. Worth it, but not free.
- **Lock-protocol friction.** Acquire-commit-push round trip adds ~30 seconds per item pickup. Friction is small but non-zero.
- **DoD discipline can feel slow when in a rush.** The temptation to skip the UI gate "just this once" is real; the methodology forbids it. Sometimes that's the right friction; sometimes it's annoying.
- **Strategy/pillar docs aren't free.** Writing them well takes time. Skimped strategy docs are worse than no strategy docs (false confidence).
- **The 11-doc set is intimidating to a new reader.** Even with reading-order guides, "11 docs" feels like a lot. Most contributors only need ~4 to start.
- **Updating docs after refactors is real work.** When the codebase changes, the project instruction file and some memory entries go stale. Maintenance is a recurring cost.
- **Memory directory bloats if not pruned.** Without periodic consolidation, the memory becomes a graveyard of stale advice.

### Net: the pros outweigh the cons by a lot

The overhead is front-loaded; the benefits compound. After ~3 months of use, the methodology pays back the setup cost many times over. Before 3 months, you might still feel the overhead more than the benefit.

The pattern: methodologies feel heavy in week 1 and indispensable in month 3. This one is no different.

---

## Areas the methodology probably should NOT cover (deliberate non-goals)

Some readers will look at this set and ask "where's X?" Below are concerns the methodology deliberately doesn't address, and why.

| Concern | Why it's not in the methodology |
|---|---|
| **Code style / linter config** | Project-specific. Lives in the project's lint config, not the process docs. |
| **Specific framework conventions** | Project-specific. React patterns, Django patterns, etc. live in the framework's own docs. |
| **Architecture decisions (ADRs)** | A worthwhile practice, but architecture is project-specific. The methodology recommends documentation; the project decides format. |
| **Specific issue-tracker integration** | The methodology is markdown-and-git. External trackers are a project choice; the methodology stays neutral. |
| **Team meeting cadence** | Methodology covers artifacts and gates, not scheduling. Standups, retros, etc. are team choices. |
| **Hiring rubrics** | Out of scope. Strategy docs touch on team shape; specifics belong elsewhere. |
| **Specific AI tool integration** | The methodology assumes some AI tool. Cursor vs. Claude Code vs. Aider — your call. The templates support several. |
| **Estimation precision** | Effort enum (XS/S/M/L/XL) is coarse on purpose. Story points / hours estimation can be added but isn't required. |
| **Roadmap presentation** | Strategy docs cover phases; how you present them to stakeholders is up to you. |

If your project needs any of these, layer them ON TOP of the methodology — don't try to fit them inside it.

---

## What I'd add next (future revisions, not done yet)

- **An "agent skills inventory" template** — for projects that build up custom AI agent prompts/skills, a way to catalog and version them.
- **A "data backfill" pattern** — for projects with long-running data jobs that need to be safe to restart, idempotent, etc. Currently lives in operational concerns; could grow its own section.
- **An "incident response" mini-doc** — what to do when production breaks. Currently implicit in operational concerns; could be its own short doc.
- **Examples gallery** — real (anonymized) examples of strategy docs, pillar docs, epic charters, BL items. The current docs have templates and abstract examples; concrete (sanitized) examples would help adopters.
- **A "common smells" doc** — patterns that signal the methodology is being misapplied (e.g., "every epic is P1," "no one ever releases a lock," "memory directory has 300 stale entries"). Diagnostic guide.

None of these are urgent. They're future work if and when adopters report needing them.

---

## How to read this evaluation

If you're considering adopting the methodology: this is the honest assessment after real-world use. The methodology works. It has gaps that have been addressed. It still has limits that are by design.

If you're already using the methodology: scan the "What's still missing (acknowledged, not addressed)" section to see what genuine project-specific work you'll need to do on your own.

If you're maintaining the methodology: this doc plus the memory entries that triggered each addition are the input for the next revision. Update when you learn something new from real practice.

---

## Provenance

This evaluation was produced by running the methodology against the source project that originated it. The findings are real; the project name is deliberately omitted because the methodology is meant to transplant. If you want to see the patterns in a real codebase, fork the methodology, apply it, and produce your own evaluation.
