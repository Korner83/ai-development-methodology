# 05 — Locks and parallel work

> **Purpose:** define the file-based lock mechanism that lets multiple humans and AI agents work the same backlog concurrently without collision. The lock is the authority for who is currently working an item; it has a time-to-live (TTL), it is git-tracked, and it requires no external service.

The lock lives on the `Lock:` field of the backlog item's frontmatter table (see [04_backlog_items.md](04_backlog_items.md)). The protocol is small enough that humans and AI agents can both follow it, and audit-friendly enough that every change is a commit.

---

## The problem

A backlog used by more than one contributor — and especially one used by AI agents that can read and write to the same files — needs a way to answer "is anyone currently working this?" without ambiguity.

Without an answer:

- Two contributors pick the same item at the same time. Both do the work. The second to push hits merge conflicts. The duplicated effort is wasted.
- A contributor abandons an item mid-flight. The next contributor cannot tell whether the abandoner is coming back. They either wait (and the work stalls) or they pick it up (and risk colliding when the abandoner returns).
- An AI agent crashes during work. No one knows whether to wait for it.
- A contributor "claims" items verbally or in chat. The claim is invisible to anyone who is not in the channel at that moment.

The standard solutions either don't fit or are too heavy:

- A central locking service (database row, distributed lock service): adds a runtime dependency, a single point of failure, an external system to keep healthy, and an API to learn. Out of proportion for a markdown backlog.
- Issue-tracker "assignment" fields: relies on the tracker being authoritative and reachable. Doesn't help when the local files are canonical.
- Chat-channel announcements: ephemeral, not greppable, missed by anyone who joined late.
- Honor system: works at small team sizes; breaks the moment AI agents are in the loop, because honor is hard to encode.

The file-based lock with TTL solves these. It is the same data the rest of the backlog uses (markdown frontmatter), tracked by the same tool (git), audited by the same mechanism (commit history). No new dependencies. No new service to babysit. And the TTL makes it self-healing — a crashed lock-holder cannot wedge an item forever.

---

## The solution: file-based locks with TTL

Every backlog item carries a `Lock:` field. Two valid states:

```
Lock: —
```

**Unlocked.** The item is free. Anyone may acquire it.

```
Lock: <holder>@<ISO-8601-timestamp>
```

**Locked until the timestamp expires.** The named holder is currently working the item. Until the timestamp passes, no one else may acquire it.

That is the entire mechanism. Everything below is the protocol that operates on this field.

### Why an em dash for "unlocked"

The em dash (`—`) is visually distinct from a holder string. It is hard to mistake for a typo. Grep tools display it cleanly. Markdown tables render it cleanly. Compared to alternatives (`null`, empty string, `none`), it is more readable in a frontmatter table that humans skim.

### Why an ISO-8601 timestamp

ISO-8601 is unambiguous, sortable, and timezone-aware. Compared to "2 PM Tuesday" or epoch seconds:

- A human reading the frontmatter table can immediately tell whether the timestamp is past or future.
- A script can parse it with one line.
- It works across timezones — every collaborator in any region reads the same wall-clock semantics.

The recommended format is `YYYY-MM-DDTHH:MMZ` (UTC, minute precision). Higher precision is unnecessary for this purpose.

---

## Why TTL

The lock has a time-to-live for one critical reason: **lock-holders die.**

- An AI agent's session ends without explicit cleanup.
- A human contributor closes their laptop and goes on vacation.
- A process crashes mid-task.
- A network partition cuts off the holder from the repo.

Without a TTL, every such event would leave a lock in place indefinitely. The item would become un-pickable, and someone would have to manually decide it's safe to clear — without good information about whether the holder is still active.

With a TTL:

- The lock holder is responsible for refreshing it (re-committing with a later timestamp) before it expires, if they need more time.
- A dead lock-holder cannot wedge the item — the lock expires automatically within the TTL.
- The next contributor doesn't need to make an interpretive call; they read the timestamp and the wall clock tells them whether the lock is still alive.

The cost of refreshing the lock periodically is one commit + push. The cost of a stuck lock without a TTL is human investigation, ambiguity, and trust erosion.

---

## The acquire protocol

Before starting work on an item, every contributor (human or AI) must follow this protocol:

```
1. Pull the latest changes from the repo so the Lock: field is current.
2. Read the item's Lock: field.
3. Decide:
   - If Lock: —, the item is free. Proceed to acquire.
   - If Lock: <holder>@<timestamp>:
       - If the timestamp is in the past → the lock has expired.
         Proceed to acquire (see "Expired locks" below first).
       - If the timestamp is in the future and the holder is not you →
         SKIP this item. Pick another. Never steal a live lock.
       - If the timestamp is in the future and the holder is you →
         you already have it. Proceed to work.
4. To acquire: set Lock: <your-id>@<now + TTL>. Optionally also flip the
   Status field to in-progress in the same edit. Commit. Push.
5. Pull again immediately after pushing. If the push raced with someone
   else's acquire and the file conflicts, that other contributor wins
   (or you do — see "Race conditions" below).
```

### Why pull-before-decide

The lock state in your local checkout may be stale. If another contributor acquired the lock thirty seconds ago, your local file still shows it free. A `git pull` (or equivalent) before reading the field minimizes the race window.

The race cannot be fully eliminated without an external coordinator, but with disciplined pull-before-acquire and small commits, the window is small enough that races are rare in practice.

### Acquire-commit message template

```
chore(backlog): lock BL-### for <holder>

Lock acquired: BL-### -> Lock: <holder>@<timestamp>
```

The shape:

- `chore` type — locking is housekeeping, not a feature or fix.
- `(backlog)` scope — disambiguates from other chore commits.
- Subject names the action and the item.
- Body restates the new lock value. Optional but useful for `git log -p` readers.

Keep the commit small: only the lock change. Combining the lock-acquire with substantive code changes makes the audit trail harder to follow.

### Pushing the acquire

Push the acquire commit immediately. The lock has no effect on other contributors until it is visible in the shared remote. A locally-committed but unpushed acquire is useless — another contributor can still acquire the same item without seeing yours.

### Race conditions

Two contributors may try to acquire the same item at the same time. The outcomes:

- **One push lands first.** The second contributor's push is rejected (non-fast-forward). They `git pull --rebase` (or merge), see the other contributor's lock now in place, and either abandon their acquire or stage it behind the first acquire.
- **Both push to different branches that later merge.** The merge produces a conflict in the `Lock:` field. Resolve in favor of the earlier-acquired lock (use commit timestamps if needed). Notify the loser.

Races are rare because each acquire is a small, fast commit; the window of vulnerability is seconds. Disciplined pull-before-acquire keeps the rate low enough that the merge-conflict path is the fallback, not the norm.

---

## The release protocol

When the work on a locked item is done (passed [Definition of Done](07_definition_of_done.md)), abandoned, or merged, release the lock:

```
1. Set Lock: — in the item's frontmatter.
2. Commit and push.
3. Best practice: include the release in the same PR that lands the work.
   This ensures the lock is released atomically with the work it covered.
```

### Release-commit message template

When the release is its own commit:

```
chore(backlog): release lock on BL-###

Lock released: BL-### -> Lock: —
```

When the release rides along with the PR that closes the item, the PR's merge commit captures the release naturally. Either path is fine; the rule is that the lock must end at `—` once the work is concluded.

### Forgetting to release

A common failure: the work is done, the PR is merged, but the `Lock:` field still shows the holder's timestamp. The lock will eventually expire on its own, but in the meantime no one knows whether the item is genuinely free.

Defenses:

- A pre-merge checklist that includes "lock released" as one of the items.
- A periodic sweep script that flags items with `Status: done` and `Lock:` not `—`. (Trivial to write; one grep.)
- Cultural: review checklists name the lock release explicitly.

### Abandoning an item mid-flight

If you decide not to continue the work — change of priorities, blocker discovered, scope misjudged:

1. If no work has been pushed: release the lock and revert the item's `Status` back to `ready` (or `blocked`, with a `Blocker:` line).
2. If partial work has been pushed: do the same. Add a `Notes:` line summarizing where the work got to and what's left. The next contributor can pick up cleanly.
3. Do not leave the lock in place. Holding a lock you do not intend to use blocks everyone else.

---

## When NOT to lock

Not every action requires a lock. Locks are for *exclusive work claims on an item.* They are overhead, and overhead applied to wrong cases adds friction without benefit.

### Do not lock for:

- **Read-only research and exploration.** Grep, browse, read files, understand context, write notes in your own scratch space. No lock needed. The item is not "in progress" — you're just investigating.
- **Mechanical moves between files.** Archiving a done item from `BACKLOG.md` to `ARCHIVE.md` is not a work claim. Anyone may do it as part of housekeeping.
- **Routine rollup updates.** Bumping `EPICS.md` counts after an archive is housekeeping. No lock.
- **Quick fixes that take less time than the lock-commit-push round-trip.** A typo in an item's description; renaming a field for clarity; fixing a broken cross-reference. These are seconds-long edits; the protocol overhead would exceed the work.
- **Filing a new item.** Creating a new entry in `BACKLOG.md` does not require locking the file. (The item starts with `Lock: —`.)

### Do lock for:

- **Picking up an item to work it.** Anytime you intend to set `Status: in-progress` and produce non-trivial code/content changes.
- **Long refactoring sessions across many items.** If you intend to touch multiple items as part of a single coordinated change, lock each one you're actively editing.
- **Anytime two contributors might collide.** When in doubt, lock — the protocol is light enough that over-locking is a smaller cost than collision.

---

## Expired locks

When a lock's timestamp is in the past, it is *expired* — the previous holder either finished without releasing, abandoned the work, or died mid-task.

Expired locks are free to acquire. But before acquiring, do one thing:

> **Investigate what partial work the previous holder may have left.**

The previous holder may have:

- Pushed a partial branch that contains useful starting work.
- Made local-only commits that never reached the remote (lost — but the lock at least tells you they intended to do something).
- Filed notes elsewhere about why they abandoned.

### How to investigate

- `git log -p -- <epic>/BACKLOG.md` — see the lock acquire commit and any other commits in the area. The acquire commit may be useful as a timestamp anchor.
- `git log --all --author=<holder>` — see other commits by the previous holder around the same time.
- Search the item ID across the repo and across PRs. There may be a stale branch named `feature/<item-slug>` containing the partial work.

If you find useful partial work, decide:

- **Continue from where they left off.** Reset the item to `in-progress`, lock to your ID, and pick up. Note in the body what you inherited.
- **Discard and restart.** Reset to `ready`, then re-acquire fresh. Sometimes the partial work isn't recoverable.

If you find nothing, just acquire cleanly.

---

## Holder ID format

The holder field identifies *who* holds the lock. The format:

```
<agent-or-user>-<short-session-id>
```

Examples:

- `claude-session-a4f2` — an AI agent's specific session.
- `alice-laptop` — Alice's primary workstation.
- `alice-mobile` — Alice's secondary device (so two of her sessions don't collide).
- `bob-ci` — Bob's automation that occasionally acquires locks.

### Rules

- **Stable per session.** Use the same ID for the duration of a session; refreshing the lock keeps the ID the same.
- **Different sessions get different IDs.** Even from the same human or agent. If two of your sessions try to share a lock, you've reduced the lock's protective value.
- **Identifiable.** A holder ID that doesn't say who or where is useless during incident triage. "anon-123" is bad; "alice-laptop" is fine.
- **No personal info beyond what's needed.** Names or screen-names, not full email addresses or other identifiers that don't belong in a git history.

### What if the same human has multiple agents acting on their behalf?

Give each agent its own holder ID. `claude-session-a4f2` and `claude-session-b193` are separate; both might be initiated by the same human, but each is a distinct lock-holder for protocol purposes. If they need to coordinate (e.g., the human is running two parallel agents on different items), the coordination happens above the lock layer.

---

## TTL recommendations

The TTL is the duration of the lock — how long from acquire until the lock expires unless refreshed.

| Holder type | Recommended TTL | Rationale |
|-------------|-----------------|-----------|
| AI agent session | 2 hours | Matches a typical session length. If the agent finishes faster, it releases. If it runs longer, it refreshes (which is one commit). |
| Human contributor — focused work | 4 hours | Comfortably covers a focused work block without forcing refreshes. |
| Human contributor — open-ended | 8 hours (one workday) | Covers a full day's intermittent attention on the item. |
| Automation (CI, scripted backfill) | 30 minutes | Automation is fast and crashes loud; short TTL bounds blast radius. |
| Coordinated multi-day work (rare) | Maximum 24 hours, refreshed | The TTL ceiling. Long work should be split or refreshed daily. |

### Picking a TTL

If unsure, default to 2 hours. It is small enough that a forgotten lock is forgiven quickly; it is long enough to cover a non-trivial unit of work.

### Refreshing

To refresh: commit a new `Lock:` value with a later timestamp. Same holder, later expiration. This signals "still working" to other contributors.

Refresh before the existing lock expires, not after. A lock that has already expired is — at that moment — anyone's to acquire; refreshing it after expiration races against any contributor who may already be trying to take it.

---

## Subagent delegation

A common pattern: an orchestrator agent picks up an item, holds the lock, and delegates specific subtasks to subagent sessions that do focused work. The subagent does not touch the lock; the orchestrator remains the lock-holder throughout.

### The pattern

```
Orchestrator agent:
  1. Acquires lock on BL-###.
  2. Plans the work; identifies independent subtasks.
  3. Spawns subagent(s) — e.g., one for research, one for testing,
     one for documentation.
  4. Subagent does its task; returns results to orchestrator.
  5. Orchestrator integrates results; produces the change.
  6. Orchestrator releases lock when work is complete.
```

### Why subagents don't touch the lock

- The lock represents an *exclusive work claim on an item.* Only one party holds it at a time. If subagents acquired sub-locks, the coordination would become a graph rather than a single field — too complex for a markdown backlog.
- The orchestrator is the accountable party. Subagents are tools the orchestrator uses; their work is the orchestrator's work.
- Subagents are typically short-lived (one task, one return) — they don't outlive the orchestrator's lock duration.

### When this pattern is useful

- **Parallel investigation:** spawn multiple research subagents in parallel; integrate their findings.
- **Specialization:** one subagent runs tests; another reviews code; another updates docs. Each focused.
- **Context isolation:** subagents have fresh context, useful for unbiased review or fresh-eyes verification.

### When NOT to use subagents

- **Trivial work** doesn't need delegation overhead.
- **Tightly-coupled steps** where each step depends on the previous one's full state — sequence in the orchestrator instead.
- **Work that mutates shared state** (writing files, making commits) — subagents that write to disk while the orchestrator is also writing can produce conflicts. Reserve writing to the orchestrator.

### Coordination

When the orchestrator spawns multiple subagents in parallel:

- Give each a clear, independent task. Avoid implicit ordering dependencies.
- Give each enough context to do its task without back-and-forth.
- Integrate results; don't trust them blindly (cross-check critical findings).
- Time-box: if a subagent runs longer than expected, assume it's stuck and proceed without it.

---

## Audit trail

Every lock change is a git commit. This makes the lock history fully auditable.

### Useful queries

- **Who has held this item, and when:**
  ```
  git log -p --follow -- backlog/epics/<NN>-<slug>/BACKLOG.md
  ```
  Filter to lines mentioning the item ID and you see every lock state change in order.
- **All locks held by a specific contributor:**
  ```
  git log --all --grep="lock .* for <holder>"
  ```
- **All currently locked items (a snapshot at HEAD):**
  ```
  rg "^\| Lock\s+\|" backlog/ | rg -v "Lock\s+\|\s+—"
  ```
- **Items whose locks are currently expired (lock is set but past now):**
  
  A short script: parse each `Lock:` line, compare timestamp to wall clock, list items where timestamp < now and value != `—`.

### Why audit trails matter

- Incident response: if a contributor reports collision, you can reconstruct what happened.
- Pattern detection: if one contributor consistently forgets to release locks, the data is there to surface and fix.
- Process iteration: if the TTL is consistently too short (locks expiring mid-work), the data shows it.

---

## A worked example of lock contention

This example walks through a realistic scenario with two AI agent sessions and one human. All times in UTC.

### Setup

- The item is `BL-0428 — Add CSV export to the activity report.`
- `BACKLOG.md` shows: `| Lock | — |`
- Three contributors are interested: `claude-session-a4f2`, `claude-session-b193`, and `alice-laptop`.

### Sequence

**14:00.** `claude-session-a4f2` pulls the repo. Reads BL-0428. Sees `Lock: —`. Decides to take it.

**14:00.** `claude-session-a4f2` commits:

```
chore(backlog): lock BL-0428 for claude-session-a4f2

Lock acquired: BL-0428 -> Lock: claude-session-a4f2@2026-04-18T16:00Z
```

(TTL = 2 hours; expiration is 16:00.) Pushes.

**14:02.** `claude-session-b193` pulls. Reads BL-0428. Sees `Lock: claude-session-a4f2@16:00Z`. Timestamp is in the future and the holder is not them. **Skips.** Picks a different item.

**14:30.** `alice-laptop` pulls. Reads BL-0428. Same conclusion: locked. **Skips.**

**15:50.** `claude-session-a4f2` is still working. The lock will expire at 16:00. They refresh:

```
chore(backlog): refresh lock on BL-0428

Lock refreshed: BL-0428 -> Lock: claude-session-a4f2@2026-04-18T18:00Z
```

Pushes.

**16:30.** `alice-laptop` pulls again. Reads BL-0428. Sees `Lock: claude-session-a4f2@18:00Z`. Still in the future. Still skips.

**17:15.** `claude-session-a4f2` finishes the work. Opens a PR. The PR's diff includes the lock release:

```
| Lock | — |
```

And the item's `Status` flips to `to-be-tested`.

**17:30.** PR is reviewed, tests pass, merged. Lock is now `—` on `master`.

**17:40.** `alice-laptop` pulls. Sees the lock is released. Item is `to-be-tested`. Alice picks up the UI verification step. Locks the item to herself:

```
chore(backlog): lock BL-0428 for alice-laptop

Lock acquired: BL-0428 -> Lock: alice-laptop@2026-04-18T21:40Z
```

Performs UI verification. Sets `Test: pass`. Flips `Status: done`. Releases the lock. Moves the item to `ARCHIVE.md`.

### What the audit trail shows

A `git log -p -- backlog/.../BACKLOG.md` filtered to BL-0428 lines, in order:

```
14:00  Lock: — -> claude-session-a4f2@16:00Z   (acquire)
15:50  ...@16:00Z -> ...@18:00Z                (refresh)
17:15  Lock: claude-session-a4f2@18:00Z -> —   (release; embedded in PR)
17:40  Lock: — -> alice-laptop@21:40Z          (acquire)
18:30  Lock: alice-laptop@21:40Z -> —          (release)
```

Every state change is recorded. Anyone reviewing the history can reconstruct what happened, when, and by whom.

### What would have gone wrong without locks

At 14:30, `alice-laptop` would have read BL-0428 with no lock indication and may have started parallel work. By the time both pushed their work, conflicts would have appeared. The waste: one of them did the work for nothing, and the merge took longer than the change itself.

---

## How locks connect to the rest of the methodology

- **Locks → Backlog items** ([04_backlog_items.md](04_backlog_items.md)). The `Lock:` field lives on the item's frontmatter table. Acquiring usually pairs with a `Status: in-progress` change in the same commit.
- **Locks → Definition of Done** ([07_definition_of_done.md](07_definition_of_done.md)). Gate 6 of the DoD includes "`Lock: —`" — a `done` item with a non-empty lock has not finished the DoD properly.
- **Locks → Git workflow** ([09_git_workflow.md](09_git_workflow.md)). Lock acquires and releases are commits on the active branch (often the feature branch for the item's work). They follow the project's commit conventions.
- **Locks → Working Principles** ([06_working_principles.md](06_working_principles.md)). Lock discipline is itself a "think before coding" practice — pulling, checking, and acquiring is the act of confirming you're not silently colliding.

---

## Common mistakes around locks

| Mistake | Fix |
|---------|-----|
| Acquire commit not pushed; you start working with only a local lock. | Push immediately after acquire. Local-only locks protect no one. |
| Pulled before acquire was skipped; you race another contributor. | Always pull, then read, then decide. The pull is the cheapest race-mitigation. |
| Stole a live lock because "they're probably done by now." | Never steal a live lock. Skip. If the lock genuinely seems abandoned, wait for expiration (or contact the holder out-of-band). |
| Lock left in place after work completed. | Release as part of the PR that lands the work. A periodic sweep script catches forgotten releases. |
| Same lock ID used across two sessions. | Use a unique session ID per session. Two of your sessions are not the same holder for protocol purposes. |
| TTL set to 24 hours by default. | Use the recommended TTL for the holder type. Long defaults waste recovery time when the holder dies. |
| Lock refresh forgotten; lock expires mid-work; another contributor takes the item. | Refresh proactively, before expiration. If you do lose the lock and another contributor takes the item, coordinate out-of-band; do not commit on top of theirs. |
| Acquire commit bundled with substantive code changes. | Keep the lock commit small. One acquire = one tiny commit. Substantive code goes in subsequent commits. |
| Lock holder ID is "anon" or empty. | Use an identifiable holder ID. Anonymous locks are unhelpful in incident triage. |
| Lock present on a `done` or `rejected` item. | Bug. Release immediately. Check whether the work actually finished or was abandoned. |

---

## Variants and adaptations

The lock mechanism described here is one point in a small design space. A project may adapt for its own needs:

- **Per-file lock granularity.** Some projects might lock at the file level rather than the item level. The same TTL principles apply. The same protocol applies, with `Lock:` at the top of each file rather than in an item frontmatter.
- **Optimistic concurrency only.** Smaller projects might skip explicit locking and rely on git's conflict-on-merge as the only signal. Acceptable when contributor counts are low and items are small.
- **External lock service.** Larger projects that have outgrown a markdown backlog might move to a tracker with native assignment fields. The TTL principle still applies (don't let assignments be open-ended).

The file-based lock with TTL is the recommended default because it has the lowest moving parts and works equally well for humans and AI agents.

---

## Authority

Locks bind work — no contributor may start `in-progress` work on an item without holding its lock. The lock outranks intent; "I was going to work this" is not the same as "I hold this lock."

Locks do not bind discussion, research, or design. Anyone may read, discuss, or sketch ideas about an item without acquiring its lock. The lock applies to *exclusive work claims that produce committed changes.*

A user (with explicit authority over the project) may override a lock — for example, releasing a clearly-stuck lock that an agent forgot to release, or breaking a lock during an incident. The override should be recorded as a commit with a clear message; the original holder is informed if reachable.

AI agents do not override locks. They follow the protocol exactly. If they observe what appears to be a wrongly-held lock, they surface the observation; they do not take action on it.

---

**Next:** [06 — Working principles](06_working_principles.md)
