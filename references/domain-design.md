# Domain Design Phase

## Decide DDD Depth

Classify the project:

- **Full DDD**: rich business rules, multiple subdomains, changing policies, significant consistency boundaries.
- **Light DDD**: clear business capabilities and rules but limited complexity.
- **Minimal domain modeling**: CRUD or technical utility with little domain behavior.

Record the decision and reason. Even minimal modeling requires clear business terminology and ownership boundaries.

## Whole First

Create an overall business map:
- Core domain
- Supporting domains
- Generic domains
- Actors
- Primary business flows
- External systems
- Data and decision ownership

Then identify bounded contexts and their relationships.

## Bounded Context Design

For each complex context document, define:
- Context ID and purpose
- Ubiquitous language
- Owned capabilities
- Owned data
- Inputs and outputs
- Aggregates and consistency boundaries
- Entities and value objects
- Domain services
- Domain events
- Policies and invariants
- Context contracts
- Upstream/downstream relationships
- Failure and compensation behavior
- Requirements covered
- Explicit exclusions

Do not equate a bounded context with a database schema, deployment unit, screen, or folder.

## Aggregate Guidance

Use an aggregate when a group of objects must preserve business invariants transactionally.

Check:
- A clear aggregate root controls changes.
- The boundary is as small as consistency allows.
- Other aggregates are referenced by identity.
- Cross-aggregate workflows use application coordination or domain events.

Avoid table-shaped anemic models when behavior and invariants belong in the domain.

## Domain Events

Use a domain event for a meaningful completed business fact that other responsibilities may react to.

Define:
- Event name in past tense
- Producer
- Business meaning
- Payload
- Ordering expectations
- Delivery/retry expectations
- Consumers

Do not use events merely to avoid a direct function call inside one simple responsibility.

## Safety-Net Audit

- Every requirement maps to at least one context.
- No capability has ambiguous ownership.
- Cross-context contracts use explicit language and models.
- Domain rules are not assigned to UI or infrastructure.
- Context boundaries match change and consistency boundaries.
- Shared kernels are rare and justified.
- Failure, compensation, and eventual consistency are explicit.
