---
name: release-version-bump
description: Workflow command scaffold for release-version-bump in frp.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /release-version-bump

Use this workflow when working on **release-version-bump** in `frp`.

## Goal

Bump the project version and release a new version, including changelog, documentation, and code updates.

## Common Files

- `pkg/util/version/version.go`
- `README.md`
- `README_zh.md`
- `Release.md`
- `go.mod`
- `go.sum`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Update version in pkg/util/version/version.go (or utils/version/version.go in older structure).
- Update README.md and README_zh.md with new version if needed.
- Update Release.md.
- Update go.mod and go.sum.
- Update Makefile or Makefile.cross-compiles if needed.

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.