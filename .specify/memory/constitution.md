<!--
Sync Impact Report
- Version change: N/A → 1.0.0
- Modified principles:
	- [PRINCIPLE_1_NAME] → Code Quality Discipline (NON-NEGOTIABLE)
	- [PRINCIPLE_2_NAME] → Testing Standards (NON-NEGOTIABLE)
	- [PRINCIPLE_3_NAME] → User Experience Consistency
	- [PRINCIPLE_4_NAME] → Performance Requirements
	- [PRINCIPLE_5_NAME] → Modular Architecture & Encapsulation
- Added sections: Defined "Additional Constraints"; Defined "Development Workflow & Quality Gates"
- Removed sections: None
- Templates requiring updates:
	- ✅ .specify/templates/plan-template.md (Constitution Check gates aligned)
	- ✅ .specify/templates/tasks-template.md (tests policy aligned to mandatory)
	- ✅ .specify/templates/spec-template.md (added performance requirements guidance)
- Follow-up TODOs: None
-->

# My Tools Constitution

## Core Principles

### Code Quality Discipline (NON-NEGOTIABLE)
All contributed code MUST meet the following quality controls:
- Linting and formatting: All linters and formatters MUST pass with zero
	errors. Repository-standard rules are authoritative.
- Static analysis: No High/Critical findings MAY be merged. Medium findings
	require explicit, documented waivers.
- Complexity and duplication: Functions SHOULD target cyclomatic complexity ≤ 10
	and MUST avoid copy-paste duplication above trivial levels. Exceeding cases
	require a justification in the PR description.
- Naming and structure: Public APIs, modules, and files MUST use clear, stable
	names. Dead code and unused dependencies MUST be removed.
- Documentation: Public functions, modules, and user-facing behaviors MUST be
	documented at the point of change.

Rationale: Enforces maintainability, readability, and long-term velocity.

### Testing Standards (NON-NEGOTIABLE)
Testing is mandatory and enforced via CI for every change:
- TDD preferred; at minimum, tests for new/changed behavior MUST be authored in
	the same PR and run in CI before merge.
- Coverage: New/changed lines MUST be covered. Projects SHOULD maintain overall
	coverage ≥ 80% unless justified.
- Test types: Unit tests for logic; integration/contract tests where modules
	interact; regression tests for fixed defects.
- Test quality: Tests MUST be deterministic, isolated, and named for intent.
	Flaky tests MUST be fixed or quarantined with an issue.

Rationale: Prevents regressions and encodes behavior as living specification.

### User Experience Consistency
User-facing interfaces (CLI, APIs, UI) MUST be consistent and predictable:
- Conventions: Naming, flags/options, error codes/messages, and exit statuses
	MUST follow project standards across tools.
- Outputs: Where applicable, provide both human-readable and JSON output modes.
- Documentation: Any UX change MUST update reference docs and quickstarts.
- Accessibility and clarity: Messages MUST be concise, actionable, and avoid
	jargon.

Rationale: Consistency reduces cognitive load and support burden.

### Performance Requirements
Performance is a first-class requirement and MUST be specified and enforced:
- Budgets: Each feature/plan MUST declare measurable performance budgets (e.g.,
	latency p95, throughput, memory/CPU caps) appropriate to its domain.
- Guardrails: CI SHOULD include benchmarks or representative performance checks
	when feasible. Merges MUST NOT regress previously established budgets unless
	explicitly approved with rationale.
- Profiling-first: Optimize based on measured profiles; premature optimization
	is discouraged but performance observability is required.

Rationale: Keeps the system fast, efficient, and sustainable at scale.

### Modular Architecture & Encapsulation
The codebase MUST be modular with strong encapsulation boundaries:
- Single responsibility: Modules and services MUST have clear, focused
	purposes and stable public interfaces.
- Encapsulation: Internal details MUST NOT leak across boundaries. Use
	dependency injection or adapters for integration points.
- Contracts and versioning: Module contracts MUST be explicit. Breaking
	changes require a migration path and semantic versioning of the contract.
- Reuse: Prefer libraries/CLIs with clear text I/O contracts over ad-hoc
	cross-module coupling.

Rationale: Promotes reuse, testability, and safer evolution.

## Additional Constraints

- Definition of Done MUST include: passing quality gates (below), updated docs,
	and green CI on main supported platforms.
- Backward incompatibilities MUST be documented in release notes with a clear
	migration guide when applicable.
- Observability SHOULD be sufficient to troubleshoot performance and correctness
	(structured logs and actionable error messages for user-facing tools).

## Development Workflow & Quality Gates

Every PR MUST pass the following gates before merge:
- Code Quality Gate: Linters/formatters pass; no High/Critical static analysis
	issues; complexity/duplication within agreed thresholds or justified.
- Testing Gate: Required unit and integration/contract tests added/updated;
	new/changed lines covered; tests deterministic in CI.
- UX Consistency Gate: Interfaces, messages, and outputs conform to standards;
	docs/quickstarts updated.
- Performance Gate: Feature plan specifies budgets; no regressions beyond
	thresholds; add/adjust benchmarks where appropriate.
- Modularity Gate: Clear ownership and boundaries; no circular dependencies;
	contracts documented when touching public interfaces.

## Governance

- Authority: This constitution supersedes informal practices where in conflict.
- Amendments: Propose via PR including: change summary, rationale, impact, and
	migration guidance if needed. Approval by project maintainers required.
- Versioning Policy: Semantic versioning for this document
	(MAJOR.MINOR.PATCH). MAJOR for incompatible governance changes; MINOR for new
	principles/sections or material expansions; PATCH for clarifications.
- Compliance: Code reviews MUST verify compliance with all gates; violations
	require explicit, documented waivers approved by maintainers.

**Version**: 1.0.0 | **Ratified**: 2025-11-28 | **Last Amended**: 2025-11-28
