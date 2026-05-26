# Tech Choices

What's in scope, what's deliberately out. This is the tech-stack section of the brief — the choices made before any planning starts.

## In scope (the substrate)

### Substrate

- **Markdown** as the only content format. Everything readable in plain text on GitHub.
- **Git** as the only state mechanism. Branches, commits, tags, releases — all standard git operations. No proprietary state outside git.
- **Mermaid diagrams** for visual content. Renders natively on GitHub; no image files to maintain; lives as text in git. (Per the methodology's own "markdown + git only, no SaaS" framing.)

### Hosting and presentation

- **GitHub** as the hosting platform. Choices:
  - `Korner83/ai-development-methodology` is the canonical repo.
  - Public visibility (already PUBLIC).
  - Discussions enabled (already).
  - Pages enabled (already; deploys from main branch root).
  - Releases generated per tagged version.
  - Topics (13 currently): `methodology`, `ai-agents`, `agentic-coding`, `claude-code`, `cursor`, `agents-md`, `llm`, `software-development`, `development-workflow`, `definition-of-done`, plus auto-added ones.
  - `.github/FUNDING.yml` present (Sponsor button active once GitHub Sponsors approves enrollment).

### Maintainer tooling

- **`gh` CLI** for repository automation (releases, PR creation, issue management). Used by the maintainer; not required for adopters.
- **`git` standard CLI** for version control. Maintainer uses git bash on Windows.
- **PowerShell + Bash** for ad-hoc verification scripts (line counts, link checks). One-shot, not persisted.
- **Plain text editor** of the maintainer's choice for writing markdown.

### Methodology conventions adopted

- **Conventional commits** for commit messages (`feat`, `fix`, `chore`, `docs`, `refactor`, `test`, `release`, `perf`, `revert`).
- **Annotated tags** for releases (`git tag -a vX.Y.Z`).
- **SemVer 2.0** for version numbers, per [methodology/09_git_workflow.md "Release tagging"](../../methodology/09_git_workflow.md).
- **Two-step release push** (`git push origin main` then `git push origin vX.Y.Z`).
- **CHANGELOG.md** in keep-a-changelog format (Unreleased section + reverse-chronological releases).
- **Squash-merge** for PRs to main, when a PR-based workflow is in effect. (Currently uses direct-to-main per the documented exception in STATUS.md.)

## Out of scope (deliberate)

### Build / CI

- **No CI for the docs.** Markdown doesn't need a build pipeline. The repo's GitHub Pages deploy is the only automation; everything else is on-demand.
- **No automated link-checking.** Manual quarterly audit (per the repo health audit pattern) is sufficient at this scale.
- **No automated changelog generation.** CHANGELOG.md is hand-written; that's part of the methodology's "write down what changed and why" discipline.
- **No automated formatting / linting** for markdown. The variation across markdown linters is high; manual review at PR time is the gate.

### Distribution infrastructure

- **No translation infrastructure** (Crowdin, Weblate, custom i18n). Decided against; browsers auto-translate and drift is the killer. (See [maintainer's decision in conversation history](../../CHANGELOG.md).)
- **No multi-language doc versions.** Same reason.
- **No newsletter / email list.** Discussions thread serves the same purpose.
- **No custom domain.** `korner83.github.io/ai-development-methodology` is sufficient.
- **No custom Pages theme.** Default Jekyll theme works.
- **No analytics on the docs** beyond what GitHub provides natively.

### Tooling for the methodology itself

- **No CLI for the methodology.** The methodology is docs; adopters copy-paste templates and edit. Building a CLI would entangle the methodology with a maintenance burden it doesn't need and a vendor lock-in it explicitly avoids.
- **No methodology-specific linters / validators.** The methodology is descriptive, not enforced.
- **No web UI / dashboard for backlog browsing.** Adopters use their own preferred tools.

### Adopter expectations (NOT requirements)

The methodology assumes adopters bring their own:

- AI coding tool (any of: Claude Code, OpenAI Codex, Cursor, Aider, Continue.dev, Google Antigravity, or others that read a project-instruction file).
- Git hosting (GitHub, GitLab, Bitbucket, Forgejo, Gitea — anything that supports markdown rendering and PRs).
- Programming language and stack of their choosing.
- Test framework of their choosing.
- Editor / IDE of their choosing.

The methodology stays out of these choices. Adopters who want guidance on tool selection look elsewhere.

## Why these choices

### Why markdown + git only

- **Survives indefinitely.** Markdown is plain text; git is mature, multi-implementation, won't be deprecated. Any SaaS or proprietary tooling locked into the methodology would be a liability when (not if) that vendor disappears.
- **Greppable.** Every artifact is searchable from the command line. AI agents can navigate without specialized parsers.
- **Vendor-neutral.** No commercial relationship with any AI vendor; the methodology works equally with all of them.
- **Cheap.** Zero hosting cost beyond git hosting itself (free on GitHub). Zero per-user cost. Zero per-feature cost.

### Why GitHub specifically (not GitLab / Forgejo / etc.)

- Where the audience is. AI-coding tool integrations target GitHub first.
- Best Mermaid rendering across hosting platforms.
- Discussions feature is mature.
- Pages, Releases, Issues, Discussions all in one platform.
- Adopters can fork and use any git hosting they prefer; the canonical repo just lives on GitHub.

### Why CC BY 4.0 (briefly; full reasoning in [06_distribution.md](06_distribution.md))

- Built for documentation and creative works.
- Permissive (commercial use OK).
- Attribution is the only obligation.
- Widely recognized outside software context.

## Tech decisions to revisit (someday)

If/when the methodology moves to "shared infrastructure" mode (per [06_distribution.md](06_distribution.md)):

- **Branch protection on main.** Currently the documented direct-to-main exception applies.
- **PR-based workflow.** Currently direct-to-main; would shift to PR for any change.
- **Possibly a status checks / CI** for basic markdown sanity (broken links, frontmatter validity). Only worth the overhead at multi-contributor scale.
- **Consider a `docs/` rename of `methodology/` and `templates/`** if the convention shifts in the broader ecosystem. Currently the at-root layout works.

Not adopting these now is deliberate. Each is overhead that's not justified at solo-maintainer scale.

## What changes about the tech surface over time

- **The methodology itself stays markdown + git forever.** That's the load-bearing decision.
- **The presentation layer might evolve.** GitHub Pages today; possibly a docusaurus-style site at scale; possibly something else if the ecosystem shifts. The content stays markdown regardless.
- **The maintainer's tooling might evolve.** Different IDE, different shell, different scripts — adopters won't see this.
- **The CI surface might appear.** Only if/when contributor base demands it.

The principle: the substrate is permanent; everything above the substrate is adjustable.
