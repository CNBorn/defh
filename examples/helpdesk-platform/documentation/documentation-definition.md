# Documentation Definition

This document records the local documentation choices for the helpdesk platform.
It applies defh 2.0. Because this example lives inside the defh repository, it links to the rules in this repository instead of a pinned URL. A real adopter pins a release tag or commit. The rules are in the [documentation definition](../../../documentation/documentation-definition.md) and [documentation principles](../../../documentation/documentation-principles.md). This document does not copy them; it records only the choices below.

## Paths And Entry

- Stable docs live in `documentation/`.
- `README.md` is the entry file. It only routes.
- `AGENTS.md` is a relative symlink to `README.md`.
- Documentation language: English.

## Governing Files

Definitions (`*-definition.md`) and principles (`*-principles.md`) are authority. These topic files are also governing:

- [architecture.md](architecture.md): boundaries and ownership for all scopes.

Other files are not authority and are not listed.

## Gap Decisions

A gap closes only by a code change or by a risk acceptance written in principles.

- Only a person may decide gaps in: VIP escalation, and any change to how tickets reach the `security-review` queue.
- Elsewhere, an agent may decide, with the reason recorded in the PR.

## Validation

| Command | What it checks |
| --- | --- |
| `make check` | Unit tests for routing and escalation, and lint. |

## Scope Map

This table is the only document index. A new scope adds a row in the same change as its first definition.

| Scope | Definition | Principles | Verification |
| --- | --- | --- | --- |
| Ticket routing | [ticket-routing-definition.md](ticket-routing-definition.md) | [support-operations-principles.md](support-operations-principles.md) | `make check` |
| VIP escalation | [vip-escalation-definition.md](vip-escalation-definition.md) | [support-operations-principles.md](support-operations-principles.md) | `make check` |

## Audit

Definition Audit follows the [audit contract](../../../documentation/definition-audit-definition.md). The last-run record goes in the audit PR title: `Definition audit: <scope> through <revision>`.
