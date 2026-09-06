# E00 — Intake — Active Backlog

_Real work that is not worth a charter. Same item format, same gates, no epic above it.
See the [charter](README.md) for what intake is and the eviction rule that empties it._

**Filed so far: 5. Closed: 3.** Three of the five came out of E10's convention sweep as decisions that were
recorded and then not executed — which is the same failure class as a claim asserted and not checked, and
is precisely the kind of work that had nowhere to live before this file existed.

## Summary

| ID | Title | Priority | Effort | Status |
|---------|------------------------------------------------------|----------|--------|-------------|
| BL-0058 | Read the Agent File spec; decide on a conformance line | P2 | S | ready |

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

