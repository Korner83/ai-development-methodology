# Vision

## What the methodology is

A portable, file-based methodology for software projects where humans and AI agents collaborate as peers. Built for projects that need to last past week 3, on teams that mix humans and AI agents, without enterprise overhead or vendor lock-in.

Markdown + git. No SaaS. No vendor lock-in. CC BY 4.0.

## What it's for

Most software projects accumulate the same failure modes once they last more than a few weeks: direction drifts, work fragments, done-ness becomes fuzzy, lessons evaporate, parallel contributors collide. **AI-assisted projects appear to accumulate these faster** — the effective contributor count doubles and the new contributors don't sleep. The methodology's framing puts this as "twice as fast"; this brief treats it as a hypothesis worth acting on rather than a measured fact. Adopter telemetry to firm the claim is one of the things the 1-year metrics aim to surface.

The methodology closes those failure modes with a small set of practices:

- Four planning layers (strategy → pillars → epics → items).
- Three discipline overlays (working principles, Definition of Done, lessons-learned memory).
- File-based locks with TTL for parallel contributors using the same protocol whether they're humans or AI agents.
- An actual-UI fix-test loop because "tests pass" doesn't mean "the page renders."
- Cross-AI validation as a gate before user testing.
- A two-tier memory system (instruction file + memory directory).
- ROI-based prioritization (Priority × Effort) as the default picking heuristic.
- `HUMAN_NEEDED.md` for items blocked on human agency so AI agents don't deadlock.
- An autonomous-loop template for long unsupervised runs between user check-ins.

## Why this matters now

AI agents are a significant share of code contribution on a growing number of projects. Most methodologies (Agile, Scrum, Kanban, Shape Up, XP) predate this shift. Adopting a pre-AI methodology and adding AI agents inside it produces a class of failures the original methodology can't address: collision between agents, "done" claimed without verification, drift between sessions, AI overreach into human-only decisions, the "cheating agent" pattern where the same AI writes both broken implementation and broken tests.

A methodology written natively for mixed-contributor work is missing from the field. Peer methodologies (Spec Kit, BMAD, Ralph loop, etc.) each address parts of the problem but leave significant gaps (see [04_market_gaps.md](04_market_gaps.md)).

This project fills those gaps without depending on a specific AI vendor, a specific tech stack, or a SaaS platform that might disappear in 18 months.

## What success looks like

### 1-year horizon (by 2027-05)

- **≥500 GitHub stars.** A needed baseline signal; not proof of depth.
- **≥10 referenced public adoption stories.** Blog posts, conference talks, podcast mentions where someone says "we use this and here's how it shaped the project."
- **≥3 substantive forks.** Adopters who have made meaningful additions, not just patches. Forks prove the methodology is generative — others can extend it usefully.
- **≥5 upstream contributions accepted** from external contributors. PRs that add or refine methodology content. Proves a contributor pipeline is forming.
- **Self-development loop operational.** At least 2 minor version releases produced via the autonomous cycle (Step 4+ of this bootstrap).

### 3-year horizon (by 2029-05)

- **Methodology is referenced as one of the "named" methodologies in AI-coding discussions**, alongside Spec Kit, BMAD, and the rest of the peer landscape. Not necessarily the most popular — but legitimately on the list when people compare options.
- **≥3 small companies / teams have publicly adopted as their internal standard.** Sustained use, not weekend trial.
- **Multiple maintained adaptations / forks for specific niches** (e.g., a research-team variant, a regulated-industry variant). CC BY 4.0 enables this; the existence of maintained adaptations proves it's worth doing.
- **Self-development loop has demonstrably evolved the methodology beyond v1.x design.** The autonomous cycle has surfaced patterns the solo maintainer wouldn't have discovered.
- **Cross-pollination: ≥2 patterns originally in this methodology have been adopted by peer methodologies.** Concrete evidence the methodology is generative for the field, not just for adopters.

## What success is NOT

- **Revenue.** CC BY 4.0; no monetization layer. If commercial value emerges (consulting, training, support), it's downstream of the open methodology, not the methodology itself.
- **Star count above some arbitrary high number.** Vanity. 500 stars with 50 real adopters beats 50,000 stars with 50 real adopters.
- **Personal recognition for the maintainer.** Not the point. The methodology should outlive any individual maintainer's attention.
- **Replacing existing methodologies.** Coexistence is the goal. This methodology runs *inside* Scrum, *on top of* Kanban, *complementing* XP. It does not replace SAFe or other enterprise frameworks.
- **Becoming the dominant methodology.** A pluralistic landscape is healthy. This methodology being one of several real options is the success state.

## The compounding mechanism

The vision is sustainable because the methodology is applied to its own development (this `self-development/` folder is that application). Insights from running the methodology on the methodology project surface gaps; those gaps become methodology improvements; the next loop run benefits from the improved methodology. Quality compounds without scaling maintainer hours linearly with adoption.

See [../../methodology/00_README.md](../../methodology/00_README.md) and [../../README.md](../../README.md) for the methodology's own structural details.
