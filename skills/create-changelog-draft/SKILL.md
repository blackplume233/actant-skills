---
name: create-changelog-draft
description: "Create a changelog draft manually, or let ship auto-create one when missing"
---

# Create Changelog Draft

Create a changelog draft manually, or let `ship` auto-create one when missing.

## Usage

```bash
python3 ./.trellis/scripts/create_changelog_draft.py --topic <topic> --title "<Title>"
python3 ./.trellis/scripts/create_changelog_draft.py --auto
```

## Contract

- output directory: `docs/agent/changelog-drafts/`
- filename: `YYYY-MM-DD-<agent>-<topic>.md`
- required sections:
  - `# <title>`
  - `## 变更摘要`
  - `## 用户可见影响`
  - `## 破坏性变更/迁移说明`
  - `## 验证结果`
  - `## 关联 PR / Commit / Issue`

Drafts preserve delivery facts. They do not replace `.trellis/spec/`.
