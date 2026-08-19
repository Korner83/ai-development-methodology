# P4 — Tool compatibility

> **Pillar goal:** the methodology's protocols work with any AI coding tool that reads a project-instruction file, without adopter rework when tools change.
>
> **Last updated:** 2026-08-19

**Related:**
- Brief: [Capability layer 4](../brief/08_capability_layers.md#4-tool-compatibility)
- Strategy phase: [Phase 1 — Foundation](../strategy/00_master_plan.md#phase-1--foundation-current--3-months) (primary)
- Depends on: [P3 — Doc currency](P3_doc_currency.md)
- Feeds into: [P5 — Adopter discoverability](P5_adopter_discoverability.md) (adopters can't adopt without a compatible tool, so compatibility is a prerequisite for discovery to convert)
- Delivering epics: (none yet)

## 1. Overview

Tool compatibility is a **prerequisite for adoption**, not a downstream concern. Adopters who find the methodology immediately ask "does this work with my tool?" before they read further. If the answer is "you need to use X," adopters who already use Y leave.

This pillar is also one of the methodology's core values. The methodology is *tool-agnostic by design*: every protocol works with any AI agent that can read files and run commands. No vendor lock-in, no CLI dependency, no SaaS dependency.

The pillar was resequenced from P6 to P4 during the Step 0 cross-AI review for exactly this reason: it's foundational, not downstream of examples.

## 2. What this pillar covers

| Tool surface | What "compatible" means here |
|---|---|
| **Claude Code (Anthropic)** | `CLAUDE.md` template provided; reads automatically; covers project-instruction needs. |
| **OpenAI Codex CLI** | `AGENTS.md` template (vendor-neutral superset); reads automatically. |
| **Google Antigravity** | `AGENTS.md` or `.agent/instructions.md`; reads automatically. |
| **Cursor** | `.cursor/rules/` or `.cursorrules` — adapt from AGENTS.md. |
| **Aider** | `CONVENTIONS.md` — adapt from AGENTS.md. |
| **Continue.dev** | `.continue/context.md` — adapt from AGENTS.md. |
| **Any other tool** | Whatever `.md` it reads — either template adapts. |
| **Switching tools** | Adopter moves from Claude Code → Cursor → Codex without re-learning the methodology — only swaps the project-instruction filename. |

## 3. Exit criteria

The pillar is *delivered* when:

- [x] All 6 major AI coding tools listed above have a usable starting template — 3 via native template files (CLAUDE.md for Claude Code; AGENTS.md for Codex and Antigravity) and 3 via adaptation from AGENTS.md (Cursor, Aider, Continue.dev). **Met as written:** adaptation *is* a usable starting template. E04 proposed promoting the latter three to native files and was parked on 2026-08-14 — three more files to keep in sync with `AGENTS.md`, against vendor conventions that are still moving, for a need no adopter has reported. Reopens if an adopter reports that adaptation actually failed them.
- [ ] The most recent semi-annual self-evaluation cross-AI review found no protocol in `methodology/*.md` that depends on a tool-specific feature — i.e., all protocols are framed tool-agnostically (locks are file-based; verification is loop-based; memory is file-based).
- [ ] The AGENTS.md template is the canonical "anything else" path: it is up-to-date in the most recent release and contains no Claude-Code-specific assumptions.
- [ ] The README "AI tool support" table is current and covers each tool listed in the brief's [07_tech.md](../brief/07_tech.md).

**Re-tested:** every time a new AI tool gains significant share; opportunistically when adopters report cross-tool issues.

**Health indicators** (not binary, depend on adopter behavior):

- ≥1 adopter publicly reports using the methodology across ≥2 different AI tools without methodology adjustment beyond filename / template choice.
- New significant AI coding tools (≥1 year of ecosystem usage) get a template entry within ~1 day of the maintainer learning about them.

## 4. Dependencies

**Depends on:** [P3 — Doc currency](P3_doc_currency.md). Templates that don't match the current methodology drift the most-visible artifact. Currency on templates matters more than currency on prose docs.

**Feeds into:**

- **P5 — Adopter discoverability** — discoverable methodology that's incompatible with the adopter's tool produces a bounce.
- **P7 — Community feedback loop** — community contributions often include "I adapted X for tool Y" patterns. Compatibility creates the surface for those contributions.

## 5. Anti-patterns

- **Adding tool-specific protocols to the methodology proper.** If a rule says "use Claude Code's plan mode" rather than "use your tool's planning feature," the methodology has lost compatibility.
- **Letting templates drift relative to each other.** CLAUDE.md and AGENTS.md should describe the same methodology; only the filename and tool-specific harness assumptions differ.
- **Maintaining different content for each template.** Maintenance burden multiplies linearly with tool count. The AGENTS.md superset + symlink pattern is the lean approach.
- **Predicting tool features.** "When Tool X adds capability Y, the methodology will..." is speculation. Wait for the tool, then adapt.
- **Promising support for tools the maintainer doesn't use.** Adopters can adapt AGENTS.md for any tool; the maintainer doesn't need to validate every variant personally.

## 6. Current state (last reviewed 2026-08-19; entries below date from v1.8.0 unless noted)

**Strong:**

- 6 templates in `templates/` cover the major surfaces (CLAUDE.md, AGENTS.md, AGENT_KICKOFF.md, AUTONOMOUS_LOOP.md, PROJECT_STRUCTURE.md, ROLE_BRIEFS.md — the last added in v1.30.0).
- AGENTS.md is the vendor-neutral superset; CLAUDE.md is the Claude-Code-harness variant.
- README "AI tool support" table maps each tool to its expected filename.
- "Permissions and vendor compatibility" section in README (added v1.3.1) makes the vendor-agnostic stance explicit.

**Known gaps:**

- No actual cross-tool adopter has publicly reported moving between tools using the methodology unchanged. (The compatibility is *designed*; the cross-tool *test* hasn't happened yet at scale.)
- No native templates for Cursor, Aider, or Continue.dev — adopters adapt from AGENTS.md. Native templates would reduce friction but multiply maintenance burden.
- New AI tools (e.g., emerging vendors) aren't proactively monitored. The pillar relies on adopter reports surfacing new compatibility needs.

**Honest:** the methodology's compatibility claim is theoretically clean but practically unproven at the cross-tool-switching level. Real adoption stories from multi-tool teams would change this.

## 7. Delivering epics

(None yet.)
