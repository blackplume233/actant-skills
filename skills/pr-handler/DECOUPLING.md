# PR Handler Decoupling Checklist

## Old Path Dependencies

- Legacy wiki paths
- Old issue and task conventions
- Old command references under `.cursor/commands/trellis-*`

## Old Workflow Dependencies

- Assumes a legacy PR validation pipeline with spec update inside the handler
- Assumes doc sync to old wiki surface

## Old Platform Dependencies

- GitHub Draft PR semantics mixed with legacy repo automation
- Old issue synchronization expectations

## Current Repo Replacement Truth

- `.trellis/spec/backend/ship-delivery-gate.md`
- `.trellis/workflow.md`
- current `ship` and `record-session` skills
- current `gh`, `git`, `pnpm`, and local branch policy

## Rewrite Goal

Keep only the PR validation / merge handoff skeleton that fits `actant-next` delivery gates. Remove wiki coupling, legacy issue coupling, and any assumptions that the handler owns spec truth.
