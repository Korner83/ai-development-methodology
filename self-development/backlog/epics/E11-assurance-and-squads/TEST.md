# E11 — Verification

Local scenario inspection and structural checks are author verification. Scenario `pass` below means the written rules and examples produce the stated outcome; it does not mean fictional product tests ran, a cold contributor performed the walkthrough, or independent assurance occurred. Independent review and human acceptance are separate, pending item-level requirements.

## Acceptance scenarios

| ID | Scenario | Expected result | Status |
|---|---|---|---|
| AT-01 | Ordinary UX change / solo contributor | A1 inherits human ownership; existing applicable gates and user testing remain | pass — A1 row + solo walkthrough retain applicable gates and user testing |
| AT-02 | Disposable prototype promoted to production | A0 bounds learning; reassess before production reuse; no gate waiver | pass — A0 row and inheritance paragraph require non-production bounds and reassessment |
| AT-03 | Authentication change in a small squad | A2 item names human owner; fresh verifier uses criteria and evidence; human accepts | pass — invitation item names Morgan; fresh verifier and acceptance remain pending |
| AT-04 | Safety-critical regulated feature | A3 has domain owner, qualified human specialist, applicable compliance evidence | pass — A3 row + doc 11 require domain owner, independent qualified human, applicable evidence |
| AT-05 | Owner missing, specialist unavailable, acceptance pending | Missing required assignment blocks readiness; unmet review or acceptance blocks completion | pass — readiness and completion rules cover missing assignment, unavailable reviewer, and pending acceptance |
| AT-06 | Risk rises or author proposes lower classification | Human resolves uncertainty; no silent downgrade; revise requirements before continuation | pass — profile selection requires human resolution and forbids silent downgrade |
| AT-07 | Queue reaches limit; verification fails back to implementation | Combined verification queue counted once; pause starts; prioritize rework without exceeding implementation cap | pass — doc 11 queue rules and worked capacity walkthrough cover saturation, overflow, and prioritized rework |
| AT-08 | Cold contributor receives item | Purpose, constraints, ownership, and reproducible verification available in repository | pass — inspected item/Code Map, owner roster, procedures, and rejected approach; no actual cold-session trial claimed |
| AT-09 | Third near-identical asset use | No automatic promotion; distinct use evidence and productization obligations required | pass — simplicity section and reuse walkthrough reject automatic promotion |
| AT-10 | Adoption and release surfaces | Links/anchors, YAML, version pins, and line budgets pass; examples labeled unvalidated | pass — final structural checks below; release remains unaccepted |

## Regression scenarios

| ID | Scenario | Expected result | Status |
|---|---|---|---|
| RT-01 | A0 self-check offered instead of DoD | Existing six gates and Test exceptions retain authority | pass — assurance overlay preserves six gates and narrow Test exceptions |
| RT-02 | A2 or A3 approval offered for agent deployment | Production execution remains human-only | pass — doc 09 production execution remains unchanged; overlay and example preserve it |
| RT-03 | L3 agreement with missing required L4 or acceptance | No premature Test: pass or Status: done | pass — doc 10 bridge requires both assurance and L levels; example keeps partial |
| RT-04 | Item limits mistaken for epic cap | Distinct controls; repository's two-active-epic cap unchanged | pass — doc 11 distinguishes item queues from epic cap; E10 + E11 occupy the two slots |

## Evidence

### Scenario review — 2026-09-15

Author read the complete canonical diff and traced each scenario above through docs 03/04/06/07/10/11 and the new solo/squad walkthrough. Outcomes are documented-rule checks, not runtime execution or independent review. A fresh verifier must still inspect the approved plan, final diff, and evidence before maintainer acceptance.

### Structural checks

Checks use the existing Python runtime with installed `markdown-it-py` and PyYAML; no packages were installed and no executable files are shipped.

| Check | Method | Result |
|---|---|---|
| Markdown links and anchors | Parse all tracked Markdown with `MarkdownIt("commonmark").enable("table")`; inspect rendered link tokens, skipping fences/inline code. Resolve decoded relative paths and GitHub-style heading slugs, including duplicate-heading suffixes. Compare unresolved links to base `1d43c70`. | 1,224 local links checked; no new unresolved links. One pre-existing illustrative filename placeholder in doc 02 remains. |
| Adopter-relative links | Count separately the instruction-template links whose roots only exist after install; remap `docs/methodology/` to the local canonical directory and check fragments. | 65 install-relative links; all 52 methodology links among them resolve after remapping. Other 13 target adopter-owned artifacts. |
| Repository web links | Resolve this repository's `blob/main/` Markdown links against the proposed local tree, without claiming the unreleased anchors are live on main. | 14 checked, zero failures. |
| Skill metadata | `yaml.safe_load` the opening frontmatter; verify name, license, required description and length. | name/description/license valid; description 505 characters. |
| Template parity | Compare the complete assurance-and-capacity sections of AGENTS and CLAUDE templates. | Identical. |
| Version pins | Inspect current-version references in README, CHEATSHEET, STATUS, and packaged skill, excluding STATUS's historical workflow reference. | Eight references equal v1.35.0. Historical examples/evaluations retained. |
| Line budgets | Count final text lines in every capped file per the release-evidence inventory. | All pass; doc 04 = 1,047/1,050; role briefs = 200/200; cheatsheet = 98/100. |
| Repository shape | Inspect tracked file suffixes, workflow action refs, all epic folders, and E11 item metadata. | No executable files; existing workflow actions still SHA-pinned; 12 complete five-file epics; two active chartered epics, excluding standing E00. |
| Diff hygiene | `git diff --check 1d43c70` on the final tree. | Pass — final diff has no whitespace errors. |

The one existing unresolved rendered link is the illustrative `P<N+1>_<short_name>.md` in doc 02; verified against the baseline rather than silently counted as valid. The parser is an in-session check, not a committed validator. Reproduce using the method above and [the release-evidence commands](../../../RELEASE_EVIDENCE.md); parser counts depend on these explicit exclusions.


### Corrections found during author validation

- Role briefs initially reached 205 lines; reduced introductory prose to meet the unchanged 200-line cap. The initial adoption commit carried the overrun; the follow-up fixes it without weakening a rule.
- BL-0064/0065 ordering was initially entered as hard dependencies although work only required the preceding draft, not its final acceptance. Corrected the metadata to soft ordering in the bodies; the original goals and acceptance criteria remain unchanged.
- Retained the original fictional project's v1.28.0 pin and its historical review attribution; neither is evidence for the new v1.35.0 examples.

### Outstanding assurance

Independent verification and maintainer acceptance are not performed by this author session. No specialist, real-user, production, or external-adoption validation is claimed. The project has no runnable product or behavioral test suite; local checks cover documentation structure and consistency only. No release tag has been created.
