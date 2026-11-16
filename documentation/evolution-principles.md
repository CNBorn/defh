# Evolution Principles

This document defines stable principles for evolving Definition Harness itself.

## Intent

Definition Harness should improve by learning from adopted repositories, without forcing churn on them.

The framework may become clearer, stricter, or better documented over time, but compatibility should be an explicit design concern for every version change.

## Principle 1: The Framework Dissolves Into Each Adopter

- After adoption, the repository's own definitions and principles are its authority. The framework is the source they started from, not a dependency.
- An adopter's local rules evolve with the project and may drift from the current framework. Drift is valid.
- Upgrades are optional, including breaking versions. A breaking version changes what new adopters start from. It does not make an existing adopter invalid.
- A framework change must not require an adopter to act. An adopter that upgrades takes only the parts it wants.

## Principle 2: Learn From Adopters

- The framework evolves mainly from practices that worked in adopted repositories, and from failures observed there.
- An adopter that evolved well is the framework's implemented behavior. Audit a framework draft against that adopter before release.
- A PR that adds or removes a framework rule explains the rule on its own merits. It may cite adopter evidence when that evidence can be shared publicly.
- Keep project-specific practice in the adopter. Generalize only the part that does not depend on the project's domain.

## Principle 3: Preserve Adopted Repository Compatibility

- Existing adopted repositories should not need to rename docs paths, rewrite stable definitions, or restructure working documentation systems for a non-breaking version.
- Full-adoption repositories using `documentation/` remain valid. A breaking version does not change this; see Principle 1.
- Scoped-adoption repositories using `docs/` or another established docs path remain valid when their local documentation rules are consistent.

## Principle 4: Additive Guidance Before Migration

- Prefer adding guidance, templates, and clarification over requiring migration.
- When a new concept is introduced, explain how it relates to the previous model.
- A breaking release states the incompatibility and explains why. It describes how an adopter can take the new version, but taking it stays optional; see Principle 1.

## Principle 5: Compatibility Is Tested Against Adoption Shapes

Before changing core rules or templates, evaluate at least these adoption shapes:

- a full-adoption repository with `documentation/`, many definitions, and strict PR documentation rules
- a scoped-adoption legacy repository with an existing `docs/` directory and mixed stable/temporary docs
- a new repository copying the current starter files

The change should not make any valid prior adoption shape invalid unless the release is intentionally breaking.

## Principle 6: Version Changes Need Operator-Facing Notes

- Update `VERSION` when the framework version changes.
- Update `CHANGELOG.md` with the behavior of the version change.
- Update `README.md` when the agent landing path changes.
- Update `ADOPTION.md` when adoption steps, starter files, compatibility rules, or migration expectations change.
- PRs that change framework rules or templates should explain compatibility impact.

## Principle 7: Keep Meta-Rules In The Repository

Important rules for evolving the harness belong in repository files, not only in prompts or discussion history.

Use:

- `documentation/evolution-principles.md` for stable evolution principles
- `ADOPTION.md` for adopter-facing compatibility and adoption guidance
- `CHANGELOG.md` for version-level changes
- PR descriptions for one-time migration notes, rejected options, and validation details
