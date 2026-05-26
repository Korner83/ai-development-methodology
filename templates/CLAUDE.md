# CLAUDE.md

<!--
  PROJECT-INSTRUCTION FILE — STARTER TEMPLATE

  This is the single file every contributor (human or AI agent) reads
  on every session. Keep it under ~300 lines. Move detail into the
  methodology docs (docs/methodology/) and the memory directory.

  Replace every <<placeholder>> with your project's specifics. Delete
  sections that genuinely don't apply. Add project-specific sections
  at the bottom as needed.

  See docs/methodology/08_lessons_and_memory.md for the full guidance
  on what belongs here vs. in memory.

  Delete this comment block before committing.
-->

This file provides guidance to contributors (human and AI) when working in this repository.

---

## Project overview

<<One paragraph. What is this product? Who uses it? What is distinctive about it?>>

---

## Working principles

These four principles bind every contribution. They are not aspirational; they are barriers. If a change violates one, the change is wrong even if it "works." See [docs/methodology/06_working_principles.md](docs/methodology/06_working_principles.md) for the full discussion.

### 1. Think before coding

State assumptions explicitly. If uncertain, ask. If multiple interpretations exist, surface them. Stop when confused; name the confusion before writing code.

### 2. Simplicity first

Write the minimum code that solves the problem. No abstractions for single-use code. No flexibility, configurability, or error handling for scenarios nobody asked for. If it could be half the lines, rewrite it.

### 3. Surgical changes

Touch only what the task requires. Match existing style. Do not refactor unrelated code. Mention drive-by observations; do not silently fix them. Every changed line traces to the task.

### 4. Goal-driven execution

Transform every task into a verifiable goal with a known stopping condition. "Fix the bug" → "write a test that reproduces it, then make it pass." For multi-step work, state a plan with a verify step per item.

---

## Methodology

The way work is organized and executed on this project is codified in [`docs/methodology/`](docs/methodology/) — 13 docs (00–12) covering strategy, pillars, epics, items, locks, working principles, Definition of Done, lessons and memory, git workflow, testing and verification, human roles, and milestone evaluation.

The methodology docs are the **authoritative source** for HOW work is done here. When you have a process question — how to file an item, what counts as "done," how to coordinate parallel sessions — the methodology doc is where the answer lives.

Operating contract for every change:

- **Before picking up any backlog item:** follow the lock protocol in [docs/methodology/05_locks_and_parallel_work.md](docs/methodology/05_locks_and_parallel_work.md). Read the `Lock:` field; if held by another live session, skip; if free, acquire atomically before starting work.
- **During every change:** apply the four working principles above.
- **Before marking any item done:** pass every gate in [docs/methodology/07_definition_of_done.md](docs/methodology/07_definition_of_done.md). The hard rule — `Status: done` requires `Test: pass` — is absolute.
- **When a recurring lesson emerges:** file a memory entry per [docs/methodology/08_lessons_and_memory.md](docs/methodology/08_lessons_and_memory.md).

---

## Tech stack

<<List the languages, frameworks, key libraries, and platforms. Keep it short — readers should be able to scan it. Detail belongs in architecture docs.>>

- **Frontend:** <<framework + key libs>>
- **Backend:** <<framework + key libs>>
- **Database:** <<engine + version>>
- **Build / package management:** <<tool>>
- **Testing:** <<framework>>
- **Deployment:** <<target + tooling>>

---

## Monorepo / project structure

<<Tree of the top-level layout. Keep to two or three levels deep — readers can drill in for details.>>

```
<<project-root>>/
  <<apps/web/>>            # <<one-line purpose>>
  <<apps/api/>>            # <<one-line purpose>>
  <<packages/shared/>>     # <<one-line purpose>>
  docs/methodology/         # the methodology (see above)
  backlog/                 # epics and items
  memory/                  # lessons-learned memory entries
  CLAUDE.md                # this file
```

---

## Commands

<<The handful of commands every contributor runs daily. Keep it tight — readers should be able to get a dev environment running from this section alone.>>

```bash
# Install
<<install command>>

# Run dev environment
<<dev command>>

# Run tests
<<test command>>

# Build for production
<<build command>>

# Lint / typecheck
<<lint command>>
```

### Dev server notes

<<Anything non-obvious about running locally: ports, required env vars, services that must be running, common pitfalls.>>

---

## Architecture summary

<<Two or three paragraphs describing the high-level architecture: services, data flow, key abstractions, integration points. Detail lives in dedicated architecture docs; this is the orientation a new contributor needs in their first 10 minutes.>>

---

## Code conventions

<<How to write code in this project. Keep this concise — extensive style guides live in the linter config, not here.>>

- **Language:** <<strict mode? specific subset?>>
- **Naming:** <<camelCase? snake_case? domain-specific conventions?>>
- **File organization:** <<one component per file? barrel exports? co-located tests?>>
- **Formatting:** <<tool>> — runs on pre-commit.
- **Imports:** <<order conventions? path aliases?>>

### Frontend patterns

<<Patterns specific to the UI layer: state management, routing, component organization, styling approach. One paragraph or a short list.>>

### Backend patterns

<<Patterns specific to the server layer: route organization, validation, error handling, ownership boundaries. One paragraph or a short list.>>

### Data / database conventions

<<Schema rules, migration discipline, data ownership boundaries, important table groupings.>>

---

## Backlog and methodology pointers

- **Backlog lives at:** [`backlog/`](backlog/). Each epic has its own folder; items live in `BACKLOG.md` inside the epic folder. See [docs/methodology/03_epics.md](docs/methodology/03_epics.md) and [docs/methodology/04_backlog_items.md](docs/methodology/04_backlog_items.md).
- **Epic rollup:** [`backlog/EPICS.md`](backlog/EPICS.md). One-page index of every epic with status and counts.
- **Pillars live at:** [`docs/pillars/`](docs/pillars/) (if applicable). See [docs/methodology/02_pillars.md](docs/methodology/02_pillars.md).
- **Strategy lives at:** [`docs/strategy/`](docs/strategy/) (if applicable). See [docs/methodology/01_strategy.md](docs/methodology/01_strategy.md).
- **Memory (lessons learned) lives at:** [`memory/`](memory/) (or wherever your agent's memory is configured). See [docs/methodology/08_lessons_and_memory.md](docs/methodology/08_lessons_and_memory.md).

---

## Hard rules

A short list of "never do this in this project" rules. Each one exists because the absence of it has caused real damage. Add to this list as you accumulate lessons.

- **Never force-push to `<<main-branch>>`.** See [docs/methodology/09_git_workflow.md](docs/methodology/09_git_workflow.md).
- **Never commit directly to `<<main-branch>>`.** All work lands via PR.
- **AI agents never run production deploys.** Production deploy command: `<<command>>` — user-only.
- **Never skip pre-commit hooks** (`--no-verify`) without explicit authorization. Fix the hook failure instead.
- **Never bypass the Definition of Done.** `Status: done` requires `Test: pass` (or two narrow exceptions documented in `methodology/04_backlog_items.md` "The hard rule": `manual-verified` with a regression-needed follow-up item, or `n/a` with a body-documented reason). Never flip from `not-tested`, `pending`, `partial`, `fail`, or `regression-needed`.
- **<<project-specific hard rule>>** — <<why this exists>>.
- **<<project-specific hard rule>>** — <<why this exists>>.

---

## UX / design principles

<<If applicable: top-level design philosophy. The handful of rules that apply to every UI decision. Detail belongs in the design system docs; the headline rules go here.>>

- **<<Principle 1>>:** <<one-line explanation>>
- **<<Principle 2>>:** <<one-line explanation>>
- **<<Principle 3>>:** <<one-line explanation>>

---

## Security and privacy

<<If applicable: the non-negotiable security/privacy boundaries. Detail in dedicated docs; the rules of engagement go here.>>

- **<<Boundary 1>>:** <<one-line explanation>>
- **<<Boundary 2>>:** <<one-line explanation>>

---

## What to read next

- [docs/methodology/00_README.md](docs/methodology/00_README.md) — the methodology entry point. Read this if you're new to the project.
- [docs/methodology/06_working_principles.md](docs/methodology/06_working_principles.md) — the four principles, expanded.
- [docs/methodology/07_definition_of_done.md](docs/methodology/07_definition_of_done.md) — the gates every item passes before "done."
- [memory/MEMORY.md](memory/) — the index of project-specific lessons learned.

When in doubt about HOW to do something, consult the corresponding methodology doc — it is the source of truth for process.
