# 模板组合指南

## 组合原则

1. **common 模板是基础层**——几乎所有任务都应该先加载 context-brief 和 scope-lock
2. **coding-agent 模板是流程层**——定义具体的执行流程
3. **snippets 是约束层**——嵌入到其他模板中，增加具体约束
4. **project-integration 不是任务层**——它用于生成项目内的 `AGENTS.md`、`CLAUDE.md`、`current-task.md` 和可选入口 prompt，不应直接混入一次性任务 prompt
5. **不要过度组合**——一般 3-5 个模板足够，超过 5 个说明你可能想多了

## 常见组合模式

### 模式 1：快速修 bug

```
context-brief → scope-lock → bugfix-with-evidence + evidence-first + no-push-no-tag
```

**为什么这样组合**：
- context-brief：确保 Agent 理解项目结构
- scope-lock：防止 Agent 在修 bug 时顺手重构
- bugfix-with-evidence：要求先查日志、状态、测试再改代码
- evidence-first：强化证据优先原则
- no-push-no-tag：安全兜底

### 模式 2：SDD 实现新功能

```
context-brief → scope-lock → sdd-implementation + implementation-notes + architecture-quality + no-push-no-tag
```

**为什么这样组合**：
- sdd-implementation：按规格逐步实现
- implementation-notes：记录实现决策
- architecture-quality：确保架构边界清晰
- no-push-no-tag：实现完成但不由 Agent 决定何时 push

如果没有完整 SDD 文档、需求编号和验收标准，使用 `coding-agent/implementation-loop.md`，不要套用 SDD 流程。

### 模式 3：独立代码审计

```
context-brief → brutal-honesty → independent-audit + architecture-quality + no-env-no-secrets
```

**为什么这样组合**：
- brutal-honesty：要求审计者不讨好、不粉饰
- independent-audit：完整的只读审计流程
- architecture-quality：关注架构层面
- no-env-no-secrets：安全边界

如果只需要专项审查模块边界、依赖方向、内聚耦合、抽象质量和演进风险，使用 `coding-agent/architecture-review.md`；综合质量门审计仍使用 `coding-agent/independent-audit.md`。

### 模式 4：修复审计问题

```
context-brief → scope-lock → fix-audit-issues + evidence-first + implementation-notes + no-push-no-tag
```

### 模式 5：长上下文压缩

```
context-brief → scope-lock → compression-loop
```

### 模式 6：项目启动审查

```
context-brief → brutal-honesty → premortem + red-team + assumption-audit
```

### 模式 7：发布就绪检查

```
context-brief → brutal-honesty → release-readiness + red-team
```

### 模式 8：首次接入真实项目

```
project-onboarding → context-brief → scope-lock + no-env-no-secrets + no-push-no-tag
```

**为什么这样组合**：
- project-onboarding：12 步执行型接入审计，建立项目地图
- context-brief：接入完成后，维护轻量上下文
- scope-lock：理解项目后锁定执行范围
- no-env-no-secrets：敏感文件安全边界
- no-push-no-tag：安全兜底

### 模式 9：修复后 commit 前检查

```
commit-readiness + evidence-first + no-env-no-secrets + no-push-no-tag
```

**为什么这样组合**：
- commit-readiness：检查变更范围、敏感文件、测试、文档是否适合 commit
- evidence-first：确保每个检查结论有证据支撑
- no-env-no-secrets + no-push-no-tag：安全边界

## 组装步骤

1. 确定任务类型（修 bug / 新功能 / 审计 / 审查）
2. 从上方常见模式中选择匹配的组合
3. 把选中模板的"完整模板"部分复制出来
4. 在 ChatGPT 中，将多个模板拼接成一份完整指令
5. 替换所有占位符
6. 检查：组装后的 prompt 有没有矛盾？有没有遗漏？

## 组装示例

假设要修一个 bug，组装后的 prompt 大致是：

```
## Context Brief
[来自 common/context-brief.md 的完整模板]

## Scope Lock
[来自 common/scope-lock.md 的完整模板]

## Bug Fix Protocol
[来自 coding-agent/bugfix-with-evidence.md 的完整模板]

## Evidence First
[来自 snippets/evidence-first.md 的完整模板]

## Safety
[来自 snippets/no-push-no-tag.md 的完整模板]

本轮任务：[具体 bug 描述]
```

## 反模式

- 把 common 的所有模板全部加载——冗余，Agent 会混乱
- 在同一份 prompt 里同时要求"快速"和"全面"——矛盾
- 组合了 template A 需要 X 行为，template B 又禁止 X 行为——冲突
- 每个模板单独发送而不组装——浪费上下文窗口
