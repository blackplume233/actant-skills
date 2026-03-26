# Issue Manager Decoupling Checklist

## Old Path Dependencies

- Local cache and archive structure under `.trellis/issues/`
- Obsidian-specific wikilink expectations

## Old Workflow Dependencies

- GitHub-first dirty-sync workflow embedded into commit / ship expectations
- Tight coupling to review and QA issue creation flows

## Old Platform Dependencies

- `gh` CLI as synchronization backbone
- Legacy label, milestone, and cache conventions

## Current Repo Replacement Truth

- actual GitHub repository configuration derived from `origin`
- current `.trellis/` usage patterns
- current delivery flow in `.trellis/workflow.md`

## Rewrite Goal

Decide whether `actant-next` really wants a local issue cache at all. If retained, rebuild around minimal GitHub sync and current repo metadata rather than importing Obsidian-oriented behavior by default.
