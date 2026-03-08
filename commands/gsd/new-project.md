---
name: gsd:new-project
description: 通过深度上下文收集与 `PROJECT.md` 初始化新项目
argument-hint: "[--auto]"
allowed-tools:
  - Read
  - Bash
  - Write
  - Task
  - AskUserQuestion
---
<context>
**标志：**
- `--auto` — 自动模式。完成配置问题后，会无额外交互地依次执行研究 → 需求 → 路线图；预期通过 `@` 引用提供想法文档。
</context>

<objective>
通过统一流程初始化新项目：提问澄清 → 研究（可选）→ 需求定义 → 路线图。

**会创建：**
- `.planning/PROJECT.md` — project context
- `.planning/config.json` — workflow preferences
- `.planning/research/` — domain research (optional)
- `.planning/REQUIREMENTS.md` — scoped requirements
- `.planning/ROADMAP.md` — phase structure
- `.planning/STATE.md` — project memory

**执行完本命令后：** 运行 `/gsd:plan-phase 1` 开始执行。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/new-project.md
@~/.claude/get-shit-done/references/questioning.md
@~/.claude/get-shit-done/references/ui-brand.md
@~/.claude/get-shit-done/templates/project.md
@~/.claude/get-shit-done/templates/requirements.md
</execution_context>

<process>
端到端执行 `@~/.claude/get-shit-done/workflows/new-project.md` 中的 `new-project` 工作流。
保留全部工作流关卡（校验、审批、提交、路由）。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
