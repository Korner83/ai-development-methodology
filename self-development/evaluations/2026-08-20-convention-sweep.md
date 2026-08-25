# Convention sweep — 2026-08-20

**Scope:** every convention added v1.25.0 → v1.31.0, every standing criterion that has been open across
releases, and E10's own acceptance rows. Output of **BL-0056**.

**Why:** [`EPICS.md`](../backlog/EPICS.md) already names the risk against itself — *eleven-plus conventions
shipped across four landscape passes with zero external adopters exercising any of them.* Then an external
audit found ten live defects in the rules those passes were adding to. **A rule nobody has ever run is not
thoroughness; it is unverified surface area**, and it is where the next contradiction comes from.

**Method:** for each convention, ask one question — *has anything in this repo, or any recorded session,
actually used it?* Not "is it a good idea." Not "would it help someone." Used.

---

## 1. Conventions added v1.25.0 → v1.31.0

| # | Convention | Added | Ever exercised? | Decision |
|---|---|---|---|---|
| 1 | **Code Map** at Effort M+ | v1.25.0 | **Yes** — E10 items, both example-project M items | **Keep** |
| 2 | **Frozen intent** + greppable marker | v1.25.0 | **Yes** — E09/E10 items and charters; held under pressure in E10 BL-0040 | **Keep** |
| 3 | **Size budgets** for context artifacts | v1.25.0 | **Yes** — used all through E10, and missed twice, which is itself the evidence | **Keep** |
| 4 | **Failure-layer routing** + two-bounce escape | v1.25.0 | **No record** | **Keep, unproven** — the audit rated this a verified strength and it is cheap; but say plainly that no item has ever been routed by it |
| 5 | **Verification-gap question** + ran-only counting | v1.25.0 | **No record** | **Keep, unproven** |
| 6 | **Memory admission test** | v1.26.0 | **No** — this repo has no `memory/` of its own; only the fictional example exercises it | **Keep, unproven** |
| 7 | **Context-integrity canary** | v1.29.0 | **No, and it could not have been** — the canary requires an instruction file to demand the marker, and this repo had no instruction file until 2026-08-20 | **Adopted 2026-08-20** — now live in root `AGENTS.md`; first exercise in the repo that wrote it |
| 8 | **House verbosity setting** | v1.29.0 | **No** — same cause: nowhere to set it | **Keep, marked unexercised** — maintainer decision 2026-08-20: retiring it is a removed section and a MAJOR bump, which is a large price for one paragraph. Revisit at the 2026-11-25 pass if still unused |
| 9 | **Cross-AI spec-verification** (third mode) | v1.29.0 | **No record** | **Keep, unproven** |
| 10 | **Doc altitude** rule | v1.29.0 | **Yes, editorially** — the "would this become false if I rewrote it?" test shaped E10's resolutions | **Keep** |
| 11 | **Architecture-layer** failure routing | v1.29.0 | **No record** | **Merge into #4** — it is one more layer on an existing ladder, not a separate convention |
| 12 | **`ROLE_BRIEFS.md`** — six per-phase briefs | v1.30.0 | **No record** | **Keep, unproven** — a template is read when used, not memorised; low standing cost |
| 13 | **Blast radius** as 7th verification dimension | v1.30.0 | **Not applicable here** — docs-only repo, no UI | **Keep** — untested by this instance, not unused in principle |
| 14 | **Unattended mode ≠ answering your own questions** | v1.30.0 | **No** — the loop has not run since | **Keep** — now wired to #15, so it has a mechanism rather than a caution |
| 15 | **`Needs clarification`** marker | v1.31.0 | **Yes — first use 2026-08-20**, E10's D1 and D2 | **Keep** |
| 16 | **Agent Skills conformance** declaration | v1.31.0 | **Yes** — and it was wrong; the check never invoked a parser | **Keep, with the lesson attached** |

**Tally: 7 of 16 have ever been exercised** — and **4 of those for the first time on 2026-08-20**, by the
epic responding to the audit. Six remain keep-but-unproven. Both change candidates were decided the same
day: the canary adopted, the verbosity setting kept.

**What this does not say.** Unexercised is not the same as wrong. Most of these are cheap, sit inside docs
a reader consults rather than memorises, and several were rated strengths by the external audit. **The
finding is not "delete them" — it is that this repo has been generating rules faster than it generates
evidence**, and the correct response is to slow the generation, not to bulk-retire what exists.

**#8, the house-verbosity setting, was the retirement candidate — and is kept.** It is the one with no
mechanism, no user, and no evidence: a preference the corpus had opinions about before it had a place to
put them. But retiring it is a *removed section* and therefore a **MAJOR** bump under this repo's own
SemVer table. **Maintainer decision 2026-08-20: keep it, marked unexercised**, and revisit at the
2026-11-25 currency pass if nothing has used it by then. A major version is a steep price for one
paragraph, and the sweep's record is enough to stop it being mistaken for proven.

---

## 2. Standing criteria that have been open across releases

| Criterion | Where | State | Decision |
|---|---|---|---|
| Every template carries a methodology version stamp | Phase 1 exit criterion, master plan | **Unmet since it was written.** None of the six templates carries one | **Drop the criterion.** A version stamp in a template is a copy that goes stale on the adopter's disk, where nothing can refresh it — the stamp belongs in `SKILL.md` and `CHEATSHEET.md`, which are read *from* the repo, and both already carry it. The criterion was asking for the drift this epic spent its time removing |
| `CHEATSHEET.md` under 100 lines | E05 charter, hard exit criterion | **Met at 99 — one line of margin, over cap for eleven releases before v1.31.0, nothing enforcing it** | **Keep the cap, accept it is unenforced.** With the checker declined there is no control; the honest record is that it is a hand-checked budget with a one-line buffer |
| WIP cap = 2 active epics | `EPICS.md` | **Never contended.** Nine epics, never two active at once | **Keep, unproven.** Do not raise it to 3 — there is no evidence either way, and raising a limit that has never bound is a change with no information behind it |
| Semi-annual currency pass | P3, due 2026-11-25 | Ran once (2026-05-25) | **Keep.** Its charge now includes this sweep and the SHA re-pin |

---

## 3. E10's own acceptance rows

Run against the tree on 2026-08-20; results recorded in [TEST.md](../backlog/epics/E10-external-audit-remediation/TEST.md).
Two rows were **cut rather than run**, because the things they tested no longer exist: the CI-required
checker and the cross-AI gate. A criterion whose subject was removed is deleted, not marked failed.

---

## 4. One gap this epic created — and closed the same day

**The context-integrity canary (#7) had somewhere to live for the first time and did not live there.** It
requires the project instruction file to demand a marker on every response; root `AGENTS.md` was added on
2026-08-20 without that rule — a gap this epic created by fixing a different one.

Three options were on the table: add it, record it as deliberately not adopted, or retire the convention
outright (its own section concedes it is "a smoke alarm, not proof of safety").

**Decided 2026-08-20: add it.** The canary is live in root `AGENTS.md`. It cost six lines, not two,
which pushed that file from 49 to 56 against a 50-line budget — **so the budget was raised to 60 rather
than the rule trimmed to fit.** A budget invented the day before should not veto a safety rule the
maintainer chose to adopt; its job is to stop the file becoming a second rulebook, and 56 lines of mostly
links does not do that. Recorded in [`RELEASE_EVIDENCE.md`](../RELEASE_EVIDENCE.md).

---

## 5. Net effect

**No convention was retired in this sweep**, so the docs did not shrink — recorded as such rather than
dressed up. Both candidates went to the maintainer on 2026-08-20: the verbosity setting is **kept and
marked unexercised** (a major version is too steep for one paragraph), and the canary was **adopted**
rather than retired, which moves it from unexercised to exercised. **Net: one fewer unproven convention,
zero lines removed.**

**What the sweep produced instead is the number**: 6 of 16 exercised, 3 of those first exercised today.
That figure belongs in the next milestone evaluation more than any individual retirement does, because it
measures the thing the project keeps doing rather than any single rule it wrote.
