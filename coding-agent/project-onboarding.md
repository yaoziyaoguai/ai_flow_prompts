# Project Onboarding —— Coding Agent 项目接入审计

## 适用场景

- Coding Agent 首次接触一个真实项目
- 需要快速理解项目结构、规则和边界
- 需要在执行任何任务前确认安全边界
- 项目文档分散，需要一次性建立全局视图

## 不适合场景

- 已经在同一项目中工作多轮，上下文已建立
- 只需要轻量级上下文建立（用 `common/context-brief.md`）
- 探索性空项目，结构尚未定型

## 可组合模块

- `common/context-brief.md` —— 接入完成后，后续用 context-brief 维护上下文
- `common/scope-lock.md` —— 理解项目后锁定执行范围
- `snippets/no-env-no-secrets.md` —— 敏感文件检查规则
- `snippets/architecture-quality.md` —— 模块边界和质量标准

## 完整模板

---

# Project Onboarding

你正在首次接触一个真实项目。在开始任何工作之前，执行以下接入审计。**全程只读，不修改任何文件。**

## Step 1：环境确认

- 当前工作路径：`[pwd]`
- 确认此路径是你理解的项目根目录
- **如果路径与用户描述不符，立即停止并 Ask User**

## Step 2：Git 状态扫描

运行以下只读命令：
- `git status`
- `git branch`
- `git log --oneline -10`
- `git tag --list | tail -20`
- `git branch -v`（查看 ahead/behind 状态）

检查是否有以下异常：
- detached HEAD
- merge conflict 未解决
- rebase in progress
- 大量未提交变更
- **以上任一异常 → 停止并 Ask User**

## Step 3：项目根目录结构扫描

只读扫描根目录（`ls -la` 或等效），记录：
- 顶层文件和目录
- 项目大致规模

## Step 4：规则文件发现

查找以下规则文件（只检查是否存在）：
- `AGENTS.md`
- `CLAUDE.md`
- `README.md`
- `docs/` 目录
- `.github/` 目录
- `.claude/` 目录

如果找到规则文件（AGENTS.md / CLAUDE.md / README.md），读取其中的关键规则和约束。这些是公开文件，不包含 secret。

## Step 5：项目类型识别

查找项目入口和配置文件（只检查是否存在）：
- `package.json` / `pyproject.toml` / `Cargo.toml` / `go.mod` / `Makefile` / `docker-compose.yml` / `pom.xml` / `build.gradle` 等
- 识别技术栈和主要依赖

## Step 6：敏感文件识别（不能读取内容）

扫描是否存在以下文件/目录。**只记录存在性，绝对不能读取内容**：
- `.env` / `.env.*`
- `*.key` / `*.pem` / `*.cert`
- `credentials.*` / `secrets.*`
- `logs/` / `*.log`
- `sessions/` / `runs/`
- 任何路径包含 `private` / `secret` / `confidential` 的文件或目录
- `data/` 目录（可能包含用户数据）

发现敏感文件时，仅在报告中标记 `[敏感文件，未读取]`。
**如果因为敏感文件无法读取而导致无法完成后续步骤，标记为 UNKNOWN 并继续。**

## Step 7：测试基础设施识别

查找（只检查存在性）：
- `tests/` / `test/` / `__tests__/` / `spec/` 目录
- 测试配置文件：`pytest.ini` / `jest.config.*` / `vitest.config.*` / `Makefile` 中的 test target 等
- 推断测试框架和推荐测试命令

## Step 8：模块边界识别

扫描主要源代码目录，识别：
- 主要模块/包目录
- 每个模块的推断职责（从目录名和文件名推断）
- 模块间可见的依赖关系（从 import/include 语句推断）
- 是否存在明显的循环依赖风险

## Step 9：文档入口识别

查找：
- `README.md`
- `docs/` 下的文件列表
- `CONTRIBUTING.md` / `CHANGELOG.md` / `ARCHITECTURE.md`
- API 文档位置（如有）

## Step 10：安全边界识别

识别项目的安全关注点（只读，不改文件）：
- 是否有 auth / authentication / authorization 相关模块？
- 是否有加密/解密相关代码？
- 是否处理用户数据（PII）？
- 是否调用外部 API？
- 是否有 rate limiting / input validation 机制？

## Step 11：输出「我理解的项目地图」

基于以上扫描，输出结构化项目地图：

```
项目名称：[从 README 或目录名推断]
技术栈：[语言、框架、主要依赖]
项目规模：[大致文件数、模块数]

Git 状态：
  分支：[当前分支]
  Ahead/Behind：[与 remote 的关系]
  未提交变更：[有/无]

模块结构：
  [module-1] —— [推断职责]
  [module-2] —— [推断职责]
  ...

规则文件：
  AGENTS.md —— [存在/不存在]
  CLAUDE.md —— [存在/不存在]
  README.md —— [存在/不存在]

测试基础设施：
  框架：[推断的测试框架]
  运行命令：[推断的测试命令]
  覆盖情况：[有/无]

敏感文件：已发现 [N] 个，均未读取内容

安全关注点：
  - [关注点 1]
  - [关注点 2]

文档入口：
  - [入口 1]
  - [入口 2]
```

## Step 12：输出「建议下一步」

基于项目地图，给出 3-5 条建议的下一步动作，例如：
- 「项目规则文件已就绪，可以直接按需求开始工作」
- 「AGENTS.md 不存在，建议先创建项目级规则文件」
- 「缺少明确的测试命令，建议先确认如何运行测试」
- 「发现大量未提交变更，建议先确认当前工作状态」
- 「检测到 [技术栈]，建议加载对应语言规则」

## 停止条件

以下任一情况**必须停止并 Ask User**，不得继续后续步骤：
1. 当前路径不符合用户描述的项目路径
2. Git 状态异常（detached HEAD、merge conflict、rebase in progress）
3. 需要读取敏感文件内容才能继续判断（标记 UNKNOWN，不要读）
4. 项目规则（AGENTS.md / CLAUDE.md）与用户指令明显冲突
5. 项目结构完全不匹配用户描述的技术栈或项目类型

---

## 使用提醒

- 这是**执行型接入审计**，不是 `common/context-brief.md` 的问答式上下文简报
- 接入完成后，后续会话用 `common/context-brief.md` 维护上下文即可
- **全程只读**：不改文件、不 commit、不 push、不 tag
- 不绑定具体项目名——所有项目名用占位符 `[your-project]` 表达
- 如果项目已有 AGENTS.md 且规则清晰，后续会话不需要重复此流程
