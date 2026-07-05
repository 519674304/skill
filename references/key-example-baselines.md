# Key Example Baselines

Start from the decisive business output and work backward to the minimum input that produces it. Treat these examples as cross-phase alignment contracts.

## Required Files

Create under `docs/project/baselines/`:

- One machine-readable primary-flow input example.
- One machine-readable expected output example.
- `README.md` describing the input-to-output mapping and the business meaning of stable IDs.

Use domain formats chosen by the project, such as TOML for editable business rules and JSON for generated analysis results. Do not prescribe storage schemas, classes, APIs, UI coordinates, or framework details in these files.

## Review Rules

- Cover the complete sunny-day primary flow before adding edge cases.
- Use stable IDs so input definitions can be traced to output facts.
- Every decisive output field must be supported by an input rule, source fact, or documented derivation.
- UI consumes the output contract; UI styling must not leak into the business output.
- Domain, responsibility, architecture, and planning documents must cite affected baseline IDs.
- When prose and an approved baseline disagree, stop and resolve the contradiction explicitly.
- Keep validation, malformed input, and rare exceptions in separate examples only after the primary baseline is approved.

## Approval Gate

Do not approve Phase 1 until the user confirms that the primary input example can express the business flow and that the expected output contains the information needed by the final user experience.
