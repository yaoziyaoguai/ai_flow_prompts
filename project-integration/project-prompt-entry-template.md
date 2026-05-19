# Project Prompt Entry 模板（可选轻量入口）

> **定位**：这是一个可选轻量入口。如果项目已通过 AGENTS.md / CLAUDE.md 定义规则，通过 `docs/prompts/current-task.md` 管理每轮任务，通常**不需要**此模板。它只适合「一次性初始化 Coding Agent 会话」的场景——让 Agent 在单次会话开始时知道要读取哪些文件。它不是项目长期规则文件，也不替代 current-task.md。

## 适用场景

- 项目需要一个一次性会话入口，让 Coding Agent 快速进入工作状态
- 项目尚未建立 AGENTS.md / current-task.md 体系，需要一个过渡入口
- 需要在多轮会话间保持一致的引导方式

## 不适合场景

- 项目没有固定的开发环境
- 一次性任务
- 已经通过 AGENTS.md / CLAUDE.md / current-task.md 清楚表达了规则和任务，不需要额外入口

## 可组合模块

- `project-integration/agents-md-template.md` —— 已经被引用
- `project-integration/current-task-template.md` —— 已经被引用

## 完整模板

```markdown
# [your-project] —— Coding Agent 入口

## 项目信息

- 项目名称：[your-project]
- 仓库路径：[your-repo-path]
- 技术栈：[语言、框架、主要依赖]
- 当前分支：[branch-name]

## 核心规则

请先阅读并遵守以下规则文件：
- `AGENTS.md` —— 项目 Coding Agent 规则（最高优先级）
- `CLAUDE.md` —— Claude Code 特定规则（如存在）
- `docs/prompts/current-task.md` —— 本轮任务描述

## 关键约束

- 不要 push / tag / 修改 remote
- 不要读取 .env 或任何包含 secret 的文件
- 修改代码前先检查现有测试和文档
- 遵循项目现有代码风格
- 记录关键决策

## 本轮任务

详见 `docs/prompts/current-task.md`

## 开始前检查

在开始工作前，请完成以下检查：

1. [ ] 确认当前分支和 git 状态
2. [ ] 确认相关测试是否可以运行
3. [ ] 确认是否有未完成的变更需要处理
4. [ ] 确认本轮任务的范围和成功标准
```

## 使用提醒

- 此文件放入项目根目录或 `docs/prompts/`，每次启动新会话时发送给 Coding Agent
- 项目信息和关键约束需要维护更新
- 这是一个可选轻量入口——它不替代 AGENTS.md 和 current-task.md，而是引导 Coding Agent 读取它们
