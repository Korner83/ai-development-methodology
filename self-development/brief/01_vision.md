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

A methodology written natively for mixed-contributor work is the bet this project takes. The structural choices it commits to are documented in [README "Why these particular structural choices"](../../README.md#why-these-particular-structural-choices) — patterns like named anti-patterns, same-format locks for humans + AI agents, DoD coupled to item frontmatter, tier matrix for autonomous loops, periodic deep-eval — each driven by a specific failure mode the maintainer encountered while running mixed-contributor work in practice.

This project fills those gaps without depending on a specific AI vendor, a specific tech stack, or a SaaS platform that might disappear in 18 months.

## What success looks like

### Early signals (within ~12 months)

- **External adoption signal exists.** Stars are a baseline-existence indicator (not the goal — see [05_success_metrics.md "What's NOT"](05_success_metrics.md#what-success-is-not)); the real signal is at least *some* baseline discoverability so adoption is possible at all.
- **Externally-authored adoption stories exist.** At least one blog post, conference talk, podcast mention, or public engineering blog where someone says "we use this and here's how it shaped the project."
- **Forks have commits.** Adopters who have made meaningful additions to the methodology, not just bookmarked-and-forgotten. Forks with substantive additions prove the methodology is generative.
- **A contributor pipeline is forming.** At least one accepted upstream contribution from an external contributor — substantive (not a patch).
- **Self-development loop has shipped methodology improvements.** The cycle has produced methodology releases attributed to its output (not just self-development internal cleanup) — proving the cycle is the methodology's most distinctive claim, not theoretical.

### Sustained signals (multi-year)

- **The methodology appears in field discussions on its own merit.** When people compare AI-coding methodologies, this one comes up because it offers something specific — not because it's the loudest. Whether it comes up at all is the signal; counting mentions invites gaming.
- **Public sustained use.** At least one team or company publicly uses the methodology as their internal standard, and is still using it 12+ months later. Public + sustained beats either alone.
- **Maintained adaptations exist.** CC BY 4.0 enables forking; maintained variants (e.g., for regulated industries, research teams, specific stacks) mean the methodology is useful enough to fork-and-maintain.
- **Self-development loop has demonstrably evolved the methodology.** The autonomous cycle has surfaced patterns the solo maintainer wouldn't have discovered alone.
- **Patterns originally in this methodology have been adopted by other methodologies in the field.** Generative for the field. Strongest possible signal of methodology quality; weakest possible signal of maintainer ego (because by then the maintainer isn't the source any more).

## What success is NOT

- **Revenue.** CC BY 4.0; no monetization layer. If commercial value emerges (consulting, training, support), it's downstream of the open methodology, not the methodology itself.
- **Star count above some arbitrary high number.** Vanity. 500 stars with 50 real adopters beats 50,000 stars with 50 real adopters.
- **Personal recognition for the maintainer.** Not the point. The methodology should outlive any individual maintainer's attention.
- **Replacing existing methodologies.** Coexistence is the goal. This methodology runs *inside* Scrum, *on top of* Kanban, *complementing* XP. It does not replace SAFe or other enterprise frameworks.
- **Becoming the dominant methodology.** A pluralistic landscape is healthy. This methodology being one of several real options is the success state.

## The compounding mechanism

The vision is sustainable because the methodology is applied to its own development (this `self-development/` folder is that application). Insights from running the methodology on the methodology project surface gaps; those gaps become methodology improvements; the next loop run benefits from the improved methodology. Quality compounds without scaling maintainer hours linearly with adoption.

See [../../methodology/00_README.md](../../methodology/00_README.md) and [../../README.md](../../README.md) for the methodology's own structural details.
