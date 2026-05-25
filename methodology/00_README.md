# 00 — Methodology

> A self-contained, portable methodology for running a software project end-to-end. Designed for teams where humans and AI agents collaborate as peers. The same set of practices works whether the contributors are all human, all AI, or any mix.

This is the index. It explains why the methodology exists, how the pieces fit together, and how to read the rest of the docs.

---

## Why this exists

Long-running software projects fail in predictable ways:

- **Direction drifts.** Without an explicit long-term anchor, every quarter's plan is litigated from scratch.
- **Work fragments.** Without a layer between "the vision" and "this week's bug," contributors cannot see how their task ladders up to anything.
- **Done-ness is fuzzy.** Items are marked complete while still buggy, untested, or undocumented. Trust in the backlog erodes.
- **Lessons evaporate.** The same mistake gets made every six months because no one wrote down what worked or what burned.
- **Parallel contributors collide.** Especially with AI agents in the loop, two contributors silently pick the same item and produce conflicting work.

This methodology is a set of practices that prevent each of these. Each doc in the set covers one practice in detail. Read together, they describe a complete, low-overhead system that scales from a solo contributor to a team mixing humans and AI agents.

The whole system runs on **markdown files plus git.** No external services. No specialized tooling. The practices are deliberately simple because complex practices do not survive contact with reality.

---

## The mental model

The methodology has two interlocking mental models. Once you have both, the docs are easier to navigate.

### Four layers of planning

Work cascades through four layers, each answering a different question and operating on a different time horizon.

| Layer | Question it answers | Time horizon | Lives in |
|-------|---------------------|--------------|----------|
| **Strategy** | *Why does this product exist? Who is it for? How does it make money?* | Years | `docs/strategy/` |
| **Pillars** | *What capability layers does the product need to deliver the strategy?* | Years (evergreen) | `docs/pillars/` |
| **Epics** | *What 3–12-week batches of work advance the pillars?* | Months | `backlog/epics/<NN>-<slug>/` |
| **Items** | *What unit of work — 1–2 weeks max — can a contributor pick up?* | Days to weeks | `backlog/epics/<NN>-<slug>/BACKLOG.md` |

Each layer constrains the one below. Strategy bounds which pillars matter. Pillars bound which epics make sense. Epics bound which items get filed. The chain prevents the most common scope-creep failures: items that don't ladder up to anything, epics that orphan themselves, pillars that don't operationalize strategy.

### Three discipline overlays

Three practices wrap all four planning layers. They are orthogonal — they apply at every level — and each addresses a different category of failure.

| Discipline | What it prevents | Doc |
|------------|------------------|-----|
| **Working principles** | Speculative abstraction, scope creep, drive-by edits, open-ended exploration. | [06_working_principles.md](06_working_principles.md) |
| **Definition of Done** | "Done in name only" — items that look complete but are buggy, untested, undocumented. | [07_definition_of_done.md](07_definition_of_done.md) |
| **Lessons-learned memory** | The same mistakes repeating across sessions and contributors. | [08_lessons_and_memory.md](08_lessons_and_memory.md) |

These are not separate workstreams. They are constraints that bind every contribution: every change is shaped by the working principles, every item passes the Definition of Done, every recurring lesson is captured in memory.

### Plus: the applied dimension

The four layers and three disciplines describe *how the work flows.* [11_human_roles.md](11_human_roles.md) describes *how humans stay meaningfully involved* when AI agents do most of the implementation — the supervisory layer, the spec-as-primary-artifact shift, anti-patterns (cheating agent, yes-man, stranger in own code, tribal knowledge loss), and the skills that grow in value vs. those that don't.

Read it alongside the disciplines for the full picture of working in this methodology.

---

## How the layers connect

```mermaid
flowchart TB
  subgraph PLANNING["Planning (cascades downward)"]
    direction TB
    S[Strategy<br/>vision, phases, business outcomes] --> P[Pillars<br/>capability layers — evergreen]
    P --> E[Epics<br/>3–12 week delivery containers]
    E --> I[Items<br/>1–2 week units of work]
  end

  subgraph DISCIPLINE["Disciplines (apply everywhere)"]
    direction TB
    W[Working principles]
    D[Definition of Done]
    M[Lessons and memory]
  end

  W -.applies to.-> S
  W -.applies to.-> P
  W -.applies to.-> E
  W -.applies to.-> I

  D -.gates.-> I
  D -.gates.-> E

  M -.captures lessons across.-> S
  M -.captures lessons across.-> P
  M -.captures lessons across.-> E
  M -.captures lessons across.-> I

  subgraph SUPPORT["Operational supports"]
    direction TB
    L[Locks — concurrency control]
    G[Git workflow]
    T[Testing and verification]
  end

  I -.uses.-> L
  I -.recorded in.-> G
  I -.verified by.-> T
  D -.enforces.-> T
```

The diagram shows three groupings:

- **Planning** flows top-down. Strategy informs pillars; pillars are advanced by epics; epics contain items.
- **Disciplines** apply across the planning stack. The working principles bind every contribution at every layer. The Definition of Done gates items and epics. Memory captures lessons that emerge anywhere.
- **Operational supports** make the system work day-to-day. Locks coordinate parallel contributors at the item level. Git is the substrate that records everything. Testing and verification operationalize the DoD's `Test: pass` requirement.

Read across the docs and you see the same flow: planning artifacts are produced and consumed in the cascade; disciplines apply at every layer; operational supports make the daily work navigable.

---

## How to read these docs

Different readers need different paths. Pick the one that fits your situation.

| Reader | Reading order |
|--------|---------------|
| **New contributor on an existing project** | 00 → 06 → 07 → 04 → 05 → 09 → 10. Skim 01–03 for context but don't memorize them; the work you'll touch first is at the item layer. |
| **Picking up a specific item to work** | 04 → 05 → 07 → 10. You need to know the item format, how to acquire it, what "done" means, and how to verify. |
| **Starting a new project from scratch** | 00 → 01 → 02 → 03 → 04 → 05 → 06 → 07 → 08 → 09 → 10 → 11. Top-down. You're building the whole stack. |
| **Setting up the disciplines on an existing project** | 06 → 07 → 08 → 09 → 10. The disciplines are the highest-leverage starting point — most projects already have some planning structure. |
| **Adapting the methodology to a different domain** | 00 → all docs in order. You'll need the whole picture to know what to keep and what to adapt. |
| **AI agent landing in a new session on this codebase** | 00 → 06 → 07. Then load specifics on demand based on the task. |
| **Auditing an existing project's process health** | 03 → 04 → 07 → 05. These layers contain the most observable signals of process health. |

The docs are designed to be readable in any order — each cross-links to the others. The reading paths above are recommendations to keep the first read efficient.

---

## Doc index

| Doc | Purpose (one line) |
|-----|---------------------|
| [00_README.md](00_README.md) | This file. Index, mental model, and how to read the set. |
| [01_strategy.md](01_strategy.md) | Long-term direction as versioned strategy docs: master plan + supporting research + phase roadmap. |
| [02_pillars.md](02_pillars.md) | Pillars as evergreen, sequentially-dependent capability layers between strategy and execution. |
| [03_epics.md](03_epics.md) | Epic charters as 3–12-week delivery containers with binary exit criteria, advancing one primary pillar. |
| [04_backlog_items.md](04_backlog_items.md) | The BL-### item format: fields, status enums, lifecycle, body sections, hard rules. |
| [05_locks_and_parallel_work.md](05_locks_and_parallel_work.md) | File-based locks with TTL that let multiple humans and AI agents work the same backlog safely. |
| [06_working_principles.md](06_working_principles.md) | The four principles every contributor follows: think first, simplicity, surgical changes, goal-driven execution. |
| [07_definition_of_done.md](07_definition_of_done.md) | The six gates an item must pass before `Status: done`. The hard rule that prevents done-in-name-only. |
| [08_lessons_and_memory.md](08_lessons_and_memory.md) | Two-layer memory: a project instruction file plus a per-agent memory directory of focused entries. |
| [09_git_workflow.md](09_git_workflow.md) | Branch protection, PR discipline, worktrees for parallel agents, destructive-command rules, deploy boundaries. |
| [10_testing_and_verification.md](10_testing_and_verification.md) | Automated tests plus the actual-UI fix-test loop. What "tests pass" does and does not prove. |
| [11_human_roles.md](11_human_roles.md) | How humans stay meaningfully involved when AI agents drive most of the implementation. Supervisory layer, spec-as-primary-artifact, four anti-patterns (cheating agent, yes-man, stranger in own code, tribal-knowledge loss), and the skills that matter now. |

Each doc is self-contained — you can read any one without having read the others, given the framing in this README. Cross-references between docs are markdown links.

---

## Quick concept reference

The most-used concepts across the set, defined once here for navigation.

### IDs and references

| Concept | Format | Example |
|---------|--------|---------|
| Pillar ID | `P<#>` | `P3` |
| Epic ID | `E<NN>` (zero-padded) | `E07` |
| Item ID | `BL-<###>` (zero-padded, monotonic, project-wide) | `BL-0428` |
| Holder ID (for locks) | `<agent-or-user>-<short-session-id>` | `claude-session-a4f2`, `alice-laptop` |
| Lock timestamp | ISO-8601, UTC, minute precision | `2026-04-18T16:30Z` |

### Status and metadata enums

| Field | Allowed values | Defined in |
|-------|----------------|------------|
| Item `Status` | `backlog`, `ready`, `in-progress`, `under-review`, `to-be-tested`, `done`, `blocked`, `rejected` | [04_backlog_items.md](04_backlog_items.md) |
| Item `Test` | `not-tested`, `pass`, `fail: <detail>`, `regression-needed` | [04_backlog_items.md](04_backlog_items.md) |
| Item `Priority` | `P0`, `P1`, `P2`, `P3` | [04_backlog_items.md](04_backlog_items.md) |
| Item `Effort` | `XS`, `S`, `M`, `L`, `XL` | [04_backlog_items.md](04_backlog_items.md) |
| Epic `Status` | `planned`, `active`, `done`, `parked` | [03_epics.md](03_epics.md) |
| Lock state | `—` (unlocked) or `<holder>@<timestamp>` | [05_locks_and_parallel_work.md](05_locks_and_parallel_work.md) |

### The hard rules

The smallest set of inviolable constraints. If a change violates one of these, it is wrong regardless of context.

| Rule | Where defined |
|------|---------------|
| `Status: done` requires `Test: pass`. No exceptions. | [04](04_backlog_items.md), [07](07_definition_of_done.md) |
| Never force-push to the trunk. | [09](09_git_workflow.md) |
| Never commit directly to the trunk. | [09](09_git_workflow.md) |
| AI agents never run production deploys. | [09](09_git_workflow.md) |
| Never bypass pre-commit hooks without explicit authorization. | [09](09_git_workflow.md) |
| Never steal a live lock; skip and pick another item. | [05](05_locks_and_parallel_work.md) |
| Items live in exactly one epic; new items always go into a specific epic. | [04](04_backlog_items.md) |
| WIP cap on active epics is real; new active epics require closing or parking another. | [03](03_epics.md) |
| The DoD's six gates apply to every item. No partial credit. | [07](07_definition_of_done.md) |

---

## How a project actually uses this set

A working day under this methodology looks like:

1. **Pull the latest from the repo.**
2. **Read [`EPICS.md`](#) for the current state of active epics.** Identify which epic you are picking from.
3. **Open the epic's `BACKLOG.md`.** Find an item with `Status: ready`, `Lock: —`, and no unresolved `Deps:`.
4. **Acquire the lock** ([05](05_locks_and_parallel_work.md)): set `Lock: <holder>@<now + TTL>`, set `Status: in-progress`, commit, push.
5. **Read the item body.** Understand the goal. State assumptions if any (Principle 1, [06](06_working_principles.md)).
6. **Transform the task into a verifiable goal** if not already one (Principle 4).
7. **Implement the change** following the working principles: minimum code, surgical scope, goal-driven.
8. **Run the full test suite** ([10](10_testing_and_verification.md)). Fix any failures.
9. **Perform the UI verification loop** for any user-observable change. Loop fix-test until clean.
10. **Update documentation** as needed: changelog, README, status doc.
11. **Open the PR** ([09](09_git_workflow.md)) with the standard body shape and test plan.
12. **Pass review.** Address feedback. Re-verify.
13. **Merge.** In the same PR (or in a follow-up commit): set `Test: pass`, `Status: done`, `Lock: —`. Move the item from `BACKLOG.md` to `ARCHIVE.md`. Update `EPICS.md` rollup counts.
14. **If a recurring lesson emerged**, file a memory entry ([08](08_lessons_and_memory.md)).
15. **Pick the next item.**

That is the loop. Strategy, pillars, and epics inform what items exist; items are how the work actually moves.

---

## How the system enables long-term, multi-session work

The methodology is designed for projects where work happens across:

- **Many sessions**, separated by hours, days, or weeks.
- **Many contributors**, mixing humans and AI agents.
- **Many tools**, as AI models, IDEs, and frameworks evolve over months.

Three mechanisms make this work:

1. **Plans persist in files, not in heads.** Strategy, pillars, epic charters, and items — all markdown in git. A contributor (human or AI) joining the project two weeks later reads the same artifacts the previous contributor wrote; nothing depends on a specific person's memory or running context.

2. **The backlog is the work queue.** An item filed by one contributor in one session can be picked up by another contributor in another session weeks later. The item's frontmatter (`Status`, `Lock`, `Test`, `Effort`, `Priority`) and body (goal, plan, verification) carry forward everything needed to resume. The [lock TTL](05_locks_and_parallel_work.md) ensures no item is held hostage by a contributor who never came back.

3. **The autonomous loop runs unsupervised between check-ins.** The [autonomous-loop prompt template](../templates/AUTONOMOUS_LOOP.md) lets an AI agent grind through the backlog toward a milestone-level stopping condition — picking the highest-impact-per-effort item ([the ROI heuristic](04_backlog_items.md#prioritization--the-roi-heuristic)), executing through the DoD, archiving, repeating. Suitable for long unattended runs (overnight, weekends, multi-day milestone pushes) where the human supervises at the milestone level rather than per-item. Blocked items leave the ready set via the normal protocol (see [`HUMAN_NEEDED.md`](04_backlog_items.md#human_neededmd--work-blocked-on-human-agency)) — the loop doesn't manage them; it just stops touching them.

The implication: **work compounds across time without depending on a single contributor's continuous attention.** Items dropped into the system today are picked up by whatever contributor is available tomorrow, next week, or next quarter.

### Common patterns that use this property

- **Drop-and-resume.** A user drops several items into the backlog with one AI session (sketching the work). Days later, an autonomous loop picks them up and executes. The user reviews the results at check-in time.
- **Hand-off between agents.** Agent A files items and partial designs in `docs/planning/`. Agent B (a different model, a different session, a different week) picks them up and completes the work.
- **Vendor switching.** Project moves from one AI tool to another. Because the methodology is markdown-and-git, the new tool reads the existing backlog, instruction file, and memory directory without translation.
- **Multi-day milestone push.** A milestone (epic exit criteria) is the stopping condition for an autonomous loop. The loop runs for hours or days, ratcheting items toward `done`, until the milestone is hit or `HUMAN_NEEDED.md` accumulates enough items to demand attention.

These are how the methodology is used in practice on real long-running projects, not aspirational features.

---

## What this methodology does *not* prescribe

A common failure mode of methodology docs is over-specification. This set deliberately stops short of:

- **A specific tech stack or framework.** The methodology works with any.
- **A team size.** It scales from one contributor to a small team. (Beyond that, additional coordination layers become useful, but the core is unchanged.)
- **A development cadence.** Sprints, kanban, continuous flow — all compatible. The methodology is about *artifacts and gates,* not *scheduling.*
- **A particular project management tool.** Markdown + git is the substrate; external tools can be added without replacing the substrate.
- **Code style rules.** The working principles ([06](06_working_principles.md)) cover the high-level shape; specific style rules live in the project's instruction file and linter configs.
- **Hiring or org structure.** Roles are referenced (contributor, reviewer, user) but team shapes are project-specific.

The methodology is intentionally narrow: it covers the *process and artifact* layer that benefits every project, and stays out of decisions that are properly the project's.

---

## What this methodology *does* prescribe

- The four planning layers (strategy → pillars → epics → items) as the work-decomposition framework.
- The three disciplines (working principles, DoD, memory) as the constraint layer.
- File-based locks with TTL as the coordination mechanism for parallel contributors.
- A specific item frontmatter table with named enum fields.
- Branch protection and PR-only merges to the trunk.
- A fix-test loop for actual-UI verification.
- A two-layer memory system: instruction file + memory directory.
- An audit trail in git for every state change.

These are the load-bearing parts. The rest is recommendation, adaptable per project.

---

## Adopting the methodology in an existing project

If a project is already in flight, you do not need to rebuild everything to start using this methodology. A practical adoption order:

1. **Write the project instruction file** ([08](08_lessons_and_memory.md)) — the single document every contributor reads. Capture the project's hard rules and conventions there first. This is the highest-leverage starting point.
2. **Adopt the working principles and DoD** ([06](06_working_principles.md), [07](07_definition_of_done.md)). The principles and DoD bind individual changes; you can start enforcing them on the next PR without restructuring anything.
3. **Reshape the existing backlog into the item format** ([04](04_backlog_items.md)). This is mechanical but moderately tedious. Do it for the active items first; let archived items stay in their old shape.
4. **Group items into epics** ([03](03_epics.md)). The grouping clarifies scope and surfaces the dependencies you've been carrying implicitly.
5. **Articulate the pillars** ([02](02_pillars.md)). At this point, the team probably knows what the pillars are; writing them down makes them shareable.
6. **Write the strategy docs** ([01](01_strategy.md)) last. By this point, the strategy is largely codified in the team's heads; the docs make it durable.
7. **Layer in locks** ([05](05_locks_and_parallel_work.md)) when more than one contributor (especially AI agents) are working in parallel. Single-contributor projects can defer this.
8. **Refine git workflow and testing practice** ([09](09_git_workflow.md), [10](10_testing_and_verification.md)) as you go. These often need the least change — most projects already have decent practice here.

The order is intentional: highest-leverage changes first. A project that adopts only steps 1 and 2 gets significant value. Steps 3–6 add structure; steps 7–8 add resilience.

---

## Brownfield reality check (when adoption fights headwinds)

The adoption guides above assume reasonable team buy-in. Some brownfield projects don't have that:

- Pre-existing backlog in a tracker that nobody wants to migrate.
- Conventions the team has used for years that conflict with the methodology's rules.
- Multiple contributors who didn't ask for new process and won't read 12 docs.
- A codebase old enough that "small surgical changes" sometimes touch 20 files because of accumulated coupling.
- Compliance, contractual, or org-political reasons that certain rules can't apply directly.

The methodology still applies — it just needs a sequencing that doesn't ask the team to adopt everything at once.

### A staged brownfield adoption

**Stage A — Adopt without announcing.** For the changes *you* personally make, follow the working principles ([06](06_working_principles.md)), write a `CLAUDE.md` or `AGENTS.md` for your AI sessions, file memory entries when you learn something. Nobody else has to participate. You'll ship better code on your own changes; the rest of the team notices the diff quality eventually.

**Stage B — Adopt for parallel-AI work.** The single highest-leverage adoption point is the [lock protocol](05_locks_and_parallel_work.md) when multiple AI sessions (or AI + human) start touching the same code. The collision pain motivates adoption better than any pitch deck.

**Stage C — Adopt the DoD on a single epic.** Pick the *next* substantial piece of work. Apply the [Definition of Done](07_definition_of_done.md) to that epic only. Don't try to retrofit the whole backlog. The contrast — items in this epic actually being done vs. items elsewhere being "done in name only" — is the demonstration.

**Stage D — Open the planning layer.** Once the disciplines (06, 07, 08) are familiar, introduce the planning structure (01, 02, 03, 04) for new work. Existing backlog stays where it is; new items go through the new format. The migration happens through attrition: old items close out in the old format; new items only appear in the new format; eventually only the new format remains.

**Stage E — Backfill upward.** Pillars and strategy come last, not first. By the time you reach Stage E, the team has the disciplines and the working pattern. Writing down the strategy and pillars *codifies* what the team already implicitly understands rather than asking them to discover it from scratch.

### What NOT to do in a brownfield adoption

- **Don't try to reformat the existing backlog all at once.** It's pure overhead that doesn't ship anything. Let it die naturally.
- **Don't fight conventions that aren't broken.** The methodology's conventions (file naming, doc structure, etc.) are recommendations. If the project has a working alternative, keep it. Adopt the *protocols* (lock, DoD, memory) which are the load-bearing parts; let the *conventions* (naming, structure) remain whatever the project already does.
- **Don't ask non-contributors to read 12 docs.** Most team members need the project-instruction file (`CLAUDE.md` / `AGENTS.md`) and one paragraph explaining locks. The deep docs are for whoever is operating the methodology, not everyone touching the repo.
- **Don't litigate the past.** The old code was written under different assumptions. Re-architecting it to fit the methodology is its own multi-month project. Touch what your tasks touch; leave the rest.

### When brownfield adoption fails

If after a few months the staging above isn't sticking, the honest answer is usually one of:

- The team genuinely doesn't have a parallel-contributor coordination problem yet, and the methodology's main value (locks, DoD coupled to items) doesn't yet pay its weight.
- The team has organizational reasons the methodology can't fit (compliance, contracting structure, etc.).
- The project is short-lived enough that the upfront investment doesn't amortize.

In any of these cases: cherry-pick the parts that do help (often the working principles plus memory) and skip the rest. Failed full-adoption isn't a methodology defect; it's a fit signal.

---

## Adopting the methodology in a new project

If you are starting from scratch, top-down works:

1. **Write the strategy master plan** ([01](01_strategy.md)). Vision, phases, and the document index for supporting docs. Other strategy docs can be filled in as needed.
2. **Define the pillars** ([02](02_pillars.md)). Five to twelve capability layers. Get the chain ordering right.
3. **Charter the first epic** ([03](03_epics.md)). Outcome, exit criteria, KPIs, out-of-scope. One epic is enough to start.
4. **File the first items** ([04](04_backlog_items.md)). Three to ten items inside the first epic. Each with a clear goal.
5. **Write the project instruction file** ([08](08_lessons_and_memory.md)). Working principles, tech stack, commands. Doesn't need to be long.
6. **Set up the git workflow** ([09](09_git_workflow.md)). Branch protection, conventional commits, PR template.
7. **Establish testing practice** ([10](10_testing_and_verification.md)). Pick the test framework. Write the first test.
8. **Adopt the locks** ([05](05_locks_and_parallel_work.md)) as soon as the second contributor (or AI agent session) joins.

Steps 1–4 can be done in a single afternoon for a small project. The infrastructure built during steps 5–8 is durable for the project's lifetime.

---

## Authority across the methodology

When constraints conflict, they resolve in this order:

1. **Explicit user direction** — overrides everything. The user can authorize exceptions to any rule for a specific operation. The exception applies to that operation only.
2. **Hard rules** (see the table above) — bind every contributor, regardless of context, absent explicit user direction.
3. **Working principles and Definition of Done** — apply to every change.
4. **Strategy, pillars, and epic charters** — constrain what work is in scope. Strategy outranks pillars when they conflict; pillars outrank epics; epics outrank items.
5. **Project-specific rules** in the instruction file or memory — apply on top of the universal layer.
6. **Memory entries** — advisory. They are accumulated experience, not authoritative rules. They can be overridden by current direction (and probably need updating when overridden).

The principles and DoD are the *floor* — every project needs them, and they cannot be eroded. Strategy, pillars, and epics are the *plan* — they can change, but only through deliberate updates, not silent drift. Memory is the *experience* — it captures what has been learned.

---

## A final word on portability

This methodology was built around a specific project but is written here without any project-specific references. The shape — four layers, three disciplines, locks, fix-test loop, two-tier memory — is the same regardless of:

- The product category (consumer app, enterprise tool, developer tool, hardware, etc.).
- The tech stack.
- The team size.
- The mix of humans and AI agents.

To adopt this methodology in a different project, **copy the `docs/methodology/` folder.** Everything else falls out of following the docs: the strategy docs you produce will be project-specific; the pillars will be project-specific; the items will be project-specific; the conventions in the project instruction file will be project-specific. But the *methodology* — the framework that holds it all together — does not need to be rewritten. It transplants.

The only project-specific decisions to make at adoption time:

- The trunk branch name.
- The pillar set (which capabilities your product needs).
- The phase sequence in the strategy master plan.
- The TTL defaults for locks.
- The project-specific overlay to the DoD (security scans, accessibility checks, etc.).

Everything else is in the docs.

---

## Ending

Read the docs once in order if you have the time. Read them as references thereafter. Treat them like the methodology itself: small, focused, and useful — not aspirational documents that nobody reads.

The methodology earns its keep by surviving real projects. If it stops earning its keep in a specific situation, adapt it. The disciplines and the structure are the part that generalizes; everything else is contingent.
