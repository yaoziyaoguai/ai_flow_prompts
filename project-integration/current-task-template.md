# Current Task 模板

## 适用场景

- 每轮新任务开始时，更新任务描述
- 需要 Coding Agent 清楚理解本轮要做什么、不做什么
- 多人/多 Coding Agent 协作时，需要统一的任务入口

## 不适合场景

- 任务不需要结构化描述（一句话能说清）
- 个人临时探索
- 项目长期规则（用 `project-integration/agents-md-template.md` 或 `project-integration/claude-md-template.md`）

## 可组合模块

- `common/scope-lock.md` —— 锁定本轮范围
- `common/context-brief.md` —— 如果项目上下文尚未建立

## 完整模板

```markdown
# Current Task —— [日期] [任务标题]

## 任务目标

[一句话描述本轮要完成什么]

## 背景

[为什么需要做这个任务？什么触发了它？]

## 成功标准

- [ ] [可验证的成功标准 1]
- [ ] [可验证的成功标准 2]
- [ ] [可验证的成功标准 3]

## 范围

### 包含
- [明确要做的事 1]
- [明确要做的事 2]

### 不包含
- [明确不做的事 1]
- [明确不做的事 2]

## 约束

- [技术约束、时间约束、依赖约束等]

## 相关文件

- `path/to/related/file1` — [为什么相关]
- `path/to/related/file2` — [为什么相关]

## 参考资料

- [设计文档、规格文档、issue 链接等]

## 完成后

- [ ] 功能已实现且符合成功标准
- [ ] 测试通过
- [ ] implementation-notes.md 已更新
- [ ] 本文件已标记为完成或归档
```

## 使用提醒

- 此文件建议放在项目 `docs/prompts/current-task.md`
- 每轮新任务更新此文件，任务完成后归档到 `docs/prompts/history/`
- 占位符 `[your-xxx]` 需要替换为实际内容
- 成功标准必须可验证——"代码质量好"不是可验证的标准，"所有测试通过且 lint 无错误"才是
