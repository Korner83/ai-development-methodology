# Agent Kickoff Prompt

The planning-mode prompt for Step 2 of the "new project" workflow described in the [README](../README.md#on-a-new-project-the-high-leverage-path).

Paste it into your AI agent at the start of a new project, after Step 1 (set up the repo) and after you have a brief from Step 0. Adjust the bracketed parts.

---

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
   c) The charter for the first epic at backlog/epics/E01-<slug>/README.md.
      Use the template in 03_epics.md. One primary pillar. Binary
      exit criteria. Folder naming uses the E<NN>-<slug> convention
      per 03_epics.md "Standard epic-folder structure."
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

---

For long-running autonomous milestone work (after the kickoff is done), see [AUTONOMOUS_LOOP.md](AUTONOMOUS_LOOP.md) — a different prompt for a different mode of work.
