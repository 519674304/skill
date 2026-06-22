---
name: project-inception
description: Guide a software project from initial context through approved requirements, DDD-informed domain and responsibility design, lifecycle and extension design, technology selection, technical architecture, and decoupled implementation plans. Use when starting a new software project, restarting an inadequately designed project, decomposing requirements before coding, or when the user asks for project initiation, requirement analysis, business/domain design, architecture design, or implementation planning. Enforce explicit approval gates and do not begin implementation.
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
- Use DDD proportionally. Record why full, light, or no DDD modeling is appropriate.
- Select patterns only after identifying lifecycle and real variation points.
- Record why plugins, interceptors, listeners, factories, strategies, state machines, or middleware are used or rejected.
- Choose technology and middleware from quantified constraints. Explicitly state when no middleware is needed.
- Maintain requirement-to-test traceability.
- Keep simple responsibilities in overview documents only when approximately 10-20 lines fully explain them. Give complex responsibilities their own documents.
- Keep implementation plans separate from requirements and design documents.

## Required Document Structure

Default to the structure in [references/document-structure.md](references/document-structure.md). Adapt paths to an established project convention without merging document responsibilities.

Maintain `docs/project/00-index.md` as navigation and approval state only.

## Workflow

### Phase 0: Explore Context

Inspect existing files, documentation, code, version history, constraints, and prior decisions.

Produce a concise fact inventory and identify contradictions. Do not make architecture decisions yet.

### Phase 1: Requirements

Read [references/requirements.md](references/requirements.md).

Use brainstorming to establish the whole first: purpose, users, scope, primary scenarios, success metrics, constraints, and delivery stages. Then decompose complex capabilities. Finish with the requirements safety-net audit.

Write the requirements documents and traceable requirement IDs.

**Approval gate:** Ask the user to approve the complete requirements set. Stop until approved.

### Phase 2: Domain and Business Decomposition

Read [references/domain-design.md](references/domain-design.md) and [references/responsibility-design.md](references/responsibility-design.md).

First create the overall business map and decide the appropriate DDD depth. Then identify bounded contexts, context relationships, aggregates, entities, value objects, domain services, domain events, and responsibilities. Split each complex context or responsibility into its own document.

Finish with the domain safety-net audit.

**Approval gate:** Ask the user to approve the domain map, context boundaries, responsibility map, and individual designs. Stop until approved.

### Phase 3: Lifecycle and Extension Design

Read [references/lifecycle-and-patterns.md](references/lifecycle-and-patterns.md).

Define lifecycle states, transitions, invariants, failure paths, cancellation, retry, recovery, and termination before selecting patterns.

Evaluate extension mechanisms and patterns against actual variation points. Define contracts, timing, ordering, failure policy, and isolation for every accepted extension point.

**Approval gate:** Ask the user to approve lifecycle and extension decisions. Stop until approved.

### Phase 4: Technology and Technical Architecture

Read [references/technical-architecture.md](references/technical-architecture.md).

Start from quantified workload, latency, throughput, data volume, memory, deployment, reliability, operability, and security constraints. Compare viable options and document decisions and rejected alternatives.

Define runtime components, dependency direction, data ownership, APIs, persistence, caching, concurrency, observability, deployment, and failure recovery without leaking infrastructure into the domain model.

Finish with the architecture safety-net audit.

**Approval gate:** Ask the user to approve technology choices and technical architecture. Stop until approved.

### Phase 5: Implementation Planning

Read [references/implementation-planning.md](references/implementation-planning.md).

Create `plans/00-roadmap.md` with order, dependencies, milestones, integration points, and simple responsibilities. If a responsibility cannot be implemented clearly in approximately 10-20 lines, create a separate plan document for it.

Every plan item must link requirements, domain/context IDs, responsibility IDs, architecture decisions, concrete changes, tests, and acceptance checks.

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
CTX-<NAME>
RESP-<NAME>
ADR-001
PLAN-<AREA>-001
TEST-<AREA>-001
```

Maintain this chain:

```text
Requirement
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

