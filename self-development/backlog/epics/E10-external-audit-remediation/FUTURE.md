# E10 — External baseline audit remediation — Future / deferred items

_The three opportunities the external audit raised alongside its findings. All are real and none is
chartered: each is either strictly larger than the finding it would strengthen, or blocked on something
this epic cannot supply. Deferred, not rejected — outright rejections live in the
[charter's "Out of scope"](README.md#out-of-scope). Promote by moving an entry into `BACKLOG.md`
unchanged; this backlog uses the repo-wide monotonic `BL-####` space for future items too, per
[`backlog/README.md`](../../README.md), so promotion needs no renumbering._

_All three entries are `methodology/`- or process-touching ⇒ **T2 (maintainer-authored)** under the tier
matrix._

---

### BL-0053 — Cold-agent conformance fixtures

Small synthetic repositories exercising the failure modes this epic fixes on paper: two agents acquiring
the same item from separate feature branches; a brownfield partial adoption; a wrong Code Map; a changed
`AGENTS.md` arriving in an untrusted PR; an L4-required feature sitting at L3. Run the same tasks through
supported agent tools and score the actions against a shared expected trace.

**Source:** audit opportunity O-01.

**Target:** a new fixtures directory, plus a scoring note per run.

**Why it is deferred rather than chartered:** every item in this epic is a *documentation* fix whose
success criterion is "one governing statement per rule". Fixtures answer a different and harder question —
whether a cold agent, reading the fixed docs, actually behaves correctly. That is worth knowing and it is
a larger piece of work than the repairs themselves. Chartering it now would also test text that is still
changing.

**Symptom that would justify promoting it:** the re-audit passes, and a cold agent still picks the wrong
reading of a rule this epic reconciled. That is the evidence that reconciliation was necessary but not
sufficient.

---

### BL-0054 — Separate source, generated surfaces, and release evidence

Keep lifecycle policy, autonomy classes and authority in small versioned data files; generate the tables,
checklists and skill excerpts from them; emit a release-evidence manifest carrying the tree SHA, checker
version, counts and tag intent.

**Source:** audit opportunity O-02.

**Target:** would supersede BL-0048's register and part of BL-0049's checker.

**Why it is deferred rather than chartered:** this is strictly stronger than declare-then-check, and
strictly more machinery. Generation removes the *possibility* of drift where checking only removes the
*persistence* of it — but it also means the fourteen docs stop being hand-authored markdown, which is a
different project. The cheaper control ships first and earns the harder one.

**Symptom that would justify promoting it:** the checker starts finding real drift repeatedly, which
would mean the register is being ignored rather than followed.

---

### BL-0055 — Independent adopter evidence

Recruit at least two independent adopters in different repository shapes, record their deviations and
failure rates, and have a reviewer who did not author the methodology score the transfer outcomes.

**Source:** audit opportunity O-03.

**Target:** no file — this is evidence collection, not a doc change.

**Why it is deferred rather than chartered:** it is **already the Phase 1 → Phase 2 blocker** recorded in
[`EPICS.md`](../../EPICS.md), and the active-campaign route was closed by maintainer decision on
2026-08-19 on the position that a good project sells itself. Recording it here keeps the audit's decision
list fully accounted for; it does not duplicate a known blocker into a second place where it can go stale.

**Note on where it does *not* belong:** this is not a `HUMAN_NEEDED.md` entry. That file holds items
blocked on a human-only *action*. There is no blocked item here — only an absent adopter, which no action
in this repo produces.

**Symptom that would justify promoting it:** an adopter appears. Until then the constraint is external and
the correct state is to wait, not to plan.
