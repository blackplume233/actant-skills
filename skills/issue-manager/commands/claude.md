# Issue Management

管理当前仓库的 Issue。默认以 GitHub 为真相源，本地脚本和缓存仅作为辅助能力。

## Usage

```
/trellis:issue [action] [args]
```

## Actions

| Action | Description |
|--------|-------------|
| `create` | 创建新 Issue |
| `list` | 列出 Issue |
| `show <id>` | 查看 Issue 详情 |
| `close <id>` | 关闭 Issue |
| `search <query>` | 搜索 Issue |
| `stats` | Issue 统计 |

## Execution

读取 Skill 指南，然后按照工作流执行：

@.agents/skills/issue-manager/SKILL.md

根据用户的 action 参数执行对应操作：

1. 如果是 **create**（或无明确 action 但用户描述了一个问题/需求）：
   - 先搜索是否已存在同类 Issue
   - 确定类型（bug/feature/enhancement...）和优先级
   - 编写结构化 body
   - 优先使用 GitHub issue 流程；本地脚本存在时可作为辅助入口

2. 如果是 **list/show/search/stats**：
   - 直接执行对应命令并展示结果

3. 如果是 **close**：
   - 确认关闭原因（completed/not-planned/duplicate）
   - 优先使用 GitHub issue 流程；本地脚本存在时可作为辅助入口

用户指令：$ARGUMENTS
