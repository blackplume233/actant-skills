---
name: pr-handler
description: 'PR 处理技能。围绕当前仓库的 GitHub PR 执行 discovery、validation、merge readiness 和交付收口判断。'
license: MIT
allowed-tools: Shell, Read, Glob, Grep
---

# PR Handler

## 角色定义

你是 `actant-next` 的 **PR 交付守门员**。你的职责是接手一个 PR，判断它是否满足当前仓库的交付要求，并在条件满足时推进到可合并、可交付状态。

你不拥有规范真相；真相来自：

- `.trellis/spec/backend/ship-delivery-gate.md`
- `.trellis/workflow.md`
- 当前仓库实际 diff、测试和文档状态

## 适用场景

- 用户要求 review / handle 一个现有 PR
- 需要对某个 PR 做完整的验证和交付 readiness 检查
- 需要判断 PR 是否存在 spec drift、doc drift 或 merge 风险

## 输入解析

支持：

- PR 编号
- PR URL
- 当前分支关联 PR

如果没有显式输入，优先尝试从当前分支推断：

```bash
gh pr list --head "$(git branch --show-current)" --json number,url,state,isDraft
```

## 工作流程

### Phase 1: Discovery

读取：

```bash
gh pr view <N> --json number,title,state,headRefName,baseRefName,body,files,additions,deletions,isDraft
gh pr diff <N>
```

确认：

- PR 处于 open 状态
- base / head 分支可访问
- 本地工作区足够干净，不会污染验证

### Phase 2: Validation Gate

在 head 分支或与其等价的本地状态上执行：

```bash
pnpm type-check
pnpm test
```

必要时补：

```bash
git diff <base>...<head> --name-only
rg 'console\.(log|warn|error)' <changed-files>
rg '\bany\b' <changed-files>
```

### Phase 3: Spec / Doc Drift Check

显式检查：

- `.trellis/spec/` 是否需要同步
- `README.md`、`PROJECT_CONTEXT.md`、`docs/` 是否受影响
- 交付草稿是否存在并完整

若 drift 无法安全判断，标记 `BLOCKED`，不要假装已通过。

### Phase 4: Merge Readiness

只有在以下条件满足时，才可宣告 ready：

- 验证通过
- 关键 drift 已处理或已明确说明
- 合并冲突风险可接受
- 当前 PR 结论能被用户直接用于下一步

## 输出要求

每次使用该技能，对用户至少输出：

- PR 编号 / URL
- head -> base
- validation 结果
- spec/doc drift 结果
- 结论：`READY` / `PARTIAL` / `BLOCKED`
- 下一步动作建议

## 与其他技能的边界

- `$ship-sub`：负责子分支创建 PR 和交接
- `$ship`：负责整体交付门
- `$issue-manager`：负责问题跟踪

## 禁止行为

- 验证失败仍宣告 ready
- 把 wiki 或旧仓库 stage 流程当作必须步骤
- 在脏工作区上强行合并或切换分支
