# 09 — Git workflow

> **Purpose:** define the git practices that keep the project navigable, auditable, and safe — for both human contributors and AI agents operating in parallel. These practices are not aesthetic; each one prevents a specific class of failure.

Every rule here exists because the absence of it has caused real damage. Read them as preventive measures, not preferences.

---

## Branch protection

### The rule

The primary branch (`master`, `main`, or whatever the project calls it — referred to below as **the trunk**) is protected.

- **Never force-push to the trunk.** Force-pushing destroys history that other contributors have built on. It is one of the few git operations that can quietly lose committed work.
- **Never commit directly to the trunk.** All work lands via pull request.
- **All merges to the trunk go through PRs.** This gives review surface, runs CI, and produces an audit-quality merge commit.

These rules apply to humans and AI agents identically. No contributor is "trusted enough" to skip them — the rules exist because the failure modes are equally bad regardless of who triggers them.

### Why this matters

- Force-push to trunk can erase work that other branches were depending on. The recovery is painful and sometimes incomplete (commits referenced only from the lost ref may be garbage-collected before recovery).
- Direct commits bypass review and CI. The first time a direct commit breaks the build, every other contributor pulling the trunk is broken too.
- A reviewed-PR-only trunk produces a clean, auditable history where every change has context (the PR body) and approval signal.

### When to break the rule

Almost never. The exceptions are:

- Initial repo setup, before there are other contributors.
- Recovering from a catastrophic mistake (e.g., a secret was committed) — and even then, only with explicit user direction, communicated to all contributors first.

If you find yourself wanting to force-push to recover from a small problem, stop and find a non-destructive path. Reverts, new commits, and PRs are almost always available.

---

## Branch naming

Branches are named by intent and content.

### Prefix by intent

```
feature/<slug>   # new functionality
fix/<slug>       # bug fix
chore/<slug>     # tooling, dependencies, infrastructure
refactor/<slug>  # restructuring without behavior change
docs/<slug>      # documentation-only changes
test/<slug>      # test-only changes
release/<slug>   # release preparation
```

### Slug rules

- **Kebab-case.** `add-csv-export`, not `add_csv_export` or `AddCsvExport`.
- **Descriptive but short.** Under 50 characters when possible.
- **Action-oriented when feasible.** `fix-date-parser-overflow` beats `date-parser`.
- **Item reference is welcome but optional.** `feature/bl-0428-csv-export` is fine. So is `feature/csv-export`.

### Examples

```
feature/add-csv-export
fix/date-parser-overflow
chore/upgrade-typescript-to-5-4
refactor/extract-session-middleware
docs/methodology-rollout
test/regression-for-bl-0517
```

### Why named branches matter

- A branch list (`git branch -a`) is a quick view of what is in flight. Cryptic names defeat this.
- Tooling (CI, deployment pipelines, automation) often keys off branch prefix. A consistent prefix scheme makes the tooling reliable.
- When picking up someone else's abandoned branch, a clear name tells you what they were working on without reading commits.

---

## Commit cadence

### The rule

**Commit and push after every completed sub-task once tests pass locally.** Do not accumulate giant uncommitted change sets.

### What counts as a sub-task

- A logical unit of progress on the current item: a new function with its tests, a schema change applied and verified, a refactor of one module.
- Something the contributor would describe in a single sentence: "added the validation," "split the helper into two," "wrote the regression test."

### Why frequent commits

- **Crash protection.** An uncommitted hour of work, lost to a power outage or process crash, is gone. Committed work survives.
- **Visibility.** A series of commits with clear messages is easier to review than a 500-line monolithic commit.
- **Bisection.** When a bug appears later and `git bisect` is used to find the introducing commit, smaller commits localize the bug more precisely.
- **Revert granularity.** A targeted revert of one sub-change is possible only if that sub-change was its own commit.

### Why "once tests pass locally"

Committing broken intermediate states bloats the history with noise and breaks bisection. The discipline is: complete a coherent sub-task, run the relevant tests, commit. If a long sub-task naturally produces broken intermediate states, keep them local until the sub-task is consistent, then commit the consistent end state.

### When pushing matters

Push the commits often, too. A local-only commit:

- Cannot be reviewed.
- Does not back up to the remote.
- Cannot be pulled by collaborators.
- Does not advance any lock-related visibility (see [05_locks_and_parallel_work.md](05_locks_and_parallel_work.md)).

Default to push-after-every-commit on the active branch. Branches in flight should always be visible on the remote.

---

## Commit message convention

Follow conventional-commits style:

```
<type>(<scope>): <subject>

<optional body>

<optional footer>
```

### Types

| Type | When to use |
|------|-------------|
| `feat` | New behavior visible to the user or an external system. |
| `fix` | Bug fix. The diff demonstrably corrects broken behavior. |
| `chore` | Tooling, deps, configuration, housekeeping. No user-visible change. |
| `refactor` | Restructuring code with no behavior change. |
| `docs` | Documentation changes only. |
| `test` | Tests added or changed (without changing tested behavior). |
| `release` | Version bumps, release-tag commits. |
| `perf` | Performance improvement (provable, with measurement). |
| `revert` | Reverts a prior commit. Body must name the reverted commit. |

### Scope

A short, lowercase identifier of what part of the codebase the commit touches: `(api)`, `(web)`, `(backlog)`, `(deploy)`, `(auth)`. Optional but useful for grep.

### Subject

- **Imperative voice.** "add" not "added" or "adds." Reads like a command to the codebase.
- **No trailing period.**
- **Under 70 characters.** Most git tools truncate longer subjects.
- **Capitalization: lowercase is standard for conventional commits.** Some projects use sentence case; pick one and stay consistent.

### Body and footer

- Body: paragraphs separated by blank lines. Explain *why* the change is being made, not *what* the diff already shows.
- Footer: machine-parseable metadata. `Closes BL-0428.` `Co-authored-by: ...` `BREAKING CHANGE: ...`.

### Examples

```
feat(api): add CSV export endpoint for activity report

Operators currently re-key totals manually. The new endpoint streams CSV
matching the on-screen table filter state.

Closes BL-0428.
```

```
fix(web): handle empty trip data in summary card

The card threw on `trips.length === 0` because of an unguarded `.reduce`.
Added a guard plus a regression test.

Closes BL-0517.
```

```
chore(deps): upgrade typescript to 5.4

No behavioral change. Picks up new control-flow narrowing.
```

```
refactor(auth): extract session validation into shared helper

No behavior change. Three routes were duplicating the same check; now
they all call validateSession() from the shared module.
```

```
docs(methodology): add 09 git workflow

Initial draft of the git practices doc.
```

### What not to commit

- **Generic messages** like `fix stuff`, `wip`, `update`, `more changes`. They are noise.
- **Multiple unrelated changes in one commit.** Split them.
- **Generated files** (build artifacts, lock files where appropriate, anything in `.gitignore` that slipped past).
- **Secrets.** API keys, tokens, passwords, `.env` files. Never. If a secret is committed by accident, treat it as compromised: rotate immediately, then scrub history (force-push *coordinated*, not silent).
- **Personal identifiers** that don't need to be there. Git authorship handles names; full email addresses or other personal info shouldn't appear in commit content.

---

## PR discipline

Pull requests are the unit of review. Each PR should be readable, scoped, and traceable.

### PR title

- Under 70 characters.
- Imperative, like a commit subject.
- Often the same as the headline commit's subject, but written for the broader PR scope.

### PR body

Two sections, always:

```markdown
## Summary

- <Bullet 1: what changed and why.>
- <Bullet 2: any non-obvious decision.>
- <Bullet 3: any tradeoff worth flagging.>

## Test plan

- [ ] <Specific verification step 1>
- [ ] <Specific verification step 2>
- [ ] <Specific verification step 3>
```

#### Summary

One to three bullets. *What* changed, *why* it changed. Not a diff recap — the diff is right there. Highlight the parts the reviewer would otherwise miss.

#### Test plan

Specific, checkable verifications. Match the [Definition of Done](07_definition_of_done.md) gates relevant to this change:

```markdown
- [ ] Ran the full test suite locally; all tests pass.
- [ ] Manually verified the CSV download in the activity report at /reports.
- [ ] Verified the export respects the date-range filter.
- [ ] Verified in both light and dark themes.
- [ ] Updated CHANGELOG.md and README.md.
```

### Tie to backlog items

Every PR should close at least one BL-### item. Reference it explicitly:

```
Closes BL-0428.
```

The word matters — `Closes`, `Fixes`, `Resolves` — pick one and stay consistent. Many tools auto-link these.

### Co-author credit

Never include co-author credit unless explicitly agreed. Auto-adding a `Co-authored-by: ...` line for an AI agent is a project-by-project decision, not a default.

### PR size

- **Small PRs are best.** Easier to review, faster to merge, lower regression risk.
- **A PR that touches more than 500 lines** (excluding generated files, snapshots, etc.) deserves a second look — is it actually one change, or should it be split?
- **A PR that touches more than 1000 lines** is almost always too big. Split.

### What not to put in a PR

- **Multiple unrelated items.** One PR closes one (or a few tightly-coupled) items.
- **WIP commits left in.** Squash or rewrite before opening.
- **Debug code left in.** `console.log`, commented-out blocks, scratch comments.
- **Secrets, generated files, lock-file changes unrelated to the work.**

---

## Pre-commit hooks

### The rule

The project should have hooks for linting, type-checking, and formatting. **Never bypass hooks** (`--no-verify` and equivalents) unless the user has explicitly authorized it for that specific commit.

### Why hooks exist

Hooks catch the cheap-to-prevent failures: a missing import, an unformatted file, a type error. CI will also catch these, but CI runs minutes later — the local hook saves the round-trip.

### What to do when a hook fails

1. **Read the failure.** Hooks usually say what went wrong.
2. **Fix the underlying issue.** Re-stage the fix and commit again.
3. **Do not bypass.** A bypass-and-promise-to-fix-later almost always becomes a bypass-and-forget.

### When bypass is allowed

The user has explicitly said "skip hooks for this commit" — usually because the hook itself is broken and fixing it is being separately tracked. In that case:

- Use `--no-verify` (or equivalent) for *that one commit.*
- Note in the commit body or PR description *why* the hook was bypassed.
- File an item to fix the hook if it isn't already filed.

The agent never decides to bypass on its own. If a hook is failing repeatedly and seems broken, surface the observation; let the user direct.

---

## Never amend published commits

### The rule

Once a commit is pushed to a shared branch, it is history. **New commits, not `--amend`.**

### Why

Amending a published commit changes its hash. Other contributors who have pulled the original commit now have a divergent history. The conflict is hard to resolve cleanly and easy to resolve destructively (force push, lose work).

A new commit, by contrast, advances history without rewriting it. Everyone's local clones converge naturally.

### Local-only amend is fine

A commit that exists only in your local working directory (never pushed) can be amended freely. The hash change has no other reference yet.

### Squashing before opening a PR

If you have a long messy local history and want to clean it before opening the PR, squash it locally. Once the PR is open, the commits inside it are part of the shared history — further history rewrites should be done with care and coordination.

### Recovering from a bad commit

- **The change isn't merged yet:** open a new commit reverting or correcting.
- **The change is merged:** use `git revert` to produce a new commit that undoes it.
- **The change broke the trunk:** revert immediately, then fix on a feature branch. Do not attempt to "patch the trunk forward" with hot commits; revert first to restore the trunk, then re-do the work cleanly.

---

## Worktrees for parallel agents

### The problem

When two or more contributors (humans, AI agents, automation) are working in the same checkout of the repo at the same time, dangerous shared state appears:

- One contributor's `git checkout other-branch` changes HEAD; the other contributor's working files now point at a different branch than they think.
- Two contributors committing to different branches in the same working tree race on staged changes.
- An AI agent's session that finishes by checking out `master` strands another session's commits on a feature branch — those commits may end up referenced from nowhere and lost to garbage collection.

### The solution

Use `git worktree` to give each contributor (especially each AI agent session) an isolated working tree.

```
git worktree add <path> <branch>
```

For example:

```
git worktree add ../project-agent-a4f2 feature/csv-export
git worktree add ../project-agent-b193 feature/date-fix
```

Each session operates in its own directory. HEAD-shifts in one tree do not affect the other. Commits, branches, and config are shared (it is the same repository), but the workspace is independent.

### When to use a worktree

- **Multiple AI agent sessions** active in the same repository at the same time. The default.
- **Long-running work** that you want isolated from quick fixes you also want to make.
- **Parallel branches** you are actively comparing or testing.

### When not to use a worktree

- A single session in a single workspace — no benefit.
- Trivial work (read-only investigation) — no benefit.

### Cleanup

When the worktree is no longer needed:

```
git worktree remove <path>
```

Or, if the directory is already gone:

```
git worktree prune
```

A *recurring failure to clean up* worktrees clutters the disk and the worktree list. Build cleanup into the end of the session.

### Symlink / junction caution

Do not create filesystem links from inside a worktree to the parent repo's directories (especially package directories like `node_modules`). When the worktree is removed, the link is followed and the target is emptied. This has happened in real projects and is brutally destructive.

If you need shared installation state (e.g., a shared package cache), use the package manager's native shared-cache feature, not filesystem links.

---

## Destructive command discipline

Some git commands cannot be cleanly reversed. Treat them with extreme care.

### The list

| Command | What it does irreversibly |
|---------|---------------------------|
| `git push --force` | Overwrites the remote branch. If others have based work on the previous version, their work becomes orphaned. |
| `git push --force-with-lease` | Safer than `--force` but still rewrites; safe only if no one else has pushed since you pulled. |
| `git reset --hard` | Discards uncommitted changes and resets HEAD. Local-only work is gone. |
| `git checkout .` / `git restore .` | Discards uncommitted changes in the working tree. |
| `git clean -fdx` | Removes untracked files and ignored files. Includes the contents of `.gitignore`. |
| `git branch -D` | Force-deletes a branch even if unmerged. The branch's commits may become unreachable. |
| `git worktree remove --force` | Removes a worktree with uncommitted changes. |
| `git rebase --onto` | Rewrites commits onto a new base; can lose commits if mishandled. |
| `git filter-branch` / `git filter-repo` | Rewrites history. Heavy-handed; usually for secret-scrubbing. |
| `rm -rf <repo>` | Removes the working tree. |

### The rules

- **AI agents do not run these autonomously.** If an AI agent decides a destructive command is needed, it surfaces the intent and waits for explicit user confirmation. "I'm about to run `git reset --hard origin/main`; this will discard your local uncommitted changes. Confirm?"
- **Humans run them with care.** Before destructive commands, ask: *is there a safer alternative?* A revert instead of a force-push; a stash instead of a reset; a soft-delete-then-archive instead of a `branch -D`.
- **Investigate unfamiliar state before deleting.** A branch you don't recognize might be someone else's in-flight work. A file you don't recognize might be a partial result of a fix. Look before you delete.

### Recovery

When a destructive command has caused damage:

- `git reflog` shows recent HEAD movements; lost commits often live there until garbage collection runs.
- Backups of the remote (your hosting platform's mirror, or an internal mirror) may have the lost state.
- The longer you wait to recover, the higher the chance the data is collected.

Move fast on recovery. Move slow on the original destructive command.

---

## Production deploys

### The hard rule

If the project has a production deploy path — a script, a CI workflow, a CLI command — **AI agents never run it autonomously.** Production is the user's domain.

This applies regardless of permissions. Even if the agent has the technical capability to run `deploy.sh production`, it does not. Production deploys carry consequences that an AI cannot fully evaluate: customer impact, data implications, timing relative to incidents, regulatory considerations.

### Why this is absolute

A bad production deploy can:

- Take the product offline for paying users.
- Corrupt the production database if the deploy includes a migration.
- Trigger billing or notification events that affect real people.
- Violate change-window policies that bind the team.

None of these is recoverable by reverting code. They require operational response.

### How to document the deploy command

In the project instruction file, document the deploy command with a clear warning:

```markdown
## Deploy

Production deploy is run via:

  scripts/deploy.bat production

**This command is user-only.** AI agents and automated workflows must
never run it. The user controls the timing of every production deploy.

For dev or staging deploys, use:

  scripts/deploy.bat staging
```

The warning is not subtle on purpose. It tells future contributors immediately that this is off-limits.

### What an AI agent can do

- Prepare the deploy: ensure the code is ready, the changelog is updated, the release tag is right.
- Stage the deploy in non-production environments.
- Write deploy scripts and runbooks.
- Verify the deploy after the human runs it.

What the agent cannot do is push the button. The button is the human's.

---

## Conflict resolution

Merge conflicts are normal. Resolving them carelessly is not.

### The rule

**Prefer resolving merge conflicts to discarding work.** Investigate whose change is whose before picking a side.

### The process

1. **Pull the latest from the trunk into your branch.** Conflicts surface.
2. **For each conflict:** open the file, read both sides, understand what each change was trying to accomplish.
3. **Reconcile.** Sometimes you keep one side. Sometimes you keep both (one merged into the other). Sometimes the conflict reveals that two contributors went in different directions and the right answer is to talk.
4. **Run the tests.** Conflict resolution can produce syntactically valid but semantically broken code.
5. **Commit the merge.** The commit message says "Merge X into Y; reconciled <field> in favor of <approach>" so future readers understand what was decided.

### Anti-patterns

- **`git checkout --theirs` / `--ours` without reading.** You may discard real work or keep stale work without realizing.
- **Stash, rebase, and "deal with conflicts later."** Later is now. Resolve.
- **Edit the conflicted file blindly to make it compile, without understanding both sides.** A compile-clean reconciliation is not necessarily a correct one.
- **Force-push to bypass the conflict.** This is the silently-destructive path.

### When the conflict is large

If the merge conflict is so large that you don't know how to resolve it, stop and surface the situation. A 30-file conflict between two long-lived branches is usually a sign that branches diverged too long; the right answer is a coordinated re-merge, not a heroic single-contributor reconciliation.

---

## Audit trail

Git history is the project's permanent record. Every commit, every PR, every backlog state change is preserved.

### What this enables

- **`git log -p -- <file>`** shows every change to a specific file with diffs. Useful for understanding why a decision was made.
- **`git blame <file>`** annotates each line with its last-modifying commit. Useful for finding the commit that introduced a particular line.
- **`git log --grep="<pattern>"`** searches commit messages. Useful for finding all commits related to an item or topic.
- **`git log --all --source`** with the right filters can reconstruct what happened on branches that have been deleted.

### Backlog state changes are commits too

Every change to a `BACKLOG.md` or `ARCHIVE.md` — adding an item, flipping a status, acquiring or releasing a lock — is a git commit. This makes the *backlog* itself fully auditable. See [05_locks_and_parallel_work.md](05_locks_and_parallel_work.md) for the lock audit pattern.

### Implications

- Treat commit messages as documentation. They will be read months later by people who do not have the context you have right now.
- Treat commits as durable. A messy commit history is a permanent tax on every future reader.
- Treat the audit trail as evidence. In an incident, the git history is often the first source consulted.

---

## PR body skeleton

Paste this when opening a new PR:

```markdown
## Summary

- <One bullet describing what changed and why.>
- <Optional bullet for a non-obvious decision.>
- <Optional bullet for a tradeoff worth flagging.>

## Test plan

- [ ] <Specific verification step 1>
- [ ] <Specific verification step 2>
- [ ] <Specific verification step 3>

Closes BL-###.
```

If the PR closes multiple items: `Closes BL-###, BL-###.`

---

## Conventional commit examples (copy-paste reference)

```
feat(<scope>): <imperative subject under 70 chars>

<Optional body. Why, not what.>

Closes BL-###.
```

```
fix(<scope>): <imperative subject>

<Body explaining the bug and the fix.>

Closes BL-###.
```

```
chore(deps): upgrade <package> to <version>

<Body if the upgrade requires action by callers.>
```

```
refactor(<scope>): <imperative subject>

No behavior change. <Why the restructure was needed.>
```

```
docs(<scope>): <imperative subject>
```

```
test(<scope>): add regression test for <bug>

Closes BL-### (regression test for the fix in BL-###).
```

```
release: v<version>

<Changelog summary.>
```

```
revert: "<original commit subject>"

This reverts commit <hash>.

<Why the revert.>
```

---

## Worktree command reference

```bash
# Create a new worktree at <path> on <branch>
git worktree add <path> <branch>

# Create a new worktree on a new branch
git worktree add -b <new-branch> <path> <base-branch>

# List all worktrees
git worktree list

# Remove a worktree (clean state)
git worktree remove <path>

# Remove a worktree forcefully (uncommitted changes will be lost)
git worktree remove --force <path>

# Clean up stale worktree entries (directories already deleted)
git worktree prune
```

---

## Operational work (deploys, pipelines, runbooks)

Most real projects have operational concerns beyond writing code: deploys, data pipelines, scheduled jobs, monitoring, on-call response. The methodology covers code workflow; operational workflow is project-specific. But certain patterns transfer.

### The pattern set

| Pattern | Why it matters |
|---|---|
| Document the deploy command(s) in the project instruction file. | Future contributors (and the AI) need to know how to ship. |
| Mark which commands are user-only (AI never runs). | Production deploys, destructive backfills, data resets — these are the user's domain. |
| Backup before any destructive operation. | A backup taken five minutes before a wrong-button-press is the cheapest recovery. |
| Smoke-test after deploy. | A successful deploy that doesn't smoke-test isn't proven to have moved real state. |
| Have a runbook for common ops. | Restarting a service, rotating a credential, rolling back a release — write the steps down so they can be followed under pressure. |
| Separate dev / staging / production environments cleanly. | The boundary between these is where most operational incidents happen. |
| Idempotent batch jobs. | A re-run of a stuck job should produce the same end state, not corrupt it. |
| One-way data flows where possible. | If content syncs from dev to prod, never the reverse, the failure modes shrink. |

### Operational items in the backlog

Backlog items can be operational, not just code:

- "Run the monthly content sync to prod."
- "Rotate the API key for the third-party service."
- "Investigate the spike in 500 errors on Tuesday."

These follow the same item lifecycle (`Status`, `Test`, `Lock`) as code items. The `Test:` for an operational item might mean "the spike subsided" or "the rotation completed and the smoke test passed." Adapt the DoD gates to the operation; the principle (verifiable completion) stays the same.

### Operational epics

A project may have epics dedicated to operational work — e.g., "Set up monitoring," "Build the disaster recovery runbook." Charter them like any other epic. The pillar may be cross-cutting (often the quality / feedback pillar, or a dedicated operations pillar).

### What the methodology deliberately doesn't specify

- Specific deploy tooling (CI, container orchestrator, hosting platform).
- Specific monitoring stack.
- Specific incident response procedures.
- Specific runbook formats.

These are too project-specific to fix. The methodology asks you to *have* them; it doesn't tell you *which* ones.

### The hard rule for operational work

If your project has production state (real users, real data, real money), **never automate destructive operations without an explicit user-authorized step.** Automation is fine for backups, deploys to staging, scheduled jobs that don't destroy state. Automation that drops tables, rolls back data, or cancels payments needs a human in the loop.

---

## How the git workflow connects to the rest of the methodology

- **Git → Working Principles** ([06_working_principles.md](06_working_principles.md)). Surgical-change discipline lives in the commit boundary. Frequent small commits make principles enforceable; one giant commit conceals violations.
- **Git → Definition of Done** ([07_definition_of_done.md](07_definition_of_done.md)). The DoD's documentation gate, archive update, and lock release all land as parts of the PR. The PR is the artifact that proves DoD was met.
- **Git → Backlog items** ([04_backlog_items.md](04_backlog_items.md)). Items are closed by PRs; commits reference items by ID. The audit trail between code and backlog is provided by git messages.
- **Git → Lock mechanism** ([05_locks_and_parallel_work.md](05_locks_and_parallel_work.md)). Lock acquires and releases are commits. Branch protection ensures no one bypasses the lock by committing direct to trunk.
- **Git → Memory** ([08_lessons_and_memory.md](08_lessons_and_memory.md)). Some lessons learned are *about* git practice (a destructive-command incident becomes a memory entry; a coordination failure becomes one). Memory captures the lessons git history doesn't.

---

## Common mistakes around git workflow

| Mistake | Fix |
|---------|-----|
| Direct commit to the trunk for "a small thing." | Open a PR. Small PRs land quickly. The exception is not worth the precedent. |
| Force-pushed to the trunk after a bad merge. | Recover via reflog and your hosting platform's branch backup. Resolve to never do this again. |
| Generic commit messages ("wip," "update," "fix"). | Rewrite locally before pushing. After pushing, follow up with better messages or a clean revert+redo. |
| Long-running branch is many commits behind the trunk. | Pull the trunk into the branch regularly. Conflicts grow non-linearly with divergence. |
| Hooks bypassed without explanation. | Bring the bypass to surface. Either fix the underlying issue or file an item for the hook itself. |
| Stale branches lingering on the remote for months. | Periodic cleanup: delete merged branches. Keep unmerged in-progress branches; archive abandoned ones with a tag. |
| PR with no test plan. | Add one. Specific, checkable verifications. The DoD requires it. |
| PR closes an item but doesn't reference it. | Add `Closes BL-###.` so the tooling and humans both make the connection. |
| Co-author trailers added without permission. | Remove them. Authorship is consensual. |
| AI agent ran `git reset --hard` on the user's working tree. | Surface and confirm before destructive operations. Recover via reflog if possible. |
| Production deploy run by automation that wasn't supposed to. | Hard rule violation. Audit how it happened; restore boundary. |

---

## Authority

The git workflow rules bind every contributor — human or AI. They are not aesthetic preferences; they are preventive measures.

When a user explicitly directs a workflow exception (e.g., "force-push this to recover from yesterday's bad merge"), the exception applies to that specific operation, not to the rule generally. The next operation reverts to the standard rules unless the user states otherwise.

When a contributor (human or AI) is uncertain whether an operation is allowed, the safe path is to ask. The cost of a question is small; the cost of an unintended destructive operation can be large.

Destructive operations are the most-protected category. AI agents never run destructive operations autonomously. Humans run them with care and a recovery plan.

---

**Next:** [10 — Testing and verification](10_testing_and_verification.md)
