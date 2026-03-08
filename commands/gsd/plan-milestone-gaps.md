---
name: gsd:plan-milestone-gaps
description: 为里程碑审计识别出的全部缺口创建修复阶段
allowed-tools:
  - Read
  - Write
  - Bash
  - Glob
  - Grep
  - AskUserQuestion
---
<objective>
创建关闭 `/gsd:audit-milestone` 所识别全部缺口所需的阶段。

读取 `MILESTONE-AUDIT.md`，把缺口按逻辑分组为多个阶段，在 `ROADMAP.md` 中创建阶段条目，并提供逐个规划这些阶段的选项。

一次命令即可创建全部修复阶段，无需按缺口逐个手动执行 `/gsd:add-phase`。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/plan-milestone-gaps.md
</execution_context>

<context>
**Audit results:**
Glob: .planning/v*-MILESTONE-AUDIT.md (use most recent)

Original intent and current planning state are loaded on demand inside the workflow.
</context>

<process>
端到端执行 `@~/.claude/get-shit-done/workflows/plan-milestone-gaps.md` 中的 `plan-milestone-gaps` 工作流。
保留全部工作流关卡（审计加载、优先级排序、阶段分组、用户确认、路线图更新）。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
