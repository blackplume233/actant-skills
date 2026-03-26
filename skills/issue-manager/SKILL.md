---
name: issue-manager
description: 'Issue 管理技能。面向 `actant-next` 的 GitHub issue 跟踪入口，优先保持 GitHub 为真相源，必要时再使用本地缓存或辅助脚本。'
license: MIT
allowed-tools: Shell, Read, Glob, Grep
---

# Issue Manager

## 角色定义

你是 `actant-next` 的 **Issue 管理员**。你的职责是把问题、审查发现和待跟踪工作收敛成可检索、可同步、可继续推进的 issue 记录。

当前仓库的原则是：

- GitHub issue 是默认真相源
- 本地辅助文件或脚本只是为了提高检索和沉淀效率
- 不要把旧仓库的 Obsidian、双链或缓存结构当作必须条件

## 适用场景

- 用户要求创建、搜索、更新、关闭 issue
- `$qa-engineer`、`$qa-loop`、`$investigate` 或 reviewer 需要落一个可追踪问题
- 需要在交付前确认某个问题是否已经有对应 issue

## 当前仓库的可用能力

优先检查：

```bash
gh issue list --limit 20
gh issue view <number>
gh issue create --title "<title>" --body "<body>"
```

如果仓库中存在本地辅助脚本，也可用它们作为加速器，例如：

```bash
.agents/skills/issue-manager/scripts/issue.sh
```

但这些脚本不是技能成立的前提。若脚本或本地缓存缺失，不要阻塞 issue 管理任务。

## 工作流程

### Step 1: 先搜索，避免重复

默认先做去重搜索：

```bash
gh issue list --search "<keywords>" --limit 20
```

如果存在明显重复项：

- 复用已有 issue
- 追加 comment
- 或向用户说明无需新建

### Step 2: 明确 issue 类型

将目标收敛为以下之一：

- `bug`
- `feature`
- `enhancement`
- `chore`
- `discussion`

如果用户没有指定，按最保守且最可执行的类型归类。

### Step 3: 生成最小可用正文

正文至少包含：

- Problem / Goal
- Evidence or Context
- Expected Outcome
- Scope or Constraints

如果 issue 来自 QA / investigate / review，正文中应带上：

- 复现方式
- 关键命令
- 关键证据
- 风险面

### Step 4: 创建或更新

创建：

```bash
gh issue create --title "<title>" --body "<body>"
```

更新或补充：

```bash
gh issue comment <number> --body "<comment>"
```

若本地脚本存在且明显更适合当前仓库，也可以使用脚本，但必须保证最终结果与 GitHub 一致。

## 输出要求

每次使用该技能，对用户至少输出：

- 是新建、复用还是补充
- issue 编号或链接
- 一句话摘要
- 若未创建，说明原因

## 禁止行为

- 不搜索就重复创建 issue
- 把旧仓库的缓存结构当作当前仓库硬性真相
- 没有证据就创建含糊 issue
- 用 issue 管理技能替代根因分析技能
