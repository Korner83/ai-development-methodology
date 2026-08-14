# P2 — Doc clarity

> **Pillar goal:** any methodology doc can be read once and applied without re-reading.
>
> **Last updated:** 2026-05-25

**Related:**
- Brief: [Capability layer 2](../brief/08_capability_layers.md#2-doc-clarity)
- Strategy phase: [Phase 1 — Foundation](../strategy/00_master_plan.md#phase-1--foundation-current--3-months) (primary)
- Depends on: [P1 — Doc completeness](P1_doc_completeness.md)
- Feeds into: [P3 — Doc currency](P3_doc_currency.md)
- Delivering epics: (none yet)

## 1. Overview

Adopters' time is the constraint. A 1,000-line doc that's actually clear gets used; an 800-line doc that's "almost clear" gets skimmed and produces drift. Clarity is the difference between a methodology adopters internalize and one they reference reluctantly.

Clarity is harder than completeness. Completeness is checklist-shaped; clarity is taste-shaped. The bar: a contributor (human or AI) reads the doc, applies what they learn without re-reading, and produces work consistent with the methodology's intent.

This pillar is also the most direct counter to the "AI-bloat" failure mode — docs written by AI without revision that read as competent-but-wordy. v1.4.0's README rewrite (348 → 220 lines, ~37% compression) was a deliberate clarity intervention.

## 2. What this pillar covers

| Quality | What "clear" means here |
|---|---|
| **Voice** | Direct, opinionated, no hedging-for-its-own-sake. Reads like a senior practitioner, not a junior copywriter. |
| **Density** | Every paragraph carries weight. No "comprehensive overview" framings, no "synergy"-style filler. |
| **Specificity** | Concrete examples and patterns; not generic principles waving at the topic. |
| **Length** | As short as possible, no shorter. A doc that's twice the length of what an adopter needs to read once is failing this pillar. |
| **Structure** | Scannable. Headings carry meaning. Tables where lists would be longer. Bullets where prose would be looser. |
| **Cross-references** | When the topic is covered elsewhere, link rather than duplicate. Don't make the reader read it twice. |
| **Honest hedging** | Where claims are uncertain ("we observe that...", "this hypothesis...") the hedging is explicit. Don't disguise uncertainty as fact. |

## 3. Exit criteria

The pillar is *delivered* when:

- [ ] Most recent semi-annual self-evaluation has been completed within the last 6 months AND the cross-AI reviewer flagged no methodology docs as "unclear" or "requires re-reading."
- [ ] README is under 350 lines (currently 374 lines as of v1.27.0).
- [x] Longest single methodology doc is under 1,050 lines — **met at v1.27.0**: `09_git_workflow.md` trimmed 1,026 → **798**; the new longest is `04_backlog_items.md` at ~1,018, still under the cap but now the doc to watch.
- [ ] During the most recent maintainer review pass, no methodology doc contained the AI-bloat indicator list (defined: "comprehensive overview" framings, stacked defensive caveats unrelated to the topic, sentences over ~50 words, subsection nesting deeper than `####`).

**Re-tested:** semi-annual self-evaluation; spot-check whenever the maintainer notices "this doc is hard to read."

**Health indicators** (not binary):

- Senior-engineer-cold-read test (would a senior practitioner reading it cold apply it?) — subjective but useful when triggered by specific feedback.
- Adopter feedback signal: "I had to read this three times" surfacing in Discussions → re-read the doc and tighten.

## 4. Dependencies

**Depends on:** [P1 — Doc completeness](P1_doc_completeness.md). You can't be clear about something you haven't written.

**Feeds into:**

- **P3 — Doc currency.** Currency requires re-reading; re-reading is cheaper when the docs are clear.
- **P5 — Adopter discoverability.** Visitors who land on the README form an opinion in 30 seconds; clarity is what makes that opinion positive.
- **P6 — Example richness.** Examples reinforce clarity. A clear doc with a worked example is more applicable than either alone.

## 5. Anti-patterns

- **Adding hedge-words to seem balanced.** "This is generally considered to potentially be useful in some cases" reads as cowardice, not nuance. Direct claims with honest hedge where genuinely uncertain.
- **"Comprehensive overview" framings.** Comprehensiveness is the *bar*, not the *claim*. Just be comprehensive; don't announce it.
- **Over-specifying for completeness.** Sometimes a topic genuinely needs 800 lines. Most times it needs 200. Default to the lower bound; expand if adopters report missing depth.
- **Long sentences with multiple clauses chained by commas, where each clause adds qualifications that might or might not bear on the underlying claim, which itself was usually clear before the qualifications.** Like that one.
- **Defensive caveats stacked.** "This is not legal advice. This is not financial advice. This is not medical advice." (...the methodology is about software.) One caveat where genuinely needed; otherwise none.
- **Writing in the voice of "the methodology says."** The methodology doesn't have a voice. The maintainer does. Write in plain direct prose; let the methodology emerge from the content.

## 6. Current state (v1.8.0)

**Strong:**

- The v1.4.0 README rewrite (348 → 220 lines) was a deliberate clarity intervention; the result is materially better than v1.3.x.
- The "no AI-bloat" feedback loop has been applied multiple times in v1.4.x (e.g., dropping the "every six months" specific claim in v1.4.3).
- Methodology docs increasingly use tables for enumerable content (which scans faster than bullets).

**Known gaps:**

- **`04_backlog_items.md` is now the doc at the edge** (~1,018 lines), having absorbed the Code Map, frozen intent, and size-budget sections in v1.25.0. `09_git_workflow.md` was trimmed to 798 in v1.27.0 (E03) and is no longer the constraint. The E03 decision doc records the trim-vs-split reasoning if 04 reaches the same point — note that 04 will not have 09's ~120 lines of outright duplication to harvest.
- **`README.md` is over its own criterion: 374 lines against a 350 target** (breached some time before v1.27.0; v1.27.0 added ~7 more reflecting the new conventions). The growth is structural — the "Why this exists" problem/solution table is now 18 rows, because every convention added to the methodology earns a row. That table will keep growing unless it is capped deliberately (e.g. hold the most compelling ~12 and let the rest live only in the docs). Maintainer call: the README's job is to *sell and orient*, not to enumerate, so a shorter table may serve better than a complete one.
- Mid-doc cross-references are sometimes still buried in prose where a table at the top would scan faster.
- No automated way to detect AI-bloat patterns — relies on maintainer eye and cross-AI review.

**Honest:** clarity is a permanent project. There's no "done"; only "currently good."

## 7. Delivering epics

(None yet.)
