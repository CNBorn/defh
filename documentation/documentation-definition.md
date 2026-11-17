# Documentation Definition

This document defines document types, writing rules, and update rules for `documentation/`.

## Scope And Paths

- `documentation/` holds the framework's definitions and principles: this document, the documentation principles, the audit contract, and the evolution principles.
- `README.md` is the entry file. It covers how to run, development commands, the reading route, and validation commands.
- `AGENTS.md` is the agent entry. It may be a symlink to `README.md`. See [Entry File](#entry-file).
- `ADOPTION.md` is a governing topic file for this repository. It owns adoption steps, starter files, prompts, and compatibility notes.

Keep an adopting repository's existing docs path. Record it in the entry file and the local documentation definition.

## Document Types

Two kinds of document are authority. [Two Kinds Of Authority](documentation-principles.md#two-kinds-of-authority) gives the test and the rationale.

| Kind | File | Holds |
| --- | --- | --- |
| Definition | `<scope>-definition.md` | Current behavior: the mechanism, including what the code does not do, constraints, terms, outcomes, boundaries, and existing checks. Every statement is checkable. |
| Principles | `<scope>-principles.md` | Intent: goals, invariants, rationale, tradeoffs, and decision rules. A principle may be checkable and should state its violation condition when one can be stated. Guides definitions without replacing them. |

Topic files that the local documentation rules name as governing, such as runbooks, are also authority. Other files are not authority. Working files, such as studies and plans, need no type.

Architecture, evaluation, and process are topics, not kinds. These files remain valid, and their statements are definitions or principles by the same test:

| Topic file | Covers |
| --- | --- |
| `<scope>-evaluation-definition.md` | Existing checks, scenarios, rubrics with pass conditions that gate acceptance, and the evidence a release requires (definition). Invariants that no check covers yet, and rubrics that only guide judgment (principles). Work to build a missing check belongs in a working file. |
| `architecture.md` | Boundaries, ownership, and dependency direction (definition). Architectural intent (principles). |
| Process file, such as a development flow | Required end state of a change (definition). Working preferences (principles). |
| Runbooks | Operational and incident procedures that operators must follow (definition). Operational judgment calls (principles). |

### Definition Levels

- A domain definition sets baseline rules for a domain, such as authentication or job orchestration.
- A topic definition applies those rules to a specific flow, policy, command, or interface.
- A topic definition must obey the domain definition it inherits from. Update the domain rules before introducing a conflicting behavior.
- Existing files that use the older terms "system definition" and "item definition" remain valid.

Definitions may reference shared principles and adjacent definitions. A scope does not need its own principles file.
`documentation-principles.md` governs authoring. Principles for an adopter's own code, such as those in `examples/principles/`, belong to that adopter.

### Shallow Naming

For new documentation, prefer a flat directory and at most two semantic naming levels: domain and optional topic.
Keep existing paths, filenames, and local naming conventions in adopted repositories.

| Scope | Definition | Optional principles |
| --- | --- | --- |
| Domain | `<domain>-definition.md` | `<domain>-principles.md` |
| Topic within a domain | `<domain>-<topic>-definition.md` | `<domain>-<topic>-principles.md` |

For example, `authentication-definition.md`, `authentication-session-definition.md`, and `authentication-password-reset-definition.md` share a domain prefix.
Multiword domains and topics do not add semantic levels. Document-type suffixes, including `evaluation-definition`, do not add levels either.

- Use stable domain terms. Do not encode source layout, numeric ordering, or a deeper category chain in filenames.
- A shared prefix groups documents for discovery. It does not establish authority or inheritance.
- State applicable domain definitions under `Inherits From` or an equivalent explicit link. Name related principles and cross-domain constraints in the document.
- Each stated inheritance relationship applies the domain rules to the topic's scope. Related links alone do not imply inheritance.
- Create a domain definition only when it has baseline rules to own. A topic may stand alone.
- Shared principles may govern several definitions. A topic does not need its own principles file.
- Apply consistent terms in the document's language. Existing naming conventions do not require translation.

### Entry File

The entry file routes readers to rules. It does not restate them. [Small Routing Entry](documentation-principles.md#small-routing-entry) gives the rationale.

Entry duties are roles, not files:

| Role | Content |
| --- | --- |
| Human entry | Purpose, setup, how to run, and development command invocations |
| Agent entry | Reading route, validation commands, and the few constraints that every session must see |

One file may perform both roles. The recommended layout is one entry file:

| Layout | Status |
| --- | --- |
| `README.md` holds both roles. `AGENTS.md` is a relative symlink to it. | Recommended. Not required. |
| `README.md` holds both roles. `AGENTS.md` is a pointer file that names `README.md`. | Valid when the repository cannot store symlinks. |
| `README.md` holds the human role. A separate `AGENTS.md` holds the agent role. | Valid. Neither file repeats the other. |

Ownership:

- A definition owns each user or operator workflow, operation, value, or limit that it describes. The entry file links to that definition and may show the command that starts the workflow.
- The entry file must not restate steps, parameters, defaults, limits, or constraints that a definition owns.
- The entry file describes a workflow directly only when no definition owns it, such as installation and development commands.
- Each always-visible constraint is one sentence and a link to the document that owns it.
- When the repository keeps a [scope map](#scope-map), the map is the only document index. The entry file links to it and does not list definitions. Without a map, the entry file links to the docs directory or the local documentation definition.
- Content without an owner does not go in the entry file. Move it to the document that owns it, or leave it to code and tests. Examples are code structure, test coverage lists, generated file names, and per-feature descriptions.
- Write the entry file in the repository's documentation language, which is the language of its definitions. Do not keep a translated copy of the entry file or of definition content.
- Other tool-specific entry paths, such as `CLAUDE.md`, may also be relative symlinks to `README.md`.

Update the entry file only for the changes listed in [Update And Review](#update-and-review).
To shrink an existing entry file, follow [Shrink An Existing Entry File](../ADOPTION.md#shrink-an-existing-entry-file).

Symlink limits:

- A Windows checkout without `core.symlinks` enabled writes `AGENTS.md` as a text file that contains `README.md`. Agents that read this file then open `README.md`.
- Raw-file URLs return the link target, not the content. Point remote readers at `README.md`.
- A repository can check the link in validation: `test "$(readlink AGENTS.md)" = README.md`.

### Navigation And Inventories

The entry file routes readers to rules and to the local documentation definition.
Unless the user requests one or explicit repo-local policy requires one, agents must not create or expand a manually maintained inventory of every Markdown file.
This rule applies to standalone indexes and exhaustive tables or lists inside other documents.

- Use a short, task-oriented set of entry points and explicit related-document links.
- A scope map may record authority and validation for each scope. It does not need to enumerate every document in a scope.
- Generated inventories and one-time discovery output are permitted. Do not copy generated listings into stable docs for manual upkeep.
- Preserve existing navigation during compatible adoption. Do not delete or reorganize it solely to adopt this guidance.
- An opted-in inventory remains navigation. It does not define behavior or replace the linked authority.

### Evaluation

Evaluation is a topic. A repository may keep it in the scope's definition or in a separate evaluation file when ordinary tests cannot express all required evidence.

- Existing scenarios, browser checks, workload measurements, and the evidence a release requires are definitions.
- An invariant that no check covers yet is a principle. Building the check is work for a working file.
- A rubric with stated pass conditions that gates acceptance is a definition. A rubric that only guides judgment is a principle. Either way, define observable dimensions, examples and anti-patterns from real review, and calibrate it against human review. Revise it when it misses repeated failures. Add weights only when justified.
- Keep tools vendor-neutral unless the repository standardizes on one.

## Writing Rules

Document the final implemented behavior, stable rationale, and reusable evaluation criteria. Put final validation results in the PR.
Keep history and migration discussion in PRs or project history.

### Clear Technical Language

Use selected principles from [ASD-STE100](https://www.asd-ste100.org/STE_faq.html). This framework does not require its controlled dictionary or claim STE compliance.

- Use short sentences, active voice, and concrete verbs. Give each sentence one main rule or action.
- When a condition controls an action, state the condition first.
- Use one term for one concept. Preserve canonical product names, code identifiers, and domain vocabulary.
- Name the actor and outcome. Replace vague words such as "appropriately" with observable conditions or values.
- Keep requirements explicit: `must` is required, `should` is recommended, and `may` is permitted.
- Remove filler, repeated explanations, and empty template sections. Preserve exceptions, failure behavior, limits, and rationale.
- Apply these principles in the document's language. Do not shorten text by omitting facts or sentence parts needed for clarity.

Write in present tense. Put the behavior summary first, then defaults and constraints.
Include constant names and values when useful. Rewrite stale claims when behavior changes.
Keep architecture docs high-level. Mention source paths only when they form part of the contract.

### Tables And Diagrams

Use the smallest format that makes the information easy to check.

| Information | Preferred format |
| --- | --- |
| A rule, constraint, or rationale | Short prose or a list |
| Comparable options, roles, states, or condition/result cases | Table |
| Branching flows, dependencies, ownership, or data movement | Diagram when relationships are clearer than in prose |
| Measurements or trends | Chart or table with units and conditions |

- Prefer editable Mermaid diagrams in Markdown for software relationships.
- Label nodes and arrows. Say whether arrows mean calls, data flow, dependencies, or state transitions.
- Show the stable model or workflow. Update a diagram with the rules it represents.
- Replace repeated relational prose with the diagram. Keep conditions, exceptions, and acceptance criteria explicit in text or tables.
- Keep each rule authoritative in one place. Link to it instead of repeating it.
- A simple rule does not need a diagram. Verify diagram syntax and rendered labels when adding or changing one.

## Traceability

Use shared names across docs, code, and tests so the mapping is discoverable.
Definitions need not list individual tests, and tests need not cite document paths.
Definition audits may build claim-to-evidence mappings for a run. Permanent rule IDs or source/test inventories are not required.
See [Definition Audit](definition-audit-definition.md) for the audit contract.

## Scoped Adoption

A scope may be a subsystem, workflow, API, operator process, or product area.
A scope is adopted when it has a definition. The definition marks the boundary; no separate list is required.
Complete repository coverage is not required. For each adopted scope, keep definitions, principles, tests, and validation expectations aligned.
Code without a definition keeps its existing practice. An audit reports missing definitions only within the scope it was asked to check.
Existing full-adoption repositories keep their structure.

### Scope Map

A scope map is optional. It is a table in the local documentation definition with one row per scope: the scope, its definition, its principles, and how it is verified.

- Keep a map when readers need one place to find each scope's authority and checks. Skip it when the docs directory and links are enough.
- When a map exists, it is the only document index. A new scope adds one row in the same change as its first definition.
- The map is navigation. It is not authority and does not replace the definitions it links.
- Existing adopted-scope tables remain valid as scope maps.

## Optional Working Docs

Working docs, such as studies, plans, or progress notes, follow [Working Files](documentation-principles.md#working-files).
Delegation, duration, multiple iterations, or crossing sessions does not itself require them.
Planning and execution state may stay in the task, session, or external harness. One-time decisions may stay in PR history.

## Update And Review

When behavior changes, search docs by scope terminology and check the relevant definitions.

| Change | Check |
| --- | --- |
| Behavior, defaults, or contracts | Matching definitions |
| Stable rationale | Matching principles |
| Checks, rubrics, or evidence requirements | Matching evaluation definitions |
| Boundaries, ownership, dependencies, or lifecycle | `architecture.md` |
| User/operator workflows or operations that a definition owns | That definition only |
| New adopted scope | Its first definition, and the scope map row when a map exists |
| How to run, development commands, reading route, or validation commands | Entry file. See [Entry File](#entry-file). |

When a change is merged, the documents it touches use no stale terms, and the definitions it touches match the final implementation. See [Same-Change Update](documentation-principles.md#same-change-update).
Tested and documented are different; see [Tested And Documented Are Different](documentation-principles.md#tested-and-documented-are-different).
