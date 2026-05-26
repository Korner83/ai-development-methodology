# Success indicators

How the maintainer will know this methodology is working — without setting public hostages to fortune (specific star counts, company counts, competitor-ranking targets). Qualitative signals + one operational rule that other docs cite.

## Early signals (within ~12 months)

Things to look for in the first year. Not pass/fail targets — directional indicators.

- **External adoption exists, not just stars.** Stars are a weak signal; people bookmark methodologies they never use. The real signal is *at least one* externally-authored adoption story — a blog post, a forked repo with substantial additions, a thread on Discussions where someone says "I tried this on project X and Y happened."
- **The methodology survives non-author use.** Someone other than the maintainer applies it to a project the maintainer didn't write, and the experience produces feedback that's specific (not just "neat idea"). Specificity = the methodology was actually tested.
- **Forks have commits.** Forks that exist but never get a commit mean people are forking-to-try and abandoning. Forks with substantive additions (new templates, additional rubric areas, domain-specific adaptations) mean the methodology is generative.
- **Self-development cycle has shipped methodology improvements.** The cycle is the methodology's most distinctive claim; either it produces real methodology releases (not just self-development cleanup) or the claim is theoretical. Tracked in CHANGELOG via release attribution notes.

## Sustained signals (multi-year)

If the methodology is alive years from now:

- **Appears in field discussions on its own merit.** When people compare AI-coding methodologies, this one comes up because it offers something specific — not because it's the loudest. (Whether it comes up at all is the signal; counting mentions invites gaming.)
- **Public sustained use.** At least one team or company publicly uses it as their internal standard, and is still using it 12+ months later. Public + sustained beats either alone.
- **Maintained adaptations exist.** CC BY 4.0 enables forking; maintained variants (e.g., for regulated industries, research teams, specific stacks) mean the methodology is useful enough to fork-and-maintain, not just bookmark.
- **Patterns from this methodology appear in peer methodologies.** Generative for the field. Strongest possible signal of methodology quality; weakest possible signal of maintainer ego (because by then the maintainer isn't the source any more).

## What's NOT a success metric

- **Revenue.** CC BY 4.0; no monetization. Commercial activity that emerges around the methodology (consulting, training) is downstream, not the methodology's success.
- **Star counts above any specific number.** A small adoption base of teams that actually use the methodology beats a large bookmarking base that doesn't. Stars are a baseline-existence signal, not a goal.
- **Release velocity.** Quality and coherence matter more than frequency. Six releases in a day (which happened on 2026-05-25) is an unusual burst, not a sustainable cadence, and not a target.
- **Personal recognition for the maintainer.** Not the point. The methodology should outlive any individual's attention.
- **Followers / subscribers / newsletter signups.** Marketing-flavored metrics. The methodology doesn't have these channels; doesn't need them.
- **Specific feature count.** "We added X new sections this year" is volume, not value.
- **Comparison-with-competitors framing** as a target ("named alongside X, Y, Z"). Adopters who care will compare on their own time; the methodology's job is to be a good methodology, not to win a ranking.

## Counter-signals (early warning)

Things that mean the methodology is failing, not succeeding:

- **Stars climb but no adoption stories appear.** People bookmark, don't use.
- **Forks appear but never get commits.** People fork to try and abandon.
- **Issues asking "how do I do basic X?"** The docs aren't clear; doc-clarity capability is underdelivering.
- **Maintainer maintenance load grows past sustainable.** The lean-maintainer model is breaking — investigate cause and either fix the methodology or shift maintenance posture.
- **Methodology releases stop happening.** The cycle stalled — investigate whether the cycle is the wrong shape or the maintainer is over-extended.
- **External contributions arrive but get bounced back repeatedly.** Contribution surface isn't clear — consider better CONTRIBUTING.md or different governance.

## The one operational rule

**Maintainer time stays sustainable.** The methodology assumes a single solo maintainer can run it indefinitely — if maintenance load grows past what one person sustains in normal life, the model is broken. Specific budget is the maintainer's call (it's their time); the rule is qualitative: *if maintaining this methodology starts to feel like a second job, something in the methodology or the maintenance posture has to change.*

This is the one quantitative rule that other docs cite (P8 — Maintenance sustainability; strategy plan exit criteria). It's an operational budget, not a vanity metric — the difference being that exceeding it isn't a failure, it's a signal to investigate cause.

## The leading-indicator pattern

Of the signals above, the **self-development cycle's health** is the leading indicator for everything else:

- Healthy cycle → methodology improves at loop velocity → adopters experience an improving artifact → adoption stories, forks, sustained use follow as downstream effects.
- Stalled cycle → static methodology → adoption stalls → all other signals plateau.

The cycle is what was bootstrapped in v1.7.0 through v1.11.0 and operationally validated in v1.14.0+ (first end-to-end self-improvement run). If the cycle stops producing methodology releases, that's the first place to investigate when other signals slow.

## Review cadence

- **Quarterly:** check the early signals + counter-signals; investigate any drift.
- **Semi-annually:** tied to the methodology self-evaluation pass (per [`methodology/07_definition_of_done.md`](../../methodology/07_definition_of_done.md)). Includes a "are these still the right indicators?" sanity check.
- **Annually:** review of the sustained-signal trajectory; restate qualitative targets if the project's context has shifted.
