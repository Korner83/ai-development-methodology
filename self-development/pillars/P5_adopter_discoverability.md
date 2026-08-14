# P5 — Adopter discoverability

> **Pillar goal:** adopters with the right intent find the methodology — via GitHub search, awesome lists, peer recommendations — without needing to know its specific name.
>
> **Last updated:** 2026-05-25

**Related:**
- Brief: [Capability layer 5](../brief/08_capability_layers.md#5-adopter-discoverability)
- Strategy phase: [Phase 2 — Discovery](../strategy/00_master_plan.md#phase-2--discovery-3--12-months-from-phase-1-exit) (primary)
- Depends on: [P4 — Tool compatibility](P4_tool_compatibility.md), [P2 — Doc clarity](P2_doc_clarity.md), [P3 — Doc currency](P3_doc_currency.md)
- Feeds into: [P6 — Example richness](P6_example_richness.md), [P7 — Community feedback loop](P7_community_feedback_loop.md)
- Delivering epics: (none yet)

## 1. Overview

The methodology can be the most complete and clearest in the field and still fail if nobody finds it. Discoverability is the bridge between "the methodology exists" and "adopters use it."

This pillar is *dormant in Phase 1* and *primary in Phase 2*. Phase 1 is foundation work — making sure the methodology is worth discovering. Phase 2 is the discovery push itself: awesome-list submissions, GitHub topic optimization, opportunistic posts, organic referral patterns.

Discoverability isn't aggressive marketing. It's *being findable when the adopter is actively searching*. The marketing posture per [brief/06_distribution.md](../brief/06_distribution.md): "be useful, be honest, be findable. Don't be loud."

## 2. What this pillar covers

| Channel | What "discoverable" means here |
|---|---|
| **GitHub search** | Repo surfaces for searches like "AI development methodology," "agentic-coding methodology," "ai-agents methodology." Achieved via topics, description, and clear README. |
| **GitHub topics** | At least 10 well-chosen topics that match adopter search vocabulary. Current count: 13. |
| **Awesome lists** | Listed in ≥3 widely-known awesome-* lists in the AI-coding space. Two PRs currently open. |
| **Organic referral** | Adopters arrive via "someone mentioned this in a talk / blog / podcast" — measurable via Discussions threads where adopters say where they heard about it. |
| **GitHub Pages site** | Adopters who prefer rendered docs over the GitHub UI have a polished landing. (Live as of v1.x.) |
| **Direct URL recall** | The repo URL is short enough and the slug clear enough that adopters can recall and share it without lookup. |
| **Snippet quality** | The repo's description (the line that appears in GitHub search results) accurately conveys what the methodology is in <200 characters. |

## 3. Exit criteria

The pillar is *delivered* (evergreen) when:

- [ ] External adoption signal exists — stars are a baseline indicator (not the goal; see [brief/05_success_metrics.md "What's NOT a success metric"](../brief/05_success_metrics.md#what-success-is-not)), but at least *some* baseline discoverability is required for adoption to be possible at all.
- [ ] Externally-authored adoption stories exist — at least one (per [brief/05_success_metrics.md "Early signals"](../brief/05_success_metrics.md#early-signals-first-year)). Real adopters publicly say "we use this" with specifics.
- [ ] Listed in widely-known awesome-* lists in the AI-coding space (at least one PR merged, others open).
- [ ] Repo description is current and accurate (the v1.3.1 honesty pass refreshed this; recheck at each release).
- [ ] At least 10 GitHub topics are set and match adopter search vocabulary.
- [ ] GitHub Pages site is live and the README renders correctly on it.

**Re-tested:** quarterly during Phase 2; opportunistically when a new high-traffic discovery channel appears (e.g., a new awesome-list emerges).

## 4. Dependencies

**Depends on:**

- [P4 — Tool compatibility](P4_tool_compatibility.md). Discoverability without compatibility = adopters bounce on first read.
- [P2 — Doc clarity](P2_doc_clarity.md). Discovery brings visitors to the README; clarity converts them to adopters.
- [P3 — Doc currency](P3_doc_currency.md). Discovered methodology with broken links or stale facts loses trust immediately.

**Feeds into:**

- [P6 — Example richness](P6_example_richness.md). Discovered adopters want to see worked examples; examples reinforce discovery's value.
- [P7 — Community feedback loop](P7_community_feedback_loop.md). Discovery is the precondition for community formation.

## 5. Anti-patterns

- **Submitting to every awesome-list to maximize coverage.** Spammy submissions burn maintainer goodwill. Submit where the methodology genuinely fits; skip lists that are tools-only.
- **SEO-stuffing the README.** Adopters spot keyword-stuffing immediately; it tanks the clarity (P2) cost-benefit.
- **Aggressive posting on social media.** The "be useful, be honest, be findable; don't be loud" framing applies. Once-per-release tasteful announcements; not weekly engagement-bait.
- **Buying visibility** (paid ads, sponsored posts, etc.) — anti-goal per [brief/06_distribution.md](../brief/06_distribution.md).
- **Focusing on stars over real adoption.** Stars are vanity; adoption stories are the goal. A methodology with 50,000 stars and 50 real adopters is failing.
- **Burying the value prop.** The README's first line and the GitHub description are the entire snippet most visitors see. Each must convey what the methodology is in one phrase.

## 6. Current state (v1.8.0)

**Strong:**

- Repo description refreshed (v1.3.1 honesty pass).
- 13 GitHub topics set.
- 2 awesome-list PRs open (webfuse-com/awesome-claude #238 — confirmed live; dontriskit/awesome-ai-software-engineering #8 — merged into the repo per earlier session).
- GitHub Pages live at korner83.github.io/ai-development-methodology.
- README leads with the value prop (the "panic-refactored your auth middleware at 2am" framing).
- Repo URL is clean: `github.com/Korner83/ai-development-methodology`.

**Known gaps:**

- Stars near zero. The Phase 2 metric of ≥500 is aspirational at present.
- No referenced public adoption stories yet (the project is too new).
- No conference talk, no podcast mention, no widely-shared blog post yet.
- Profile pinning hasn't been done — the maintainer's GitHub profile doesn't surface this repo prominently. (Highest single GitHub-internal visibility action still pending.)
- No proactive outreach in adjacent communities (Anthropic's Discord, Cursor's community, etc.).

**Honest:** discoverability is currently the most underdeveloped pillar relative to its eventual primary-pillar status. Phase 1 work is foundation; Phase 2 work is the discovery push. This pillar moves from "set up infrastructure" (now) to "actively work" when Phase 2 begins.

## 7. Delivering epics

(None yet. Likely Phase 2 epics: "Awesome-list saturation" (target ≥3 listings); "First public adoption story" (write one or commission one); "Profile pinning + visible repo placement.")
