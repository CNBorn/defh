# Documentation Principles

This document captures the guiding principles for documentation under `documentation/`.

## Two Kinds Of Authority

Repository knowledge has two kinds of authority: definitions and principles. Audit is the one action that checks them.

Two separate questions sort every statement:

1. Is it authority? A statement is authority when it lives in a definition or principles file, or in another file that the local documentation rules name as governing, such as a runbook or `architecture.md`. The author decides this by where the statement is written, not by its content.
2. Which kind? A statement is a definition when it describes current behavior. A statement is a principle when it states intent: what the system must achieve or why.

| Statement | Home | Audit result |
| --- | --- | --- |
| Current behavior, including the mechanism and what the code does not do | Definition | Supported, conflict, insufficient evidence, or unclear |
| Intent: goals, invariants, rationale, tradeoffs, preferences | Principles | Followed, not guaranteed, or violated, with the reasoning |
| Not authority | Any file that is not a definition, principles, or a named governing file | Not a basis for findings. Read it as background, evidence, or history. |

- A definition must be checkable. Code, a test, a measurement, or a person's observation against a stated pass condition can check it. A check need not be automated; manual acceptance items with a stated condition are definitions.
- A principle may be checkable or may need judgment. An invariant such as "a job runs at most once per trigger" is a checkable principle even when current code does not guarantee it.
- A principle should state its violation condition when one can be stated. This is recommended, not required. Without one, a principle is judged as followed or violated, with the reasoning.
- A check that does not exist yet is not a definition. The invariant it would check is a principle. The work to build the check belongs in a working file. Existing checks, and rules that name the evidence a release requires, are definitions.

### Intent And Gaps

A gap exists when current behavior does not guarantee a principle. The gap itself is not written into any authority file. It is an audit finding.

A fact and a gap differ in what they name. "The spend step takes no lock" is a fact about the code; it belongs in the definition. "Admission is not yet guaranteed under concurrent callers" names a principle the facts fail to meet; it is a gap. A definition section that tracks unmet intent, or progress toward it, holds gaps; move its facts to the definition body and report the rest.

- A definition records the mechanism as it is, including what the code does not do, such as no lock, no recheck, or no unique index. These are facts about current behavior.
- A gap finding depends on two inputs: a principle that states its violation condition, and a definition that records the mechanism faithfully. When either is missing, the gap cannot be found.
- Report a gap when it is found, during an audit or any other change. Do not wait for the next audit.
- Do not make a gap disappear by changing the principle, removing its violation condition, or removing the claim that exposes it.
- A gap closes only by an explicit decision: a code change that guarantees the principle, or a statement in principles that accepts the risk and gives the reason. Local rules name the paths where only a person may make that decision. Until then, an agent may add checks.

### Topics Are Not Kinds

- Classify by statement, not by topic. Architecture, evaluation, process, and reusable procedures are topics. Each splits into definition statements and principle statements.
  - Architecture: "the domain layer imports only the contracts package, and lint enforces it" is a definition. "The domain layer stays independent of orchestration" is a principle.
  - Evaluation: "the release check fails when p95 latency exceeds 200 ms on workload W" is a definition. "p95 stays under 200 ms" without an existing check is a principle. A rubric for copy quality is a principle.
  - Process: "every PR records its validation commands" is a definition when it is current practice. "Work in small slices" is a principle.
  - Procedure: "use a single homography only with at least 10 markers" is a definition of that workflow when later work must follow it. A reusable procedure that later work may use or skip is a working file.
- Files organized by topic, such as `architecture.md`, an evaluation definition, or a runbook, remain valid and remain authority when the local documentation rules name them as governing. Their statements sort into the two kinds by the same test.
- A definition may keep rationale that governs only its own scope, next to the values it explains, so that later tuning does not reverse a decision by accident. Rationale that governs more than one scope belongs in principles.
- When one sentence mixes both kinds, split it. For example, "the build measures against the baseline" is a definition; "a result over the baseline must buy visible value" is a principle.

### Working Files

- Studies, research notes, plans, analyses, and other working files are valid. They need no particular name, path, or retention rule. They are not authority. Adopters do not need to list them.
- A consistent name suffix, such as `-study`, and a first line that says the file is not authority make authority-by-location easy to read. This is recommended, not required.
- A conclusion is lasting when a later change must respect it. Move a lasting conclusion about current behavior to a definition. Move a lasting intent or decision rule to principles. The working file may then stay as history or evidence.
- Content also moves the other way. Per-run evidence, incident narratives, review history, test or source inventories, and last-run records leave a definition for a working file or the PR; the definition keeps only the rule derived from them.
- An authority file may cite a working file as evidence. It must not depend on the working file for the rule itself. When a definition cites a working file as the reason for a limit or contract, state the limit or contract in the definition.
- A status line such as "Draft" does not change authority. Content in a definition or principles file on the main branch is authority. Keep unconfirmed content on a branch or in a working file, such as a `-study` file.
- An audit reports authority that exists only in a working file.

Fewer kinds lower the cost of every write and every read. A writer asks two short questions instead of choosing among document types. A reader knows that authority lives in two places.

## Same-Change Update

A change to behavior updates, in the same change, the definition that owns the behavior, the tests that check the changed claims, and the derived outputs that describe it.

- Tests here means the tests that check the claims the change touches, not every test in the scope.
- Derived outputs, such as a user manual, its translations, generated figures, and procedure executors such as agent skills, are not authority. They follow the definition and change with it. They exist only when the scope has them.
- Evidence artifacts, such as a formal model, are evidence, not derived outputs. The scope's definition states whether they change with the behavior.
- Audit finds drift after it happens. This principle keeps drift in the owning definition from accumulating between audits. Small follow-up fixes after an audit, in documents that mention the behavior but do not own it, are expected; that ripple is what audits catch.
- It states the required end state of a change, not the steps to reach it.
- A change with no effect on owned behavior, such as a refactor or a presentation change that no definition describes, updates nothing.
- A change that adds a lasting intent or decision rule updates principles in the same way.

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

Definitions describe the system as it exists now, not as it used to be or might become later. Intent that current behavior does not yet meet belongs in principles.

- Write in present tense.
- Remove or rewrite stale statements when behavior changes.
- Keep migration notes, one-time tradeoffs, and historical context in PR descriptions or design history, not in active definitions. Rationale that still governs a scope's values may stay in its definition; see [Topics Are Not Kinds](#topics-are-not-kinds).

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
- Existing repositories may retain their opted-in tracking conventions; adopting defh does not require them to add or remove working artifacts.

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
- The entry file describes a workflow directly only when no definition owns it, such as installation and commands. Describing owned workflows makes the entry file grow with every feature.
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
