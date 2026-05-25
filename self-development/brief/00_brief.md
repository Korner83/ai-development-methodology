# Brief — TL;DR

This folder contains the **brief** for the AI Development Methodology project itself. It back-engineers the project's intent into the eight inputs that the methodology's own [Step 0 — Have a brief](../../README.md#how-to-use-it) requires as prerequisites to strategy work.

These docs anchor everything downstream: Step 1 (master plan + pillars), Step 2 (epics), Step 3 (items / tasks), Step 4 (autonomous loop).

## At a glance

| Question | Answer | Doc |
|---|---|---|
| Why does this exist; who does it serve at success? | A portable, file-based methodology that makes AI-collaborated software development sustainable past week 3 — for solo devs, small mixed teams, indie hackers, and engineering leaders — without enterprise overhead or vendor lock-in. | [01_vision.md](01_vision.md) |
| Who specifically is the audience? | Four primary segments (solo + AI; small mixed teams; indie hackers / startup founders; engineering leaders adding AI to existing workflows) plus three secondary (AI-tool builders, educators, researchers). | [02_audience.md](02_audience.md) |
| What public alternatives exist? | Nine named alternatives surveyed during the v1.5.0 research: GitHub Spec Kit (~106k★), BMAD Method, Ralph loop, stdlib pattern, AGENTS.md standard, GSD, nano-spec, vendor docs (Anthropic / OpenAI / Cursor / Aider), academic papers (Agentsway, Agile V). | [03_competitive_landscape.md](03_competitive_landscape.md) |
| What do those alternatives leave unaddressed? | Nine concrete gaps: cheating-agent anti-pattern, locks for humans+agents same protocol, challenge-before-consenting prompt, four-layer planning, DoD coupled to item, HUMAN_NEEDED.md, ROI heuristic with table, self-evaluation cadence, decision-ownership matrix. | [04_market_gaps.md](04_market_gaps.md) |
| What does success look like by horizon? | **1-year:** ≥500 stars + ≥10 referenced adoption stories + ≥3 substantive forks + self-development loop operational. **3-year:** referenced as a "named" methodology alongside Spec Kit / BMAD; ≥3 small companies adopt as internal standard; cross-pollination to peers. | [05_success_metrics.md](05_success_metrics.md) |
| How does the project sustain itself? | CC BY 4.0. Solo maintainer. Lean overhead. "PRs welcome but no SLA." Self-development loop reduces maintainer burden over time. No revenue model. No SaaS. | [06_distribution.md](06_distribution.md) |
| What's the tech surface? | Markdown + git only. Mermaid diagrams. GitHub for hosting, Pages, Discussions, Releases. `gh` CLI for automation. No CI for docs. No translation infrastructure. | [07_tech.md](07_tech.md) |
| What capability layers does the project need? | Nine candidates that become pillars in Step 1: doc completeness, doc clarity, doc currency, tool compatibility, adopter discoverability, example richness, community feedback loop, maintenance sustainability, self-improvement velocity. | [08_capability_layers.md](08_capability_layers.md) |

## Status

Drafted 2026-05-25 as Step 0 of the [self-development bootstrap](../../). Awaiting cross-AI review and maintainer approval before Step 1 (strategy + pillars) begins.

## How to read this brief

- **Fresh contributor:** read `01_vision.md` first (anchors everything), then `08_capability_layers.md` (concrete capabilities ground the abstract vision), then jump around.
- **Cross-AI reviewer:** read all eight detail files cold (no prior context from the maintainer's session). Report missing sections, overclaimed assertions, weak competitive analysis, unclear capability layers.
- **Maintainer reviewing before approval:** spot-check `03_competitive_landscape.md` (is the survey accurate?) and `08_capability_layers.md` (will these pillars actually hold up to Step 1 conversion?).
