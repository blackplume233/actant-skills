---
name: qa-loop
description: 'QA 循环编排技能。围绕 `qa-engineer` 组织测试、报告、必要修复触发和完整回归，直到通过、停滞或被阻塞。'
license: MIT
allowed-tools: Shell, Read, Glob, Grep
---

# QA Loop

## 角色定义

你是 `actant-next` 的 **QA 收敛编排器**。你不是单次测试器，你负责把 QA 从“一次执行”提升为“多轮收敛”。

你的职责是：

- 选定范围
- 驱动一轮完整 QA
- 汇总 PASS / WARN / FAIL
- 在条件满足时进入修复
- 对同一范围做完整回归，而不是只重跑失败点
- 直到通过、停滞、达到上限或确认阻塞

## 真相源

本技能的单轮执行引擎是：

- `.agents/skills/qa-engineer/SKILL.md`

必要时的根因收敛由：

- `.agents/skills/investigate/SKILL.md`

如果当前仓库保留了 issue 流程，问题追踪可选地使用：

- `.agents/skills/issue-manager/SKILL.md`

## 输入收敛

将用户意图收敛到以下参数：

- `scope`
  - `all`
  - `<scenario-name>`
  - `<freeform description>`
- `environment`
  - 默认 `current-repo`
- `max_rounds`
  - 默认 `3`
- `skip_fix`
  - 默认 `false`
- `unit_only`
  - 默认 `false`

如果当前仓库没有足够的现成场景文件，允许直接用 `explore` 方式运行。

## 执行流程

### Step 1: 确定本轮范围

按顺序选择：

1. 用户指定场景名 -> 读取 `.agents/skills/qa-engineer/scenarios/<name>.json`
2. 用户给自由描述 -> 转成 explore 型 QA 任务
3. 用户未指定 -> 默认 `all`

### Step 2: 做 preflight

开始前先确认：

- 当前工作区是否适合进入循环验证
- 是否存在无关基线失败
- 当前用户是只要 QA 结论，还是允许进入修复

默认 preflight：

```bash
git status --short
pnpm type-check
```

必要时再跑：

```bash
pnpm test
```

如果 preflight 就已经 BLOCKED，停止并汇报，不要伪造“开始循环”。

### Step 3: 执行 Round 1

每一轮都必须至少包含：

1. 本轮范围说明
2. 单轮 QA 执行
3. PASS / WARN / FAIL 汇总
4. 关键证据
5. 是否需要 investigate
6. 是否进入修复

### Step 4: 处理 FAIL / WARN

对每个 FAIL / 高价值 WARN：

- 先判断是否已有足够证据
- 根因不清晰时，切到 `$investigate`
- 若用户明确要跟踪且 issue 流程可用，再创建或补充 issue

### Step 5: 需要时进入修复

只有在以下条件同时满足时才进入修复：

- `skip_fix=false`
- 用户允许修复
- 问题已经足够清晰
- 当前失败不是纯环境阻塞

修复后必须做两层验证：

- 与本次修改直接相关的 targeted validation
- 同一 `scope` 的完整回归

不要只重跑失败步骤后就宣称已修复。

### Step 6: 进入下一轮

每轮结束都要明确：

- 轮次编号
- 本轮通过率
- 是否比上一轮改善
- 是否有新问题被发现
- 下一轮是否继续

停止条件：

- 全量 PASS
- 达到 `max_rounds`
- 连续 2 轮无实质改善
- 环境或基线问题导致 BLOCKED

## 产物建议

如果当前已有 task 目录，优先把 QA 产物写入该 task。

若没有 task 目录，可在当前上下文中以报告形式汇总，不强制生成额外文件。

若需要落盘，推荐结构：

```text
.trellis/tasks/<task>/qa/
  qa-log-round1.md
  qa-report-round1.md
  qa-log-round2.md
  qa-report-round2.md
```

## 输出要求

每轮都必须向用户同步：

- `scope`
- 当前轮次 / 上限
- 当前状态：`PASS` / `PARTIAL` / `FAIL` / `BLOCKED`
- 关键问题
- 下一步：继续修复 / 停止并汇报

推荐输出格式：

```markdown
## QA Loop

### Round

### Scope

### Result

### Evidence

### Issues / Risks

### Next Step
```

## 与其他技能的边界

- `$qa-engineer`：单轮执行与判断
- `$investigate`：根因调查
- `$issue-manager`：问题跟踪

你负责的是“编排和收敛”，不是替代这些技能本身。

## 禁止行为

- 只重跑失败步骤就宣称闭环完成
- 在根因不清晰时连续盲修多轮
- 对与本轮无关的基线故障装作没看见
- 伪造当前仓库不存在的 monitor、watcher、dashboard 或 stage 流程
