# Document Structure

Use this default layout:

```text
docs/project/
  00-index.md
  requirements/
    00-overview.md
    01-scope-and-constraints.md
    <complex-capability>-requirements.md
  domain/
    00-domain-map.md
    <bounded-context>-design.md
  responsibilities/
    00-responsibility-map.md
    <complex-responsibility>-design.md
  architecture/
    00-lifecycle-and-extension-model.md
    01-technical-selection.md
    02-technical-architecture.md
  plans/
    00-roadmap.md
    <complex-responsibility>-plan.md
```

## Separation Rules

- `00-index.md`: navigation, current phase, approval state, document dependencies.
- `requirements/`: user and business needs, rules, constraints, acceptance. No framework or class design.
- `domain/`: business language, contexts, aggregates, rules, events, context relationships.
- `responsibilities/`: responsibility boundaries, contracts, dependencies, errors, extension points, test boundaries.
- `architecture/`: lifecycle, pattern decisions, technology selection, runtime architecture.
- `plans/`: implementation order and actionable work only.

Never combine requirements, domain design, architecture, and implementation tasks in one document.

## Adaptive Splitting

Keep an item in an overview when approximately 10-20 lines fully define it.

Create a separate document when an item has one or more of:
- Independent workflow or lifecycle
- Multiple states or transitions
- Nontrivial business rules
- Public contract or integration boundary
- Dedicated data model
- Multiple failure modes
- Security, performance, or migration risk
- Several implementation milestones

Overview documents reference detailed documents. They do not duplicate them.

## Metadata

Start every governed document with:

```text
Document ID:
Status: Draft
Approved by:
Approved at:
Depends on:
Supersedes:
```

## Index Content

The index should contain:
- Project objective
- Current phase
- Phase approval table
- Document catalog
- Dependency graph
- Open decisions
- Superseded documents
