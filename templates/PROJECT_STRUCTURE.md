# Project Structure Template

A recommended folder structure and file-naming convention for projects adopting this methodology. **Adapt to your project's needs** — this is a starting point, not a prescription. The methodology itself only requires the items/epics/locks/memory layer; everything else is convention.

---

## Top-level layout

```
my-project/
├── README.md                    # Project pitch + setup commands
├── CHANGELOG.md                 # Reverse-chronological release history
├── LICENSE                      # Your license
├── STATUS.md                    # Maintenance posture + current phase
├── CLAUDE.md  /  AGENTS.md      # Project instruction file (vendor-specific filename)
│
├── docs/                        # All durable documentation
│   ├── strategy/                # Vision, market research, business model, roadmap
│   ├── pillars/                 # Pillar definitions (capability layers)
│   ├── planning/                # Pre-epic design exploration (optional)
│   ├── architecture/            # System design (data flow, schema, services)
│   ├── operations/              # Runbooks, on-call, deploy procedures
│   ├── audits/                  # Integrity checks, periodic health reports (optional)
│   └── methodology/             # Vendored copy of this methodology (or symlink)
│
├── backlog/                     # All work-tracking artifacts
│   ├── README.md                # Backlog workflow + AI agent playbook
│   ├── EPICS.md                 # Cross-epic rollup (active, done, parked counts)
│   ├── TEST_BACKLOG.md          # Cross-epic manual-QA queue (optional; see 03)
│   ├── HUMAN_NEEDED.md          # Items blocked on human agency (see 04)
│   └── epics/
│       └── E<NN>-<slug>/        # One folder per epic (E-prefix per 03)
│           ├── README.md        # Epic charter (pillar, outcome, exit criteria)
│           ├── BACKLOG.md       # Active items
│           ├── ARCHIVE.md       # Done items
│           ├── FUTURE.md        # Deferred items (out-of-scope this epic)
│           └── TEST.md          # Epic-specific acceptance + regression scenarios
│
├── memory/                      # Per-project memory directory (see 08)
│   ├── MEMORY.md                # Index file
│   └── *.md                     # Individual memory entries
│
├── src/                         # Application code (project-specific)
├── tests/                       # Test code (project-specific)
└── scripts/                     # Build, deploy, operational scripts
```

---

## File-naming conventions

| Artifact | Pattern | Example |
|---|---|---|
| **Strategy docs** | `NN_topic.md` (zero-padded numeric prefix, snake_case body) | `01_market.md`, `04_business.md`, `10_roadmap.md` |
| **Pillar docs** | `P<#>_<slug>.md` | `P1_authentication.md`, `P2_billing.md`, `P9_compliance.md` |
| **Epic folders** | `E<NN>-<slug>` (literal `E` prefix, zero-padded 2-digit number, kebab-case slug — see [`methodology/03_epics.md`](../methodology/03_epics.md#naming-convention-enn-slug)) | `E01-onboarding`, `E02-payments`, `E12-compliance` |
| **Work items** | `BL-<####>` (monotonic, zero-padded, **repo-wide**) | `BL-0001`, `BL-0428`, `BL-1337` |
| **Memory entries** | `<type>_<topic>.md` | `feedback_no_emojis.md`, `project_auth_flow.md`, `reference_grafana.md` |
| **Architecture docs** | `<topic>.md` (descriptive, kebab-case or snake_case — pick one) | `database-schema.md`, `data-flow.md`, `service-boundaries.md` |
| **Runbooks** | `<scenario>_runbook.md` | `incident_runbook.md`, `deploy_runbook.md`, `on_call_runbook.md` |
| **Audits** | `<topic>_audit_YYYY-MM-DD.md` | `dependency_audit_2026-05-25.md` |

### ID-space rules

- **Work item IDs (BL-####) are monotonic and repo-wide**, not scoped per epic. This prevents collisions when items move between epics and makes `grep BL-0428` unambiguous across the whole repo.
- **Epic IDs (NN) are sequential within `backlog/epics/`**, zero-padded so a directory listing sorts naturally.
- **Pillar IDs (P<#>) are sequential within `docs/pillars/`**. The number is permanent — even if you reorder importance, don't renumber. New pillars get the next available number.
- **Strategy doc numbers (NN_) follow a deliberate ordering** — see [01_strategy.md](../methodology/01_strategy.md) for the recommended doc set and order.

### Why these conventions

- **Predictability for AI agents.** Agents that have read the convention can navigate any project that follows it. No re-learning per project.
- **Greppability.** `grep BL-0428` always finds the item. `find docs/strategy` always works.
- **Stable cross-references.** Links between docs (e.g., a strategy doc linking to a pillar) survive moves because the paths are convention-based, not arbitrary.
- **Tool-agnostic.** Markdown + git only. No IDE-specific files, no SaaS dependencies, no migration cost when the team's tooling changes.

---

## What lives where — quick reference

| Question | Lives in |
|---|---|
| Why does this product exist? | `docs/strategy/00_master_plan.md` |
| What capabilities does the product need long-term? | `docs/pillars/` |
| What 3–12 week batch are we doing right now? | `backlog/epics/E<NN>-<slug>/README.md` (charter) |
| What's the next 1–2 week unit (human) / next day's work (AI)? | `backlog/epics/E<NN>-<slug>/BACKLOG.md` |
| What did we ship? | `backlog/epics/E<NN>-<slug>/ARCHIVE.md` + `CHANGELOG.md` |
| What's deferred but not abandoned? | `backlog/epics/E<NN>-<slug>/FUTURE.md` |
| What's blocked waiting on a human? | `backlog/HUMAN_NEEDED.md` |
| How do I run the project? | `README.md` + `CLAUDE.md` / `AGENTS.md` |
| How does the system actually work? | `docs/architecture/` |
| What do I do when X breaks? | `docs/operations/<scenario>_runbook.md` |
| What's been measured / audited recently? | `docs/audits/` |
| What lesson did we learn (so we don't relearn it)? | `memory/feedback_<topic>.md` |
| What's the current methodology? | `docs/methodology/` |

---

## Project-instruction filename per AI tool

The methodology is tool-agnostic; only the project-instruction filename differs:

| AI tool | Filename it reads |
|---|---|
| Claude Code (Anthropic) | `CLAUDE.md` |
| OpenAI Codex CLI | `AGENTS.md` |
| Google Antigravity | `AGENTS.md` or `.agent/instructions.md` |
| Cursor | `.cursor/rules/` or `.cursorrules` |
| Aider | `CONVENTIONS.md` |
| Continue.dev | `.continue/context.md` |

If your team uses multiple tools, see the README's "AI tool support" section for symlink vs duplicate-maintenance trade-offs.

---

## Adaptations

- **Skip folders you don't need.** Most small projects don't need `audits/` or `operations/` initially — add when warranted.
- **Adjust `docs/methodology/` location** if you want to symlink to a pinned methodology version rather than vendor it.
- **Replace `BL-####` with a project-prefix** if you maintain multiple projects (e.g., `PROJ1-0428`). Stay monotonic regardless.
- **Use a different instruction-file name** if your tool calls for one (see table above).
- **Drop `TEST.md`** at the epic level if your testing lives in `tests/` and the epic doesn't need standalone scenarios.

---

## What this convention deliberately does not include

- **Project-specific source-code layout** (`src/`, `apps/`, packages, etc.). The methodology stays out of code organization — that's a stack decision.
- **CI/CD configuration files** (`.github/workflows/`, `.gitlab-ci.yml`). Tool-specific and orthogonal.
- **External-tracker integration** (Jira, Linear, GitHub Issues). If your team uses an external tracker as the authoritative backlog, this folder structure is irrelevant for backlog files; the rest still applies.
- **Specific test framework conventions.** `tests/` is named generically; the framework's own conventions apply inside.

---

For the methodology this template supports, see [methodology/00_README.md](../methodology/00_README.md).

For the conceptual diagrams of how the layers fit together, see the [main README](../README.md).
