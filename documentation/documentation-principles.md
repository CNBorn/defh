# Documentation Principles

This document captures the guiding principles for documentation under `documentation/`.

## Two Kinds Of Authority

Repository knowledge has two kinds of authority: definitions and principles. Audit is the one action that checks them.

Two separate questions sort every statement:

1. Is it authority? A statement is authority when it lives in a definition or principles file. The author decides this by where the statement is written, not by its content.
2. Which kind? A statement is a definition when an observable check can prove it. A statement is a principle when it needs judgment.

| Statement | Home | Audit result |
| --- | --- | --- |
| Authority that an observable check can prove | Definition | Supported, conflict, insufficient evidence, or unclear |
| Authority that needs judgment: intent, rationale, tradeoffs, preferences | Principles | Followed or violated, with the reasoning |
| Not authority | Any other file | Not a basis for findings. Read it as background, evidence, or history. |

An observable check is code, a test, a measurement, or a person's observation against a stated pass condition. A check need not be automated. Manual acceptance items, such as feel or sound with a stated condition, are definitions.

### Topics Are Not Kinds

- Classify by statement, not by topic. Architecture, evaluation, process, and reusable procedures are topics. Each splits into definition statements and principle statements.
  - Architecture: "the domain layer does not import orchestration" is a definition. "Keep the domain layer testable" is a principle.
  - Evaluation: "p95 latency stays under 200 ms on workload W" is a definition. A rubric for copy quality is a principle.
  - Process: "every PR records its validation commands" is a definition. "Work in small slices" is a principle.
  - Procedure: "use a single homography only with at least 10 markers" is a definition of that workflow. A reusable procedure that later work must follow is a definition, not a working file.
- Files organized by topic, such as `architecture.md` or an evaluation definition, remain valid.
- A definition may keep short rationale next to the value it explains, such as a scene parameter and the reason for it. Rationale that governs more than one scope belongs in principles.
- When one sentence mixes both kinds, split it. For example, "measure against the baseline" is a definition; "explain the value gained when over the baseline" is a principle.

### Working Files

- Studies, research notes, plans, analyses, and other working files are valid. They need no particular name, path, or retention rule. They are not authority.
- A conclusion is lasting when a later change must respect it. Move a lasting conclusion that describes the system now to a definition. Move a lasting decision rule to principles. The working file may then stay as history or evidence.
- An authority file may cite a working file as evidence. It must not depend on the working file for the rule itself. When a definition cites a working file as the reason for a limit or contract, state the limit or contract in the definition.
- An audit reports authority that exists only in a working file.

Fewer kinds lower the cost of every write and every read. A writer asks two short questions instead of choosing among document types. A reader knows that authority lives in two places.

## Same-Change Update

A change to behavior updates, in the same change, the definition that owns the behavior and the tests that check it.

- Audit finds drift after it happens. This principle keeps drift from accumulating between audits. Repeated catch-up changes after audits are a sign that it is not followed.
- It states the required end state of a change, not the steps to reach it.
- A change with no effect on owned behavior, such as a refactor or a presentation change that no definition describes, updates nothing.
- A change that adds a lasting decision rule updates principles in the same way.

## Three-Pillar Independence

Documentation, code, and tests are independent pillars that check each other.

- Documentation describes what the system should do and why.
- Code implements behavior.
- Tests verify behavior.
- Each pillar is authoritative in its own domain and does not duplicate another's responsibility.
- Code and tests may agree while both conflict with a definition. Passing tests do not resolve that disagreement.
- When documentation and runtime behavior disagree, report the evidence without assuming which pillar is wrong.
- Use approved intent and change history to decide whether to correct implementation, tests, or documentation.
- A failing test derived from a definition claim is a valuable signal that behavior may have drifted from intent.

## Current-State Only

Documentation describes the system as it exists now, not as it used to be or might become later.

- Write in present tense.
- Remove or rewrite stale statements when behavior changes.
- Keep migration notes, tradeoffs, and historical context in PR descriptions or design history, not in active definitions.

## Implementation Decoupling

Definitions describe behavior and constraints, not internal file layout.

- Do not couple definition text to source paths or transient module names.
- Definitions should survive a refactor without needing major rewrites.
- `architecture.md` is the intentional exception because its purpose is boundary and ownership description.

## Clarity Before Brevity

Short, concrete text is easier to inspect for errors. Use STE-inspired writing principles: one main idea per sentence, active voice, and consistent terms.

- Cut repetition and filler. Keep conditions, exceptions, values, and stable rationale.
- Put a rule in one authoritative place. Link to it from other docs.
- Use a table for comparisons or a diagram for relationships when it reduces reading effort.
- Keep acceptance criteria explicit in text or tables. A diagram must not hide a requirement.
- Word count measures size, not correctness. Full ASD-STE100 compliance is not required.

## Final-State Capture By Default

The repository knowledge layer captures final behavior, stable rationale, and reusable evaluation criteria. Final validation evidence makes those claims reviewable.

- Implementation plans, attempt logs, progress, and handoff notes are transient execution state.
- External harnesses or sessions may manage that state without creating repository files.
- Create temporary working documents only when requested by the user or required by explicit repo-local policy.
- Existing repositories may retain their opted-in tracking conventions; adopting the harness does not require them to add or remove working artifacts.

## Testable Precision

Definitions must be specific enough that a developer can derive verification from the text.

- Prefer concrete values, named constants, explicit conditions, and observable outcomes over vague intent.
- "Retries up to 3 times with exponential backoff" is testable.
- "Retries reasonably" is not.

## Separate Quality Gates

`tested` and `documented` are separate checks.

- A change can be tested but not documented.
- A change can be documented but not tested.
- Both must be verified explicitly before merge.
- Neither gate substitutes for the other.

## Discoverability Over Prompt Memory

Important project knowledge should live in the repository in named files, not only in prompts, chat history, or oral tradition.

- Prefer many scoped documents over one monolithic manual.
- Keep names predictable so humans and agents can find the right document with simple search.
- Put durable project knowledge in repo files where it can be reviewed and updated.

## Shallow Organization

Flat documentation with domain and topic names gives readers a useful grouping without a deep directory tree.

- Use naming to aid discovery. Use explicit links to establish governing rules.
- Keep cross-domain relationships visible through links instead of adding naming levels.
- Prefer focused entry points over manually maintained exhaustive inventories. An inventory adds another place that can become stale.
- Preserve useful existing navigation and explicit local choices during compatible adoption.

## Small Routing Entry

Agent tools load the agent entry file in every session. Every line in it costs context each time and is another copy that can drift.
This supports the "map, not manual" position in `POSITIONING.md`.

- Ownership comes before file roles. When a definition owns a user operation, the operation is behavior. The entry file links to it, so a feature change updates only the definition.
- "README covers user workflows" applies only to workflows that no definition owns, such as installation and commands. Applying it to owned workflows makes the entry file grow with every feature.
- Entry duties are roles, not files. One file can carry the human and agent roles. A symlink keeps the `AGENTS.md` path that agent tools expect.
- `README.md` holds the content because repository hosts and package registries render it. Agent tools read local files and follow symlinks.
- One index and one language keep one copy. A second definition list or a translated entry file is a third copy.
- The entry file answers "where is the rule". The owning document answers "what is the rule".
- One file is recommended, not required. Separate files remain valid when neither repeats the other or a definition.

## Evidence Before Alignment

A definition audit gives the documentation pillar an explicit path to check implementation and tests.

- Read governing claims before inspecting implementation, so current code does not silently become the expected behavior.
- Include relevant principles and architecture constraints. Distinguish observable requirements from rationale that needs judgment.
- Separate supported claims, conflicts, unclear rules, and missing evidence. Static inspection and passing tests have different limits.
- Report differences before changing any pillar. An audit must not silently erase disagreement by rewriting documentation.
