# Status

## Maturity

**Battle-tested in one production project.** Generalizability to other projects is a hypothesis, not yet a verified fact.

The methodology has been in active use through:

- Multi-month delivery cycles across multiple epics.
- Concurrent human + AI agent contributors working the same backlog.
- Real Definition-of-Done enforcement that caught bugs before ship.
- Lock-based concurrency control across overlapping sessions — in its **cooperative-signalling** form. What was exercised is announce-and-detect, not enforced mutual exclusion; see [`05`](methodology/05_locks_and_parallel_work.md#what-the-lock-does-and-does-not-guarantee). The stronger shared-ref protocol has not been exercised in production by anyone.

It works as designed in that one context. Whether the same shape transplants cleanly to a different stack, team, or product category will become clear only as others try it.

**Second instance: the methodology applied to itself.** [`self-development/`](self-development/) runs this repo's own development under these rules — strategy, nine pillars, chartered epics, locked items, DoD gates, an autonomous loop with tiered autonomy over the docs it edits, and a semi-annual self-evaluation. It is a real instance, but a docs-only one; it exercises the planning, review, and memory disciplines far harder than it exercises the UI-verification and testing disciplines.

**Honest current state** (v1.34.0): the [first self-evaluation](self-development/evaluations/2026-05-25-eval-01.md) scored the project **8.11 average, minimum 6** and returned **NOT READY for closed beta** — one area (adopter discoverability) sits below the rubric's minimum, and under the *no area averaged away* rule that single score decides the verdict. The blocker is not a doc gap. The eval named it "zero external promotion has happened," which was **already inaccurate when written** — [P5](self-development/pillars/P5_adopter_discoverability.md) records 13 GitHub topics, a live Pages site, and two awesome-list submissions. The accurate statement is that no *active campaign* has run, and as of 2026-08-19 **none is planned**: the staged distribution drafts were deleted by maintainer decision, on the position that a good project sells itself. The score and the verdict stand; what was removed is the prepared path to changing them, not the gap. That eval also flags its own weakness: it was conducted by the session that authored the release under review, so its scoring is biased toward charity.

## Maintenance commitment

**Lean.** This repo is published as a *reference artifact,* not a *managed project.*

What that means in practice:

- **PRs are welcome but not promised.** If you open one, I'll read it; I cannot commit to a review SLA.
- **Issues are welcome but not actively triaged.** Use them to share experience or flag confusion in the docs. Do not expect a response.
- **No roadmap.** This isn't going somewhere; it's already where it's going.
- **No support.** I cannot help you adapt the methodology to your specific project. The docs are intended to be self-sufficient.
- **No deprecation policy.** Versions, if they happen, will be tagged. Old versions stay forever.

If this approach to maintenance doesn't work for you: **fork freely.** The CC BY 4.0 license exists for exactly this case. You don't need permission to maintain your own fork; you can rename it, restructure it, and adapt it to your needs without involving the upstream — just keep the attribution.

## Workflow: PR-only (the direct-to-main exception has been retired)

**Current practice:** this repo follows the methodology's [09_git_workflow.md](methodology/09_git_workflow.md) rule in full. Every change lands on `main` via a feature branch and a PR — see PRs #13 onward, including every versioned methodology release since v1.19.0.

The exception below applied to this repo's early life and is **retired**, on its own stated trigger: independent AI sessions now work in this repo, which is the second-contributor condition the exception named. The original text is preserved rather than deleted, because it documents a decision someone may have read and copied.

> [!IMPORTANT]
> **Superseded.** The section below described this repo's practice until the PR-only flow was adopted. It is kept for lineage; it no longer describes how this repo works.

### ~~Workflow exception: this repo uses direct-to-main~~ (historical)

The methodology's own [09_git_workflow.md](methodology/09_git_workflow.md) requires PR-only merges to the trunk and forbids direct commits. **This repo deliberately doesn't follow that rule** — every commit here lands directly on `main` without a feature branch or PR.

Why the exception: this repo is solo-maintained. With one human + a paired AI session working the same branch, a PR-self-review adds no value:

- It doesn't add a second human reviewer.
- It doesn't trigger CI gates that aren't already running locally.
- It adds round-trip delay between authoring and shipping.

The methodology's PR-only rule exists for **multi-contributor projects** where the PR is the artifact that brings independent eyes to a change. With a single contributor pairing with their own AI, the rule's reason for existing isn't present.

**Trigger for revisiting:** when a second contributor (human or independent AI session) starts working in this repo, the exception ends. Branch protection gets enabled, feature-branch + PR flow gets adopted, the methodology's rule applies in full.

This is the methodology's own [authority hierarchy](methodology/00_README.md#authority-across-the-methodology) at work: explicit user direction can override a general rule for a specific scope when the deviation is documented and the rationale is sound. The failure mode the rule guards against ("the trunk breaks because someone pushed a bad commit with nobody watching") is mitigated here by working tree size: one contributor, small focused changes, immediate post-push verification.

Don't take this as license to skip PRs on multi-contributor projects. It's not. The exception is narrow.

## Stability

Documents will change as understanding sharpens. Material changes will:

- Increment the methodology version (semantic-ish: a new or changed convention is a minor bump, a correction is a patch).
- Preserve old versions where the original made a substantive claim someone may have built on.
- Be summarized in [`CHANGELOG.md`](CHANGELOG.md), which is the single source of truth for what changed and why. Each release entry names the docs touched and, for landscape-informed additions, where the idea came from.

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
