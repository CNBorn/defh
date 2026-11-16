# Documentation Definition

This document records the local documentation choices for this repository.
It applies Definition Harness at <commit or version>, pinned at `<pinned harness URL>`. The rules are in the pinned [documentation definition](<pinned harness URL>/documentation/documentation-definition.md) and [documentation principles](<pinned harness URL>/documentation/documentation-principles.md). This document does not copy them; it records only the choices below.

## Paths And Entry

- Stable docs live in `<docs path>/`.
- `README.md` is the entry file. It only routes.
- `AGENTS.md` is <a relative symlink to `README.md` | a pointer file that names `README.md` | a separate agent entry that does not repeat `README.md`>.
- Documentation language: <language>.

## Governing Files

Definitions (`*-definition.md`) and principles (`*-principles.md`) are authority. These topic files are also governing:

- <List each topic file this repository names as governing, such as a runbook or `architecture.md`. Write "None" if there are none.>

Other files are not authority and are not listed.

## Gap Decisions

A gap closes only by a code change or by a risk acceptance written in principles.

- Only a person may decide gaps in: <paths or scopes, such as anything that moves money or deletes user data. Write "None" if agents may decide all gaps.>
- Elsewhere, <a person | an agent with the reason recorded in the PR> may decide.

## Validation

| Command | What it checks |
| --- | --- |
| `<command>` | <claims or scopes it protects> |

## Scope Map

Optional. Delete this section if the docs directory and links are enough. A scope with a definition is adopted whether or not it appears here.
When kept, this table is the only document index. A new scope adds a row in the same change as its first definition.

| Scope | Definition | Principles | Verification |
| --- | --- | --- | --- |
| `<scope>` | `<docs path>/<scope>-definition.md` | `<docs path>/<scope>-principles.md` | `<command, test target, or manual check>` |

## Audit

Definition Audit follows the pinned [audit contract](<pinned harness URL>/documentation/definition-audit-definition.md). <Add local choices only, such as where the last-run record lives, or delete this section.>
