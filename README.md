# AI Development Methodology

How to run a software project when some of your contributors are AI agents — and one of them just panic-refactored your auth middleware at 2am while a different one was halfway through the same task.

Twelve short docs. Markdown + git. No SaaS, no signup, no vendor lock-in. Read in 90 minutes; use forever (or until you find something better).

By **Miklós Polgár** ([polgarmiklos@gmail.com](mailto:polgarmiklos@gmail.com)) — [CC BY 4.0](LICENSE). Fork it, ship it, charge for it, teach it. Just keep the credit.

---

## TL;DR

- **Four planning layers** — strategy → pillars → epics → items. Each one answers a different question. None of them overlap.
- **Three discipline overlays** — working principles, Definition of Done, lessons-learned memory. They bind every change at every layer.
- **File-based locks with TTL** so two AI agents (or two humans) don't both grab the same item and silently produce conflicting work.
- **A fix-test loop for the UI** because "tests pass" doesn't mean "the page renders."
- **Cross-AI validation + user testing** as the final gates — automated tests are necessary, never sufficient.
- **Plan before executing** non-trivial work. Use your tool's plan mode.
- Battle-tested in one production project. Currently at v1.2.0 — see [CHANGELOG.md](CHANGELOG.md) for what's shipped and when.

---

## Why this exists

Most software projects accumulate the same failure modes once they last more than a few weeks. AI-assisted projects accumulate them twice as fast because the effective contributor count doubles (and the new contributors don't sleep). Each row below is a real failure mode and the part of this set that closes it.

| The problem | Why it keeps happening | How this set closes it |
|---|---|---|
| **Direction drifts.** Every quarter, "what are we actually building?" gets re-litigated. | Decisions live in chat, in slide decks, in heads — nowhere durable. | [Strategy docs](methodology/01_strategy.md) — versioned snapshots with phases, exit criteria, and a re-evaluation protocol. |
| **Work fragments.** Contributors can't see how today's task ladders up to the vision. | Backlogs are flat. The chain from strategy to today is implicit. | [Four planning layers](methodology/00_README.md) — every item traces upward to a pillar and a strategic phase. |
| **Done-ness is fuzzy.** Items get marked done while still buggy or untested. | "Done" means whatever the current contributor decides. | [Definition of Done](methodology/07_definition_of_done.md) — six binary gates, with the hard rule that `Status: done` requires `Test: pass`. No partial credit. |
| **"Tests pass" ≠ "it works."** Green CI ships broken layouts, dark-mode disasters, white pages on mobile. | Unit tests cover what they cover. Layout, theme, viewport, auth gating, missing imports — they don't catch these. | [Actual-UI fix-test loop](methodology/10_testing_and_verification.md) with required dimensions (theme, viewport, auth, empty, error). |
| **Tests pass and the UI looks fine — and the user still hates it.** | Synthetic verification can't model real users. | [Cross-AI validation + user testing](methodology/10_testing_and_verification.md) as the final gates. The user is always the last word. |
| **Lessons evaporate.** Same mistake every six months. Tribal knowledge stays in heads. | No system for capturing recurring fixes. | [Two-layer memory system](methodology/08_lessons_and_memory.md) — instruction file + memory directory. Lessons survive sessions and contributors. |
| **Parallel contributors collide.** Two agents grab the same item; both do the work. | Markdown backlogs have no coordination primitive; chat-based "I've got this" is invisible. | [File-based locks with TTL](methodology/05_locks_and_parallel_work.md) — works for humans and AI agents identically. |
| **AI agents wander off-task.** Without explicit constraints, they speculate, refactor adjacent code, build cathedrals for one-line problems. | The default "helpful" LLM tendency is to add abstraction and defensive scaffolding. | [Four working principles](methodology/06_working_principles.md) — distilled from real LLM-coding failure modes. |
| **Humans drift out of the loop as AI does more coding.** Reviews become rubber stamps; the team becomes strangers in its own codebase; AI confidently proposes the same broken approach you tried two years ago. | When AI generates code faster than humans can meaningfully review it, supervisory work gets squeezed without anyone noticing. | [Human roles in an AI-driven workflow](methodology/11_human_roles.md) — supervisory layer, spec-as-primary-artifact, four anti-patterns (cheating agent, yes-man, stranger in own code, tribal-knowledge loss), and the skills that matter now. |
| **AI agrees with you and you're both wrong.** Production incident; you propose a theory; the AI agrees; the system keeps failing. | AI models default to helpful agreement; consensus between you and the AI is not validation. | [Challenge before consenting](methodology/06_working_principles.md) + [cross-AI validation](methodology/10_testing_and_verification.md) — invert the default; prompt for the contrarian case. |
| **AI writes broken code AND broken tests that validate it.** Green test suite hides bugs. | When the same AI writes implementation and tests, the tests can be subtly tuned to validate the broken code. | [The "cheating agent" anti-pattern](methodology/10_testing_and_verification.md) — write tests first, cross-AI validate, human-review test names. |
| **AI agents start without a plan and you find out three hours later they went the wrong way.** | No required planning step. | [Plan before executing non-trivial work](methodology/06_working_principles.md) — use your tool's plan mode. |
| **Design work has no home.** Features ship with vague scope because the design wasn't finished before the charter. | The four planning layers don't fit "design exploration." | [Pre-epic planning](methodology/03_epics.md) — `docs/planning/` as the incubation layer. |
| **Scope creep.** Epics absorb every adjacent suggestion and never finish. | "Out of scope" is vague intent, not documentation. | [Epic charters](methodology/03_epics.md) — every charter has an explicit out-of-scope section with pointers. |
| **Operational work is invisible.** Deploys, pipelines, runbooks, on-call — somehow not in the backlog, somehow still failing. | Most methodologies ignore ops. | [Operational work](methodology/09_git_workflow.md) — patterns that transfer; project-specific runbooks layered on top. |
| **The trunk breaks.** A force-push, a destructive command in the wrong window, and someone's day is gone. | Branch protection is "best-effort"; destructive git commands are easy to run autonomously. | [Git workflow rules](methodology/09_git_workflow.md) — branch protection, PR-only merges, and the "AI agents never run destructive commands or production deploys" boundary. |
| **Vendor lock-in.** Methodology gets entangled with a tool that's gone in 18 months. | Convenience pulls toward whatever you started with. | **Markdown + git only.** Works identically whether your agent is Claude Code, Cursor, Aider, Codex, or human. |

### Why it works (the short version)

Three properties make the set hold together:

1. **Everything is a file.** Strategy, pillars, epics, items, locks, lessons. Files in git. Greppable, version-controlled, mergeable, reviewable. No SaaS to babysit.
2. **Every layer has one job.** Strategy is *why.* Pillars are *what capabilities.* Epics are *what 3–12-week batch.* Items are *what 1–2 week unit.* Disciplines are *how to work and when it's done.* No layer creeps into another's territory.
3. **AI agents are first-class.** Every protocol — lock acquisition, item lifecycle, working principles, DoD — is written so an agent can follow it without translation. Agents get the same workflow as humans, not a worse one.

---

## What's in the repo

```
ai-development-methodology/
├── README.md                 # this file
├── CHANGELOG.md              # version history (self-applies the methodology)
├── LICENSE                   # CC BY 4.0
├── STATUS.md                 # maintenance posture
├── methodology/              # the 12 methodology docs
│   ├── 00_README.md          #   index + mental model
│   ├── 01_strategy.md        #   strategy docs
│   ├── 02_pillars.md         #   pillars
│   ├── 03_epics.md           #   epics + pre-epic planning
│   ├── 04_backlog_items.md   #   backlog items + resolution notes
│   ├── 05_locks_and_parallel_work.md
│   ├── 06_working_principles.md
│   ├── 07_definition_of_done.md
│   ├── 08_lessons_and_memory.md
│   ├── 09_git_workflow.md    #   git + operational work
│   ├── 10_testing_and_verification.md
│   └── 11_human_roles.md     #   human roles in AI-driven workflow
└── templates/
    ├── CLAUDE.md             # project-instruction file (Claude Code)
    ├── AGENTS.md             # same content, vendor-neutral filename
    └── AUTONOMOUS_LOOP.md    # prompt for long autonomous dev sessions
```

Total: ~6,100 lines across 19 files (12 methodology docs + 3 instruction-file templates + repo meta). The longest single doc is ~700 lines. Each doc is self-contained — you don't have to read them in order.

---

## Who it's for

- **Solo developers** using AI coding agents who want process that survives past week 3.
- **Small teams** mixing humans and AI agents, tired of "who's working on what?" being a question.
- **Indie hackers and startup founders** who need real process without enterprise overhead.
- **Engineering leaders** trying to fit AI agents into existing workflows without inventing the wheel.

**Not** for: large enterprises with existing process frameworks. This won't replace SAFe. It can coexist with team-level practices, but it's not a top-of-org methodology.

---

## How to use it — at the start of a new project

This is the highest-leverage path: hand the methodology to an AI agent in planning mode *before* you write any code. Let the agent produce the initial strategy, pillars, and first epic. By the time you start implementing, the structure is in place.

### Step 0 — Before this methodology kicks in (the brief)

**This methodology does not solve the upstream work.** It executes on already-defined goals. It does not tell you what to build, who to build it for, or how to validate that anyone wants it. Those decisions need real thinking *before* any of the steps below can produce anything useful.

Concretely, before Step 1, you need at least rough written answers to:

- **What** are we building, and **why** does it matter?
- **Who** is it for? What problem do they have today, and how do you know they have it?
- **What does success look like** at the 1-year horizon, the 3-year horizon?
- **Who else is in this space?** What do they do better or worse? What's your wedge?
- **Is this financially viable?** Revenue model? Cost structure? Unit economics that survive scrutiny?
- **What's the tech stack?** Frontend, backend, database, hosting, AI tooling — choices that fit the product, the budget, and the team.
- **What are the 5–10 capability layers** the product will need? (These become your [pillars](methodology/02_pillars.md).)

How you produce these answers is your own work. Founder intuition, structured frameworks (Lean Canvas, Business Model Canvas, JTBD interviews, Porter's Five Forces, customer-discovery calls, paid market research, advisor conversations) — pick what fits the situation. This methodology is silent on the *method* of getting to a solid brief; it just assumes you have one.

**A common failure mode** is treating `docs/strategy/` and `docs/pillars/` as a substitute for upstream thinking. They're not — they're the *recording layer* for decisions you've already made and validated externally. If you populate them with hand-wavy guesses, every layer below (epics, items, code) executes confidently on a shaky foundation, and you find out the foundation was wrong many months later when the product doesn't fit the market.

**The honest deliverable from Step 0:** a written brief — covering the bullets above — that you'd be willing to hand to an investor, an advisor, or your future self. Could be a one-pager, could be a 20-page document, could be a Notion workspace. Format doesn't matter; the discipline of having written, defensible answers does.

**If you don't have answers yet: stop.** Do that work first. The methodology will be here when you're ready. Skipping Step 0 to "just start coding with AI" produces a velocity illusion: you ship a lot of working code that builds the wrong product.

---

### Step 1 — Set up the repo

```bash
mkdir my-new-project && cd my-new-project
git init -b main
git clone --depth 1 https://github.com/Korner83/ai-development-methodology.git _methodology_src
mkdir -p docs && cp -r _methodology_src/methodology docs/methodology
cp _methodology_src/templates/CLAUDE.md ./CLAUDE.md   # or AGENTS.md — see below
rm -rf _methodology_src
git add docs/methodology CLAUDE.md
git commit -m "docs: import ai-development-methodology"
```

You now have `docs/methodology/` in your project and a starter `CLAUDE.md` at the root.

### Step 2 — Hand it to your AI agent (planning-mode prompt)

Paste this into your AI agent at the start of the project. Adjust the bracketed parts.

```
I'm starting a new software project. Before we write any code or
file any tasks, I want you to use the AI development methodology
(located in this repo at docs/methodology/ — start with 00_README.md
for the mental model).

Here's what I know about the project so far:

- Product: [one or two sentences describing what you're building]
- Target user: [who it's for]
- Constraints: [budget, timeline, team size, tech preferences]
- What success looks like: [the outcome that would make this worth doing]

Your job, in order:

1. Read docs/methodology/00_README.md, 01_strategy.md, 02_pillars.md,
   and 03_epics.md. Skim the others.

2. Ask me clarifying questions ONLY about things you genuinely cannot
   guess. Don't ask permission questions; ask information questions.

3. Propose:
   a) A draft strategy master plan at docs/strategy/00_master_plan.md
      with vision, 3–5 phases (each with exit criteria), and the
      document index. Follow the skeleton in 01_strategy.md.
   b) An initial pillar set (5–8 pillars) as separate files at
      docs/pillars/P1_*.md ... PN_*.md. Use the skeleton in
      02_pillars.md. Sequential dependency chain.
   c) The charter for the first epic at backlog/epics/01-<slug>/README.md.
      Use the template in 03_epics.md. One primary pillar. Binary
      exit criteria.
   d) The first 3–5 backlog items in that epic's BACKLOG.md. Use the
      format in 04_backlog_items.md.

4. Use plan mode (your tool's planning feature). Show me each
   artifact before moving to the next. Don't bundle.

5. Once everything is approved, fill in the starter ./CLAUDE.md
   (already at the root from Step 1) with the project-specific
   conventions, commands, and hard rules. The skeleton already
   contains the working principles and a pointer to
   docs/methodology/ as the authoritative source for HOW work is
   done — you just need to fill in the <<placeholders>>.
```

The agent reads the methodology, asks the right questions, produces a complete planning skeleton. You review and refine. By the time you sit down to write code, you have strategy, pillars, an epic, and items — all in the right places.

### Step 3 — Ongoing development

After Steps 0–2 are done, the project-instruction file (`CLAUDE.md` or `AGENTS.md` at the repo root) is what carries the methodology into every AI session. **Modern AI coding tools read it automatically — you don't paste anything at the start of each session.** The file's contents (working principles, lock protocol, DoD, verification order) become the AI's standing context.

What you actually do during development is **steer when the AI drifts.** Four short phrases worth keeping handy:

- **"Do you have any questions before you start?"** — surfaces ambiguities before they become code (see the small-tip section below).
- **"What's wrong with this plan? What's the strongest case against it?"** — counters the AI agreement bias (see [Challenge before consenting](methodology/06_working_principles.md)).
- **"Use plan mode and show me the plan before executing."** — when the AI is about to start non-trivial work without planning.
- **"Stop. Split this item — you're growing scope."** — when scope creep appears mid-task.

These are session-time interventions, not setup ceremony. The methodology runs continuously from the project-instruction file; your job is to *steer* when the AI drifts and to *approve* when it pauses for review.

For dedicated milestone-pushing where you want the AI to grind autonomously between check-ins, see [For long autonomous sessions](#for-long-autonomous-sessions) below — that's the one case where pasting an explicit prompt is the right move.

### A small tip that pays off

When you give the AI its first task in a new session — *before letting it proceed* — ask:

> **"Do you have any questions before you start?"**

This one line routinely surfaces:

- Ambiguities the AI was about to resolve silently with a guess.
- Missing context the AI assumed but you'd want to confirm.
- Edge cases the AI is uncertain how to handle.
- Tool / library / pattern choices where the AI sees multiple reasonable options.

A 30-second exchange of questions saves hours of rework later. The working principles already require the AI to raise questions when uncertain ([06 — Principle 1: Think before coding](methodology/06_working_principles.md)), but you prompting "any questions?" is the social cue that gives the AI permission to surface them. Use it liberally — especially before plan-mode approvals, before large refactors, and at the start of any new session.

---

### For long autonomous sessions

When you want the AI to grind toward a milestone without you reviewing every step, use the [autonomous-loop prompt template](templates/AUTONOMOUS_LOOP.md). It tells the AI to apply the methodology as a continuous *analyze → prioritize → execute → validate → repeat* loop, with a milestone-level stop condition (not per-task completion). Includes the integrity rule: never claim what wasn't actually verified.

Not for exploratory work — for that, the "Step 2" prompt above is the right shape.

---

## How to use it — selectively in an existing project

Cherry-pick. Each doc stands alone:

- Backlog is chaotic? → [03 Epics](methodology/03_epics.md) + [04 Backlog items](methodology/04_backlog_items.md).
- Items keep shipping half-broken? → [07 Definition of Done](methodology/07_definition_of_done.md) + [10 Testing and verification](methodology/10_testing_and_verification.md).
- AI agents colliding? → [05 Locks and parallel work](methodology/05_locks_and_parallel_work.md).
- Same mistakes repeating? → [08 Lessons and memory](methodology/08_lessons_and_memory.md).
- Code is over-engineered? → [06 Working principles](methodology/06_working_principles.md).
- Strategy keeps drifting? → [01 Strategy](methodology/01_strategy.md).
- Deploys feel unsafe? → [09 Git workflow](methodology/09_git_workflow.md) (operational work section).

Full adoption order is in [methodology/00_README.md](methodology/00_README.md).

---

## AI tool support

This methodology is **tool-agnostic.** The protocols work for any AI agent that can read files and run commands. Only the *project-instruction filename* differs per tool.

| AI tool | Filename it reads | Template to use |
|---|---|---|
| Claude Code (Anthropic) | `CLAUDE.md` | [templates/CLAUDE.md](templates/CLAUDE.md) |
| OpenAI Codex CLI | `AGENTS.md` | [templates/AGENTS.md](templates/AGENTS.md) |
| Google Antigravity | `AGENTS.md` or `.agent/instructions.md` | [templates/AGENTS.md](templates/AGENTS.md) |
| Cursor | `.cursor/rules/` or `.cursorrules` | Adapt [templates/AGENTS.md](templates/AGENTS.md) |
| Aider | `CONVENTIONS.md` | Adapt [templates/AGENTS.md](templates/AGENTS.md) |
| Continue.dev | `.continue/context.md` | Adapt [templates/AGENTS.md](templates/AGENTS.md) |
| Any other tool | Whatever it reads (often any `.md` in the repo root) | Either template |

The two templates have identical content. If your team uses multiple tools, either:

- Maintain both `CLAUDE.md` and `AGENTS.md` with identical content (small duplication cost), or
- Symlink one to the other (`ln -s AGENTS.md CLAUDE.md` on Unix), or
- Pick one filename and leave the other tools unconfigured (most modern AI tools fall back gracefully).

The *content* is what matters — the project-instruction file. The filename is a tool-specific detail.

---

## What makes this different from existing methodologies

Agile, Scrum, Kanban, Shape Up — all predate AI agents in the coding loop. They optimize for human teams.

This set explicitly accounts for:

- **AI agents as first-class contributors.** Locks, item formats, principles, and DoD are written so an agent can follow them without translation.
- **Verification beyond automated tests.** The actual-UI fix-test loop catches what tests don't — spelled out, not assumed.
- **Cross-AI validation.** A separate AI auditing the work catches what the implementing AI missed. User testing remains the final gate.
- **Lessons that survive across sessions.** The memory system formalizes a pattern that's emerging in agent workflows but not yet well-documented.
- **Pre-epic planning.** Design work has its own layer between strategy and chartering — so epics don't ship with vague scope.

Common ground with prior methodologies: small deliberate iterations, explicit definition of done, outcome-based gating. The shape is familiar; the AI-agent integration is new.

### How this relates to specific methodologies

| Methodology | What we adopt | What we do differently |
|---|---|---|
| **Agile Manifesto** | The values: working software, responding to change, individuals over process | We add explicit artifacts (strategy → pillars → epics → items) and gates (DoD) — values alone don't bind AI agents |
| **Scrum** | Outcome-based work, Definition of Done, retrospectives | No fixed sprints, no Scrum Master role, no story points; ceremonies replaced by async artifacts |
| **Kanban** | Pull-based work, WIP limits (we cap active epics at 3), flow visualization (`EPICS.md` rollup) | We add a planning hierarchy upstream — pure Kanban has no upstream constraint, just the board |
| **Shape Up** | Outcome-based pitches (≈ epic charters), explicit out-of-scope, fixed appetite (≈ effort enum) | Epics close on binary exit criteria, not on a calendar-based appetite |
| **Extreme Programming (XP)** | Test-first discipline, frequent commits, simple design, refactoring | Adds cross-AI validation + user-testing-as-final-gate; pair programming becomes human + AI pairing |

**Coexistence:** this methodology can run *inside* a Scrum team (treat sprints as a scheduling overlay; the artifact layer below stays the same). It can layer *on top of* a Kanban-only workflow by adding the upstream planning layers. It complements XP practices directly. It's not designed to replace enterprise frameworks like SAFe — those operate above the team level, and this stays at the team level.

**Net:** if you know one of the above, you'll find this familiar. The differences are not philosophical — they're concrete additions that came from running multi-contributor AI-assisted projects long enough to see what breaks under that specific shape of work.

---

## Attribution

If you use or adapt this, please include credit:

> AI Development Methodology by Miklós Polgár, licensed CC BY 4.0.
> https://github.com/Korner83/ai-development-methodology

For modified versions, indicate you've made changes.

This is the only obligation the license imposes. Use it commercially, in client work, in books, in courses, anywhere — as long as the credit travels with it.

---

## Status

See [STATUS.md](STATUS.md). Short version: battle-tested in one production project, currently at v1.2.0 — see [CHANGELOG.md](CHANGELOG.md) for the version history. Maintenance is lean — PRs welcome, but no SLA. The CC BY 4.0 license exists precisely so you can fork it if you want a more actively-maintained version.

For direct contact: [polgarmiklos@gmail.com](mailto:polgarmiklos@gmail.com).

---

## License

[CC BY 4.0](LICENSE) — Creative Commons Attribution 4.0 International. Copyright © 2026 Miklós Polgár.

You are free to share and adapt for any purpose, commercial or not, provided you give appropriate credit and indicate changes.

---

## Origins

Extracted from a real production project's working practice, then republished as a portable abstract version. The source project name and domain appear nowhere in the methodology — by design. The intent is for anyone (human or AI agent) to read these and apply them to any codebase.

What you're reading isn't a theoretical framework. It's what worked. Specifically, it's what worked *after* it had failed in other shapes. See [CHANGELOG.md](CHANGELOG.md) for the running record of what's been added, refined, or rolled back as understanding sharpens.
