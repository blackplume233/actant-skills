---
name: ship
description: "Blocking delivery gate for spec sync, changelog draft readiness or auto-creation, verification, commit, and push"
---

# Ship - Delivery Gate

Use this skill only when work is ready to deliver.

`ship` is a blocking delivery gate, not a commit shortcut.

## Read Before Shipping

1. `.trellis/spec/index.md`
2. `.trellis/spec/terminology.md`
3. `.trellis/spec/backend/index.md`
4. `.trellis/spec/backend/ship-delivery-gate.md`
5. `.trellis/workflow.md`

## Phase 1: Blocking Review

- run active truth / terminology review
- run spec-sync review against changed files
- validate changelog draft readiness; if missing, auto-create it before continuing
- run verification and pattern scans

If any blocking item fails, stop before commit.

## Phase 2: Commit and Push

```bash
git status
git diff --stat
git add -A
git commit -m "<type>: <description>"
git push origin <current-branch>
```

Rules:
- use English commit messages
- use Conventional Commits
- do not commit secrets
- do not use `--no-verify`
- non-`main` branch ship is child-branch delivery only

## Phase 3: Record

After ship, use `$record-session` to persist:
- commit hash
- verification summary
- related changelog draft path
