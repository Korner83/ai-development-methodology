# Software squads — assurance and accountability in practice

**Illustrative v1.35.0 walkthroughs, not adoption evidence.** Names, assignments, paths, and results below are fictional. Snippets show selected sections of an adopting repository, not another complete project tree. No product tests or specialist sign-offs described here have actually run.

Read the canonical [assurance profiles](../methodology/07_definition_of_done.md#assurance-profiles--consequences-determine-the-required-evidence), [human responsibilities](../methodology/11_human_roles.md#authorship-verification-and-acceptance), and [conditional item fields](../methodology/04_backlog_items.md#assurance-and-accountable-owner) for the rules.

## 1. Solo contributor: a reversible UX improvement

An internal scheduling tool has one human contributor, Alex, pairing with an AI author. The project instruction file records **A1** and **Accountable human: Alex**. Its epic assigns customer intent, product/UX, technical delivery, verification coordination, and acceptance to Alex; Alex also owns security assessment. No separate numerical item limits are needed for sequential work.

The item improves the empty schedule screen so a user can find the first action. It inherits A1 and Alex without adding metadata rows. Its acceptance criteria describe the visible action, keyboard access, and expected empty/error states. Applicable automated tests and actual-product verification still apply; if the change class requires user testing, Alex performs it rather than substituting an AI opinion.

Alex may author and verify this A1 change where the existing gates permit it. Using AI to implement the UI does not make AI the acceptor or remove human decision requirements.

**Change of scope:** if the work exposes another user's private schedule or changes authorization, stop affected work and ask Alex to resolve the higher risk. Add A2 fields and independent verification requirements before continuing. Alex can remain the author and acceptor, with a fresh AI session verifying criteria and reproducible evidence independently; Alex cannot call their own self-review independent verification.

## 2. Three-person squad: secure invitation links

The product lets customers invite coworkers. A UX contributor, technical contributor, and customer liaison work with AI authors. Job titles do not confer authority to change security policy or accept risk on someone else's behalf.

### Project and epic excerpt

```markdown
**Project assurance baseline:** A1
**Accountable human:** Morgan — product owner/customer liaison
**Implementation WIP:** 3
**Verification WIP:** 2

## Epic capability owners

| Capability | Current human owner |
|---|---|
| Customer intent/outcome | Morgan — customer liaison |
| Product/UX judgment | Taylor — UX contributor |
| Technical delivery | Casey — technical contributor |
| Verification coordination | Casey — arranges a verifier separate from the author |
| Accountable acceptance | Morgan — product owner |
| Security/compliance assessment | Casey — consults a qualified shared specialist when needed |
| Release operations | Casey — human operator |

**Epic assurance baseline:** A2 — invitation authorization and access boundaries
```

Taylor can author interaction behavior with AI assistance; Morgan can author customer acceptance criteria. Casey remains responsible for technical decisions assigned to that role. Morgan accepts the complete evidence package; Casey executes any production deployment as a human. The squad can draw on shared specialists without adding a mandatory permanent job title.

### Material item excerpt

```markdown
### BL-0012 — Reject expired and reused invitation links

| Field | Value |
|---|---|
| Epic | E02-invitations |
| Pillar | P2 |
| Priority | P1 |
| Effort | M |
| Status | to-be-tested |
| Test | partial — independent verification and human acceptance pending |
| Deps | — |
| Lock | — |
| Assurance | A2 — material, inherited from the epic |
| Accountable owner | Morgan — product owner |

**Why / Description:** Prevent expired or previously redeemed invitations
from granting access, including retries and concurrent redemption.

**Done means:**
- When an expired or redeemed invitation is submitted, access is denied.
- When two requests redeem one valid invitation concurrently, at most one succeeds.
- Required suite, UI/error-state checks, security checks, independent verification,
  human user testing, and Morgan's acceptance are recorded.

**Code Map:**
- `src/invitations/redeem.ts` owns redemption; reuse the repository's atomic
  consume operation rather than a read-then-write check.
- `src/invitations/InvitationPage.tsx` owns the expired/redeemed UI states.
- `tests/invitations/` covers expiry, replay, concurrency, and tenant boundaries.
- Rejected approach: checking expiry only in the browser allows direct API replay.
- The fresh verifier checks these claims against source before implementation.

**Verification procedure:** From a clean checkout, run `npm ci` using the
approved lockfile, `npm test`, and `npm run test:invitations` against the isolated
test database described in `docs/testing.md`; follow its invitation UI procedure
in staging. This example assumes those commands exist in that fictional repo.

**Review:** Fresh verifier session, separate from the author, checks the approved
criteria, source, and reproducible suite/security evidence. Record its identity,
reviewed commit, findings, and evidence under `docs/reviews/BL-0012.md`.

**Release arrangements:** `docs/runbooks/invitations.md` names Casey as operator,
describes disabling invitations and recovery, and defines failed-redemption and
unauthorized-access monitoring with alert routing. Morgan reviews these before
release acceptance; production execution remains Casey's human action.

**Acceptance:** Pending — Morgan; no residual-risk decision recorded yet.
```

The fictional filenames are illustrative, not evidence that a real codebase has those helpers. An adopting contributor must replace them with verified paths and commands. The `Test` value stays `partial` even if the technical checks are green. It may become `pass` only when all required verification and acceptance are complete, followed by the remaining DoD gates before `done`.

### Capacity walkthrough

With three items `in-progress`, nobody starts a fourth. With one `under-review` and one `to-be-tested`, the verification queue is at two; no new implementation starts even if an implementation slot is free. An already-running item may finish, temporarily taking verification to three; record the real count and drain it rather than hiding the third item.

If an invitation test fails, record the failure and prioritize rework. When an implementation slot becomes free, move that item back to `in-progress`; until then it remains in review/testing with the rework need visible. An author can prepare fixtures or clarify documentation but cannot become their own independent verifier to clear capacity. A queue waiting on Morgan's acceptance stays visible.

## 3. Boundary cases

| Situation | Required handling |
|---|---|
| Disposable mock-up | Explicit A0, a bounded learning question, non-production marking, applicable checks. A0 never waives DoD. |
| Mock-up becomes the delivered feature | Reassess its consequences and applicable evidence before reuse; exploratory completion is not release acceptance. |
| Regulated safety-critical software decision | A3; assign a human domain owner and a qualified human specialist independent of the author, with applicable compliance evidence. Morgan's acceptance and AI review alone are insufficient. |
| Required human owner is missing | Keep the item out of `ready`; obtain a real assignment. An AI author or an unfilled title cannot accept it. |
| Assigned specialist is unavailable | Keep completion blocked; record the human dependency. Do not substitute another model or downgrade A3 for convenience. |
| Models agree but relied on the author's summary | Independent-evidence requirement unmet; restart verification from approved criteria and repository evidence. |
| Human acceptance is unresolved | `partial`/`pending`, never `pass` with an "awaiting approval" suffix. |

## 4. Rotation and reusable assets

A replacement contributor receives the item link. They should be able to explain its purpose and constraints, locate the human owners, check the Code Map and rejected approach, and run the documented verification without consulting private chat. Missing instructions are a handoff defect. Only record a successful cold walkthrough after someone actually performs it.

If the invitation mechanism becomes a shared asset, a second use makes it a candidate pattern. A third meaningfully different use can validate its generality; three identical customer installations cannot. Productizing it additionally needs a named owner, versioning, compatibility policy, documentation, tests, and stated support expectations. Keeping it local remains valid when those costs outweigh demonstrated reuse.
