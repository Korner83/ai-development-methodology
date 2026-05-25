# Audience

Four primary segments and three secondary segments. Plus explicit non-audience.

## The problem each segment shares

The four primary segments differ in scale and resources, but all face the same underlying problem: **software projects accumulate methodology debt fast when AI agents are in the contributor mix.** The specific frustrations vary by segment — collisions for small teams, drift for solos, tech debt for indies, integration ambiguity for leaders — but the root is the same: no established methodology was built natively for human + AI collaboration. The four segments below are different lenses on that one problem.

## Primary segments

### 1. Solo developers using AI coding agents

**Profile:** one person + one or two AI coding tools (Claude Code, Cursor, Codex, Aider, Continue), working on a personal or freelance project. Probably solo SaaS, indie game, side project, or research code.

**What they're trying to accomplish:** ship a working product. Move fast. Use AI to do what would otherwise take far longer to type by hand.

**Current frustrations:**

- AI does the wrong thing autonomously and they catch it three commits later.
- Lost context between sessions — yesterday's plan isn't in today's session, AI re-derives (often differently).
- Backlog drift — "what was I working on?" every Monday morning.
- The project starts feeling unmaintainable at week 3–6 because methodology debt accumulates invisibly.

**What they'd pay (in attention) to fix:** anything that lets them keep velocity without losing the thread. They'll read a 12-doc methodology if it pays off; they won't read SAFe.

**Why this methodology fits:** every protocol works for one person, lock TTL is generous (single contributor rarely collides with themselves), CLAUDE.md / AGENTS.md gives the AI standing context, the four planning layers prevent drift, the DoD prevents shipping half-done.

### 2. Small mixed-contributor teams (2–5 people + AI agents)

**Profile:** small startup engineering team, agency project team, research group, or open-source maintainers. Humans and AI agents working in the same codebase on overlapping concerns.

**What they're trying to accomplish:** coordinate work across humans and AI without enterprise process overhead. Ship features. Maintain quality. Avoid the "who broke main?" question.

**Current frustrations:**

- Parallel work collisions — two contributors (human or AI) grab the same task and silently produce conflicting work.
- "Who's working on what?" is a question that takes Slack time to answer.
- AI agents over-reach authority — they make architectural decisions that should have been human-reviewed.
- Items shipping with one person's understanding only; the rest of the team is surprised by what landed.

**What they'd pay (in attention) to fix:** lightweight coordination they don't have to manually orchestrate. Locks that work for both humans and AI. A clear "who owns which decision" reference.

**Why this methodology fits:** file-based locks with TTL (humans and agents use the same protocol), decision-ownership matrix (concrete who-decides-what), HUMAN_NEEDED.md (blocked work surfaces visibly), DoD coupled to item frontmatter (can't fake done).

### 3. Indie hackers and startup founders

**Profile:** building a product mostly with AI doing the implementation work. Limited time, limited resources, no full-time engineer.

**What they're trying to accomplish:** ship something real. Validate the product. Avoid building the wrong thing fast.

**Current frustrations:**

- AI generates a lot of code that works, but the team has no shared mental model of what's actually been built.
- Tech debt accumulates from AI-generated code that wasn't reviewed deeply.
- "What are we building again?" every quarter — strategy keeps drifting because the AI doesn't push back on direction.
- Backlog is chaotic — tasks live in a TODO list, in Slack, in heads. Nothing's authoritative.

**What they'd pay (in attention) to fix:** anything that makes the project less fragile. They especially value the working-principles ("AI agents stay on task") and the four planning layers ("today's commit traces back to a strategy phase").

**Why this methodology fits:** the methodology is designed for projects where AI does most of the typing. The supervisory-layer framing in `11_human_roles.md` is exactly the founder's job. The Step 0 brief is what most indies skip — and what most indies later regret skipping.

### 4. Engineering leaders fitting AI agents into existing workflows

**Profile:** team lead, eng manager, or VPE at a small-to-mid company. Existing team with established process (Scrum-ish, Kanban-ish, GitHub Issues, some kind of sprint cadence). Adding AI agents — Copilot, Cursor, Claude Code — into the workflow.

**What they're trying to accomplish:** integrate AI agents without disrupting what works, without inventing the wheel, without committing to a vendor lock-in. Answer the team's "how should we work with AI now?" question with something defensible.

**Current frustrations:**

- Existing process doesn't say what AI agents can/can't do.
- Reviews become rubber stamps when AI generates code faster than humans can read it.
- Senior engineers drift out of the codebase ("the AI handles it now") — slow rot.
- The team is asking for guidance and the leader is improvising.

**What they'd pay (in attention) to fix:** a defensible overlay on top of existing process that names the new failure modes (cheating agent, yes-man, stranger in own code, tribal-knowledge loss) and provides counters.

**Why this methodology fits:** explicit "coexists with Scrum / Kanban / XP" framing in the README; the four anti-patterns in `11_human_roles.md` are exactly the failure modes leaders are worried about; the decision-ownership matrix gives a defensible answer to "what should AI decide vs what should humans decide?"

## Secondary segments

### AI coding tool builders

Vendors and open-source maintainers of AI coding tools (Anthropic, OpenAI, Cursor, Aider, Continue, Antigravity). Read the methodology to see what their tools should support — instruction files, plan mode, cross-session memory, etc. The methodology is a soft spec for what good AI-coding tooling enables.

### Educators teaching AI-collaborated development

Bootcamp instructors, CS educators, internal training leads. Use the methodology as curriculum reference for "how to use AI tools responsibly in real projects." The methodology's voice (direct, opinionated, principle-based) translates well to teaching.

### Researchers studying AI-augmented software development

Academics working on human-AI collaboration in software engineering. Use the methodology as case-study material (a real, in-use methodology with versioned history). The CHANGELOG is the kind of artifact a research paper can cite.

## Out of scope as audience

- **Large enterprises with SAFe / LeSS / DAD already established.** This methodology won't replace those. It can coexist at the team level inside one, but the marketing isn't directed there.
- **Pure-human teams with no AI in the workflow.** The methodology works, but it's over-specified for that case — they don't need the AI-specific patterns (locks across human+agent, cheating agent, decision-ownership matrix). They'd be better served by Shape Up, XP, or vanilla Kanban.
- **Non-software projects.** The patterns are software-shaped (PRs, branches, tests, lock files). They don't transfer cleanly to writing a book, producing a film, or running an event. Possible adaptation effort exists but is not the maintainer's path.

## What changes about the audience over time

The 1-year horizon audience is the **early adopter** subset — people who actively seek methodology guidance for AI-coding. The 3-year horizon audience grows to include the **mainstream** subset — people who notice the named methodology as the field stabilizes.

The 3-year horizon also includes **fork maintainers** for niche variants (regulated industry, research teams, etc.) who didn't exist in the 1-year window because there hadn't been time for forks to mature.
