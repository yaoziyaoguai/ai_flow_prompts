# COMMANDS —— 可直接复制的短命令

复制对应编号的命令，直接发给 Claude Code / Codex。

> 使用前：将命令中的 `ai_flow_prompts/` 替换为本仓库在你机器上的实际路径。

---

## 全局安全默认规则

以下规则适用于下方所有命令。每条可复制命令也会重复最低安全边界，避免只复制单条命令时丢失约束。

- **不读取 .env 或任何包含 secret / 私密数据的文件**
- **不 push / tag / 修改 remote**（除非用户当前会话中明确要求）
- **不确定时 Ask User**（不要猜测，不要假设）
- **只读场景不修改任何文件**
- **UNKNOWN ≠ PASS**（证据不足时标记 UNKNOWN，不假设通过）

---

### #1 首次接入项目

> 请读取 ai_flow_prompts/coding-agent/project-onboarding.md，对当前项目做只读接入审计。只读执行，不修改文件。遵守最低安全边界：不读取 .env/secret/private data；不 push/tag/修改 remote；UNKNOWN 不能当 PASS；不确定就 Ask User。

### #2 只读独立审计

> 请读取 ai_flow_prompts/coding-agent/independent-audit.md 和 ai_flow_prompts/common/brutal-honesty.md，对当前项目做只读独立审计。只读执行，不修改文件。遵守最低安全边界：不读取 .env/secret/private data；不 push/tag/修改 remote；UNKNOWN 不能当 PASS；不确定就 Ask User。

### #3 修复审计问题

> 请读取 ai_flow_prompts/coding-agent/fix-audit-issues.md。在修改任何文件前必须先输出修复计划并 Ask User 确认。遵守最低安全边界：不读取 .env/secret/private data；不 push/tag/修改 remote；UNKNOWN 不能当 PASS；不确定就 Ask User。

### #4 Bug 修复

> 请读取 ai_flow_prompts/coding-agent/bugfix-with-evidence.md。先查日志和状态确认根因，再修改代码。遵守最低安全边界：不读取 .env/secret/private data；不 push/tag/修改 remote；UNKNOWN 不能当 PASS；不确定就 Ask User。

### #5 按规格实现

> 请读取 ai_flow_prompts/coding-agent/implementation-loop.md。按规格逐步实现，每步验证后记录。遵守最低安全边界：不读取 .env/secret/private data；不 push/tag/修改 remote；UNKNOWN 不能当 PASS；不确定就 Ask User。

### #6 SDD 规格驱动实现

> 请读取 ai_flow_prompts/coding-agent/sdd-implementation.md。严格按规格文档逐条实现，维护规格-实现映射表。遵守最低安全边界：不读取 .env/secret/private data；不 push/tag/修改 remote；UNKNOWN 不能当 PASS；不确定就 Ask User。

### #7 架构审查

> 请读取 ai_flow_prompts/coding-agent/architecture-review.md，对当前项目做架构审查。只读执行，不修改文件。遵守最低安全边界：不读取 .env/secret/private data；不 push/tag/修改 remote；UNKNOWN 不能当 PASS；不确定就 Ask User。

### #8 Commit 前检查

> 请读取 ai_flow_prompts/coding-agent/commit-readiness.md，对当前工作区做 commit 前检查。只检查，不执行 commit/tag/push/release；只读执行，不修改文件。遵守最低安全边界：不读取 .env/secret/private data；不 push/tag/修改 remote；UNKNOWN 不能当 PASS；不确定就 Ask User。

### #9 Release 前检查

> 请读取 ai_flow_prompts/coding-agent/release-readiness.md，对当前版本做发布就绪检查。只检查，不执行 commit/tag/push/release；只读执行，不修改文件。遵守最低安全边界：不读取 .env/secret/private data；不 push/tag/修改 remote；UNKNOWN 不能当 PASS；不确定就 Ask User。

### #10 红队审查

> 请读取 ai_flow_prompts/common/red-team.md 和 ai_flow_prompts/common/premortem.md，攻击当前方案找弱点。只读执行，不修改文件。遵守最低安全边界：不读取 .env/secret/private data；不 push/tag/修改 remote；UNKNOWN 不能当 PASS；不确定就 Ask User。

### #11 长上下文压缩

> 请读取 ai_flow_prompts/common/compression-loop.md，将当前会话上下文压缩为结构化交接文档。只读执行，不修改文件。遵守最低安全边界：不读取 .env/secret/private data；不 push/tag/修改 remote；UNKNOWN 不能当 PASS；不确定就 Ask User。

### #12 让 ChatGPT 生成 prompt

> 请参考 ai_flow_prompts 的风格，帮我根据当前项目状态生成一条给 Claude Code 的 prompt。要求包含 context-brief、scope-lock、evidence-first、no-push-no-tag。我的项目信息：[描述你的项目和技术栈]。我本轮要做：[描述任务]。只输出文本，不写文件。遵守最低安全边界：不读取 .env/secret/private data；不 push/tag/修改 remote；UNKNOWN 不能当 PASS；不确定就 Ask User。

---

## 方案设计（未纳入编号，按需使用）

> 请读取 ai_flow_prompts/coding-agent/planning.md。对当前需求做轻量方案设计，输出 GO / NO-GO / NEEDS_USER_DECISION。只读执行，不修改文件。遵守最低安全边界：不读取 .env/secret/private data；不 push/tag/修改 remote；UNKNOWN 不能当 PASS；不确定就 Ask User。
