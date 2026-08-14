# 06 — Working Principles

> **Purpose:** the small set of working principles that prevent the most common failure modes when humans and AI agents share a codebase. Every contributor — human or AI — operates under these. They are deliberately few, deliberately strict, and deliberately phrased so they are testable against any change.

These principles are not aspirational. They are barriers. If a change violates one, the change is wrong even if it "works."

---

## Why these principles exist

A codebase that grows under multiple contributors — and especially under AI contributors — fails in a recognizable pattern. Each individual change looks reasonable in isolation, but the codebase drifts toward:

- **Speculative abstraction** — interfaces, factories, configuration knobs, and extension points built for futures that never arrive. The code gets harder to read while solving nothing real.
- **Scope creep** — a task to "fix the bug in `parseDate`" returns with seven adjacent renames, a refactor of the date module, and a new helper file. The diff is huge, the review is shallow, the regression risk is invisible.
- **Style drift** — every new file uses a slightly different convention than the surrounding ones, because each contributor reaches for whatever style they prefer. The codebase loses its readability.
- **Open-ended exploration** — tasks treated as "see what's there and improve things" rather than "produce this specific verifiable outcome." Work runs long, results are unfocused, nothing is testably done.
- **Made-up guarantees** — error handling for impossible cases, fallbacks for code paths that cannot be reached, defensive checks at trusted boundaries. The code looks robust and is actually obscured.

The four principles below are written to make these failure modes hard to commit to. They are short on purpose so they fit in a contributor's head.

---

## Principle 1 — Think before coding

**Rule:** state your assumptions before you write code. If you are uncertain, ask. If the task admits multiple interpretations, name them. If you are confused, stop and say what is unclear. Do not pick silently and ship.

### What this looks like in practice

- Before writing code, write one or two sentences saying what you understand the task to be and what assumptions you are making. This is the cheapest possible alignment check.
- If the task description could mean two different things, surface both interpretations and choose one explicitly. Do not pick the easier one without saying so.
- If you find yourself confused mid-task, stop. Name the confusion. Confusion at the keyboard is a signal that you are about to write the wrong code.
- If a simpler approach exists than the one the task implies, say so before you start. The requester may not have known about it.

### What this is not

- Not a license for stalling. If the task is unambiguous, do not invent ambiguity to delay. Reasonable assumptions stated up front are better than questions for their own sake.
- Not a license for thinking out loud forever. A few sentences of framing is enough; long deliberation before any code lands is its own anti-pattern.

### Why this matters

The cost of stating an assumption is one sentence. The cost of building on the wrong assumption is the entire change plus the rework. Asking the question — or at least naming the assumption — is always cheaper than the recovery.

---

## Principle 2 — Simplicity first

**Rule:** write the minimum code that solves the problem. Nothing speculative. No abstractions for single-use code. No flexibility, configurability, or error handling for scenarios nobody asked for. If the same thing could be done in half the lines, do it in half the lines.

### What this looks like in practice

- A single helper function used in exactly one place is not a "helper." It is a layer of indirection. Inline it.
- Three similar lines are better than one premature abstraction. Wait until the pattern repeats often enough to be obviously worth extracting.
- Configuration options exist when there is a real, named caller who needs each option. Speculative configurability — a `mode` flag that nobody currently passes a non-default value to — is dead code.
- Error handling exists at trust boundaries (user input, network, filesystem, external APIs). Inside the codebase, trust your own functions and the framework's guarantees. Defensive `try/catch` around internal calls obscures more than it protects.
- Validation exists at the system edge. Once data is past the edge, treat it as valid.
- Backwards-compatibility shims, fallbacks for "the old shape," and feature flags for cleanups — none of these are simplicity. They are debt the next contributor pays.

### The senior-engineer test

When you are done, imagine a senior engineer reading your diff cold. Would they call it overcomplicated? If yes, simplify before you ship.

### What this is not

- Not anti-abstraction. Real abstractions — used in more than one place, named after the concept they represent — are still good. The bar is "earned by use," not "anticipated for the future."
- Not anti-safety. Validation at boundaries is still required. The rule is against defensive code for impossible states.

### Why this matters

Every line of code is a maintenance liability. Every abstraction is a thing the next reader must learn. The cheapest code to maintain is the code that does not exist. Default to less.

---

## Principle 3 — Surgical changes

**Rule:** touch only what the task requires. Do not "improve" adjacent code, comments, or formatting on the way past. Match existing style even if you would do it differently. Every changed line should trace directly to the task.

### What this looks like in practice

- A bug-fix diff should contain the fix and its test. Nothing else.
- If you notice a typo in a comment two lines above your fix, leave it. File a separate item if it matters.
- If you find unrelated dead code, mention it in your end-of-turn report. Do not delete it as part of this change.
- Match the surrounding indentation, naming, and import order. If the file uses `snake_case` and the wider codebase uses `camelCase`, the file's style wins inside the file.
- Do not reorder imports, sort keys, reformat whitespace, or change brace style as part of an unrelated task. These are review-noise generators.
- Remove only the imports and variables that *your* changes orphaned. Pre-existing unused imports stay until someone files a cleanup item.

### The traceability test

Pick any line in your diff. Ask: "Did the task require this?" If the answer is no, revert that line.

### What this is not

- Not anti-cleanup. Dedicated cleanup items exist and are valuable. They are filed as items, scoped explicitly, and reviewed on their own merits.
- Not a ban on noticing things. Notice. Report. Do not silently bundle.

### Why this matters

Bundled "improvements" make diffs unreadable, expand the regression surface, and hide the real change. The reviewer cannot tell what was the task and what was the side trip. Surgical changes are reviewable; bundled changes are not.

### Protected regions (declared edit boundaries)

Principle 3 limits the *scope of a single change.* Some files go further: they are off-limits to ordinary work *regardless of the task* — editing them is almost always a mistake, and when it isn't, it needs explicit authorization. A project declares these **protected regions** once, in its instruction file, so every contributor (human or AI) knows the lanes before starting rather than discovering them through a bad diff.

Typical protected regions:

- **Generated or compiled artifacts** — anything emitted by a build step or codegen (`dist/`, hand-edited lockfiles, generated clients, snapshots). Edit the source and regenerate; never hand-edit the output.
- **Vendored or framework code** — third-party code copied into the repo, or the shared framework/core in a product-on-a-framework layout. Product behavior goes in the product's own modules (e.g. `src/modules/<name>/`), not in the generic core.
- **Machine-managed config and infrastructure** — files a tool owns (CI-managed secrets, environment manifests, migration history). Hand-editing them desyncs them from the tool that manages them.
- **Anything the project marks "do not touch"** — a file with a known reason it looks the way it does (a shim mid-migration, a security-reviewed boundary). The reason usually lives in a memory entry (see [08_lessons_and_memory.md](08_lessons_and_memory.md)).

The rule: **treat declared protected regions as read-only. If the task genuinely requires touching one, stop and get explicit authorization first** — surface *what* you need to change and *why*, the same way Principle 1 surfaces an assumption. Editing a protected region silently is the failure this prevents.

This is the code-side sibling of the autonomous-loop [tier matrix](../templates/AUTONOMOUS_LOOP.md#tiered-autonomy-for-authoritative-artifacts), which draws the same kind of boundary around *authoritative docs* (what a loop may auto-edit vs. what a human must author). Both say the same thing: not every file is fair game, and the off-limits ones are named in advance.

### Frozen intent (approved work definitions)

The third member of that family bounds not files but *the definition of the work itself.* Once a human approves an item's goal and acceptance criteria (or an epic charter's exit criteria), that region is **frozen intent — human-owned.** Principle 3 says don't touch code the task doesn't require; frozen intent says don't touch the *task's own success definition* to fit what you built. Principle 4 depends on it: a verifiable goal only converges if the goal holds still while you work toward it.

If execution shows the approved goal is genuinely wrong, the move is the same as Principle 1's: **halt and surface it.** Get explicit re-approval; the change lands as a visible edit, never a silent one. Mechanics — the marker badge, who can thaw, how it meets scope-creep recovery — live in [04_backlog_items.md "Frozen intent"](04_backlog_items.md#frozen-intent--approved-goals-are-human-owned).

---

## Principle 4 — Goal-driven execution

**Rule:** transform every task into a verifiable goal before starting. The goal must be testable: someone should be able to look at the result and say "yes, this is done" or "no, it is not" without further interpretation. For multi-step work, state a brief plan with a verification step for each item.

### How to transform tasks

| Vague task | Verifiable goal |
|------------|-----------------|
| "Fix the bug." | "Write a test that reproduces the bug. Then make the test pass." |
| "Add validation." | "Write tests for the invalid inputs the task names. Then make them pass." |
| "Refactor X." | "Ensure the existing test suite passes before the refactor, after the refactor, and at every intermediate commit." |
| "Make it faster." | "Establish a baseline measurement. Define the target. Verify the new measurement meets the target." |
| "Clean this up." | List the specific things to clean. Each one becomes its own goal. If you cannot list them, the task is not ready to start. |
| "See what's there." | This is a research task, not an implementation task. Produce a written finding, not code. |

### Multi-step plans

For any work spanning more than one or two changes, write the plan first. Each step gets its own verification:

1. Step description.
2. How to verify the step succeeded (test command, manual check, output comparison).
3. What "blocker" looks like for this step.

If a step has no verification, it is not a step. It is a wish. Replace it or split it.

### Why this matters

Strong success criteria let a contributor — human or AI — loop independently. "Make it work" provides no stopping condition; the contributor keeps changing things until they get tired. "Make this specific test pass" stops when the test passes. Goal-driven execution is the difference between a task that converges and one that drifts.

---

## Plan before executing non-trivial work

The four principles above govern *how* you work moment-to-moment. This rule governs *when* you start. **It is not a fifth principle** — the count of principles stays at four. It is the gating rule that decides when the four principles begin applying to a piece of work.

**Rule:** for any task larger than a small focused change, produce a written plan and get approval before executing. The plan names what you'll do, in what order, and how each step will be verified.

### What "non-trivial" means

- Anything that will touch more than ~3 files.
- Anything that introduces a new abstraction, API surface, or schema change.
- Anything you cannot fully envision before starting.
- Anything with multiple reasonable approaches where the choice matters.
- Anything that will produce a PR you'd want a reviewer to understand.

A typo fix, a one-line CSS tweak, a single-function refactor with obvious shape — these are trivial. Proceed.

### What goes in the plan

- The goal (verifiable, with a stopping condition — see Principle 4).
- The approach (high-level: what will you change and in what order).
- The steps (each step has its own verification).
- The risks (what could go wrong; what would force a re-plan).
- Out of scope (what you're explicitly not doing, even if related).

### Tool support

Most modern AI coding tools support a "plan mode" or equivalent that pauses execution until the plan is approved. Use it. Examples:

- **Claude Code:** explicit plan mode.
- **Cursor:** Composer with plan-first workflow.
- **Other tools:** if there's no built-in plan mode, write the plan in a comment or temporary file and pause for approval.

### Why this matters

A wrong plan caught at planning time costs minutes. A wrong plan caught after implementation costs hours of rework — plus the regression risk of unwinding the wrong direction. Planning is cheap; un-implementing is expensive.

A plan is also the artifact that lets the user redirect *before* you've committed to one interpretation. "Are you about to write X? I'd rather Y." That conversation is impossible after the code lands.

---

## Tools the agent uses (install what helps)

The agent's toolset is not fixed. If the task would be significantly faster, safer, or more reliable with a tool that isn't currently available, install it (or ask the user to install it). Don't reinvent.

### Common tool categories

- **MCP servers:** browser automation, database explorers, file search engines, web fetchers, IDE bridges.
- **Plugins and skills:** AI-tool-specific extensions that add capabilities (Cursor plugins, Claude Code skills, OpenAI Codex tools).
- **Project packages:** if your code would benefit from a battle-tested library, prefer adding the dependency over hand-rolling.
- **Verification tools:** linters, type-checkers, accessibility scanners, security scanners — install before the gap matters.

### When to install

- The task is *significantly* easier with the tool. Marginal gains don't justify the tool sprawl.
- The tool has a clear license and isn't introducing surprising dependencies.
- The user is aware (or will be told in the next message) — surprise installations of heavy dependencies erode trust.

### When NOT to install

- You can do the task with the tools you already have.
- The tool requires the user's account, credentials, or paid subscription you don't already know they have.
- The tool is experimental or unverified for your stack.
- The tool is destructive (auto-deploys, auto-merges, etc.) and the user hasn't sanctioned its install.

### The rule

When in doubt: ask. The cost of a question is small; the cost of an unwanted package or MCP server in the project is annoying.

---

## Challenge before consenting

AI models are trained to be helpful and agreeable. That bias toward agreement is useful most of the time and dangerous when it matters: in a crisis, debugging a baffling failure, or evaluating a load-bearing architectural decision, an AI that defaults to "yes, that sounds right" can produce a false consensus while the actual system fails.

### The pattern

When the stakes are high — production incident, architectural choice, security-sensitive change — invert the default. Prompt the AI to *challenge* rather than confirm:

```
"Before we proceed: what's wrong with this plan?
What am I missing?
What's the strongest case AGAINST doing it this way?
What would a senior engineer at a competing company poke holes in?"
```

The AI is fully capable of producing the contrarian case. It just won't by default — you have to ask.

### When to use it

- Before approving any plan for non-trivial work (alongside the "any questions?" prompt — see README "A small tip that pays off").
- Mid-incident when a fix attempt is being proposed.
- When evaluating which of two architectures to choose.
- After the AI has produced a confident-sounding answer to an ambiguous question.
- When you notice you're agreeing with the AI a lot — that's the signal.

### Why this matters

Consensus between you and the AI is not validation. You may both be wrong in the same way. A flawed theory you both believe is harder to escape than a flawed theory that one of you doubts.

The methodology already has mechanisms for this at the systemic level — [cross-AI validation](10_testing_and_verification.md) uses a different model to catch what the implementing model missed, and [user testing](10_testing_and_verification.md) is the final gate. *Challenge before consenting* is the per-decision version of the same idea: don't let a single conversation's agreement substitute for genuine review.

See [11_human_roles.md](11_human_roles.md) "The yes-man (the agreement bias)" for the deeper framing.

---

## How the four principles interact

The principles compose. A change that violates none of them looks like this:

1. Started with an explicit statement of what the task means and what is being assumed. **(Principle 1)**
2. Transformed into a verifiable goal with a known stopping condition. **(Principle 4)**
3. Implemented with the minimum code that hits the goal — no speculative abstractions, no defensive shells. **(Principle 2)**
4. Touches only what the goal requires; no drive-by edits. **(Principle 3)**

A change that violates one tends to drag the others down with it. Speculative abstractions (P2) bundle into adjacent files (P3). Open-ended tasks (P4) invite silent picking (P1). The four are mutually reinforcing.

---

## How these interact with Definition of Done

The principles govern *how you work moment to moment.* The Definition of Done governs *what makes a task complete.* Both are required and they are not the same gate.

- You can violate the principles and still meet the DoD (e.g., a change that works but is over-engineered). The result is bad code that ships. The principles catch what the DoD does not.
- You can follow the principles and still miss the DoD (e.g., a clean small change that was never UI-verified). The result is unverified work that should not ship. The DoD catches what the principles do not.

See [07_definition_of_done.md](07_definition_of_done.md) for the gates that prove a task is actually done.

---

## What these principles do not replace

These four principles cover general LLM-coding and multi-contributor pitfalls. They do not cover:

- **Project-specific rules.** Each project has its own conventions, prohibitions, and hard rules (e.g., "never deploy to production," "always use the shared ownership helper"). Those live in the project's instruction file (see [08_lessons_and_memory.md](08_lessons_and_memory.md)) and override the principles when they speak to the same situation.
- **Domain-specific patterns.** Database migration discipline, API security boundaries, accessibility requirements, performance budgets — none of these are covered by the four principles. They are layered on top by the project's own documentation.
- **Tooling and process.** Git workflow, testing approach, lock acquisition — these are separate disciplines. The principles say nothing about them.

When a project-specific rule and a principle appear to conflict, the project-specific rule wins. The principles are the floor, not the ceiling.

---

## Anti-patterns the principles forbid

A short list of behaviors that are always wrong under these principles. Use it as a quick check before committing.

| Anti-pattern | Which principle it violates |
|--------------|-----------------------------|
| Picking one of two reasonable interpretations of the task without saying so. | P1 |
| Writing a `config` object with one option, used in one place. | P2 |
| Wrapping internal function calls in `try/catch` for "safety." | P2 |
| Renaming variables in a file you happened to be editing for an unrelated reason. | P3 |
| Reformatting whitespace, reordering imports, or sorting keys as part of an unrelated change. | P3 |
| Treating "improve the code" or "see what's there" as an actionable task. | P4 |
| Starting a multi-step change without writing the verification step for each item. | P4 |
| Adding a feature flag for "future flexibility" with no current caller. | P2 |
| Building a `BaseFooBar` abstract class because there might be more subclasses later. | P2 |
| Bundling a small refactor into a bug fix "while I'm here." | P3 |
| Hand-editing a generated, vendored, or framework-core file instead of its source — or touching a declared protected region without authorization. | P3 (protected regions) |
| Rewording an approved goal or acceptance criterion to match what was actually built, instead of halting and renegotiating. | P4 (frozen intent) |
| Patching code to compensate for a plan the review showed to be wrong, instead of fixing the plan and re-deriving the code. | P4 (see [07 — Routing findings by failure layer](07_definition_of_done.md#routing-findings-by-failure-layer)) |
| Adding fallback behavior for a state that the type system already rules out. | P2 |
| Continuing to write code after you have lost the thread, rather than stopping and naming the confusion. | P1 |

---

## A principles checklist (copy into your project's instruction file)

The text below is the canonical short form. Paste it into your project's contributor instructions verbatim. It works because it is short.

```
Working Principles (apply to every change):

1. Think before coding.
   State assumptions explicitly. If uncertain, ask. If multiple interpretations
   exist, surface them. Stop when confused; name the confusion before writing code.

2. Simplicity first.
   Write the minimum code that solves the problem. No abstractions for single-use
   code. No flexibility, configurability, or error handling for scenarios nobody
   asked for. If it could be half the lines, rewrite it.

3. Surgical changes.
   Touch only what the task requires. Match existing style. Do not refactor
   unrelated code. Mention drive-by observations; do not silently fix them.
   Every changed line traces to the task.

4. Goal-driven execution.
   Transform every task into a verifiable goal with a known stopping condition.
   "Fix the bug" -> "write a test that reproduces it, then make it pass."
   For multi-step work, state a plan with a verify step per item.

These complement Definition of Done; they do not replace it. Both required.
Project-specific rules and lessons-learned memory override these when they speak
to the same situation. Principles are the floor, not the ceiling.
```

---

## Authority

When a principle and a request appear to conflict — e.g., a request to "just add a quick wrapper" that would violate Principle 2 — the contributor's job is to surface the conflict, not to silently violate the principle. State what you would have to do, why it violates the principle, and ask. The requester may agree and override, or may revise the request. Either outcome is good; silently violating the principle is not.

The principles outrank convenience. They do not outrank explicit user direction. They do outrank assumed user direction.
