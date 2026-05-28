<!-- Sync Impact Report
Version change: (none) → 1.0.0
Modified principles: N/A — initial fill from template
Added sections: All (Core Principles, Development Standards, Quality Gates, Governance)
Removed sections: None
Templates requiring updates:
  - .specify/templates/plan-template.md ✅ reviewed — Constitution Check gate already present
  - .specify/templates/spec-template.md ✅ reviewed — no updates needed
  - .specify/templates/tasks-template.md ✅ reviewed — no updates needed
  - .specify/templates/commands/ ⚠ no command files found — skipped
Follow-up TODOs:
  - TODO(TECH_STACK): Confirm primary language, framework, and runtime versions
-->

# mr_agent Constitution

## Core Principles

### I. Spec-Driven Development

Every feature MUST begin with a written specification before any implementation starts.
The workflow MUST follow the four-phase sequence: Spec → Plan → Tasks → Implement — no phase
may be skipped or reordered.
Specifications MUST remain technology-agnostic; implementation details belong in the plan phase.

**Rationale**: Skipping the spec phase has historically led to rework when requirements were
misunderstood. Written specs create a shared contract between humans and the AI agent.

### II. AI-Augmented Workflow

Claude Code is the primary development agent; all implementation MUST be driven through
Spec-Kit commands (`/speckit-specify`, `/speckit-plan`, `/speckit-tasks`, `/speckit-implement`).
Human review is REQUIRED at each phase gate before the next phase begins.
Ad-hoc coding that bypasses the Spec-Kit workflow MUST be justified and documented.

**Rationale**: The AI agent is only as good as the instructions given to it. Structured phases
ensure the agent operates within a known, auditable scope at each step.

### III. Test-First Quality

Tests MUST be authored and confirmed to fail before implementation begins (Red-Green-Refactor).
Contract tests are REQUIRED for all external interfaces and API boundaries.
Integration tests are REQUIRED for all inter-component communication paths.
Tests MUST NOT be mocked at the database or vector-store layer — use real instances.

**Rationale**: Mock-based tests have previously masked integration failures at the storage layer;
real-instance tests are mandatory to prevent regression.

### IV. Simplicity & YAGNI

Every design decision MUST be justified against the current requirement — not hypothetical future
needs. Three similar implementations are preferred over a premature abstraction.
Complexity MUST be documented in the plan's Complexity Tracking table with explicit rationale.
No feature flags or backwards-compatibility shims unless the deployment context requires them.

**Rationale**: AI-generated code tends toward over-engineering. This principle keeps scope tight
and output reviewable.

### V. Observability

All agent operations MUST emit structured logs to the `logs/` directory.
Vector store operations (ChromaDB) MUST be instrumented with query latency and result counts.
Errors MUST surface with sufficient context for diagnosis without requiring code inspection.
No silent failures: every caught exception MUST be logged before being swallowed.

**Rationale**: The agent's reasoning is opaque without structured logging. Observability is the
primary debugging surface for AI-driven systems.

## Development Standards

TODO(TECH_STACK): Confirm primary language, framework, and runtime versions for this project.

- All code MUST pass linting and formatting checks before merge.
- Dependencies MUST be pinned to exact versions in lock files.
- Secrets MUST NOT be committed; use `.env` (gitignored) for local configuration.
- ChromaDB collections MUST be named consistently and documented in `docs/`.

## Quality Gates

Each phase transition requires explicit sign-off before proceeding:

| Gate | Criteria |
|------|----------|
| Spec → Plan | Spec reviewed; acceptance scenarios defined; priorities assigned (P1/P2/P3) |
| Plan → Tasks | Architecture reviewed; Constitution Check passed; dependencies identified |
| Tasks → Implement | Tasks are atomic, dependency-ordered, and independently testable |
| Implement → Done | All tests pass; observability confirmed; `docs/` updated |

## Governance

This constitution supersedes all other development practices and conventions for mr_agent.
Amendments MUST be documented with a version bump rationale and propagated to all dependent
templates via `/speckit-constitution`.
All pull requests MUST include a Constitution Check verifying compliance with active principles.
Complexity violations MUST be justified in the plan before implementation begins.

**Versioning policy**:
- MAJOR: Removal or redefinition of a core principle (breaking governance change).
- MINOR: New principle or section added; materially expanded guidance.
- PATCH: Clarifications, wording refinements, non-semantic edits.

**Amendment procedure**: Draft change → run `/speckit-constitution` → version bump → PR with
"docs: amend constitution to vX.Y.Z" commit message.

**Compliance review**: Each `/speckit-plan` execution MUST re-evaluate the Constitution Check
gate against the current version of this document.

**Version**: 1.0.0 | **Ratified**: 2026-05-28 | **Last Amended**: 2026-05-28
