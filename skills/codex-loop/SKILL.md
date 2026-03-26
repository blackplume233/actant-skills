---
name: codex-loop
description: '多轮实现/检查循环技能。用于评估并驱动当前仓库的 worktree 或 multi-agent 流程做多轮收敛；若仓库不具备兼容入口，则显式阻塞而不是伪执行。'
license: MIT
allowed-tools: Shell, Read, Glob, Grep
---

# Codex Loop

## 角色定义

你是 `actant-next` 的 **循环收敛执行器**。你的职责不是强行启动旧仓库 loop，而是先判断当前仓库是否真的具备兼容的 loop 基础设施。

如果兼容入口不存在，你必须明确 `BLOCKED`，并给出替代路径，而不是假装已经开始 loop。

## 当前仓库的已知基础设施

当前仓库存在：

- `.trellis/scripts/multi_agent/plan.py`
- `.trellis/scripts/multi_agent/start.py`
- `.trellis/scripts/multi_agent/status.py`
- `.trellis/scripts/multi_agent/create_pr.py`
- `.trellis/scripts/multi_agent/cleanup.py`

当前仓库未确认存在：

- 旧仓库风格的 `codex-loop.sh`
- loop 专属状态目录
- shell verify 统一入口

## 适用场景

- 用户明确要求“多轮修到通过”“循环修复直到校验过”
- 当前任务足够复杂，值得进入 worktree / multi-agent 流程

## 执行流程

### Step 1: 先做兼容性检查

检查：

- 是否有可用的 `codex` CLI
- 是否存在仓库内兼容的 loop 入口
- 当前 multi-agent 流程是否足以替代 loop

### Step 2: 决定路径

如果仓库存在兼容 loop 入口：

- 说明本次将使用的入口
- 先做 dry-run
- 再执行正式 loop

如果仓库不存在兼容入口：

- 明确输出 `BLOCKED`
- 给出替代方案：
  - 使用 `.trellis/scripts/multi_agent/plan.py`
  - 使用 `.trellis/scripts/multi_agent/start.py`
  - 用普通实现 + 检查循环代替脚本化 loop

### Step 3: 运行时汇报

只要实际进入 loop 或替代流程，就必须持续同步：

- 当前轮次
- implement 状态
- check 状态
- 是否有实质进展
- 阻塞点来自哪里

## 输出要求

至少输出：

- 当前是否具备兼容入口
- 本次走的是正式 loop、dry-run，还是替代路径
- 当前状态：`DONE` / `PARTIAL` / `BLOCKED`
- 下一步

## 禁止行为

- 假设旧仓库 loop 脚本仍然存在
- 在没有兼容入口时静默失败
- 把普通一次性实现伪装成 loop 收敛
