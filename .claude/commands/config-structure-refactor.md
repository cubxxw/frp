---
name: config-structure-refactor
description: Workflow command scaffold for config-structure-refactor in frp.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /config-structure-refactor

Use this workflow when working on **config-structure-refactor** in `frp`.

## Goal

Refactor or migrate configuration files and related code to a new structure or version.

## Common Files

- `pkg/config/`
- `models/config/`
- `client/`
- `server/`
- `cmd/`
- `test/e2e/legacy/`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Move or rename config files (e.g., from models/config/ to pkg/config/).
- Update related code to use new config structure (client/, server/, cmd/, etc.).
- Update or add new test files for config (pkg/config/*_test.go, test/e2e/legacy/, test/e2e/v1/).
- Update documentation if needed.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.