# Experience and Prototyping Phase

Validate the user-facing direction visually before domain, architecture, or frontend implementation decisions harden around an untested layout.

## Applicability

This phase is required for Web, mobile, desktop, kiosk, embedded-display, and other graphical UI applications. Record a not-applicable decision for headless services, libraries, command-line tools, and background workers; do not silently skip the phase.

## Low Fidelity First

Create low-fidelity visual prototypes covering:

- screen or page inventory and navigation;
- information hierarchy and primary content regions;
- primary user flows and decisive outputs;
- major actions and transitions;
- empty, loading, error, permission-denied, and completion states when material;
- responsive structure where different viewport classes change the flow.

Keep color, typography, branding, animation polish, component libraries, and frontend-framework decisions out unless they are themselves requirements. A prose description, route list, or component tree does not replace the visual prototype.

Store the overview and artifact links under `docs/project/experience/`. Assign `UX-<AREA>-NNN` IDs and map primary screens and flows to requirement IDs.

## Progressive Detail Decision

After the user approves the overall direction, ask explicitly whether more detail is needed.

Refine only when uncertainty or risk remains, such as:

- a complex multi-step or branching flow;
- dense data presentation or editing;
- important responsive behavior;
- permissions or role-dependent UI;
- destructive, recovery, partial-success, or unusual error interactions;
- accessibility behavior that cannot be validated from the low-fidelity artifact.

If no refinement is needed, record that decision and treat the low-fidelity prototype as the approved baseline. High fidelity is optional, not an automatic next step.

## Approval Check

Before approval verify:

- every primary requirement flow reaches a screen and decisive output;
- navigation and ownership of major actions are unambiguous;
- material states and role differences are visible;
- open questions and deliberately deferred visual details are recorded;
- artifact paths or links are stable and reviewable;
- downstream plans can reference the approved UX IDs.

Prototype approval completes only this phase. Frontend development starts only after the remaining domain, lifecycle, architecture, and implementation-plan gates are approved.
