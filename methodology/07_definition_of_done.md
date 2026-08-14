# 07 — Definition of Done

> **Purpose:** define the gates a work item must pass before its `Status` can be set to `done`. Prevents "done in name only" — items that look complete on a board but are buggy, untested, undocumented, or broken in the actual product.

The Definition of Done (DoD) is the hardest discipline in this methodology. Skipping it is the most common way the system fails. Read it carefully and apply it without negotiation.

---

## Why a strict DoD

Without an enforced DoD, items drift to `done` while still imperfect:

- A change passes unit tests but breaks the page when actually loaded.
- A feature is implemented but the changelog is never updated.
- A refactor passes the suite but breaks the dark theme.
- A bug fix lands but no regression test was added; six weeks later the bug returns.
- An item is marked `done` while its test status still reads `not-tested`.

Each of these creates downstream cost: the next contributor builds on a foundation they believe is solid and is not. The bug returns. The user finds the breakage. Trust in the backlog erodes.

The DoD prevents this by being a *hard barrier*. An item that has not passed every gate is not done. There is no partial credit. There is no "mostly done."

If a gate cannot be ticked, the item stays at `to-be-tested`, `under-review`, or `blocked`. It does not move to `done`.

---

## The six gates

Every item must pass all of these before its status flips to `done`.

### Gate 1 — Code review loop

Review every file you changed. Check for:

- Logic errors and off-by-one bugs.
- Type errors the compiler did not catch.
- Edge cases: empty inputs, null values, boundary conditions, error paths.
- Security: input validation, authorization checks, injection vectors.
- Adherence to the project's working principles (see [06_working_principles.md](06_working_principles.md)).
- Adherence to project-specific rules (see [08_lessons_and_memory.md](08_lessons_and_memory.md)).

If you find an issue, fix it. Then review again. Continue until you complete a full pass with zero issues found. **One clean pass is the bar, not "I think it's fine."**

This is a loop, not a single review.

#### Two ordered stages: spec, then quality

Run the review as two questions in order, not one blurred pass:

1. **Spec-compliance** — does the change actually satisfy the item's `**Done means:**` acceptance criteria (and nothing it shouldn't)? This is *findings-verification* — see [10_testing_and_verification.md "Two modes"](10_testing_and_verification.md#two-modes-findings-verification-and-diff-verification).
2. **Quality** — *given* that it meets the spec, is it well-made? The checks listed above: logic, edge cases, security, adherence to the principles.

Where possible, the two stages get **different eyes.** The author is the worst-placed reviewer for stage 1 — they will tend to confirm the interpretation they already built. A fresh session or a second contributor (a human, or a different model — see [cross-AI validation](10_testing_and_verification.md#cross-ai-validation)) catches "built the wrong thing, correctly," the failure a same-author quality pass sails straight past.

#### Routing findings by failure layer

The two stages order the *review*; this routes each *finding*. A defect enters the work at some layer — classify which one, and fix at that layer, not below it:

| Layer the defect entered | Finding looks like | Route |
|---|---|---|
| **Intent** — the approved goal itself is mistaken | "This does what the item says, and what the item says is wrong." | Halt. Back to the human who approved it — this is a [frozen-intent](04_backlog_items.md#frozen-intent--approved-goals-are-human-owned) renegotiation, not a code fix. |
| **Plan** — goal fine; the approach or [Code Map](04_backlog_items.md#the-code-map--writing-m-items-for-cold-handoff) led the code astray | "The code faithfully implements a wrong approach." | Fix the item body first, then re-derive the code from it. **Never patch code to compensate for a wrong plan** — the patch encodes the confusion permanently. |
| **Code** — goal and plan fine; implementation wrong | The ordinary bug. | Patch. This is the normal review-loop case. |
| **Out of scope** — real, but not this item | "While reviewing, I noticed X elsewhere." | File it — `FUTURE.md` or a new item per [scope-creep recovery](04_backlog_items.md#scope-creep-mid-task). Don't fix inline. |
| **Invalid** — the finding is wrong | A misread, a false positive. | Reject with a one-line reason (findings from [cross-AI validation](10_testing_and_verification.md#cross-ai-validation) are candidates, not ground truth). |

Process in that order — **an intent- or plan-level finding moots the code-level findings below it**, because the code will be re-derived anyway. Triage the layer first, then spend effort.

**The escape hatch:** if the same item bounces at the intent or plan layer more than twice, stop looping and surface it to the human — repeated upper-layer findings mean the item wasn't ready to work. This is the definition-side sibling of the [attempt cap](12_milestone_evaluation.md#the-attempt-cap-making-resists-multiple-attempts-executable): that cap bounds how many times you retry a *fix* that keeps failing; this bounds how many times you re-derive from a *definition* that keeps proving wrong. Both end the same way — a human picks a disposition per [handle / postpone / mark — never force](12_milestone_evaluation.md#unsolvable-issues-handle-postpone-or-mark--never-force), rather than the loop grinding on.

### Gate 2 — Automated tests pass

Run the project's full test suite locally. Not just the new tests. Not just the file you changed. The full suite.

- Every behavior change has at least one test that exercises the new behavior.
- Every bug fix has a regression test that fails on the broken code and passes after the fix.
- Tests test behavior, not implementation. A refactor should not require rewriting tests.
- The suite must pass cleanly. Skipped tests, expected failures, and flaky tests are not "passing."

#### The verification-gap question

Before ticking this gate, ask once per behavior the change adds or alters: **"if this behavior broke, would any test fail?"** The output is not a list of bugs — it is a list of *untested behavior changes*, each of which needs a test or a documented reason it can't have one. Two rules sharpen it:

- **A test counts only if it ran.** A test that exists but was skipped, filtered out, or never executed in the verifying run is a missing test — "the suite passed" speaks only for the tests that actually ran.
- **Never edit the expectation to match the code.** When a test fails, the fix is the code — or, if the *criterion* is wrong, a [frozen-intent renegotiation](04_backlog_items.md#frozen-intent--approved-goals-are-human-owned). Adjusting the assertion until it goes green is the [cheating-agent move](10_testing_and_verification.md#the-cheating-agent-anti-pattern) in its most compact form.

For details on testing approach, see [10_testing_and_verification.md](10_testing_and_verification.md).

### Gate 3 — Actual UI verification (the loop)

This is the gate that "tests pass" does not replace.

For any change visible in the user-facing product, perform end-to-end verification in the actual running application:

1. Start the dev server(s). For a multi-server stack, all relevant servers must be running. Check that the wiring is correct (frontend talks to backend, backend talks to database, etc.).
2. Open the app at the user-facing entry point. Not the raw API. Not a test harness. The real URL the user uses.
3. Navigate to every surface the change touches. Not just the headline screen — every page, modal, and state path the change can affect.
4. Execute the user flow end to end. Click the buttons. Submit the forms. Trigger the error states. Watch what happens.
5. Watch the browser console and network panel for errors. A 500 on a background fetch counts. A console warning about an unmounted component counts.
6. If you find an issue, fix it. Then return to step 3 — re-navigate, re-execute. Do not skip back to the failing screen and "spot fix." The fix may have broken something earlier in the flow.
7. Repeat until you complete a full pass with zero issues across every surface the change touches.

This is the most-skipped gate. It is also the most expensive to skip.

#### Required verification dimensions

Before the loop is complete, verify:

| Dimension | What to check |
|-----------|---------------|
| **Theme** | Both light and dark themes if the product supports both. Many changes break one and not the other. |
| **Viewport** | The product's primary target viewport FIRST (e.g., mobile-first products: verify at mobile width before desktop). Then secondary viewports. |
| **Auth state** | The relevant auth states for the change: logged-in, logged-out, gated, ungated. |
| **Empty state** | A user with no data — does the change still render and make sense? |
| **Error state** | When the API fails or the network is down, does the UI handle it? |
| **Offline state** | If the product supports offline use, does the change still work without network? |

Only the dimensions that *can* be affected by your change are required. A pure backend-tool change does not need viewport verification. But err on the side of checking — the cost of one extra check is small; the cost of shipping a broken state is large.

### Gate 4 — Documentation updated

If the change is user-facing or alters behavior an operator or developer needs to know about, update the relevant docs in the same change:

- **Changelog** — every behavior change gets an entry. Be specific about what changed and why someone would care.
- **Top-level README** — if commands, setup, or features the README mentions have changed.
- **Status / project-readiness doc** — if the change moves a feature from incomplete to complete.
- **Project instruction file** (e.g., `CLAUDE.md`) — if the change introduces a new convention, command, or hard rule that future contributors need to know.

Documentation is part of the change, not a follow-up. If you defer it, you are deferring the work that lets the next person understand what you did.

### Gate 5 — Final verification loop

After the per-gate work is done, do one more full pass:

1. Re-read the entire diff. Cold. As if you had not written it.
2. Re-run the test suite from a clean state.
3. Re-run the UI smoke test for the primary affected surface.

You are looking for: anything the per-gate work missed because of fatigue or tunnel vision. Late-stage bugs often hide in this pass — typos in copy, broken imports introduced by an unrelated fix, a regression test that was supposed to be added and was forgotten.

Zero issues at the end of this pass is the bar.

### Gate 6 — Backlog state correct

The item's metadata must match reality:

- `Status: done`
- `Test: pass` (never flip `Status: done` from any other Test value — see hard rule below)
- `Lock: —` (lock released)
- The item moved from the epic's `BACKLOG.md` to `ARCHIVE.md` (see [`04_backlog_items.md` "Lifecycle of an item"](04_backlog_items.md#lifecycle-of-an-item) for the archive mechanics).
- The epic's rollup count incremented (`done` count up by one, `open` count down by one — see [`03_epics.md` "Epic rollup (`EPICS.md`)"](03_epics.md#epic-rollup-epicsmd) for the rollup format).
- If the change closes additional items as a side effect, those items are also moved with the same care.

The backlog is a source of truth. If the file says `done` but the work is half-finished, the backlog has lied — and every future decision based on that state is poisoned. Update metadata accurately or do not flip the status.

---

## The hard rule

**`Status: done` requires `Test: pass`, `manual-verified` (with a regression-needed follow-up item), or `n/a` (with a body-documented reason).**

The canonical path is `pass`. The two narrow extensions exist to handle real-world cases automated testing can't cover honestly:

- **`manual-verified`** — verified by a human (UI walkthrough, manual reproduction) but no automated test exists. Acceptable when automation is impractical for the change AND a `regression-needed` follow-up item exists to backfill automation when feasible. Manual-verified without a follow-up is the cheating-agent anti-pattern.
- **`n/a`** — the item has no testable behavior (folder creation, README edit, repo-state chore). Acceptable with a body-documented reason; "I didn't feel like writing tests" is not a valid reason.

There is no path from `not-tested`, `pending`, `partial`, `fail: <detail>`, or `regression-needed` (without a backing `pass`) directly to `done`. The Test field must read `pass`, `manual-verified`, or `n/a` first. If it reads anything else, the item is not done — regardless of how close the work feels.

This is not bureaucracy. It is the single most important enforcement point in the methodology. Every other gate can be checked by good intent. This one requires the test to have actually run and actually passed (or the manual-verification + follow-up trail to exist, or the `n/a` reasoning to be documented). It is the gate that catches all the others when they slip.

See [`04_backlog_items.md "The hard rule"`](04_backlog_items.md#the-hard-rule) for the canonical statement of the rule and the Test enum.

If you cannot tick the Test field to `pass`, the item stays at:

- `to-be-tested` — code complete, awaiting verification.
- `under-review` — code awaiting review.
- `blocked` — cannot proceed; record why in a `Blocker:` body line.

Not `done`.

---

## "Servers up" is not proof

A clean `pnpm test`, a successful TypeScript compile, a green CI run, a dev server that started without errors — none of these prove the application works for the user.

What they prove:

- Tests pass: the tested behaviors work. Untested behaviors are not covered.
- Compile passes: the types are consistent. Runtime behavior is not verified.
- CI green: the tested behaviors work in the CI environment. Differences between CI and the actual app environment are not caught.
- Server started: the process runs. The user-facing experience is not verified.

What they do not prove:

- The page renders.
- The styles loaded.
- The feature is reachable from the navigation.
- The migration ran against the actual database the app uses.
- The auth gate lets the right users in.
- The change does not break a sibling feature.

The Actual UI Verification gate exists because of this gap. Tests are necessary; they are not sufficient.

---

## The loop pattern is the gate

"Run the test once. If it passes, ship." — wrong.

"Run the test. Fix any issues. Run again. Fix any issues. Run again until clean." — right.

The same applies to UI verification, to the review loop, and to the final verification loop. **A loop with a stopping condition is the gate. A single run is not.**

The stopping condition for every loop is the same: complete a full pass with zero issues. One clean pass after possibly many imperfect passes. Not "tests pass with one known flaky failure." Not "UI works except for that one thing I'll file separately." Zero.

If you find yourself excluding issues to claim a clean pass, the pass is not clean.

---

## Per-project DoD overlay

Different projects have different non-negotiables. The six gates above are the *base set* — the minimum any project needs.

Some projects need additional gates. Layer them on top of the base set; do not replace gates.

Common additions:

| Gate | When to add |
|------|-------------|
| **Schema migration applied** | Any project with a database where migrations are tracked separately. The change does not pass DoD until the migration runs cleanly against a representative dataset. |
| **Security scan run** | Any project with sensitive data, authentication, or payment flows. The change does not pass DoD until the project's security tooling clears the diff. |
| **Accessibility check** | Any user-facing product. The change does not pass DoD until a11y rules pass at the project's target level (e.g., WCAG 2.1 AA). |
| **Visual regression check** | Any project with a strict design system or pixel-level expectations. The change does not pass DoD until visual regression snapshots pass or are knowingly updated. |
| **Performance budget** | Any project where load time, bundle size, or query latency is a hard constraint. The change does not pass DoD until the budget is met. |
| **Type coverage threshold** | Any project enforcing typed coverage. The change does not pass DoD until coverage stays above the floor. |
| **Compliance review** | Any project under regulatory constraints (privacy, finance, healthcare). The change does not pass DoD until the relevant review signs off. |
| **Cross-browser smoke** | Any user-facing product targeting more than one browser engine. The change is verified in each target engine. |

The pattern is the same in every case: the additional gate has a binary pass/fail criterion, runs as part of the change (not after), and blocks `done` if it fails.

Document the project-specific additions in the project's instruction file so every contributor knows the full set.

---

## Maintaining living project documents

Beyond the per-item DoD gates, certain project documents are *living artifacts* that drift if not maintained. Each has its own maintenance trigger, cadence, and owner. Letting them drift turns the project's narrative into a lie — and trust in the artifacts erodes fast once that happens.

This section is the practical playbook for keeping them honest. It expands Gate 4 (documentation updated) with concrete patterns.

### The set of living documents

| Document | Lives at | What it answers | Update trigger |
|---|---|---|---|
| **Changelog** | `CHANGELOG.md` | What changed and when | Every behavior change or release |
| **README** | `README.md` | How to set up and run | When setup commands or top-level architecture change |
| **Project status / readiness** | `STATUS.md` or `docs/STATUS.md` | What's shipped, what's open | When a phase milestone moves |
| **Project instruction file** | `CLAUDE.md` / `AGENTS.md` | How contributors (human + AI) work here | When a hard rule or convention changes |
| **Epic rollup** | `backlog/EPICS.md` | Active epics + open/done counts | When any item changes state |
| **Backlog README** | `backlog/README.md` | Workflow and item-format conventions | When the workflow changes |
| **Strategy master plan** | `docs/strategy/00_master_plan.md` | Vision + phases + supporting-doc index | On re-evaluation (quarterly or trigger-driven) |
| **Memory index** | `memory/MEMORY.md` | The lessons-learned index | Same commit as the memory entry's add / remove / rename (per [`08_lessons_and_memory.md` "Index update discipline"](08_lessons_and_memory.md#index-update-discipline)) |

Each row is enforced by either the per-item DoD (CHANGELOG, README, STATUS, EPICS) or by its own re-evaluation protocol (strategy, memory).

### Changelog — the practical patterns

The changelog is the project's behavior diary. Most projects skip it, over-engineer it, or let it rot. The shape below is what works.

**One source of truth.** Exactly one `CHANGELOG.md` at the repo root. Not split across `docs/CHANGELOG.md`, the root, and per-package files. If you find duplicates, consolidate immediately and note the consolidation date at the top: *"Previously maintained in both root and `docs/CHANGELOG.md` — consolidated here on YYYY-MM-DD."*

**Reverse-chronological with an `[Unreleased]` section.** Newest at the top. `[Unreleased]` holds entries that have landed on the trunk but not yet been released (versioned + tagged). When you cut a release, rename `[Unreleased]` to the version number, then create a fresh `[Unreleased]` above it.

**Categorized entries.** Use a small fixed set of categories matching your commit conventions:

- `Feat` — new user-visible behavior.
- `Fix` — bug fix.
- `Chore` — tooling, dependencies, infrastructure (no user-visible change).
- `Refactor` — restructuring without behavior change (usually omitted; some projects include).
- `Release` — version bump entries.

**Entry header format:**

```
### <Category> — <short description> (<date> or <BL-###> or both)
```

Examples:

```
### Feat — Add CSV export to the activity report (BL-0428, 2026-05-22)
### Fix — Off-by-one in date parser overflow (BL-0517, 2026-05-21)
### Chore — Upgrade typescript to 5.4 (2026-05-20)
### Release — v0.8.0: versioning regime starts here (2026-05-17)
```

**Entry body** — detailed paragraphs. *What* changed, *why*, *where* (with file links), *what's out of scope* on this commit, and *verification notes* (especially when verification went beyond the test suite). Bullet lists are welcome. The entry should be readable cold by someone who didn't write it.

**Link to source files.** Use markdown links to the actual changed files. `[apps/api/src/routes/auth.ts](apps/api/src/routes/auth.ts)` rewards readers who want to dig in.

**Tie to backlog items.** Reference `BL-###` in the header or body. The changelog and the backlog stay cross-linked.

**Don't over-summarize.** A changelog entry that says "Various fixes" is useless. An entry that names what was wrong and how it was fixed teaches future contributors (including future-you).

**Update timing** — in the same PR as the change. DoD Gate 4 enforces this. A PR that lands behavior without updating the changelog is incomplete.

### README — the practical patterns

The README is the front door. It rots faster than any other document because everyone reads it on day 1 and nobody re-reads it after.

**Must always be current:**

- Setup commands (install, dev, test, build). If these are wrong, contributors hit walls before they start.
- Top-level repo structure tree. If the tree is wrong, contributors can't navigate.
- Quick-start ("hello world for this project"). One paragraph or one code block.
- Versioning regime. SemVer? Calendar versioning? Something else? Say so.

**Can be brief or external:**

- Detailed architecture (lives in `docs/`).
- Full API reference (lives in API docs).
- Long-form feature lists (rot quickly; let users discover via the product or its release notes).

**Update trigger** — any time the setup commands change, the repo structure changes, or a feature the README explicitly mentions is added or removed.

**Test the README literally.** Once a quarter, follow the README setup commands on a fresh clone and see if they actually work. They often don't. Fix.

### Project status / readiness doc

A short doc that answers "what state is this project in right now?" Useful for stakeholders who don't read the changelog and for your future self.

Suggested sections:

- Current phase (per the strategy master plan).
- What's shipped (one paragraph).
- What's open (one paragraph + link to active epics).
- Known limitations / risks.
- Last updated date.

**Update trigger** — when a phase milestone moves or a major risk materializes / resolves. Monthly minimum.

### Project instruction file (CLAUDE.md / AGENTS.md)

See [08_lessons_and_memory.md](08_lessons_and_memory.md) for the full discipline. Maintenance triggers:

- A new hard rule is added.
- A convention changes (naming, file organization, test approach).
- A new common command or tool is introduced.
- An old rule is no longer relevant — delete it; the file is supposed to be compact.

**The "explained twice" rule.** Whenever you find yourself explaining the same project-specific rule to a contributor (human or AI) more than once, that's the signal to write it down in the instruction file.

### When all the docs disagree, the docs all lose

The biggest failure mode for living documents is *partial maintenance.* The CHANGELOG mentions a feature; the README still says "coming soon"; the STATUS says "in alpha"; the project instruction file describes the old auth flow. Three readers, four docs, four contradictory impressions, and nobody knows which one to trust.

Defense:

- **Update all relevant docs in the same PR.** Gate 4 of the DoD requires this. A PR that updates one doc but contradicts another is incomplete.
- **One source of truth per topic.** Don't repeat the same fact in multiple docs — link instead. Two copies will always drift; one copy + N links won't.
- **Periodic doc audits.** Quarterly, do a pass: read every living document and ask "is this still true?" Fix what isn't. This is itself a backlog item with effort `S`. **The quarterly pass covers the *project's* living docs (CHANGELOG, README, STATUS, instruction files, backlog).** The *methodology* docs themselves are out of scope for the quarterly pass — they get the deeper semi-annual evaluation described in "Methodology self-evaluation (semi-annual)" below.

### Periodic repo health audits (quarterly)

Beyond doc audits, a quarterly *repo health audit* catches imbalances and decay that no individual change reveals. File it as a recurring backlog item with effort `S`–`M`:

- **Lines of code by area.** Run a LOC counter grouped by directory (frontend / backend / scripts / docs / tests). Compare to last quarter. A 5x growth in one area without corresponding growth in tests is a signal.
- **Dead code scan.** Unused exports, unreferenced files, orphaned routes. Most projects accumulate these; nobody removes them unless a process forces it.
- **Dependency drift.** How many production dependencies are more than 6 months behind? More than 12? Any security advisories? Address before the gap becomes painful.
- **Test coverage trend.** Not the absolute number — the *trend.* Coverage dropping over multiple quarters is a leading indicator of test-skipping behavior.
- **Backlog health.** Items in `backlog` status for more than 6 months; items `blocked` with no recent activity; epics `active` for more than 12 weeks. All signals to triage.
- **Memory entry decay.** Entries referencing files that no longer exist; entries describing workarounds for bugs since fixed; clusters of 3+ related entries that should become methodology additions (see [08_lessons_and_memory.md](08_lessons_and_memory.md) "Memory as a leading indicator").
- **Lock hygiene.** Items marked `done` with non-empty `Lock:` fields (forgotten releases); expired locks that have been sitting for days.

A small scripted `repo-stats` utility that emits these numbers as a markdown summary is worth writing once. The methodology doesn't ship one — your stack determines the right implementation — but the *practice* of measuring is what matters.

### Methodology self-evaluation (semi-annual)

The audit above checks the *codebase*. A complementary practice checks the *methodology docs themselves* — do they still describe how the team actually works?

Methodology and practice naturally drift. The team learns shortcuts that aren't in the docs. New patterns emerge that the docs don't acknowledge. Old rules survive in the docs after their reason for existing has gone. Without a deliberate self-evaluation pass, the methodology becomes a fossil: technically correct as of when it was written, less and less descriptive of what's actually happening.

**Cadence:** semi-annual (every six months). More often is overhead; less often lets drift compound. The cadence is half that of the quarterly repo health audit because methodology docs change more slowly than code — and they *should* change slowly, since stability is part of their value.

**What to do:**

1. **Re-read every methodology doc cold.** Pretend you're a new contributor. Mark every rule that doesn't match what you've actually been doing.
2. **Classify each gap:**
   - **Practice is wrong** — the doc rule is sound; practice has drifted. Re-anchor: file a memory entry capturing the recurring gap, train the team, or strengthen the instruction file.
   - **Docs are wrong or incomplete** — the doc no longer matches reality. Update via the promotion loop (see [08_lessons_and_memory.md — The promotion path](08_lessons_and_memory.md#the-promotion-path-from-one-off-correction-to-durable-rule)). If the same gap appears as multiple memory entries already, the path is even shorter: it's a methodology addition waiting to be made.
   - **Both** — the rule was right at the time but context changed (new tooling, new model capabilities, new team composition). Rewrite for the new reality; note explicitly what changed.
3. **Ship the methodology updates as a release.** Same CHANGELOG entry shape as any other change. Tag the commit so future audits can find the lineage — e.g., `chore(methodology): semi-annual self-evaluation — close drift around <area>`.
4. **Note any rule the team consistently ignores.** A rule everyone routes around may not be the right rule. Investigate before reinforcing.

**The reverse case.** Sometimes a methodology doc gets *ahead* of practice — a section was written but the team hasn't yet needed it. That's fine; the methodology is aspirational on those edges. But if a year passes and the section was never needed, consider whether it should be pruned or marked as optional. Aspirational forever becomes clutter.

**What this is NOT:**

- **A rewrite.** Methodology stability matters; rewriting every six months trains the team not to trust the docs. Self-evaluation is about *closing gaps*, not about *redesigning*.
- **An audit of individual contributors.** The artifact under review is the docs, not the people.
- **A planning exercise.** The methodology describes *how* work is done; it doesn't decide *what* to do next.

**Connection to the existing patterns:**

- **[Memory as a leading indicator](08_lessons_and_memory.md#memory-as-a-leading-indicator-for-methodology-gaps)** is the *bottom-up* signal that the methodology has a gap. Self-evaluation is the *top-down* check that catches gaps memory hasn't flagged yet.
- **[The promotion path](08_lessons_and_memory.md#the-promotion-path-from-one-off-correction-to-durable-rule)** is the mechanism for landing the methodology changes self-evaluation surfaces. Self-evaluation is the trigger; the promotion path is the execution.
- **[Periodic repo health audits](#periodic-repo-health-audits-quarterly)** (above) and self-evaluation cover complementary surfaces: code health vs. doc health. Run both; they catch different things.

The healthy state: docs and practice inform each other continuously. Each self-evaluation pass moves the docs ~5% closer to current reality; the cumulative effect across years is what keeps the methodology alive instead of stale.

### A practical checklist (paste into your project's PR template)

```
- [ ] CHANGELOG.md updated (entry under [Unreleased] with category +
      date + BL ref + body).
- [ ] README.md updated if setup commands, repo structure, or top-
      level architecture changed.
- [ ] STATUS / project-readiness doc updated if a milestone moved or
      a known limitation changed.
- [ ] Project instruction file (CLAUDE.md / AGENTS.md) updated if a
      convention or hard rule was added.
- [ ] Memory index (MEMORY.md) updated if a memory entry was added.
- [ ] EPICS.md rollup counts updated if items changed state.
```

This checklist is the operational reality of Gate 4. If you can tick every relevant row for your change, you've met the documentation gate.

---

## DoD checklist (copy into your project's instruction file)

The short form. Paste into the project's contributor instructions verbatim.

```
Definition of Done (every item, no exceptions):

[ ] Code review loop: every changed file reviewed; logic/type/edge-case
    issues found and fixed; one clean pass at the end.
[ ] Automated tests pass: full suite run locally; new behavior covered;
    bug fixes include a regression test.
[ ] Actual UI verification: ran the change in the actual app, navigated
    every affected surface, fixed issues, looped until clean. Verified in
    both themes, primary viewport first.
[ ] Documentation updated: changelog, README, status doc, and project
    instruction file updated where relevant.
[ ] Final verification loop: one more clean pass of review + tests + UI
    after all per-gate work.
[ ] Backlog state correct: Status: done, Test: pass, Lock: —, item moved
    to ARCHIVE.md, epic rollup counts updated.

Hard rule: Status: done REQUIRES Test: pass. If you cannot tick Test: pass,
the item stays at to-be-tested or under-review. Never flip to done from
not-tested / fail: / regression-needed.

"Servers up" / "tests pass" is not proof. The UI gate is required.
```

---

## Extended DoD checklist (project-specific additions)

Append project-specific gates as needed. Template:

```
Project-specific gates (in addition to the base DoD):

[ ] Schema migration applied to local DB; smoke-tested an endpoint that
    uses the new column.
[ ] Security scan passes (<tool name>).
[ ] Accessibility check passes (WCAG 2.1 AA; <tool name>).
[ ] Performance budget met (<target>; <tool name>).
[ ] Compliance reviewer signed off (if change touches <regulated area>).
```

The list should be short and concrete. Each gate names *what* must be checked and *how* to check it. Vague gates ("looks good") are not gates.

---

## Common DoD failures and how they show up

| Failure mode | What it looks like | What was skipped |
|--------------|--------------------|------------------|
| "All tests pass" but the page is white. | Item flipped to `done`. User reports a blank screen on the next deploy. | Gate 3 (UI verification). |
| Dark theme broken after a UI change. | Item is `done`; users on dark theme see unreadable text. | Gate 3 dimensions (theme). |
| Bug returns three weeks later. | Same item is filed again. | Gate 2 (regression test required for bug fixes). |
| Item is `done` but README still says "coming soon." | Doc drift; future contributors are confused about what's shipped. | Gate 4 (documentation). |
| Item is `done` with `Test: not-tested`. | Backlog claims complete; in reality untested. Trust in backlog erodes. | Gate 6 + hard rule. |
| Migration applied locally but not run against staging. | Endpoint 500s after deploy because the column is missing. | Project-specific overlay (schema migration applied to the right environment). |
| Reviewer asks "did you check X?" and the answer is no. | Item gets bounced back. Loop restarts. Time lost. | Gate 5 (final verification loop should catch this before review). |

Each row is a real failure pattern. Each one is fully prevented by following the gate it skipped.

---

## DoD is not negotiable per-item

Every contributor will, at some point, be tempted to skip a gate for "just this one item." A common pretext:

- "It's a tiny change."
- "I'm in a hurry."
- "I already tested it manually before refactoring; it's the same."
- "The CI will catch it."
- "It's just a doc change."

Resist the temptation. The DoD exists because every one of these has been wrong before. Tiny changes break things. Hurried work creates the most rework. Manual testing before refactoring does not cover post-refactor behavior. CI does not catch UI-only issues. "Just a doc change" can mislead users.

The DoD is the floor for every item. If a project wants to allow some items to skip some gates (e.g., trivial typo fixes), it can define that explicitly in its project-specific overlay — but the rule is named, not improvised.

---

## How DoD relates to other parts of the methodology

- **The constitution** ([00_README.md "The constitution check"](00_README.md#the-constitution-check)). The hard-rules set is re-confirmed at the DoD gate, not only at plan time — the DoD is where "did we hold every non-negotiable?" gets its final check before `done`.
- **Working Principles** ([06_working_principles.md](06_working_principles.md)) govern *how* you work. DoD governs *whether the work is finished.* Both required.
- **Backlog item lifecycle** ([04_backlog_items.md](04_backlog_items.md)) describes the path a single item takes. DoD is the final gate on that path.
- **Locking** ([05_locks_and_parallel_work.md](05_locks_and_parallel_work.md)) is released as part of Gate 6.
- **Testing and verification** ([10_testing_and_verification.md](10_testing_and_verification.md)) explains the *technique* used inside Gates 2 and 3 (the loops). The DoD says what must be done; the testing doc says how to do it.
- **Lessons and memory** ([08_lessons_and_memory.md](08_lessons_and_memory.md)) is where new recurring DoD-related lessons get captured. If a class of failure passes the base gates twice, add a project-specific gate or memory entry to catch it next time.
- **Git workflow** ([09_git_workflow.md](09_git_workflow.md)) — the PR is the artifact that demonstrates DoD compliance. The PR body should make it possible to verify the gates were passed.

---

## Authority

The DoD outranks deadlines. The DoD outranks "we'll fix it later." The DoD outranks "the user is waiting."

The DoD does not outrank explicit user direction. If a user, knowing the rules, explicitly says "ship this without UI verification because the dev environment is down and I need it on staging in the next hour," that overrides the gate — and the consequence (untested ship) is now the user's accepted risk, recorded in the item's notes.

Implicit pressure ("the user seems impatient") does not override the gate. The contributor's job is to follow the gate or surface that it cannot be followed, never to silently skip it.
