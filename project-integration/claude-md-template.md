# CLAUDE.md 模板（项目级）

定位说明：这是目标项目级 `CLAUDE.md` 模板，用于复制到某个具体项目根目录并补充 Claude Code 特定规则。它不是全局规则模板，也不是 `ai_flow_prompts` 仓库自用规则；项目级 CLAUDE.md 应补充项目上下文、构建/测试/lint 命令、目录结构、安全边界、`current-task.md` 和 workflow-router 关系。项目规则可以收紧全局规则，但不能放宽最低安全边界。

## 适用场景

- 项目中需要使用 Claude Code，需要项目级的行为规则
- 与用户级的 `~/.claude/CLAUDE.md` 配合使用（项目级规则更高优先级）
- 需要约束 Claude Code 的 MCP 工具使用、slash command 行为等

## 不适合场景

- 非 Claude Code 的 Coding Agent（用 AGENTS.md 即可）
- 已经通过 AGENTS.md 覆盖了所有规则
- 本轮任务 prompt（用 `project-integration/current-task-template.md`）

## 可组合模块

- `project-integration/agents-md-template.md` —— 通用 Coding Agent 规则
- `project-integration/current-task-template.md` —— 本轮任务入口

## 完整模板

```markdown
# CLAUDE.md —— [your-project] 项目 Claude Code 规则

本文件约束 Claude Code 在此项目中的行为。

---

## 项目上下文

- 技术栈：[语言、框架、主要依赖]
- 关键目录：[核心代码目录说明]
- 构建方式：[如何构建和运行]

## Claude Code 特定规则

### MCP 工具使用
- [指定哪些 MCP 工具可用]
- [指定哪些 MCP 工具不可用]

### 文件操作
- 只修改与任务直接相关的文件
- 修改前先读取并理解文件
- 不要创建不必要的文件

### Git 操作
- 不要 push / tag / 修改 remote
- 可以创建新分支
- commit 前确认变更合理

### 代码修改原则
- 优先最小修改
- 不引入不必要的抽象
- 修改后验证（lint、测试）
- 遵循项目现有代码风格

## 与其他配置文件的关系

- 项目 AGENTS.md：通用 Coding Agent 规则（所有 Coding Agent 遵守）
- 本文件：Claude Code 特定规则（补充 AGENTS.md）
- ~/.claude/CLAUDE.md：用户全局规则（优先级最低）
- docs/prompts/current-task.md：本轮任务描述
```

## 使用提醒

- 此模板放入项目根目录，命名为 `CLAUDE.md`
- 如果已有 AGENTS.md 且内容已经覆盖，CLAUDE.md 可以只写 Claude Code 特有的规则
- 项目级 CLAUDE.md 的优先级高于用户级 `~/.claude/CLAUDE.md`
- 不要在此文件中放入敏感信息（secret、内部 URL 等）
