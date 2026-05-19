# COMMANDS —— 可直接复制的短命令

复制对应编号的命令，直接发给 Claude Code / Codex。每条命令已内置安全约束。

> 使用前：将命令中的 `ai_flow_prompts/` 替换为本仓库在你机器上的实际路径。

---

### #1 首次接入项目

> 请读取 ai_flow_prompts/coding-agent/project-onboarding.md，对当前项目做只读接入审计。不修改任何文件。不读取 .env。不 push、不 tag、不修改 remote。不确定就 Ask User。

### #2 只读独立审计

> 请读取 ai_flow_prompts/coding-agent/independent-audit.md 和 ai_flow_prompts/common/brutal-honesty.md，对当前项目做只读独立审计。不修改任何文件。不读取 .env。不 push、不 tag、不修改 remote。不确定就 Ask User。

### #3 修复审计问题

> 请读取 ai_flow_prompts/coding-agent/fix-audit-issues.md。在修改任何文件前必须先输出修复计划并 Ask User 确认。不读取 .env。不 push、不 tag、不修改 remote。

### #4 Bug 修复

> 请读取 ai_flow_prompts/coding-agent/bugfix-with-evidence.md。先查日志和状态确认根因，再修改代码。不读取 .env。不 push、不 tag、不修改 remote。不确定就 Ask User。

### #5 按规格实现

> 请读取 ai_flow_prompts/coding-agent/implementation-loop.md。按规格逐步实现，每步验证后记录。不读取 .env。不 push、不 tag、不修改 remote。不确定就 Ask User。

### #6 SDD 规格驱动实现

> 请读取 ai_flow_prompts/coding-agent/sdd-implementation.md。严格按规格文档逐条实现，维护规格-实现映射表。不读取 .env。不 push、不 tag、不修改 remote。

### #7 架构审查

> 请读取 ai_flow_prompts/coding-agent/architecture-review.md，对当前项目做架构审查。不修改任何文件。不读取 .env。不 push、不 tag、不修改 remote。

### #8 Commit 前检查

> 请读取 ai_flow_prompts/coding-agent/commit-readiness.md，对当前工作区做 commit 前检查。只输出 GO / NO-GO / CONDITIONAL GO，不要执行 commit。不读取 .env。不 push、不 tag、不修改 remote。

### #9 Release 前检查

> 请读取 ai_flow_prompts/coding-agent/release-readiness.md，对当前版本做发布就绪检查。只输出 GO / NO-GO / CONDITIONAL GO，不要执行发布。不读取 .env。不 push、不 tag、不修改 remote。

### #10 红队审查

> 请读取 ai_flow_prompts/common/red-team.md 和 ai_flow_prompts/common/premortem.md，攻击当前方案找弱点。不修改任何文件。不读取 .env。不 push、不 tag、不修改 remote。

### #11 长上下文压缩

> 请读取 ai_flow_prompts/common/compression-loop.md，将当前会话上下文压缩为结构化交接文档。不读取 .env。不 push、不 tag、不修改 remote。

### #12 让 ChatGPT 生成 prompt

> 请参考 ai_flow_prompts 的风格，帮我根据当前项目状态生成一条给 Claude Code 的 prompt。要求包含 context-brief、scope-lock、evidence-first、no-push-no-tag。我的项目信息：[描述你的项目和技术栈]。我本轮要做：[描述任务]。
