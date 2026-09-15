# HUMAN_NEEDED.md

Tasks blocked on human action. Each entry links to the originating BL item. Add an entry when you set `Status: blocked` and the blocker is human-only (not waiting on another agent, not waiting on a dependency that an agent can resolve).

Per the [methodology pattern](../../methodology/04_backlog_items.md#human_neededmd--work-blocked-on-human-agency), this is a **passive registry** — items land here via the normal blocked-item protocol; humans scan when they check in; the autonomous loop does not interact with this file directly.

## Active

### BL-0065 — Review and accept the v1.35.0 documentation update

- **Source:** [E11 backlog](epics/E11-assurance-and-squads/BACKLOG.md#bl-0065--verify-consistency-and-prepare-v1350).
- **Human owner:** repository maintainer.
- **Needed:** arrange independent review of the final proposed tree and record acceptance for E11/BL-0063–0065 after considering [local evidence](epics/E11-assurance-and-squads/TEST.md). The approved plan does not supply the final acceptance verdict.
- **Prepared:** canonical rules, adoption surfaces, examples, and local verification; v1.35.0 remains unreleased.
- **Unblocks:** BL-0065 and E11 closure, then the normal human-controlled release process.
- **Filed:** 2026-09-15.


## Recently unblocked (last 30 days)

- **Publish the distribution drafts** — **closed 2026-08-19 by deciding not to do it.** This was the
  sole entry here from 2026-08-14, and the only thing the
  [first self-evaluation](../evaluations/2026-05-25-eval-01.md) identified as blocking the
  closed-beta milestone: [P5 — Adopter discoverability](../pillars/P5_adopter_discoverability.md)
  scored **6/10**, and under the rubric's *no area averaged away* rule that single score holds the
  verdict at **NOT READY for closed beta**.

  The maintainer deleted the four staged drafts (Show HN, awesome-list PR, blog post, Discussions
  seeds) on the position that **a good project sells itself.** Recorded plainly because it is a
  strategy decision, not a completed task: **the score does not move as a result.** P5 stays at
  6/10, the closed-beta verdict stays NOT READY, and the difference is that the prepared path to
  changing it no longer exists. Adoption now depends entirely on the passive channels already in
  place — GitHub search and topics, the Pages site, and the awesome-list listings recorded in P5's
  current-state section.

  **What would reopen this:** an adopter arriving through a passive channel and giving structured
  feedback closes the gap without any campaign, which is the outcome the decision bets on. A long
  quiet stretch with no arrivals is the counter-evidence, and at that point the question is not
  "republish the drafts" — they are gone — but whether the passive-only position still holds.

## Status

Seeded empty on 2026-05-25 as Step 2 of the self-development bootstrap. One entry has been filed and closed since: the distribution-drafts entry above, closed by decision rather than by action. The registry was empty again as of 2026-08-19; E11 added the active release-review entry on 2026-09-15.

_(Older unblocked items live in their epic's `ARCHIVE.md`.)_
