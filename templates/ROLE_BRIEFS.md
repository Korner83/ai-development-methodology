# Role Briefs

Short paste-able prompts for the phases of work that have documented rules but no prompt of their
own. Two phases already have one — [`AGENT_KICKOFF.md`](AGENT_KICKOFF.md) for setting up a new
project, [`AUTONOMOUS_LOOP.md`](AUTONOMOUS_LOOP.md) for long unattended runs. These six cover the
rest.

**A brief is a stance, not a persona.** It says what posture the phase requires and points at the
doc holding the rules. It deliberately does not restate those rules: a brief that repeats a rule
becomes a second copy that goes stale silently, which is the failure
[`07_definition_of_done.md`](../methodology/07_definition_of_done.md#when-all-the-docs-disagree-the-docs-all-lose)
names as *when all the docs disagree, the docs all lose*. If a brief and its doc ever conflict, the
doc wins and the brief is the bug.

**Why stance matters at all:** the same agent, same repo, same context produces different work
depending on what it thinks it is doing. An agent that believes it is implementing will rationalize
a shaky plan into code; the same agent told it is reviewing will find the crack. The briefs exist to
make that choice explicit instead of incidental.

**Paths:** prose links below are relative to this repo. Inside the fenced blocks, paths are written
as `docs/methodology/…` because that is where the methodology lives once copied into an adopting
project — see the note in [`CLAUDE.md`](CLAUDE.md). Adjust if you put it somewhere else.

**Use one at a time.** Start a fresh session per phase where you can. The point of separate stances
is lost if one session carries the implementation mindset into the review.

---

## 1. Epic chartering

**Stance:** you are drawing a boundary, not planning work. The charter's value is what it *excludes.*

Rules: [`03_epics.md`](../methodology/03_epics.md).

```
I want to charter a new epic. Read docs/methodology/03_epics.md and follow
its charter template exactly.

Before drafting, check backlog/EPICS.md: is a WIP slot free, and does this
work genuinely not fit an existing epic? If it fits one, say so and stop.

Draft the charter. Hold yourself to these:
- Exactly one primary pillar. If you need three, the epic is too broad -
  say so rather than listing three.
- Exit criteria must be binary. "Improved" and "better" are not criteria;
  a criterion I can only satisfy by arguing is not binary.
- The out-of-scope section is not optional. Name what a reasonable person
  would assume is included and is not, with the reasoning.
- Do not file items yet.

Show me the charter and tell me which exit criterion you are least
confident is actually checkable.
```

---

## 2. Item authoring

**Stance:** you are writing for a stranger — a session with none of your context, six weeks from now.

Rules: [`04_backlog_items.md`](../methodology/04_backlog_items.md).

```
I want to file backlog items against <epic>. Read
docs/methodology/04_backlog_items.md and use its item format.

Write for a cold session. The test: could someone implement this from the
item alone, without re-investigating what you already worked out?

- Every frontmatter field present. Use a dash, never omit a row.
- Acceptance criteria in EARS shape - a trigger and an observable
  response. "Works correctly" is not a criterion.
- At Effort M or above, write the Code Map: drain what you learned about
  the codebase into the item - which files, which helpers already exist,
  which approach you rejected and why. That knowledge dies with this
  session otherwise.
- Size to the contributor. If it cannot be finished in one sitting, split
  it and say where the seam is.

Ask me about anything genuinely ambiguous before writing. Do not resolve
an ambiguity by picking the reasonable-looking option. If I am not there
to answer, leave it on the item as a `Needs clarification` marker - an
item carrying one is not ready for anyone to pick up.
```

---

## 3. Implementation

**Stance:** you are executing an approved plan, not improving it. Deviations get surfaced, not absorbed.

Rules: [`06_working_principles.md`](../methodology/06_working_principles.md).

```
Implement <item>. The four working principles in
docs/methodology/06_working_principles.md bind this work.

- Touch only what the item requires. Note drive-by problems; do not fix
  them.
- Minimum code that satisfies the criteria. No abstraction for one
  caller, no configurability nobody asked for.
- Reuse what the Code Map named. If you are about to write something
  that already exists, stop and use the existing one.
- If the plan turns out to be wrong, stop and tell me. Do not reshape
  the code to make a wrong plan work, and never edit the item's goal or
  acceptance criteria to match what you built - that is frozen intent
  and it is mine, not yours.

State your understanding of the goal in one sentence before you start.
```

---

## 4. Review

**Stance:** adversarial. Your job is to find what is wrong, and you are not the author.

Rules: [`07_definition_of_done.md`](../methodology/07_definition_of_done.md) (Gate 1).

```
Review this change against docs/methodology/07_definition_of_done.md.
You did not write it. Do not defend it.

For each finding, name the layer the defect entered at - intent, plan,
architecture, or code - and route the fix there. A plan-layer defect gets
the plan fixed; patching the code to compensate for a wrong plan is
itself a finding. Do not grade findings by loudness; the layer already
says what to do.

Also run the verification-gap question: for each behavior this change
adds or alters, would any test that actually ran fail if it broke? Every
"no" is a finding.

If the change is sound, say so plainly and stop. Manufacturing findings
to look thorough wastes more time than missing one.
```

---

## 5. Verification

**Stance:** you are trying to prove the change works, in the running product. A green suite is evidence, not proof.

Rules: [`10_testing_and_verification.md`](../methodology/10_testing_and_verification.md).

```
Verify <item> per docs/methodology/10_testing_and_verification.md.

Run the fix-test loop in the actual running app, not the test harness.
When you fix something you find, restart from upstream of the fix - your
fix may have broken something earlier in the flow.

Cover the required dimensions that could be affected, including blast
radius: enumerate what else consumes the code you changed - other
callers, configuration profiles, feature-flag variants, platform builds,
tenants, locales - and check one representative of each. The change
being right on the surface you developed against says nothing about the
three that share it.

Report what you actually ran. If you skipped a dimension, name it and
say why. "Tests pass" is not a verification report.
```

---

## 6. Milestone evaluation

**Stance:** you are scoring the project cold, as an outsider would. Your own prior work earns no credit.

Rules: [`12_milestone_evaluation.md`](../methodology/12_milestone_evaluation.md).

```
Run a milestone evaluation per docs/methodology/12_milestone_evaluation.md.

Score each area 0-10 against the rubric, with evidence per score - a
number I cannot trace to something observable is not a score.

No area is averaged away. One area below the minimum holds the verdict,
however good the average is. State the verdict as the rubric computes it,
not as the work deserves.

Where an area scores low, name the root cause, not the symptom. Then stop
- do not fix anything in this session. Fixes chosen by the same session
that found the problem are the ones that skip the cheapest option.
```

---

## What these are not

- **Not personas.** No names, no characters, no "you are a senior engineer with 20 years of
  experience." A stance is about what the phase requires; a persona is about who the agent pretends
  to be. The methodology has rejected personas three times, for the same reasons each time — see
  [E08's charter](../self-development/backlog/epics/E08-role-briefs/README.md#out-of-scope).
- **Not a replacement for the docs.** Every brief is a pointer. If the agent has no access to
  `docs/methodology/`, the brief gives it a posture and no rules, which is worse than nothing.
- **Not a pipeline.** These do not chain into an automated flow, and the gaps between them are
  where you decide things. If you want the unattended version, that is
  [`AUTONOMOUS_LOOP.md`](AUTONOMOUS_LOOP.md), and it carries its own constraints.
