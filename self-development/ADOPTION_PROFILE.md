# Adoption profile — how much of this methodology this repository actually uses

[`README.md`](../README.md) presents [`self-development/`](.) as the methodology applied to its own
development. That is true and it is partial, and until 2026-08-20 **the partiality was nowhere stated** —
so a brownfield adopter reading this directory as the worked reference could copy an omission and think it
was the convention. That is audit finding F-09.

**Partial adoption is legitimate. Undeclared partial adoption is not.** This file is the declaration.

**Read the omissions and adaptations first.** A profile that opens with what went well is marketing.

---

## Omitted, and where the gap shows

| Component | State | Why |
|---|---|---|
| **Committed integrity checker / CI beyond a secret scan** | **omitted by decision** (2026-08-20) | This repo ships no runnable elements. The cost is real: every published count is hand-maintained, and the same tag-count error shipped three releases running. [`RELEASE_EVIDENCE.md`](RELEASE_EVIDENCE.md) writes the commands down instead — **weaker than a control, and stated as such** |
| **Two-layer memory** ([`08`](../methodology/08_lessons_and_memory.md)) | **omitted** | This repo has no `memory/` directory. The methodology's memory discipline is exercised only by the fictional [`examples/example-project`](../examples/example-project/), not here. The memory admission test has therefore never run on real content |
| **Context-integrity canary** ([`08`](../methodology/08_lessons_and_memory.md)) | **omitted — and it could not have been adopted** | It requires a project instruction file to demand a response marker, and this repo had none until 2026-08-20. **Open maintainer decision** — see [the sweep](evaluations/2026-08-20-convention-sweep.md) §4 |
| **House verbosity setting** ([`08`](../methodology/08_lessons_and_memory.md)) | **omitted — same cause** | Nowhere to set it until today. Recommended for retirement in the sweep; retiring it costs a MAJOR bump, so it is a maintainer call |
| **UI verification loop, blast radius, most of `10`** | **not applicable** | Docs-only. There is no UI to verify and no consumer graph to enumerate. This is the single largest thing this instance does *not* exercise, and it is why [`STATUS.md`](../STATUS.md) says the self-application "exercises the planning, review, and memory disciplines far harder than it exercises the UI-verification and testing disciplines" |
| **Cross-AI validation as a gate** | **adapted, then dropped for E10** | Run for E06/E07/E08 (E06's returned 16 PASS / 2 FAIL, both real). **Waived for E09** by decision, and **removed from E10's exit criteria** by decision on 2026-08-20. The convention remains published for adopters; this repo no longer gates on it |

---

## Adapted, with the deviation named

| Component | Adapted how | Why |
|---|---|---|
| **Epic file shape** ([`03`](../methodology/03_epics.md)) | Five files required; **nine epics ran on four** until 2026-08-20 | The rule was **not** weakened to match. `TEST.md` was backfilled into all nine as empty-but-present with a pointer to the real verification record in each `ARCHIVE.md`. **No acceptance rows were reconstructed** — back-filling scenarios that never ran would be fabricated evidence in a repo audited for asserting unperformed checks |
| **WIP cap** ([`03`](../methodology/03_epics.md)) | **2**, not the methodology default of 3 | Raised from 1 after E02. **Never contended** — nine epics, never two active at once — so there is no evidence for raising it further, and raising a limit that has never bound would be a change with no information behind it |
| **Epic lifecycle** | Five of nine closures ran `charter → close` inside one maintainer-directed session | Real, and worth naming against ourselves: same-day charter-to-close is the norm here, which means the WIP cap is not the mechanism doing any work — **maintainer attention is** |
| **Versioning** | Self-development work ships as minor or patch; `methodology/` versions independently | Recorded in [`backlog/README.md`](backlog/README.md) |
| **Autonomous loop** | Tiered: T0/T1 loop-enabled on authoritative docs, **T2/T3 maintainer-authored** | Stricter than the published default. Every E10 item was T2 or T3 |

---

## Adopted as written

Strategy → pillars → epics → items; the `BL-####` item format with its eight required fields; the
`Status`/`Test` enums and the `done` hard rule; frozen intent on approved goals and exit criteria; the
`Needs clarification` marker; Code Maps at Effort M+; the six DoD gates; the file lock protocol; the git
workflow including PR-only trunk; the AI-safety rules; semi-annual currency passes; milestone evaluation
with its rubric.

**Two of those were first exercised on 2026-08-20** — the `Needs clarification` marker and, under real
pressure, frozen intent. The sweep records that **6 of 16 conventions added v1.25.0 → v1.31.0 have ever
been used at all.**

---

## What an adopter should take from this

- **The planning cascade and the item discipline are the load-bearing parts**, and they are exercised hard
  here. Copy those with confidence.
- **The testing and UI-verification chapters are the least proven by this instance.** A docs repo cannot
  exercise them. If those are the parts you need, [`examples/example-project`](../examples/example-project/)
  is a worked sketch, not evidence.
- **Do not copy the omissions.** No memory directory, no canary, no integrity checking — those are this
  repo's choices under its own constraints, not recommendations.
- **The honest headline** stays the one in [`STATUS.md`](../STATUS.md): one production project, one
  docs-only self-application, **no external adopters**, and a closed-beta verdict of NOT READY.
