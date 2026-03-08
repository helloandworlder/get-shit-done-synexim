---
name: gsd:new-milestone
description: 开启新的里程碑周期——更新 `PROJECT.md` 并进入需求流程
argument-hint: "[milestone name, e.g., 'v1.1 Notifications']"
allowed-tools:
  - Read
  - Write
  - Bash
  - Task
  - AskUserQuestion
---
<objective>
开启新的里程碑：提问澄清 → 研究（可选）→ 需求定义 → 路线图。

它是 `new-project` 在存量项目中的对应流程。项目已存在，`PROJECT.md` 保留历史；该命令会收集“下一步做什么”，更新 `PROJECT.md`，然后继续执行需求与路线图流程。

**会创建/更新：**
- `.planning/PROJECT.md` — updated with new milestone goals
- `.planning/research/` — domain research (optional, NEW features only)
- `.planning/REQUIREMENTS.md` — scoped requirements for this milestone
- `.planning/ROADMAP.md` — phase structure (continues numbering)
- `.planning/STATE.md` — reset for new milestone

**完成后：** 运行 `/gsd:plan-phase [N]` 开始执行。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/new-milestone.md
@~/.claude/get-shit-done/references/questioning.md
@~/.claude/get-shit-done/references/ui-brand.md
@~/.claude/get-shit-done/templates/project.md
@~/.claude/get-shit-done/templates/requirements.md
</execution_context>

<context>
里程碑名称：`$ARGUMENTS`（可选；如未提供会继续询问）

项目与里程碑上下文文件会在工作流内部通过 `init new-milestone` 解析，并在使用子代理时通过 `<files_to_read>` 区块传递。
</context>

<process>
端到端执行 `@~/.claude/get-shit-done/workflows/new-milestone.md` 中的 `new-milestone` 工作流。
保留全部工作流关卡（校验、提问、研究、需求、路线图确认、提交）。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
