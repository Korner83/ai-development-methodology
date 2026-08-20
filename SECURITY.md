# Security Policy

## What this repository is

This is a **documentation and methodology project** — markdown plus git, nothing else.

- **No executable code.** No JavaScript, Python, or other source to run.
- **No package dependencies.** No `package.json`, `requirements.txt`, lockfiles, or third-party packages in the delivered artifact.
- **No build step and no install scripts.** Nothing runs on clone, install, or open. There are no `preinstall` / `postinstall` / `prepare` hooks because there is no package manifest at all.
- **No telemetry, no network calls, no credential collection.** The repo does not phone home, read your environment, or touch your secrets.
- **One workflow, and it is the whole CI dependency surface.** A secret scan ([`.github/workflows/gitleaks.yml`](.github/workflows/gitleaks.yml)) runs with `contents: read`. It uses two third-party actions — `actions/checkout` and `gitleaks/gitleaks-action` — **pinned to full commit SHAs rather than to mutable major tags**, because a major tag can be repointed by its owner and this job passes the repository `GITHUB_TOKEN` to the second one. This runs in *this* repository's CI only; it is not part of what an adopter clones or installs.

**The delivered artifact executes nothing on clone or open and has no package dependencies**, so the usual code-scanning tooling (CodeQL, dependency audits, SBOMs) has nothing to analyze. That is a narrower claim than "no supply chain": the two pinned GitHub Actions above *are* a dependency surface, they are simply this repository's rather than an adopter's, and Dependabot's `github-actions` ecosystem is the tool that applies to them. The main risk surface remains the *instructional content* itself.

## Scope

Security concerns that are in scope for this project:

- **Prompt-injection risks** in the methodology docs or templates — wording that could lead a downstream AI agent to treat untrusted content as instructions.
- **Unsafe agent instructions** — guidance that could cause an agent to take a destructive, secret-exposing, or gate-bypassing action.
- **Secret leakage** — credentials, tokens, or keys accidentally committed to this repository.
- **Misleading or malicious workflow instructions** that could harm a project adopting the methodology.

How the methodology itself defends against these is documented in [methodology/13_ai_safety_and_prompt_injection.md](methodology/13_ai_safety_and_prompt_injection.md).

## Reporting a vulnerability

Please report privately rather than opening a public issue. Email **polgarmiklos@gmail.com**.

Include what you can:

- A description of the issue and which files or prompts are affected.
- How to reproduce it (e.g. the input that triggers unsafe behavior).
- The potential impact.
- A suggested fix, if you have one.

This is a lean, solo-maintained reference artifact (see [STATUS.md](STATUS.md)): reports are read, but there is **no response SLA**. Critical issues — anything that could cause downstream harm — will be prioritized.

## How to verify the repository yourself

You do not have to take the statements above on trust:

1. **Inspect the tree.** Confirm there is no `package.json`, no source files, no install scripts — only markdown and the one read-only workflow.
2. **Run a secret scan.** `gitleaks detect --no-banner` should report zero findings. (The repo runs this on every push and pull request.)
3. **Review the safety doc.** [methodology/13_ai_safety_and_prompt_injection.md](methodology/13_ai_safety_and_prompt_injection.md) states the rules the methodology gives downstream agents; the templates ([`templates/CLAUDE.md`](templates/CLAUDE.md), [`templates/AGENTS.md`](templates/AGENTS.md)) carry the same rules in the form agents actually load.

## A note for adopters

This methodology governs *which instructions an AI agent obeys.* It does not sandbox your agent's runtime or scan your project's dependencies — those remain your project's responsibility, layered on top. Adopting the methodology is a strong default for safe AI-assisted development, not a substitute for your own security controls.
