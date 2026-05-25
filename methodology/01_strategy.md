# 01 — Strategy

> **Purpose:** explain how to capture and maintain long-term product strategy as a set of versioned documents. Strategy answers *why* the product exists and *what* the business outcomes are; the rest of the methodology answers *how* the team gets there.

Strategy lives in a dedicated folder, organized as a master plan plus numbered supporting docs. Each doc is a snapshot, versioned (`vN`), and updated on cadence or on metric breach — never overwritten silently.

---

## What strategy docs are for

Strategy docs answer questions that pillars, epics, and items cannot:

- *Why does this product exist?*
- *Who is it for?*
- *How does it make money?*
- *What is the market — who else is in it, and where do we sit?*
- *What is the rollout sequence — phase by phase, who do we serve next?*
- *What are the headline numbers we are trying to hit, and when?*
- *What stops us from getting there?* (legal, talent, infrastructure, competition)
- *When do we change course?*

These are decisions that bind years of work. They cannot live in a backlog item — items deliver against strategy; they do not define it.

### Three layers of "how"

The methodology distinguishes three levels of "how":

| Layer | What it answers | Where it lives |
|-------|-----------------|----------------|
| Strategy | Why the product exists. Business model. Market positioning. Headline outcomes per phase. | `docs/strategy/` |
| Pillars | The product-level capability layers required to deliver the strategy. | `docs/pillars/` (see [02_pillars.md](02_pillars.md)) |
| Epics & Items | The time-boxed delivery work that advances pillars. | `backlog/epics/` (see [03_epics.md](03_epics.md), [04_backlog_items.md](04_backlog_items.md)) |

Strategy is the *why* and the *business how.* Pillars are the *product how.* Epics and items are the *delivery how.*

If a doc tries to be more than one of these, it ends up being none of them well. Keep them separate. Cross-link instead of merge.

---

## The master plan pattern

A single document anchors the strategy folder: the master plan. It is the entry point for anyone — new contributor, investor, AI agent, future-self — trying to understand the project's long-term direction.

### What the master plan contains

The master plan is short on purpose. It is not the place for deep analysis. It is the index plus the headline narrative. Detailed analysis lives in the supporting research docs.

Required sections:

1. **Vision** — one or two sentences. The world this product creates. Phrased as a future state, not a feature list. ("Become the [analog from a different category] for [our category]." is a common, useful pattern — it sets ambition without committing to specific implementation.)
2. **Phases** — the rollout sequence, numbered (Phase 0, 1, 2, ...). Each phase has its own subsection with: target audience, headline metric targets, budget envelope, team shape, exit criteria.
3. **Document index** — a table listing every supporting strategy doc with a one-line purpose. Updated whenever a doc is added.
4. **Re-evaluation protocol** — see below.
5. **Version history** — table at the end.

That is the entire required structure. Resist adding more. Detail goes in the supporting docs.

### Why phases (not deadlines)

Phases are defined by who you serve and what you must prove, not by calendar dates. "Phase 2 begins when we have N active users and a confirmed second cohort" is a better gate than "Phase 2 begins on October 1." Calendar-based phases pressure the team to declare phases done that are not done. Outcome-based phases let the work finish properly.

Each phase carries headline metrics, not feature lists. The metrics are how you know the phase is done; the features are how you got there. Feature inventories live in supporting docs (typically a "feature roadmap" doc) or in the backlog itself.

### Vision phrasing

The vision lives at the top of the master plan. Two patterns that work:

- **The analog.** "Become the [X] for [Y]." Borrows a recognizable shape from a different category to set ambition. Works when the analog is famous and the category is clear.
- **The future state.** "By [phase N], every [user role] in [region] will [outcome]." Concrete. Falsifiable. Inviting comparison to current state.

Either works. Both are short enough to remember. A vision longer than two sentences is too long.

---

## Supporting research docs

Each strategic concern gets its own numbered doc. Numbering is for reading order and stable references. The set is the strategy; the master plan is the entrance.

A common set:

| # | Doc | What it covers |
|---|-----|----------------|
| 00 | Master plan | Vision, phases, doc index, re-evaluation, version history. |
| 01 | Market research | Who is in this market. Size of the opportunity. Tailwinds, headwinds. |
| 02 | Differentiation | What makes this product distinct. Defensibility. Moats. |
| 03 | User needs | The problems the product solves. Jobs-to-be-done framing. Validation plan. |
| 04 | Business model | How revenue happens. Unit economics. Cost structure. |
| 05 | Marketing and sales | How users find the product. Channels per phase. Messaging philosophy. |
| 06 | Infrastructure and operations | Hosting, deployment, CI/CD, monitoring, scaling, on-call. |
| 07 | Team and roles | Hiring plan. Org shape per phase. Role definitions. |
| 08 | Legal, licensing, and privacy | Legal structure. Data protection. Content licensing. Liability. |
| 09 | Risk register | What could stop us. Likelihood and impact. Mitigations. |
| 10 | Feature roadmap | What ships per phase, at a coarse level. Detailed planning lives in the backlog. |
| 11+ | Project-specific | Any concern that does not fit the above. Pricing, expansion, content protection, partnership strategy, etc. |

The list above is a starting point. Add docs as concerns become important enough to warrant their own page. Remove docs that turn out to be unused — but archive, do not delete (see versioning below).

Each supporting doc is independent. You should be able to read any one without having read the others, given the master plan's framing. Cross-link where the docs reference each other; do not duplicate.

---

## Required sections in every strategy doc

Every doc in the strategy folder follows the same skeleton. Predictable structure makes the set readable and reviewable.

### The skeleton

```markdown
# [Topic title] [vN]

> **Vision / Goal:** <one-sentence focus for this doc>
> **Last updated:** YYYY-MM-DD
> **Version:** N

## 1. <Section>

<Tables or short prose. Tables preferred.>

### 1.1 <Subsection>

| Column A | Column B | Column C |
|----------|----------|----------|
| ... | ... | ... |

## 2. <Section>

...

## Re-evaluation protocol

<How to know this doc is out of date. What to measure. Cadence.>

## Version history

| Version | Date | Author | Summary of change |
|---------|------|--------|-------------------|
| v1 | YYYY-MM-DD | <name> | Initial. |
```

### Conventions

- **Tables, not prose.** A 4-column table comparing competitors is more useful than three paragraphs describing each. A phase-budget table is more useful than a budget paragraph. Reach for tables whenever you have a list of items with structured attributes.
- **Specific numbers, not adjectives.** "Phase 2 targets 5,000–10,000 active users with 3–5% conversion to paid" is useful. "Phase 2 targets growth in users and conversion" is not.
- **Cross-link to pillars and epics.** Every strategy doc should reference the pillars or epics that operationalize it. If a strategy doc cannot point at the work that delivers it, the work is missing or the strategy is unactionable.
- **Date everything.** Dates make staleness visible. A strategy doc from two years ago without a recent update should look two years old.

### The vision/goal line

Every supporting doc opens with a one-sentence vision or goal *for that doc.* This is not the product vision (that lives in the master plan). It is the focus of *this specific document.* Examples:

- For a market research doc: "Quantify the addressable opportunity and map the active competitive landscape."
- For a business model doc: "Define how revenue happens, at what unit economics, and under what cost structure."
- For a risk doc: "Enumerate the failure modes that could end the project and the mitigations we will run."

If you cannot write the one-sentence goal, the doc lacks focus. Find the focus before writing the body.

---

## Phase-based roadmap

Each phase in the master plan is a stable contract about *who we serve next* and *what we must prove before moving on.*

### Anatomy of a phase

| Element | What goes here |
|---------|----------------|
| Number | Phase 0, 1, 2, ... |
| Name | Short, descriptive ("private beta", "limited launch", "expansion"). |
| Target audience | Who specifically. Not "everyone" — a named cohort. |
| Headline metrics | Two to four numbers. Active users, retention, revenue, conversion — pick the ones that matter at this phase. |
| Budget envelope | Coarse: spend over the phase, not month-by-month. |
| Team shape | Roles you need. Sizes optional. |
| Exit criteria | Specific, falsifiable conditions that mean "move to next phase." |
| Risks specific to this phase | The 2–3 things most likely to stall progress here. |

### Sample phase entry (template)

```markdown
### Phase N — <Phase name>

**Target audience:** <Specific cohort. Numbers if known.>

**Headline metrics:**
- <Metric 1>: target <value> by end of phase.
- <Metric 2>: target <value> by end of phase.
- <Metric 3>: target <value> by end of phase.

**Budget envelope:** <Total spend over the phase.>

**Team shape:** <Roles needed. Hire-by dates if applicable.>

**Exit criteria (move to Phase N+1 when all true):**
- [ ] <Specific, falsifiable condition>
- [ ] <Specific, falsifiable condition>
- [ ] <Specific, falsifiable condition>

**Phase-specific risks:**
- <Risk 1>
- <Risk 2>
```

### What not to put in a phase

- **Feature lists.** Features are the *means* to hit phase metrics. They live in the backlog (and in the feature roadmap supporting doc, at a coarse level). The phase entry is about outcomes.
- **Detailed schedules.** Phases are gated by outcomes, not by dates. Internal timelines for individual epics live in epic charters and item effort estimates.
- **Cross-phase dependencies.** If Phase N depends on something completed in Phase N+1, the phases are wrongly ordered. Reorder them.

---

## Re-evaluation protocol

Strategy goes stale. A market shifts. A metric breaches. A risk that was theoretical becomes real. Without a protocol to revisit the strategy, the docs become wishful artifacts that nobody trusts.

Every strategy doc — including the master plan — has a Re-evaluation Protocol section. It defines:

1. **When to revisit.** Cadence (e.g., quarterly), or trigger conditions (e.g., "if churn exceeds X for two consecutive months").
2. **What to measure.** The specific numbers or facts to gather before deciding.
3. **The four-step loop.** Always the same:

### The four-step loop

```
1. Measure.   Pull actuals against the targets. Note variance.
2. Diagnose.  Identify why variance exists. Distinguish bad luck from
              wrong strategy. Distinguish "we did not execute" from "the
              plan was wrong."
3. Decide.    Pivot or persevere. Explicitly. In writing.
4. Update.    If you persevered, note it in the version history with no
              version bump. If you pivoted, increment the version. Update
              the affected sections. Preserve the old version (see below).
```

### When to pivot vs. persevere

Pivot when:
- The market signal contradicts the strategy and the contradiction is sustained (not a single quarter's noise).
- A core assumption was tested and disproved.
- A risk on the register has materialized and changed the game.

Persevere when:
- Execution lagged the plan but the plan is still right.
- A metric breached because of identifiable, fixable execution issues.
- The data is too noisy to tell yet — and you write down what you are waiting to see.

Either answer is fine. *Not deciding* is the failure mode. The protocol forces a decision; the version history records what was decided and why.

### Re-evaluation checklist

Paste into your strategy docs verbatim:

```markdown
## Re-evaluation protocol

**Cadence:** <quarterly | monthly | on metric breach>
**Triggers:** <list specific conditions that force an early review>

When re-evaluating:

- [ ] Pull actuals against every target in this doc.
- [ ] Note variance — both directions. Outperformance is also signal.
- [ ] Diagnose causes. Separate bad luck, bad execution, and wrong plan.
- [ ] Decide: pivot or persevere. Write the decision down.
- [ ] If pivoting: increment version. Update affected sections. Preserve
      old version as `<doc>_vN.md` for audit.
- [ ] If persevering: append a row to the version history noting "no
      changes after re-evaluation on YYYY-MM-DD" with rationale.
- [ ] Update cross-linked pillars and epics if their work changes.
```

---

## Versioning

Strategy docs are *snapshots,* not living documents. The pillars are living (see [02_pillars.md](02_pillars.md)). The strategy is dated and versioned.

### Versioning rules

- Every strategy doc carries `vN` in the title and a "Version" line at the top.
- Minor updates (fix a typo, add a row to the document index, append to version history) keep the same version.
- Material updates (change a phase target, change the business model, change the risk register) increment the version. Old version archived.

### Archiving an old version

When incrementing from `v1` to `v2`:

1. Copy the existing `<topic>_v1.md` to a `_archive/` subfolder. Do not delete.
2. Update the live `<topic>.md` (or `<topic>_v2.md` — naming convention chosen per project; stay consistent).
3. Add a row to the version history table summarizing what changed and why.

The old version stays accessible because future contributors will sometimes need to understand *why* a decision was made under the old plan. Deleting the old version destroys that context.

### Version history table

Every strategy doc ends with this table. It is the audit trail.

```markdown
## Version history

| Version | Date       | Author       | Summary of change                                  |
|---------|------------|--------------|----------------------------------------------------|
| v3      | YYYY-MM-DD | <name>       | Pivoted target audience based on Phase 2 retention. |
| v2      | YYYY-MM-DD | <name>       | Increased Phase 1 budget envelope after hiring delay. |
| v1      | YYYY-MM-DD | <name>       | Initial.                                            |
```

Rows are oldest-at-bottom so the most recent change is the first thing the reader sees.

---

## Indexing

The master plan contains a Document Index — a table listing every supporting strategy doc with a one-line purpose. This is the navigation surface for the strategy folder.

### Document index template

```markdown
## Document index

| #  | Doc                                  | Purpose (one line)                                              |
|----|--------------------------------------|-----------------------------------------------------------------|
| 01 | [Market research](01_market.md)      | Quantify the opportunity and map the competitive landscape.     |
| 02 | [Differentiation](02_diff.md)        | Define what makes the product distinct and defensible.          |
| 03 | [User needs](03_users.md)            | Capture the problems we solve and how we will validate them.    |
| 04 | [Business model](04_business.md)     | Revenue mechanics, unit economics, cost structure.              |
| 05 | [Marketing and sales](05_marketing.md) | Channels, messaging, GTM by phase.                            |
| 06 | [Infrastructure](06_infra.md)        | Hosting, CI/CD, monitoring, scaling, on-call.                   |
| 07 | [Team and roles](07_team.md)         | Hiring plan and org shape per phase.                            |
| 08 | [Legal and licensing](08_legal.md)   | Legal structure, data protection, content licensing.            |
| 09 | [Risk register](09_risk.md)          | Failure modes, likelihoods, mitigations.                        |
| 10 | [Feature roadmap](10_roadmap.md)     | Coarse feature schedule per phase.                              |
```

### Keeping the index honest

- Every doc in `docs/strategy/` has an index entry. If it is not in the index, it does not exist.
- Adding a new strategy doc updates the index in the same change.
- If a doc is archived to `_archive/`, the index entry moves with it (the link points at the archive path) or the entry is removed and noted in the version history.

A stale index is worse than no index. Treat it as a high-trust artifact.

---

## Master plan skeleton (full template)

Paste this as the starting point for `00_master_plan.md`:

```markdown
# Strategy — Master Plan [v1]

> **Vision:** <one or two sentences. The world this product creates.>
> **Last updated:** YYYY-MM-DD
> **Version:** 1

## 1. Vision

<One or two paragraphs expanding the vision. Why this product. Why now.>

## 2. Phases

### Phase 0 — <Name>
<Target audience, headline metrics, budget, team, exit criteria, risks.>

### Phase 1 — <Name>
<...>

### Phase 2 — <Name>
<...>

(... as many as needed)

## 3. Document index

| #  | Doc | Purpose |
|----|-----|---------|
| 01 | [Market research](01_market.md) | ... |
| ... | ... | ... |

## 4. Re-evaluation protocol

**Cadence:** <quarterly>
**Triggers:** <list specific conditions>

When re-evaluating:
- [ ] Pull actuals.
- [ ] Note variance.
- [ ] Diagnose.
- [ ] Decide: pivot or persevere.
- [ ] Update affected docs. Preserve old versions.

## 5. Version history

| Version | Date       | Author | Summary of change |
|---------|------------|--------|-------------------|
| v1      | YYYY-MM-DD | <name> | Initial.          |
```

---

## Supporting strategy doc skeleton (full template)

Paste this as the starting point for any new strategy doc (e.g., `09_risk.md`):

```markdown
# <Topic> [v1]

> **Goal:** <one sentence — the focus of this specific doc>
> **Last updated:** YYYY-MM-DD
> **Version:** 1

## 1. <Primary section>

<Tables preferred. Specific numbers. Cross-links to pillars and epics.>

## 2. <Secondary section>

<...>

## 3. <Tertiary section if needed>

<...>

## Re-evaluation protocol

**Cadence:** <e.g., quarterly>
**Triggers:** <list specific conditions>

- [ ] Pull actuals against targets in this doc.
- [ ] Note variance both directions.
- [ ] Diagnose causes.
- [ ] Decide: pivot or persevere.
- [ ] Update affected sections. Preserve old version if pivoting.

## Version history

| Version | Date       | Author | Summary of change |
|---------|------------|--------|-------------------|
| v1      | YYYY-MM-DD | <name> | Initial.          |
```

---

## How strategy docs connect to the rest of the methodology

- **Strategy → Pillars.** Each pillar (see [02_pillars.md](02_pillars.md)) should reference the strategy doc(s) it operationalizes. A pillar without a strategy reference is a project nobody asked for; a strategy without pillars is a wish.
- **Strategy → Epics.** Epic charters (see [03_epics.md](03_epics.md)) link back to strategy docs in their "Linked docs" section. The link makes scope arguments easier: "this epic exists because Phase 2 needs metric X to hit Y."
- **Strategy → Re-evaluation.** When a phase exit criterion is hit or a metric breaches, the re-evaluation protocol fires. The result may be an updated strategy version, which may in turn require new pillars or new epics.
- **Strategy and Working Principles** ([06_working_principles.md](06_working_principles.md)) and **Definition of Done** ([07_definition_of_done.md](07_definition_of_done.md)) — strategy docs are themselves changes that pass through the contributor workflow. The same surgical-change and goal-driven discipline applies to strategy edits.

---

## Common mistakes when writing strategy docs

| Mistake | Fix |
|---------|-----|
| Vision is a feature list. | Replace with a future-state sentence. |
| Phase has a date but no metric. | Add a falsifiable metric target. |
| Phase has a metric but no exit criterion. | Define the specific condition for moving on. |
| Doc is paragraphs of prose. | Convert claims into tables. Reserve prose for the framing line. |
| Cross-references are missing. | Link every claim that operationalizes elsewhere to its operationalization. |
| Doc has not been updated in over a year and no review happened. | Apply the re-evaluation protocol. Update or explicitly persevere. |
| Old version was overwritten and lost. | Recover from git history. Establish the archive convention going forward. |
| Master plan is 30 pages. | Move detail into supporting docs. The master plan is the index and the headline. |
| Two supporting docs cover overlapping topics. | Merge or split cleanly. Each topic has one home. |

---

## Authority

Strategy outranks pillars when they conflict. Pillars outrank epics when they conflict. Epics outrank items when they conflict. (The same precedence rule is restated in [`00_README.md` "Authority across the methodology"](00_README.md#authority-across-the-methodology) and [`02_pillars.md` "Authority"](02_pillars.md#authority); a change here should propagate to both.)

If a backlog item appears to require violating a pillar, the pillar wins — but the conflict should be surfaced; the strategy or pillar may need updating, not the item suppressed.

If a pillar appears to require violating the strategy, the strategy wins — same caveat.

Strategy itself can be changed. The mechanism is the re-evaluation protocol, which produces a versioned update. Strategy is not changed by quiet edit; it is changed by recorded decision.
