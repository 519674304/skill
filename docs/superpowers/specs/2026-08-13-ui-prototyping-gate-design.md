# UI Prototyping Gate Design

Status: Draft

## Objective

Extend `project-inception` so Web applications and other applications with a user interface cannot proceed toward frontend implementation before their experience direction has been validated visually.

## Workflow change

Add a mandatory **Experience and Prototyping** phase after Requirements and before Domain and Business Decomposition.

The phase applies when the project includes a Web UI, desktop UI, mobile UI, or another user-facing graphical interface. Headless services, libraries, command-line tools, and background workers may explicitly record the phase as not applicable.

## Progressive fidelity

1. Start with low-fidelity prototypes. Cover navigation, page or screen inventory, information hierarchy, primary user flows, major actions, and essential states without choosing a frontend framework or polishing visual style.
2. Ask the user to approve the overall experience direction.
3. After the direction is approved, ask explicitly whether further prototype detail is needed.
4. If needed, refine only the uncertain or high-risk flows, states, responsive layouts, or interaction details, then request approval again.
5. If not needed, record the low-fidelity prototype as the approved UI baseline and finish the phase.

## Gate semantics

- A text-only description is not a substitute for the initial low-fidelity prototype when the phase applies.
- Prototype approval does not authorize coding by itself. The remaining domain, lifecycle, architecture, and implementation-planning gates still apply.
- Frontend development may begin only after the final implementation plan is approved.
- Approved prototypes become governed baselines. Upstream requirement changes or later prototype changes mark affected downstream documents stale.

## Required artifacts and traceability

Store prototype records under `docs/project/experience/`:

- `00-experience-overview.md`: users, screen inventory, navigation model, primary flows, fidelity decision, approval state, and links to visual artifacts.
- Low-fidelity prototype files or links using the most suitable repository-supported format.
- Optional refined prototypes for flows that require additional detail.

Assign stable `UX-<AREA>-NNN` IDs and trace primary screens and flows to requirements. Implementation plans for UI work must reference the approved UX IDs and prototype baseline.

## Reference and audit updates

Add a focused prototyping reference covering applicability, low-fidelity content, refinement criteria, approval checks, and common omissions. Update the document structure, final audit, implementation-planning guidance, main skill workflow, and README summary so the new phase cannot be skipped accidentally.

## Verification scenarios

Test the skill against pressure cases where an agent is asked to:

- start React implementation immediately because requirements are clear;
- replace a low-fidelity prototype with a prose screen list to save time;
- assume high-fidelity work is mandatory after low-fidelity approval;
- begin frontend coding immediately after prototype approval;
- skip the phase for a genuinely headless application without recording why.

Expected behavior: require low fidelity for applicable UI projects, allow explicit early completion after direction approval, preserve all downstream approval gates, and record a reasoned not-applicable decision for headless projects.
