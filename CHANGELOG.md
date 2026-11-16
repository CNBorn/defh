# Changelog

## 2.0.0

Definition Harness is now **defh**: two kinds of document, definitions and principles, and one action, audit. There is no required process.

This is a breaking release for the framework's own files: several files and templates are removed. It asks nothing of adopters. Local copies of removed files, adopted-scope tables, file-based audit records, and the old name remain valid. Upgrading is optional.

### Name

- Rename the framework to defh, short for Definition Harness, pronounced "def-H". The `def` follows Lisp's `defun`, `defvar`, and `defmacro`. The repository moves from `CNBorn/definition-harness` to `CNBorn/defh`. Document names and "Definition Audit" are unchanged.
- Rename `documentation/harness-evolution-principles.md` to `documentation/evolution-principles.md`.

### Two kinds of authority

- A statement is authority when it lives in a definition or principles file, or in a topic file that local documentation rules name as governing, such as a runbook or `architecture.md`. Other files are not authority.
- Definitions describe current behavior, including the mechanism and what the code does not do, and must be checkable. Principles state intent, including checkable invariants that current code may not guarantee; a principle should state its violation condition when one can be stated.
- A check that does not exist yet is not a definition: the invariant goes to principles and the work to a working file.
- A rubric with pass conditions that gates acceptance is a definition; a rubric that only guides judgment is a principle.
- The pre-merge "verify tested and documented separately" step becomes the principle that tested and documented are different; there is no required pre-merge step. The end state stays: at merge, touched documents use no stale terms and touched definitions match the final implementation.
- Architecture, evaluation, process, and reusable procedures are topics, not document kinds. A definition may keep rationale that governs only its own scope. The two definition levels are now called domain and topic definitions; "system" and "item" remain valid.
- Working files, such as studies and research notes, are valid under any name, are not authority, and need not be listed. defh neither requires nor limits them. A "Draft" status line does not change authority. A conclusion is lasting when a later change must respect it, and moves to a definition or principles. Authority files may cite working files as evidence but must state the rule themselves.
- Add the Same-Change Update principle: a behavior change updates its owning definition, the tests that check the changed claims, and derived outputs such as manuals and skills in the same change. Derived outputs are not authority. Evidence artifacts, such as formal models, follow the scope's definition.

### Audit

- Gaps between intent and behavior are audit findings, not document content. A fact names what the code does or does not do; a gap names an intent the facts fail to meet. Principle results are followed, not guaranteed, or violated, reported in their own section. A gap is reported when found, cannot be cleared by editing the principle or removing the exposing claim, and closes only by a code change or a stated risk acceptance in principles.
- Every audit states its window: start and end revisions. A last-run record is optional; the recommended place is the audit PR title, such as `Definition audit: <scope> through <revision>`. File-based records, including "Reviewed against" lines, remain valid.
- Audits also report non-authority content inside definitions, and any document that restates another authority file.

### Adoption

- A scope is adopted when it has a definition. The adopted-scope table becomes an optional scope map; when kept, it is the only document index.
- `ADOPTION.md` is a governing topic file with one adoption path, four starter files, and prompts. The entry-file shrink becomes an audit finding. Delegated-work, working-doc, and PR-closure guidance is removed.
- Templates go from twelve to five: definition (system and item merged), principles (with an optional violation condition), definition audit (with principle results), entry file (absorbs the README docs section), and local documentation rules (local choices and links only; no copied rules).

### Removed

- `documentation/development-flow.md`, `documentation/agent-workflow-definition.md`, and the generic `documentation/architecture.md`. Rubric guidance moves to the evaluation topic in the documentation definition.
- The evaluation, architecture, acceptance-contract, agent-progress, adopted-scope, system-definition, item-definition, and README-docs-section templates.
- `code-structure-principles.md` and `programming-principles.md` move to `examples/principles/`. They are principles an adopter may write for its own code.

### Evolution and positioning

- Add evolution principles: the framework dissolves into each adopter, local drift is valid, upgrades are optional, and the framework learns from adopters.
- Rewrite POSITIONING around the pitch: two kinds of document and one action, no required process, attention as the scarce resource, and the Lisp-inspired idea that the framework is written in its own terms.
- Move the helpdesk platform example to 2.0. Its escalation definition records a mechanism that does not guarantee one of its principles, so an audit of the example finds a gap.

## 1.4.2

- Definitions describe implemented behavior. A repository without code completes adoption without a definition; the first definition is written from the first implemented behavior.
- Full-repository adoption uses the local documentation rules template, with an adopted-scope table that may start empty. The template links to the pinned harness rules instead of copying them; its filename is unchanged.
- Explain how to handle links in copied starter docs that point to harness documents outside the starter set.
- Existing adopters need no action.

## 1.4.1

- Add entry-file rules. The entry file only routes: how to run, development commands, the reading route, validation commands, and one-sentence links for always-visible constraints.
- Ownership comes first. When a definition owns a user or operator workflow, the entry file links to it and does not restate it. "README covers workflows" now applies only to workflows without an owner, such as installation and commands.
- Behavior and operation changes update only the owning definition. A new adopted scope updates only the adopted-scope table. The entry file changes only when its routing content changes.
- Make the local documentation definition and its adopted-scope table the only document index. Keep the entry file in the documentation language, without translated copies. Move content without an owner to its owner or leave it to code and tests.
- Define entry duties as roles, not files. One `README.md` with `AGENTS.md` as a relative symlink is recommended, not required. Pointer files and separate files remain valid. Document symlink limits and a `readlink` check.
- Add "Shrink An Existing Entry File" with an orphan check. Shrink `README.md` before converting `AGENTS.md` to a symlink, and record the agent entry size before and after in the PR. Add the "Small Routing Entry" principle, and `templates/entry-file.template.md`. Align development flow, audit scope, adoption guidance, and templates.
- Apply the rules to this repository. `README.md` is routing-only and `AGENTS.md` links to it. Adoption prompts, starter files, and scoped-adoption examples moved to `ADOPTION.md`.
- Existing adopters need no action. Paths, separate entry files, existing navigation, and entry content written before 1.4.1 remain valid. Shrinking an existing entry file is optional, needs user approval, and confirms that owners contain every fact before deleting.
- Add an Adoption Outcome checklist and concrete starter-file template paths to `ADOPTION.md`.

## 1.4.0

- Add an on-demand Definition Audit contract and task template. Include applicable principles, evaluation definitions, architecture constraints, and workflow rules.
- Require claim-level evidence, separate test coverage, explicit conflicts and uncertainty, and coverage limits. Report findings before repairs without assuming which pillar is correct.
- Add flat domain/topic naming guidance with at most two semantic levels and explicit governing links.
- Prevent agents from adding or expanding manual inventories of every Markdown file unless requested or required by explicit local policy. Keep focused entry points, adopted-scope tables, and generated discovery available.
- Align agent routing, adoption guidance, development flow, and authoring templates with the new defaults.
- Preserve existing paths, filenames, directory structures, navigation, and explicit local policies. Audits are opt-in; no migration, default CI gate, or repository report is required.

## 1.3.0

- Add STE-inspired writing rules and guidance for tables, charts, and editable diagrams.
- Simplify document types, work roles, adoption guidance, and development flow. Add a Mermaid evaluation loop and align authoring templates.
- Default repository capture to final behavior, stable rationale, reusable evaluation criteria, and final validation evidence.
- Make implementation guides, context, progress, handoff, and acceptance-contract files opt-in through user requests or explicit repo-local policy.
- Remove automatic repository tracking requirements for delegated, multi-session, and unattended work, while preserving existing opted-in conventions and templates.
- Remove the delegated-work artifact reporting section from the default PR template.
- Preserve existing docs paths, definitions, and explicit working-artifact policies. No migration is required.

## 1.2.0

- Add a vendor-neutral repository contract for delegated agent work.
- Define initializer, implementer, evaluator, and closer as work roles rather than runtime components.
- Add progress, acceptance-contract, and evaluation-definition guidance for external agent harnesses.
- Add templates for delegated-work progress, acceptance contracts, and evaluation definitions.
- Expand evaluation guidance for rubric-based review, baseline examples, anti-patterns, and evaluator calibration.
- Update the PR template to capture evaluation evidence and delegated-work artifact closure.

## 1.1.0

- Add scoped adoption guidance for existing and partially adopted repositories.
- Add backward-compatibility guidance for repositories already using the original `documentation/` model.
- Add `ADOPTION.md`.
- Add templates for existing-repo documentation rules and adopting one scope at a time.
- Shorten `README.md` into an agent-oriented landing page.
- Make prompt-based adoption the primary README quick start path.
- Add `VERSION`.
- Add harness evolution principles for future compatibility-aware changes.
