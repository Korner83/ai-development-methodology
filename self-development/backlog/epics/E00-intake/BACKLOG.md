# E00 — Intake — Active Backlog

_Real work that is not worth a charter. Same item format, same gates, no epic above it.
See the [charter](README.md) for what intake is and the eviction rule that empties it._

**Filed so far: 8. Closed: 3.** Three of the five came out of E10's convention sweep as decisions that were
recorded and then not executed — which is the same failure class as a claim asserted and not checked, and
is precisely the kind of work that had nowhere to live before this file existed.

## Summary

| ID | Title | Priority | Effort | Status |
|---------|------------------------------------------------------|----------|--------|-------------|
| BL-0058 | Read the Agent File spec; decide on a conformance line | P2 | S | ready |
| BL-0066 | Provenance for repo-supplied agent config that executes | P1 | S | backlog |
| BL-0067 | Tests that wait on work: no fixed sleeps | P2 | S | backlog |

---

### BL-0058 — Read the Agent File spec; decide on a conformance line

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E00-intake                         |
| Pillar   | P4                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | ready                              |
| Test     | not-tested                         |
| Deps     | —                                  |
| Lock     | —                                  |

> **Frozen intent** — `Why / Description:` and `Done means:` approved by maintainer on 2026-08-25.

**Why / Description:** A triage of `alvinreal/awesome-opensource-ai` on 2026-08-25 found the list is
overwhelmingly runtime infrastructure — inference engines, training frameworks, serving stacks — against a
methodology that governs *projects using* agents. Roughly nine tenths is not applicable, which is the same
result E09 got from `agent-engineer` and is itself the useful half of the answer.

**One entry is worth reading.** Agent File (`.af`) is an open format for serializing stateful agents with
persistent memory. Every other candidate solves state or coordination with a *running service*; Agent File
solves portability with a *file format* — the same wager this methodology makes, reached independently by
people building runtimes. **It is the only entry on that list that can validate or falsify the core
premise.**

The move is the BL-0034 shape, which worked: read the normative spec, compare field by field, and if the
models line up publish a **compatibility signal** — one sentence naming the format the handoff artifacts
resemble. A statement of fact, not a rule to learn. If they do not line up, that finding is worth the same
paragraph in `FUTURE.md`.

**Done means:**

- [ ] The normative spec is read before anything is written — not the awesome-list description.
- [ ] Its state model is compared field by field against `ACTIVE_CONTEXT.md` and `08`'s two-layer memory,
      and the comparison is recorded so it can be re-run rather than trusted.
- [ ] The outcome is one of: a single conformance sentence, or a recorded rejection with its reason.
- [ ] **No new convention is added either way.** This is a compatibility claim or nothing.

**Files (probable):** possibly `skills/ai-dev-methodology/SKILL.md` and `README.md`; possibly nothing.

**Notes:** The triage that produced this item ranked candidates from one-line descriptions and opened no
repositories. That is enough to pick; it is not enough to conclude. Runners-up recorded in
[FUTURE.md](FUTURE.md).

---

### BL-0066 — Provenance for repo-supplied agent config that executes

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E00-intake                         |
| Pillar   | P1                                 |
| Priority | P1                                 |
| Effort   | S                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | —                                  |
| Lock     | —                                  |

> **Needs clarification** — Does `13` take on a rule about repo files that *execute*, given its own scope
> line says it governs "which instructions an agent obeys" and leaves runtime isolation to the adopter?
> Yes means widening that line; no means this item closes as a recorded rejection.

**Why / Description:** `13`'s *trust follows provenance* rule covers instruction **text**: a modified
`AGENTS.md` on an untrusted branch is *believed* because of where it sits, so authority files are read from
the reviewed base commit. A read of `agent-of-empires/agent-of-empires` (at `c2bc548`, 2026-09-25) names the
next step that rule does not reach: once an agent harness trusts a workspace, the repo's own agent config
— `.claude/settings.json` hooks, `.mcp.json` servers, equivalent files in other tools — **runs**. Nothing
needs to be believed; it is *executed* because of where it sits, before the agent has read the diff.

AoE's answer has two parts, both tool-agnostic: a repo-committed config may not set anything that decides
**what launches or how much it may do** (default tool, env passthrough, privileged mode, permission-skip
mode), and trust is **keyed to the command content**, so any change to a hook re-prompts. The methodology
equivalent is small: checking out an untrusted branch is not safe in a harness that auto-runs repo hooks or
MCP servers, and changes to those files in a diff are treated like changes to the instruction file.

**Done means:**

- [ ] The clarification above is answered by the maintainer before any text is written.
- [ ] If yes: `13` states the rule once, next to *trust follows provenance*, and its threat-model table
      gains one row for repo-supplied executable agent config; the scope line is amended to match.
- [ ] If yes: the surface map in `00` ("Untrusted content and provenance") is walked — the pasteable block,
      both templates and the SKILL either reproduce the addition in full or carry none of it and link.
- [ ] Root `AGENTS.md` stays within its 60-line budget ([`RELEASE_EVIDENCE.md`](../../../RELEASE_EVIDENCE.md));
      it is at 56, so a block change that adds more than four lines needs a trade named in the PR.
- [ ] If no: the rejection and its reason are recorded here, so the next landscape pass does not re-file it.

**Files (probable):** `methodology/13_ai_safety_and_prompt_injection.md`; the surfaces listed in `00`'s map
for that row; root `AGENTS.md` if the pasteable block changes.

**Notes:** Source docs read: AoE `docs/guides/repo-config.md` (hook trust, the repo-may-not-set table) and
`docs/guides/sandbox.md` ("Folder trust"). Separately, AoE's README carries a line addressed to AI agents
asking them to star the project — benign, but a live example of an embedded directive asking for a public
action on the user's account in a widely read repo. It was surfaced, not acted on, and would serve as a
concrete example in `13` if this item goes ahead.

---

### BL-0067 — Tests that wait on work: no fixed sleeps

| Field    | Value                              |
|----------|------------------------------------|
| Epic     | E00-intake                         |
| Pillar   | P1                                 |
| Priority | P2                                 |
| Effort   | S                                  |
| Status   | backlog                            |
| Test     | not-tested                         |
| Deps     | —                                  |
| Lock     | —                                  |

**Why / Description:** `10` has no rule for a test that must wait for asynchronous work, and the fixed
`sleep` is the flaky-test pattern agent-written tests produce most. `agent-of-empires/agent-of-empires`
(`AGENTS.md`, at `c2bc548`) states the rule in a language-agnostic form worth adapting: wait on a channel,
barrier or **observable predicate with a deadline**, never a fixed sleep; a deadline **bounds failure, it
does not establish completion**; and before a negative assertion ("X did not happen"), establish the causal
precondition that would have made X happen, or the assertion passes vacuously.

The last clause is the one that matters here: a vacuous negative assertion is the test-side twin of `10`'s
"must fail first" discipline — a test that cannot fail is not testing anything.

**Done means:**

- [ ] `10` gains one short subsection under "Automated tests" stating the three clauses above in the
      methodology's own words, cross-linked to "Why 'must fail' first".
- [ ] No new enum, gate or checklist field — it is guidance inside an existing section.
- [ ] The surface map in `00` is checked; no row restates `10`'s test-writing guidance today, so the
      expected outcome is no fan-out, and that is recorded.

**Files (probable):** `methodology/10_testing_and_verification.md`.

**Notes:** Effort S — a paragraph and a link. It is `backlog` rather than `ready` only because its intent
has not yet been approved; nothing about it is open.

---
