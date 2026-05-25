# P3 — Doc currency

> **Pillar goal:** methodology docs accurately describe how the project (and adopters) actually work today, not how they worked at some earlier point.
>
> **Last updated:** 2026-05-25

**Related:**
- Brief: [Capability layer 3](../brief/08_capability_layers.md#3-doc-currency)
- Strategy phase: [Phase 1 — Foundation](../strategy/00_master_plan.md#phase-1--foundation-current--3-months) (primary) and [Phase 2 — Discovery](../strategy/00_master_plan.md#phase-2--discovery-3--12-months-from-phase-1-exit) (primary)
- Depends on: [P2 — Doc clarity](P2_doc_clarity.md)
- Feeds into: [P5 — Adopter discoverability](P5_adopter_discoverability.md) (stale docs hurt discoverability when adopters find references that don't resolve)
- Delivering epics: (none yet)

## 1. Overview

Stale docs are worse than no docs. Adopters lose trust when they hit a recommendation that no longer applies, a file count that's wrong, a link that 404s. The v1.3.1 "honesty pass" release was the first deliberate currency-fix effort — it found three concrete drift items shipped in v1.3.0 within hours.

Currency is the cumulative test: across many small drifts, the methodology as a whole still describes reality. Each individual drift is small; the aggregate becomes "the methodology is a fossil — accurate to when it was written, not to today."

The methodology added the [semi-annual self-evaluation cadence in v1.6.0](../../methodology/07_definition_of_done.md#methodology-self-evaluation-semi-annual) precisely because currency requires a scheduled pass; ad-hoc maintenance lets drift compound.

## 2. What this pillar covers

| Surface | What "current" means here |
|---|---|
| **Methodology docs** | Each doc accurately describes how the practice works today. No stale rules; no obsolete cross-references. |
| **README facts** | Line counts, file counts, version references, "longest doc" claims — all match reality within rounding. |
| **CHANGELOG accuracy** | Each entry described what actually shipped; no broken links to removed files; no stale references. |
| **Cross-document consistency** | When fact X appears in doc A and doc B, both say the same thing. |
| **Live integrations** | Links to GitHub features (Discussions, Pages, Releases) work; templates link to current files; mermaid diagrams render. |
| **Brief / self-development docs** | The brief and pillar docs in `self-development/` reflect current strategic state, not v1.x speculation. |

## 3. Exit criteria

The pillar is *delivered* (evergreen, not done) when:

- [ ] Most recent semi-annual self-evaluation has been completed within the last 6 months.
- [ ] No known broken internal links in any doc (per quarterly link scan).
- [ ] No known factual mis-statements (line counts within ±5%, version references current, file counts accurate per the tree convention).
- [ ] CHANGELOG's most recent release entry accurately matches the diff shipped (verified at release time per [methodology/09_git_workflow.md "Release tagging"](../../methodology/09_git_workflow.md#release-tagging-and-semantic-versioning)).
- [ ] No stale CHANGELOG entries linking to removed content (per most recent honesty pass).

**Re-tested:** quarterly repo health audit (the lighter pass) + semi-annual methodology self-evaluation (the deeper pass).

## 4. Dependencies

**Depends on:** [P2 — Doc clarity](P2_doc_clarity.md). Stale clear docs can be detected and fixed; stale unclear docs are harder to even diagnose as stale.

**Feeds into:**

- **P5 — Adopter discoverability** — adopters who find stale references lose confidence; currency protects the trust visitors form on first read.
- **P7 — Community feedback loop** — currency depends on the community surfacing drift (issues, Discussions). Without P3, the feedback loop has nothing to refine.
- **P8 — Maintenance sustainability** — currency is one of the major recurring maintenance demands. The cadence (quarterly + semi-annual) is what makes it sustainable.

## 5. Anti-patterns

- **"We'll fix it when someone notices."** Drift compounds; the cost of fixing 15 small drifts is much higher than fixing one immediately.
- **Updating only the line that's wrong** rather than scanning for related drift. When you find one stale fact, look for adjacent ones.
- **Promising currency without scheduling it.** "We'll keep docs current" without a cadence is wishful. The cadence (quarterly / semi-annual) is the commitment.
- **Updating one doc but not its cross-references.** Drift creates ripples; check inbound links when changing a section's slug or moving content.
- **Treating release notes as authoritative over CHANGELOG.** CHANGELOG is canonical; release notes are derived. If they disagree, CHANGELOG wins.
- **Adding "verified 2027-05-25" stamps as theater.** Verification is in the actual fact-checking, not the stamp. Stamps that aren't earned by real verification mislead.

## 6. Current state (v1.8.0)

**Strong:**

- v1.3.1 honesty pass set the precedent that drift is fixable in patch releases.
- v1.6.0 added the semi-annual self-evaluation cadence to [methodology/07_definition_of_done.md](../../methodology/07_definition_of_done.md).
- Line counts, file counts, longest-doc claims have been refreshed across multiple releases (v1.4.0, v1.4.1, v1.5.0, v1.6.0, v1.7.0).
- CHANGELOG entries are dated and reference specific commits.

**Known gaps:**

- No automated link-checking; relies on manual scans (which have caught broken links twice — `EVALUATION.md` in v1.3.1 and others surfaced via PowerShell scripts).
- The first semi-annual self-evaluation hasn't happened yet (the cadence was just added in v1.6.0). Next one due ~2026-11-25.
- No process for catching "rule the team consistently routes around" — that's a deeper currency check that requires adopter telemetry.

**Honest:** currency is fragile in solo-maintained projects. The cadence is the protection.

## 7. Delivering epics

(None yet. A likely Phase 1 epic: "First semi-annual methodology self-evaluation pass" — chartered when the cadence first triggers.)
