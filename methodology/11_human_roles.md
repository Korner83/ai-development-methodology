# 11 — Human roles in an AI-driven workflow

> **Purpose:** define how human contributors stay meaningfully engaged when AI agents do most of the implementation work. The bottleneck has shifted from writing code to specifying intent and supervising output; this doc says what humans *do* now that AI does most of the typing.

The rest of the methodology assumes humans and AI agents collaborate as peers. This doc says what the *human side* of that collaboration looks like — and what stops working when humans drift out of the loop.

---

## Why this doc exists

When AI generates code faster than humans can review it, three things happen if nothing changes:

1. **The review bottleneck.** Code volume outpaces the team's capacity to actually understand what's landing. Reviews become rubber stamps. Defects accumulate invisibly until they manifest in production.
2. **The strangers-in-our-own-code problem.** Humans on the team stop being able to recognize the codebase. They wrote little of it; they reviewed some of it superficially; they have no architectural memory of *why* anything looks the way it does. When something breaks, the only debugger is the AI that wrote the broken code in the first place — using the same biases that produced the bug.
3. **The agreement spiral.** AI defaults to helpful agreement. Humans default to trusting the AI that just gave them a confident-sounding answer. Both can be wrong in exactly the same way, and the consensus between them is mistaken for validation.

The methodology's other docs cover *how to work* and *how to gate completion.* This one covers *how the human stays a real contributor* when they're not the one typing the most.

---

## The shifted bottleneck

The classical software workflow bottleneck was **execution**: writing code is slow; understanding requirements is comparatively fast; reviewing code at a sensible pace fits in between.

The AI-assisted workflow inverts this: writing code is fast (sometimes order-of-magnitude faster); understanding what you actually want is now the slow step; reviewing volume is the constraint on the system.

The implication: rigor must shift **upstream**. The specification is the thing that determines whether the AI produces useful output. Sloppy specs produce confident-looking wrong code, and the wrong code passes superficial review because the spec was never sharp enough to disprove it.

### Code is becoming a commodity

A well-defined test suite can be fed to an AI agent to reproduce an implementation in a different language, framework, or runtime. The *implementation* is increasingly replaceable; the *test suite* (when it accurately captures intent) is not.

That's a real shift in what the team should treat as the durable asset:

| Era | Durable asset | Replaceable |
|---|---|---|
| Pre-AI | Code (humans wrote it; it took months) | Tests (often added later, often skimped) |
| AI-assisted | Specification + test suite (captures intent) | Code (AI rewrites in any stack from the spec) |

Teams that treat code as the asset and tests as overhead will be slower than teams that treat the spec + test suite as the asset and let AI regenerate code as needed.

---

## The new supervisory layer

A new layer of work has appeared between *writing code* and *shipping to production.* The article-of-record term is "supervisory work." It consists of:

- **Breaking problems into agent-sized chunks.** Tasks the AI can fully understand and complete in one session, with verifiable acceptance criteria.
- **Knowing when to let an agent run and when to intervene.** Some work the AI should do unattended; some requires step-by-step human approval. Telling them apart is a skill.
- **Fixing output by refining the prompt, not by rewriting the code.** If the AI produces wrong output, the first move is usually to improve the input (clearer spec, better context, more constraints), not to manually fix what was generated. Manual fixes don't propagate; prompt improvements do.
- **Maintaining the institutional knowledge AI doesn't have.** Documented edge cases, prior incident postmortems, "we tried this and it didn't work" notes — the kind of context AI agents can't grow on their own.
- **Reviewing architectural decisions before AI codes them.** Not after. The cost of unwinding a wrong architecture from generated code is much higher than the cost of catching the wrong direction at planning.

This supervisory layer is *the human contribution* in an AI-driven workflow. It is not less work than writing code was; it is differently shaped work.

---

## Anti-patterns to recognize

Four anti-patterns capture most of the ways an AI-driven workflow fails. Each has a defense.

### 1. The cheating agent

The AI writes the implementation. The AI also writes the tests. The tests are subtly tuned to validate the (wrong) implementation. The test suite passes; the code is wrong; the loop is self-consistent. No human in the loop catches it because the green test suite looks like done.

This is the AI-coding equivalent of marking your own homework.

**Defenses:**

- Write the test (or at least the acceptance criteria) *before* the implementation, ideally by a human or by a separate AI session with no knowledge of the planned implementation.
- Use a separate AI to audit the test suite specifically (see [10_testing_and_verification.md](10_testing_and_verification.md) "Cross-AI validation" and the dedicated "cheating agent" section).
- Human review of test *names* and acceptance criteria, even when the test body is AI-written.

### 2. The yes-man (the agreement bias)

AI models are trained to be helpful and agreeable. That works most of the time and breaks at the worst moments: during a production incident, when evaluating an architectural fork, or when a load-bearing assumption is on the table.

In those moments, you propose a theory. The AI agrees with it. You both proceed. The system continues to fail because the theory was wrong — but you both believed it because you reached consensus.

**Consensus between you and the AI is not validation.** You may both be wrong in the same way.

**Defenses:**

- *Invert the default.* Prompt the AI to challenge before approving. See [06_working_principles.md](06_working_principles.md) "Challenge before consenting."
- Use a different AI model (or a fresh session with no prior context) to argue the contrarian case.
- Treat suspicious unanimity as a signal, not a result. If you and the AI agree too quickly on a complex problem, that's a warning, not a conclusion.

### 3. The stranger in your own code

You used to know your codebase. Now most of it was written by an AI agent over the last quarter and you've only superficially reviewed it. When something breaks, you reach for the AI that wrote it — because *you* don't know where to start.

This is a slow-rotting failure mode. It doesn't manifest as a single incident; it manifests as a steady decline in your team's ability to operate the system without the AI.

**Defenses:**

- **Force the AI to lay out every architectural decision it makes** before writing code. Senior humans review these decisions in dedicated sessions, not as PR comments after the fact.
- **Periodic codebase walks** with humans only — read a module together, explain it to each other, build the architectural muscle memory that AI doesn't share. (Quarterly is reasonable.)
- **Maintain the project instruction file as a real document, not boilerplate.** The conventions and hard rules captured there are the human-authored constraints the AI works within. If the file is stale, the AI fills the gap with whatever feels reasonable to it.
- **Treat the architectural-review meeting as a non-negotiable.** Not a meeting about *what's planned;* a meeting about *what the AI is about to do and why it's the right approach.*

### 4. The loss of tribal knowledge

The AI reads documentation. It does not have the lived experience of "we tried this two years ago and it failed because…" or "this looks redundant but is workaround for the X-Y bug." That context lives in human heads, in old issue threads, in postmortems nobody reads anymore.

When that context is missing, AI agents will confidently propose the same failed approach the team tried two years ago — because nothing in the codebase or the docs warns against it.

**Defenses:**

- **An incident archive.** Every production incident produces a short writeup: what happened, root cause, what we'd do differently. Live in `docs/incidents/` or similar. AI agents read them as context for new work.
- **"Why we don't do X" docs.** Every counter-intuitive decision gets a short doc explaining the path-dependency. The AI then knows not to "fix" the seeming oddity.
- **Use the memory directory aggressively.** See [08_lessons_and_memory.md](08_lessons_and_memory.md) — the memory system is exactly the place for tribal knowledge that doesn't fit elsewhere.
- **Postmortems before forgetting.** A postmortem written one week after an incident captures the lived experience. A postmortem six months later captures the sanitized story.

---

## Specification as the primary artifact

When AI is doing most of the implementation, the *specification* — not the code — is the thing the team should be best at producing.

A good specification is:

- **Unambiguous.** Two readers, regardless of background, should reach the same understanding. The AI is one of those readers.
- **Complete on the relevant axes.** State diagrams for stateful flows. Decision tables for branching logic. Pre/post-conditions for functions with non-trivial contracts. Examples for ambiguous edges.
- **Falsifiable.** It should be possible to say "the implementation does NOT match this spec because of X." Specs that can't be disproved aren't specs; they're aspirations.
- **Linked to test cases.** Every spec assertion has at least one test that exercises it. The test suite *is* the spec, made executable.

### Formats that work well with AI

| Format | Good for | Why AI handles it well |
|---|---|---|
| **State machines** (mermaid `stateDiagram-v2` or text tables) | Stateful flows, lifecycles, modal UIs | Discrete states + named transitions = code that almost writes itself |
| **Decision tables** | Branching logic, permissions, eligibility rules | Exhaustive coverage of input combinations; AI can detect missing rows |
| **Sequence diagrams** (mermaid `sequenceDiagram`) | Multi-actor flows, API choreography | Explicit ordering removes a major source of AI guesswork |
| **Schema-first definitions** (JSON Schema, Zod, Pydantic, etc.) | Data contracts, API requests/responses | Type system as spec; AI generates parsing + validation deterministically |
| **Given / When / Then acceptance criteria** | Item-level behavior | Maps directly to test names; AI implements until the named test passes |
| **Examples + counter-examples** | Edge cases, ambiguous categorization | "Input X → output Y; input X' (one char different) → output Z" forces the AI to reason about the boundary |

### Formats that don't work well

- Prose-only specifications. The AI will pick a reasonable interpretation; you'll find out later it wasn't the one you meant.
- Pictures without text. The AI can sometimes interpret images, but the interpretation isn't audit-able.
- "Inspired by" specs that point at an existing system without specifying which parts are normative. The AI imitates the wrong parts.

---

## Reviewing AI architectural decisions BEFORE the code lands

The methodology's existing [plan-mode rule](06_working_principles.md) is the foundation. This section sharpens it for the supervisory layer.

### What "architectural decision" means here

- Choice of data model.
- Choice of where state lives (client vs. server vs. database, in-memory vs. persisted).
- Choice of synchronous vs. asynchronous, blocking vs. queued.
- Choice of new dependency (library, MCP, service).
- Choice of where a responsibility lives (which module, which layer).
- Choice of public API shape (request/response, errors, naming).
- Choice of authorization or trust boundary.

These are all things the AI will pick *something* for if you don't specify. Picking something is usually fine for trivial work and dangerous for non-trivial work.

### The pre-implementation review

For non-trivial work, the human reviews:

- *Each* of the architectural decisions the AI is about to make.
- The AI's reasoning for each choice (alternatives considered, why rejected).
- The implications for code that will need to change downstream.
- The implications for the team's ability to operate the result.

This is a dedicated review, not a PR comment after the code is written. Unwinding a wrong architecture from generated code is much more expensive than catching the wrong direction at the planning stage.

Format suggestion: an "Architecture Decision Record" (ADR) per non-trivial choice, written by the AI, reviewed by a human, before the code lands. Plain markdown; one page; what / why / alternatives / consequences.

### When to skip

- The change is small (effort `XS` or `S`).
- The architectural decisions are obvious (one reasonable answer, no judgment call).
- The work is a pure replacement for existing well-tested code with the same shape.

Use judgment; over-applying this slows everything down. The goal is to catch the high-impact wrong directions, not to add ceremony to every change.

---

## The skills that matter now

Not all human skills transfer equally to an AI-assisted workflow. Some that were peripheral become central; some that were central become less critical.

### Skills that grow in value

- **Architectural thinking.** Knowing how the parts fit together; predicting how a change in one place ripples elsewhere.
- **Unambiguous specification.** Writing the kind of requirements an AI (and a careful junior engineer) can execute on without rework.
- **Supervisory skill — debugging code you didn't write.** Reading unfamiliar code, finding the failure, understanding why it happens.
- **Taste and judgment.** What makes a UI feel good, what makes an API feel right, when a "correct" implementation is still wrong for the product. AI doesn't do taste.
- **System thinking across abstraction layers.** Connecting a user-visible bug to a database constraint, a cache invalidation, a deploy timing issue.
- **Knowing what NOT to do.** The path-dependent "we tried that; here's why we won't" knowledge. AI agents don't develop this; they need it transferred.

### Skills that grow less critical

- **Pure code-writing speed.** AI is faster.
- **Memorizing framework APIs.** AI looks them up reliably.
- **Boilerplate and ceremony.** Tests with obvious shapes, setup code, configuration files. AI does this well.
- **Stylistic consistency.** Linters + AI conventions handle this.

This isn't a claim that writing code is obsolete. It's a claim that *being fast at writing code* is no longer the differentiator it used to be. The differentiator is the upstream and supervisory work — the architecture, the spec, the review, the judgment.

---

## Implications for team composition

The methodology is silent on hiring (that's strategy-doc territory). But the patterns above shift what's worth hiring for:

- **Junior contributors thrive** in an AI-assisted workflow when they're paired with strong supervisory practices. They use AI as a teammate; they reach production-relevant output quickly. The risk: they may not build the architectural intuition that comes from doing the implementation work themselves.
- **Mid-level contributors face the steepest transition.** Their established skill — competent code production — is the part AI has most disrupted. Re-anchoring on spec-writing, review, and supervisory work is the path forward; clinging to the old skill set is the failure mode.
- **Senior contributors are at risk of drowning** in review volume if the team scales AI output without scaling supervisory capacity. The senior role evolves toward: spec authorship, architectural review, incident response, mentoring others into the supervisory mindset.

The point isn't to rank these tiers. The point is that the *shape of work* changes for each, and pretending it doesn't is the failure mode.

---

## How this doc connects to the rest of the methodology

- **[01 Strategy](01_strategy.md) and [02 Pillars](02_pillars.md)** are increasingly the human-authored spec layer that AI executes against. The clearer they are, the better the AI's output.
- **[03 Epics](03_epics.md) and [04 Backlog items](04_backlog_items.md)** are where "agent-sized chunks" live. Item sizing (XS / S / M / L / XL) should match what an AI can confidently complete in one session.
- **[06 Working principles](06_working_principles.md)** includes the *Challenge before consenting* rule — the per-decision defense against the yes-man problem.
- **[07 Definition of Done](07_definition_of_done.md)** includes the documentation-maintenance gate that prevents the "stranger in our own code" failure.
- **[08 Lessons and memory](08_lessons_and_memory.md)** is the institutional-knowledge mechanism that gives AI the tribal context it doesn't naturally have.
- **[10 Testing and verification](10_testing_and_verification.md)** includes the *cheating agent* anti-pattern and cross-AI validation — the safety net against AI-validates-its-own-output failures.
- **[templates/AUTONOMOUS_LOOP.md](../templates/AUTONOMOUS_LOOP.md)** assumes a human supervisor is in the loop at the milestone level, not absent.

---

## Common mistakes around human roles

| Mistake | Fix |
|---|---|
| Senior contributors approve PRs without reading the diffs because volume exceeds capacity. | Reduce PR volume per cycle, or add another reviewer (human or cross-AI), or invest in pre-implementation review so post-implementation review can be lighter. |
| Architectural decisions get made implicitly in AI-generated code. | Require explicit ADRs (or equivalent) for non-trivial choices, reviewed before code lands. |
| Tests are written by the AI immediately after the implementation; nobody human-reviews the test design. | At minimum: human-review the test *names* and acceptance criteria. Ideally: write the test (or the acceptance criteria) first. |
| Team agrees with AI on a debugging theory; the system keeps failing. | "Challenge before consenting." Use a different model to argue the contrarian case. Treat suspicious unanimity as a signal. |
| AI proposes the same broken approach you tried two years ago. | Build the incident archive; write the "why we don't do X" docs; populate the memory directory. |
| Junior contributor ships AI-generated code they don't understand. | Mentor them through what the AI did and why; build their architectural muscle alongside their AI fluency. |
| Senior contributor checks out of the codebase because "the AI handles it now." | Codebase walks (humans only) on a quarterly cadence; force the architectural muscle to stay active. |
| Specifications are vague prose; AI fills the gaps with plausible-sounding guesses. | Move spec format toward state machines, decision tables, schema-first definitions, Given/When/Then. |
| AI keeps recommending the documented fix even when the actual cause is elsewhere. | Build the tribal-knowledge layer (incident archive + memory) so the AI has the context to consider non-documented causes. |
| The team has no idea what the AI just shipped over the last week. | The supervisory layer has collapsed. Reduce AI throughput until human review can keep up, or invest in the supervisory layer until throughput is sustainable. |

---

## Authority

This doc defines the *shape* of the human contribution in an AI-driven workflow. It doesn't prescribe specific roles, titles, or org structure — those are project-specific. The patterns and anti-patterns transfer; the implementation is yours.

When the methodology's other docs and this one appear to conflict: the working principles ([06](06_working_principles.md)) and the Definition of Done ([07](07_definition_of_done.md)) are foundational and win. This doc adds *human-side* guidance on top of those foundations.

The integrity rule from [templates/AUTONOMOUS_LOOP.md](../templates/AUTONOMOUS_LOOP.md) ("never claim something is tested / secure / complete / production-ready unless it was actually verified") applies doubly to the human side: don't claim oversight you didn't actually exercise.

---

**End of the methodology set.** Return to [00_README.md](00_README.md) for the index.
