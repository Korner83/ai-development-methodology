# P6 — Example richness

> **Pillar goal:** adopters can see how the abstract methodology patterns translate to real projects — not just read about them.
>
> **Last updated:** 2026-05-25

**Related:**
- Brief: [Capability layer 6](../brief/08_capability_layers.md#6-example-richness)
- Strategy phase: [Phase 2 — Discovery](../strategy/00_master_plan.md#phase-2--discovery-3--12-months-from-phase-1-exit) (primary)
- Depends on: [P5 — Adopter discoverability](P5_adopter_discoverability.md), [P2 — Doc clarity](P2_doc_clarity.md)
- Feeds into: [P7 — Community feedback loop](P7_community_feedback_loop.md) (adopters who see examples are more likely to share their own experience)
- Delivering epics: (none yet)

## 1. Overview

Abstract docs are necessary but insufficient. Adopters need to see concrete instantiations to know "this would actually work in my situation." This is one of the most consistent gaps adopters mention in open-source-project research.

The `self-development/` folder is the **first canonical example**. It's the methodology applied to its own development — a worked example that grows in scope as the bootstrap completes (Steps 0–4) and as the autonomous loop operates (Step 5+).

Beyond the self-development example, this pillar covers additional anonymized real-project artifacts that adopters can lift directly: example strategy docs, example pillar files, example epic charters, example BL items. These don't exist yet (as of v1.8.0) and are likely Phase 2 epic work.

## 2. What this pillar covers

| Example type | What "rich" means here |
|---|---|
| **Self-development worked example** | The `self-development/` folder demonstrates the methodology applied to a real ongoing project (this one). Grows with the bootstrap. |
| **Anonymized strategy doc set** | At least one anonymized example of a strategy master plan + supporting docs from a real adopter project. (Pending.) |
| **Anonymized pillar set** | At least one anonymized example of 5-8 pillars for a real product. (Pending.) |
| **Anonymized epic charter** | At least one fully-worked epic charter with outcome, exit criteria, items. (Pending.) |
| **Anonymized BL items** | A handful of full BL item blocks showing real frontmatter, body, lifecycle. (Pending.) |
| **Worked failure scenarios** | Examples of "things went wrong, here's how the methodology helped recover." Likely lives in adopter case studies once they exist. |
| **Adapter examples** | Examples of how to adapt the methodology for niche cases (research teams, regulated industry, etc.). Pending fork emergence. |

## 3. Exit criteria

The pillar is *delivered* when:

- [ ] `self-development/` folder is at least at Step 4 of the bootstrap (autonomous loop config exists), making it a complete worked example through epic + items + loop.
- [ ] At least one anonymized example set exists in the repo (strategy + pillars + epic charter + items) — likely in a new `examples/` folder.
- [ ] At least 2 public adopter case studies exist (third-party-authored or maintainer-written with adopter consent), demonstrating real applications.
- [ ] At least 1 niche adaptation (regulated industry, research team, etc.) has been forked and shows methodology variants.

**Re-tested:** quarterly during Phase 2; the bar rises as adoption matures.

## 4. Dependencies

**Depends on:**

- [P5 — Adopter discoverability](P5_adopter_discoverability.md). Without adopters, there are no adoption stories to examplify.
- [P2 — Doc clarity](P2_doc_clarity.md). Examples are downstream of clarity — they reinforce, not replace, clear abstract docs.

**Feeds into:**

- [P7 — Community feedback loop](P7_community_feedback_loop.md). Adopters who see examples are more likely to contribute their own.
- [P9 — Self-improvement velocity](P9_self_improvement_velocity.md). The self-development example IS the test case for whether the cycle works at scale.

## 5. Anti-patterns

- **Fictional examples that pretend to be real.** Adopters can tell. Use either truly anonymized real-project artifacts or clearly-labeled illustrative examples.
- **Examples that just demonstrate the format, not the value.** A BL item with frontmatter and body but no genuine decision shown isn't an example; it's a template.
- **Stale examples.** Examples from v1.0 referring to methodology shapes that have evolved confuse adopters. Examples must be current relative to the methodology version they pair with.
- **Over-curated examples that hide real friction.** If the example smooths over the actual messiness of real-project work, it teaches the wrong lesson. Show the loop fix-test, the blocker discovery, the scope split.
- **Treating the self-development folder as the only example needed.** It's *an* example, but it's a docs-only project. Adopters with code projects need code-shaped examples too.

## 6. Current state (v1.8.0)

**Strong:**

- `self-development/` folder created (v1.7.0 with Step 0 brief; v1.8.0 adds Step 1 strategy + pillars).
- The brief and strategy/pillars together demonstrate Steps 0–1 of the methodology applied to a real project (this one).
- Methodology docs include illustrative examples inline (e.g., 04_backlog_items.md has worked BL item examples).

**Known gaps:**

- No `examples/` folder yet. The brief's menu (from very early in this project's history) noted this as missing; remains missing.
- No anonymized real-project artifacts beyond inline methodology-doc examples.
- No public adopter case studies (the project is too new).
- The self-development folder is docs-only; adopters with code-heavy projects lack a code-shaped worked example.
- No "things went wrong" failure-mode worked examples.

**Honest:** this is the least-developed pillar as of v1.8.0 (excepting P7, P8, P9 which are intentionally dormant in Phase 1). Building rich examples is Phase 2 work and depends on having adopters whose work can be (anonymously) cited.

## 7. Delivering epics

(None yet. Likely Phase 2 epics: "Create `examples/` folder with anonymized real-project artifacts"; "First adopter case study"; "Failure-mode worked examples.")
