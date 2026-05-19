# 使用指南

## 概述

本仓库的模板按两个维度组织：

1. **适用场景**（common → coding-agent；project-integration 用于项目级规则和入口）
2. **粒度**（完整模板 → 可嵌入片段）

## 基本用法

### 1. 选择模板

根据任务类型选择：

| 任务类型 | 推荐模板 |
|----------|----------|
| 开始任何任务前（轻量上下文） | `common/context-brief.md` |
| 首次接入真实项目（深度接入审计） | `coding-agent/project-onboarding.md` |
| 需要诚实反馈 | `common/brutal-honesty.md` |
| 审查方案安全性 | `common/red-team.md` |
| 防止 scope creep | `common/scope-lock.md` |
| 审查答案假设 | `common/assumption-audit.md` |
| 长上下文压缩 | `common/compression-loop.md` |
| 项目启动前 | `common/premortem.md` |
| 审计代码 | `coding-agent/independent-audit.md` |
| 修审计问题 | `coding-agent/fix-audit-issues.md` |
| 修 bug | `coding-agent/bugfix-with-evidence.md` |
| 按规格实现 | `coding-agent/implementation-loop.md` |
| SDD 实现 | `coding-agent/sdd-implementation.md` |
| 架构评审 | `coding-agent/architecture-review.md` |
| 本地 commit 前检查 | `coding-agent/commit-readiness.md` |
| 发布/部署前检查 | `coding-agent/release-readiness.md` |

**相似模板区分**：
- `project-onboarding.md` vs `context-brief.md`：前者是执行型 12 步接入审计（首次接触项目时用），后者是轻量上下文简报（日常会话中维护上下文用）
- `commit-readiness.md` vs `release-readiness.md`：前者判断工作区是否适合本地 commit，后者判断版本是否适合发布/部署/tag/release

### 2. 组合模板

大多数真实任务需要组合多个模板。见 `docs/composition-guide.md`。

典型组合示例：
- **修 bug** = context-brief + scope-lock + bugfix-with-evidence + evidence-first
- **SDD 实现** = context-brief + scope-lock + sdd-implementation + implementation-notes + architecture-quality
- **代码审计** = context-brief + brutal-honesty + independent-audit + architecture-quality

### 3. 在 ChatGPT 中使用

将选中的模板内容复制给 ChatGPT，并附上本轮任务描述：

```
我要做 [任务描述]。
项目背景：[简要上下文]。

请按照以下模板来组织你的分析和输出：

[粘贴模板内容]
```

### 4. 在 Coding Agent 中使用

方式 A：将组装好的 prompt 直接发给 Coding Agent。
方式 B：将相关模板内容放入项目的 `docs/prompts/current-task.md`，让 AGENTS.md 引用。

## 模板粒度选择

- **common/** —— 通用流程模板，适用于所有类型的 Coding Agent
- **coding-agent/** —— 针对 Coding Agent 的专用流程模板
- **snippets/** —— 可嵌入到其他模板中的短片段
- **project-integration/** —— 放在项目里的常驻规则和任务入口模板，不是一次性任务 prompt

## 什么时候不应该用模板

- 任务非常简单，一句话就能说清楚
- 任务是探索性的，不需要结构化流程
- 当前模板库中没有匹配的模板（不要强行套用）

遇到不匹配的情况，先用自然语言完成任务。如果这个场景重复出现 3 次以上，再考虑沉淀为模板。
