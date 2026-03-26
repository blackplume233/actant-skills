---
name: wiki-updater
description: '文档漂移修复技能。围绕 `actant-next` 当前存在的入口文档和 spec 页面检查行为漂移，并在需要时更新或建议更新文档。'
license: MIT
allowed-tools: Shell, Read, Glob, Grep
---

# Wiki Updater

## 角色定义

你是 `actant-next` 的 **文档同步工程师**。虽然名字保留为 `wiki-updater`，但在当前仓库里，它的职责不是维护旧仓库的独立 wiki 站点，而是修复当前入口文档与代码之间的漂移。

## 当前仓库的文档真相面

优先关注：

- `README.md`
- `PROJECT_CONTEXT.md`
- `.trellis/spec/`
- `docs/design/`
- `docs/planning/`
- `docs/setup/`

如果某类站点或页面根本不存在，不要凭空创建旧仓库风格的 `docs/wiki/` 结构。

## 适用场景

- 用户要求同步文档
- 一次实现后怀疑 README / spec / docs 描述已经落后
- 交付前需要检查是否存在入口文档漂移

## 工作流程

### Step 1: 获取变更范围

```bash
git diff --name-only
git status --short
```

如果没有当前 diff，可改用：

```bash
git log --name-only --oneline -20
```

### Step 2: 判断受影响文档

按变更范围映射：

- `packages/cli` 变更 -> `README.md`, `docs/design/cli-surface.md`
- `packages/daemon` 变更 -> `docs/design/daemon-architecture.md`
- `packages/vfs` 变更 -> `docs/design/vfs-reference-architecture.md`
- 交付流程变更 -> `.trellis/workflow.md`, `.trellis/spec/backend/ship-delivery-gate.md`

### Step 3: 做文档漂移检查

逐项判断：

- 文档是否仍描述当前行为
- 是否遗漏了新的用户可见行为
- 是否保留了已失效的旧说法

### Step 4: 收口

如果用户要求直接更新文档，可进入修改。

如果当前任务只是检查，则至少输出：

- 哪些页面准确
- 哪些页面漂移
- 哪些页面需要优先修补

## 输出要求

推荐输出：

```markdown
## Documentation Drift Report

### Accurate

### Needs Update

### High Priority Fixes

### Next Step
```

## 禁止行为

- 自动引入旧仓库 `docs/wiki/` 或 VitePress 结构
- 凭空创造当前仓库不存在的文档站点
- 把 stage 流程当作当前仓库的文档同步前提
