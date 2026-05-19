# Commit Readiness —— 本地 commit 前检查

## 适用场景

- 准备在本地执行 `git commit` 之前
- 需要确认工作区变更是否适合提交
- 需要生成规范的 commit message
- 需要在 commit 前发现遗漏和风险

## 不适合场景

- 发布/部署前的检查（用 `release-readiness.md`）
- 代码评审（用 `independent-audit.md` + `brutal-honesty.md`）
- 需要实际执行 commit / push / tag 的任务（本模板只做就绪检查）
- 持续集成流水线中的自动检查（流水线本身已有检查逻辑）

## 可组合模块

- `common/brutal-honesty.md` —— 诚实的 commit 评估
- `common/output-format.md` —— 约束输出格式
- `snippets/no-push-no-tag.md` —— 安全边界
- `snippets/no-env-no-secrets.md` —— 敏感文件检查
- `snippets/implementation-notes.md` —— 实现笔记检查参考

## 完整模板

---

# Commit Readiness Checklist

对当前工作区进行本地 commit 前检查。不执行 commit，不 push，不 tag。

## 操作边界

- 只做 commit readiness review，不执行 `git commit`。
- 不执行 `git push`、`git tag` 或修改 remote。
- 不修改任何文件（只读检查）。

## 检查项

### 1. 环境确认
- [ ] 当前路径：`[pwd 输出]`
- [ ] 当前分支：`[git branch 输出]`
- [ ] 最近 commit：`[git log --oneline -5]`

### 2. 变更范围
- [ ] `git status` 输出确认
- [ ] `git diff --stat` 输出确认
- [ ] 是否有范围外修改？
  - **检查**：变更文件是否全部与本次任务相关
  - **若有范围外修改**：标记为 commit-blocking
- [ ] `git diff --check` 是否通过？
  - **若未通过**：标记为 commit-blocking（有 whitespace 错误）

### 3. 敏感文件检查
- [ ] 是否有 `.env` / `*.key` / `credentials.*` / `secrets.*` 出现在变更中？
  - **若有**：标记为 commit-blocking
- [ ] 是否有真实日志文件出现在变更中？
  - **若有**：标记为 commit-blocking
- [ ] 是否有私人数据文件（session、run、user data）出现在变更中？
  - **若有**：标记为 commit-blocking
- [ ] 确认未读取或写入 .env / secret 文件内容
- [ ] 确认未在代码中引入新的 secret / API key / token 硬编码

### 4. 代码质量
- [ ] 是否有临时 debug 代码（如 `console.log`、`print()`、`fmt.Println`、`dbg!`、`println!`、临时 logger 语句，或项目所用语言中等价的调试输出）？
- [ ] 是否有未完成的 TODO 占坑代码？
- [ ] 是否有被注释掉的代码块？
- [ ] 是否仍有 CRITICAL 或 HIGH 级别未修复问题？
  - **若有 CRITICAL**：标记为 commit-blocking
  - **若有 HIGH**：标记为 CONDITIONAL GO，需说明原因

### 5. 测试
- [ ] 测试是否已运行？
  - **证据**：`[your-test-command]` 的输出
  - **若未运行**：标记 UNKNOWN，建议运行后再 commit
- [ ] 测试是否全部通过？
  - **若有失败**：标记为 commit-blocking

### 6. 文档
- [ ] `implementation-notes.md` 是否需要更新？
  - **若需要但未更新**：标记为 CONDITIONAL GO
  - **若不需要**：说明原因（如：本次变更无新决策需要记录）
- [ ] README / docs 是否需要更新？
  - **若需要但未更新**：标记为 CONDITIONAL GO
  - **若不需要**：说明原因
- [ ] 是否有 breaking change 未在文档中标注？
  - **若有**：标记为 commit-blocking

## 输出

### Commit 判定

GO / NO-GO / CONDITIONAL GO（满足条件 X 后可 commit）

### UNKNOWN 项

列出所有标记为 UNKNOWN 的检查项及其影响。

### Commit-Blocking 问题

列出所有导致 NO-GO 的具体阻塞项。

### 建议 Commit Message

```
[type]: [description]

[变更原因、影响范围]
```

类型：feat / fix / refactor / docs / test / chore / perf / ci

### 安全确认

- [ ] 本轮未执行 `git push`
- [ ] 本轮未执行 `git tag`
- [ ] 本轮未修改 remote

---

## 使用提醒

- 这是 **commit readiness**，不是 release readiness——只管工作区是否适合本地 commit
- 发布/部署前检查用 `coding-agent/release-readiness.md`
- 不要自动执行 commit——本模板只输出判定和建议，由用户决定是否提交
- UNKNOWN 项不等于 PASS——在确认前保持 CONDITIONAL GO
- 如果 commit message 建议的 type 不确定，优先用 `chore` 或向用户确认
