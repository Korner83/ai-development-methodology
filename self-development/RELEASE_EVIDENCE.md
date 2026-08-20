# Release evidence — the commands behind every published number

**Why this file exists.** Release entries in [`CHANGELOG.md`](../CHANGELOG.md) state counts: links checked,
lines per doc, tags versus releases. Until 2026-08-20 those numbers came from a checker that lived on one
machine and was never committed, so **no reader could reproduce a single one of them** — and the same
count error shipped three releases running. That is audit finding F-08, and it is the root cause of F-11.

**What this file is not.** A committed validator was considered and **declined**: this repository ships no
runnable elements. So these are commands a person runs, not a control that fails a build. **It is weaker
than CI on purpose**, and the weakness is real — nothing here stops a release that skips the step. What it
buys is that any reader can check the claim, which is the property that was actually missing.

Precedent for the shape: [`SECURITY.md`](../SECURITY.md) already tells readers to run `gitleaks detect`
themselves rather than asking them to trust a badge.

---

## Two ordering rules that produced real errors

1. **Take every count after the final edit.** A number measured mid-change is stale before it ships. This
   is the v1.30.1 correction, and it exists because a release recorded a clean count and then changed a
   derived artifact.
2. **A tag count taken before the tag exists is wrong the moment it is pushed.** Write the arithmetic, not
   the total: *"N prior tags; this release's annotated tag makes N+1."* The v1.31.0 entry names this
   failure mode in the same sentence that commits it. See
   [`09`](../methodology/09_git_workflow.md#counts-in-a-release-entry-carry-an-as-of-marker).

---

## The commands

Run from the repository root, on the final tree.

**Skill frontmatter parses** — the check v1.31.0's conformance pass did not run:

```bash
python -c "import yaml;t=open('skills/ai-dev-methodology/SKILL.md',encoding='utf-8').read();d=yaml.safe_load(t.split('---')[1]);print(sorted(d), len(d['description']))"
```

**Line counts for every capped file:**

```bash
for f in methodology/*.md templates/*.md README.md CHEATSHEET.md AGENTS.md skills/ai-dev-methodology/SKILL.md; do printf "%6d  %s\n" "$(wc -l < "$f")" "$f"; done
```

**Markdown file count and total lines** — the two figures in the README's repo-stats line:

```bash
git ls-files '*.md' | wc -l
git ls-files '*.md' | xargs wc -l | tail -1
```

**Tag and release parity** — run *after* pushing the release tag:

```bash
grep -c '^## v' CHANGELOG.md
git tag | wc -l
```

**Version pins all equal** — seven hand-maintained sites; any mismatch is a stale pin:

```bash
grep -rn "v1\.[0-9]\+\.[0-9]\+" README.md CHEATSHEET.md STATUS.md skills/ai-dev-methodology/SKILL.md | grep -v CHANGELOG
```

**No executable files** — the no-runnable-elements stance, checked rather than asserted:

```bash
find . -path ./.git -prune -o -type f \( -name '*.py' -o -name '*.sh' -o -name '*.js' -o -name '*.ps1' \) -print
```

**Every workflow action pinned to a full SHA:**

```bash
grep -rn 'uses:' .github/workflows/
```

**Rendering links and anchors.** No one-liner does this honestly — it needs a parser that skips fenced
blocks and inline code, resolves relative paths, and slugs headings GitHub-style (each space becomes one
hyphen, so `— ` yields a double hyphen). Any such parser will do; what matters is reporting the method
alongside the number, because two parsers disagree on adopter-relative links. **The template files carry
55 links that resolve only after install** — count them separately or the total looks broken.

---

## The line budgets that bind this repo

Until 2026-08-20 these lived only inside closed epic charters, where a contributor editing a file 14 lines
from its cap had no way to find them.

| File | Cap | Where it came from |
|---|---|---|
| Any `methodology/*.md` | **1,050** | E03's trim analysis — the soft cap that triggered splitting `09` |
| `README.md` | **350** | [P2](pillars/P2_doc_clarity.md) |
| `CHEATSHEET.md` | **100** | E05's charter, a hard exit criterion. Currently at 99 — one line of margin |
| `templates/ROLE_BRIEFS.md` | **200** | E08, self-imposed |
| Root `AGENTS.md` | **50** | E10, self-imposed |
| `skills/.../SKILL.md` | **500** | the Agent Skills format's own recommendation |

**None of these is enforced.** They are hand-checked budgets, and the cheatsheet spent eleven releases over
its cap before anyone noticed. Recorded here so the next contributor at least knows the number.
