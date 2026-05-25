# Distribution materials (drafts, staged for maintainer publication)

_Created 2026-05-25 as the loop's output to address the "Adopter discoverability" gap (score 6/10) surfaced by the [first periodic deep-eval](../evaluations/2026-05-25-eval-01.md)._

**These are drafts only.** Per the methodology's own rule ("voice belongs to the human maintainer; AI-authored posts risk both authenticity and trust" — [`templates/AUTONOMOUS_LOOP.md` negative list](../../templates/AUTONOMOUS_LOOP.md)), the autonomous loop never publishes these. The maintainer reviews, edits to their voice, and publishes at their timing.

## Files in this folder

| File | Channel | Maintainer action |
|---|---|---|
| [`SHOW_HN_DRAFT.md`](SHOW_HN_DRAFT.md) | Hacker News "Show HN" post | Edit to maintainer voice; post to https://news.ycombinator.com/submit; choose a Tuesday/Wednesday morning US-time for best visibility. |
| [`AWESOME_LISTS_PR.md`](AWESOME_LISTS_PR.md) | Awesome-lists PR descriptions | Pick one or more target lists; submit PR with the entry text per each list's contributor guidelines. |
| [`BLOG_POST_DRAFT.md`](BLOG_POST_DRAFT.md) | Maintainer's blog / personal channel | Edit substantially to maintainer voice; consider cross-posting to dev.to, Hashnode, LinkedIn. |
| [`DISCUSSIONS_SEEDS.md`](DISCUSSIONS_SEEDS.md) | GitHub Discussions on this repo | Enable Discussions in repo Settings; create the 3 starter threads (FAQ, Show & Tell, Roadmap) using the seed content. |

## Sequence recommendation

1. **Enable GitHub Discussions first** (`DISCUSSIONS_SEEDS.md` — lowest reversibility cost; lowest stakes). Sets up the receive-feedback infrastructure.
2. **Submit awesome-lists PRs second** (`AWESOME_LISTS_PR.md` — moderate reversibility; PRs can be closed). Each merged entry is durable but discoverable through search.
3. **Publish blog post third** (`BLOG_POST_DRAFT.md` — durable; under maintainer's full editorial control on their own channel).
4. **Show HN last** (`SHOW_HN_DRAFT.md` — one-shot; post once + don't repost; comments visible forever). Comes after the other channels so visitors have somewhere to go (Discussions, awesome-list entries, blog post for backstory).

## After publication

- **Update `loop-notes/2026-05-25.md`** with each channel's publication date + initial response data.
- **Triage incoming feedback** via the flow in [`methodology/12_milestone_evaluation.md` "Feedback triage"](../../methodology/12_milestone_evaluation.md#the-feedback-triage-flow). Create `self-development/backlog/FEEDBACK.md` if not yet present.
- **Re-score "Adopter discoverability"** at the next deep-eval (Run 6 cadence). Target: ≥ 7 with ≥ 1 external adopter signal.

## What NOT to publish

- **Anything claiming the methodology is "the best" or "revolutionary".** Per `self-development/brief/03_competitive_landscape.md` — the field is crowded; humility wins.
- **Anything implying batch adoption is the norm.** This is a CC BY 4.0 markdown methodology; adopters fork or copy. No support contract.
- **Anything that overclaims the WayWhisper validation.** The methodology was applied to one real project; "battle-tested in one production project" is the honest framing.
