# Changelog

All notable changes to this methodology are documented here.
Updated per the Definition of Done in [methodology/07_definition_of_done.md](methodology/07_definition_of_done.md).

This is the single source of truth for the changelog.

---

## [Unreleased]

(nothing yet)

---

## v1.4.2 — 2026-05-25

### Docs — Diagram refinements: pillars labeled as long-term goals + items sized by contributor type (2026-05-25)

Two diagram-label refinements based on maintainer feedback:

- **Pillars relabeled "long-term capability goals"** (was "capability layers · evergreen"). Both diagrams. Pillars are the closest thing the methodology has to long-term goals; making that explicit helps adopters see the link to their own product roadmap.
- **Items sized by contributor type, not by calendar.** Was "1–2 week units of work"; now "1–2 weeks for humans · daily for AI" (Diagram 1) and "sized to the contributor: 1–2 weeks for humans · daily for AI" (Diagram 2). Reflects what's true in mixed-contributor projects — the same backlog item that takes a human 1–2 weeks of focused work might take an AI agent hours-to-days. Item *scope* is the constant; calendar time is contributor-dependent.

Diagram-only change in this release. If the underlying methodology docs (especially `methodology/04_backlog_items.md` and the "Effort: XS–XL" sizing guidance) should be updated to reflect contributor-aware sizing more explicitly, that's a separate follow-up.

---

## v1.4.1 — 2026-05-25

### Docs — Two Mermaid diagrams added to README + v1.3.1 → v1.4.0 reference bumps (2026-05-25)

Two diagrams give visitors and adopters a visual entry point alongside the prose:

**New section "How it fits together"** (right after TL;DR) — conceptual diagram showing the four planning layers (Strategy → Pillars → Epics → Items) cascading downward, three discipline overlays (Working Principles / Definition of Done / Memory) binding every change, and three operational supports (Locks / Git Workflow / Fix-Test Loop) making the day-to-day navigable. Colors map to function (planning blue, disciplines amber, supports green).

**New section "How the work cascades"** (right after "What's in the repo") — data-cascade diagram with file paths, from Step 0 (your brief, BEFORE the methodology kicks in) → `docs/strategy/` → `docs/pillars/` → optional `docs/planning/` → `backlog/epics/NN-slug/` → individual BL-XXXX items inside each epic's `BACKLOG.md`. Includes the four-file shape of each epic folder (README/BACKLOG/ARCHIVE/FUTURE) and the item frontmatter schema (Pillar / Status / Test / Lock / Priority / Effort). Explicitly notes the "one ticket type" design — feature, bugfix, task, and user-story-shaped items all use the same BL-XXXX format, no Jira-style taxonomy.

Both diagrams use Mermaid markdown blocks (no separate image files) so they render natively on GitHub, edit as text, and live in git — consistent with the methodology's "markdown + git only, no SaaS" framing.

**Mechanical:** two stale "v1.3.1" references in the README (TL;DR + Status section) bumped to v1.4.0. Should have been bumped at v1.4.0 ship; folded in here.

---

## v1.4.0 — 2026-05-25

### Feat — Four methodology additions: stdlib growth loop, verification taxonomy, brownfield onboarding, decision-ownership matrix (2026-05-25)

Closes four real gaps surfaced by external research comparing this methodology to its peers (GitHub Spec Kit, BMAD Method, Geoffrey Huntley's Ralph loop and stdlib pattern, et al.). Each addition is a section within an existing methodology doc — no new doc number, no restructure.

**`08_lessons_and_memory.md` — new section "The promotion path: from one-off correction to durable rule"** (~70 lines)

Names the explicit promotion loop: one-off correction → memory entry → instruction file → methodology addition (and the reverse loop for demotion and deletion). The existing doc already had two of the four stages (Trigger 2: "Same correction 2+ times" → memory; "Memory as a leading indicator" → methodology). The new section adds the missing middle stage (memory → instruction file) and frames the whole pipeline as a named loop. Peers — particularly Geoffrey Huntley's [stdlib pattern](https://ghuntley.com/specs/) — make this loop the centerpiece of their methodology; this addition adopts the discipline without dropping the existing planning hierarchy.

**`10_testing_and_verification.md` — new section "Verification levels: matching depth to risk"** (~80 lines)

Graduates the binary `Test: pass` field into a five-level taxonomy (L0 type check → L1 automated tests → L2 actual-UI loop → L3 cross-AI validation → L4 user testing). Includes a mapping from change class (typo / refactor / new feature / schema migration / security-sensitive / production hotfix) to required levels, with an optional level annotation in the item's `Test:` field (e.g., `Test: pass (L3)`). The DoD's hard rule (`Status: done` requires `Test: pass`) is unchanged — the taxonomy clarifies *what `pass` means* for the specific change. Closes the "unusually strict for trivial work / unusually loose for risky work" gap surfaced in peer-methodology research.

**`00_README.md` — new section "Brownfield reality check (when adoption fights headwinds)"** (~70 lines)

Explicit staging (Stage A → E) for adopting the methodology in legacy projects where the team hasn't asked for new process: start with personal-discipline adoption, add the lock protocol when AI parallelism creates collisions, apply DoD to a single epic, open the planning layer for new work only, backfill pillars and strategy last. Includes "what NOT to do" anti-patterns (don't reformat the existing backlog all at once, don't ask non-contributors to read 12 docs, don't litigate the past) and a "when brownfield adoption fails" honest failure-mode section. The existing "Adopting in an existing project" 8-step list remains — the new section addresses harder cases where that gentle staging assumes too much buy-in.

**`11_human_roles.md` — new section "The decision-ownership matrix"** (~100 lines)

A RACI-lite matrix mapping 21 decision types (code style → naming → refactor → bug fix → new feature → library choice → schema → API shape → auth → architecture → production deploy → destructive operations → strategy → pricing → hiring → legal) to five ownership columns (AI proposes / AI decides / Human reviews / Human decides / Human-only). Includes guidance on how to adapt for project risk tolerance, hard-coded rightmost-column rows (production deploys, force-push, destructive operations) that match the methodology's existing hard rules, an "ownership is unclear" escalation protocol, and an explicit cross-reference to the memory promotion loop above. Peer methodologies (per external research) consistently flagged this as the #1 missing artifact for teams adopting AI-collaborated workflows.

**Mechanical updates:**

- `README.md` line-count claim refreshed (~7,100 → ~7,500). The four additions added ~320 lines of methodology content; longest doc remains `04_backlog_items.md` at 778 lines.
- No new doc files. The four additions all extend existing docs. Doc count stays at 12 (00–11).

Discovery: all four additions came from a research pass that surveyed ~14 peer methodologies including GitHub Spec Kit, BMAD Method, Ralph loop, stdlib pattern, AGENTS.md standard, GSD, nano-spec, plus academic papers (Agentsway, Agile V) and vendor docs (Anthropic, OpenAI). The gaps these additions close were ranked by recurrence across peers — these were the four that came up most often.

### Docs — README rewrite (benefit-led + competitive context) + new `templates/AGENT_KICKOFF.md` (2026-05-24)

README rewritten — cut from 348 to 220 lines (~37% compression). Motivated by external feedback that the README "felt AI-written" and was missing benefit-led framing plus context on how this methodology relates to the wider ecosystem of AI-collaboration methodologies that now exists.

**Added:**

- **"What you get"** — a benefits-led section (10 bullets) right after the TL;DR. Each bullet maps to a specific methodology element (DoD hard rule, locks, memory entries, working principles, fix-test loop, challenge-before-consenting, cross-AI validation, vendor-neutral templates). Adopters see the value-prop before the mechanics.
- **"What's similar, what's different"** — honest comparison to 7 peer methodologies discovered via external research: [GitHub Spec Kit](https://github.com/github/spec-kit) (~106k★), [BMAD Method](https://github.com/bmad-code-org/BMAD-METHOD), Geoffrey Huntley's [Ralph loop](https://ghuntley.com/ralph/) and [stdlib pattern](https://ghuntley.com/specs/), the [AGENTS.md standard](https://agents.md/), [Get Shit Done (GSD)](https://www.prafulls.me/blogs/gsd-spec-driven-development), and [nano-spec](https://github.com/tao-hpu/nano-spec). Includes explicit "this methodology has 0 stars at the time of writing and is solo-maintained" disclosure so the comparison isn't oversold.
- New **`templates/AGENT_KICKOFF.md`** — the 40-line Step 2 planning-mode prompt that was bloating the README, extracted to its own file with a pointer from the README.

**Compressed:**

- "Why this exists" table: 16 rows → 10 highest-value rows; 3-column format (Problem / Why / Solution) → 2-column (Problem → Solution).
- "Why it works (the short version)" subsection removed — meta-commentary that just rephrased the table.
- "A small tip that pays off" subsection removed — the same advice already lives in Step 3's four-phrases bullet list.
- Step 0 prose: ~25 lines → 1 paragraph (substance kept, repetition dropped).
- Step 2 prompt: 40+ lines → 1 sentence + link to `templates/AGENT_KICKOFF.md`.
- "Permissions and vendor compatibility": ~13 lines → 5 lines, same content denser.
- Two parallel comparison sections ("What makes this different" + "How this relates to specific methodologies") merged into the new "What's similar, what's different" section. The Agile/Scrum/Kanban/Shape Up/XP comparison was replaced with the contemporary AI-methodology landscape (Spec Kit, BMAD, Ralph, etc.) — peers that didn't exist when v1.0 was framed.

Repo total now: 7,152 lines across 21 files (the README displays a tree of 20, excluding the `.github/FUNDING.yml` metadata file from the prior commit).

Research surfaced ~14 peer methodologies (Spec Kit alone has ~106k stars), confirming the README needed to position this work in the current landscape rather than only against pre-AI methodologies. Several peer methodologies provided concrete language for distinguishing strengths — most notably the "cheating agent" anti-pattern, file-based locks for humans+agents using the same protocol, and the challenge-before-consenting copy-paste prompt, none of which appear in peer methodologies surveyed.

---

## v1.3.1 — 2026-05-24

### Docs — Add "Permissions and vendor compatibility" section to README (2026-05-24)

New README section addresses three reader questions: (1) what the CC BY 4.0 license actually permits in practice (private, commercial, open-source use; fork, modify, redistribute, charge for derivatives; ship inside a paid product; use with paid, free, self-hosted, or on-prem AI tools — only obligation is attribution); (2) whether the methodology is compatible with AI tool vendor acceptable-use policies (Anthropic, OpenAI, Google, Cursor, Continue, Aider, etc.) — yes, because the methodology calls no vendor API and asks AI agents to do nothing restricted under any major AUP, and the project-instruction file (`CLAUDE.md`, `AGENTS.md`, `.cursorrules`, `.continue/context.md`) is the vendor-supported mechanism for project context; (3) how the methodology's safety practices (no production deploys by agents, no force-push to trunk, no hook bypass, no destructive commands autonomously, branch protection + PR-only by default, cross-AI validation + user testing as final gates) align with vendor AUPs rather than conflicting with them.

Includes a clear "not endorsed by, partnered with, or affiliated with any AI tool vendor" disclaimer and a "not legal advice" disclaimer for adopters operating under specific compliance requirements (regulated industry, data residency, classified work, government procurement).

Added because adopters considering the methodology were uncertain whether using it with their preferred AI tool would put them at odds with vendor policies. The answer is no, and the answer should live in the README rather than be left for adopters to infer.

### Chore — Honesty pass on v1.3.0 (2026-05-24)

Three small fixes for facts that drifted or never matched reality. The methodology applies to itself; a repo whose README mis-states its own size and whose CHANGELOG links to a deleted file fails its own DoD Gate 4.

- `README.md:84` — line-count claim updated from ~6,100 to ~7,100 (actual: 7,115 lines across 19 files; v1.3.0's "refreshed" claim was 16.5% low). "Longest single doc" updated from ~700 to ~780 (actual longest: `methodology/04_backlog_items.md` at 778 lines).
- `README.md:263–267` — "The two templates have identical content" softened to "substantially identical." AGENTS.md is the superset by 22 lines (~11%), with vendor-neutral sections on plan-mode discipline, tool-install guidance, verification order, and an operational-safety rule that Claude Code's harness covers implicitly. Symlink advice updated to recommend pointing CLAUDE.md → AGENTS.md so the superset stays the source of truth.
- `CHANGELOG.md:151` — broken link `[EVALUATION.md](EVALUATION.md)` in the v1.0.0 historical entry rewritten to plain text + parenthetical pointing to the v1.3.0 removal entry. Historical narrative preserved; broken link removed.
- `README.md:19, 334` — two stale "Currently at v1.2.0" references bumped to v1.3.1 (this release). These should have been bumped at v1.3.0 ship; they weren't, completing the picture of v1.3.0 documentation drift that this honesty pass closes.

Discovered via an external fresh-eyes audit on 2026-05-24 (the same day v1.3.0 shipped). Each fix would have been caught at the time by stricter Gate 4 / Gate 5 application; this release closes that gap and the audit findings are now folded back into the project's working practice.

---

## v1.3.0 — 2026-05-24

### Docs — README: new Step 0 (the brief is a prerequisite) + Step 3 made realistic (2026-05-24)

Two substantive README changes that close a methodology-honesty gap.

**New Step 0 — "Before this methodology kicks in (the brief)":** explicit acknowledgment that the methodology does NOT solve the upstream work — product / market / user / business / tech stack decisions. Lists the 7 questions a project needs written, defensible answers to before Step 1 can produce anything useful (what / who / success / competitors / viability / stack / capability layers → pillars). Names a common failure mode (treating `docs/strategy/` and `docs/pillars/` as a substitute for upstream thinking rather than the *recording layer* for already-validated decisions) and the resulting velocity illusion (shipping confidently-built wrong product). Mentions Lean Canvas, JTBD interviews, Five Forces, etc. as candidate frameworks without prescribing.

**Revised Step 3 — "Ongoing development":** removed the unrealistic "paste this 30-line prompt at the start of every session" framing. The project-instruction file (`CLAUDE.md` / `AGENTS.md`) is what AI tools read automatically; nothing to paste. Replaced with four short steering phrases for when the AI drifts ("Do you have any questions?", "What's wrong with this plan?", "Use plan mode", "Stop — split this item"). AUTONOMOUS_LOOP remains the explicit-paste path for dedicated milestone work; everything else runs from the instruction file.

Adjacent cleanup: the "small tip that pays off" intro no longer references a "prompt above."

### Docs — README "How this relates to specific methodologies" comparison (2026-05-24)

The "What makes this different" section now includes a comparison table mapping the major prior methodologies (Agile Manifesto, Scrum, Kanban, Shape Up, Extreme Programming) to what this methodology adopts vs. what it does differently. Plus a coexistence paragraph: runs inside Scrum (sprints as scheduling overlay), layers on top of Kanban (adds upstream planning), complements XP directly, not designed to replace SAFe or other enterprise frameworks.

Addresses the common first-read question: "where does this fit relative to what I already know?"

### Chore — Remove `EVALUATION.md` from public repo (2026-05-24)

The gap-analysis report that triggered v1.1.0 and v1.2.0 is no longer worth carrying as a top-level repo artifact. The gaps it identified are mostly closed (see those releases); a stale "here's what's missing" doc at the root would mislead new readers about the current state of the methodology.

Internal copy preserved as a dated snapshot in the source project's docs folder. Ongoing maintenance flows through this `CHANGELOG.md` instead — release-by-release, in the format the methodology itself prescribes (see [methodology/07_definition_of_done.md](methodology/07_definition_of_done.md) "Changelog — the practical patterns").

`README.md` updated: four references to `EVALUATION.md` rewritten (now pointing at `CHANGELOG.md` where appropriate); file tree no longer lists `EVALUATION.md`; line count refreshed (~6,100 lines across 19 files).

---

## v1.2.0 — 2026-05-24

### Feat — Backlog mechanics: practical artifacts from real-practice comparison (2026-05-24)

Closes nine gaps identified by comparing the methodology's backlog spec against an actual production project's backlog. The methodology had the conceptual model right; these additions provide the operational templates and recovery guidance that real practice has invented.

**`methodology/03_epics.md` additions:**

- **Rollup table now has a "Next milestone" column** — human-readable "what's the next visible shipment" gives at-a-glance status without opening the epic. Open/Done collapsed to one combined column to keep the table readable.
- **Pillar Coverage section** — inverse table showing which epics touch each pillar. Useful for "what's active on pillar X right now?" queries and pillar audits.
- **Last-refresh metadata** — pattern for the freshness note at the top of `EPICS.md` so readers see what shipped since the last sweep and any known count drift.
- **`TEST.md` template** — proper template with two sections: "Acceptance tests for exit criteria" + "Regression scenarios to protect (with last-verified date)." Plus when-to-use and when-to-skip guidance.

**`methodology/04_backlog_items.md` additions:**

- **`BACKLOG.md` structure section** — defines the summary-table-at-top pattern (one line per item: `ID | Title | Priority | Effort | Status`) before the detailed item blocks. Massively improves scannability for epics with 20+ items.
- **Coupled fields: `Lock` + `Status` + `Test`** — table of valid combinations for typical outcomes (item picked up, code merged, blocked, etc.). The three fields are coupled; the table shows what valid joint states look like for each outcome.
- **"When things go sideways" recovery patterns** — unified guidance for: tests fail (keep lock, fix in same PR), external blocker (release lock, set blocked, leave `**Blocker:**` note), scope creep (stop, split, file follow-ups), expired-own-lock recovery, reopening a `done` item.
- **Greppable metadata: specific `rg` query patterns** — example commands for "all P0 items," "all unlocked items," "all in-progress items," "all blocked items with context," "find next BL-ID," etc. Plus the ID collision rule.
- **`FUTURE.md` numbering: two valid schemes** — names the choice between monotonic project-wide IDs vs. epic-scoped F-prefixed IDs. Both are valid; project picks one and documents it.
- **TL;DR for a fresh contributor** — one-paragraph quick-start so a contributor (human or AI) can pick up an item cold without reading the rest of the doc.

Synthesized from focused gap analysis between the methodology's backlog docs (03_epics, 04_backlog_items) and a real production project's `backlog/README.md` + `EPICS.md` + sample epic folder.

### Chore — Document workflow exception in `STATUS.md` (2026-05-24)

The methodology's own [09_git_workflow.md](methodology/09_git_workflow.md) requires PR-only merges to the trunk and forbids direct commits, but this repo is solo-maintained and has been using direct-to-main commits since v1.0.0. `STATUS.md` now names the exception explicitly: why it's deliberate, why the rule's reason-for-existing doesn't apply in a solo-maintained context, and the trigger for revisiting (second contributor joins → adopt branch protection + PR flow). Frames the exception via the methodology's own authority hierarchy.

Also fixed a stale `MIT license` reference in `STATUS.md` (license is CC BY 4.0; the wrong name slipped through when the license was switched from MIT during v1.0 prep).

---

## v1.1.0 — 2026-05-24

### Feat — New doc `methodology/11_human_roles.md` (2026-05-24)

Adds the methodology's missing "human side": how human contributors stay meaningfully engaged when AI agents do most of the implementation work. The bottleneck has shifted from execution to specification and supervision; this doc says what humans *do* now that AI does most of the typing.

Sections include: the shifted bottleneck (code-as-commodity vs. spec-as-asset), the new supervisory layer (agent-sized chunks, when to let the AI run vs. intervene, prompt-refinement over manual fixes, pre-implementation architectural review), four anti-patterns (the cheating agent, the yes-man / agreement bias, the stranger in your own code, the loss of tribal knowledge), specification as the primary artifact (state machines, decision tables, schema-first definitions, Given/When/Then), and the new human skills (architectural thinking, unambiguous specification, supervisory skill, taste, system thinking across abstraction layers).

Synthesized from external analysis of AI integration in a software team plus the methodology's existing patterns.

### Feat — `methodology/06_working_principles.md` adds "Challenge before consenting" (2026-05-24)

Per-decision defense against the AI agreement bias. AI models default to helpful agreement; when the stakes are high, invert the default and prompt the AI to challenge rather than confirm. Includes copy-paste prompt ("what's wrong with this plan? what's the strongest case AGAINST? what would a senior engineer poke holes in?").

When to use: before approving plans, mid-incident, when evaluating architectures, after a confident-sounding answer, when you notice you're agreeing with the AI a lot.

### Feat — `methodology/10_testing_and_verification.md` adds "The cheating agent" anti-pattern (2026-05-24)

Warns about the failure mode where AI writes both the implementation and the tests that validate its (broken) implementation — the green test suite looks like done; no human in the loop catches it. Defenses: test-first / TDD as an AI-collaboration discipline, cross-AI validation of test suites, human review of test names and acceptance criteria, periodic random audits of AI-written test/implementation pairs.

Includes the deeper implication: the test suite is the durable artifact (survives language/framework migration when it captures intent correctly); implementation is replaceable. Test quality matters MORE in an AI-assisted workflow, not less.

### Chore — Cross-doc updates

- `methodology/00_README.md`: doc 11 added to doc index; mental model now includes "the applied dimension"; "Starting a new project from scratch" reading order extended to include doc 11.
- `README.md` (repo): file tree updated (12 docs instead of 11); total line count updated; "Why this exists" table grew by three rows (humans drift from loop, AI-agreement bias, cheating agent) pointing at the relevant docs.
- `templates/AUTONOMOUS_LOOP.md`: "Pairing with plan mode" section now references the challenge-before-consenting pattern.

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

`EVALUATION.md` was the honest field report shipped in v1.0.0: what the methodology covered, what was missing when compared to real practice, what got added in this release, and what remained deliberately out of scope. Coverage mapping plus practical pros and cons. (Removed in v1.3.0 — see that entry above for rationale.)

### Chore — Repo scaffolding

- [LICENSE](LICENSE) — CC BY 4.0 (attribution-required).
- [README.md](README.md) — TL;DR, problems-it-solves table, kickoff guide with AI prompts, AI tool support, attribution guidance.
- [STATUS.md](STATUS.md) — maintenance posture (lean — PRs welcome but no SLA; CC BY 4.0 means anyone can fork).

### Out of scope on this release

- Project-specific deploy commands, monitoring stacks, CI providers — by design (project choice).
- An `examples/` folder with anonymized real artifacts — future work, noted in EVALUATION.md.
- A one-page CHEATSHEET — README's TL;DR currently serves this; revisit if requested.
