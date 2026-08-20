# E10 — External baseline audit remediation — Test scenarios

_Epic-specific acceptance + regression scenarios. This backlog carries no cross-epic `TEST_BACKLOG.md`;
that surface is optional per [`03`](../../../../methodology/03_epics.md) and this repo has never needed one._

**This is the first `TEST.md` in the self-development backlog.** Its absence across all nine prior epics
is audit finding F-09; BL-0052 backfills the rest.

**What "test" means for a documentation change.** There is no runtime, so every row below is a
reproducible check against the tree — a parse, a grep, a count. **A row whose result is a claim rather
than an output does not count as run**, which is the defect class this epic exists to repair.

## Acceptance tests for exit criteria

Run 2026-08-20 on the working tree, counts taken after the final edit.

| ID    | Scenario | Status |
|-------|----------|--------|
| AT-01 | Every chartered item resolved — shipped, deferred, or rejected with reasoning | partial — 12 of 14 closed; BL-0049 and BL-0052 open |
| AT-02 | For each finding, one governing statement; every audit-cited line is it or links to it | pass — greps for subset enums, competing destructive framings, unconditional lock authority and "solo-maintainer" all return clean. One residual lock claim was found by this row at `04:993` and fixed |
| AT-03 | Skill frontmatter loads under strict `yaml.safe_load` | pass — returns `['description', 'license', 'name']`; 472 of 1,024 chars |
| AT-04 | The lock-mechanism decision is recorded with its rejected options and their costs | pass — D1 recorded in BL-0047 and in `ARCHIVE.md` |
| AT-05 | ~~Checker runs in CI and is required by the branch ruleset~~ | **cut** — the checker was declined on 2026-08-20; the criterion's subject no longer exists |
| AT-06 | A second session reproduces every published number from a clean clone | not-tested — blocked on BL-0049, which writes the commands down |
| AT-07 | ~~Cross-AI findings-verification ran on the assembled diff~~ | **cut** — the gate was removed from this epic on 2026-08-20 |
| AT-08 | Markdown and config only; no executable file added | pass — repo-wide `find` for `*.py`/`*.sh`/`*.js`/`*.ps1` returns nothing |
| AT-09 | Every touched doc under its cap | pass — `04` **1,036/1,050, net change 0**; `09` 815, `10` 791, `05` 565, `11` 357, `13` 146; `README.md` 333/350, `CHEATSHEET.md` 99/100, `ROLE_BRIEFS.md` 199/200, `AGENTS.md` 49/50 |
| AT-10 | A fresh read-only re-audit returns no Critical and no High | not-tested — runs against the final tree after the release |

**Two rows were cut rather than failed.** AT-05 and AT-07 tested things that were deliberately removed —
the committed checker and the cross-AI gate. **A criterion whose subject no longer exists is deleted with
its reason, not carried as a permanent failure**; carrying it would misreport a decision as a defect.

**AT-02 earned its place.** It is the only row that found something: an unqualified "the `Lock:` field is
the authority" survived in `04`'s cross-reference list after `05` had been corrected. The finding was in a
*link description*, which is exactly where the audit said drift hides.

## Regression scenarios to protect

Hand-run, with the commands recorded — **there is no CI check behind any of these**, per the
no-runnable-elements decision. That is the standing weakness of this list and the reason it is written
down at all.

| Area | Scenario | Last verified |
|------|----------|---------------|
| Skill portability | Frontmatter parses under strict YAML; `name` matches its parent directory | 2026-08-20 |
| State contract | No file carries a proper subset of the eight `Test` values | 2026-08-20 |
| Verification levels | No example shows `pass` on a change whose required level is unreached | 2026-08-20 |
| Autonomy classes | Every destructive operation maps to one class; legend and handling text agree | 2026-08-20 |
| Trust boundary | Both templates carry the provenance rule; the root block matches the canonical one byte-for-byte | 2026-08-20 |
| Lock semantics | The authority claim reads the same in `05`, `04`, `09`, `CHEATSHEET`, the skill and `STATUS.md` | 2026-08-20 |
| Line budgets | All five caps hold | 2026-08-20 |
| Release evidence | Changelog headings equal `git tag` count **after** the tag is pushed; version-pin sites equal | pending — at release |
| Supply chain | Every `uses:` is a full 40-character SHA; no claim contradicts `.github/` | 2026-08-20 |
| Self-application | All epic folders carry five files; the backlog README's diagram matches the filesystem | pending — BL-0052 |

## Manual scenarios (operator-driven)

- **The paste test.** Copy each pasteable block — the DoD checklist, the safety block, the item skeleton —
  into an empty file and check it stands alone. **These are the surfaces every copy-surface finding lived
  on.** Run 2026-08-20 for the DoD checklist and the safety block; both now carry their exceptions.
- **The adopter walk.** Follow the install instructions from a clean clone on a spec-compliant loader.
  This is what F-04 broke and what nobody had run.
