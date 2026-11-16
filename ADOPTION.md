# Adoption Guide

Adopt Definition Harness in a new repository or in one part of an existing repository.

The framework has two kinds of authority, definitions and principles, and one action, audit. See [Two Kinds Of Authority](documentation/documentation-principles.md#two-kinds-of-authority).
After adoption, the repository's own definitions and principles are its authority. They may evolve and drift from this framework; see [harness evolution principles](documentation/harness-evolution-principles.md).

## Compatibility

Version 2.0 removes framework files and templates that earlier versions offered: development flow, agent workflow, the architecture starter, and the evaluation, acceptance, progress, and adopted-scope templates.
Repositories that copied those files keep them. They remain valid as topic files when local documentation rules name them as governing, or as working files otherwise. No adopter needs to delete, rename, or rewrite anything.
Adopted-scope tables remain valid as optional scope maps. Existing paths, names, and navigation remain valid. Upgrading is optional.

## Adoption

A scope is adopted when it has a definition. The definition marks the boundary; no separate list is required.
Start with the whole repository or with one high-risk or high-change scope. Code without a definition keeps its existing practice.

Definitions describe implemented behavior. A repository without code completes adoption without a definition and writes the first definition from the first implemented behavior.

Adoption is complete when the repository states:

- where stable docs live, such as `documentation/` or an existing `docs/`
- which topic files, besides definitions and principles, are named as governing
- which validation commands prove changes

Definition Harness does not replace engineering controls. Connect definitions to the repository's own checks: typed or validated boundaries, static analysis, tests, CI, and reproducible workloads where behavior needs them.

### Starter Files

| File | Source | When |
| --- | --- | --- |
| Entry file, with `AGENTS.md` as a symlink | `templates/entry-file.template.md` | New repository. In an existing one, add only its "Read Before Changing" section. |
| Local documentation rules | `templates/existing-repo-documentation-definition.template.md` | Always. It links to the pinned harness rules instead of copying them. |
| Definition | `templates/definition.template.md` | When behavior exists. |
| Principles | `templates/principles.template.md` | When intent must guide future changes. |

Copy only the files you need. Adapt paths and validation commands to the target repository.
Copied docs may link to harness documents that are not starter files, such as `definition-audit-definition.md`. Point those links at a pinned harness URL, or remove them.

See the [helpdesk platform example](examples/helpdesk-platform/README.md) for an adopted repository. [Example code principles](examples/principles/) show principles an adopter may write for its own code.

## Adoption Prompts

Point a coding agent at the Definition Harness repository URL with the prompt for your case. A local checkout is not required.

New repository:

```text
Use Definition Harness from <repo URL> for this project's documentation.
Read its README and ADOPTION.md. Add the starter files and adapt paths and validation commands to this project's stack. If the project already has behavior, write the first definition from the code of its highest-risk scope. If it has no code yet, do not write a definition now.
```

Existing repository:

```text
Use Definition Harness from <repo URL> in this existing repository.
Do not reorganize the docs tree. Keep this repo's existing docs path.
Pick one high-risk or high-change scope. Add local documentation rules that name any governing topic files, write or update the definition of that scope from its current behavior, and name the tests or commands that protect its claims.
```

One existing scope:

```text
Use Definition Harness from <repo URL> to adopt only <scope name> in this repository.
First inspect the current docs, code, tests, and entry files. Do not reorganize unrelated docs.
Create or update the current-state definition for <scope name>, add a row to the scope map if the repository keeps one, and identify the tests or validation commands that protect it.
```

Repository that adopted an earlier version:

```text
Review Definition Harness from <repo URL> and report which improvements this repository could take.
Do not rename documentation directories, delete local copies of framework files, or rewrite existing definitions to match the new version.
Report the compatibility impact first. Apply nothing without approval.
```

For an on-demand audit, use `templates/definition-audit.template.md`.

## What To Capture

| Knowledge | Home |
| --- | --- |
| Current behavior, including the mechanism and what the code does not do | `*-definition.md` |
| Intent, invariants with violation conditions, rationale, and tradeoffs | `*-principles.md` |
| How to run, development commands, the reading route, and validation commands | Entry file |
| Final validation evidence, one-time decisions, and audit reports | The PR |
| Studies, plans, and other working notes | Any working file. Not authority. |

## Shrink An Existing Entry File

An entry file that restates definitions is a documentation finding. A [Definition Audit](documentation/definition-audit-definition.md) reports each restatement, and a conflict when the copies differ.
To shrink the file, confirm that the owning document holds every fact, then replace the restatement with a link. Ask before deleting, keep one documentation language, and check that every document the removed text linked is still reachable.
Shrinking is optional for existing adopters. Converting `AGENTS.md` to a symlink is optional.

## Optional Definition Audit

A user or explicit local policy may request a [Definition Audit](documentation/definition-audit-definition.md).
Reference the pinned audit contract or adapt it; copying it is not required. Every audit states its window. Keep the report in the session or PR.

## Framework Versions

Non-breaking updates preserve paths, filenames, and valid adoption shapes.
Breaking updates state the incompatibility, explain why, and change only what new adopters start from. Existing adopters stay valid and choose whether to upgrade.
