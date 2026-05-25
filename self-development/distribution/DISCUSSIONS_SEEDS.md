# GitHub Discussions seed threads

_Maintainer: enable Discussions in repo Settings → General → Features → Discussions. Then create the 3 starter threads below using their content as the OP. These give visitors a place to land + a signal that the project is alive._

## Categories to enable

Create these category buckets (Settings → General → Features → Discussions → Categories):

| Category | Format | Purpose |
|---|---|---|
| **Announcements** | Announcement | Release notes, major changes — maintainer-only. |
| **Q&A** | Q&A | Adopter questions; answers get marked. |
| **Show & tell** | Discussion | Adopters share how they're using the methodology. |
| **Ideas** | Discussion | Methodology change proposals; feeds the T2/T3 backlog. |
| **General** | Discussion | Anything that doesn't fit elsewhere. |

## Seed thread 1 — Announcements

### Title

```
v1.16.0 — Multi-level scoring + expanded Test enum + first periodic deep-eval
```

### Body

```markdown
v1.16.0 shipped 2026-05-25. Highlights:

- **Multi-level scoring rubric** — the periodic deep-eval (`methodology/12`) can now score at project / pillar / epic / item level. Adopters pick what fits.
- **Expanded scoring areas** — 20 default areas covering UX, backend, database, auth/authz, security, perf, tests, a11y (design + testing), content, docs, CI/CD, ops, paywall, admin tools, i18n, privacy, brand, onboarding. AI can help define areas per project.
- **Test enum expansion** — adds `pending`, `manual-verified`, `partial`, `n/a` to the existing values. Test field also accepts free-form artifact refs (paths, PR numbers) after the enum value.
- **Status enum tolerance** — `todo` is an acceptable alias for `backlog`; `future` is acceptable for FUTURE.md items; `parked` is a project-specific option.

This was the first version shipped via the full self-improvement cycle introduced in v1.13.0 (tier matrix on patch branches with cross-AI diff-verification).

Full changelog: https://github.com/Korner83/ai-development-methodology/blob/main/CHANGELOG.md#v1160--2026-05-25
```

---

## Seed thread 2 — Q&A — How does this differ from [insert other methodology]?

### Title

```
FAQ — How does this differ from Spec Kit / BMAD / standard agile?
```

### Body

```markdown
A common opening question; collected answers here for easy reference.

**vs. GitHub Spec Kit:** Spec Kit centers the spec as the planning unit; this methodology centers the four-layer cascade (strategy → pillars → epics → items) and adds disciplines (working principles, DoD, memory) as overlays. Spec Kit and this methodology can compose — a project can use Spec Kit for spec authorship + this methodology for the planning + execution + autonomous-loop layers.

**vs. BMAD / multi-persona approaches:** BMAD uses defined personas (architect, dev, QA) as agent roles. This methodology is persona-agnostic — the same agent can play any role; the gating is by the artifact (lock + DoD + tier matrix), not by the agent's identity.

**vs. standard agile (Scrum, Kanban):** Agile assumes humans-only contributors who attend ceremonies. This methodology drops ceremonies and adds machine-readable artifacts (frontmatter fields, file-based locks, status enum) so AI agents can participate without translation. The four planning layers map roughly to epic/story/task hierarchies but with stricter cascade rules.

**vs. AGENTS.md / project-instruction-file standards:** AGENTS.md is one artifact this methodology uses (it's one of the 5 templates). The methodology is the broader set of practices + planning layers around it.

What questions are you arriving with? Add a comment; I'll update this thread.
```

---

## Seed thread 3 — Show & tell — How are you using it?

### Title

```
Show & tell — How are you using this methodology in your project?
```

### Body

```markdown
Seeding this thread so adopters have somewhere to share patterns.

If you're using the methodology — partially or fully — drop a comment with:

- **What your project shape is** (web app / CLI / library / regulated-industry / research / etc.).
- **Which methodology docs you found most useful** (00 / 06 / 07 / 12 / etc.).
- **Which you skipped or adapted heavily** — these are the signal for what doesn't fit your shape.
- **One pattern you wish was in the methodology** — feeds the T2 backlog for future releases.

I'll start: this methodology is applied to its own development under [`self-development/`](https://github.com/Korner83/ai-development-methodology/tree/main/self-development), and the fictional `tinker` example under [`examples/`](https://github.com/Korner83/ai-development-methodology/tree/main/examples) demonstrates the abstract → concrete mapping.
```

---

## After all three threads are posted

- **Pin "Announcements" + "Show & tell"** at the top of the Discussions tab.
- **Subscribe to all categories** as the maintainer so you see new threads.
- **Set a triage cadence** for Discussions per `methodology/12`'s feedback-triage flow (weekly during alpha is right at this stage).
- **Re-score "Adopter discoverability"** at the next deep-eval based on engagement metrics (threads per week; question-to-answer ratio; show-and-tell submissions).
