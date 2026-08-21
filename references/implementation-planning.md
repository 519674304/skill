# Implementation Planning

## Plan Separation

Keep plans under `docs/project/plans/`. Do not add implementation tasks to requirements, domain, responsibility, or architecture documents.

## Overall Roadmap

`00-roadmap.md` contains:
- Scope and approved inputs
- Milestones
- Dependency order
- Integration sequence
- Risks and spikes
- Release/acceptance checkpoints
- Links to complex responsibility plans
- Simple responsibility plans that fit in approximately 10-20 lines

It does not duplicate detailed plans.

## Complexity Rule

Keep a responsibility in the roadmap only when its implementation can be unambiguously described in approximately 10-20 lines.

Create `<complex-responsibility>-plan.md` when it includes:
- Multiple modules or layers
- New contracts
- Persistence or migration
- Integration with another context
- Concurrency, caching, or performance work
- Plugin, interceptor, listener, factory, or lifecycle framework
- Several test levels
- Rollout or compatibility risk

## Critical-Path and Token-Investment Review

Before treating a plan as implementation-ready, record:

- the hard or uncertain steps;
- each step's relative reasoning, implementation, and verification cost;
- why that cost is justified by the decisive user output; and
- tempting work deliberately not funded in this iteration.

Use relative bands or percentages, not fabricated exact token counts. If a non-primary concern consumes disproportionate effort, simplify it, defer it, or ask the user to choose before implementation.

## Plan Item Content

Every plan item includes:
- Plan ID
- Requirement IDs
- Context and responsibility IDs
- ADR IDs
- UX IDs and approved prototype baseline for UI work
- Goal
- Dependencies
- Concrete files/modules to add or change
- Contracts and data changes
- Step sequence
- Unit, integration, performance, and acceptance tests as applicable
- Error and rollback handling
- Completion evidence
- Version-control boundary changes: intentional tracked paths, ignored artifact classes, generated-source policy, and staged-diff verification

## Ordering

Prefer:
1. Stable domain contracts and tests
2. Core business behavior
3. Application orchestration
4. Infrastructure adapters
5. UI implementation against the approved prototype baseline
6. Cross-cutting observability and hardening
7. End-to-end acceptance

Adjust when a technical spike must retire a high-risk assumption first.

## Final Plan Review

- Every requirement reaches a plan and acceptance test.
- Every plan has a requirement source.
- Dependencies form an executable order.
- Plans do not conceal unresolved business questions.
- Plans include a critical-path and token-investment review, with non-investments stated explicitly.
- Complex responsibilities have independent plans.
- Integration points have contract tests.
- Performance requirements have benchmark tasks.
- Rollback, migration, and compatibility are included where relevant.
- UI plans reference approved UX IDs and include visual, interaction-state, responsive, and accessibility acceptance checks as applicable.
- Plans prevent dependencies, disposable outputs, caches, logs, local environment files, credentials, and secrets from entering Git unintentionally.
- Lockfiles, migrations, generated source, fixtures, and vendored artifacts have explicit inclusion decisions when ambiguous.
