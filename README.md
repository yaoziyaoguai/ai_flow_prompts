# ai_flow_prompts

AI Workflow Prompt Library —— 让 ChatGPT / Claude Code / Codex 更稳定执行项目任务的 prompt 模板库。

> 不知道用哪个模板？→ **[START_HERE.md](START_HERE.md)**
> 只想复制命令？→ **[COMMANDS.md](COMMANDS.md)**
> 接入真实项目？→ **[docs/project-integration-guide.md](docs/project-integration-guide.md)**
> 想在项目里说"审计一下"自动触发？→ **[Workflow Router](project-integration/workflow-router-template.md)**

## 它解决什么问题

- 不想每次从零写 prompt
- 不想每次复制一大坨重复的安全约束
- 不想 Coding Agent 乱改文件、乱 push、读 .env、越界做事
- 想让多个项目复用同一套 Agent 指挥方法
- 想把跟 ChatGPT 聊出来的好 prompt 沉淀为长期资产

## 核心工作方式

| 层级 | 负责 |
|------|------|
| **Prompt Library**（本仓库） | **方法** —— 可复用的工作流模板 |
| **AGENTS.md / CLAUDE.md** | **规则** —— 项目级和个人级行为约束 |
| **current-task.md** | **本轮任务** —— 每次会话的具体目标 |
| **ChatGPT** | **判断和组装** —— 理解意图、选择模板、生成 prompt |
| **Coding Agent** | **执行** —— Claude Code / Codex 等 |

## 最常用入口

1. [project-onboarding](coding-agent/project-onboarding.md) —— 首次接入项目
2. [independent-audit](coding-agent/independent-audit.md) —— 只读独立审计
3. [fix-audit-issues](coding-agent/fix-audit-issues.md) —— 修复审计问题
4. [implementation-loop](coding-agent/implementation-loop.md) —— 按规格实现
5. [commit-readiness](coding-agent/commit-readiness.md) —— commit 前检查

更多场景 → **[START_HERE.md](START_HERE.md)** | 所有可复制命令 → **[COMMANDS.md](COMMANDS.md)**

## 目录

```
ai_flow_prompts/
  README.md / START_HERE.md / COMMANDS.md
  common/                 通用 prompt 模块
  coding-agent/           Coding Agent 执行型模板
  snippets/               可插拔约束片段
  project-integration/    接入真实项目的规则模板
  docs/                   使用指南、组合指南、安全边界
  examples/               脱敏示例
```

## 安全边界

本仓库不存 API key、.env 内容、内部 URL、真实日志、私人数据。所有示例使用占位符。详见 [docs/safety-boundaries.md](docs/safety-boundaries.md)。

## 推荐工作流

```
接到任务 → ChatGPT 判断+选模板 → 组装 prompt → Coding Agent 执行 → 回顾沉淀
```
