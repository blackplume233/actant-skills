# QA Engineer Scenarios

This directory stores reusable QA scenarios for `qa-engineer`.

Guidelines:

- Keep scenarios repository-specific and executable from the repo root.
- Prefer current verification paths such as `pnpm test`, `pnpm type-check`, or small shell commands.
- Do not assume a packaged `actant` binary exists unless the repository actually exposes one.
- Use `expect` as natural-language acceptance criteria, not brittle string snapshots.

Recommended file shape:

```json
{
  "name": "status-smoke",
  "description": "Verify daemon start and status output through the current Phase 1 surface.",
  "tags": ["cli", "smoke"],
  "preflight": ["pnpm type-check"],
  "steps": [
    {
      "id": "cli-tests",
      "kind": "test",
      "command": "pnpm test",
      "expect": "CLI and daemon smoke coverage passes without new regressions."
    }
  ]
}
```
