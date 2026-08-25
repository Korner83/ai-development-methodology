# E10 — External baseline audit remediation — Archive

_Completed and rejected items. Archives are append-only once released; this epic is unreleased, and these
entries were condensed on 2026-08-20 from a first draft whose per-item write-ups were longer than the doc
changes they described._

**All fourteen items closed, shipping together in `v1.32.0`.** Every Critical and High finding from the
external audit is addressed — the audit's own "must fix before relying on multi-agent or safety-critical
operation" list — plus the supply-chain claim and this repository's missing instruction file.

**Shared verification.** On the final tree, counts taken after the final edit:

- Skill frontmatter: `yaml.safe_load` returns `['description', 'license', 'name']`; `description` 472 of
  the format's 1,024 characters, unchanged; body 135 lines against a 500-line recommendation. Before the
  fix it raised `ScannerError` at line 3, column 212.
- Repo-wide rendering-link and anchor check: **1,151 relative links across 127 markdown files, zero
  broken.** 55 are adopter-relative links in the templates that resolve only after install — the same 55
  the external audit isolated independently.
- Line caps: `04_backlog_items.md` **1,036 of 1,050, net change 0** as chartered; `09` 815, `10` 791,
  `05` 565, `11` 357, `13` 146, `00` 547; `README.md` 333/350, `CHEATSHEET.md` 99/100, `ROLE_BRIEFS.md`
  199/200, root `AGENTS.md` 49/50. Zero executable files; both `uses:` refs are 40-character SHAs.
- Enum parity: no file carries a proper subset of the eight `Test` values; `not-run` appears nowhere.
- No example records `pass` on a change whose required verification level is unreached.
- `grep -rn "solo-maintainer" skills/` returns nothing. Both workflow `uses:` refs are full commit SHAs.
- The root `AGENTS.md` safety block was compared byte-for-byte against the canonical block in `13`.
- 46 tags **as of the release commit**; this release's annotated tag makes 47, matching 47 changelog headings.

**Lock handling, recorded because it is what BL-0047 is about.** These items were worked in one session
on a feature branch, so their `Lock:` values were only ever visible there. Under this methodology's own
PR-only rule, a second contributor pulling trunk could not have seen them. The protocol was followed
exactly and provided nothing. **F-01 was reproduced by the work that fixes it.**

---

### BL-0039 — Quote the skill `description` so the frontmatter parses

`Status: done` · `Test: pass` — parse run, command and output above · **F-04**

**Files:** `skills/ai-dev-methodology/SKILL.md` line 3.

The description was an unquoted plain scalar containing `question: sizing`; a plain scalar in a block
mapping cannot carry a colon-space. **An adopter on a spec-compliant loader could not install the skill
at all.** Fixed by quoting, so the trigger text is byte-identical inside the quotes.

**The lesson is upstream of the fix.** v1.31.0 shipped a field-by-field Agent Skills conformance check on
this exact frontmatter and recorded `description` as "472 of 1024" — it measured the value's length and
never invoked a parser. *A conformance check that does not run the parser is an assertion wearing a
check's clothing.*

---

### BL-0040 — Retire the solo-maintainer exception; correct the skill's authority claim

`Status: done` · `Test: pass` — grep returns nothing; precedence reads against `00`'s ladder · **F-04**

**Files:** `skills/ai-dev-methodology/SKILL.md` lines 17, 47, 121.

The skill permitted a "solo-maintainer exception" to PR-only work that `STATUS.md` had retired and that
`00` forbids as a hard rule, and declared that a project's instruction file wins outright — inverting the
authority ladder. It now defers to the ladder: the instruction file outranks this skill's general
guidance, **not** the hard rules.

**Pairs with BL-0046.** The skill granted `CLAUDE.md`/`AGENTS.md` override authority while `13` trusted
those filenames regardless of provenance. Either fix alone leaves a file arriving in an unreviewed PR
able to outrank a hard rule.

**One criterion was accepted rather than met.** It read "net-negative in lines"; the file is 135 lines
before and after, because both exceptions were parentheticals inside existing lines. Held at
`under-review` rather than closed, because rewriting a frozen-intent criterion to match what was built is
the move `04` forbids. **Maintainer decision: the criterion measured the wrong thing** — what it meant was
*removes content, adds no new rule*, and that held. Recorded because the cheap version of this — quietly
reading "net-negative" as "didn't grow" — is the failure mode this whole epic exists to repair.

---

### BL-0041 — Correct the count claims forward; add an as-of marker convention

`Status: done` · `Test: pass` — counts re-derived from the tree · **F-11**

**Files:** `methodology/09_git_workflow.md` (+11, release-tagging section), `CHANGELOG.md` (new entry;
the historical line untouched).

A release entry stating a live repository total in the present tense is false the moment its own tag is
pushed. Three times in the same lineage: 44/44, 45/45, and the tree is 46/46 — and **the v1.31.0 entry
diagnoses the failure mode by name in the same sentence that commits it.** Counts now carry an as-of
marker, anything the release increments is stated as arithmetic, and corrections go forward because a
published entry is history.

**Stated limit: this is a convention, not a control.** With the checker declined, nothing enforces it.

---

### BL-0042 — Refresh the stale self-development enumerations

`Status: done` · `Test: pass` — every figure re-read from the tree · **housekeeping**

**Files:** `self-development/backlog/README.md`, `EPICS.md`, `epics/E05-cheatsheet/README.md`.

The backlog README described E01–E08, a highest ID of `BL-0033` and a WIP cap of 1 — stale by two epics,
twenty-two IDs and a cap. The rollup called the cheatsheet 144 lines after v1.31.0 trimmed it to 99.
E05's charter still said "~80 lines", a figure corrected in two sibling files and missed there.

The structure diagram is the part worth naming: it drew the **four**-file epic shape as if that were the
convention, so the repo contradicted `03`'s five-file rule **and the filesystem matched the diagram
rather than the methodology.**

---

### BL-0043 — Reconcile the `Test` enum everywhere an agent copies it

`Status: done` · `Test: pass` — every enumeration site returns all eight values or a link · **F-02**

**Files:** `methodology/04_backlog_items.md` (line 103, one row widened in place, net 0),
`00_README.md` (line 289), `07_definition_of_done.md` (Gate 6 + the pasteable checklist),
`03_epics.md`, two `examples/` files, `README.md` (the flow diagram).

Eight canonical values; the frontmatter table an agent pastes listed four, and the index's table the same
four — omitting `manual-verified` and `n/a`, **two of which the index's own hard rule depends on twelve
lines later.** Gate 6 said `pass` and "never any other value" immediately before the hard rule granting
two exceptions. Gate 6 now states no rule at all; it points at the one definition.

**The no-subset rule found drift the audit had not:** `03_epics.md` claimed its epic `TEST.md` column
"mirrors the Test enum" and then listed seven values including **`not-run`, which exists nowhere in the
enum** — inherited into three rows of the example project.

---

### BL-0044 — Generalise the level-vs-`pass` rule past L2

`Status: done` · `Test: pass` — no example records `pass` with an outstanding required level · **F-03**

**Files:** `methodology/10_testing_and_verification.md`.

The examples sanctioned `Test: pass (L3) — cross-AI validated, awaiting user gate` while new features
require L4 and levels are cumulative. **`Test:` is a machine-readable token and the DoD closes an item
from any value beginning with `pass`** — the prose after the dash does not hold the gate. An agent that
copied the example, applied the hard rule, released the lock and archived the item would have followed
the documentation exactly and closed an item whose required gate never ran.

Now `partial (L3; L4 pending)` — a value the enum already had and nothing pointed at — and the rule
generalises to every step. **The DoD's `pass → done` rule is untouched; it was never the defect.**

---

### BL-0045 — Split destructive operations into two disjoint classes

`Status: done` · `Test: pass` — every operation maps to one class; legend and handling text agree · **F-06**

**Files:** `methodology/11_human_roles.md`, `09_git_workflow.md`, `13_ai_safety_and_prompt_injection.md`,
`templates/AGENTS.md`, `templates/CLAUDE.md`.

Three incompatible framings on an irreversible boundary: "the AI doesn't act, period", "agents surface,
never execute", "explicit per-operation authorization", and "never *autonomously*".

**`approval-gated`** — the agent may execute after an explicit, scoped, per-operation yes that does not
carry to the next one. **`agent-prohibited`** — a human executes, and a yes authorizes *the human to
proceed*, not the agent to act. The line is **blast radius, not danger**: a destroyed working tree costs
an afternoon and the reflog often has it; a dropped production table does not.

**This resolves the authority-ladder conflict without amending the ladder.** "User direction overrides
everything" and "the AI doesn't act, period" both survive, because the prohibited class is defined by
*who acts* rather than by who consents — there is nothing for consent to unlock.

**Six git rows loosened** from prohibited to gated (`reset --hard`, `checkout --`/`restore`, `clean -fd`,
`branch -D`, `worktree remove --force`, `rm -rf <repo>`). Bounded: the production subset did not move, and
the wording those rows moved *to* is what `templates/AGENTS.md` has shipped since before the audit.
**`templates/CLAUDE.md` gained the rule it never had** — its absence had been justified as "covered
implicitly by Claude Code's harness", an assumption about one vendor standing in for a safety rule.

---

### BL-0046 — Replace filename-based trust with provenance-based trust

`Status: done` · `Test: pass` — `13` conditions trust on provenance; both templates carry the rule · **F-05**

**Files:** `methodology/13_ai_safety_and_prompt_injection.md`, `templates/AGENTS.md`, `templates/CLAUDE.md`.

Methodology docs and the instruction file were trusted "by contrast", with nothing qualifying *which
version*. A contributor edits `AGENTS.md` inside their PR, an agent checks the branch out, the harness
auto-loads the modified file **before the diff is read**. No injection marker needed — the file is
believed because of where it sits.

Authority files are now read **from the reviewed base commit** when evaluating an untrusted branch. The
doc already made this argument one level lower — backlog items are untrusted "because anyone (or any
prior agent) can write them" — and had not applied it upward. **Rank is earned at review, not at the path.**

**A criterion that could not be met pointed at something true.** It asked for the templates' safety
blocks to be verified by diffing fenced regions; the templates carry the rules in prose, not as a copy of
the fenced block. So `13`'s claim that the block "is already embedded in" both templates was itself
imprecise. **That claim is now corrected** to say the templates carry an adaptation.

---

### BL-0047 — Make the lock's authority conditional on visibility

`Status: done` · `Test: pass` — the claim matches the mechanism; no hard rule amended · **F-01, Critical**

**Files:** `methodology/05_locks_and_parallel_work.md` (+65), `09_git_workflow.md`, `STATUS.md`.

Three sentences that could not all be true: the lock "is the authority" preventing collision; lock commits
live on the active branch, "often the feature branch"; every change lands on the trunk via PR. **A
contributor pulling the trunk cannot see a lock on someone else's unmerged branch.** Two agents branch
from the same state, both read `Lock: —`, both push to *different* refs — both succeed, because git
rejects a non-fast-forward only when two writers update the **same** ref. Both do the work; the conflict
appears at merge, after the duplication.

The normative rule is now **a lock has authority only where it is visible**, and the default protocol is
named for what it is: cooperative signalling with late collision detection. The opt-in **shared-ref
protocol** makes the strong claim true — every lock write targets one shared ref, the loser's push is
rejected non-fast-forward, and **that rejection is the compare-and-swap.** No service, no dependency.

**`09`'s cross-reference was backwards** and is inverted: it claimed branch protection "ensures no one
bypasses the lock", when branch protection is precisely what keeps acquires off the trunk and therefore
what makes the lock invisible. `STATUS.md`'s battle-tested claim is qualified to the form actually
exercised.

**Rejected:** demote-only (leaves adopters informed and with no path to exclusion) and mandatory
trunk-anchored acquisition (amends a hard rule adopters have pasted into their own instruction files,
for a major version, on behalf of a guarantee nobody has asked for — because there are no adopters).

---

### BL-0050 — Pin the actions to SHAs; narrow the no-supply-chain claim

`Status: done` · `Test: pass` — no claim in `SECURITY.md` or `README.md` is contradicted by `.github/` · **F-07**

**Files:** `.github/workflows/gitleaks.yml`, `SECURITY.md`, `README.md`, `methodology/13`.

`SECURITY.md` said there were no dependencies and that code-scanning tooling did not apply because there
was nothing to analyse; the README said there was no code or supply chain to scan. The one workflow pulled
`actions/checkout@v4` and `gitleaks/gitleaks-action@v2` **by mutable major tag** and passed the repository
token to the second, on every push and pull request. A repointed tag runs attacker code with that token.

Both are now full commit SHAs with version comments — `actions/checkout@11d5960a…` (v4) and
`gitleaks/gitleaks-action@ff98106e…` (v2, resolved through its annotated tag object to the commit). **No
workflow was added and no script was committed**, per the maintainer's no-runnable-elements decision;
this is two `uses:` lines.

**The claims were narrowed rather than deleted.** The clone-safety property is real and worth stating
precisely: *the delivered artifact executes nothing on clone or open and has no package dependencies.*
What is no longer claimed is the absence of a supply chain — the two actions are one, and it is this
repository's rather than an adopter's. Deleting the CI to preserve the sentence would have been the worse
trade. Re-pinning is folded into the semi-annual currency pass rather than given a new cadence.

---

### BL-0051 — Add this repository's own root instruction file

`Status: done` · `Test: pass` — file exists at 49 lines; safety block byte-identical to the canonical one · **F-09 (part)**

**Files:** `AGENTS.md` (new, 49 lines).

`13` tells every adopter to paste the safety block into a project instruction file. **This repository had
none**, so agents working here never loaded the safety checklist it publishes — and the instruction at the
heart of the AI-safety doc described something the repo did not do.

**Held to ≤ 50 lines and almost entirely links.** The one duplication is the block the methodology itself
instructs adopters to paste verbatim; it was verified byte-identical to the canonical copy rather than
retyped. Project-specific overrides are linked to `self-development/backlog/README.md`, not restated —
a second copy here would be the drift the audit found everywhere else.

**It came in at 51 lines and was trimmed to 49 rather than the budget being raised.** Same shape as
BL-0040's criterion, opposite resolution, and cheaper: two lines of merging beat a maintainer decision.

---

### BL-0048 — Name the surfaces that restate each rule

`Status: done` · `Test: pass` — every row's canonical target and restating surfaces verified by grep · **F-08 (part)**

**Files:** `methodology/00_README.md` (+19, new section under the constitution check; 528 → 547 of 1,050).

Before this, **the only propagation instruction in the entire corpus covered exactly one rule** — a note
that the precedence ladder is restated in `01` and `02`. Nothing said that changing the `Test` enum means
touching six other files, which is why five hard-rules lists existed with five different memberships.

An eight-row table names, per rule, the canonical file and every surface that restates it, with one
governing line: **a surface reproduces the rule in full or carries none of it and links.** A partial
restatement is the failure mode, because it reads as complete.

**Kept to a map rather than a register file.** With the checker declined, a separate machine-readable
register would be a second source of truth that drifts — the exact thing being fixed. It sits beside the
hard-rules table, where a contributor editing a canonical rule will meet it, and **adds nothing to obey.**

---

### BL-0056 — Sweep the never-checked rules and criteria; decide each

`Status: done` · `Test: pass` — every convention v1.25.0 → v1.31.0 listed with its exercise record; E10's acceptance rows run · **maintainer request**

**Files:** `self-development/evaluations/2026-08-20-convention-sweep.md` (new),
`self-development/backlog/epics/E10-external-audit-remediation/TEST.md` (rows run),
`methodology/04_backlog_items.md` (one residual lock claim, found by AT-02).

**The number is the finding: 6 of 16 conventions have ever been exercised, and 3 of those for the first
time on 2026-08-20** — by the epic responding to the audit. Two of the unexercised ones *could not* have
been: the context-integrity canary and the house-verbosity setting both require a project instruction
file, and this repo had none until BL-0051 added one today.

**Unexercised is not wrong**, and the sweep says so — most are cheap, live in docs a reader consults
rather than memorises, and several were rated strengths by the audit. **The finding is that this repo has
been generating rules faster than it generates evidence.**

**Net effect on doc size: zero**, which is worse than the item hoped for and is recorded rather than
dressed up. Both retirement candidates need a maintainer decision, and one costs a major version.

**Running E10's own acceptance rows earned its place.** AT-02 found an unqualified *"the `Lock:` field is
the authority"* still sitting in `04`'s cross-reference list after `05` had been corrected — **in a link
description**, which is exactly where the audit said drift hides. Fixed in place; `04` stayed at 1,036.

**Two rows were cut rather than failed** — the CI-checker row and the cross-AI row, whose subjects were
removed by decision on 2026-08-20. A criterion whose subject no longer exists is deleted with its reason;
carrying it would misreport a decision as a defect.

**Two decisions are open and belong to the maintainer**, recorded in the sweep: retiring the
house-verbosity setting (a removed section ⇒ **MAJOR**), and whether the root `AGENTS.md` should carry the
context-integrity canary. The sweep recommends adding the canary — the alternative is a repo publishing a
safety convention it declined to use, which is the shape of F-09.

---

### BL-0049 — Write down the release-evidence commands

`Status: done` · `Test: pass` — every command in the file was run on this tree while producing this release · **F-08**

**Files:** `self-development/RELEASE_EVIDENCE.md` (new), linked from `backlog/README.md`.

Release entries stated counts produced by a checker that lived on one machine and was never committed, so
**no reader could reproduce a single published number.** A committed validator was the obvious fix and was
declined: this repository ships no runnable elements.

What ships instead is the commands, in markdown, runnable by anyone. **It is weaker than CI and the file
says so in its second paragraph** — nothing stops a release that skips the step. What it buys is the
property that was actually missing: a reader can check the claim.

**It also gives the line budgets a home.** 1,050 / 350 / 100 / 200 / 50 / 500 existed only inside closed
epic charters, so a contributor editing a file fourteen lines from its cap had no way to discover it. The
cheatsheet spent eleven releases over its cap before anyone noticed, which is what that costs.

---

### BL-0052 — Publish the adoption profile; complete the five-file epic shape

`Status: done` · `Test: pass` — all ten epic folders carry five files; every methodology component mapped · **F-09**

**Files:** `self-development/ADOPTION_PROFILE.md` (new), nine new `TEST.md` files across E01–E09,
`self-development/backlog/README.md`, `README.md` (one link).

The repo presented `self-development/` as the methodology applied to itself while **the degree of partial
adoption was nowhere stated** — so a brownfield adopter could copy an omission and think it was the
convention.

**The profile opens with the omissions**, deliberately: no committed checker, no `memory/` directory of its
own, no context-integrity canary, no house-verbosity setting, and — the largest — **a docs-only instance
cannot exercise the UI-verification and testing chapters at all.** Then the adaptations, each with its
deviation named, including the WIP cap that has never been contended and the five closures that ran
charter-to-close inside a single session.

**Nine `TEST.md` files were created empty-but-present**, each pointing at the real verification record in
its `ARCHIVE.md`. **No acceptance rows were reconstructed.** Back-filling scenarios that never ran would be
fabricated evidence in a repository audited for asserting checks it had not performed — an empty table with
an honest pointer is worth more than a full one that invents history. `03_epics.md` was not weakened to
grandfather the historical shape; the rule stood and the practice caught up.
