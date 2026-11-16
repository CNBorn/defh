# defh

Short for Definition Harness. Pronounced "def-H".

Two kinds of document, definitions and principles, and one action, audit, that keep software behavior, intent, and tests aligned. No required process. Why it is this small, and how Lisp inspired it: [Short Version](POSITIONING.md#short-version). The current version is in `VERSION`.

This file is the only entry for humans and agents. `AGENTS.md` is a symlink to it.
It only routes. Rules live in `ADOPTION.md` and `documentation/`; this file does not restate them.

## Quick Start

Point your coding agent at this repository URL. A local checkout is not required.

```text
Use defh from <repo URL>. Read its README and ADOPTION.md. If this repository already adopted an earlier version, follow the earlier-version prompt in ADOPTION.md. Otherwise follow the prompt for your case.
```

Prompts for a new repository, an existing repository, one scope, and an earlier-version adopter are in [Adoption Prompts](ADOPTION.md#adoption-prompts).
For an audit, use `templates/definition-audit.template.md`.

## Read Before Adopting

1. [ADOPTION.md](ADOPTION.md): adoption, compatibility, starter files, and prompts.
2. [Documentation principles](documentation/documentation-principles.md): the two kinds of authority, gaps, and same-change updates.
3. [Documentation definition](documentation/documentation-definition.md): document types, naming, writing, entry-file, and update rules.
4. [Definition audit definition](documentation/definition-audit-definition.md): the one action that checks definitions and principles.

Adapt `templates/` paths and validation commands to the target repository before use.
[POSITIONING.md](POSITIONING.md) explains why this exists. [CHANGELOG.md](CHANGELOG.md) lists version changes.

## Working In This Repository

Follow the documents above for changes to this repository, and [evolution principles](documentation/evolution-principles.md) for changes to rules, templates, versions, or compatibility.
Preserve compatibility for adopted repositories unless a breaking version is planned; see [Framework Versions](ADOPTION.md#framework-versions).

Validation:

```sh
test "$(readlink AGENTS.md)" = README.md
```

Also check changed Markdown links and Mermaid diagrams. When rules or templates change, run a Definition Audit of this repository against itself. Record results in the PR.
