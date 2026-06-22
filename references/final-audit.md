# Final Safety-Net Audit

Run this audit after the detailed plans are written and before final approval.

## Whole

- Project objective, users, scope, and primary flow remain consistent.
- Delivery stages still match approved priorities.
- Domain and technical architecture support the same business outcome.
- The roadmap has one clear dependency order.

## Parts

- Every complex capability has a requirements document.
- Every complex context and responsibility has an independent design.
- Every complex responsibility has an independent implementation plan.
- Simple items are concise and not hiding complexity in overview files.

## Cross-Boundary Flows

- End-to-end flows crossing contexts are documented.
- Contracts, ownership, and failure behavior are clear at every boundary.
- Data translation and anti-corruption needs are handled.
- Transactions, eventual consistency, and compensation are explicit.

## Exceptions and Recovery

- Validation failure
- Partial success
- Duplicate input
- Timeout
- Cancellation
- Retry exhaustion
- Dependency outage
- Corrupt or incompatible data
- Degraded mode
- Rollback or compensation
- Restart and recovery

Mark each item applicable, handled, or explicitly out of scope.

## Extension Safety

- Plugins have compatibility and isolation rules.
- Interceptor ordering and short-circuit rules are defined.
- Listener delivery, retry, and duplicate behavior are defined.
- Factories protect real construction rules.
- No pattern owns hidden business policy outside its proper layer.

## Traceability

Verify:

```text
REQ -> CTX -> RESP -> ADR -> PLAN -> TEST
```

List and resolve:
- Orphan requirements
- Orphan plans
- Missing acceptance tests
- Stale downstream documents
- Unapproved dependencies

## Final Decision

Do not approve implementation when:
- A material business decision remains hidden or unresolved.
- A requirement is not testable.
- A responsibility has ambiguous ownership.
- A lifecycle has undefined failure or terminal behavior.
- A technology choice lacks a quantified reason.
- A plan cannot identify concrete completion evidence.
