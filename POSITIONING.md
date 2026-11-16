# Positioning

## Short Version

Two kinds of document and one action.
Definitions say what the system does now. Principles say what it must achieve and why. Audit finds where they disagree with each other, with the code, and with the tests.

That is the whole framework. There is no required process: no lifecycle of specs, plans, and tasks to follow, no roles to play, no tracking files to keep. An audit reports what is inconsistent; it does not say who fixes it or how. A capable agent reads the finding and works out the change itself.

It is small on purpose. Agents can already do most of the work. What runs out is attention, the reader's and the agent's. Every extra concept is something each session must load, understand, and then decide to skip. Two nouns and one verb fit in every session's context, every time.

It is inspired by Lisp, and so is its name. defh is short for Definition Harness; the `def` comes from Lisp's `defun`, `defvar`, and `defmacro`, which define things. The framework is written in its own two kinds of document, so the rules and the knowledge they govern have the same form, and an audit can check the framework itself. After adoption the framework dissolves into the repository: the repository's own definitions and principles become the authority and evolve with the project.

It works for new repositories and for old ones. An existing repository starts with one scope and grows from there.

## The Problem

Many repositories have one of these failure modes:

- important intent lives in prompts, chat logs, or people's heads
- implementation moves faster than durable documentation
- tests verify behavior, but the repository cannot clearly explain what the behavior is supposed to be
- specs exist only as temporary planning docs and disappear after implementation

These problems hurt both humans and agents.

Humans lose context and make local changes without enough system understanding.
Agents can move quickly, but without durable in-repo guidance they drift, overfit to local patterns, or produce changes that are hard to review.

## The Core Idea

This kit treats the repository itself as the place where durable product and engineering knowledge should live.

The model is two nouns and one verb:

- `definitions` capture current behavior, including what the code does not do
- `principles` capture intent: what the system must achieve and why
- `audit` checks them against each other, against code and tests, and reports the gaps

Nothing else is required. Architecture, evaluation, and process are topics, not kinds: each statement about them is a definition or a principle. The entry file acts as a map, not a manual; agents load it every session, so it only routes.

When behavior does not guarantee an intent, nobody writes the gap down as documentation. The definition records the facts, including what the code does not do; the principle states the intent and, when it can, the condition that would violate it. The audit puts the two side by side and reports the gap. Editing the principle does not make the gap go away; only a code change or an explicit, reasoned acceptance of the risk does.

The goal is not just better prompting. The goal is a codebase that gradually becomes easier to reason about.

Just as important: this documentation layer is meant to live inside a larger quality system, not replace one.

## What Makes It Different From Typical Spec-Mode Workflows

Many spec-driven workflows are centered on the lifecycle of a piece of work:

`idea -> spec -> plan -> tasks -> implementation`

That is useful, but it is not the main focus here.

Those workflows ask every contributor, human or agent, to remember a process. This framework asks them to remember two nouns and one verb.

This kit is centered on the lifecycle of repository knowledge:

`intent -> behavior -> implementation -> verification -> maintenance`

The difference matters.

- In many spec-mode systems, the feature spec is the center.
- In this kit, the repository's long-lived knowledge layer is the center.

That makes the framework:

- more persistent
- more maintainable
- more suitable for refactors and long-term operation
- more useful for future humans and future agent runs

## Why "Spec-Anchored"

This framework is best described as `spec-anchored`.

The definitions are not disposable planning artifacts. They remain in the repository and continue shaping:

- maintenance
- refactors
- tests
- reviews
- future agent behavior

The docs are part of the operating model of the repository, not just pre-coding paperwork.

## Written In Its Own Terms

The framework is written in its own two kinds of document: `documentation-definition.md`, `documentation-principles.md`, `definition-audit-definition.md`, and `evolution-principles.md`.
Rules and the knowledge they govern have the same form, so an audit can check the framework itself. This is the idea Lisp calls homoiconicity: code and data share one representation, so a program can read and change programs. Here, the rules for documentation are documentation, and the audit that checks a repository also checks the framework.

The same idea shapes adoption. After adoption the framework dissolves into the repository. The repository's own definitions and principles are its authority, and they evolve with the project. The framework learns from what adopters do well; upgrading is optional.

This repository is not an agent runtime or an evaluation service. It supplies no model loop, scheduler, sandbox, or approval system. External agent tools act on the repository; the repository supplies the definitions, principles, and audit contract they act against. Plans, progress, and handoff state stay in those tools unless a repository chooses to keep them.

## Why It Works For Legacy Repositories

This approach does not require a perfect greenfield setup.

You can adopt it gradually:

1. Start with one unstable or high-value subsystem.
2. Write a small number of principles and definitions.
3. Align tests with the new behavioral claims.
4. Make future changes update those docs.
5. Expand outward over time.

That makes it practical for:

- inherited codebases
- partially documented systems
- exploratory projects
- teams still learning the domain

## Relationship To Quality Tooling

This framework does not replace engineering controls such as:

- typed or schema-validated boundaries
- static analysis and linting
- automated tests
- coverage or another change-risk signal
- CI enforcement

It works with them.

defh helps the project preserve intent and behavior.
The engineering toolchain helps prevent that behavior from degrading silently.

Together, they create a more stable environment for both human and agent contribution.

This part is generalized by function, not by specific vendor or language tool.

Every adopting repository should define its own native toolchain for those roles.

Examples:

- Python: type checker or schema validation, linter, `pytest`, coverage, CI
- Go: `go test`, linter, race detector, benchmarks, CI
- Rust: compiler checks, `clippy`, `cargo test`, coverage, CI
- JVM projects: build checks, static analysis, JUnit, coverage, CI

In the originating project, one concrete implementation of that broader pattern included:

- strict TypeScript compilation
- ESLint with explicit TypeScript boundary rules
- Vitest unit testing
- coverage reporting plus stricter patch-coverage checks
- CI gates for lint, typecheck, coverage, and deterministic regression validation
- PR templates that require explicit validation and documentation reporting
- reproducible workload and scenario-based validation for performance- and behavior-sensitive changes

That example matters because it shows the real shape of the method:

not "documentation instead of engineering rigor,"
but documentation combined with mechanical checks and domain-specific validation loops.

## Practical Value

In practice, this approach is useful when:

- you want agents to move quickly without losing the plot
- you are working in a domain you do not fully know yet
- you need a way to preserve what has been learned from spikes and iteration
- you want the codebase to become more understandable over time instead of less

That is the real promise of the kit:

not heavier process for its own sake, but a way for a software project to keep accumulating usable intent, behavior, and verification as it grows.
