# No Push No Tag —— 禁止 push / tag 片段

## 适用场景

- 嵌入到任何编程类模板中作为安全约束
- 防止 Agent 擅自 push 代码或创建 tag

## 完整片段

```text
## 安全约束：版本控制

以下操作在本次任务中**严格禁止**：

- `git push`（包括 `git push --force`）
- `git tag`
- 修改 remote 配置（`git remote add` / `git remote set-url` 等）
- 强制操作：`git reset --hard` / `git clean -fd`（除非用户明确要求）

允许的操作：
- `git status` / `git diff` / `git log`（只读）
- `git add` / `git commit`（本地提交）
- `git branch` / `git checkout -b`（本地分支管理）

如果任务需要 push 或 tag，必须先确认用户意图。
```

## 使用提醒

- 这是一个**可嵌入片段**，不是独立模板
- 嵌入位置：通常放在完整 prompt 的末尾，作为"安全约束"部分
- 如果项目配置了 AGENTS.md 且已包含此规则，模板中可省略此片段
