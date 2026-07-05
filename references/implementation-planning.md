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

## Plan Item Content

Every plan item includes:
- Plan ID
- Requirement IDs
- Context and responsibility IDs
- ADR IDs
- Goal
- Dependencies
- Concrete files/modules to add or change
- Contracts and data changes
- Step sequence
- Unit, integration, performance, and acceptance tests as applicable
- Error and rollback handling
- Completion evidence

## Ordering

Prefer:
1. Stable domain contracts and tests
2. Core business behavior
3. Application orchestration
4. Infrastructure adapters
5. UI integration
6. Cross-cutting observability and hardening
7. End-to-end acceptance

Adjust when a technical spike must retire a high-risk assumption first.

## Final Plan Review

- Every requirement reaches a plan and acceptance test.
- Every plan has a requirement source.
- Dependencies form an executable order.
- Plans do not conceal unresolved business questions.
- Complex responsibilities have independent plans.
- Integration points have contract tests.
- Performance requirements have benchmark tasks.
- Rollback, migration, and compatibility are included where relevant.

