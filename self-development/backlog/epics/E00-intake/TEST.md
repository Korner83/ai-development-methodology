# E00 — Intake — Test scenarios

_Epic-specific acceptance + regression scenarios, per [`03`](../../../../methodology/03_epics.md)._

**A standing epic has no exit criteria**, so there are no acceptance tests here in the usual sense. What it
has instead is a set of properties that must stay true for intake to be worth having — and the whole point
of intake is that a missing charter must not mean a missing gate.

## Properties to protect

Each is checkable against the tree at any time. **From here these are what a reader should verify rather
than take on trust.**

| ID | Property | Status |
|----|----------|--------|
| AT-01 | Every intake item carries the full eight-field frontmatter table — no reduced format | pass — 2026-08-25, 3 items filed |
| AT-02 | Every intake item carries frozen intent on its `Done means:` | pass — 2026-08-25 |
| AT-03 | No intake item closes on a `Test` value the hard rule forbids | pass — BL-0057 closed on `pass` |
| AT-04 | No "lite DoD" exists anywhere; the six gates apply here unchanged | pass — no variant gate is defined in this folder |
| AT-05 | The eviction rule has fired when three open items shared a theme | not-tested — fewer than three open |
| AT-06 | The intake ratio was reported at the semi-annual pass | not-tested — first due 2026-11-25 |

**AT-05 and AT-06 are the two that decide whether this was worth doing**, and neither can be run yet.
Recorded as `not-tested` rather than omitted, because a property nobody can check is how the last audit's
findings survived six releases.

## Regression scenarios to protect

| Area | Scenario | Last verified |
|------|----------|---------------|
| No second format | An intake item is byte-comparable in shape to a cascade item | 2026-08-25 |
| No gate erosion | The DoD referenced from intake is the same `07`, not a variant | 2026-08-25 |
| Cap honesty | `E00`'s WIP-cap exemption stays a *declared deviation*, not a silent re-reading of the rule | 2026-08-25 |
| Publication discipline | Focused mode stays out of `methodology/` until the promotion trigger in [FUTURE.md](FUTURE.md) fires | 2026-08-25 |

The last row is the one most likely to fail, and it fails quietly: the temptation will be to publish the
convention because it now exists and looks tidy. **The trigger is written down so that decision has to be
made against a stated condition rather than a feeling.**
