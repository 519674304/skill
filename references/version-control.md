# Version-Control Boundary

Define what the project owns in Git before implementation creates dependencies, outputs, and local configuration.

## Inspect First

Review repository status, existing ignore rules, tracked generated files, local configuration, build and code-generation tooling, and secret exposure risk. Do not replace an established ignore file with a generic template without reviewing its intent.

## Default Classification

Normally keep these out of Git:

- installed dependency directories;
- build, package, coverage, and test-result outputs;
- caches, logs, temporary files, process IDs, and crash dumps;
- local IDE and operating-system metadata;
- local environment overrides and machine-specific configuration;
- credentials, private keys, tokens, certificates, and secrets.

Evaluate rather than automatically ignore:

- dependency lockfiles;
- database migrations and schemas;
- generated API clients, parsers, protocol bindings, or assets;
- fixtures, snapshots, vendored dependencies, and deployment manifests.

Track an evaluated artifact when the repository intentionally owns it and doing so is required for reproducible builds, review, offline use, release, or deployment. Record the generator, source, update command, and drift check when generated source is tracked.

## Ignore-Rule Design

Create the smallest technology-specific rule set that covers observed tools. Prefer anchored or directory-specific patterns when a broad pattern could hide legitimate source files. Keep sanitized examples such as `.env.example` trackable while ignoring local secret-bearing variants.

An ignore rule prevents future accidental additions; it does not remove an already tracked file and does not remediate an exposed secret.

## Staging and Commit Gate

Before staging or committing:

1. Inspect `git status --short`, including untracked files.
2. Verify representative excluded paths with `git check-ignore -v` when ignore behavior matters.
3. Stage reviewed paths explicitly. Do not use `git add .`, `git add -A`, or an equivalent repository-wide add while unreviewed files are present.
4. Inspect `git diff --cached --stat` and `git diff --cached`.
5. Search the staged set for secrets, local paths, large generated files, dependency trees, build outputs, caches, and logs.
6. Commit only when every staged path is intentional.

If a secret is tracked or staged, stop. Remove it through an explicit remediation workflow and rotate the credential when exposure is possible. Adding it to `.gitignore` afterward is insufficient.

## Approval Check

Record the ignore strategy, ambiguous generated or vendored artifact decisions, sanitized configuration examples, existing risks that need remediation, and the staging verification expected during implementation.
