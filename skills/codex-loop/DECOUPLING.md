# Codex Loop Decoupling Checklist

## Old Path Dependencies

- `.trellis/scripts/multi-agent/codex-loop*.sh`
- task directory conventions and embedded loop logs
- `.trellis/worktree.yaml`

## Old Workflow Dependencies

- Assumes loop execution and verification are script-owned
- Assumes automatic per-round session recording behavior

## Old Platform Dependencies

- Requires `codex` CLI availability
- Requires worktree isolation and a compatible verify gate

## Current Repo Replacement Truth

- `.trellis/scripts/multi_agent/`
- `.trellis/workflow.md`
- current task scripts and any future worktree policy

## Rewrite Goal

Preserve the multi-round convergence model only if `actant-next` keeps a compatible worktree and verification story. Do not import shell entrypoints until that compatibility is proven.
