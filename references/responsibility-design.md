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
- Validation, boundary, and exception handling ownership
- Issue categories, severities, receivers, continuation policies, logging levels, and user-facing conversion
- Observability
- Test boundary
- Alternatives considered

## Validation and Exception Design

When requirements contain an issue table for validation, boundary, or exception cases, resolve it during responsibility and lifecycle design. Consider these patterns only after identifying real variation points and lifecycle timing:

Before selecting a pattern, define a project-wide structured issue contract containing:

- Category: the business or technical area that owns the problem.
- Severity: use `TIP`, `WARNING`, and `EXCEPTION` by default unless approved project language requires different names.
- Source: the responsibility that detects and produces the issue.
- Receiver: the responsibility that owns the response policy for the category.
- Location and structured details: enough context to identify the affected file, record, rule, request, stage, or operation.
- Cause: the underlying technical exception when one exists; it may be absent.
- Continuation policy: continue, skip, degrade, or abort the current operation.

Define severity behavior before concrete codes:

- `TIP`: continue; log at `INFO`; optionally show a non-blocking user message.
- `WARNING`: continue, skip, or degrade according to the category policy; log at `WARN`.
- `EXCEPTION`: abort the current operation and preserve the last valid state; log at `ERROR`.

Use category to select the receiving handler and severity to select the generic control-flow and logging policy. Producing responsibilities emit structured issues and must not assemble UI text. Preserve technical causes for diagnostics, but do not expose raw stack traces to users.

Do not invent a full error-code catalog during project inception unless concrete codes are required for an external contract, compatibility, operations, or acceptance. It is sufficient to approve categories, severities, receivers, and handling policies first. A later code format may follow `<CATEGORY>-<SEVERITY>-<SEQUENCE>` or an approved project convention.

Require every validation, warning, and exception path to follow this flow:

```text
Detect issue
  -> create structured issue
  -> route by category to the owning receiver
  -> apply severity policy
  -> perform recovery, degradation, or abort
  -> log at the mapped level
  -> convert to a user-facing result at the application boundary
```

Record this taxonomy and flow in the responsibility map. Give unified issue routing and handling its own complex responsibility document when several categories, receivers, recovery policies, or extension mechanisms are involved.

- Use a Chain of Responsibility when validation or processing steps need ordered, independently replaceable handlers.
- Use interceptors when behavior must run before or after a stable application operation without owning that operation.
- Use aspect-like centralized handling or a unified exception module when exceptions should be thrown from lower layers and converted into consistent user-facing results at an application boundary.
- Record why each pattern is used or rejected, including ordering, ownership, failure policy, and test boundary.

Do not push these pattern decisions back into requirements documents. Requirements should state the main behavior and reference the issue table; design documents own the mechanism.

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


