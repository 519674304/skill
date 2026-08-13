---
name: project-inception
description: Guide a software project from initial context through approved requirements, UI prototyping when applicable, DDD-informed domain and responsibility design, lifecycle and extension design, technology selection, technical architecture, and decoupled implementation plans. Use when starting a new software project, restarting an inadequately designed project, decomposing requirements before coding, or when the user asks for project initiation, requirement analysis, UI or Web application design, business/domain design, architecture design, or implementation planning. Enforce explicit approval gates and do not begin implementation.
---

# Project Inception

Turn a project idea into approved, traceable, implementation-ready documents. Keep requirements, business design, technical architecture, and plans in separate documents.

## Hard Gate

Do not scaffold, code, install project dependencies, or implement behavior while this skill is active.

Complete each phase in order. Do not enter the next phase until:
1. Its documents pass self-review.
2. The user explicitly approves the phase.

If the user changes an approved upstream decision, mark affected downstream documents stale and return to the earliest impacted phase.

## Working Order: Whole, Parts, Safety Net

Apply this order in every phase:

1. **Whole**: settle project-level goals, boundaries, primary flow, major business map, and governing constraints.
2. **Parts**: decompose complex capabilities, contexts, responsibilities, flows, and plans.
3. **Safety net**: audit omissions, cross-boundary flows, exception paths, degradation, rollback, unresolved decisions, and traceability breaks.

Do not start by designing isolated classes, tables, APIs, plugins, or UI components.

## Core Rules

- Use `$brainstorming` to clarify intent one question at a time.
- Prefer facts from existing code and documents over assumptions.
- Separate business requirements from implementation choices.
- In requirements, keep the main flow, sunny-day scenarios, and smoke scenarios primary; collect validation, boundary, and exception cases into a visible issue table for later responsibility and architecture design instead of interrogating every edge case one by one.
- Use DDD proportionally. Record why full, light, or no DDD modeling is appropriate.
- Select patterns only after identifying lifecycle and real variation points.
- Record why plugins, interceptors, listeners, factories, strategies, state machines, or middleware are used or rejected.
- Choose technology and middleware from quantified constraints. Explicitly state when no middleware is needed.
- Maintain requirement-to-test traceability.
- Before choosing exception-handling patterns, define a structured issue taxonomy: category, severity, producing responsibility, receiving responsibility, continuation policy, logging level, and user-facing conversion. Define concrete error codes only when the project needs them.
- Work backward from the project's decisive output. Maintain approved key input and output examples as executable-looking data contracts, and use them to correct requirements, domain design, architecture, and plans when prose drifts.
- Keep simple responsibilities in overview documents only when approximately 10-20 lines fully explain them. Give complex responsibilities their own documents.
- Keep implementation plans separate from requirements and design documents.
- Establish the repository boundary before implementation. Read [references/version-control.md](references/version-control.md). Do not allow dependencies, generated outputs, caches, logs, temporary files, local environment files, credentials, or secrets into version control by accident.
- Treat source-control inclusion as an ownership decision, not a filename guess. Lockfiles, migrations, required generated source, fixtures, and other reproducibility inputs may belong in Git; document the decision when it is not obvious.
- Before any staging or commit operation, inspect repository status, ignore behavior, and the staged diff. Stage reviewed paths intentionally; do not use an indiscriminate repository-wide add while unreviewed or untracked files are present.

## Required Document Structure

Default to the structure in [references/document-structure.md](references/document-structure.md). Adapt paths to an established project convention without merging document responsibilities.

Maintain `docs/project/00-index.md` as navigation and approval state only.

## Workflow

### Phase 0: Explore Context

Inspect existing files, documentation, code, version history, constraints, and prior decisions.

Inspect repository hygiene using [references/version-control.md](references/version-control.md): existing ignore rules, tracked generated files, local-only configuration, secret exposure risk, and the expected treatment of dependencies, outputs, caches, logs, lockfiles, migrations, and generated source. For a new repository, define a minimal technology-specific `.gitignore`; for an existing repository, preserve established intentional tracking decisions unless evidence requires a change.

Produce a concise fact inventory and identify contradictions. Do not make architecture decisions yet.

### Phase 1: Requirements

Read [references/requirements.md](references/requirements.md).

Use brainstorming to establish the whole first: purpose, users, scope, primary scenarios, success metrics, constraints, and delivery stages. Then decompose complex capabilities. Finish with the requirements safety-net audit.

Write the requirements documents and traceable requirement IDs.

Create the project's key example baselines under `docs/project/baselines/`. Read [references/key-example-baselines.md](references/key-example-baselines.md). At minimum, include one primary-flow input example, one expected output example, and an explicit mapping between them. These are required review artifacts, not illustrative appendices.

**Approval gate:** Ask the user to approve the complete requirements set. Stop until approved.

### Phase 2: Experience and Prototyping

Read [references/experience-prototyping.md](references/experience-prototyping.md).

For every Web, desktop, mobile, or other graphical user-interface application, start with a visual low-fidelity prototype after requirements approval. A prose screen list is not a substitute. Validate the screen inventory, navigation, information hierarchy, primary flows, major actions, and essential states without selecting a frontend framework or polishing visual style.

Ask the user to approve the overall experience direction. After approval, ask explicitly whether any uncertain or high-risk flow, interaction state, or responsive layout needs further detail. Refine only what is needed. If no refinement is needed, record the approved low-fidelity prototype as the UI baseline and complete the phase.

For a headless service, library, command-line tool, or background worker, record why this phase is not applicable.

**Approval gate:** Ask the user to approve the prototype baseline or the recorded not-applicable decision. Prototype approval does not authorize frontend development; all downstream gates still apply. Stop until approved.

### Phase 3: Domain and Business Decomposition

Read [references/domain-design.md](references/domain-design.md) and [references/responsibility-design.md](references/responsibility-design.md).

First create the overall business map and decide the appropriate DDD depth. Then identify bounded contexts, context relationships, aggregates, entities, value objects, domain services, domain events, and responsibilities. Split each complex context or responsibility into its own document.

Finish with the domain safety-net audit.

**Approval gate:** Ask the user to approve the domain map, context boundaries, responsibility map, and individual designs. Stop until approved.

### Phase 4: Lifecycle and Extension Design

Read [references/lifecycle-and-patterns.md](references/lifecycle-and-patterns.md).

Define lifecycle states, transitions, invariants, failure paths, cancellation, retry, recovery, and termination before selecting patterns.

Evaluate extension mechanisms and patterns against actual variation points. Define contracts, timing, ordering, failure policy, and isolation for every accepted extension point.

**Approval gate:** Ask the user to approve lifecycle and extension decisions. Stop until approved.

### Phase 5: Technology and Technical Architecture

Read [references/technical-architecture.md](references/technical-architecture.md).

Start from quantified workload, latency, throughput, data volume, memory, deployment, reliability, operability, and security constraints. Compare viable options and document decisions and rejected alternatives.

Define runtime components, dependency direction, data ownership, APIs, persistence, caching, concurrency, observability, deployment, and failure recovery without leaking infrastructure into the domain model.

Finish with the architecture safety-net audit.

**Approval gate:** Ask the user to approve technology choices and technical architecture. Stop until approved.

### Phase 6: Implementation Planning

Read [references/implementation-planning.md](references/implementation-planning.md).

Create `plans/00-roadmap.md` with order, dependencies, milestones, integration points, and simple responsibilities. If a responsibility cannot be implemented clearly in approximately 10-20 lines, create a separate plan document for it.

Every plan item must link requirements, domain/context IDs, responsibility IDs, architecture decisions, concrete changes, tests, and acceptance checks.

Include repository-boundary work when required: ignore-rule updates, generated-code policy, secret-safe configuration examples, and pre-commit verification. Plans must name the files that should be tracked and the classes of local or generated files that must remain untracked.

Finish with the final safety-net audit in [references/final-audit.md](references/final-audit.md).

**Final approval gate:** Ask the user to approve all plans before transitioning to implementation. After approval, invoke `$writing-plans` only if more task-level planning is needed; otherwise hand off to the implementation workflow requested by the user.

## Approval Recording

For every document, record:

```text
Status: Draft | Approved | Superseded
Approved by: <user or role>
Approved at: <date>
Depends on: <document IDs>
```

Do not silently treat conversational agreement on one section as approval of an entire phase. Ask explicitly.

## Traceability

Use stable IDs such as:

```text
REQ-<AREA>-001
UX-<AREA>-001
CTX-<NAME>
RESP-<NAME>
ADR-001
PLAN-<AREA>-001
TEST-<AREA>-001
```

Maintain this chain:

```text
Requirement
  -> Approved Experience Baseline (when applicable)
  -> Bounded Context
  -> Responsibility
  -> Architecture Decision
  -> Implementation Plan
  -> Acceptance Test
```

Block final approval when either:
- A requirement has no implementation and acceptance path.
- A plan item has no requirement source.

## Scope Discipline

- Avoid speculative abstractions.
- Do not introduce a pattern because it is named in the request.
- Do not merge independent bounded contexts for convenience.
- Do not split tiny responsibilities into document noise.
- Do not choose a database, cache, queue, search engine, or plugin framework before proving the need.
- Do not hide unresolved business decisions inside technical assumptions.
