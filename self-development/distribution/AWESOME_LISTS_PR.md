# Awesome-lists PR drafts

_Maintainer: pick one or more target lists; submit PR per each list's contributor guidelines. Entry text below is the recommended one-line per list._

## Recommended target lists (ROI-ranked)

1. **[awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code)** — highest fit (the methodology pairs with Claude Code as one of its native tools). Section suggestion: "Workflows" or "Best Practices."
2. **[awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps)** — broader fit. Section suggestion: "Development Tools" or "Frameworks."
3. **[awesome-ai-agents](https://github.com/e2b-dev/awesome-ai-agents)** — fits the multi-agent / autonomous-loop angle. Section suggestion: "Methodologies" or "Tooling."
4. **[awesome-software-architecture](https://github.com/mehdihadeli/awesome-software-architecture)** — angle: project structure + planning layers. Section suggestion: "Project Structure" or "Best Practices."
5. **[awesome-engineering-team-management](https://github.com/kdeldycke/awesome-engineering-team-management)** — angle: human roles + decision-ownership matrix. Section suggestion: "Process" or "Frameworks."

## One-line entry (recommended phrasing per list)

### awesome-claude-code

```markdown
- [AI Development Methodology](https://github.com/Korner83/ai-development-methodology) - A markdown + git methodology for running projects where humans and AI agents collaborate as peers. Includes CLAUDE.md template, autonomous-loop prompt with tier matrix, file-based locks for parallel agents, and periodic milestone evaluation. CC BY 4.0.
```

### awesome-llm-apps

```markdown
- [AI Development Methodology](https://github.com/Korner83/ai-development-methodology) - Markdown-and-git development methodology built for projects where AI agents are first-class contributors. Planning cascade (strategy → pillars → epics → items), file-based locks, autonomous-loop tier matrix, cross-AI validation. No SaaS, CC BY 4.0.
```

### awesome-ai-agents

```markdown
- [AI Development Methodology](https://github.com/Korner83/ai-development-methodology) - Methodology for multi-agent software projects: file-based locks with TTL prevent two agents from picking the same item; an autonomous-loop tier matrix splits methodology-doc changes by risk (T0 cosmetic auto-patch via cross-AI diff-verify, T2 deferred to human authorship). 13 docs, CC BY 4.0.
```

### awesome-software-architecture

```markdown
- [AI Development Methodology](https://github.com/Korner83/ai-development-methodology) - A four-layer planning cascade (strategy → pillars → epics → items) plus three discipline overlays plus periodic milestone-evaluation gate. Markdown + git only. Battle-tested on one production project + self-applied. CC BY 4.0.
```

### awesome-engineering-team-management

```markdown
- [AI Development Methodology](https://github.com/Korner83/ai-development-methodology) - A methodology for teams where some contributors are AI agents. Includes a decision-ownership matrix (which decisions are AI / human-reviewed / human-only), supervisory-layer practices, and four anti-patterns (cheating agent, yes-man, stranger in own code, tribal knowledge loss). CC BY 4.0.
```

## PR-description template

When the awesome-list requires a PR description, use this:

```markdown
## Adding: AI Development Methodology

**Why this fits:** [pick the relevant angle per list — see one-liners above]

**Link:** https://github.com/Korner83/ai-development-methodology

**License:** CC BY 4.0 (open source / open content).

**Maintenance status:** actively maintained; v1.16.0 shipped 2026-05-25.

**What it adds to the list:** [Cover one or two of: AI-multi-agent coordination patterns / planning-cascade structure / autonomous-loop prompts / cross-AI validation patterns / decision-ownership matrix for AI-assisted teams]

I am the maintainer (no conflict of interest — disclosing per the awesome-list etiquette).
```

## What to avoid

- **Submitting to lists where the methodology doesn't fit.** Each awesome list has a specific scope; off-topic submissions get closed and damage credibility.
- **Submitting to multiple lists same-day.** Spread submissions across 2–3 weeks so each PR gets focused review.
- **Hyperbole in the entry.** Awesome-list maintainers reject "best", "revolutionary", "ultimate." Plain factual language only.

## After merge

- Add the awesome-list link to the README's "Where we're listed" section (create if absent).
- Watch the awesome-list's traffic for the methodology's link clicks (if the list publishes stats).
