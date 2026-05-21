# 示例：独立审计

## 场景

对一个名为 `[your-project]` 的后端服务进行发布前独立审计。

## 组装方式

组合以下模板：
- `common/context-brief.md`
- `common/brutal-honesty.md`
- `common/output-format.md`
- `coding-agent/independent-audit.md`
- `snippets/architecture-quality.md`
- `snippets/no-env-no-secrets.md`

## 组装后的完整 prompt

```text
# 发布前独立审计

## Context Brief

项目路径：`[your-repo-path]`
技术栈：Go + PostgreSQL + Redis
关键目录：`cmd/`、`internal/`、`pkg/`、`migrations/`

请先检查：
- git status 和当前分支
- 最近的 commit 记录
- 是否有未提交的变更
- 确认没有 `.env` / `*.key` 等敏感文件被读取

## Brutal Honesty Protocol

本次审计的要求是"说出残酷的真相"。不要讨好、不要粉饰、不要回避。每个结论必须有具体证据支撑。

## Audit Scope

审计维度：代码质量、架构、测试、安全性、文档和可维护性、构建和部署。

审计规则：
- 只读，不修改任何文件
- 每个结论附带文件路径和行号
- 按 CRITICAL / HIGH / MEDIUM / LOW 分级

## Architecture Quality

在审计中特别注意：
- 模块边界是否清晰
- 是否高内聚、低耦合
- 是否存在循环依赖
- 数据流是否清晰可追踪
- 是否有过度抽象

## 安全约束

- 不读取 .env 或密钥文件
- 不 push / tag
- 审计结果中有任何涉及敏感信息的内容，用占位符替代

## 输出格式

按 `common/output-format.md` 的格式输出：
- 审计摘要（PASS / CONDITIONAL PASS / FAIL + 总体评级）
- 发现清单（按严重程度排列）
- 正面发现
- 建议优先级（top 5）
```

## 使用说明

1. 替换 `[your-repo-path]` 为实际仓库路径
2. 调整"技术栈"和"关键目录"为项目的实际值
3. 如果审计范围需要聚焦在特定模块（如只审计 `internal/auth/`），在 Audit Scope 中指定
4. 此 prompt 可以直接发给 Coding Agent

## 预期产物

一份结构化的审计报告，包含：
- 总体评级和发布建议
- 按严重程度分类的问题清单
- 正面发现
- 可执行的改进优先级

## 坏产出信号

- 问题没有附带文件路径和行号——只有结论没有证据
- 全是 LOW / MEDIUM，没有 CRITICAL / HIGH——可能在讨好
- 问题描述模糊（"代码质量需要改进"），没有指出具体是什么问题
- 审计摘要和问题清单中的严重程度不一致
