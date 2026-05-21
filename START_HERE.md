# START_HERE —— 我现在要做什么？

按你的场景选择模板。有两种使用方式：

- **模式 A：直接复制命令** —— 打开 [COMMANDS.md](COMMANDS.md)，复制对应编号的命令发给 Coding Agent
- **模式 B：项目内自然语言路由** —— 将 [Workflow Router](project-integration/workflow-router-template.md) 嵌入项目的 AGENTS.md，之后在项目里说"审计一下"/"能提交吗"即可自动路由到正确模板

先分清文件类型：`coding-agent/`、`common/`、`snippets/`、`project-integration/` 中的文件是可复制/可执行的模板；`examples/` 是学习样例，不是规则源；`docs/` 是说明文档，不是执行模板。全局规则模板在 `project-integration/global-agent-rules-template.*`，项目级规则模板在 `project-integration/agents-md-template.md` / `project-integration/claude-md-template.md`。

---

## 我想让 Coding Agent 首次接入一个项目

→ 模板：[coding-agent/project-onboarding.md](coding-agent/project-onboarding.md)
→ 命令：[COMMANDS.md #1](COMMANDS.md#1-首次接入项目)

## 我想对代码做只读独立审计

→ 模板：[coding-agent/independent-audit.md](coding-agent/independent-audit.md) + [common/brutal-honesty.md](common/brutal-honesty.md)
→ 命令：[COMMANDS.md #2](COMMANDS.md#2-只读独立审计)

## 我想根据审计报告修复问题

→ 模板：[coding-agent/fix-audit-issues.md](coding-agent/fix-audit-issues.md)
→ 命令：[COMMANDS.md #3](COMMANDS.md#3-修复审计问题)
注意：修改前会先输出修复计划并 Ask User 确认。

## 我想修一个 bug

→ 模板：[coding-agent/bugfix-with-evidence.md](coding-agent/bugfix-with-evidence.md)
→ 命令：[COMMANDS.md #4](COMMANDS.md#4-bug-修复)

## 我想按规格实现功能

→ 模板：[coding-agent/implementation-loop.md](coding-agent/implementation-loop.md)
→ 命令：[COMMANDS.md #5](COMMANDS.md#5-按规格实现)

## 我想做 SDD 规格驱动实现

→ 模板：[coding-agent/sdd-implementation.md](coding-agent/sdd-implementation.md)
→ 命令：[COMMANDS.md #6](COMMANDS.md#6-sdd-规格驱动实现)

## 我想审查架构

→ 模板：[coding-agent/architecture-review.md](coding-agent/architecture-review.md)
→ 命令：[COMMANDS.md #7](COMMANDS.md#7-架构审查)

## 我想判断能不能 commit

→ 模板：[coding-agent/commit-readiness.md](coding-agent/commit-readiness.md)
→ 命令：[COMMANDS.md #8](COMMANDS.md#8-commit-前检查)

## 我想判断能不能发布

→ 模板：[coding-agent/release-readiness.md](coding-agent/release-readiness.md)
→ 命令：[COMMANDS.md #9](COMMANDS.md#9-release-前检查)

## 我想攻击方案找弱点（红队）

→ 模板：[common/red-team.md](common/red-team.md) + [common/premortem.md](common/premortem.md)
→ 命令：[COMMANDS.md #10](COMMANDS.md#10-红队审查)

## 我想压缩长对话上下文

→ 模板：[common/compression-loop.md](common/compression-loop.md)
→ 命令：[COMMANDS.md #11](COMMANDS.md#11-长上下文压缩)

## 我想让 ChatGPT 帮我组装 prompt

→ 命令：[COMMANDS.md #12](COMMANDS.md#12-让-chatgpt-生成-prompt)
ChatGPT 负责选择模板、填入参数、生成最终 prompt。

## 我想把好 prompt 沉淀回仓库

→ 标准见 [docs/usage-guide.md](docs/usage-guide.md) 底部的沉淀判断条件
→ 简单原则：重复使用 ≥3 次 + 跨项目通用 + 不含敏感信息 → 值得沉淀

---

## 我想配置全局 Coding Agent 行为规则

→ 模板：[project-integration/global-agent-rules-template.zh.md](project-integration/global-agent-rules-template.zh.md)（中文）或 [.en.md](project-integration/global-agent-rules-template.en.md)（英文）
复制到 `~/.claude/CLAUDE.md`（Claude Code 全局）或 Codex 全局 `AGENTS.md` 中使用。

## 我想给某个项目创建 AGENTS.md / CLAUDE.md

→ 项目级 AGENTS.md 模板：[project-integration/agents-md-template.md](project-integration/agents-md-template.md)
→ 项目级 CLAUDE.md 模板：[project-integration/claude-md-template.md](project-integration/claude-md-template.md)
这些模板复制到目标项目根目录使用。

## 不确定用哪个？

→ 先用 [common/context-brief.md](common/context-brief.md) 建立上下文
→ 或直接描述你的场景给 ChatGPT，让它帮你选

## 需要更详细的说明？

→ [docs/usage-guide.md](docs/usage-guide.md) —— 完整使用指南
→ [docs/composition-guide.md](docs/composition-guide.md) —— 模板组合方式
→ [docs/safety-boundaries.md](docs/safety-boundaries.md) —— 安全边界
