# Ship Sub Decoupling Checklist

## Old Path Dependencies

- References to legacy `trellis-ship` and `trellis-finish-work`
- Legacy task metadata fields and PR creation helpers

## Old Workflow Dependencies

- Assumes a full two-stage child-branch delivery flow already exists
- Assumes spec checks mirror old ship command behavior

## Old Platform Dependencies

- Strong `gh` PR flow assumptions
- Legacy branch naming and delivery semantics

## Current Repo Replacement Truth

- `.trellis/spec/backend/ship-delivery-gate.md`
- `.trellis/workflow.md`
- current branch policy on `main`
- any future `pr-handler` rewrite

## Rewrite Goal

Retain only the child-branch delivery concept. Rebuild the exact checks, branch semantics, and PR handoff around `actant-next` rather than importing old ship shell behavior.
