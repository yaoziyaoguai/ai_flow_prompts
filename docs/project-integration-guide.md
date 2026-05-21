# 项目集成指南

## 集成方式概述

Prompt Library 可以通过两种方式集成到项目中：

1. **静态集成**：将项目级规则和入口模板放入项目的 AGENTS.md / CLAUDE.md / docs/prompts/
2. **动态集成**：通过 ChatGPT 从 Prompt Library 中选择模板，组装后发给 Coding Agent

推荐两者配合使用。

## project-integration 的边界

`project-integration/` 不是“直接发给 Coding Agent 的任务 prompt”分类。它用于生成真实项目中的常驻规则文件和本轮任务入口：

- `ai_flow_prompts` 维护者可以在本地使用被 `.gitignore` 忽略的根目录 `AGENTS.md` / `CLAUDE.md`，但这些不是用户模板
- `agents-md-template.md`：项目长期规则，面向所有 Coding Agent
- `claude-md-template.md`：Claude Code 的项目级补充规则
- `current-task-template.md`：本轮任务入口，记录目标、范围和成功标准
- `project-prompt-entry-template.md`：可选轻量入口，用于新会话时引导 Coding Agent 读取规则和本轮任务
- `global-agent-rules-template.zh.md` / `.en.md`：可复制到 Claude Code / Codex **全局** `CLAUDE.md` 或 `AGENTS.md` 的通用行为准则模板

一次性任务 prompt 应从 `common/`、`coding-agent/` 和 `snippets/` 组合；项目长期规则才放入 `project-integration/` 生成的文件。

## 静态集成：项目配置文件

### AGENTS.md（项目根目录）

定义一个项目的 Coding Agent 行为规则。模板见 `project-integration/agents-md-template.md`。

包含内容：
- 项目技术栈
- 编码规范
- 测试要求
- 安全边界
- 禁止事项

### CLAUDE.md（项目根目录）

定义 Claude Code 在该项目中的行为规则。模板见 `project-integration/claude-md-template.md`。

与 AGENTS.md 的区别：
- AGENTS.md 面向所有 Coding Agent（通用）
- CLAUDE.md 面向 Claude Code 特定行为（如 MCP 工具、slash command 等）

### docs/prompts/current-task.md（项目内）

存放当前任务的详细描述。模板见 `project-integration/current-task-template.md`。

每轮新任务时更新此文件。

## 动态集成：ChatGPT 组装流程

```
1. 我在 ChatGPT 中描述任务
2. ChatGPT 理解任务后，从 Prompt Library 中选择合适模板
3. ChatGPT 替换模板中的占位符，填入项目上下文
4. ChatGPT 输出组装好的完整 prompt
5. 我将 prompt 发送给 Coding Agent
```

## 项目入口 prompt（可选轻量入口）

复杂项目可以保留一个入口 prompt，用于新会话时初始化 Coding Agent。模板见 `project-integration/project-prompt-entry-template.md`。

入口 prompt 应该包含：
- 项目目标简述
- 技术栈
- 关键约束
- 指向 AGENTS.md 和 CLAUDE.md 的引用
- 本轮任务（或指向 current-task.md）

如果项目已经有清晰的 AGENTS.md / CLAUDE.md，并且每轮任务都通过 `docs/prompts/current-task.md` 管理，可以不额外维护入口 prompt。

## 目录结构建议

```
[your-project]/
  AGENTS.md                  # 项目 Coding Agent 规则
  CLAUDE.md                  # 项目 Claude Code 规则（可选）
  docs/
    prompts/
      current-task.md        # 本轮任务描述
      history/               # 已完成任务的决策日志归档（可选，不是项目记忆或进度账本）
  ...
```

## 与 ai_flow_prompts 的关系

- 不要将 ai_flow_prompts 作为 submodule 引入项目
- 不要将 ai_flow_prompts 的模板全量复制到项目中
- 只在需要时，从 ai_flow_prompts 选择相关模板，复制到项目或通过 ChatGPT 动态引用
- 项目中的 AGENTS.md 是**实例**，`project-integration/` 中的是**模板**，维护者本地的根目录 AGENTS.md / CLAUDE.md 是本仓库自用规则且不作为仓库内容分发——三者独立维护

## 常见问题

**Q：AGENTS.md 和 CLAUDE.md 里的内容会不会和模板重复？**

不会。AGENTS.md / CLAUDE.md 定义"规则"（什么能做、什么不能做），模板定义"方法"（怎么做）。规则是持久的，方法是按需加载的。

**Q：为什么要分离 current-task.md？**

因为任务描述会频繁变化，不适合放在 AGENTS.md（稳定规则）中。分离后，AGENTS.md 可以长期不变，current-task.md 每轮更新。
