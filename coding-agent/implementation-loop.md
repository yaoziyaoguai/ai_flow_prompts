# Implementation Loop —— 实现循环

## 适用场景

- 有明确的功能规格、issue、审计修复清单或小功能说明，需要按目标实现
- 需要在实现过程中维护 implementation-notes.md
- 实现涉及多个文件、多个步骤
- 需要确保实现和本轮目标保持一致，但不需要严格 SDD 追踪

## 不适合场景

- 单文件的小改动
- 探索性编程（还不确定要做什么）
- 纯粹的重构（没有功能变化）
- 已有完整 SDD 文档、需求编号和验收标准，需要逐条追踪（用 `coding-agent/sdd-implementation.md`）

## 可组合模块

- `common/context-brief.md` —— 建立上下文
- `common/scope-lock.md` —— 锁定本轮范围
- `common/output-format.md` —— 约束实现报告格式
- `snippets/implementation-notes.md` —— 核心要求
- `snippets/architecture-quality.md` —— 架构质量约束
- `snippets/evidence-first.md` —— 修改前检查现有状态
- `snippets/no-push-no-tag.md` —— 安全边界

## 完整模板

---

# Implementation Loop

按照以下循环实现功能。每完成一个循环才进入下一个。

## 前置条件

- 本轮目标、范围和成功标准已明确
- 如果来自 issue、审计报告或规格文档，相关条目已经列出
- 实现范围已锁定（见 scope-lock）

## 与 SDD Implementation 的边界

- 普通 spec / issue / audit fix / small feature：使用本模板。
- 完整 SDD 文档、需求可追踪、验收标准明确：使用 `coding-agent/sdd-implementation.md`。
- 如果实现过程中发现需要逐条映射规格编号，切换到 SDD 模板，而不是在本模板里临时扩展一套追踪表。

## 循环流程

### Loop Step 1：分析
- 阅读本次要实现的功能规格
- 识别涉及的文件和模块
- 确认理解边界：改什么、不改什么

### Loop Step 2：实现
- 按照规格实现代码
- 保持高内聚、低耦合
- 不引入不必要的抽象
- 不修改与目标无关的代码

### Loop Step 3：记录
按 `snippets/implementation-notes.md` 的要求，在 `[project-path]/docs/prompts/implementation-notes.md` 中记录：

```markdown
## [日期] Step [N]：[简短标题]

### 做了什么
- [修改 1]
- [修改 2]

### 为什么这样做
- [决策理由 1]
- [决策理由 2]

### 修改的文件
- `path/to/file1` — [改动描述]
- `path/to/file2` — [改动描述]

### 遇到的问题
- [问题描述] → [解决方案]

### 待处理
- [遗留问题或后续步骤]
```

### Loop Step 4：验证
- 运行相关测试
- 确认没有引入回归
- 确认实现符合本轮目标、成功标准和范围约束

### Loop Step 5：检查
- 是否符合 `snippets/architecture-quality.md` 的高内聚、低耦合、不过度抽象要求？
- 是否符合 `snippets/evidence-first.md` 的证据优先要求？
- 是否有应该删除的临时代码或 debug 输出？
- 是否所有修改都有明确的理由？

## 完成标准

- [ ] 所有本轮目标和成功标准已实现
- [ ] 测试通过（或解释了为什么不能运行）
- [ ] implementation-notes.md 已更新
- [ ] 没有遗留的临时代码或 debug 输出
- [ ] 代码风格与项目一致
- [ ] 没有修改范围外的文件

---

## 使用提醒

- implementation-notes.md 是核心资产——不要跳过记录步骤
- 每个循环应该小而聚焦，不要在一个循环里做太多事
- 如果实现过程中发现规格、issue 或审计条目有问题，暂停并反馈，不要擅自修改目标
- 对于简单改动（单文件、几行），跳过完整循环，但记录仍然要做
- 如果任务要求严格按 SDD 文档逐条实现，改用 `coding-agent/sdd-implementation.md`
