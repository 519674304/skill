# Responsibility Design Phase

## Whole First

Create `00-responsibility-map.md` showing:
- Responsibility ID and name
- Owning bounded context
- Purpose
- Requirements covered
- Inputs and outputs
- Dependencies
- Complexity classification
- Detailed document link when needed

## Responsibility Test

A responsibility should:
- Have one clear business or application purpose.
- Have one primary reason to change.
- Expose a stable contract.
- Hide internal implementation.
- Be testable without unrelated responsibilities.

Do not force one class per responsibility. A responsibility may be a module, service, aggregate, policy, pipeline stage, or adapter.

## Complex Responsibility Document

Include:
- Responsibility ID
- Purpose and non-goals
- Requirements and context
- Public contract
- Inputs, outputs, and invariants
- Internal workflow
- State and lifecycle participation
- Dependencies and dependency direction
- Errors and recovery
- Concurrency/idempotency rules
- Extension points
- Observability
- Test boundary
- Alternatives considered

## Dependency Rules

- Domain responsibilities depend on domain abstractions.
- Application responsibilities orchestrate use cases.
- Infrastructure implements ports owned by inner layers.
- UI consumes application contracts and does not own domain rules.
- Cross-context access goes through explicit contracts.

## Adaptive Documentation

Keep a responsibility in the map when approximately 10-20 lines fully describe it.

Split it when it has:
- Multiple workflow steps
- State transitions
- External integration
- Complex error handling
- Performance-sensitive algorithms
- Extension mechanisms
- Several collaborators
- Independent implementation or release risk

## Safety-Net Audit

- Each responsibility has an owner.
- No two responsibilities silently own the same rule.
- No responsibility is a miscellaneous utility bucket.
- Inputs and outputs are explicit.
- Failure ownership is explicit.
- Test boundaries align with responsibility boundaries.
- UI changes can occur without moving business rules.
