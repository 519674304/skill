# Requirements Phase

## Whole First

Confirm these project-level decisions before decomposing features:

1. Problem and desired business outcome
2. Target users and stakeholders
3. Primary end-to-end scenarios
4. In-scope and out-of-scope boundaries
5. Delivery stages and MVP boundary
6. Success metrics
7. Workload, latency, resource, deployment, security, and compliance constraints
8. Business terminology

Use brainstorming one question at a time. Prefer a concrete choice when ambiguity would affect downstream design.

## Requirements Documents

### Overview

Include:
- Purpose
- Users and stakeholders
- Business context
- Primary scenarios
- Capability map
- Delivery stages
- Success criteria
- Glossary

### Scope and Constraints

Include:
- Included and excluded scope
- Assumptions
- External dependencies
- Data constraints
- Performance and capacity
- Reliability
- Security and compliance
- Deployment and operations

### Complex Capability

For every complex capability document, include:
- Requirement IDs
- User or actor
- Goal and value
- Preconditions
- Trigger
- Main flow
- Alternative flows
- Exception flows
- Business rules
- Inputs and outputs
- State changes
- Data ownership and retention
- Performance requirements
- Acceptance criteria
- Dependencies
- Explicit exclusions

## Requirement Quality

Write measurable statements. Replace words such as "fast", "friendly", "support", or "optimized" with testable behavior and conditions.

Specify performance with:
- Data size
- Hardware or environment
- Warm/cold state
- Percentile
- Measurement boundary
- Allowed degradation

Keep implementation choices out unless they are externally imposed constraints.

## Safety-Net Audit

Check:
- Every capability belongs to a delivery stage.
- Every main flow has exceptions and recovery.
- Cross-capability flows are explicit.
- Import/export, cancellation, retry, timeout, partial success, and duplicate handling are considered where relevant.
- Data lifecycle and deletion are covered.
- Accessibility, audit, security, and operability are considered proportionally.
- No requirement contradicts scope or another requirement.
- Every requirement has acceptance criteria.
- Open decisions are visible and do not masquerade as assumptions.
