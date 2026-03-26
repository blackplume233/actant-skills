# Wiki Updater Decoupling Checklist

## Old Path Dependencies

- `docs/wiki/`
- VitePress config and sidebar structure
- stage-generated wiki artifacts

## Old Workflow Dependencies

- Assumes stage / ship always ends with wiki synchronization
- Assumes changelog and architecture snapshots feed wiki pages

## Old Platform Dependencies

- Old documentation site architecture
- Legacy feature page taxonomy

## Current Repo Replacement Truth

- `README.md`
- `PROJECT_CONTEXT.md`
- `.trellis/spec/`
- `docs/` pages that actually exist in `actant-next`

## Rewrite Goal

Reframe this as a documentation drift checker for current repo entry docs and specs. Do not import wiki-site maintenance behavior unless `actant-next` actually introduces a dedicated docs site.
