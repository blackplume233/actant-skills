# Project Reviewer Decoupling Checklist

## Old Path Dependencies

- Old roadmap paths and issue cache layout
- Old quality guideline files that do not exist in `actant-next`

## Old Workflow Dependencies

- Review output hard-wired to old issue workflow
- Review criteria tied to old spec surfaces and historical architecture

## Old Platform Dependencies

- Implicit dependence on legacy package layout and roadmap taxonomy

## Current Repo Replacement Truth

- `README.md`
- `PROJECT_CONTEXT.md`
- `.trellis/spec/index.md`
- `.trellis/spec/backend/index.md`
- `.trellis/spec/backend/ship-delivery-gate.md`
- current `packages/*` layout and `__tests__/`

## Rewrite Goal

Turn this into a read-only reviewer for `actant-next` that audits current package structure, CLI-first behavior, spec-sync expectations, and test coverage without importing legacy roadmap or issue assumptions.
