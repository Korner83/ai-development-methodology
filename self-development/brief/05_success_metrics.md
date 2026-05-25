# Success Metrics

Concrete, observable outcomes at 1-year and 3-year horizons. Vanity metrics excluded.

## 1-year horizon (target: 2027-05-25)

| # | Metric | Target | Why it matters | How to measure |
|---|---|---|---|---|
| 1 | GitHub stars | ≥500 | Baseline signal of adoption interest. Insufficient alone, but needed. | GitHub API; quarterly check. |
| 2 | Referenced public adoption stories | ≥10 | Real adopters publicly say "we use this." Proves the methodology survives the trial. | Maintainer logs; passive search for repo URL mentions. |
| 3 | Substantive forks | ≥3 | Forks with meaningful additions (not patches). Proves the methodology is generative — others can extend usefully. | GitHub API; manual inspection of top forks; "additions" judged by diff content, not LOC. |
| 4 | Accepted upstream contributions | ≥5 | PRs from external contributors that add or refine methodology content. Proves a contributor pipeline is forming. | GitHub PR history. |
| 5 | Self-development cycle releases | ≥2 minor releases via autonomous loop | Demonstrates the cycle works end-to-end. Without this, the "self-improving" claim is theoretical. | CHANGELOG analysis — releases tagged as "via autonomous loop" or with that body language. |
| 6 | Maintainer hours/quarter | ≤40 hours/quarter sustained | Sustainability check. If maintenance exceeds this, the lean-maintainer model is broken. | Maintainer self-log. |

## 3-year horizon (target: 2029-05-25)

| # | Metric | Target | Why it matters | How to measure |
|---|---|---|---|---|
| 7 | Named in AI-coding methodology discussions | Referenced alongside Spec Kit / BMAD / Ralph in ≥5 blog posts, talks, or papers comparing options | Legitimately on the list when people compare. Not necessarily most popular; on the radar. | Search mentions; community lists; conference talk indices. |
| 8 | Public adoption as internal standard | ≥3 small companies / teams publicly adopt as their methodology | Sustained use, not weekend trial. Hard to fake; the team is willing to attach their name to it. | Public statements (engineering blogs, talks, hiring docs). |
| 9 | Maintained adaptations / forks for niches | ≥2 maintained variants (e.g., regulated industry, research teams) | CC BY 4.0 enables adaptation; existence of maintained variants proves the methodology is useful enough to fork-and-maintain. | GitHub fork inspection; "maintained" = commits in last 60 days. |
| 10 | Self-development loop has shifted the methodology | The autonomous cycle has surfaced ≥3 patterns the solo maintainer wouldn't have discovered | Proves the loop is generative, not just executing. | Methodology release attribution; "this came from the cycle" notes in CHANGELOG. |
| 11 | Cross-pollination to peer methodologies | ≥2 patterns originally here have been adopted by peer methodologies | Generative for the field, not just for adopters. The strongest signal of methodology quality. | Peer methodology CHANGELOGs and READMEs; community discussion. |
| 12 | Stars (secondary check) | ≥2,500 | A 3-year baseline if the other metrics are tracking. Not a goal in itself. | GitHub API. |

## What's NOT a metric

- **Revenue.** CC BY 4.0; no monetization. If commercial activity emerges around the methodology (consulting, training), that's downstream, not the methodology's success.
- **Star count above some arbitrary high number.** 500 stars with 50 real adopters > 50,000 stars with 50 real adopters. Stars are a baseline signal, not the goal.
- **Velocity of releases.** Quality and coherence matter more than release frequency. Six releases in a day (which happened on 2026-05-25) is an unusual burst, not a sustainable pace, and not a target.
- **Personal recognition for the maintainer.** Not the point. The methodology should outlive any individual's attention.
- **Followers / subscribers / newsletter signups.** Marketing-flavored metrics. The methodology doesn't have these channels; doesn't need them.
- **Specific feature count.** "We added X new sections this year" is volume, not value.

## Counter-signals (early warning)

Things to watch that mean the methodology is failing, not succeeding:

- **Stars climb but no adoption stories appear.** Means people are bookmarking, not using.
- **Forks appear but never get commits.** Means people are forking-to-try and abandoning.
- **Issues asking "how do I do basic X?"** Means the docs aren't actually clear; the doc-clarity capability layer is underdelivering.
- **Maintainer hours climb past 40/quarter.** Means the lean-maintainer model is breaking; consider what's causing the rise and either fix the methodology or shift to a different maintenance posture.
- **Methodology releases stop happening.** Means the cycle stalled. Worth investigating whether the cycle is the wrong shape or the maintainer is over-extended.
- **External contributions arrive but get bounced back repeatedly.** Means contribution surface isn't clear; consider better CONTRIBUTING.md or different governance.

## Review cadence

- **Quarterly:** check metrics 1, 3, 4, 5, 6 (the easily-quantified ones) plus any counter-signals. Adjust if drift is significant.
- **Semi-annually:** full review tied to the methodology self-evaluation pass (per [`methodology/07_definition_of_done.md`](../../methodology/07_definition_of_done.md)). Includes the metrics review plus a "are these still the right metrics?" sanity check.
- **Annually:** end-of-year review of 1-year-horizon metrics; restate 3-year-horizon targets if context has shifted.

## How metrics interact with the self-development cycle

Metric 5 (self-development cycle releases) and metric 10 (loop has shifted the methodology) are the **leading indicators** for everything else. If the cycle is operational and generative, the other metrics improve as a downstream effect:

- Better methodology → better adoption stories → more stars → more substantive forks → more upstream contributions.
- Stalled cycle → static methodology → adoption stalls → metrics plateau.

The self-development bootstrap (this folder) exists precisely to make the cycle operational. Until Step 4 lands, metrics 5 and 10 are unreachable.
