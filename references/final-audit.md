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

## Experience Baseline

- Every graphical UI project has an approved low-fidelity visual prototype; a prose-only screen list is not accepted.
- Screen inventory, navigation, information hierarchy, primary flows, major actions, and material states trace to requirements through UX IDs.
- The user explicitly chose whether further prototype detail was needed after approving the overall direction.
- UI implementation plans reference the approved prototype baseline and include visual and interaction acceptance checks.
- A non-UI project has a recorded not-applicable decision rather than a silently skipped phase.
- Prototype approval was not treated as authorization to bypass downstream design and planning gates.

## Exceptions and Recovery

Before auditing individual paths, verify that the project defines a structured issue taxonomy and that every category has an owning receiver. Verify that severity determines continuation and logging behavior, while category determines the responsible handler. Concrete error-code numbers may remain deferred when no external contract requires them.

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

Also verify:

- Every issue-producing responsibility emits the shared structured issue contract.
- No domain responsibility assembles UI error text.
- `TIP`, `WARNING`, and `EXCEPTION` handling policies are explicit or approved equivalents exist.
- Technical causes and stack traces are retained for diagnostics but excluded from user-facing output.
- New errors cannot bypass the unified classification, routing, logging, and conversion flow.

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

## Version-Control Safety

- Ignore rules match the actual technology stack and do not hide legitimate source through unjustified broad patterns.
- Installed dependencies, disposable build/test outputs, coverage, caches, logs, temporary files, local environment overrides, credentials, and secrets remain untracked.
- Lockfiles, migrations, generated source, fixtures, vendored content, and deployment artifacts have explicit inclusion decisions rather than blanket treatment.
- Sanitized configuration examples contain no working credentials.
- Plans require intentional path staging plus status, ignore-rule, staged-diff, and secret checks before commit.
- Already tracked outputs or exposed secrets have an explicit remediation plan; adding an ignore rule alone is not accepted as remediation.

## Final Decision

Do not approve implementation when:
- A material business decision remains hidden or unresolved.
- A requirement is not testable.
- A responsibility has ambiguous ownership.
- A lifecycle has undefined failure or terminal behavior.
- A technology choice lacks a quantified reason.
- A plan cannot identify concrete completion evidence.
