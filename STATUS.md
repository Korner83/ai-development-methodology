# Status

## Maturity

**Battle-tested in one production project.** Generalizability to other projects is a hypothesis, not yet a verified fact.

The methodology has been in active use through:

- Multi-month delivery cycles across multiple epics.
- Concurrent human + AI agent contributors working the same backlog.
- Real Definition-of-Done enforcement that caught bugs before ship.
- Lock-based concurrency control across overlapping sessions.

It works as designed in that one context. Whether the same shape transplants cleanly to a different stack, team, or product category will become clear only as others try it.

## Maintenance commitment

**Lean.** This repo is published as a *reference artifact,* not a *managed project.*

What that means in practice:

- **PRs are welcome but not promised.** If you open one, I'll read it; I cannot commit to a review SLA.
- **Issues are welcome but not actively triaged.** Use them to share experience or flag confusion in the docs. Do not expect a response.
- **No roadmap.** This isn't going somewhere; it's already where it's going.
- **No support.** I cannot help you adapt the methodology to your specific project. The docs are intended to be self-sufficient.
- **No deprecation policy.** Versions, if they happen, will be tagged. Old versions stay forever.

If this approach to maintenance doesn't work for you: **fork freely.** The MIT license exists for exactly this case. You don't need permission to maintain your own fork; you can rename it, restructure it, and adapt it to your needs without involving the upstream.

## Stability

Documents will change as understanding sharpens. Material changes will:

- Increment the relevant doc's version (the methodology itself uses a strategy-doc-style versioning pattern internally; see [01_strategy.md](methodology/01_strategy.md)).
- Preserve old versions where the original made a substantive claim someone may have built on.
- Be summarized in commit messages and (eventually) in a `CHANGELOG.md`.

Forks that need to pin to a specific state should pin to a specific commit hash or a tagged release.

## Feedback

If you've adopted this and learned something — what worked, what didn't, what you adapted — the most valuable thing you can do is **share it.** Blog post, comment, talk at a meetup. Public experience reports help shape future iterations more than issues do.

If you find a factual error or a broken cross-link, an issue or PR is welcome.

For direct contact: **polgarmiklos@gmail.com**. No response SLA, but emails about real adoption experiences are read.

## Contributions

The bar for accepted PRs is high:

- Must preserve the **fully abstract** voice. No project names, no domain references. Generic placeholders only.
- Must preserve the **doc structure** (the same sections, the same cross-link conventions, the same canonical templates).
- Must be **small and surgical.** Massive restructures will be declined; the methodology values incremental sharpening over wholesale rewrites.
- Must include a clear motivation (what is the change *for*?) — not "I think this would be better" but "I tried this and the existing wording caused X to happen."

Most things people want to add or change are better expressed as a **fork** with a clear note in the fork's README explaining what's different and why. The upstream is intentionally narrow.

## Provenance

Extracted from the working practice of a real production project. The docs were written from scratch as a portable, abstract version. The source project's name, domain, technology stack, and specific tooling appear nowhere in the methodology. This was a deliberate constraint at authoring time, not a transformation applied after the fact.
