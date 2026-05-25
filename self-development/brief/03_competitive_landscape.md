# Competitive Landscape

Nine named alternatives, surveyed during the v1.5.0 research pass and refreshed for this brief. Each entry: what it covers, what it does well, where it falls short, and whether it overlaps or complements this methodology.

For market gaps these alternatives leave open, see [04_market_gaps.md](04_market_gaps.md).

---

## 1. GitHub Spec Kit (~106k★)

- **URL:** [github.com/github/spec-kit](https://github.com/github/spec-kit)
- **License / status:** MIT, very active. GitHub-backed.
- **What it covers:** Spec-Driven Development. The cycle is **Constitution → Specify → Clarify → Plan → Tasks → Implement** with vendor-neutral CLI scaffolding and per-step artifact templates.
- **What it does well:** sharp spec-first discipline; vendor-neutral; thorough artifact generation. The "Constitution" step (project-wide invariants) is conceptually similar to this methodology's working principles + hard rules. Very polished templates and CLI tooling.
- **Where it falls short:** thin on Definition of Done as a binding gate, no concurrency primitive (lock pattern), no memory layer for cross-session learning, no named anti-patterns for the AI-specific failure modes.
- **Relationship to this methodology:** **biggest direct competitor** by mindshare. Adopters comparing options will likely see Spec Kit first. The differentiation is in the discipline overlays (DoD, locks, memory) and the named anti-patterns (cheating agent, yes-man, etc.).

## 2. BMAD Method

- **URL:** [github.com/bmad-code-org/BMAD-METHOD](https://github.com/bmad-code-org/BMAD-METHOD)
- **License / status:** MIT, very popular, active. Persona-heavy: PM, Architect, Dev, UX, QA, etc. (12+ defined agent personas).
- **What it covers:** multi-agent workflows with explicit roles, "party mode" (multiple agents at once), CLI + Web UI, scale-adaptive workflows.
- **What it does well:** explicit role separation; rich tooling; good for teams that want a defined agent persona system.
- **Where it falls short:** persona-heavy and tooling-heavy; culturally opposite to the "markdown + git, no SaaS" framing; locked into the BMAD CLI / web UI for some workflows.
- **Relationship to this methodology:** **complementary in some ways, opposite in others.** BMAD answers "what AI personas are on the team?" This methodology answers "what discipline binds every contributor regardless of which AI?" Adopters who want personas should use BMAD; adopters who want minimalism should use this.

## 3. Ralph loop (Geoffrey Huntley)

- **URL:** [ghuntley.com/ralph](https://ghuntley.com/ralph/)
- **License / status:** Blog post (CC-ish), highly influential.
- **What it covers:** the literal pattern `while :; do cat PROMPT.md | claude-code; done` — one task per loop, prompt-tuning over tool-blame.
- **What it does well:** brutally simple. Captures the essential "loop until done" insight. Generated a lot of conversation in the AI-coding community.
- **Where it falls short:** greenfield-biased; assumes single-driver (no parallel work); no formal DoD or review gate; depends on backpressure from tests/types to course-correct.
- **Relationship to this methodology:** **the autonomous-loop template (`AUTONOMOUS_LOOP.md`) is a structured Ralph loop.** This methodology builds on Ralph's insight but adds: parallel work via locks, formal DoD, four planning layers, brownfield support, HUMAN_NEEDED.md for blocked items, ROI heuristic for picking next.

## 4. stdlib pattern (Geoffrey Huntley)

- **URL:** [ghuntley.com/specs](https://ghuntley.com/specs/)
- **License / status:** Blog post (CC-ish), influential.
- **What it covers:** build up a library of thousands of small composable prompting rules over time; learn from every mistake → new rule.
- **What it does well:** captures the *accumulation* property — methodology improves with use. Names the "rule grows from a single mistake" mechanism.
- **Where it falls short:** no locks, no planning hierarchy, rule-corpus-only.
- **Relationship to this methodology:** **the stdlib growth loop section in `methodology/08_lessons_and_memory.md` adapts Huntley's pattern**, explicitly crediting the connection. This methodology integrates rule-accumulation as one mechanism within a broader system rather than as the whole system.

## 5. AGENTS.md standard

- **URL:** [agents.md](https://agents.md/)
- **License / status:** CC; adopted by Cursor, Aider, OpenAI Codex, Jules, Zed.
- **What it covers:** single canonical instruction file consumed by many AI coding tools. Just the file standard, not a process.
- **What it does well:** vendor-neutral, simple, no opinion beyond the format itself.
- **Where it falls short:** doesn't tell you *what to put in the file* — just where it goes.
- **Relationship to this methodology:** **this methodology uses AGENTS.md as one of its primary templates** (along with CLAUDE.md, .cursorrules, .continue/context.md). AGENTS.md is the carrier; this methodology supplies the contents.

## 6. Get Shit Done (GSD)

- **URL:** [prafulls.me/blogs/gsd-spec-driven-development](https://www.prafulls.me/blogs/gsd-spec-driven-development)
- **License / status:** Open, growing.
- **What it covers:** "Specs are prompts" — the quality of the spec dictates the quality of the AI's output.
- **What it does well:** sharp single-axis insight (spec quality is everything).
- **Where it falls short:** single-axis; doesn't cover concurrency, DoD gates, memory, or autonomous loops.
- **Relationship to this methodology:** **the "spec is the asset" principle in `methodology/11_human_roles.md` is consistent with GSD's framing.** GSD is narrower; this methodology covers more surface area.

## 7. Nano-Spec

- **URL:** [github.com/tao-hpu/nano-spec](https://github.com/tao-hpu/nano-spec)
- **License / status:** Open.
- **What it covers:** four templates (README, todo, doc, log). ~10 minutes to set up. Deliberately tiny.
- **What it does well:** lowest-friction adoption. Anyone can copy four templates.
- **Where it falls short:** deliberately minimal. No DoD, no locks, no memory, no verification protocol.
- **Relationship to this methodology:** **this methodology is the larger superset** of what nano-spec does. Adopters who want the absolute minimum should try nano-spec first; adopters who need DoD, locks, memory, and verification graduate to this.

## 8. Vendor best-practice docs

- **Anthropic** — ["How teams use Claude Code"](https://www-cdn.anthropic.com/58284b19e702b49db9302d5b6f135ad8871e7658.pdf) PDF + [code.claude.com/docs](https://code.claude.com/docs/en/best-practices). Covers plan-mode discipline, TDD, Writer/Reviewer pair pattern, parallel sessions via worktrees, CLAUDE.md context.
- **OpenAI Codex** — built-in workflow docs in the Codex CLI.
- **Cursor** — `.cursorrules` and rules system documentation.
- **Aider** — `CONVENTIONS.md` patterns.
- **Continue.dev** — `.continue/context.md` patterns.

- **What they do well:** authoritative on their own tools; written from the vendor's seat with real signal about how the tool is actually used.
- **Where they fall short:** vendor-specific by definition; observation-shaped rather than methodology-shaped; tools change, so the docs change.
- **Relationship to this methodology:** **complementary.** Vendor docs say "how to use this specific tool"; this methodology says "how to organize the project regardless of which tool you use." Both useful; different layers.

## 9. Academic papers

- **Agentsway** ([arxiv.org/pdf/2510.23664](https://arxiv.org/pdf/2510.23664)) — proposes a full SDLC methodology specifically for AI-agent teams. Challenges Agile / Kanban assumptions. Academic framing.
- **Agile V** ([arxiv.org/pdf/2602.20684](https://arxiv.org/pdf/2602.20684)) — Agile iteration + V-Model verification + mandatory human approval gates ("Infinity Loop"). Compliance / audit framing.

- **What they do well:** rigorous, conceptually deep, peer-reviewed.
- **Where they fall short:** academic-paper format isn't a usable methodology kit; no templates, no protocols, no day-to-day flow.
- **Relationship to this methodology:** **adjacent but different shape.** Useful for adopters who want intellectual grounding; less useful for adopters who want a working set of practices today.

---

## Map of the field

| Axis | Position |
|---|---|
| **Mindshare** | GitHub Spec Kit dominates. BMAD second. The rest are niche or specialized. This methodology has near-zero current mindshare. |
| **Discipline-overlay depth** | This methodology > Spec Kit ≥ BMAD > others. Most peers lean on tooling or templates rather than enforced gates. |
| **Tool-agnosticism** | This methodology = AGENTS.md = nano-spec > Spec Kit > BMAD > vendor docs. |
| **Minimalism** | nano-spec < Ralph < this methodology ~ Spec Kit < BMAD. |
| **Multi-contributor (humans + AI same protocol)** | This methodology is distinctive — locks for both. Peers assume single-driver or use heavy isolation (VMs, sub-agent spawning). |
| **Named anti-patterns** | This methodology distinctive — most peers don't name the cheating-agent / yes-man / stranger-in-own-code / tribal-knowledge-loss failure modes. |

---

## What this means for positioning

- **Don't compete head-on with Spec Kit on mindshare or polish.** Spec Kit has GitHub-the-company behind it; competing for the same attention is a losing trade.
- **Compete on discipline depth + tool-agnosticism + multi-contributor support.** These are real gaps where the methodology is genuinely different, not just marginally better.
- **Position alongside, not against.** The README's "What's similar, what's different" table does this well — names alternatives, says where each is strong, says where this differs. Adopters trust honest comparison more than chest-thumping.
- **Lean into the self-development cycle** as a differentiator. No peer methodology publicly applies itself to its own development as a living example.

---

## Note on this survey

This competitive analysis covers nine methodologies as of **2026-05-25**. The AI-coding methodology field moves fast; new methodologies may emerge that fill some of the gaps claimed in [04_market_gaps.md](04_market_gaps.md). The semi-annual methodology self-evaluation (per [methodology/07_definition_of_done.md](../../methodology/07_definition_of_done.md#methodology-self-evaluation-semi-annual)) should re-survey the field. Treat the "no peer has X" claims as snapshot-in-time observations, not permanent statements.
