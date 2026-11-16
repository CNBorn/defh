# <Scope Name> Definition

This document defines the current behavior of `<scope>`. Every statement describes what the system does now and can be checked.
Remove unused sections without omitting required behavior or constraints.
For new docs, prefer `<domain>-definition.md` or `<domain>-<topic>-definition.md` in a flat directory. Keep existing adopted filenames.

## Scope

- Describe the subsystem, workflow, command, policy, or interface this definition covers.
- State what is intentionally out of scope.

## Inherits From

- `<docs path>/<domain>-definition.md`

Link the domain definition whose baseline rules apply. A filename prefix does not establish inheritance. Remove this section when no domain definition governs this scope.

## Governing Principles

- `<docs path>/<scope>-principles.md`

Link shared principles and cross-domain constraints. A separate principles file for this scope is not required.

## Behavior

- Summarize the current behavior first, then the rules, defaults, and limits.
- Describe the mechanism, including what the code does not do, such as no lock, no retry, or no unique index. An audit compares this with the principles' violation conditions.
- Include triggers, preconditions, branches, failure behavior, and edge cases when relevant.
- Use concrete terms, named constants, and values.
- Use a table or Mermaid diagram when it clarifies relationships. Label arrows and keep conditions explicit in text.
- Rationale that governs only this scope may stay next to the values it explains.

## Verification

- Name the existing checks that protect these claims: tests, commands, measurements, or manual acceptance with a stated pass condition.
- A check that does not exist yet is not listed here. Its invariant belongs in principles.

## Non-goals

- State what this definition does not specify.
