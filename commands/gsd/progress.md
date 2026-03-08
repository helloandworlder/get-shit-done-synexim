---
name: gsd:progress
description: 检查项目进度、展示上下文，并路由到下一步动作（执行或规划）
allowed-tools:
  - Read
  - Bash
  - Grep
  - Glob
  - SlashCommand
---
<objective>
检查项目进度，概述最近完成的工作与接下来要做的事，并智能路由到下一步动作——执行已有计划或创建下一个计划。

在继续工作前提供清晰的整体态势感知。
</objective>

<execution_context>
@~/.claude/get-shit-done/workflows/progress.md
</execution_context>

<process>
端到端执行 `@~/.claude/get-shit-done/workflows/progress.md` 中的 `progress` 工作流。
保留全部路由逻辑（Route A 到 F）以及边界情况处理。

完成任何文档编写或实现步骤后，补充输出一个中文进度卡式总结（聚焦产物、状态、下一步）。
</process>
