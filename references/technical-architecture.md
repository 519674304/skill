# Technology Selection and Architecture

## Quantify Before Selecting

Collect:
- Users and concurrency
- Request and event rates
- Data size and growth
- Read/write patterns
- Latency percentiles
- Memory and CPU limits
- Local, server, cloud, or edge deployment
- Availability and recovery objectives
- Security/compliance
- Offline requirements
- Team skills and operational capacity
- Team familiarity with selected languages, frameworks, and runtime tools

Do not select technology from popularity alone.

## Option Evaluation

For each material choice, compare 2-3 viable options:
- Requirement fit
- Performance
- Operational burden
- Development cost
- Portability
- Failure modes
- Exit/migration cost

Record the decision as an ADR ID with rejected alternatives.

## Middleware Decision

Evaluate databases, caches, queues, search engines, object storage, workflow engines, and plugin frameworks only when requirements justify them.

For each candidate ask:
1. What quantified problem does it solve?
2. Can an in-process or embedded solution meet the requirement?
3. What new operational and consistency cost does it add?
4. What is the fallback if it is unavailable?

Explicitly record "no middleware" when appropriate.

## Technical Architecture Document

Define:
- Runtime components
- Layer and dependency direction
- Domain/application/infrastructure/UI boundaries
- APIs and contracts
- Data ownership and persistence
- Cache strategy and invalidation
- Concurrency and idempotency
- Background processing
- Configuration and secrets
- Deployment and startup
- Observability
- Error handling and recovery
- Security boundaries
- Performance test strategy
- Migration and compatibility
- Code readability and documentation strategy for unfamiliar technologies

## Decoupling Rules

- UI consumes view/application models, not storage records.
- Data acquisition, processing, and presentation are separate.
- Infrastructure adapters implement inner-layer ports.
- Business rules do not depend on framework types.
- Technology replacement should not alter domain semantics.
- When using unfamiliar languages or frameworks, architecture must define how code explains itself: module responsibility headers, public type/function documentation, important invariants, failure policy, and step comments for complex flows. Avoid clever abstractions, macros, or generic layers that make code the only understanding entry point.

## Safety-Net Audit

- Every component has a clear owner and responsibility.
- Dependencies point inward toward stable policy.
- No circular runtime or document dependencies.
- Failure of optional components has defined degradation.
- Data consistency and transaction boundaries are explicit.
- Capacity assumptions match requirements.
- Observability can prove acceptance criteria.
- Technology choices are reversible where change is plausible.
- New or unfamiliar technology has an explicit readability and onboarding strategy.
