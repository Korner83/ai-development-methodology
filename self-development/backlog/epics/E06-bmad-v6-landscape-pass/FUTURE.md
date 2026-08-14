# E06 — BMAD v6 landscape pass — Future / deferred items

_Tier-2 ideas from the 2026-08-14 BMAD v6.11 review (`self-development/brief/03_competitive_landscape.md`,
local-only). Deferred, not rejected: good fits that lose the ROI contest against the five
BACKLOG items. Promote by moving an entry into `BACKLOG.md` unchanged (Scheme A: this backlog
uses the repo-wide monotonic `BL-####` space for future items too, per
[`backlog/README.md`](../../README.md), so promotion needs no renumbering)._

_All entries are `methodology/`-touching ⇒ T2 (maintainer-authored) like the rest of the epic._

---

### BL-0020 — Boundaries triad (Always / Ask First / Never) in item and charter templates

Replace prose-only scope sections with three actionable tiers: **Always** (invariants),
**Ask First** (decisions that trigger halt-and-ask — wires directly into the existing
escalate-by-default stance), **Never** (non-goals and forbidden approaches). Sharper for
agents than "Out of scope" prose alone. **Source:** the Boundaries & Constraints block in
BMAD's `spec-template.md`. **Targets:** `templates/`, `04_backlog_items.md`, `03_epics.md`.

### ~~BL-0021 — Derivable-from-source admission test for memory and instruction entries~~

**Promoted and shipped in v1.26.0** — see [ARCHIVE.md](ARCHIVE.md#bl-0021--derivable-from-source-admission-test-for-memory-and-instruction-entries).
Promoted out of order (ahead of BL-0020) at maintainer direction, after E06 had already closed;
the entry stays here struck through so the deferral decision and its reversal are both legible.

### BL-0022 — Optional per-epic context digest with a staleness rule

For long epics, an optional one-page digest distilling strategy/pillar/charter constraints an
implementer actually needs ("by purpose, not by source"), with the mechanical staleness rule:
**stale if any upstream planning doc is newer than the digest** — regenerate before trusting.
Builds on BL-0019's budgets. Defer until BL-0015/BL-0019 land (they may make this unnecessary
for most projects). **Source:** BMAD `compile-epic-context.md` (800–1500-token epic context
with mtime invalidation). **Targets:** `03_epics.md`, `08_lessons_and_memory.md`.

### BL-0023 — Brownfield discovery pass ("ratify what's there")

Extend brownfield adoption stages A–B with a reverse-engineering session: inventory the
existing conventions and *ratify* them rather than inventing new ones, and **run every command
before writing it down** (verified, not guessed, project facts). Output feeds the instruction
file and pillar backfill (stage E). **Source:** BMAD `bmad-project-context` discovery mode +
architecture "ratify the conventions already there." **Target:** `00_README.md` brownfield
section.

### BL-0024 — Human-review walkthrough ergonomics at the user gate

Guidance for the moment work reaches the human final gate: instead of a raw diff, provide an
oriented walkthrough — what changed and why, where to look first, how to test it, `path:line`
references — then stop talking and let the human review ("front-load, then shut up").
Cheap addition; the user gate is our binding constraint, so making review fast compounds.
**Source:** BMAD `bmad-checkpoint-preview`. **Targets:** `07_definition_of_done.md`,
`11_human_roles.md`.
