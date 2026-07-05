# Lifecycle and Extension Design

## Lifecycle Before Patterns

For every long-lived business object or process, define:
- Creation
- Validation
- Activation/start
- Processing states
- Transitions and guards
- Completion
- Failure
- Cancellation
- Timeout
- Retry
- Recovery/compensation
- Expiration/archive/deletion

Document who initiates each transition, what invariant must hold, and what event or result follows.

## Pattern Decision Table

Use patterns only for demonstrated variation or policy:

| Need | Candidate | Required decision |
|---|---|---|
| Replaceable algorithm or policy | Strategy | What varies and at what runtime scope? |
| Multiple creation families | Factory | What construction invariant is protected? |
| Lifecycle notification | Domain event/listener | Is it a completed fact and are consumers independent? |
| Cross-cutting checks around calls | Interceptor/middleware | What boundary and ordering are required? |
| Optional third-party capability | Plugin | What stable extension contract and isolation exist? |
| Fixed workflow skeleton with variable steps | Template method/pipeline | Which steps are fixed and replaceable? |
| Behavior changes by state | State pattern | Are transitions meaningful domain behavior? |
| Deferred or queued work | Command/job | What idempotency, retry, and cancellation rules apply? |

For every candidate, record:
- Decision: adopt or reject
- Problem solved
- Simpler alternative
- Contract
- Execution timing
- Ordering
- Failure policy
- Isolation boundary
- Observability
- Test strategy

## Plugin Design

Use a plugin only when independently added or replaced capabilities are a real requirement.

Define:
- Plugin manifest and version compatibility
- Discovery and loading
- Capability contract
- Configuration
- Lifecycle hooks
- Isolation and resource limits
- Failure containment
- Unload/reload behavior

## Interceptor Design

Use interceptors for boundary-level cross-cutting behavior such as validation, authorization, tracing, metrics, or transaction scope.

Do not hide core business decisions in interceptors.

Define order, short-circuit behavior, error propagation, and whether execution is synchronous.

## Listener Design

Use listeners when a completed event may have independent consumers.

Define delivery semantics, duplicate handling, ordering, retry, poison-event handling, and transaction boundary.

## Safety-Net Audit

- Lifecycle has no unreachable or undefined state.
- Every failure state has an owner and recovery decision.
- Patterns correspond to real variation points.
- Extension contracts do not expose internal models unnecessarily.
- Plugin/listener failure cannot corrupt core invariants.
- Replacing UI, storage, or an algorithm does not rewrite domain rules.

