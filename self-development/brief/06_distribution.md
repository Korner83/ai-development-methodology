# Distribution and Sustainability

How the methodology reaches adopters, and how it stays maintainable long-term without scaling maintainer hours linearly with adoption.

## Distribution channels

### Primary (high signal, low effort)

- **GitHub** (`Korner83/ai-development-methodology`) — canonical source. Where adopters find, read, fork. The repo is the product; everything else routes back to it.
- **GitHub Pages** (`korner83.github.io/ai-development-methodology`) — rendered docs for adopters who prefer browsing over the GitHub UI. Already live as of v1.x.
- **GitHub Discussions** — adopter conversation, "is this approach reasonable for X?" questions, adoption-story sharing. Already enabled; welcome thread seeded.
- **GitHub Releases** — versioned release notes for adopters who pin to versions. Every release has a release page generated from the CHANGELOG entry.
- **Awesome-list submissions** — surfaces in `awesome-*` curated lists where adopters discover methodologies. Two PRs already open (webfuse-com/awesome-claude #238, dontriskit/awesome-ai-software-engineering #8); future submissions when fit is clear.

### Secondary (opportunistic, low frequency)

- **Hacker News** — occasional "Show HN" or comment with the URL when a substantive update lands. Not a regular cadence.
- **X / LinkedIn** — opportunistic posts when there's something substantive to share. Not a content-marketing strategy.
- **Vendor adjacencies** — natural mentions when discussing Claude Code, Cursor, etc. in community channels. Organic, not pursued.
- **Blog posts / podcasts** — if hosts reach out. Not actively pitched.
- **Conference talks** — if invitations arrive. Not actively pitched.

### Out of scope

- **Paid advertising.** Doesn't fit a CC BY 4.0 reference artifact.
- **Email newsletter / mailing list.** Discussions thread serves the same purpose without subscription management.
- **Translation / multi-language versions.** Decided against; browsers auto-translate and drift is the killer.
- **Custom domain (e.g., `methodology.dev`).** github.io subdomain is sufficient.
- **Companion website beyond GitHub Pages.** No marketing landing page beyond the README.

## Sustainability model

### Lean-maintainer commitment

Per [STATUS.md](../../STATUS.md): published as a *reference artifact*, not a *managed project*. Specific commitments:

- **PRs welcome but no SLA.**
- **Issues welcome but not actively triaged.**
- **No roadmap.** The methodology isn't going somewhere; it's already where it's going (and the self-development cycle handles evolution).
- **No support.** Docs are intended to be self-sufficient.
- **No deprecation policy.** Versions, when they happen, are tagged. Old versions stay forever.

**The CC BY 4.0 license is the escape hatch.** If the lean maintenance doesn't work for an adopter, they fork and run their own variant.

### Maintainer hours budget

Target: **≤40 hours per quarter** sustained. This includes:

- Reviewing/merging external PRs.
- Reviewing/responding to Discussions threads.
- Self-development cycle check-ins (between autonomous loop runs).
- Quarterly repo health audit + semi-annual methodology self-evaluation.
- Opportunistic distribution (the secondary channels above).

If hours exceed 40/quarter for two consecutive quarters, the model is breaking. Options:

- Reduce scope (fewer methodology additions, fewer responses).
- Add a co-maintainer (per STATUS.md's "second contributor joins" trigger).
- Adjust the methodology to require less ongoing maintenance (e.g., delete sections that need constant updating).

### Why CC BY 4.0 (not MIT, not GPL, not custom)

- **CC BY 4.0 is built for documentation and creative works**, not code. The methodology is docs; the license matches.
- **Permissive enough for commercial reuse.** Companies can adopt internally, charge for consulting, build paid products on top — all fine, as long as attribution travels.
- **Attribution-only is the lightest viable obligation.** Heavier obligations (e.g., requiring derivative-works distribution) would limit who's willing to adopt.
- **CC is widely recognized** in non-software contexts (academia, education, content creation) where some adopters live.
- **MIT or Apache would also work** but are more code-flavored. CC BY 4.0 signals "this is a documentation artifact."

### When this stops being a personal artifact

Per STATUS.md, the project moves from "reference artifact" to "shared infrastructure" when:

- ≥3 external maintainers have made substantive contributions, AND
- ≥5 publicly-acknowledged adopters reference it in their own work.

At that point: consider community governance (CODE_OF_CONDUCT.md, CONTRIBUTING.md, second maintainer, possibly a steering decision process).

Until then: solo maintenance with the lean commitments above.

## Adopter-facing distribution principles

These shape *how* the methodology reaches adopters:

- **Honest comparison, not chest-thumping.** The "What's similar, what's different" table in the README names alternatives, says where each is strong, says where this differs. Adopters trust honest framing.
- **Discoverable from search.** GitHub topics, awesome-list inclusion, clear repo description. The maintainer doesn't push to top-of-search; the repo earns its visibility.
- **Low-friction trial.** Step 1 of "How to use it" is a 6-line bash block. Adopters can try before they commit.
- **Worked example in repo.** The `self-development/` folder (where this brief lives) is the example — adopters can see the methodology applied to a real project without leaving the repo.
- **No vendor entanglement.** The methodology works with any AI tool; adopters don't have to commit to a vendor by adopting.

## What "shared infrastructure" mode looks like (if reached)

Speculative; only relevant once the triggers above are met. Likely additions:

- `CODE_OF_CONDUCT.md` (Contributor Covenant standard).
- `CONTRIBUTING.md` with PR / review / governance guidance.
- A second maintainer with merge permissions.
- Possibly a `STEERING.md` or similar for decisions affecting backward compatibility.
- Branch protection on main (currently the [documented exception](../../STATUS.md) per STATUS.md applies).

Not adopting these now is deliberate. Each adds maintenance overhead that's only worth paying once the contributor base demands it.

## Marketing posture

In one sentence: **be useful, be honest, be findable. Don't be loud.**

The methodology's value is its content. Marketing it harder than that risks attracting attention that produces churn (people who try, don't fit, complain) without retaining adoption (people who try, fit, stay). The honest-comparison approach in the README is the entire pitch.
