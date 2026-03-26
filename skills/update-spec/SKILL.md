---
name: update-spec
description: "Update binding code-spec documents before ship"
---

# Update Code-Spec

Update `.trellis/spec/` when the change affects binding contracts.

For infra or cross-layer work, this is a required pre-ship step.

## Mandatory Triggers

Run this before ship when the diff includes any of:

- new or changed CLI command signature
- daemon status or lifecycle contract change
- VFS operation surface change
- plugin/daemon boundary change
- shared contract or error-code change
- delivery gate, changelog draft contract, or ship semantics change

## Required Output

For triggered tasks, the updated spec must include:

1. scope / trigger
2. signatures
3. contracts
4. validation & error matrix
5. good / base / bad cases
6. tests required
7. wrong vs correct

## Pre-Ship Rule

If the diff touches a mandatory trigger, do not allow `$ship` to proceed until the relevant `.trellis/spec/` files are updated in the same delivery set.
