# actant-skills

Private agent skills repository — managed by the actant platform.

## Quick Start

```bash
# Install all skills globally
npx skills add blackplume233/actant-skills --skill '*' -g -y

# Install a specific skill
npx skills add blackplume233/actant-skills --skill gua -g
```

## ⚠ Essential: skill-repo-manager

**`skill-repo-manager` is the most important skill in this repository.** Every agent (Cursor, Claude Code, Codex CLI, or any other) should have it installed and active.

It manages the full lifecycle of this skill library — **search, install, and publish** — with built-in version control, privacy auditing, and changelog tracking. Without it, skills cannot be safely published or discovered.

**Install it first, always:**

```bash
npx skills add blackplume233/actant-skills --skill skill-repo-manager -g
```

> Any agent that needs to add, update, or publish skills must load `skill-repo-manager` before proceeding.

## Skills

### Core Workflow

| Skill | Description |
|-------|-------------|
| **skill-repo-manager** | Search, install, and publish skills with version control and privacy audit |
| **start** | Initialize AI dev session, read specs, report context |
| **brainstorm** | Requirements discovery before implementation |
| **finish-work** | Pre-ship review checklist |
| **ship** | Blocking delivery gate: spec sync, verify, commit, push |
| **ship-sub** | Sub-branch delivery: verify, push, create PR |
| **pr-handler** | PR merge readiness and delivery gate |
| **record-session** | Record work progress after tested and committed code |

### Development Guards

| Skill | Description |
|-------|-------------|
| **before-backend-dev** | Read backend guidelines before writing code |
| **before-frontend-dev** | Read frontend guidelines before writing code |
| **check-backend** | Verify backend code against guidelines |
| **check-frontend** | Verify frontend code against guidelines |
| **check-cross-layer** | Cross-layer data flow verification |
| **guard** | High-risk session guardrails |

### Loops & Investigation

| Skill | Description |
|-------|-------------|
| **codex-loop** | Multi-round implement/check convergence loop |
| **qa-loop** | QA convergence orchestrator |
| **qa-engineer** | Single-round QA execution |
| **investigate** | Root cause analysis: evidence → hypothesis → verification |
| **break-loop** | Deep bug analysis to prevent recurring issues |

### Utilities

| Skill | Description |
|-------|-------------|
| **gua** | 周易揲蓍占卦推演 — I Ching divination via yarrow stalk method |
| **create-command** | Create new CLI commands |
| **create-changelog-draft** | Draft changelog entries |
| **integrate-skill** | Integrate new skills into the system |
| **issue-manager** | Issue tracking and management |
| **wiki-updater** | Wiki documentation updater |
| **onboard** | New contributor onboarding |
| **project-reviewer** | Project-level code review |
| **update-spec** | Capture conventions into spec documents |
| **freeze** | Freeze current state |
| **find-skills** | Discover and install skills from the ecosystem |

## Publishing Skills

Use `skill-repo-manager` to publish. The workflow enforces:

1. **Version check** — new skills must be `1.0.0`, updates must increment
2. **Privacy audit** — 5-dimension review of all files (secrets, identity, paths, business, generalization)
3. **Changelog** — auto-updated under today's date
4. **Git commit** — Conventional Commits format
5. **Push** — to origin/main
