# Market Gaps

The competitive landscape ([03_competitive_landscape.md](03_competitive_landscape.md)) covers nine named alternatives. This doc names the gaps those alternatives leave open — and where this methodology is genuinely distinct.

Gaps are concrete (linked to specific peer surveys), not aspirational. If a gap turns out to be filled by a peer this brief missed, the gap closes and this doc should be updated.

## The nine gaps

### 1. "Cheating agent" anti-pattern

**The gap:** when the same AI writes both the implementation and the tests, the test can be subtly tuned to validate the broken implementation. Green test suite → assumed done → bug ships. None of the surveyed peer methodologies names this failure mode explicitly. Spec Kit and BMAD both assume tests-pass = done.

**This methodology's coverage:** [`methodology/10_testing_and_verification.md` "The cheating agent" section](../../methodology/10_testing_and_verification.md) plus [`methodology/11_human_roles.md` anti-pattern #1](../../methodology/11_human_roles.md). Defenses: write tests first (ideally by human); cross-AI validate the tests; human-review test names and acceptance criteria; periodic random audits of AI-written test/impl pairs.

### 2. File-based locks for humans + agents using the same protocol

**The gap:** peer methodologies assume a single driver, or use heavy isolation (VMs, container per agent, sub-agent spawning). I haven't found a peer methodology that ships a same-format lock for humans and AI agents to use identically.

**This methodology's coverage:** [`methodology/05_locks_and_parallel_work.md`](../../methodology/05_locks_and_parallel_work.md) — file-based `Lock: <holder>@<TTL-expiry>` field with bounded TTL (typically 2h) that any contributor (human or AI) follows. Git-tracked. No central registry needed.

### 3. Challenge-before-consenting as a named pattern with copy-paste prompt

**The gap:** peers acknowledge the AI agreement bias in passing (Anthropic's docs mention it; academic papers note it). None ships a copy-paste counter-prompt as a named pattern that adopters can use mid-decision.

**This methodology's coverage:** [`methodology/06_working_principles.md` "Challenge before consenting" section](../../methodology/06_working_principles.md) — explicit prompt: *"Before we proceed: what's wrong with this plan? What's the strongest case AGAINST? What would a senior engineer poke holes in?"* Plus guidance on when to use it (mid-incident, before approving plans, when noticing suspicious unanimity).

### 4. Four-layer planning hierarchy

**The gap:** most peers stop at two layers (spec → tasks). Spec Kit has Constitution → Specify → Clarify → Plan → Tasks (multi-step but not multi-layer; all within one project scope). BMAD has phases but no upstream strategy layer. Adopters with longer time horizons end up improvising the upstream layers.

**This methodology's coverage:** [`methodology/00_README.md` "The mental model"](../../methodology/00_README.md) — Strategy (years) → Pillars (years, evergreen capability layers) → Epics (3–12 weeks) → Items (1–2 weeks human / daily AI). Each layer answers a different question and operates on a different time horizon.

### 5. Definition of Done coupled to the work-item frontmatter

**The gap:** peers typically have a DoD as a separate doc or checklist. Coupling DoD enforcement to the item's frontmatter (Status / Test / Lock fields that must agree) is unusual. Without coupling, DoD can be silently skipped — the item's "done" status doesn't enforce the DoD's "tested" status.

**This methodology's coverage:** [`methodology/07_definition_of_done.md` "The hard rule"](../../methodology/07_definition_of_done.md) and [`methodology/04_backlog_items.md` "Coupled fields"](../../methodology/04_backlog_items.md) — `Status: done` requires `Test: pass`. No path from `Test: not-tested` or `Test: fail:` to `Status: done`. Mechanically enforced by the field coupling.

### 6. HUMAN_NEEDED.md pattern

**The gap:** peer methodologies don't ship a dedicated pattern for tracking items blocked on human-only action. Blocked items tend to either deadlock (agent holds lock waiting for human credential), get lost in the backlog, or surface only via ad-hoc Slack pings.

**This methodology's coverage:** [`methodology/04_backlog_items.md` "HUMAN_NEEDED.md"](../../methodology/04_backlog_items.md) — dedicated file at `backlog/HUMAN_NEEDED.md` (sibling of `EPICS.md`). Protocol: agent sets `Status: blocked`, releases lock, adds `**Blocker:**` line, adds one-line entry to `HUMAN_NEEDED.md`, moves on. Humans scan the file at check-in time.

### 7. ROI-based prioritization with explicit heuristic table

**The gap:** peer methodologies have priority and effort fields, but typically don't ship a default decision rule for combining them. The result: contributors (especially AI agents in autonomous mode) pick whatever item caught their attention.

**This methodology's coverage:** [`methodology/04_backlog_items.md` "Prioritization — the ROI heuristic"](../../methodology/04_backlog_items.md) — explicit table mapping (Priority × Effort) → "what to do." P0 always, P1-XS first, P2-M defer unless scheduled, P3-any belongs in `FUTURE.md`. Used directly by the autonomous loop to converge on milestone outcomes.

### 8. Methodology self-evaluation cadence

**The gap:** peer methodologies don't include "the methodology checks itself" as a recurring practice. Docs and reality drift apart over months; eventually the docs become stale ("what we wrote a year ago") rather than descriptive ("how we actually work").

**This methodology's coverage:** [`methodology/07_definition_of_done.md` "Methodology self-evaluation (semi-annual)"](../../methodology/07_definition_of_done.md) — sits as a parallel concept to the existing quarterly repo-health audit. Re-read every doc cold, classify gaps as "practice is wrong / docs are wrong / both," ship updates via the promotion loop. This very `self-development/` folder is the operationalization of the practice.

### 9. Decision-ownership matrix

**The gap:** peers acknowledge AI vs human roles abstractly. None ships a concrete RACI-lite matrix mapping ~20 specific decision types (code style, naming, refactor, schema, API shape, auth, architecture, production deploy, destructive operations, strategy, pricing, hiring, legal) to five ownership columns (AI proposes / AI decides / Human reviews / Human decides / Human-only).

**This methodology's coverage:** [`methodology/11_human_roles.md` "The decision-ownership matrix"](../../methodology/11_human_roles.md) — 21-row table with hard-coded rightmost-column rows (production deploys, force-push, destructive operations) that match the methodology's existing hard rules. Adopters use it as a starting point and adapt per their risk tolerance. Concrete enough to settle "should the AI do X?" arguments.

## Adjacent gaps explicitly NOT addressed

Some real gaps exist where this methodology deliberately doesn't go. Adopters who need these should look elsewhere:

- **AI persona system** (BMAD's specialty). This methodology stays minimal; no PM / Architect / Dev personas.
- **CLI tooling for the methodology itself** (BMAD has, Spec Kit has). This methodology is markdown + git only.
- **Visual / UI for the backlog** (Linear, Jira, BMAD Web UI). This methodology stays text-only.
- **Specific test framework recommendations.** Stack-agnostic.
- **Compliance / regulatory framing** (Agile V academic paper goes here). This methodology stays general-purpose; regulated industries adapt via project-specific overlay.
- **Translation infrastructure.** Decided against (browsers auto-translate; drift is the killer).

## Where this leaves the methodology

The methodology's distinctiveness is concentrated in **gaps 1, 2, 3, 6, 8, 9** — the named anti-patterns, the lock protocol for both human and AI, the challenge prompt, HUMAN_NEEDED.md, self-evaluation cadence, decision-ownership matrix. These don't exist in equivalent shape in any surveyed peer.

The other gaps (4 — four-layer planning, 5 — DoD coupled to item, 7 — ROI heuristic) exist in *partial* form in some peers. The methodology's version is sharper or more enforced, but adopters considering Spec Kit might find Spec Kit's coverage "good enough" on these.

**Strategic implication:** marketing should lead with the six distinctive gaps. The other three are improvements at the margin.
