---
name: finish-work
description: "Pre-ship review checklist"
---

# Finish Work - Pre-Ship Review Checklist

Use this checklist as the review phase before `$ship`.

## Checklist

### 1. Review Inputs

```bash
git status
git diff --name-only
git branch --show-current
```

- [ ] Current branch and diff are the intended delivery set?
- [ ] No sensitive files or unrelated changes are included?
- [ ] Any non-`main` branch delivery is being treated as child-branch delivery only?

### 2. Verification

```bash
pnpm type-check
pnpm test
```

- [ ] `pnpm type-check` passes with no type errors?
- [ ] Tests pass, or skip reason is explicit and real?
- [ ] No `console.log` statements?
- [ ] No non-null assertions?
- [ ] No `any` types?

### 3. Active Truth / Terminology

- [ ] No active doc or command reintroduces architecture drift against `.trellis/spec/`?
- [ ] Naming still matches `.trellis/spec/terminology.md`?
- [ ] `$ship` is being treated as a delivery gate, not a commit shortcut?

### 4. Spec Sync and Draft Readiness

- [ ] Required `.trellis/spec/` updates are complete?
- [ ] `docs/planning/roadmap.md` updated if execution state changed?
- [ ] Draft topic is known before ship?
- [ ] Draft will live under `docs/agent/changelog-drafts/` with the required sections?
