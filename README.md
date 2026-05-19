# ai_flow_prompts

AI Workflow Prompt Library —— 用于 ChatGPT / Claude Code / Codex / Coding Agent 的 prompt 模板库。

## 一句话介绍

把「跟 ChatGPT 聊出来的好 prompt」沉淀为可复用的工作流模板。不是普通收藏夹——每个模板都经过真实项目验证，可直接复制使用。

## 它解决什么问题

- 不想每次从零写 prompt
- 不想每次都复制一大坨重复的安全约束
- 不想 Coding Agent 乱改文件、乱 push、读 .env、越界做事
- 想让多个项目复用同一套 Agent 指挥方法
- 想让 ChatGPT 继续做动态判断，但让好 prompt 能沉淀为长期资产

## 核心工作方式

| 层级 | 负责 |
|------|------|
| **Prompt Library**（本仓库） | **方法** —— 可复用的工作流模板 |
| **AGENTS.md / CLAUDE.md** | **规则** —— 项目级和个人级 Coding Agent 行为约束 |
| **docs/prompts/current-task.md** | **本轮任务** —— 每次会话的具体目标 |
| **ChatGPT** | **判断和组装** —— 理解意图、选择模板、生成最终 prompt |
| **Coding Agent** | **执行** —— Claude Code / Codex 等 |

ChatGPT 仍然是指挥参谋。Prompt Library 让它有标准件可用，不替代它的判断。

## 最快开始

### 场景 A：让 ChatGPT 帮你生成 prompt

对 ChatGPT 说：

> 请参考 ai_flow_prompts 的风格，帮我根据当前项目状态生成一条给 Claude Code 的修复 prompt。要求包含 context-brief、scope-lock、evidence-first、no-push-no-tag。

### 场景 B：让 Coding Agent 首次接入项目

对 Coding Agent 说：

> 请读取 ai_flow_prompts/coding-agent/project-onboarding.md，对当前项目做只读接入审计。不要修改文件。

### 场景 C：项目已接入 AGENTS.md + current-task.md

对 Coding Agent 说：

> 请遵守 AGENTS.md，读取 docs/prompts/current-task.md，按其中任务执行。需要通用模板时参考 ai_flow_prompts。

### 场景 D：修完代码后判断能不能 commit

对 Coding Agent 说：

> 请读取 ai_flow_prompts/coding-agent/commit-readiness.md，对当前工作区做 commit readiness 检查。只输出 GO / NO-GO / CONDITIONAL GO，不要执行 commit。

## 常见使用场景

| 场景 | 推荐模板 | 可直接用的短命令 |
|------|----------|-----------------|
| 新项目首次接入 | `coding-agent/project-onboarding.md` | 「读取 project-onboarding.md，对当前项目做只读接入审计」 |
| 只读独立审计 | `coding-agent/independent-audit.md` + `common/brutal-honesty.md` | 「读取 independent-audit.md + brutal-honesty.md，审计当前项目」 |
| 根据审计报告修复 | `coding-agent/fix-audit-issues.md` | 「读取 fix-audit-issues.md，按审计报告修复 CRITICAL 和 HIGH」 |
| Bug 修复 | `coding-agent/bugfix-with-evidence.md` | 「读取 bugfix-with-evidence.md，先查日志和状态再改代码」 |
| 按规格实现 | `coding-agent/implementation-loop.md` | 「读取 implementation-loop.md，按规格逐步实现并记录」 |
| SDD 规格驱动 | `coding-agent/sdd-implementation.md` | 「读取 sdd-implementation.md，严格按规格文档逐条实现」 |
| 架构专项审查 | `coding-agent/architecture-review.md` | 「读取 architecture-review.md，审查当前项目架构」 |
| commit 前检查 | `coding-agent/commit-readiness.md` | 「读取 commit-readiness.md，做 commit 前检查，不要执行 commit」 |
| release 前检查 | `coding-agent/release-readiness.md` | 「读取 release-readiness.md，做发布就绪检查，不要执行发布」 |
| 长上下文压缩 | `common/compression-loop.md` | 「读取 compression-loop.md，压缩当前会话上下文为交接文档」 |
| 方案红队/前期验尸 | `common/red-team.md` + `common/premortem.md` | 「读取 red-team.md + premortem.md，攻击当前方案找弱点」 |

更多场景和组合方式见 `docs/composition-guide.md`。

## 目录结构

```
ai_flow_prompts/
  README.md
  CLAUDE.md                             # 本仓库自身的 Coding Agent 规则

  common/                               # 通用 prompt 模块（适用于所有场景）
    context-brief.md                    # 轻量上下文建立
    brutal-honesty.md                   # 强制诚实、反讨好
    scope-lock.md                       # 范围锁定
    output-format.md                    # 输出格式约束
    red-team.md                         # 方案摧毁、魔鬼倡导者
    premortem.md                        # 项目前期验尸
    assumption-audit.md                 # 假设审计
    compression-loop.md                 # 长上下文压缩

  coding-agent/                         # Coding Agent 执行型工作流模板
    project-onboarding.md               # 首次接入项目审计（12 步）
    independent-audit.md                # 只读独立审计
    fix-audit-issues.md                 # 修复审计问题（含 Ask User 确认）
    bugfix-with-evidence.md             # 证据驱动的 bug 修复
    implementation-loop.md              # 实现循环
    sdd-implementation.md               # SDD 规格驱动实现
    architecture-review.md              # 架构评审
    commit-readiness.md                 # 本地 commit 前检查
    release-readiness.md                # 发布/部署前检查

  snippets/                             # 可插拔约束片段（嵌入到其他模板中）
    no-push-no-tag.md
    no-env-no-secrets.md
    evidence-first.md
    implementation-notes.md
    architecture-quality.md
    chinese-learning-comments.md

  project-integration/                  # 接入真实项目用的规则和入口模板
    agents-md-template.md
    claude-md-template.md
    current-task-template.md
    project-prompt-entry-template.md    # 可选轻量入口

  docs/                                 # 使用指南、组合指南、安全边界
    usage-guide.md
    composition-guide.md
    safety-boundaries.md
    project-integration-guide.md

  examples/                             # 脱敏使用示例
    example-independent-audit.md
    example-fix-audit-issues.md
    example-sdd-implementation.md
    example-context-compression.md
```

## 如何接入一个真实项目

1. 复制 `project-integration/agents-md-template.md` → 项目根目录 `AGENTS.md`，填入项目规则
2. 复制 `project-integration/current-task-template.md` → `docs/prompts/current-task.md`，填入本轮任务
3. （可选）复制 `project-integration/project-prompt-entry-template.md` → 项目根目录，作为一次性会话入口
4. 每次新会话，让 Coding Agent 读取 `AGENTS.md` + `current-task.md`
5. 需要通用流程时，引用本仓库对应模板

详见 `docs/project-integration-guide.md`。

## 安全边界

本仓库**不应该存**：
- API key / token / 密码
- .env 内容
- 公司内部 URL / 真实 IP / 真实域名
- 真实日志内容
- 私人数据
- 真实项目名 / 真实人员名
- 未脱敏的业务上下文

所有示例使用 `[your-project]`、`[your-repo-path]` 等占位符。违反安全边界的模板不应被创建。

详见 `docs/safety-boundaries.md`。

## 什么时候值得沉淀一个 prompt

**值得沉淀：**
- 会重复使用（≥3 次且效果稳定）
- 能跨项目复用（不含项目特定上下文）
- 有稳定结构和明确边界
- 能减少 Agent 出错

**不值得沉淀：**
- 一次性问题
- 绑定真实业务上下文
- 包含敏感信息
- 还没有被验证有效

宁可缺，不要滥。

## 推荐工作流

```
1. 接到任务
      ↓
2. 在 ChatGPT 中描述任务，ChatGPT 判断需要哪些模板
      ↓
3. ChatGPT 从 Prompt Library 中选择和组装模板，填入本轮参数
      ↓
4. 把组装好的 prompt 发给 Coding Agent
      ↓
5. Coding Agent 执行，产出结果
      ↓
6. 回顾：这次用的模板有效吗？
      ↓
7. 有效且通用 → 考虑沉淀新模板 / 无效 → 修订或标记不适合场景
```
