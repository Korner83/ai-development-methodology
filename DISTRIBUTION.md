# Distribution status

GitHub is the canonical source. Directories are discovery channels; a listing, scan badge, or valid skill header does not establish behavioral correctness.

## Choose the source deliberately

| Source | State | Suitable use |
|---|---|---|
| [v1.34.0 tag](https://github.com/Korner83/ai-development-methodology/tree/v1.34.0) | Latest tagged baseline as of 2026-10-18 | Reproducible trial and initial packaged distribution |
| Default branch | Includes unreleased v1.35.0 and v1.36.0 changes | Preview; review the [changelog](CHANGELOG.md) and [pending acceptance](self-development/backlog/HUMAN_NEEDED.md) |
| GitHub Releases | Latest published Release entry was v1.17.3 as of 2026-10-18 | Older release records; a Release page and a Git tag are separate records |

Tags identify source snapshots. They do not certify external adoption or clear the outstanding E10/E11 reviews. These listing-preparation changes do not release either pending methodology version.

## Install or inspect

For the tagged operating guide:

    npx skills add https://github.com/Korner83/ai-development-methodology/tree/v1.34.0/skills/ai-dev-methodology

To inspect without the installer, open the [tagged skill folder](https://github.com/Korner83/ai-development-methodology/tree/v1.34.0/skills/ai-dev-methodology). Copying the folder manually is also supported by the format.

The unpinned command follows the default branch and can load unreleased material:

    npx skills add Korner83/ai-development-methodology

The skill contains Markdown, not executable components. The external installer is separate software; review it before running. Installing the operating guide does not create the full project scaffold or enforce its rules mechanically.

## Compatibility and evidence

The skill uses the [Agent Skills](https://agentskills.io) format. Format conformance is distinct from installation, automatic triggering, explicit invocation, and behavior in any particular client. No blanket count of tested clients is claimed.

Before advertising a client as tested, record its version, source revision, installation result, and observed outcomes for: a process question, pending review, a live lock, an untrusted conflicting instruction, and an unrelated project. Client-specific invocation syntax varies.

## Listing and package checks

- Use Miklós Polgár as author, the canonical repository URL, and [CC BY 4.0](LICENSE); include the [notice](NOTICE.md). Keep credit in detached copies of the skill.
- Identify the actual source revision. Uploaded ZIPs do not automatically track GitHub; repository-indexed directories may follow the default branch.
- Include only the intended skill and necessary notices in an upload. Keep private research, local paths, credentials, and evidence bundles out.
- Preserve reuse rights. Clarify any marketplace terms that conflict with CC BY before publishing there.
- State lean maintenance and no support SLA. Do not turn illustrative examples into claims of observed success.
- After publication, inspect the public source link, author, license, version, and installation path. Distinguish submission from acceptance.

No directory submission is completed by this document. Release approval, independent review, and external adoption remain separate evidence.
