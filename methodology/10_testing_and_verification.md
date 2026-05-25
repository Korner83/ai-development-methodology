# 10 — Testing and verification

> **Purpose:** define the two-layer verification practice that backs the [Definition of Done's](07_definition_of_done.md) `Test: pass` requirement. Automated tests catch one kind of failure cheaply; actual-UI verification catches the rest. Both are required for user-observable changes.

This doc explains *how* to do testing and verification well. The DoD says it must be done; this doc says how.

---

## Why both layers

A change can pass an automated test suite and still be broken for the user. A change can also be visually verified and still regress under an unhappy code path. Each kind of test catches what the other misses.

### What automated tests catch

- Logic errors in the change's code path.
- Type errors and contract violations the compiler caught (or the type-aware test runner caught).
- Regression of *previously-tested* behaviors.
- Integration mismatches at module or service boundaries (when integration tests exist).

### What automated tests DO NOT catch

- Layout breakage and styling regressions.
- Theme issues (a change that looks fine in light theme and unreadable in dark theme).
- Mobile-vs-desktop differences.
- Broken navigation paths.
- Broken auth gating (the page renders but the wrong users can access it).
- Missing imports or runtime errors that only fire when the code actually executes in a browser/runtime context.
- Console warnings and errors a user would see in devtools.
- "Server started" not equaling "feature works."
- Accessibility issues a manual scan would catch.
- Visual quality issues — alignment, spacing, color, contrast.

The actual-UI verification layer exists because these are real failure modes that the test suite cannot reach. Tests are *necessary;* they are not *sufficient.*

### Why this split matters

Without the split:

- A contributor writes a change, runs `pnpm test`, sees green, marks the item `done`, and ships a broken UI.
- The user reports the breakage.
- The contributor is surprised: "but tests pass."
- The trust in the "Test: pass" field erodes — because it only proved one half.

With the split:

- Tests pass means the *tested behaviors* work.
- UI verification means the *user-visible behaviors* work.
- Both passing is the bar for `Test: pass`.

---

## Automated tests

### The principle

**Every behavior change has at least one test that exercises the new behavior.** Every bug fix has a regression test that fails on the broken code and passes after the fix.

### Test the behavior, not the implementation

A good test asks "does this function/route/page produce the right outcome for this input?" A bad test asks "does this function call its internal helper three times?"

The behavior test survives refactors. The implementation test breaks every time you rearrange internals — even when the behavior is unchanged. Implementation-coupled tests are noise.

A useful check: if you rewrote the implementation completely while preserving the externally-visible behavior, would the test still pass? If yes, it's testing behavior. If no, it's testing implementation.

### Run the full suite, not just the new tests

A change can pass *its own* new tests while breaking three pre-existing ones. Running only the new tests would miss the regression.

Run the full suite locally before marking the change ready for review. If the suite is slow, find ways to make it faster (parallelism, test selection by changed file, smarter mocking) — *don't* skip running it.

### Test framework agnostic

This doc does not prescribe a test framework. Pick what fits the stack:

- Unit tests for pure functions, classes, components in isolation.
- Integration tests for module-to-module behavior.
- End-to-end tests for full user-flow paths (these overlap with UI verification but are scripted).

The test types are not exclusive. A healthy codebase has all of them.

### Where tests live

Two common conventions:

- **Alongside the code:** `Foo.ts` and `Foo.test.ts` in the same directory. Easy to find, easy to keep in sync.
- **In a parallel test tree:** `src/Foo.ts` and `test/Foo.test.ts`. Useful when test infrastructure differs significantly from production code (e.g., requires different tooling).

Either is fine. Pick one and stay consistent across the project.

### Test naming

Tests should describe behavior in plain language:

```
describe('exportActivityReport', () => {
  it('returns CSV with the right columns for the given filter', ...)
  it('streams large result sets without buffering', ...)
  it('returns 400 when the date range is inverted', ...)
})
```

A reader looking at the test list should be able to tell what the function is supposed to do without reading the function.

### What tests should cover

For any non-trivial unit:

- **The happy path.** The normal input produces the normal output.
- **Edge cases.** Empty input, null, boundary values, very large input.
- **Error cases.** Invalid input is rejected gracefully (with the right error shape).
- **The contract.** Inputs and outputs match the documented or typed shape.

For a bug fix:

- A **regression test** that fails on the broken code and passes after the fix. This is non-negotiable — see "Regression tests" below.

---

## Actual-UI verification: the fix-test loop

This is the most important and most-skipped gate. Take it slowly the first few times; the discipline pays off.

### The loop, step by step

```
1. Start the dev server(s).
   - For a multi-server stack (e.g., frontend + backend + worker), ALL
     relevant servers must be running.
   - Check that the wiring is correct: frontend can reach backend,
     backend can reach the database, etc.

2. Open the app at the user-facing entry point.
   - Not the raw API port. Not the test harness. The real URL.

3. Navigate to every surface the change touches.
   - Not just the headline screen. Every page, modal, and state path
     the change can affect, directly or indirectly.

4. Execute the user flow end to end.
   - Click the buttons. Submit the forms. Trigger the error states.
   - Watch the result of each interaction.

5. Watch the browser console and network panel.
   - A 500 on a background fetch counts. A console warning about an
     unmounted component counts. A missing asset counts.

6. If you find an issue, fix it.
   - Then return to step 3 — re-navigate, re-execute.
   - DO NOT skip back to just the broken screen. Your fix may have
     broken something earlier in the flow.

7. Repeat until you complete a full pass with zero issues across every
   surface the change touches.
```

### Why "re-navigate, re-execute" matters

A fix at step 4 can introduce a regression at step 3. If you skip back to step 4 alone, you don't see it. The discipline is: when you find an issue and fix it, restart the verification from a point upstream of the fix.

For small fixes (a typo, a CSS tweak), this might mean re-navigating the affected screen. For larger fixes (a change to shared state, a route refactor), it means restarting from the beginning of the user flow.

### Required verification dimensions

Before declaring the verification complete, cover the dimensions below. Only those that *could* be affected by your change are required, but err on the side of checking — the cost of one extra check is small.

#### Theme

- **Light theme.** Verify all affected surfaces.
- **Dark theme.** Verify the same surfaces. Many changes that look fine in one theme are unreadable in the other.

Common theme failures:

- Color contrast: text in a brand color is readable on the light background but invisible on the dark.
- Theme-conditional CSS: a style references a variable that exists in one theme but not the other.
- Hard-coded colors: a hex value passes light but fails dark.

#### Viewport

- **Primary target FIRST.** If the product is mobile-first, verify at mobile width before desktop. The discipline is: verify the most common user state before the rare one.
- **Secondary viewports.** Desktop if the product is mobile-first; tablet/mobile if desktop-first.

Common viewport failures:

- Horizontal overflow on mobile: a wide table or unbroken string spills off-screen.
- Touch targets too small: a 24px button is fine on desktop and frustrating on mobile.
- Layout breaks at specific widths: works at 375px and 1024px, broken at 768px.
- Mobile-specific affordances (drawers, sheets, swipes) not tested.

#### Auth state

For each user role the product supports, verify the change in that role:

- **Logged out** (unauthenticated visitor).
- **Logged in** (authenticated user, possibly with a free or default tier).
- **Premium / paid tier** if applicable.
- **Admin / operator** if applicable.

Common auth failures:

- A change that works for logged-in users 500s for guests.
- A gated feature is accidentally accessible to unentitled users.
- An admin-only surface is accidentally visible to regular users.

#### Empty state

A user with no data:

- New user, no created content, no history.
- Search returns zero results.
- A list/feed/dashboard with no entries.

Common empty-state failures:

- The empty state is missing entirely; the page is blank.
- An error renders because the code assumes at least one element.
- The empty state's call-to-action is wrong (links to a page that doesn't apply).

#### Error state

What happens when the API fails, the network drops, the user input is invalid?

- API returns 500 — does the UI render a usable error?
- Network is offline — does the UI degrade gracefully or fail loudly?
- User submits invalid input — is the error message actionable?

Common error-state failures:

- The UI freezes silently (spinner forever).
- A cryptic error from a deep library leaks to the user.
- The recovery path is impossible (no way to retry, no back button).

#### Offline state

If the product is meant to work offline:

- Disable the network (devtools "Offline" mode or actually turn off Wi-Fi).
- Try the affected flows.
- Verify the offline experience is acceptable (cached data shown, useful messaging, no broken UI).

Skip this dimension only if the product genuinely does not support offline.

### What to do when verification fails

The discipline is: *fix what you find, then re-verify from upstream.*

Specifically:

1. **Note the issue.** Even if you can fix it immediately, note it — the pattern of issues found is itself useful information (you may be about to file a memory entry; see [08_lessons_and_memory.md](08_lessons_and_memory.md)).
2. **Fix the issue.** In the code, not in the verification loop.
3. **Re-verify from upstream.** Start from a point earlier in the flow than the fix.
4. **Repeat.**

The loop terminates when a full pass completes with zero new issues.

---

## Tools

Verification can be manual or automated. Both have a place.

### Manual verification

A human clicking through the app. Necessary for:

- Visual quality assessment.
- Interaction feel (does the click feel responsive?).
- First-time verification of a new feature.
- Edge cases hard to script.

The downside: manual verification is slow, expensive, and prone to fatigue. Use it for what only humans can do.

### Headless browser tools

Scripts that drive a browser to navigate and assert. Useful for:

- Regression coverage of important user flows.
- Smoke tests run on every commit.
- Verification that runs in CI without a human in the loop.

Common categories:

- **Playwright, Puppeteer, Cypress** — full-featured headless browser automation.
- **MCP-based browser controllers** — AI-driven browser navigation, useful when the verification is part of an AI agent's loop.
- **Visual-regression tools** — capture screenshots and compare to a baseline; flag pixel-level changes.

The choice is project-specific. Adopt what fits the stack and the team's tolerance for tooling.

### Preview tools

Built into some development environments: a tool that lets an AI agent or contributor inspect a running preview of the app — read DOM snapshots, click elements, capture screenshots — without a full browser automation framework.

When available, preview tools are the right path for AI agents doing UI verification. They are faster than full browser automation and tailored for the AI-driven verification loop.

### What to choose

| Situation | Suggested tool |
|-----------|----------------|
| Manual verification of a small change. | Click through manually. |
| Repeated verification of a critical user flow. | Scripted E2E test (Playwright et al.). |
| AI agent verifying its own UI change. | Preview tool / headless browser MCP if available; manual click-through if user is present. |
| Visual quality / pixel-level verification. | Visual regression tool, then human eye for actual assessment. |
| Accessibility check. | Dedicated tool (axe, Lighthouse, etc.) + manual keyboard navigation. |

---

## What "tests pass" does NOT prove

This is worth stating in detail because the failure mode is common.

A clean `npm test` (or equivalent), a successful compile, a green CI run, a dev server that started without errors — none of these prove the application works for the user.

What they prove:

- **Tests pass:** the *tested* behaviors work. Untested behaviors are not covered.
- **Compile passes:** the types are consistent. Runtime behavior is not verified.
- **CI green:** the tested behaviors work in the CI environment. Differences between CI and the actual app environment are not caught.
- **Server started:** the process runs. The user-facing experience is not verified.

What they do NOT prove:

- The page renders.
- The styles loaded correctly.
- The feature is reachable from the navigation.
- The migration ran against the actual database the app uses.
- The auth gate lets the right users in.
- The change does not break a sibling feature.
- The console is clean.
- The network panel is clean.
- The change works at the target viewport.

The Actual UI Verification loop exists because of this gap. Tests are necessary; they are not sufficient.

---

## Skipping verification

The UI verification loop is required for any user-observable change. It is *not* required for:

- **Pure refactors** with no behavior change. (But: a refactor with no behavior change still needs to pass the existing tests, and a quick smoke of affected surfaces is good practice.)
- **Doc-only edits.** README, comments, methodology docs, etc.
- **Tooling config** that doesn't affect the running app (CI config, lint config, formatter rules).
- **Tests-only changes.** Adding test coverage without changing tested behavior.
- **Internal-only changes** — internal types, internal naming, dead code removal — that have no path to user-observable effect.

If you skip verification, state that you skipped it in the PR description with the reason. The reviewer can challenge the skip if it looks wrong.

**Do not skip verification for "tiny" user-observable changes.** A one-line CSS change can break a layout. A "trivial" copy update can change the meaning of an error message. The size of the change is not the right criterion; whether the user can see the change is.

---

## Regression tests

When fixing a bug, write a test that reproduces the bug *first.*

### The discipline

```
1. Identify the failing behavior.
2. Write a test that asserts the correct behavior.
3. Run the test. It MUST FAIL on the broken code.
4. Implement the fix.
5. Run the test again. It MUST PASS.
6. Run the full suite. It MUST STILL PASS.
```

### Why "must fail" first

A test that passes on broken code does not actually test what you think it tests. It might be testing a different code path, asserting against the wrong value, or skipping silently.

The "must fail first" step proves the test is real. If the test passes on broken code, the test is wrong — find the discrepancy before continuing.

### Where the regression test lives

Alongside the existing tests for the affected code. The test name should reference the original symptom or the item:

```
it('does not throw when the trips array is empty (regression for BL-0517)', ...)
```

A future reader who breaks the same code will see the test fail and read the comment / item reference to understand what they broke.

### Why this matters

Bugs return when fixes are not pinned by regression tests. Six weeks after the fix, a different change touches the same area; if no test pinned the original behavior, the bug returns silently. Regression tests prevent this.

---

## Per-project additions

The base testing/verification practice covers what every project needs. Some projects need additional checks. Layer them on top, do not replace.

### Common additions

| Check | When to add | Tool category |
|-------|-------------|---------------|
| **Accessibility** | Any user-facing product. Catches contrast, keyboard navigation, screen-reader issues. | Lighthouse, axe-core, manual keyboard test. |
| **Performance budget** | Any product with hard latency or bundle-size constraints. | Lighthouse, custom bundle analyzers, load tests. |
| **Visual regression** | Any product with a strict design system or pixel-level expectations. | Percy, Chromatic, or local snapshot diffs. |
| **Security scan** | Any product handling sensitive data, auth, or payments. | OWASP ZAP, Snyk, project-specific scanners. |
| **Cross-browser smoke** | Any product targeting more than one browser engine. | Playwright with multiple browser configs. |
| **API contract tests** | Any product with public or internal API consumers depending on stable contracts. | Pact, JSON-schema based tooling, OpenAPI lint. |
| **Type coverage threshold** | Any project enforcing typed code with a coverage floor. | TypeScript strict mode, tsc --noUnusedLocals, etc. |
| **Snapshot diffs of derived artifacts** | Any project that generates files (PDFs, reports, configs) where the output should be stable. | Project-specific. |

### How to layer on

For each addition:

1. **Name the check** in the project instruction file and the [DoD overlay](07_definition_of_done.md).
2. **Make it cheap to run locally.** A check that only runs in CI gets discovered after PR open, which is the wrong time.
3. **Make the failure clear.** A failing accessibility check should produce an actionable report ("Heading levels skip from H1 to H3 on the report page"), not a hash mismatch.
4. **Decide the bar.** "Must pass" (hard gate) versus "must not regress" (soft gate, fails on worsening).

---

## Verification checklist (paste into each PR's test plan)

The short form. Adapt by removing dimensions that genuinely don't apply.

```markdown
## Test plan

- [ ] Full automated test suite passes locally.
- [ ] New behavior covered by at least one test.
- [ ] If a bug fix: regression test added and verified to fail on the
      broken code.
- [ ] Manually verified the change in the running app:
  - [ ] Affected screens navigated end to end.
  - [ ] Console clean (no errors, no concerning warnings).
  - [ ] Network panel clean (no unexpected 4xx/5xx).
- [ ] Theme verified:
  - [ ] Light.
  - [ ] Dark.
- [ ] Viewport verified:
  - [ ] Primary target (<viewport>).
  - [ ] Secondary target (<viewport>).
- [ ] Auth states verified (as applicable):
  - [ ] Logged out.
  - [ ] Logged in (free / default tier).
  - [ ] Premium / paid tier.
  - [ ] Admin / operator.
- [ ] Empty state verified.
- [ ] Error state verified (API failure path).
- [ ] Offline state verified (if applicable).
- [ ] Documentation updated:
  - [ ] CHANGELOG.
  - [ ] README (if commands or setup changed).
  - [ ] Status / project-readiness doc (if scope shifted).
  - [ ] Project instruction file (if a new convention/rule landed).
- [ ] Backlog state correct:
  - [ ] Status: done.
  - [ ] Test: pass.
  - [ ] Lock: —.
  - [ ] Item moved to ARCHIVE.md.
  - [ ] EPICS.md rollup counts updated.
```

---

## Fix-test loop flow

A pseudocode view of the loop. Useful as a mental model for both human and AI agent contributors.

```
function verify(change):
  surfaces = identify_affected_surfaces(change)
  dimensions = required_dimensions(change)
  
  loop:
    issues = []
    
    for surface in surfaces:
      for dimension in dimensions:
        result = check(surface, dimension)
        if result.failed:
          issues.append(result)
    
    if issues is empty:
      return PASS
    
    for issue in issues:
      fix = implement_fix(issue)
      apply(fix)
    
    # Loop again. The fix may have broken something upstream.
    # Do not narrow the verification scope on subsequent passes —
    # re-verify all surfaces and dimensions.
```

Key properties:

- The loop terminates only when *one full pass* has zero issues.
- Each iteration of the loop checks *all* surfaces and dimensions, not just the ones where issues were found previously.
- The loop is the gate. A single pass with zero issues is not enough if it was preceded by no checking — the fix might be undocumented or untested.

---

## The "cheating agent" anti-pattern

When an AI agent writes both the implementation AND the tests for the same change, a failure mode appears: the AI may write a test that validates the *broken* code it wrote. The test passes; the code is wrong; the loop is self-consistent. No human in the loop catches it because the green test suite looks like done.

This is the AI-coding equivalent of marking your own homework.

### Defenses

- **Write tests first, ideally by a human.** When the test exists and fails before the implementation, the AI cannot tune the test to match its eventual (wrong) implementation. Test-first / TDD applied as an AI-collaboration discipline.
- **Cross-AI validate the tests.** Have a different AI (or the same model in a different session with no prior context) review the test suite for: *does this test actually exercise the intended behavior? Could a broken implementation slip through?* See "Cross-AI validation" below for the broader practice.
- **Human review of test names and acceptance criteria.** Even if the AI writes the test body, the test *name* and the acceptance criteria it asserts should come from human intent. "Test does the right thing" is the gap; "test asserts that X happens when Y" is the fix.
- **Audit a sample of AI-written test/implementation pairs periodically.** Pick a random sample and read both halves cold. If the test looks suspiciously specific to one implementation choice, dig deeper.

### The deeper implication

The test suite is the durable artifact — when it accurately captures intent, it can survive a language rewrite or framework migration. Implementation is replaceable; the test suite (assuming it tests behavior, not implementation) is not. That makes test quality MORE important in an AI-assisted workflow, not less.

See [11_human_roles.md](11_human_roles.md) "The cheating agent" for the human-role framing and "Specification as the primary artifact" for the related shift in what the team should be best at producing.

---

## Cross-AI validation

A separate AI system, periodically, audits the work that the implementing AI did. The audit catches blind spots the implementer missed — pattern-recognition gaps, security oversights, performance regressions, accessibility issues.

### Why "cross-AI"

AI models have characteristic blind spots:

- An AI that wrote the code may struggle to find its own bugs (same biases that produced the bug obscure it).
- An AI may consistently miss certain failure modes (race conditions, OWASP categories, accessibility patterns) that a different model catches reliably.
- A model trained on different data may notice patterns the implementing model doesn't.

Cross-AI validation is *not* a substitute for code review by a human or for actual user testing. It is a cheap "fresh eyes" pass that catches what would otherwise reach review or production.

### What to validate cross-AI

- **Performance:** is there a clear regression? Any obviously slow paths? N+1 queries?
- **Logic:** are there missed edge cases the original didn't cover?
- **Security:** OWASP categories — injection, broken auth, sensitive data exposure, etc. Pen-test mindset.
- **Accessibility:** WCAG-style checks the original didn't run.
- **Architecture:** is the change consistent with the codebase's existing patterns?
- **Test coverage:** are there behaviors the test suite doesn't exercise?

### Cadence

- For each meaningful change: a quick cross-AI pass before merging is cheap and worthwhile.
- Weekly or per-sprint: a deeper cross-AI audit of the codebase.
- Before any release: a full pass focused on regressions.

### How to set it up

- Use a different model (or a different vendor's model) from the one that implemented.
- Give the validator the diff, not the whole repo, if the diff is small.
- Ask for specific categories (performance, security, etc.) rather than "review this" — focused prompts produce focused findings.

### Limits

- Cross-AI validation will produce false positives. Treat findings as candidates for investigation, not as ground truth.
- Cross-AI validation cannot judge user experience. Only actual users can.

### Two modes: findings-verification and diff-verification

Cross-AI validation has two distinct modes, each appropriate at a different step:

**Findings-verification (the usual mode).** The implementing session produces work; the fresh session verifies the work meets a checklist (e.g., "this BL-#### item's Done-means are all satisfied," or "this PR's described changes match what the diff actually does"). The validator is checking *completeness and correctness of claims.* Output: PASS / FAIL per checklist item, with grounded citations.

**Diff-verification (when a loop or agent proposes an autonomous patch to authoritative content).** The implementing session produces a *proposed patch* — typically a branch with an edit, a CHANGELOG entry, and a finding the patch addresses. The fresh session reads the original cited content, the proposed edit, and the finding, then verifies three things:

1. **Grounded:** does the cited content actually have the problem the finding describes?
2. **Correct:** does the proposed edit actually fix the cited problem without introducing a new one?
3. **Scoped:** does the edit touch *only* the cited content (no scope creep into adjacent text)?

Diff-verification is the cross-AI gate for the patch-branch convention in [`09_git_workflow.md` "Patch-branch convention for authoritative artifacts"](09_git_workflow.md#patch-branch-convention-for-authoritative-artifacts). Without it, an autonomous loop's "I fixed the typo" claim is unverified. With it, the maintainer can review the cross-AI's PASS/FAIL on grounded/correct/scoped before reviewing the diff themselves — the maintainer's role becomes ratification, not original review.

Both modes use the same "fresh session, different model where possible" setup. The difference is the input shape (a checklist vs. an original + proposed-edit + finding triple) and the output shape (PASS/FAIL per checklist item vs. PASS/FAIL on grounded/correct/scoped).

---

## Verification levels: matching depth to risk

The previous sections describe *what* each layer of verification does. This section is about *which layers a given change requires.* `Test: pass` is binary in the [DoD](07_definition_of_done.md), but the work to earn it should match the change's risk profile. Verifying a typo fix with cross-AI validation is theatre; verifying a payment-flow refactor with only unit tests is negligence.

### The levels

| Level | Name | What it covers | Time cost |
|---|---|---|---|
| **L0** | Type / compile | Static type check; build passes; no syntax or import errors. | Seconds |
| **L1** | Automated tests | Full automated suite passes locally — unit, integration, contract tests. | Seconds to minutes |
| **L2** | Actual-UI fix-test loop | The fix-test loop above, with required dimensions (theme, viewport, auth, empty, error, offline). | Minutes to an hour |
| **L3** | Cross-AI validation | A separate AI audits the diff for performance, security, accessibility, missed edge cases. | Minutes |
| **L4** | User testing | A real user (or representative) tries the change and accepts it. | Hours to days |

Levels are cumulative — L3 assumes L0–L2 have been done. Skipping a lower level to "save time" usually costs more time when a defect surfaces later.

### Which levels a change requires

A pragmatic mapping — adjust for your project's risk tolerance:

| Change class | Required | Optional |
|---|---|---|
| **Typo, comment, doc edit** | L0 | — |
| **Pure refactor, behavior unchanged** | L0, L1 | L2 (smoke check of affected surfaces) |
| **Internal-only change** (no user-observable effect) | L0, L1 | L3 if architecturally significant |
| **User-facing fix or small feature** | L0, L1, L2 | L3 if non-trivial |
| **New feature** | L0, L1, L2, L4 | L3 |
| **Schema migration / breaking API change** | L0, L1, L2, L3, L4 | — |
| **Security-sensitive change** (auth, authz, payment, PII) | L0, L1, L2, L3, L4 | — |
| **Performance-critical change** | L0, L1, L2 + perf measurement | L3, L4 |
| **Production incident hotfix** | L0, L1, L2 minimum (verified on staging) | L3 deferred to follow-up |

These are not absolute. A trivial typo in a security-critical place still warrants L2. A feature behind a flag with no users may not need L4. Use judgment; document the choice.

### Recording the level

The item's `Test:` field can carry the level reached:

```
Test: pass (L2)             — actual-UI verified, no cross-AI, no user
Test: pass (L3)             — cross-AI validated, awaiting user gate
Test: pass (L4)             — user-accepted
Test: pass                  — assumed L2 minimum (default for user-observable)
Test: pass (L1, refactor)   — explicit lower bar with reason
```

The level annotation is optional but useful for risk-tracking. A PR that ships a security-sensitive change at L2 is a red flag the reviewer can catch.

### Why graduate the gate

Without graduation:

- **Over-verification.** Trivial changes drag through the full loop, slowing the team and training contributors to skip steps that "weren't really needed."
- **Under-verification.** Risky changes get the same L1–L2 treatment as routine work because nothing in the process flagged them as different.
- **Implicit shortcuts.** Contributors silently skip levels they think don't matter; reviewers can't tell what was actually done.

Naming the levels makes the choice explicit. When a contributor says "L3 wasn't required for this class of change," the reviewer can challenge the classification rather than re-derive what was checked.

### How this interacts with the DoD

The Definition of Done's hard rule remains: `Status: done` requires `Test: pass`. The taxonomy doesn't soften it — it clarifies *what `pass` means* for the specific change. A change requiring L3 cannot be marked `Test: pass` after only L2.

The DoD overlay for the project should name which change classes require which minimum level.

---

## User testing is the final gate

No matter how thorough the automated tests, the UI verification loop, or the cross-AI validation — **a real user trying the feature is the only test that produces the truth.**

### Why

- Automated tests cover what was anticipated. Users find what wasn't.
- AI validation finds patterns it was trained to find. Users find what's specific to their context.
- A passing test suite is a *necessary* condition for ship; it is not a *sufficient* condition.

### What user testing catches that nothing else does

- The feature doesn't match the mental model the user actually has.
- The flow is technically correct but unusable in practice (too many steps, unclear copy, etc.).
- The empty state, the error state, or the offline state surprises real users in ways the spec didn't predict.
- Performance is "fine" in synthetic tests and "painfully slow" on the user's actual device or network.
- The feature works for the developer's account configuration but breaks for users with different permissions, locales, or data shapes.

### Cadence

- For internal-facing features: a teammate's hands on the feature before ship.
- For external-facing features: at least one outside-the-team person before broad release; a small canary cohort before full rollout.
- For high-impact features: a structured user test (script, observed sessions, recorded feedback).

### The order of operations

```
Automated tests → UI verification loop → Cross-AI validation → User testing → Ship
```

Each gate is cheaper to run than the next. Each one catches what the previous doesn't. Skipping the last one is the most common methodology violation; it's also the most expensive when it bites.

### A practical rule

When the user accepts a feature ("yes, this works"), the loop terminates. Until then, you are still iterating. "I ran the tests and they pass" is not user acceptance; only the user can give that.

---

## How testing and verification connect to the rest of the methodology

- **Testing → Definition of Done** ([07_definition_of_done.md](07_definition_of_done.md)). The DoD names the gates; this doc explains how to execute them. The `Test: pass` value on an item requires both the automated suite and the UI verification loop to have passed.
- **Testing → Backlog items** ([04_backlog_items.md](04_backlog_items.md)). The `Test:` field on the item reflects the verification status. `not-tested` is the default; `pass` requires the full loop; `fail: <detail>` records what specifically failed.
- **Testing → Working Principles** ([06_working_principles.md](06_working_principles.md)). The goal-driven principle (Principle 4) is operationalized here: "fix the bug" becomes "write a test that reproduces it, then make it pass." The verification loop is the test that determines whether the goal is met.
- **Testing → Git workflow** ([09_git_workflow.md](09_git_workflow.md)). PR test plans are the artifact that records the verification was performed. A PR without a test plan cannot be merged under this methodology.
- **Testing → Memory** ([08_lessons_and_memory.md](08_lessons_and_memory.md)). A class of verification failures (a category of UI regression, a flaky test pattern) often becomes a memory entry, so the next contributor avoids it.

---

## Common mistakes around testing and verification

| Mistake | Fix |
|---------|-----|
| Ran only the new tests, not the full suite. | Run the full suite. A change can pass its own tests and break others. |
| Test asserts implementation details, breaks on every refactor. | Rewrite to assert behavior — input/output, not internal calls. |
| Bug fix shipped without a regression test. | Add the regression test. The bug will return otherwise. |
| Regression test passes on the broken code (i.e., didn't actually reproduce the bug). | Test is wrong. Re-run on broken code to verify it fails; fix until it does. |
| Single UI pass declared "verified." | The single-pass approach is not the loop. Iterate fix-and-verify until a full pass is clean. |
| Verified only on desktop; product is mobile-first. | Verify primary viewport first. Mobile-first products: mobile before desktop. |
| Verified only in light theme. | Verify both themes. Many regressions appear in only one. |
| Skipped UI verification because "the change is small." | Size is not the criterion; observability is. Small changes break things. |
| "Tests pass" claimed as proof for a user-observable change. | Not sufficient. UI verification is required. Tests cover what tests cover. |
| Verification dimensions check-listed in the PR but never actually run. | The checklist is a memory aid, not a substitute. The checks must be performed. |
| Headless browser ran the checks but a real human never looked. | Automated checks miss visual quality issues. A human glance is part of the loop for visible changes. |
| Empty state never tested; page crashes for a new user. | Empty state is its own dimension; verify it. |
| Error state never tested; user gets a stack trace on a transient API failure. | Error state is its own dimension; verify the recovery path. |
| Console errors ignored because "they were there before." | Triage them. Pre-existing console errors are technical debt; new ones are regressions. Don't conflate. |

---

## Authority

Testing and verification rules outrank speed. They do not outrank explicit user direction, but they do outrank "we'll add the test later" and "it's fine, I checked it once." The lesson "checked it once" produces silently broken changes is too widespread to allow exceptions.

The user can explicitly accept an unverified ship (e.g., "I need this on staging in 30 minutes for a demo; ship without full verification") — and that risk is then theirs, recorded in the item.

What the contributor never does on their own:

- Skip UI verification for a user-observable change.
- Declare `Test: pass` without running the loop.
- Add a feature without at least one test.
- Fix a bug without a regression test.

These rules bind humans and AI agents identically. Their purpose is not bureaucratic; it is to prevent the failure modes that have happened before.

---

**Next:** [00 — README](00_README.md)
