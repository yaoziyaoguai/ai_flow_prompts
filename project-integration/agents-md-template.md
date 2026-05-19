# AGENTS.md 模板

## 适用场景

- 初始化新项目时，需要创建项目的 AGENTS.md
- 已有项目需要规范化 Coding Agent 行为约束
- 项目被多个 Coding Agent 使用，需要统一的规则

## 不适合场景

- 个人一次性脚本（不需要 AGENTS.md）
- 已经有一套完善的 AGENTS.md 且运行良好
- 本轮任务 prompt（用 `project-integration/current-task-template.md`）

## 可组合模块

- `project-integration/claude-md-template.md` —— CLAUDE.md 特定规则
- `project-integration/current-task-template.md` —— 本轮任务入口
- `snippets/no-push-no-tag.md` —— 可嵌入的安全约束
- `snippets/no-env-no-secrets.md` —— 可嵌入的安全约束
- `snippets/architecture-quality.md` —— 可嵌入的架构约束

## 完整模板

```markdown
# AGENTS.md —— [your-project] 项目 Coding Agent 规则

本文件约束所有在此项目中工作的 Coding Agent 的行为。

---

## 项目概述

- 项目名称：[your-project]
- 技术栈：[语言、框架、主要依赖]
- 项目目标：[一句话描述]

## 编码规范

- [语言特定的编码规范]
- 命名约定：[项目命名约定]
- 文件组织：[目录结构说明]
- 代码风格：[遵循的风格指南]

## 测试要求

- 测试框架：[测试框架名]
- 最低覆盖率：[如 80%]
- 测试类型要求：[单元测试 / 集成测试 / E2E 测试]

## 安全规则

- 不要读取 .env 或任何包含 secret 的文件
- 不要在代码中硬编码 secret
- 不要修改认证/授权相关代码，除非明确要求
- [项目特定的安全规则]

## 禁止事项

- 不要 push / tag / 修改 remote，除非用户明确要求
- 不要修改与任务无关的文件
- 不要引入新的依赖，除非确有必要并得到确认
- 不要擅自更改项目配置文件
- [项目特定的禁止事项]

## 修改前检查

在修改任何代码之前：
1. 理解当前代码的行为
2. 检查是否有相关测试
3. 确认修改不会破坏现有功能
4. 如果修改影响其他模块，先确认

## 文档

- 关键设计决策应记录在 docs/ 中
- 复杂逻辑应有注释说明
- 不要为显而易见的代码写注释
```

## 使用提醒

- 此模板放入项目的根目录，命名为 `AGENTS.md`
- 根据项目的实际技术栈和约束填充 `[your-xxx]` 占位符
- 不要照搬此模板的全部内容——只保留与项目相关的规则
- AGENTS.md 应该保持简洁（建议不超过 200 行）
- 规则更新频率：按季度回顾和更新
