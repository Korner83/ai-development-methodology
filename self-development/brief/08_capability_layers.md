# Capability Layers

The methodology project needs to be capable of nine distinct things. These are the **capability layers** that become pillars in Step 1.

Per [methodology/02_pillars.md](../../methodology/02_pillars.md), pillars are capability-shaped (what the product needs to *be able to do*), not feature-shaped (what to build) and not goal-shaped (what state to reach). The nine below are deliberately capability-shaped — testable via "can the project do X today?" rather than via deliverables.

The layers are roughly sequentially dependent: doc completeness comes before doc clarity (you have to have docs before you can be clear about them); discoverability comes before community feedback loop (people have to find you before they can give feedback); etc.

## The nine capability layers

### 1. Doc completeness

**The capability:** for every common situation an adopter encounters, the methodology has explicit guidance.

**Why it matters:** gaps in coverage send adopters away. A methodology that's good on 8 of 10 needed surfaces feels incomplete; adopters either improvise (and get burned) or leave.

**Tested by:**
- Surveys of adopter questions in Discussions / Issues — do questions cluster around topics the docs don't cover?
- Cross-AI review during the semi-annual self-evaluation — what does a fresh AI session say is missing?
- Adopter feedback (when it arrives) — what did they wish was documented?

**Current state (v1.6.0):** 12 methodology docs + 5 templates covering planning hierarchy, working principles, DoD, locks, memory, git workflow, testing/verification, human roles, project structure, autonomous loop, agent kickoff. Substantial coverage; gaps closed in v1.5.0 (stdlib growth loop, verification taxonomy, brownfield onboarding, decision matrix) and v1.6.0 (self-evaluation cadence, five git additions).

**Pillar shape:** P1 — Doc completeness.

### 2. Doc clarity

**The capability:** any methodology doc can be read once and applied without re-reading.

**Why it matters:** adopters' time is the constraint. A 1,000-line doc that's actually clear gets used; an 800-line doc that's "almost clear" gets skimmed and produces drift.

**Tested by:**
- Cross-AI review of voice and density (catches AI-bloat, over-hedging, unnecessary repetition).
- Adopter feedback signals — "I had to read this three times" is failure.
- Maintainer self-review during semi-annual self-evaluation.

**Current state (v1.6.0):** ongoing concern. The v1.4.0 README rewrite cut 348 → 220 lines explicitly to address "feels AI-written." The v1.4.3 patch removed an oddly-specific "every six months" claim. Methodology docs have been refined incrementally for voice.

**Pillar shape:** P2 — Doc clarity.

### 3. Doc currency

**The capability:** methodology docs accurately describe how the project (and adopters) actually work today, not how they worked at some earlier point.

**Why it matters:** stale docs are worse than no docs. Adopters lose trust when they hit a recommendation that no longer applies.

**Tested by:**
- Semi-annual methodology self-evaluation (added in v1.6.0, lives at [methodology/07_definition_of_done.md](../../methodology/07_definition_of_done.md)).
- Quarterly repo health audit checks for stale claims (e.g., line counts, doc counts, version references).
- Memory-as-leading-indicator: clusters of memory entries about the same topic signal a stale doc.

**Current state (v1.6.0):** self-evaluation cadence newly established. v1.3.1's "honesty pass" was the first deliberate currency-fix release.

**Pillar shape:** P3 — Doc currency.

### 4. Tool compatibility

**The capability:** the methodology's protocols work with any AI coding tool that reads a project-instruction file.

**Why it matters:** vendor-neutral is one of the methodology's core values. Tool compatibility is a *prerequisite for adoption*, not a downstream concern — adopters who find the methodology immediately ask "does this work with my tool?" before they read further. If the answer is "you need to use vendor X," adopters who already use vendor Y leave.

**Tested by:**
- The 5 template files in `templates/` support all 6 major AI tools — 3 natively (Claude Code via CLAUDE.md, Codex/Antigravity via AGENTS.md) and 3 via adaptation from AGENTS.md (Cursor, Aider, Continue.dev). Adaptation is the settled answer: E04 proposed native files for the latter three and was parked 2026-08-14 (sync burden against still-moving vendor conventions, for unreported demand).
- Adopter reports of cross-tool use without methodology adjustment.
- New AI tools entering the field — does the methodology gracefully support them?

**Current state (v1.6.0):** templates cover Claude Code, OpenAI Codex, Google Antigravity, Cursor (via adaptation), Aider (via adaptation), Continue.dev (via adaptation). AGENTS.md standard is the canonical "anything else" path.

**Pillar shape:** P4 — Tool compatibility.

### 5. Adopter discoverability

**The capability:** adopters with the right intent find the methodology without knowing its specific name.

**Why it matters:** the methodology can be the best in the field and still fail if nobody can find it. Awesome-list inclusion, GitHub topics, search-engine discoverability all matter at this layer.

**Tested by:**
- GitHub search rankings for relevant queries ("AI development methodology", "ai-agents methodology", etc.).
- Awesome-list inclusion (currently 2 PRs open).
- Organic referral patterns (where do adopters say they found it?).
- Star growth rate as a baseline signal.

**Current state (v1.6.0):** 13 topics set; public visibility confirmed; Pages live; 2 awesome-list PRs open; description refreshed; Discussions welcome thread seeded. Stars near zero — discoverability is the rate-limiting capability for the 1-year metrics.

**Pillar shape:** P5 — Adopter discoverability.

### 6. Example richness

**The capability:** adopters can see how the abstract patterns translate to real projects, not just read about them.

**Why it matters:** abstract docs are necessary but insufficient. Adopters need to see concrete instantiations to know "this would actually work in my situation." Examples reinforce both clarity (P2) and discoverability (P5) — a project that surfaces in search benefits from a visible worked example showing real usage. This is one of the most consistent gaps adopters mention in OSS-project research.

**Tested by:**
- Presence and currency of worked examples.
- Adopter feedback — do they ask "how would this apply to X?" indicating the abstract docs aren't enough?
- The `self-development/` folder is the canonical example (where this brief lives).

**Current state (v1.6.0):** `self-development/` folder created; this brief is the first Step 0 output. Other examples (anonymized real-project artifacts, per the brief's menu) not yet created. Example richness is currently the *least developed* capability layer.

**Pillar shape:** P6 — Example richness.

### 7. Community feedback loop

**The capability:** adopter experience flows back into the methodology via Discussions, Issues, PRs, and direct contact — and shapes future iterations.

**Why it matters:** the methodology improves through real-world friction. Without a feedback loop, the maintainer is improvising; with one, the methodology incorporates lessons from contexts the maintainer hasn't experienced.

**Tested by:**
- Discussions activity (count + quality).
- Issue patterns (what's recurring? what's a one-off?).
- Accepted contributions from external contributors.
- Maintainer's "I learned X from an adopter" notes in CHANGELOG entries.

**Current state (v1.6.0):** Discussions enabled with welcome thread; one external contributor has been the user (the maintainer himself); no external community yet. This capability is mostly dormant until external adoption starts producing feedback signal (see [05_success_metrics.md "Early signals"](05_success_metrics.md#early-signals-first-year)).

**Pillar shape:** P7 — Community feedback loop.

### 8. Maintenance sustainability

**The capability:** the methodology stays current within a sustainable maintainer-time budget — qualitative, not a published quarterly number.

**Why it matters:** burnout is the failure mode for solo-maintained projects. The methodology must not require more attention than the maintainer can give without burning out.

**Tested by:**
- Whether maintaining the methodology starts to feel like a second job (the rule in [05_success_metrics.md "The one operational rule"](05_success_metrics.md#the-one-operational-rule)).
- Frequency and depth of releases.
- Quality of CHANGELOG entries (rushed releases have thin entries).
- The self-development cycle's contribution to maintenance load — does the cycle reduce or increase burden?

**Current state (v1.6.0):** unproven. The 2026-05-25 burst (eight releases in a day) is not sustainable; that pace reflects a maintainer + AI session pushing through accumulated work, not the steady state. Steady-state maintenance hours will become measurable after a few months of operation.

**Pillar shape:** P8 — Maintenance sustainability.

### 9. Self-improvement velocity

**The capability:** the methodology improves itself via the self-development cycle, faster than ad-hoc maintenance could.

**Why it matters:** this is the compounding mechanism. If the cycle works, the methodology evolves with less effort over time; if it doesn't work, the cycle is overhead.

**Tested by:**
- Whether the self-development cycle ships methodology improvements (not just self-development cleanup). The cycle is the methodology's most distinctive claim; if it doesn't produce real methodology releases, the claim is theoretical. See [05_success_metrics.md "Early signals"](05_success_metrics.md#early-signals-first-year).
- "This came from the cycle" attribution in CHANGELOG entries.
- Methodology shifts the maintainer wouldn't have discovered solo (see [05_success_metrics.md "Sustained signals"](05_success_metrics.md#sustained-signals-multi-year)).

**Current state (v1.6.0):** cycle not yet operational. This brief is Step 0 of bootstrapping it. The capability becomes testable only after Step 4 (autonomous loop setup) lands.

**Pillar shape:** P9 — Self-improvement velocity.

## How these become pillars

In Step 1 (master plan + pillars), each capability layer above becomes a pillar file at `self-development/pillars/PN_*.md`. The skeleton from [methodology/02_pillars.md](../../methodology/02_pillars.md) applies: each pillar gets goal + capability description + exit criteria + dependencies on other pillars.

Likely sequential dependencies:

```
P1 (Doc completeness) — quality starts with coverage
  └─ P2 (Doc clarity) — clarity is improvement on top of completeness
      └─ P3 (Doc currency) — currency is maintenance on top of clarity
          └─ P4 (Tool compatibility) — adopters can't use the methodology without a compatible tool
              └─ P5 (Adopter discoverability) — they have to find it before they can adopt
                  └─ P6 (Example richness) — examples reinforce clarity + accelerate adoption from discovery
                      └─ P7 (Community feedback loop) — feedback requires discoverability + compatibility + active adoption
                          └─ P8 (Maintenance sustainability) — sustainability is a long-term constraint that only matters with traction
                              └─ P9 (Self-improvement velocity) — only meaningful after all of the above; the compounding mechanism
```

Some of these might merge or split during Step 1 conversion. The set above is the **starting seed**, not a finalized pillar list.

## What's NOT a capability layer (and why)

- **Visual design / branding.** Not a methodology concern; markdown + git is the brand.
- **Performance / speed of the docs.** Static markdown loads fast enough on any infrastructure.
- **Localization.** Decided against (see [07_tech.md](07_tech.md)).
- **Mobile-friendliness.** GitHub's default rendering is mobile-OK; not a separate capability.
- **Security of the docs themselves.** Markdown files have no attack surface.
- **Integration with specific AI vendors.** Anti-goal — vendor-neutral is the value.

## How this brief connects to the rest of the planning cascade

This file (`08_capability_layers.md`) is the **most consequential** brief file for Step 1, because pillars derive from these layers. Vague or weak layers here produce vague or weak pillars later.

The cross-AI review for this brief should pay particular attention to: are the layers truly capabilities (vs. features or goals)? Are they testable? Is the sequential dependency order plausible? Are any obvious capabilities missing?

If the answer to any of these is no, this file needs revision before Step 1 starts.
