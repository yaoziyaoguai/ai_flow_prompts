# SDD Implementation —— 规格驱动实现

## 适用场景

- 有完整的 SDD / Spec 文档，需要严格按规格实现
- 采用 SDD（Specification-Driven Development）方法论
- 规格中已有需求编号、验收标准或可追踪条目
- 规格和实现之间的双向追溯

## 不适合场景

- 没有完整规格文档（用 `coding-agent/implementation-loop.md`）
- 只有 issue、审计修复清单或普通小功能说明（用 `coding-agent/implementation-loop.md`）
- 规格还在变化中（先稳定规格）
- 原型阶段（可以偏离规格探索）

## 可组合模块

- `common/context-brief.md` —— 建立上下文
- `common/scope-lock.md` —— 锁定范围（特别重要）
- `snippets/implementation-notes.md` —— 维护实现笔记
- `snippets/architecture-quality.md` —— 架构质量
- `snippets/evidence-first.md` —— 证据优先
- `snippets/no-push-no-tag.md` —— 安全边界

## 完整模板

---

# SDD Implementation Protocol

你现在的工作是**严格按规格文档实现功能**。规格文档是唯一的事实来源。

## 与 Implementation Loop 的边界

- 本模板只用于完整 SDD 场景：规格可追踪、验收标准明确、实现必须逐条映射。
- 普通 spec / issue / audit fix / small feature 使用 `coding-agent/implementation-loop.md`。
- 如果规格没有编号，先提取稳定的规格条目；如果无法提取，暂停并要求澄清，不要把普通实现流程伪装成 SDD。

## 核心原则

1. **规格是法律**：如果实现和规格不一致，实现是错的。
2. **不要偏离规格**：如果你觉得规格有问题，不要自行修改——先报告，等确认。
3. **逐条实现**：规格的每一条功能要求，都要有对应的实现。
4. **可追溯**：实现的每个部分，都要能追溯到规格的某一条要求。

## 前置工作

### Step 0：加载并理解规格

1. 阅读完整的规格文档
2. 列出规格中的所有功能要求（提取编号或标记）
3. 对每条要求标注：是否理解清楚 / 有无歧义
4. 如果有歧义，先澄清再继续

### Step 0.1：建立实现计划

根据规格拆解实现步骤：
- 哪些文件需要新建？
- 哪些文件需要修改？
- 实现顺序是什么？
- 每个步骤对应规格的哪条要求？
- 如何维护 `snippets/implementation-notes.md` 要求的实现记录？

## 实现循环

对实现计划中的每个步骤：

### 1. 实现
- 实现该步骤的功能
- 严格按照规格描述，不添加、不删减、不修改

### 2. 对照核查
- 对照规格原文，逐条确认实现是否正确
- 如果发现偏离，立即修正

### 3. 测试
- 为实现的规格条目编写测试
- 测试通过 = 实现正确

### 4. 记录
按 `snippets/implementation-notes.md` 的要求，在 implementation-notes.md 中记录规格映射和实现决策：

```markdown
## SDD 实现记录

### 规格条目映射

| 规格条目 | 实现位置 | 测试位置 | 状态 |
|----------|----------|----------|------|
| SPEC-01  | [文件:行] | [文件:行] | DONE |
| SPEC-02  | [文件:行] | [文件:行] | DONE |
| ...      | ...      | ...      | ...  |

### 实现决策

- [决策 1]：为什么选择这种实现方式
- [决策 2]：...
```

## 完成标准

- [ ] 所有规格条目都已实现
- [ ] 每个规格条目都有对应的测试
- [ ] 所有测试通过
- [ ] 实现和规格的映射表已更新
- [ ] 没有实现规格要求之外的任何功能
- [ ] 架构边界符合 `snippets/architecture-quality.md`
- [ ] 修改前证据和验证结果符合 `snippets/evidence-first.md`
- [ ] implementation-notes.md 完整

## 规格问题处理

如果在实现过程中发现规格问题：
1. 停止当前实现步骤
2. 描述发现的问题（引用规格原文 + 说明为什么有问题）
3. 提出建议的修改方案
4. 等待规格更新确认后再继续

---

## 使用提醒

- 这是严格的 SDD 流程——如果团队不遵循 SDD，用 `implementation-loop.md` 代替
- 规格条目映射表是防止遗漏和偏离的关键工具
- 如果规格本身质量差（模糊、矛盾），先修复规格再进入实现
- SDD 不等于"盲目遵守规格"——发现规格问题必须提出，但不应擅自修改
