---
name: record-session
description: "Record work progress after human has tested and committed code"
---

[!] This skill should only be used AFTER the human has tested and committed the code.

If this was ship / merge level delivery, record the related changelog draft path and verification summary.

## Record Work Progress

### Step 1: Get Context & Check Tasks

```bash
python3 ./.trellis/scripts/get_context.py --mode record
python3 ./.trellis/scripts/task.py list
```

### Step 2: Add Session

```bash
python3 ./.trellis/scripts/add_session.py \
  --title "Session Title" \
  --commit "hash1,hash2" \
  --summary "Brief summary of what was done"
```

### Required Delivery Facts for Ship / Merge Work

Record these in the session content:

- changelog draft path under `docs/agent/changelog-drafts/`
- shipped commit hash
- verification results or explicit skip reasons
- whether the ship happened on `main` or a child branch
