# 示例：SDD 规格驱动实现

## 场景

有一个完整的功能规格文档，描述了一个用户认证模块。需要严格按照规格实现。

## 组装方式

组合以下模板：
- `common/context-brief.md`
- `common/scope-lock.md`
- `coding-agent/sdd-implementation.md`
- `snippets/implementation-notes.md`
- `snippets/architecture-quality.md`
- `snippets/no-push-no-tag.md`

## 组装后的完整 prompt

```text
# SDD Implementation —— 用户认证模块

## Context Brief

项目路径：`[your-repo-path]`
技术栈：TypeScript + Express + PostgreSQL
规格文档：`docs/specs/auth-module.md`
实现目录：`src/auth/`

## Scope Lock

### 本轮目标
严格按照 `docs/specs/auth-module.md` 实现用户认证模块。

规格中的功能要求：
- SPEC-AUTH-01：用户注册（邮箱 + 密码）
- SPEC-AUTH-02：用户登录（返回 JWT）
- SPEC-AUTH-03：Token 刷新
- SPEC-AUTH-04：密码重置流程
- SPEC-AUTH-05：登录失败次数限制

### 允许的操作
- 在 `src/auth/` 下新建文件
- 修改 `src/middleware/auth.ts`（添加认证中间件）
- 在 `tests/auth/` 下新建测试文件
- 更新 `docs/prompts/implementation-notes.md`

### 禁止的操作
- 不要修改 `src/` 下与 auth 无关的模块
- 不要修改数据库 schema（假设已完成）
- 不要引入新的 npm 依赖（假设依赖已就绪）
- 不要 push / tag

## SDD Protocol

1. 阅读规格文档 `docs/specs/auth-module.md`
2. 列出所有功能要求（SPEC-AUTH-01 到 05）
3. 逐条实现，每条实现后对照核查 + 编写测试 + 记录
4. 维护规格-实现映射表

## Architecture Quality

- 认证逻辑与业务逻辑分离
- Token 管理独立为一个子模块
- 中间件不包含业务逻辑，只做验证和转发
- 数据流向：Request → Middleware → Handler → Service → Repository → DB

## Implementation Notes

在 `docs/prompts/implementation-notes.md` 中记录全过程。
```

## 使用说明

1. 替换所有占位符为实际项目值
2. 规格文档路径必须指向一个真实存在的文件
3. "禁止的操作"中的约束需要根据项目实际状态调整
4. 如果规格中有歧义，先澄清再实现

## 预期产物

- 完整的认证模块实现
- 对应每个规格条目的测试
- 规格-实现映射表
- implementation-notes.md

## 坏产出信号

- 实现与规格条目无法一一对应——有遗漏或超出范围
- 测试只覆盖 happy path，未覆盖规格中的边界条件和错误场景
- 规格-实现映射表缺失或只列了文件名
- implementation-notes.md 中缺少关键决策记录（为什么选这个方案而不是另一个）
