# 示例：修复审计问题

## 场景

审计报告已产出，发现 3 个 CRITICAL、7 个 HIGH、12 个 MEDIUM 问题。本轮目标是修复所有 CRITICAL 和 HIGH 问题。

## 组装方式

组合以下模板：
- `common/scope-lock.md`
- `common/output-format.md`
- `coding-agent/fix-audit-issues.md`
- `snippets/evidence-first.md`
- `snippets/implementation-notes.md`
- `snippets/no-push-no-tag.md`

## 组装后的完整 prompt

---

# 修复审计问题 —— Round 1

## Scope Lock

本轮范围：修复审计报告中的 CRITICAL 和 HIGH 级别问题（共 10 个）。

审计报告：[引用审计报告路径或内容]

### 允许的操作
- 修改代码以修复 CRITICAL 和 HIGH 问题
- 添加或更新测试
- 更新 implementation-notes.md

### 禁止的操作
- 不要修复 MEDIUM / LOW 问题（留待下一轮）
- 不要重构不相关的代码
- 不要引入新依赖
- 不要 push / tag

## Fix Protocol

按优先级修复：
1. 先修 CRITICAL（3 个）
2. 再修 HIGH（7 个）
3. 每修一个就验证，不要批量修完再测

## Evidence First

修改每个问题前：
- 理解审计报告引用的代码
- 确认问题确实存在
- 设计最小修改方案
- 验证修改不引入新问题

## Implementation Notes

在 `docs/prompts/implementation-notes.md` 中记录每个修复：
- 审计发现编号
- 修改的文件和内容
- 为什么选择这种修复方式
- 验证结果

## Output Format

修复完成后输出：
- 修复摘要（FIXED / WON'T FIX / NEEDS DISCUSSION）
- 每个修复的详细记录
- 修改文件清单

---

## 使用说明

1. 替换"审计报告"引用为实际路径或内容
2. 根据实际情况调整修复优先级和范围
3. 如果 CRITICAL 问题太多，可以分批修复
4. WON'T FIX 的决定需要用户二次确认后才能跳过

## 预期产物

- 所有 CRITICAL 和 HIGH 问题已修复的代码
- 更新的测试
- 完整的 implementation-notes.md

## 坏产出信号

- 只修了代码没加测试——修复没有验证
- implementation-notes.md 只有文件名列表，没有记录"为什么这样修"
- 修复了范围外的问题（MEDIUM / LOW 或无关重构）
- 修复引入了新问题但未发现（没有逐条验证）
