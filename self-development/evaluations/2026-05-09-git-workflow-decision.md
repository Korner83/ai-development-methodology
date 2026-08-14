# `09_git_workflow.md` — trim-vs-split decision (BL-0011)

**Analysis performed:** 2026-08-14 (against v1.26.0).
**Filename note:** the `2026-05-09` date comes from the path BL-0011's acceptance criteria specify;
it predates the analysis. Kept as specified rather than silently renamed — changing an approved
criterion to match what was built is the [frozen-intent](../../methodology/04_backlog_items.md#frozen-intent--approved-goals-are-human-owned) violation this methodology now names.

## Measured state

| Metric | Charter (E03) | Actual, 2026-08-14 |
|---|---|---|
| Total lines | 986 | **1,026** |
| Soft cap | 1,050 | 1,050 — **98% consumed** |
| Real `##` sections | — | **24** (a naive scan reports 29; five are template headings inside code fences) |
| Mean section length | — | ~43 lines |
| Largest sections | — | Commit message convention (91), Branch naming (81), Release tagging (78), Worktrees (62), Hot-fix (56), Conventional-commit examples (56) |

The doc grew ~40 lines since chartering. **No single section is oversized.** The length comes from
section *count* across a genuinely broad topic, which is the central fact driving this decision.

## Option A — Trim to under 800 lines

**Identified cuts, in descending confidence:**

| Cut | Lines | Confidence | Why it's safe |
|---|---|---|---|
| Delete "Conventional commit examples (copy-paste reference)" (L859–913) | −56 | **High** | Pure duplication. "Commit message convention → Examples" (L196–233) already gives five worked examples with real bodies. The appendix restates the same shapes with placeholders. |
| Delete "PR body skeleton" (L835–856) | −22 | **High** | Pure duplication. "PR discipline → PR body" (L304–320) already shows the identical skeleton. |
| Fold "Worktree command reference" (L915–936) into the Worktrees section | −20 | **High** | Overlaps "Worktrees for parallel agents" (L469–505). Only two commands are unique (`add -b`, `remove --force`); both fit inline. |
| Merge "Destructive command discipline" with the ✗ rows of "the affirmative list" | −25 | **Medium-high** | Six operations appear in both tables (`push --force`, `reset --hard`, `restore`, `clean`, `branch -D`, `filter-branch`). One table with an autonomy column carries both meanings without the split. |
| Trim "Operational work (deploys, pipelines, runbooks)" (L939–982) to its hard rule + a pointer | −30 | **Medium** | Weakest topical fit in a *git workflow* doc — it covers deploys, pipelines, monitoring, and runbooks. The transferable content is the hard rule and the pattern table. |
| Prose density pass across remaining sections (~10%) | −50 | **Medium** | Stacked caveats and repeated "why this matters" framing. Risk: this is where the doc's value lives; cuts must remove restatement, not reasoning. |
| **Total** | **≈ −203** | | **1,026 → ~823** |

To reach **under 800** the prose pass has to yield ~75 rather than ~50 — achievable, but it is the
least certain line item and the one that can damage the doc.

**Pros:** no inbound link breakage; no structural commitment; the "fourteen short docs" identity in
`README.md` survives; ~120 of the cut lines are outright duplication that costs nothing to lose;
easy to partially revert.
**Cons:** the last ~75 lines must come from prose, which is where the reasoning lives; the doc
remains the longest in the corpus, so this buys headroom rather than solving the category.

## Option B — Split into 2–3 docs

A clean topical cleave exists:

| Doc | Sections | Est. lines |
|---|---|---|
| `09a` — Daily flow | branch protection, branch naming (+patch branches), commit cadence, commit messages, pre-commit hooks, never-amend, PR discipline, merge strategy, conflict resolution | ~370 |
| `09b` — Releases and operations | release tagging + SemVer, hot-fix workflow, production deploys, operational work | ~230 |
| `09c` — Agents and parallel work | lock files, worktrees, destructive commands, the affirmative list, audit trail | ~240 |

Each lands well under 700.

**Pros:** preserves every line; each doc is individually scannable; the three groups are genuinely
distinct audiences (daily contributor / release manager / agent-safety reviewer).
**Cons, and they are the deciding factor:**

- **It is a T3 restructure**, not a T2 edit — new docs, changed doc count, changed identity. Per the tier matrix that is human-only and a MAJOR-flavoured change for anyone who pinned to a version.
- **`README.md` claims "Fourteen short docs"** in its opening paragraph, and the numbering 00–13 is part of how the corpus is navigated. `09a/09b/09c` breaks both.
- **Inbound anchor churn is large**: `09` is linked from `00`, `07`, `10`, `12`, both templates, the skill, `CHEATSHEET.md`, and several `self-development/` files — many by section anchor, which would move across files.
- **The topic is cohesive.** Branch protection, the affirmative list, and hot-fixes all answer "how does work move through git safely here?" Splitting scatters the answer.

## Decision: **TRIM**

Committing to Option A, for three reasons:

1. **~120 of the needed lines are pure duplication** — three appendix sections that restate content
   already given inline, better, earlier in the same doc. Removing them is a strict improvement
   independent of any line target.
2. **The length diagnosis doesn't support splitting.** A split is the right answer when sections are
   individually bloated or the topic is really two topics. Here the mean section is 43 lines and the
   topic is one. The doc is long because git safety in a mixed human/AI project has 24 genuine
   facets.
3. **Cost asymmetry.** Trimming risks over-cutting prose, which is visible in review and cheap to
   restore. Splitting spends a T3 restructure, breaks the corpus identity claim, and scatters
   anchors across three files — and would have to be undone wholesale if it read worse.

**Scope for BL-0012:** execute the six cuts above in that order, stopping when the doc is under 800
lines. If the four high/medium-high cuts (≈ −123) plus a disciplined prose pass cannot reach 800
without cutting reasoning, **stop at the lowest honest number and report it** rather than stripping
the "why" to hit a target — the target serves the doc, not the reverse.

**Explicitly not in scope:** renumbering, splitting, or moving sections to other docs; adding new
git-workflow content.

---

# Execution log (BL-0012)

**Result: 1,026 → 798 lines (−228, −22%).** Under the 800-line exit criterion. Sections 24 → 20.
Diff: 50 insertions, 277 deletions.

## What was removed, and why each removal is safe

| # | Removed | Lines | Where the content still lives |
|---|---|---|---|
| 1 | **"Conventional commit examples (copy-paste reference)"** — whole section | −56 | "Commit message convention → Examples" gives the same shapes as *worked* examples with real bodies. The `revert:` template was the only shape without an inline twin; its rule survives in the Types table ("Reverts a prior commit. Body must name the reverted commit."). |
| 2 | **"PR body skeleton"** — whole section | −22 | "PR discipline → PR body" shows the identical skeleton. |
| 3 | **"Worktree command reference"** — whole section | −20 | Folded into "Worktrees → Command reference", which now carries all six commands including the two that were unique to the appendix (`add -b`, `remove --force`). |
| 4 | **"Destructive command discipline"** merged into the affirmative list | −40 | One "operation table" with ✓/⚠/✗. Every destructive command kept its irreversibility note; the six operations that appeared in both tables now appear once. The rules and recovery guidance became "Handling the ✗ rows" and "Recovery when damage is done". |
| 5 | **Operational work** — backlog/epics/not-specified subsections condensed | −25 | Two paragraphs. The pattern table and the hard rule — the transferable parts — are untouched. |
| 6 | **Prose density pass** — branch-name examples, two commit examples, PR summary/test-plan subsections, merge-strategy exceptions, release pushing + notes, audit-trail bullets, lock-file agent bullets | −65 | Restatements collapsed to sentences. No rule, table, or reasoning removed — only the second telling of it. |

## Deliberate non-removals

- **"Common mistakes around git workflow"** — several rows restate rules stated above. Kept: the
  mistake→fix table is a corpus-wide convention present in every methodology doc, and its value is
  precisely that it repeats the rule in failure form.
- **The Types table, the operation table, the pattern set, the SemVer table** — all reference
  surfaces, all kept whole.
- **Every "why this matters" that carries reasoning** — the trim targeted second tellings, not
  first ones. Where a cut would have removed the *reason* a rule exists, it was skipped.

## Anchor repairs (BL-0013)

Merging two sections renamed one anchor. Three inbound links updated:

- `methodology/11_human_roles.md` (decision-ownership matrix "Pairs with" note)
- `self-development/AUTONOMOUS_LOOP.md` ×2 (Constraint 3, and the negative-list row on history rewrites)

`#destructive-command-discipline` and `#what-ai-agents-can-and-cant-do-in-git--the-affirmative-list`
no longer resolve anywhere; both now point at `#what-ai-agents-can-and-cant-do-in-git--the-operation-table`.
Repo-wide anchor check across all 86 tracked markdown files: **zero broken anchors.** 85 inbound
references to `09_git_workflow.md` verified.

One reference was deliberately **not** updated: `self-development/evaluations/2026-05-first-pass.md`
cites the affirmative list by name and by line number. It is a dated historical eval; rewriting it
would falsify what that eval actually examined.

---

# Closure note (BL-0014) — clarity assessment

Comparing the post-trim doc to the v1.6.0 baseline named in the E03 charter:

| Measure | Baseline (v1.6.0) | At analysis (v1.26.0) | After trim | Change |
|---|---|---|---|---|
| Total lines | 986 | 1,026 | **798** | −19% vs baseline, −22% vs analysis |
| `##` sections | 24 | 24 | **20** | −4 (all four were duplicate appendices) |
| Mean section length | ~41 | ~43 | **~40** | flat |
| Longest section | 91 | 91 | **81** | −11% |
| Longest unbroken prose stretch | ~7 lines | ~7 lines | **~6 lines** | flat |
| Share of doc that is reference tables | — | — | ~22% | unchanged in absolute terms |

**Assessment.** The doc is meaningfully shorter without being thinner. The mean section length is
flat, which is the key signal: the reduction came from deleting *whole duplicate sections* and
collapsing *second tellings*, not from thinning sections uniformly. A uniform thinning would have
shown up as a falling mean and a falling longest-section figure — instead the reference tables that
carry the doc's load are all intact at full size.

The one structural improvement beyond length: **destructive operations now have a single home.**
Before, an agent had to consult a negative list and an affirmative list that disagreed on six
operations by omission. Now one table answers "may I run this?" for every operation in the doc.

**Headroom restored:** 798 of a 1,050 soft cap — 24% headroom, from 2%. At the corpus's historical
growth rate for this doc (~40 lines per two releases) that is roughly six releases of runway before
the question returns.

**What the trim did not solve:** `09` remains the longest doc in the corpus and the topic remains
broad. If it approaches the cap again, the split analysis in Option B above stands ready — and the
next time, the duplication that made trimming easy this round will no longer be available.
