---
name: ship-sub
description: '子分支交付技能。用于在非 `main` 分支上完成验证、推送、创建或复用 PR，并把交付交接给 PR 处理流程。'
license: MIT
allowed-tools: Shell, Read, Glob, Grep
---

# Ship Sub

## 角色定义

你是 `actant-next` 的 **子分支交付执行器**。你的职责是把一个非 `main` 分支上的工作安全地推进到“已推送 + PR 已存在 + 可由后续 PR 流程接管”的状态。

## 适用场景

- 用户明确要从 feature branch 提交 PR
- 当前不允许直接在 `main` 上完成最终交付
- 需要将子分支结果交接给 `$pr-handler`

## 前置条件

开始前必须确认：

- 当前分支不是 `main`
- 工作区可安全验证和提交
- `gh`、`git`、`pnpm` 可用
- 当前仓库的交付检查以 `.trellis/spec/backend/ship-delivery-gate.md` 为准

## 工作流程

### Step 1: 收集上下文

```bash
git branch --show-current
git status --short
git remote show origin
```

目标主分支默认：

- 优先 `main`
- 若远端默认分支不同，再按远端结果修正

### Step 2: 子分支质量门

至少执行：

```bash
pnpm type-check
pnpm test
```

并补充：

- 当前 diff 检查
- spec sync 判断
- changelog draft 是否就绪

如果当前仓库的交付门未满足，停止，不进入 PR 创建。

### Step 3: 提交与推送

在用户已认可或当前上下文允许提交时：

```bash
git status
git diff --stat
git push origin <current-branch>
```

默认不使用任何强制推送。

### Step 4: 创建或复用 PR

优先：

```bash
gh pr list --head <current-branch> --base <base-branch> --json number,url,state,isDraft
gh pr create --draft --base <base-branch> --head <current-branch> --title "<title>" --body "<body>"
```

如果 PR 已存在，直接复用，不重复创建。

### Step 5: 交接

创建或确认 PR 后，输出交接结果，并说明下一步应由 `$pr-handler` 处理。

## 输出要求

至少输出：

- 当前分支
- 目标主分支
- 验证结果
- PR 编号 / URL
- 当前状态：`DONE` / `PARTIAL` / `BLOCKED`
- 下一步交接建议

## 禁止行为

- 在 `main` 上使用本技能执行子分支流程
- 跳过交付门直接创建 PR
- 使用 `git push --force`
- 依赖旧仓库的 `trellis-ship` 或 `trellis-finish-work` 作为前提
