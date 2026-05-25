# Blog post draft — "How I keep AI agents from breaking my project"

_Maintainer: this draft is structured to be edited substantially to your voice. The skeleton + concrete examples are reusable; the framing + tone must come from you. Target length: 1,200–1,800 words. Reading time: 6–9 minutes._

---

## Title (pick one — or write your own)

**A.** How I keep AI agents from breaking my project (a 13-doc methodology)

**B.** The methodology I wrote after two AI agents both refactored my auth at 2am

**C.** Markdown + git is enough: a methodology for AI-collaborated software projects

**D.** Self-improving methodology: applying a methodology to its own development

## Hook (first 2–3 paragraphs — write these last; this is the part editors and readers judge)

[Maintainer-authored. Suggested ingredients: the 2am parallel-refactor story; the specific feeling of opening the repo the next morning to see two branches with conflicting auth changes both labeled "fix"; the realization that AI doesn't break workflows because AI is bad — it breaks them because workflows assume human velocity.]

## Section 1 — Why a methodology now

The implicit conventions that let small teams coordinate ("ping the person who owns this," "we discussed this in standup last week," "the PR template will catch it") break down when contributors include AI agents. Specifically:

- **Two contributors silently pick the same task.** With AI agents, this happens at AI speed — the conflict is committed before either contributor notices.
- **"Done" means whatever the contributor decided.** An AI agent will flip a task to done if no explicit gate prevents it. The gate has to be in the file, not in someone's head.
- **The same lesson gets relearned every session.** AI contributors don't have institutional memory unless the project gives them an explicit one.
- **Direction drifts faster than humans can re-anchor.** AI ships features fast; without an explicit long-term anchor, the project ships the wrong features fast.

The methodology I'll describe addresses each of these as a specific practice. None of the practices are novel individually; the value is having them as one coherent set that scales from solo + AI to small-team + AI.

## Section 2 — What's in it

[Maintainer: condense the README's "What you get" section here. Focus on the 13 docs + 5 templates + the autonomous-loop prompt. Mention CC BY 4.0 once.]

The two patterns that matter most for AI-assisted projects:

### Pattern 1 — File-based locks with TTL

Every item has a `Lock:` field. An agent picking up the item sets `Lock: <agent-id>@<timestamp+2h>`, commits, pushes. Any contributor pulling the repo can see the lock and skip the item. After the TTL, the lock expires and the item is anyone's. Two agents cannot silently pick the same item — they race at commit time, the loser sees the lock and moves on.

This sounds trivial. It's the single most-leverage practice in the methodology for multi-agent projects.

### Pattern 2 — Tier matrix for autonomous loops

When an autonomous loop is allowed to modify documentation (or any authoritative artifact), the rule "AI never touches this" is too strict, and "AI does whatever" is too loose. The tier matrix splits proposed changes by risk:

- **T0 — Cosmetic** (typos, dead anchors, version drift). Loop auto-patches on a `methodology-patch/YYYY-MM-DD-NN` branch with cross-AI diff-verification. Maintainer fast-forwards.
- **T1 — Surgical** (stale examples, single-paragraph clarifications). Same flow as T0.
- **T2 — Substantive** (rule wording, new constraints). Loop drafts in `loop-notes/`; maintainer authors the actual change.
- **T3 — Architectural** (new doc, removed doc, structural changes). Human-only.

"Escalate on doubt": if a finding could plausibly be T1 or T2, T2 wins. The cost of over-classification is much smaller than the cost of under-classification.

Cross-AI verifies the tier classification AND verifies the diff (grounded / correct / scoped). The maintainer reviews verified diffs, not raw findings. Time per fix drops from ~15 minutes to ~30 seconds.

## Section 3 — The eat-your-own-dog-food story

After v1.13.0 introduced the tier matrix, I applied the methodology to the methodology itself. Four autonomous loop runs in one day:

- **Run 1** seeded an `evaluations/` folder.
- **Run 2** cold-read methodology docs 00–05 (fresh Opus session, no prior context) — 25 findings.
- **Run 3** cold-read docs 06–11 — 29 findings + 5 cross-batch inconsistencies.
- **Run 4** classified all 59 findings on a two-axis matrix (practice/docs + tier T0–T3), shipped 30 T0/T1 patches across all 12 docs in one batch (v1.14.0), deferred 28 T2 findings to me as the maintainer.

The escalate-on-doubt rule fired on 5 of 10 sampled tier classifications (50% over-claim rate). Cross-AI diff-verification caught 3 mechanical issues in the patch batch (a broken anchor, an inaccurate paraphrase, a typo).

The thing I'd predicted would be the hardest — keeping the loop honest about which fixes it should and shouldn't attempt — was actually solved by the matrix itself. The thing I hadn't predicted — that diff-verification would routinely catch implementing-session mistakes — turned out to be the most operationally valuable gate.

## Section 4 — The periodic deep-eval

[Maintainer: this is the section to expand or condense based on the blog's audience.]

Per-item Definition of Done catches single-change defects. It doesn't catch the compounded UX debt, the cross-cutting performance regression, or the slow security drift across many items that each individually passed their DoD.

The periodic deep-eval (doc 12, shipped today in v1.15.0) runs every Nth loop iteration. It scores the project on a 0–10 rubric per area — UX, frontend, backend, security, performance, test coverage, content quality, documentation, ops, accessibility — adapted per project. Default thresholds: minimum 8 per area, average 9. No area averaged away.

Unsolvable issues get handled / postponed / marked — never forced. The methodology's stance: marking is honest; forced progression is dishonest.

## Section 5 — What I haven't tested yet

The methodology has been applied to two projects: a real one (a location-based audio app) and the methodology itself. **It has not been tested on:**

- A regulated-industry project where Compliance is a load-bearing rubric area.
- A consumer mobile app with iOS/Android parity concerns.
- A team larger than 2 humans + 3 AI agents.
- A different programming-language ecosystem than what I work in.

I'd love to hear from anyone who tries it on a different shape of project. The failure modes I find most interesting: when does the tier matrix break down? When does the rubric become theater? When does the periodic deep-eval slow throughput more than it improves quality?

## Section 6 — How to try it

1. Read the [CHEATSHEET](https://github.com/Korner83/ai-development-methodology/blob/main/CHEATSHEET.md) — ~80 lines, 5-minute read.
2. If it looks worth more time, read [`methodology/00_README.md`](https://github.com/Korner83/ai-development-methodology/blob/main/methodology/00_README.md) — sets the mental model.
3. Look at [`examples/`](https://github.com/Korner83/ai-development-methodology/tree/main/examples) for a worked example.
4. Copy the relevant templates from [`templates/`](https://github.com/Korner83/ai-development-methodology/tree/main/templates) into your project. Adapt to your situation.
5. CC BY 4.0 — fork freely.

## Closing

[Maintainer-authored. Suggested ingredients: humility about claiming this is "the" methodology; acknowledgement that any methodology that survives contact with reality changes within months; invitation for criticism; the maintainer's own contact info.]

---

## After publication

- Cross-post the canonical URL to your social channels.
- Pin the post on your blog's homepage for 30 days.
- Save reader feedback (comments + tweets) for the FEEDBACK.md inbox.
- Re-score "Adopter discoverability" at the next deep-eval (Run 6) once the post has had 30 days of organic reach.
