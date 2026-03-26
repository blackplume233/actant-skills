---
name: start
description: "Start Session"
---

# Start Session

Initialize your AI development session and begin working on tasks.

If the upcoming work is intended for delivery, plan the changelog draft early. Do not leave draft creation to the very end.

## Initialization

### Step 1: Understand Workflow

```bash
cat .trellis/workflow.md
cat .trellis/spec/index.md
cat .trellis/spec/terminology.md
cat .trellis/spec/backend/index.md
```

If the work is likely to ship, also read:

```bash
cat .trellis/spec/backend/ship-delivery-gate.md
```

### Step 2: Get Current Context

```bash
python3 ./.trellis/scripts/get_context.py
python3 ./.trellis/scripts/task.py list
git status
```

### Step 3: Report and Ask

Report:
- developer identity
- current branch
- uncommitted state
- active tasks
- whether the work appears to be heading to ship / merge delivery

If the user already knows this work is heading to ship / merge delivery, remind them that a changelog draft will be required before ship.

## Working Rule

- Read spec before changing implementation
- If work changes contracts, update spec before ship
- Use `$finish-work` before `$ship`
- Create changelog draft before `$ship`
- Use `$record-session` after tested and committed work
