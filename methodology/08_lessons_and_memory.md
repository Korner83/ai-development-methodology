# 08 — Lessons and memory

> **Purpose:** define the two-layer memory system that captures recurring lessons, user preferences, and project context across sessions and contributors. The first layer is a single project-instruction file read by every contributor; the second is a memory directory of focused, loadable-on-demand entries.

This system exists because the same mistake otherwise gets made repeatedly across sessions and contributors. Write it down once, in the right place, and the next person — human or AI — does not relearn the lesson at cost.

---

## The problem

A project that lives longer than a few weeks accumulates lessons faster than any single contributor can remember:

- A particular fix pattern works; nobody writes it down; the same bug reappears six months later and is solved the slow way.
- A non-obvious rule ("never touch this file, it's machine-generated") is known by two people and missed by the third.
- The user prefers terse responses but every new AI session begins with a paragraph of preamble.
- A subsystem has tribal knowledge about *why* it looks weird ("the previous library was deprecated; we wrapped it in a shim during migration") that is invisible from reading the code.
- An external system is the canonical source for some kind of data — but you have to know to look there.

These are all knowledge transfer problems. Code review and documentation help partially; chat history helps not at all (it is ephemeral and unsearchable in practice). Without a deliberate system, every new contributor — whether they're human-new or just a fresh AI session — pays full re-learning cost.

The memory system solves this by *deliberately* writing down the lessons in a format that future contributors can find and use.

---

## Two layers

### Layer 1: the project-instruction file

A single file at the repo root (e.g., `CLAUDE.md`, `CONTRIBUTING.md`, `AGENTS.md` — pick a name and stay consistent). This is the *one file every contributor reads on their first day and re-reads on every session.*

It must be:

- **Compact.** A few hundred lines. Long enough to be useful, short enough to read in a sitting and remember.
- **Universal to the project.** Rules that apply to every task, every contributor, every change.
- **The single source of truth for project conventions.** If a convention is here, it overrides whatever feels natural from outside.
- **Loaded automatically.** For AI agents, the project-instruction file is loaded into context on every session. For humans, it is the first link in the README or in onboarding docs.

### Layer 2: the memory directory

A directory of focused memory entries, typically at `memory/` (or `.<agent>/memory/` for per-agent memory). Each entry is a small markdown file covering one lesson.

It must be:

- **Indexed.** A `MEMORY.md` index file at the root lists every entry as a one-line link.
- **Loadable on demand.** The index is read into context every session; individual entries are read only when relevant. (For AI agents, this matches the natural cost model — the index is cheap; loading every entry is expensive.)
- **Greppable.** A new contributor (human or AI) facing a confusing situation can grep the directory for keywords and find the lesson.
- **Maintainable.** Entries are updated and pruned as projects evolve.

### Why two layers, not one

- A single giant file fails because nobody re-reads a thousand lines on every session, especially AI agents with bounded context.
- A directory without a top-level instruction file fails because there is no universal "read this first" — and contributors miss baseline rules.
- The two layers complement each other: the instruction file holds rules that apply *everywhere;* memory holds rules that apply *sometimes.*

---

## What goes in the project-instruction file

The instruction file is for rules that apply to *every task.* If a rule is conditional ("only when working on the frontend"), it belongs in memory instead.

Typical contents:

| Section | What goes here |
|---------|----------------|
| Project overview | One paragraph: what the product is, who uses it, what's distinctive. |
| Working principles | The four LLM-coding principles (see [06_working_principles.md](06_working_principles.md)). |
| Tech stack | Monorepo layout, languages, frameworks, key libraries. |
| Commands | How to install, build, test, lint, run dev servers. The handful of commands every contributor runs daily. |
| Architecture summary | The mental model: services, data flow, key abstractions. |
| Code conventions | How to write code in this project. Naming, file organization, formatting tools. |
| Frontend/backend patterns | Pattern conventions specific to each layer. |
| Database/data conventions | Schema rules, migration discipline, data ownership boundaries. |
| Backlog and methodology pointers | Link to the backlog folder and the methodology docs. *"Read `backlog/README.md` before picking up a task."* |
| Hard rules | A short list of "never do this in this project" rules. Things that have burned the team before. |
| UX or design principles | Top-level design philosophy. Detailed design system docs go elsewhere; the broad rules go here. |

### What does NOT go in the instruction file

- **Specific lessons learned.** Those are memory entries.
- **Ephemeral state.** Current sprint, in-progress refactors, this week's priorities — none of these belong. The instruction file is durable.
- **Long-form documentation.** Architecture deep-dives, design system specifications, API references — all live in `docs/` and are linked from here.
- **Personal preferences of specific contributors.** Those are personal-config items, not project rules.

### Keeping the file short

Periodically (e.g., once a quarter), re-read the instruction file critically. Look for:

- Sections that haven't been re-read in months — probably stale, or covered better elsewhere now.
- Conditional rules that have crept in — relocate to memory.
- Duplicates of other docs — link instead.
- Items that have become so universally known that they no longer need to be written down (rare, but it happens).

A 200-line instruction file that every contributor reads every session beats a 2000-line file that gets skimmed.

---

## What goes in memory

The memory directory holds focused lessons too narrow or too conditional for the instruction file. Four typical types:

### Type 1: Feedback / recurring fix patterns

When the same category of error appears 2 or more times in different contexts, the pattern is durable — write it down. The entry captures:

- The pattern (the symptom and the fix).
- The reason it keeps happening (often something non-obvious about the codebase or environment).
- How to recognize it in the future.

These are usually named `feedback_<topic>.md` to mark their nature.

### Type 2: User preferences and behavioral guidance

How the user (or operator, or the team) wants contributors to behave. Examples:

- "Reply tersely; the user reads diffs themselves and doesn't want a recap."
- "Don't ask permission before making changes the user has already endorsed in spirit."
- "Avoid emojis in code and comments."

These are usually named `feedback_<behavior>.md` (the line between behavioral feedback and recurring-fix feedback is fuzzy; both get `feedback_` prefix).

### Type 3: Project context

Non-obvious facts about the project that aren't derivable from reading the code or git history. Examples:

- *Why* the auth middleware looks the way it does (it was rewritten last quarter to comply with a regulation).
- *Who* is in the beta wave and what their tolerance for breakage is.
- *Where* the product is in its rollout and what's blocked behind the next milestone.

These are usually named `project_<topic>.md` or by domain.

### Type 4: References

Pointers to external systems where information lives. Examples:

- "Bugs are tracked in the X tracker, project named Y."
- "The performance dashboard is at <internal URL>."
- "Feedback from beta users is collected in <channel>."

These are usually named `reference_<topic>.md`.

---

## Memory entry template

Every memory entry is a markdown file with frontmatter and a body. The frontmatter is structured; the body has a small required shape.

### The template

```markdown
---
name: <short-kebab-case-slug>
description: <one-line summary for the index>
metadata:
  type: feedback | project | reference | user
---

<Body — one or two paragraphs stating the rule or fact.>

**Why:** <The reason for the rule. Usually a past incident or strong
preference. This is what lets future-you judge edge cases instead of
blindly applying the rule.>

**How to apply:** <When and where this kicks in. The trigger conditions
or scope.>
```

### Frontmatter fields

- **`name`** — kebab-case slug, also used as the filename (`<name>.md`). Examples: `feedback-no-emojis`, `project-beta-wave`, `reference-grafana-dashboards`.
- **`description`** — a single line that appears in the index. Should be specific enough that a contributor can decide from the index whether the entry is relevant to their current task.
- **`metadata.type`** — one of `feedback`, `project`, `reference`, or `user`. Determines how the entry is meant to be applied.
- **`metadata.status`** *(optional)* — `active` (the default; omit it), `stale` (flagged for archival on the next sweep), or `archived` (kept for lineage, dropped from the live index). See [Archive, don't destroy](#archive-dont-destroy-the-memory-lifecycle).
- **`metadata.pinned`** *(optional)* — `true` marks a load-bearing entry (one that guards against data loss, a security regression, or an irreversible action) that sweeps never auto-archive, however rarely it is referenced.

### The body

Two mandatory components:

1. **The rule or fact.** State it plainly. One or two paragraphs.
2. **`Why:`** — the rationale. Without the rationale, the rule is brittle; future contributors cannot tell when an edge case warrants deviation.

And one strongly recommended:

3. **`How to apply:`** — the trigger conditions. Where and when does this rule kick in?

### Optional sections

- **`Symptoms:`** — for recurring-fix entries, how to recognize the problem.
- **`Anti-pattern:`** — what to avoid.
- **`Related:`** — cross-links to other memory entries (use `[[other-name]]` syntax for memory-internal links).

### Length

Most entries should be 30–100 lines of markdown. Long memory entries are often signs that the content belongs in a regular doc (like a pillar or a design document) instead.

---

## The index pattern

The index file at the root of the memory directory (`MEMORY.md`) lists every entry as a single line:

```markdown
# Memory Index

- [Title](file.md) — one-line hook describing when this matters.
- [Another title](other-file.md) — one-line hook.
- ...
```

A concrete example (note the kebab-slug filename + actionable hook):

```markdown
# Memory Index

- [definition-of-done.md](definition-of-done.md) — Every task tested on actual UI in fix-test loop before commit; CHANGELOG + README updated after each meaningful change.
- [git-branch-protection.md](git-branch-protection.md) — Feature branches for new work; merge to master only via PRs; never force-push.
- [feedback-no-permission-prompts.md](feedback-no-permission-prompts.md) — Skip "may I…?" — just make the change unless it's destructive.
```

### Rules for the index

- **One line per entry, under ~150 characters.**
- **The hook is action-oriented.** Tell the reader *when* this matters, not just *what* it says.
- **No frontmatter on the index itself.** It is a navigational file, not a memory.
- **Keep it short.** The index is read on every session; over 200 lines becomes burdensome. If the project genuinely has more entries than fit, split the index by category (separate files for `feedback`, `project`, etc.) or archive entries that are no longer load-bearing.

### Why the index hook matters

A new contributor (or an AI agent in a fresh session) sees the index but cannot read every entry. The hook is how they decide which entries to load. A vague hook ("about CSS") forces loading the entry to know if it applies; a specific hook ("never use the non-existent --color-stone-50 var; use --card-bg") tells them at a glance whether their current task is touched by it.

### Index update discipline

- Every new memory entry adds an index line in the same commit.
- Every removed entry removes its line.
- Every renamed entry updates its line.
- A periodic sweep checks for orphans (entry exists, index line missing) or dangling lines (line exists, entry file missing).

---

## When to write a new memory

There are four reliable triggers. If none of these apply, you probably do not need a new memory.

### Trigger 1: Explicit user direction

The user says "remember this" or "save this as a memory" or words to that effect. Write the entry immediately. Use the type they implied or, if unclear, pick the best fit (usually `feedback` or `project`).

### Trigger 2: Same correction or fix has appeared 2+ times

If you've had to correct the same kind of error in two different sessions or two different contexts, that's a pattern. Write a `feedback` entry capturing the fix.

(The "2+ occurrences ⇒ promote" bar is the same one used elsewhere in the methodology — e.g., backlog items that recur land as patterns rather than one-offs. It's the threshold that separates "noise" from "rule.")

The bar for this is *category of error,* not literal identical error. If the same kind of CSS variable mistake has happened twice (different specific variables, but same pattern), it counts.

### Trigger 3: A non-obvious decision was made

A decision that future-you would not be able to reconstruct from reading the code. Common signals:

- A counter-intuitive choice ("we deliberately do not use the obvious library here because…").
- A workaround for a specific bug ("this looks redundant; it works around <bug>").
- A constraint that came from outside the code ("legal said this must be opt-in, not opt-out").
- A path-dependent choice ("we ended up here because of <previous attempt>; reverting requires understanding that history").

A `project` entry captures these.

### Trigger 4: A validated judgment call

The user confirms an unusual approach worked ("yes, that's the right call; keep doing that"). This is the *positive* counterpart to a correction — the user has just told you a non-default choice is correct for this project. Capture it as a `feedback` entry.

Without this trigger, the memory drifts toward "list of corrections" and loses the validated choices the team has accepted. Both kinds of feedback are worth saving.

---

## What NOT to save as memory

Saving things that don't belong as memory is worse than not saving them — the memory directory bloats, the index becomes unscannable, and the actual durable lessons get lost in the noise.

### Do not save:

- **Patterns derivable from reading the current code.** Architecture, file paths, naming conventions, framework choices — these can be re-derived. They belong (briefly) in the instruction file or are self-evident from the codebase.
- **Git history details.** Who changed what when is recoverable from `git log` / `git blame`. Don't snapshot it into memory.
- **Specific bug fixes after the fact.** The fix is in the code; the rationale is in the commit message. A memory entry duplicates both. (The *pattern* of a class of bug is worth a memory; a single fix is not.)
- **Ephemeral task state.** Current in-progress work, this session's plan, mid-task notes — use the task list or scratch files, not memory.
- **Anything already in the instruction file.** Memory should not duplicate the universal rules.
- **Predictions or wishes.** "We should probably move to library X someday." Either file as a backlog item (if it's real work) or discard (if it's musing). Memory is for durable facts and rules, not aspirations.
- **Sensitive information.** Credentials, personal data, internal-only URLs of a sensitive nature — never. Memory files are version-controlled and visible to everyone with repo access.

### A useful test

Before saving, ask: *will this still be useful and correct in six months?*

- "Use this specific function name to do X" — probably stale in six months; don't save.
- "Never write defensive code at trust boundaries we control internally" — durable; save.
- "The tests for module X are slow because Y" — durable until the slowness is fixed; save with the understanding that it should be removed when fixed.
- "I just fixed a typo in the README" — useless as memory; don't save.

### The admission test: derivable from source is never stored

The first "do not save" rule above generalizes into the sharpest single filter for both layers. **If a contributor can learn it by reading the repo right now, it is read live — never written down.** What earns a line is only what the source *cannot* tell you:

| Not stored (derivable) | Stored (not derivable) |
|---|---|
| The test command — it's in `package.json` | *"The suite takes eleven minutes, so run the focused file first"* |
| The directory layout — it's on disk | *"`legacy/` is mid-migration; new code goes in `core/`"* |
| Which library handles dates — it's in the imports | *"We moved off X because of its DST bug; don't reintroduce it"* |
| That a function exists — grep finds it | *"That function looks generic but is load-bearing for billing"* |

Four things pass this test: **intent, rationale, policy, and observed pitfalls.** Everything else is a snapshot of a moving target, and a snapshot is worse than nothing — it goes stale silently, and a confidently wrong instruction file costs more than an absent one.

This is also why a consolidation pass **ends smaller or equal, never larger.** An audit that grows the file has usually re-derived things the code already says. The [size budgets](04_backlog_items.md#size-budgets--context-artifacts-must-earn-their-length) give the same rule a number; this gives it a criterion.

**The asymmetry worth knowing:** admission is strict, but *retirement* is not symmetric with it. A policy or pitfall retires when the thing it guards is gone — not when it stops being mentioned. A rule that is working erases its own evidence: nobody reintroduces the DST-buggy library, so the entry looks inert precisely because it succeeded. Low reference frequency is never grounds for removal; see [Archive, don't destroy](#archive-dont-destroy-the-memory-lifecycle) and the `pinned` flag.

---

## Active context: the volatile working file

Memory (above) is *durable* — lessons and facts meant to outlive many sessions. But a contributor mid-task also carries *volatile* state: what they are doing right now, what just changed, what comes next. [What NOT to save](#what-not-to-save-as-memory) rules this out of memory deliberately — yet it still needs a home, because an AI session loses it on every context reset, and a fresh session (or a different agent picking up the work) starts blind.

Keep this state in a single **active-context file** — one short, fast-changing markdown file, separate from durable memory. A common location is `backlog/ACTIVE_CONTEXT.md` (project-wide), or one per active epic; for AI-agent work it can live alongside the agent's own files. Whatever the location, there is **one** per work-stream and it is *expected* to churn.

### What it holds

- **Current focus** — the item (`BL-###`) or goal being worked right now.
- **Recent changes** — the last few meaningful edits, with file paths, since the previous reset.
- **Next steps** — the short, ordered list of what to do next.
- **Open questions / waiting-on** — pending decisions, blockers, things to confirm.

Keep it to a screen. It is a *baton*, not a journal: when an item closes, its lines are cleared or overwritten, not accumulated. The permanent record lives in commits, the item's `ARCHIVE.md` entry, and — for durable lessons — memory.

### The save / rehydrate ritual

The file earns its keep at the two moments a session's working memory is most fragile:

- **Before a context reset** (compaction, handoff, end of session, stepping away): flush the current focus / recent changes / next steps into the active-context file *before* the context is lost. Treat it as writing a cache back to disk.
- **After a reset, or on pickup** (new session, resumed loop, or a different agent acquiring the lock): read the active-context file *first*, alongside the instruction file and the memory index, to rehydrate where the work stood. Then verify against live state (`git log`, the item's `Status:` / `Lock:`) per [Memory and current state](#memory-and-current-state) — the file is a claim about where things *were*, not proof of where they *are now*.

### Why this is separate from memory

Durable memory answers *"what have we learned?"*; active context answers *"where am I?"*. Mixing them rots both: volatile state stuffed into memory makes the index churn and buries durable lessons, while a durable lesson left in a scratch file gets cleared on the next reset. Keep the durable in `memory/`, the volatile in the active-context file. The one bridge between them — if something written as volatile context keeps reappearing (the same "next step" recurs across items), that is a [Trigger 2](#trigger-2-same-correction-or-fix-has-appeared-2-times) signal to promote it into a real memory entry.

---

## Maintenance

Memory decays. Projects evolve. A memory entry written six months ago may now be wrong (the rule changed, the workaround is no longer needed, the file it references no longer exists). Without maintenance, the memory directory becomes a graveyard of stale advice.

### Before acting on a memory

When a memory entry names a specific function, file, or flag, that's a claim it *existed when the memory was written.* It may have been renamed or removed since.

Before recommending or relying on a memory entry that names specifics:

- If it names a file path: check the file exists.
- If it names a function or flag: grep for it.
- If the user is about to act on the recommendation, verify first.

"The memory says X exists" is not the same as "X exists now." Trust but verify.

### Memory and current state

Memory captures a snapshot at the time it was written. For *current* state — what is in the repo now, what was recently changed, what the active set of items is — prefer reading the live state (`git log`, the actual files, the live backlog) over recalling a memory.

When a recalled memory conflicts with current state, trust what is observable now, and update or delete the stale memory rather than acting on it.

### Periodic consolidation

Every few months (or whenever the memory directory feels noisy), do a consolidation pass:

- **Merge duplicates.** Two entries saying the same thing should be one entry.
- **Update the wrong.** Entries that no longer match current reality get rewritten or deleted.
- **Archive the obsolete.** Entries about workarounds for bugs that have since been fixed; entries about file paths that no longer exist; entries about decisions that have been replaced. Archive these rather than deleting them outright — see [Archive, don't destroy](#archive-dont-destroy-the-memory-lifecycle) below.
- **Sharpen the vague.** Entries with one-line bodies that don't actually convey the lesson get expanded or removed.
- **Verify the index.** Every entry has an index line. Every index line resolves to an entry.

The consolidation pass is itself a kind of work. It can be filed as a backlog item with effort estimate `S` (half a day for most projects).

### Archive, don't destroy: the memory lifecycle

A memory entry moves through states: **active → stale → archived.** True deletion is reserved for entries that never carried durable value. The reflex to *delete* a stale entry throws away its lineage — the `Why:`, the incident that produced it, the record that the team once held this belief. When an entry *was* a real lesson but no longer applies, **archive it instead of deleting it.**

- **Mark stale before archiving.** On a sweep, an entry that looks obsolete but isn't obviously worthless gets `metadata.status: stale` with the date. If it is still unreferenced at the next sweep, archive it. This one-sweep delay protects entries that are merely *dormant* — tied to a paused subsystem or a seasonal workflow — from being removed the moment they go quiet.
- **Archive, don't hard-delete.** Move the entry to `memory/archive/` (or set `metadata.status: archived` and drop its index line). It leaves the live index — so it no longer costs context on every session — but the lesson and its `Why:` stay discoverable to anyone who greps. Archived entries are out of the way, not gone.
- **Pin the load-bearing ones.** Entries that guard against data loss, security regressions, or irreversible actions get `metadata.pinned: true`. A sweep never marks a pinned entry stale or archives it, no matter how rarely it is referenced — low reference frequency on a "never drop the prod database" rule means the rule is *working*, not that it is dead.
- **True deletion is for entries that never had value.** A memory capturing ephemeral state, a typo fix, or session-specific context (the things [What NOT to save](#what-not-to-save-as-memory) already rules out) can be deleted outright — there is no lineage worth keeping. Everything that was once a genuine lesson gets archived, not deleted.

Git history is the ultimate backup: a deleted entry is always recoverable via `git log` / `git show`. The archive is not about recoverability — it is about *discoverability.* A grep of `memory/archive/` surfaces "we used to believe X, and here is why we stopped" without git archaeology, and that lineage is often the fastest way to avoid re-introducing a problem the team already solved.

### Renaming and reorganizing

If a memory's name turns out to be a poor description, rename the file *and* update the index *and* update any `[[other-name]]` cross-references in other memory entries. Treat renames as small atomic changes.

---

## Worked (abstract) example of a feedback entry

```markdown
---
name: feedback-trust-internal-types
description: Don't add defensive type-checks for inputs the type system has already validated.
metadata:
  type: feedback
---

Internal-to-internal function calls do not need defensive type-checks
at the receiving side. If the type system says the input is `User`,
treat it as `User`. Re-validating with `if (!user || typeof user.id
!== 'string')` clutters the code and obscures the actual logic, and
the check cannot fail because the type system has already proved it.

This applies only to *internal* boundaries (your own code calling
your own code, with shared types). At *external* boundaries (user
input, network responses, filesystem reads), validation is required
because the type system cannot enforce contracts across the boundary.

**Why:** This came up after a code review where a contributor added
`assertIsUser(user)` calls inside every function that took a `User`
parameter. The result: 200 lines of dead code, no observable benefit,
slower reads. The cleanup took a day. The pattern persisted because
nobody had named the rule.

**How to apply:** When writing or reviewing internal functions: if
the parameter type already encodes the constraint you're about to
check, delete the check. Reserve defensive validation for trust
boundaries (HTTP route handlers, file parsers, third-party API
responses, user input from forms).

**Anti-pattern:** Wrapping internal calls in try/catch "just in case."
If the call cannot throw a recoverable error, the try/catch hides
bugs without protecting against anything real.

**Related:** [[feedback-simplicity-first]]
```

The entry is short, specific, has a `Why:`, has a `How to apply:`, and uses one cross-reference to a sibling memory. A new contributor reading it understands the rule, the rationale, and the boundary case in a minute.

---

## Worked (abstract) example of a project entry

```markdown
---
name: project-content-deletion-flow
description: Content deletions must happen on dev first; prod sync re-creates rows otherwise.
metadata:
  type: project
---

Content tables (places, articles, narratives, tags) flow one direction
only: dev → prod via the scheduled content sync. There is no prod →
dev path for content. If you delete content directly on prod, the
next content sync re-creates it from the dev dump.

Authoritative deletion workflow:
1. Delete on dev (via admin UI or the merge-duplicates script).
2. Verify dev is clean.
3. Run the content sync to push dev's state to prod. The sync removes
   the prod row in passing.

**Why:** A team member deleted a duplicate place on prod, the next
sync re-created it, and they thought they'd fixed it. Confusion cost
two days. The directionality of the sync was not documented anywhere
visible, so the lesson was easy to repeat.

**How to apply:** Any time you're about to delete content data on
prod, stop and route the change to dev first. The only safe direct-
on-prod delete is one immediately mirrored on dev before the next
sync.

**Related:** Content sync deploy command lives in `scripts/deploy.bat
content`; behavior documented in the project instruction file.
```

This entry could not be derived from reading the code. The `Why:` makes the danger concrete. The `How to apply:` gives the rule.

---

## Memory as a leading indicator for methodology gaps

When you find yourself filing memory entries that cluster around the same theme — three different `feedback_*` entries about deploy verification, five about a class of CSS-variable mistakes, four about platform-specific quirks — that cluster is a signal: **the methodology itself probably has a gap that's producing the recurring lessons.**

### The pattern

```
Single memory entry        → an individual lesson
Two related memory entries → a recurring lesson; might just be a coincidence
Three or more related     → the methodology is missing something
```

When you see three, do the work:

- **Identify the theme.** What do the related entries have in common?
- **Locate the methodology gap.** Which existing doc *should* have prevented this class of issue?
- **Update the methodology.** Add a section, strengthen an existing one, or create a new doc if warranted.
- **Reference the memory entries** in the methodology update so future readers can see the lineage.

### Why this matters

Memory entries are *symptoms.* The methodology is the *system.* If the symptoms are recurring, the system has a defect — patching individual symptoms forever is not the right response.

When the methodology absorbs the lesson, the memory entries become *redundant.* You can prune them, or leave them as historical context with a note pointing at the methodology.

### Cadence

Quarterly:

- Scan the memory directory's index.
- Group entries by theme.
- For any cluster of three or more related entries, ask: should this become a methodology addition?
- If yes: propose the addition; if accepted, add to the methodology and prune (or annotate) the underlying memory entries.

This closes the loop: real practice → memory → methodology updates → fewer recurring lessons. Without this loop, memory becomes a graveyard and the methodology becomes stale.

### The reverse loop

Sometimes the methodology gets ahead of practice — a section is written that the team hasn't yet needed. That's fine; the methodology is aspirational on those edges. But if a year passes and the section was never needed, consider whether it should be pruned or marked as optional.

The healthy state: methodology and memory inform each other continuously. Both stay current.

---

## The promotion path: from one-off correction to durable rule

The memory system, the project-instruction file, and the methodology docs form a layered hierarchy of durability. Mistakes flow upward when they prove they need to:

```
One-off correction              → handled in conversation; nothing written.
Same correction 2+ times        → write a memory entry. (See "When to write" above.)
Memory entry referenced often   → consider promoting to the instruction file.
Cluster of 3+ related entries   → consider absorbing into the methodology.
```

Each layer raises the bar for what survives. Memory is project-specific. The instruction file is universal-within-the-project. The methodology is universal-across-projects. Promoting a rule moves it from one scope to a broader one, and demands a higher level of confidence that the rule will hold.

### Stage 1 → 2: in-conversation correction → memory entry

Covered above under [When to write a new memory](#when-to-write-a-new-memory), Trigger 2. Once the same category of mistake has occurred twice in different contexts, the cost of leaving it unwritten exceeds the cost of writing it. Capture the pattern.

### Stage 2 → 3: memory entry → instruction file

A memory entry has *graduated* and belongs in the instruction file when:

- **It's been referenced explicitly in 3+ contributor sessions** as a rule the contributor needed to remember. Frequent reference is a signal of universality.
- **It applies to every task, not some tasks.** Memory holds the conditional rules; the instruction file holds the universal ones. If you keep loading the same memory entry for unrelated work, it's no longer conditional.
- **It's been validated across multiple subsystems.** A rule that holds in one corner might be a local quirk; a rule that holds across the codebase is a project convention.
- **It captures a hard constraint.** "Never do X" rules — especially those guarding against data loss, security regressions, or irreversible actions — belong in the instruction file even at low reference frequency. The cost of missing them is too high.

When promoting:

1. Add the rule to the appropriate section of the instruction file (Hard Rules, Code Conventions, etc.).
2. **Delete the memory entry** (don't leave both — duplicates drift). Remove its index line.
3. Note the promotion in the commit message so the audit trail is intact.

### Stage 3 → 4: instruction file → methodology addition

This is the upward limit. A rule belongs in the methodology when:

- **It generalizes beyond the current project.** Other projects with different stacks, different domains, different team sizes would benefit from the same rule.
- **It's the answer to a recurring class of problem, not a project-specific quirk.** "Always validate at trust boundaries" is methodology-scale; "validate the `userId` parameter in route X" is not.
- **It's been captured in the instruction files of 2+ projects.** Real cross-project validation is rare and valuable.

Methodology additions go via the patterns in [Memory as a leading indicator for methodology gaps](#memory-as-a-leading-indicator-for-methodology-gaps).

### Pressure-test before promoting

A rule that holds in the calm of the moment it was written can still fail under the conditions where rules actually get broken. Before promoting one up a layer (memory → instruction file, or instruction file → methodology), stress it against the situations that break rules:

- **Deadline pressure.** Does it still hold when the work is due in an hour? A rule everyone abandons under pressure isn't a rule — it's a preference. Either harden it (and state *why* it survives pressure) or keep it advisory.
- **Sunk cost.** Does it hold after a day of work has already gone the other way? Rules that demand throwing away effort are the first ones rationalized away; the rule needs a `Why:` strong enough to justify the loss.
- **The confident-wrong case.** Does it hold when the contributor is *sure* the exception applies? Most violations feel justified in the moment. State the trigger precisely enough that "I'm sure this one is different" doesn't qualify.
- **Edge cases.** Name two or three concrete situations at the rule's boundary and check it gives a sensible answer in each. If it doesn't, scope it down to where it does.

A rule that survives the stress earns promotion — and should carry the reasoning that got it there. A rule that cracks gets narrowed, kept advisory in memory, or dropped. Promoting a brittle rule just teaches contributors to route around the layer it lives in.

### Why explicit promotion matters

Without the named loop: mistakes get fixed in conversation, forgotten, recur, get fixed again, recur, get added to memory once someone notices, sit in memory forever even after they've graduated, and never reach the instruction file or the methodology where they would prevent the failure mode systematically.

Naming the loop names the trigger. The trigger triggers the promotion. The promotion makes the rule durable.

### The reverse loop: demotion and deletion

Rules also flow downward when they no longer hold:

- A methodology rule that turns out to be over-specified → mark optional or remove.
- An instruction-file rule no longer needed → delete (the codebase has evolved past the failure mode).
- A memory entry whose underlying bug has been fixed → delete the entry. Don't keep historical bandages.

The healthy state: each rule lives at the lowest layer that captures its actual scope. No higher, no lower.

---

## How memory connects to the rest of the methodology

- **Memory → Working Principles** ([06_working_principles.md](06_working_principles.md)). The principles are the universal rules; memory captures the specific lessons that come from applying them in this project's context.
- **Memory → Definition of Done** ([07_definition_of_done.md](07_definition_of_done.md)). Recurring DoD-related failures (a class of UI regression, a class of test gap) often become memory entries. The memory then prevents the failure on the next item.
- **Memory → Backlog items** ([04_backlog_items.md](04_backlog_items.md)). A memory entry sometimes inspires a backlog item ("we keep working around this; let's fix it"). The item and the memory can co-exist; once the item lands, the memory may need updating.
- **Memory → Strategy / Pillars / Epics** ([01_strategy.md](01_strategy.md), [02_pillars.md](02_pillars.md), [03_epics.md](03_epics.md)). Higher-level docs are the *plan;* memory captures the *experience.* When experience contradicts plan repeatedly, that is a signal for re-evaluation.

---

## Common mistakes around memory

| Mistake | Fix |
|---------|-----|
| Memory entry has no `Why:`. | Add the rationale. Without it, edge cases cannot be judged. |
| Memory entry duplicates a rule already in the instruction file. | Delete the memory; the instruction file is the universal rule. |
| Memory entry is a wish ("we should use library X"). | File as a backlog item instead. Memory is for facts and rules, not aspirations. |
| Memory entry has gone stale (file/function it references no longer exists). | Update it, or archive it if the lesson once mattered. Stale memory left in the live index is worse than no memory. |
| Stale entry was hard-deleted, losing its `Why:` and lineage. | Archive instead (`memory/archive/` or `metadata.status: archived`). Reserve outright deletion for entries that never carried durable value. |
| Index has an entry the body doesn't, or vice versa. | Audit and reconcile. The index is the navigational truth. |
| Memory directory is unmaintained for over a year. | Run a consolidation pass. Prune, merge, sharpen. |
| Same lesson is captured in two entries with different angles. | Merge into a single entry; reference both angles in the body. |
| Memory entry is hundreds of lines long. | Probably belongs as a regular doc (pillar, architecture refinement, design doc). Memory is for short, focused lessons. |
| User explicitly said "forget this" but the entry is still there. | Delete the entry. Honor explicit forget requests. |
| Memory references session-specific context ("the bug I fixed last Tuesday"). | Generalize the lesson. Session context decays; the durable pattern does not. |
| Volatile "where am I" state (current focus, next steps) stuffed into a memory entry. | Move it to the [active-context file](#active-context-the-volatile-working-file). Memory is for durable lessons; the active-context file is for session state. |

---

## Authority

Memory entries are *advisory.* They are accumulated experience, not authoritative rules. They are intended to make contributors faster and to prevent repeated mistakes, not to override explicit current direction.

When a memory entry conflicts with current user direction, current direction wins. The memory may need updating (and probably does — the user explicitly disagreed with the captured rule). Surface the conflict, ask whether to update or delete, and proceed.

When two memory entries appear to conflict, the contributor should surface the conflict to the user. Memory entries are not refereed by an editor; conflicts are resolved by humans.

The project-instruction file is more authoritative than memory. Memory cannot override the instruction file; only the user or an explicit project decision can update the instruction file. When in doubt, the instruction file wins.

Working principles ([06_working_principles.md](06_working_principles.md)) and Definition of Done ([07_definition_of_done.md](07_definition_of_done.md)) are foundational; memory cannot override either. Memory adds *project-specific* color on top of these universal layers.

---

**Next:** [09 — Git workflow](09_git_workflow.md)
